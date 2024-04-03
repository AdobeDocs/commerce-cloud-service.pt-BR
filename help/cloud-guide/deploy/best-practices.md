---
title: Práticas recomendadas de implantação
description: Descubra as práticas recomendadas para implantar o Adobe Commerce na infraestrutura em nuvem.
feature: Cloud, Deploy, Best Practices
exl-id: bac3ca83-0eee-4fda-9a5c-a84ab25a837a
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '1904'
ht-degree: 0%

---

# Práticas recomendadas de implantação

Os scripts de criação e implantação são ativados quando você mescla códigos em um ambiente remoto. Esses scripts usam o ambiente [arquivos de configuração](../environment/overview.md) e o código do aplicativo para provisionar a infraestrutura em nuvem com dados e serviços adequados. Além disso, esses scripts são usados para instalar ou atualizar o aplicativo do Adobe Commerce, serviços de terceiros e extensões personalizadas no ambiente de nuvem.

O processo de criação e implantação é um pouco diferente para cada plano:

- **Planos iniciais**— para o ambiente de integração, cada ramificação ativa cria e implanta em um ambiente completo para acesso e testes. Teste completamente seu código depois de mesclar com a `staging` filial. Para iniciar seu site, envie por push `staging` para `master` para implantar no ambiente de produção. Você tem acesso total a todas as ramificações por meio do [!DNL Cloud Console] e os comandos da CLI.

- **Planos profissionais**— para o ambiente de integração, cada ramificação ativa cria e implanta em um ambiente completo para acesso e testes. Mescle seu código com a `integration` antes de mesclar com os ambientes de preparo e produção. É possível mesclar os ambientes de armazenamento temporário e produção usando o [!DNL Cloud Console] ou usando SSH e `magento-cloud` Comandos da CLI.

## Rastrear o processo

Você pode rastrear ações de criação e implantação em tempo real usando o terminal ou o [!DNL Cloud Console] Mensagens de status—`in-progress`, `pending`, `success`ou `failed`—exibir durante o processo de implantação. Você pode exibir detalhes nos arquivos de log. Consulte [Exibir logs](../test/log-locations.md).

Se você estiver usando repositórios GitHub externos, o log de operações não será exibido na sessão do GitHub. No entanto, ainda é possível seguir as atividades na interface para o repositório externo e a [!DNL Cloud Console]. Consulte [Integrações](../integrations/overview.md).

