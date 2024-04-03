---
title: Gerenciamento de configuração de armazenamento
description: Saiba como gerenciar e sincronizar configurações de armazenamento em todos os ambientes de infraestrutura em nuvem do Adobe Commerce.
feature: Cloud, Configuration, SCD
exl-id: f2dd876d-24ee-4d47-b9ac-44fcf77b61b5
source-git-commit: 13e76d3e9829155995acbb72d947be3041579298
workflow-type: tm+mt
source-wordcount: '1439'
ht-degree: 0%

---

# Gerenciamento de configuração de armazenamento

As configurações padrão da loja são armazenadas em um `config.xml` para o módulo apropriado. Quando você altera as configurações no Commerce Admin ou na CLI `bin/magento config:set` as alterações são refletidas no banco de dados principal, especificamente no `core_config_data` tabela. Essas configurações substituem as configurações padrão armazenadas no `config.xml` arquivo.

Configurações de armazenamento, que se referem às configurações no Administrador **Lojas** > **Configurações** > **Configuração** são armazenados nos arquivos de configuração de implantação com base no tipo de configuração:

- `app/etc/config.php`— configurações para lojas, sites, módulos ou extensões, otimização de arquivos estáticos e valores do sistema relacionados à implantação de conteúdo estático. Consulte a [referência config.php](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/files/config-reference-configphp.html) no _Guia de configuração_.
- `app/etc/env.php`—valores para substituições específicas do sistema e configurações confidenciais que devem _NOT_ ser armazenado no controle de origem. Consulte a [referência env.php](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/files/config-reference-envphp.html) no _Guia de configuração_.

>[!NOTE]
>
>Como o Adobe Commerce na infraestrutura em nuvem oferece suporte apenas aos modos de produção e manutenção, o **Avançado** > **Desenvolvedor** seção não está acessível no Administrador. Você deve ter [Privilégios de administrador do ambiente](../project/user-access.md) para concluir tarefas de gerenciamento de configuração. É possível definir configurações adicionais usando [variáveis de ambiente](../environment/configure-env-yaml.md).

O gerenciamento de configurações fornece uma maneira de implantar configurações de armazenamento consistentes em seus ambientes com tempo de inatividade mínimo usando a implantação de pipeline. O projeto de infraestrutura do Adobe Commerce na nuvem inclui o servidor de criação, scripts de criação e implantação e ambientes de implantação criados com o [estratégia de implantação do pipeline](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/deployment/technical-details.html) em mente.

## Esquema de substituição de configuração

Todas as configurações do sistema são definidas durante as fases de criação e implantação de acordo com o seguinte esquema de substituição:

1. Se uma variável de ambiente existir, use a configuração personalizada e ignore a configuração padrão.
1. Se uma variável de ambiente não existir, use a configuração de um `MAGENTO_CLOUD_RELATIONSHIPS` par nome-valor na variável [`.magento.app.yaml` arquivo](../application/configure-app-yaml.md). Ignorar a configuração padrão.
1. Se uma variável de ambiente não existir e `MAGENTO_CLOUD_RELATIONSHIPS` não contém um par nome-valor, remove todas as configurações personalizadas e usa os valores da configuração padrão.

Em resumo, as variáveis de ambiente substituem todos os outros valores.

>[!TIP]
>
>Consulte [Gerenciamento de configuração](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/deployment/technical-details.html) no _Guia de configuração_ para obter mais informações sobre o esquema de substituição para implantação de pipeline.

Se a mesma configuração for definida em vários locais, a aplicação dependerá da seguinte hierarquia de configuração para determinar qual valor aplicar ao ambiente:

