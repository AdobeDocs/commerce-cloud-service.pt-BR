---
title: Variáveis globais
description: Consulte a lista de variáveis de ambiente que controlam ações no processo de implantação do Adobe Commerce na infraestrutura em nuvem.
feature: Cloud, Configuration, Build, Deploy, Eventing, Logs, SCD
recommendations: noDisplay, catalog
role: Developer
exl-id: 04c2861d-746d-42d4-a678-f6c7b464eb51
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '752'
ht-degree: 0%

---

# Variáveis globais

As variáveis globais controlam ações em cada fase do [!DNL Commerce] processo de implantação: criação, implantação e pós-implantação. Como as variáveis globais afetam cada fase, você deve defini-las no `global` fase do `.magento.env.yaml` arquivo:

```yaml
stage:
  global:
    GLOBAL_VARIABLE_NAME: value
```

Para obter mais informações sobre como personalizar o processo de criação e implantação:

- [Configuração de implantação](configure-env-yaml.md)
- [Processo de implantação](../deploy/process.md)

## `ENABLE_EVENTING`

- **Padrão**-_Não definido_
- **Versão**—Adobe Commerce 2.4.5 e posterior

Quando definido como `true`, permite que o cron execute consumidores da fila de mensagens. Os Adobe I/O Eventos para Adobe Commerce usam filas de mensagens para agilizar a entrega de eventos críticos.