>[!NOTE]
>
>Em ambientes de integração, não é possível visualizar os logs de implantação do [!DNL Cloud Console]. Esse recurso está disponível somente para ambientes de produção e de preparo. No entanto, você pode visualizar logs para cada fase da implantação em qualquer ambiente usando o [criar e implantar](../test/log-locations.md#build-and-deploy-logs) logs. Para obter informações sobre solução de problemas, consulte [Referência de erro de implantação](../dev-tools/error-reference.md).

Você pode ativar [Rastrear implantações com o New Relic](../monitor/track-deployments.md) para monitorar eventos de implantação e analisar o desempenho entre implantações.

## Práticas recomendadas para builds e implantação

Revise estas práticas recomendadas e considerações para seu processo de implantação:

- **Verifique se você está executando a versão mais recente do `ece-tools` pacote**

  Consulte [Notas de versão de ECE-Tools](../release-notes/ece-tools-package.md).

- **Siga o processo de criação e implantação**

  Verifique se você tem o código correto em cada ambiente para evitar a substituição de configurações ao mesclar código entre ambientes. Por exemplo, para aplicar alterações de configuração a todos os ambientes, modifique e teste as alterações no ambiente local antes de implantar no ambiente de integração remota. Em seguida, implante e teste as alterações no ambiente de preparo antes de implantar na produção. Quando você mescla de um ambiente para outro, a implantação substitui todo o código no ambiente, exceto as configurações específicas do ambiente.

- **Usar as mesmas variáveis em ambientes**

  Os valores dessas variáveis podem diferir entre os ambientes; no entanto, normalmente são necessárias as mesmas variáveis em cada ambiente. Consulte [Gerenciamento de configurações para configurações de armazenamento](../store/store-settings.md).

- **Manter valores e dados confidenciais de configuração em variáveis específicas do ambiente**

  Esses valores incluem variáveis especificadas com o uso da CLI da nuvem, a variável [!DNL Cloud Console]ou adicionado à `env.php` arquivo. Consulte [Níveis variáveis](../environment/variable-levels.md).

- **Garantir que todo o código esteja disponível na ramificação do ambiente**

  Fazer referência ao código de outras ramificações, como uma ramificação privada, pode causar problemas durante o processo de compilação e implantação. Por exemplo, se você fizer referência a um tema de uma ramificação privada, ele não estará acessível e não poderá ser criado com o código do aplicativo.

- **Adicionar extensões, integrações e código em ramificações iteradas**

  Faça e teste as alterações localmente, envie para `integration`, depois para `staging` e `production`. Teste e resolva os problemas em cada ambiente antes de mesclar as atualizações com o próximo ambiente. Algumas extensões e integrações devem ser ativadas e configuradas em uma ordem específica devido às dependências. Adicionar e testar em grupos pode tornar o processo de criação e implantação muito mais fácil e ajudar a determinar onde ocorrem problemas.

- **Verificar versões e relações do serviço e a capacidade de conexão**

  Verifique os serviços disponíveis para seu aplicativo e certifique-se de que você esteja usando a versão mais atual e compatível. Consulte [Relacionamentos de serviço](../services/services-yaml.md#service-relationships) e [Requisitos do sistema](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/system-requirements.html) no _Guia de instalação_ para versões recomendadas.

- **Testar localmente e no ambiente de integração antes de implantar no ambiente de preparo e produção**

  Identifique e corrija problemas em seus ambientes locais e de integração para evitar um tempo de inatividade prolongado ao implantar em ambientes de preparo e produção.

  >[!TIP]
  >
  >Há [assistente inteligente](../deploy/smart-wizards.md) comandos que podem ser usados para verificar se a configuração do projeto na nuvem segue as práticas recomendadas para a configuração de criação e implantação, incluindo a estratégia de implantação de conteúdo estático (SCD).

- **Após concluir os testes em ambientes locais e de integração, implante e teste no ambiente de preparo**

  Consulte [Teste de preparo e produção](../test/staging-and-production.md).

- **Verificar a configuração do ambiente de produção**

  Antes de implantar na produção, conclua as seguintes tarefas:

   - Verifique se você pode se conectar a todos os três nós no ambiente de produção usando [SSH](../development/secure-connections.md).

   - Verifique se os Indexadores estão definidos como _Atualização programada_. Consulte [Modos de indexação](https://developer.adobe.com/commerce/php/development/components/indexing/) no _Guia do desenvolvedor de extensões_.

   - Prepare o ambiente atualizando quaisquer variáveis específicas do ambiente no código de Produção, verificando a disponibilidade e a compatibilidade do serviço e fazendo quaisquer outras alterações de configuração necessárias.

- **Monitorar o processo de implantação**

  Revise as mensagens de status da implantação e reduza os problemas conforme necessário. Revise a nuvem [logs](../test/log-locations.md#) para obter mensagens de log detalhadas.

## Cinco fases de criação e implantação da integração

As fases a seguir ocorrem no ambiente de desenvolvimento local e no ambiente de integração. Para planos Pro, o código não é implantado nos ambientes de armazenamento temporário ou produção nessas fases iniciais.

### Fase 1: validação de código e configuração

Ao configurar inicialmente um projeto, [o modelo de infraestrutura em nuvem](https://github.com/magento/magento-cloud) O fornece uma base para os arquivos de código. Esse código de repositório é clonado para seu projeto como o `master` filial.

- **Para começar**—`master` A ramificação é o seu ambiente de produção.
- **Para Pro**—`master` começa como a ramificação de origem do ambiente de integração.

Criar uma ramificação de `master` para seu código personalizado, extensões e módulos do e integrações de terceiros. Há um ambiente de integração remota para testar seu código na nuvem.

Quando você envia seu código do espaço de trabalho local para o repositório remoto, uma série de verificações e validações de código é concluída antes do início da criação e implantação dos scripts. O servidor Git integrado valida o que você está enviando e faz alterações. Por exemplo, se você adicionar um serviço OpenSearch, o servidor Git integrado verificará se a topologia do cluster foi modificada adequadamente.

Se você tiver um erro de sintaxe em um arquivo de configuração, o servidor Git rejeitará o push. Consulte [Bloqueio de proteção](../development/protective-block.md).

Essa fase também é executada `composer install` para recuperar dependências.

### Fase 2: criação

>[!NOTE]
>
>Durante a fase de criação, o site não está no modo de manutenção e se ocorrerem erros ou problemas não será desativado. Ele cria apenas o código que foi alterado desde a build anterior.

Essa fase cria a base de código e executa ganchos no `build` seção de `.magento.app.yaml`. O gancho de criação padrão é o `php ./vendor/bin/ece-tools` e executa o seguinte:

- Aplica patches em `vendor/magento/ece-patches`e patches opcionais específicos do projeto no `m2-hotfixes`
- Regenera o código e o [injeção de dependência](https://experienceleague.adobe.com/docs/commerce-operations/operational-playbook/glossary.html) configuração (ou seja, a variável `generated/` diretório, que inclui `generated/code` e `generated/metapackage`) usando `bin/magento setup:di:compile`.
- Verifica se [`app/etc/config.php`](../store/store-settings.md) arquivo existe na base de código. O Adobe Commerce gera automaticamente esse arquivo se ele não for detectado durante a fase de criação e incluir uma lista de módulos e extensões. Se existir, a fase de criação continua normalmente, compacta arquivos estáticos usando GZIP e implanta, o que reduz o tempo de inatividade na fase de implantação. Consulte [opções de build](../environment/variables-build.md) para saber mais sobre como personalizar ou desativar a compactação de arquivos.

>[!WARNING]
>
>Neste ponto, o cluster não foi criado, portanto, não tente se conectar a um banco de dados ou suponha que haja um processo de daemon ativo.

Depois que o aplicativo for criado, ele será montado em um **sistema de arquivos somente leitura**. Você pode configurar pontos de montagem específicos que serão de leitura/gravação. Não é possível transferir um FTP para o servidor e adicionar módulos. Em vez disso, você deve adicionar o código ao repositório local e executar `git push`, que cria e implanta o ambiente. Para obter a estrutura do projeto, consulte [Estrutura de diretório de projeto local](../project/file-structure.md).

### Fase 3: Preparar a slug

O resultado da fase de criação é um sistema de arquivos somente leitura, conhecido como _slug_. Essa fase cria um arquivamento e coloca o slug em armazenamento permanente. Na próxima vez que você enviar o código, se um serviço não for alterado, ele usará o slug do arquivamento.

- Acelera a integração contínua ao reutilizar o código inalterado
- Se o código for alterado, atualiza a descrição da próxima build a ser reutilizada
- Permite a reversão instantânea de uma implantação, se necessário
- Inclui arquivos estáticos se a variável `app/etc/config.php` arquivo existe na base de código

O slug inclui todos os arquivos e pastas **excluindo o seguinte** montagens configuradas em `magento.app.yaml`:

- `"var": "shared:files/var"`
- `"app/etc": "shared:files/etc"`
- `"pub/media": "shared:files/media"`
- `"pub/static": "shared:files/static"`

### Fase 4: implantação de slugs e cluster

Seus aplicativos e todos [back-end](https://experienceleague.adobe.com/docs/commerce-operations/operational-playbook/glossary.html) prestação de serviços da seguinte forma:

- Monta cada serviço em um contêiner, como servidor Web, OpenSearch, [!DNL RabbitMQ]
- Monta o sistema de arquivos de leitura e gravação (montado em uma grade de armazenamento distribuída altamente disponível)
- Configura a rede para que os serviços possam &quot;ver&quot; uns aos outros (e somente uns aos outros)

>[!NOTE]
>
>Faça as alterações em uma ramificação Git após a conclusão da compilação e da implantação e envie novamente. Todos os sistemas de arquivos do ambiente são _somente leitura_. Um sistema somente leitura garante implantações determinísticas e melhora drasticamente a segurança do site, pois nenhum processo pode gravar no sistema de arquivos. Também funciona para garantir que seu código seja idêntico nos ambientes de integração, preparo e produção.

### Fase 5: Ganchos de implantação

>[!NOTE]
>
>Esta fase coloca a [!DNL Commerce] aplicativo no modo de manutenção até a conclusão da implantação.

A última etapa executa um script de implantação, que pode ser usado para tornar os dados anônimos em ambientes de desenvolvimento, limpar caches e consultar ferramentas de integração contínua externa. Quando esse script é executado, você tem acesso a todos os serviços em seu ambiente, como o Redis.

Se a variável `app/etc/config.php` arquivo não existe na base de código, os arquivos estáticos são compactados usando `gzip` e implantados durante essa fase, o que aumenta a duração da fase de implantação e da manutenção do site.

>[!NOTE]
>
>Consulte [implantar variáveis](../environment/variables-deploy.md) para saber mais sobre como personalizar ou desativar a compactação de arquivos.

Há dois ganchos de implantação. A variável `pre-deploy.php` o gancho conclui a limpeza e a recuperação necessárias dos recursos e do código gerados no gancho de compilação. A variável `php ./vendor/bin/ece-tools deploy` O hook executa uma série de comandos e scripts:

- Se o Adobe Commerce for **não instalado**, ele é instalado com o `bin/magento setup:install`, atualiza a configuração de implantação, `app/etc/env.php`e o banco de dados para o ambiente especificado, como Redis e URLs de sites. **Importante:** Quando você concluiu o [Primeira implantação](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/launch/overview.html) durante a instalação, o Adobe Commerce foi instalado e implantado em todos os ambientes.

- Se o Adobe Commerce **está instalado**, faça as atualizações necessárias. O script de implantação é executado `bin/magento setup:upgrade` para atualizar o esquema do banco de dados e os dados (que são necessários após a extensão ou atualizações do código principal) e também atualiza a configuração de implantação, `app/etc/env.php`e o banco de dados do seu ambiente. Finalmente, o script de implantação limpa o cache do Adobe Commerce.

- O script gera opcionalmente conteúdo estático da Web usando o comando `magento setup:static-content:deploy`.

- Usa escopos (`-s` sinalizador nos scripts de criação) com uma configuração padrão de `quick` para estratégia de implantação de conteúdo estático. É possível personalizar a estratégia usando a variável de ambiente [`SCD_STRATEGY`](../environment/variables-deploy.md#scd_strategy). Para obter detalhes sobre essas opções e recursos, consulte [Estratégias de implantação de arquivos estáticos](../deploy/static-content.md) e a variável `-s` sinalizador para [Implantar arquivos de exibição estáticos](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/static-view/static-view-file-deployment.html).

>[!NOTE]
>
>O script de implantação usa os valores definidos pelos arquivos de configuração no `.magento` , o script excluirá o diretório e seu conteúdo. O ambiente de desenvolvimento local não é afetado.

### Pós-implantação: configurar roteamento

Enquanto a implantação está em execução, o processo interrompe o tráfego de entrada no ponto de entrada por 60 segundos e reconfigura o roteamento para que o tráfego da Web chegue ao cluster recém-criado.

A implantação bem-sucedida remove o modo de manutenção para permitir o acesso normal e cria arquivos de backup (BAK) para o `app/etc/env.php` e a variável `app/etc/config.php` arquivos de configuração.

Habilitar a geração de conteúdo estático usando o `SCD_ON_DEMAND` e configure a variável [`post_deploy` gancho](../application/hooks-property.md) para que ele limpe o cache e pré-carregue (aquece) o cache _após_ o contêiner começa a aceitar conexões e _durante_ tráfego de entrada normal.

Para revisar os logs de build e implantação, consulte [Exibir logs](../test/log-locations.md#view-and-manage-logs).