| Prioridade | Configuração<br>Método | Descrição |
| -------- | ------------------------ | ----------- |
| 1 | [!DNL Cloud Console]<br>variáveis de ambiente | Valores adicionados do _Variáveis_ guia da configuração de ambiente na guia [!DNL Cloud Console]. Especifique valores aqui para configurações confidenciais ou específicas do ambiente. As configurações especificadas aqui não podem ser editadas no Administrador. Consulte [Variáveis de configuração de ambiente](../project/overview.md#configure-environment). |
| 2 | `.magento.app.yaml` | Valores adicionados na variável `variables` seção do `.magento.app.yaml` arquivo. Especifique valores aqui para garantir uma configuração consistente em todos os ambientes. **Não especifique valores confidenciais na variável `.magento.app.yaml` arquivo.** Consulte [Configurações do aplicativo](../application/configure-app-yaml.md). |
| 3 | `app/etc/env.php` | Os valores de configuração específicos do ambiente armazenados aqui são adicionados usando o `app:config:dump` comando. Defina os valores específicos do sistema e confidenciais usando variáveis de ambiente ou a CLI. Consulte [Dados sensíveis](#sensitive-data). A variável `env.php` o arquivo é **não** incluído no controle de origem. |
| 4 | `app/etc/config.php` | Os valores armazenados aqui são adicionados usando o `app:config:dump` comando. Os valores de configuração compartilhados são adicionados ao `config.php`. Defina a configuração compartilhada pelo Admin ou usando a CLI. A variável `config.php` o arquivo está incluído no controle do código-fonte. |
| 5 | Banco de dados | Os valores armazenados aqui são adicionados definindo configurações no Administrador. As configurações definidas usando qualquer um dos métodos anteriores são bloqueadas (esmaecidas) e não podem ser editadas pelo administrador. |
| 6 | `config.xml` | Muitas configurações têm valores padrão definidos no `config.xml` para um módulo. Se o Adobe Commerce não conseguir encontrar nenhum valor definido por nenhum dos métodos anteriores, ele voltará ao valor padrão, se definido. |

{style="table-layout:auto"}

## Despejo de configuração

Você pode usar o seguinte `ece-tools` comando para gerar um `config.php` arquivo que contém todas as configurações de armazenamento atuais:

```bash
./vendor/bin/ece-tools config:dump
```

Os dados &quot;despejados&quot; no `app/etc/config.php` arquivo torna-se _bloqueado_, o que significa que o campo correspondente no Administrador do Commerce se torna **somente leitura**. A variável `config.php` O arquivo inclui somente as configurações definidas por você. Ela não bloqueia os valores padrão. Bloquear apenas os valores atualizados também garante que todas as extensões usadas nos ambientes de Preparo e Produção não sejam interrompidas devido a configurações somente leitura, especialmente o Fastly.

>[!WARNING]
>
>A variável `ece-tools config:dump` não recupera configurações detalhadas para módulos, como B2B. Se precisar de um despejo de configuração abrangente, use o `app:config:dump` , mas esse comando bloqueia os valores de configuração em um estado somente leitura.

### Dados sensíveis

Todas as configurações confidenciais são exportadas para o `app/etc/env.php` arquivo ao usar o `bin/magento app:config:dump` comando. Você pode definir valores confidenciais usando o comando da CLI: `bin/magento config:sensitive:set`. Consulte  [Configurações sensíveis e específicas do ambiente](https://developer.adobe.com/commerce/php/development/configuration/sensitive-environment-settings/) no _Extensões PHP do Commerce_ guia para saber como designar definições de configuração como confidenciais ou específicas do sistema.

Veja uma lista de [Configurações sensíveis ou específicas do sistema](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/paths/config-reference-sens.html) no _Guia de configuração_.

### Desempenho do SCD

Dependendo do tamanho do armazenamento, você pode ter um grande número de arquivos de conteúdo estático para implantar. Normalmente, o conteúdo estático é implantado durante a fase de implantação, quando o aplicativo está no modo de manutenção. A configuração mais ideal é gerar conteúdo estático durante a fase de criação. Consulte [Escolha de uma estratégia de implantação](../deploy/static-content.md).

Se você tiver ativado o Gerenciamento de configurações após despejar as configurações, mova as variáveis SCD_* do estágio de implantação para o estágio de criação para ativar adequadamente a geração de conteúdo estático durante a fase de criação. Consulte [Variáveis de ambiente](../environment/configure-env-yaml.md#environment-variables).

**Antes do gerenciamento de configuração**:

```yaml
  deploy:
    CRON_CONSUMERS_RUNNER:
      cron_run: true
      consumers: []
    SCD_STRATEGY: compact
    SCD_MATRIX:
      ...
    REDIS_USE_SLAVE_CONNECTION: 1
```

**Depois de habilitar o Gerenciamento de configuração**:

Mova as variáveis SCD_* para o estágio de criação:

```yaml
  deploy:
    CRON_CONSUMERS_RUNNER:
      cron_run: true
      consumers: []
    REDIS_USE_SLAVE_CONNECTION: 1
  build:
    SCD_STRATEGY: compact
    SCD_MATRIX:
      ...
```

>[!NOTE]
>
>Antes de implantar arquivos estáticos, as fases de criação e implantação compactam o conteúdo estático usando GZIP. A compactação de arquivos estáticos reduz as cargas do servidor e aumenta o desempenho do site. Consulte [opções de build](../environment/variables-build.md) para saber mais sobre como personalizar ou desativar a compactação de arquivos.

## Procedimento para gerenciar suas configurações

A seguir, uma visão geral de alto nível desse processo:

![Visão geral do gerenciamento de configuração do Starter](../../assets/starter/configuration-management-flow.png)

**Para configurar sua loja e gerar um arquivo de configuração**:

1. Conclua todas as configurações das lojas no Administrador para um dos ambientes:

   - Início: uma ramificação de desenvolvimento ativa
   - Pro: uma filial ativa no ambiente de integração

   Essas configurações não incluem os produtos reais, a menos que você planeje despejar o banco de dados desse ambiente para ambientes de preparo e produção. Normalmente, os bancos de dados de desenvolvimento não incluem os dados completos da loja.

1. Na estação de trabalho local, altere para o diretório do projeto.

1. Criar um dump local do banco de dados remoto.

   ```bash
   magento-cloud db:dump
   ```

1. Adicionar, confirmar e enviar alterações de código para atualizar um ambiente remoto.

   ```bash
   git add app/etc/config.php
   ```

   ```bash
   git commit -m "Add system-specific configuration"
   ```

   ```bash
   git push origin <branch-name>
   ```

Depois que a implantação for concluída, faça logon no Admin do ambiente atualizado para verificar as configurações. Continue a mesclar todas as configurações adicionais com os ambientes de preparo e produção, conforme necessário.

### Atualizar configurações

Quando você modifica seu ambiente por meio do Administrador e executa o comando novamente, novas configurações são anexadas ao código no `config.php` arquivo.

>[!WARNING]
>
>Embora seja possível editar manualmente a variável `config.php` nos ambientes de armazenamento temporário e produção, é **não** recomendado. O arquivo ajuda a manter todas as configurações consistentes em todos os ambientes. Nunca exclua o `config.php` arquivo para recriá-lo. A exclusão do arquivo pode remover configurações específicas necessárias para processos de compilação e implantação.

### Restaurar arquivos de configuração

Cópias do original `app/etc/env.php` e `app/etc/config.php` os arquivos foram criados durante o processo de implantação e armazenados na mesma pasta. O exemplo a seguir mostra o BAK (arquivos de backup) e o PHP (arquivos originais) na mesma `app/etc` pasta:

```terminal
...
config.php.bak
di.xml
env.php.bak
vendor_path.php
config.php
db_schema.xml
env.php
...
```

As configurações mais antigas usavam o `app/etc/config.local.php` arquivo. Consulte [Migrar configurações mais antigas](#migrate-older-configurations).

**Para restaurar arquivos de configuração**:

1. Na estação de trabalho local, use o SSH para fazer logon no projeto e no ambiente remotos.

   ```bash
   magento-cloud ssh
   ```

1. Verifique o local e a disponibilidade dos arquivos de backup.

   ```bash
   ./vendor/bin/ece-tools backup:list
   ```

   Exemplo de resposta:

   ```terminal
   The list of backup files:
   app/etc/env.php
   app/etc/config.php
   ```

1. Restaurar arquivos de backup.

   ```bash
   ./vendor/bin/ece-tools backup:restore
   ```

### Migrar configurações mais antigas

Se você atualizar para o Adobe Commerce na infraestrutura em nuvem 2.2 ou posterior, convém migrar as configurações do `config.local.php` arquivo para o novo `config.php` arquivo. Se as configurações no Administrador corresponderem ao conteúdo do arquivo, siga as instruções para gerar e adicionar o `config.php` arquivo.

Se forem diferentes, é possível anexar conteúdo do `config.local.php` arquivo para o novo `config.php` arquivo:

1. Siga as instruções para gerar o `config.php` arquivo.

1. Abra o `config.php` e exclua a última linha.

1. Abra o `config.local.php` arquivo e copie o conteúdo.

1. Cole o conteúdo na `config.php` arquivo, salve e conclua a adição ao Git.

1. Implante em seus ambientes.

Você só conclui essa migração uma vez. Após a migração, use o `config.php` arquivo.

### Alterar localidades

Você pode alterar as localidades da loja sem seguir um processo complexo de importação e exportação de configuração, _se_ você tem [SCD_ON_DEMAND](../environment/variables-global.md#scd_on_demand) ativado. Você pode atualizar as localidades usando o Administrador.

Você pode adicionar outro local ao ambiente de preparo ou produção ativando `SCD_ON_DEMAND` em uma ramificação de integração, gere uma atualização `config.php` com as novas informações de local e copie o arquivo de configuração no ambiente de destino.

>[!WARNING]
>
>Este processo **substitui** a configuração da loja; faça o seguinte somente se os ambientes contiverem as mesmas lojas.

1. No ambiente de integração, habilite a opção `SCD_ON_DEMAND` usando o [`.magento.env.yaml` arquivo](../environment/configure-env-yaml.md).

1. Adicione os locais necessários usando o Administrador.

1. Use o SSH para fazer logon no ambiente remoto e gerar o `/app/etc/config.php` arquivo contendo todas as localidades.

   ```bash
   ssh <SSH-URL> "./vendor/bin/ece-tools config:dump"
   ```

1. Copie o novo arquivo de configuração do ambiente de integração remota para o diretório do ambiente local.

   ```bash
   rsync <SSH-URL>:app/etc/config.php ./app/etc/config.php
   ```

1. Adicionar, confirmar e enviar alterações de código para atualizar um ambiente remoto.