A Adobe recomenda que você também adicione a variável [`CRON_CONSUMERS_RUNNER`](./variables-deploy.md#cron_consumers_runner) variável para o `deploy` fase do `.magento.env.yaml` arquivo com `cron_run` definir como `true`.

O exemplo a seguir mostra uma configuração completa `ENABLE_EVENTING` variável.

```yaml
stage:
  global:
    ENABLE_EVENTING: true
  deploy:
    CRON_CONSUMERS_RUNNER:
      cron_run: true
      max_messages: 0
      consumers: []
```

## ENABLE_WEBHOOKS

- **Padrão**-_Não definido_
- **Versão**—Adobe Commerce 2.4.4 e posterior

Quando definido como `true`, ativa webhooks do Commerce. O webhook é executado em um endpoint externo, como uma ação de tempo de execução do App Builder ou um sistema de gerenciamento de inventário de terceiros. A variável [_Guia do Webhooks_](https://developer.adobe.com/commerce/extensibility/webhooks) A descreve esse recurso detalhadamente.

```yaml
stage:
  global:
    ENABLE_WEBHOOKS: true
```

## `MIN_LOGGING_LEVEL`

- **Padrão**—_Não definido_
- **Versão**—Adobe Commerce 2.1.4 e posterior

Substitui o nível mínimo de log para todos os fluxos de saída sem alterar o código, o que ajuda a solucionar problemas com a implantação. Por exemplo, se a implantação falhar, você pode usar essa variável para aumentar a granularidade do registro globalmente. Consulte [Níveis de log](log-handlers.md#log-levels). A variável `min_level` em Manipuladores de registro substitui essa configuração.

```yaml
stage:
  global:
    MIN_LOGGING_LEVEL: debug
```

>[!WARNING]
>
>A configuração da variável `MIN_LOGGING_LEVEL` não altera a configuração do nível de log do manipulador de arquivos, que está definido como `debug` por padrão.

## `SCD_ON_DEMAND`

- **Padrão**—_Não definido_
- **Versão**—Adobe Commerce 2.1.4 e posterior

Ative a geração de conteúdo estático quando solicitado por um usuário (SCD). O conteúdo estático sob demanda é ideal para o fluxo de trabalho de desenvolvimento e teste, pois diminui o tempo de implantação.

Pré-carregamento do cache usando o [`post_deploy` gancho](../application/hooks-property.md) reduz o tempo de inatividade do site. O aquecimento do cache está disponível somente para projetos Pro que contêm ambientes de preparo e produção na [!DNL Cloud Console] e para projetos iniciais. Adicione o `SCD_ON_DEMAND` variável de ambiente para o `global` etapa no `.magento.env.yaml` arquivo:

```yaml
stage:
  global:
    SCD_ON_DEMAND: true
```

A variável `SCD_ON_DEMAND` ignora o SCD em ambas as fases (criação e implantação), limpa a variável `pub/static` e `var/view_preprocessed` pastas e grava o seguinte no `app/etc/env.php` arquivo:

```php?start_inline=1
return array(
   ...
   'static_content_on_demand_in_production' => 1,
   ...
);
```

## `SCD_MAX_EXECUTION_TIME`

- **Padrão**—_Não definido_
- **Versão**—Adobe Commerce 2.2.0 e posterior

Permite aumentar o tempo de execução máximo esperado para implantação de conteúdo estático.

Por padrão, o Adobe Commerce define a execução máxima esperada para 900 segundos, mas em alguns cenários, pode ser necessário mais tempo para concluir a implantação do conteúdo estático para um projeto na nuvem.

```yaml
stage:
  global:
    SCD_MAX_EXECUTION_TIME: 3600
```

{{scd-timing-warning}}

## `SCD_NO_PARENT`

- **Padrão**—_Não definido_
- **Versão**—Adobe Commerce 2.4.2 e posterior

Defina como `true` para evitar a geração de conteúdo estático para temas principais durante as fases de criação e implantação. Quando essa opção estiver definida como `true`No entanto, menos conteúdo estático é gerado, o que melhora os tempos gerais de criação e implantação.

```yaml
stage:
  global:
    SCD_NO_PARENT: true
```

## `SCD_USE_BALER`

- **Padrão**—_Não definido_
- **Versão**—Adobe Commerce 2.3.0 e posterior

[Baler](https://github.com/magento/baler) O é um módulo que verifica o código JavaScript gerado e cria um pacote JavaScript otimizado. Implantar o pacote otimizado em seu site pode reduzir o número de solicitações de rede ao carregar seu site e melhorar o tempo de carregamento da página.

Defina como `true` para executar o Baler após executar a implantação de conteúdo estático.

```yaml
stage:
  build:
    SCD_USE_BALER: true
```

>[!NOTE]
>
>Instale e configure o módulo Baler antes de usar esse recurso. Como o Baler está na versão alfa, ative essa opção somente em ambientes de preparo.

## `SKIP_HTML_MINIFICATION`

- **Padrão**:
   - `true`— for `ece-tools` 2002.0.13 e posterior
   - `false`—para versões anteriores do `ece-tools`
- **Versão**—Adobe Commerce 2.1.4 e posterior

Ativa ou desativa a cópia de arquivos de visualização estáticos para o `<magento_root>/init/` diretório no final da etapa de compilação. Se definida como `true`, os arquivos não são copiados e a minificação de HTML está disponível mediante solicitação. Defina esse valor como `true` para reduzir o tempo de inatividade ao implantar em ambientes de preparo e produção.

- **`false`**—Copia o `view_preprocessed` diretório para o `<magento_root>/init/` diretório no final da fase de criação e restaura o diretório no `<magento_root>/var` diretório no início da fase de implantação.
- **`true`**—Permite a minificação de HTML sob demanda; _não_ copie o `<magento_root>var/view_preprocessed` para o `<magento_root>/init/` diretório no final da fase de compilação.

Adicione o `SKIP_HTML_MINIFICATION` variável de ambiente para o `global` etapa no `.magento.env.yaml` arquivo:

```yaml
stage:
  global:
    SKIP_HTML_MINIFICATION: true
```

## `X_FRAME_CONFIGURATION`

- **Padrão**—_Não definido_
- **Versão**—Adobe Commerce 2.1.4 e posterior

Use o `X_FRAME_CONFIGURATION` para alterar a variável [`X-Frame-Options`](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/security/xframe-options.html) configuração do cabeçalho para o site do Adobe Commerce. Essa configuração controla como o navegador renderiza uma página em um `<frame>`, `<iframe>`ou `<object>`. Use uma das seguintes opções:

- `DENY`—A página não pode ser exibida em um quadro.
- `SAMEORIGIN`—(A configuração padrão do Adobe Commerce.) A página pode ser exibida somente em um quadro na mesma origem da própria página.

>[!WARNING]
>
>A variável `ALLOW-FROM <uri>` A opção foi descontinuada porque os navegadores compatíveis com o Adobe Commerce não são mais compatíveis com ela. Consulte [Compatibilidade do navegador](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/X-Frame-Options#Browser_compatibility).

Adicione o `X_FRAME_CONFIGURATION` variável de ambiente para o `global` etapa no `.magento.env.yaml` arquivo:

```yaml
stage:
  global:
    X_FRAME_CONFIGURATION: SAMEORIGIN
```
