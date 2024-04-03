---
title: Propriedades
description: Use a lista de propriedades como referência ao configurar o [!DNL Commerce] aplicativo para criação e implantação na infraestrutura em nuvem.
feature: Cloud, Configuration, Build, Deploy, Roles/Permissions, Storage
exl-id: 58a86136-a9f9-4519-af27-2f8fa4018038
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '797'
ht-degree: 0%

---

# Propriedades para configuração de aplicativo

A variável `.magento.app.yaml` O arquivo usa propriedades para gerenciar o suporte ao ambiente para o [!DNL Commerce] aplicação.

| Nome | Descrição | Padrão | Obrigatório |
| ------ | --------------------------------- | ------- | -------- |
| [`access`](#access) | Personalizar funções de usuário | — | Não |
| [`crons`](crons-property.md) | Atualizar especificações e agendar trabalhos cron | — | Não |
| [`dependencies`](#dependencies) | Habilitar dependências adicionais | `php:composer/composer: '2.2.4'` | Não |
| [`disk`](#disk) | Definir o tamanho do disco persistente | `5120` | Sim |
| [`firewall`](firewall-property.md) | (Somente iniciador) Controlar tráfego de saída | — | Não |
| [`hooks`](hooks-property.md) | Personalizar comandos do shell para as fases de criação, implantação e pós-implantação | — | Não |
| [`mounts`](#mounts) | Definir caminhos | Caminhos:<ul><li>`"var": "shared:files/var"`</li><li>`"app/etc": "shared:files/etc"`</li><li>`"pub/media": "shared:files/media"`</li><li>`"pub/static": "shared:files/static"`</li></ul> | Não |
| [`name`](#name) | Definir o nome do aplicativo | `mymagento` | Sim |
| [`relationships`](#relationships) | Serviços de mapa | Serviços:<ul><li>`database: "mysql:mysql"`</li><li>`redis: "redis:redis"`</li><li>`opensearch: "opensearch:opensearch"`</li></ul> | Não |
| [`runtime`](#runtime) | A propriedade de tempo de execução inclui extensões exigidas pelo [!DNL Commerce] aplicação. | Extensões:<ul><li>`xsl`</li><li>`newrelic`</li><li>`sodium`</li></ul> | Sim |
| [`type`](#type-and-build) | Definir a imagem base do contêiner | `php:8.1` | Sim |
| [`variables`](variables-property.md) | Aplicação de uma variável de ambiente para uma versão específica do Commerce | — | Não |
| [`web`](web-property.md) | Lidar com solicitações externas | — | Sim |
| [`workers`](workers-property.md) | Lidar com solicitações externas | — | Sim, se não estiver usando a propriedade da Web |

{style="table-layout:auto"}

## `name`

A variável `name` fornece o nome do aplicativo usado na variável [`routes.yaml`](../routes/routes-yaml.md) arquivo para definir o upstream de HTTP (por padrão, `mymagento:http`). Por exemplo, se o valor de `name` é `app`, você deve usar `app:http` no campo upstream.

>[!WARNING]
>
>Não altere o nome do aplicativo após sua implantação. Isso resulta em perda de dados.

## `type` e `build`

A variável `type`  e `build` as propriedades fornecem informações sobre a imagem base do contêiner para construir e executar o projeto.

O compatível `type` a linguagem é PHP. Especifique a versão do PHP da seguinte maneira:

```yaml
type: php:<version>
```

A variável `build` determina o que acontece por padrão ao criar o projeto. A variável `flavor` especifica um conjunto padrão de tarefas de compilação a serem executadas. O exemplo a seguir mostra a configuração padrão para `type` e `build` de `magento-cloud/.magento.app.yaml`:

```yaml
# The toolstack used to build the application.
type: php:8.1
build:
    flavor: none

dependencies:
    php:
        composer/composer: '2.2.4'
```

### Instalação e uso do Composer 2

A variável `build: flavor:` A propriedade não é usada para o Composer 2.x; portanto, você deve instalar o Composer manualmente durante a fase de criação. Para instalar e usar o Composer 2.x em seus projetos Starter e Pro, você deve fazer três alterações nos `.magento.app.yaml` configuração:

1. Remover `composer` como o `build: flavor:` e adicionar `none`. Essa alteração impede que a Cloud use a versão 1.x padrão do Composer para executar tarefas de build.
1. Adicionar `composer/composer: '^2.0'` as a `php` dependência para instalar o Composer 2.x.
1. Adicione o `composer` criar tarefas em um `build` gancho para executar as tarefas de criação usando o Composer 2.x.

Use os fragmentos de configuração a seguir em seu próprio `.magento.app.yaml` configuração:

```yaml
# 1. Change flavor to none.
build:
    flavor: none

# 2. Add Composer ^2.0 as a php dependency.
dependencies:
    php:
        composer/composer: '^2.0'

# 3. Add a build hook to run the build tasks using Composer 2.x.
hooks:
    build: |
        set -e
        composer --no-ansi --no-interaction install --no-progress --prefer-dist --optimize-autoloader
```

Consulte [Pacotes obrigatórios](../development/overview.md#required-packages) para obter mais informações sobre o Composer.

## `dependencies`

Especifique as dependências que seu aplicativo pode precisar durante o processo de compilação.

O Adobe Commerce oferece suporte a dependências nos seguintes idiomas:

- PHP
- Ruby
- Node.js

Essas dependências são independentes das eventuais dependências do aplicativo e estão disponíveis no `PATH`, durante o processo de criação e no ambiente de tempo de execução do aplicativo.

Você pode especificar essas dependências da seguinte maneira:

```yaml
ruby:
   sass: "~3.4"
nodejs:
   grunt-cli: "~0.3"
```

## `runtime`

Use para modificar a configuração do PHP no tempo de execução, como habilitar extensões. As seguintes extensões são necessárias:

```yaml
runtime:
    extensions:
        - xsl
        - newrelic
        - sodium
```

Consulte [Configurações do PHP](php-settings.md) para obter detalhes sobre como ativar extensões.

## `disk`

Define o tamanho de disco persistente do aplicativo em MB.

```yaml
disk: 5120
```

O tamanho de disco mínimo recomendado é de 256 MB. Se você vir o erro `UserError: Error building the project: Disk size may not be smaller than 128MB`, aumente o tamanho para 256 MB.

>[!NOTE]
>
>Para ambientes de preparo e produção profissionais, você deve [Enviar um tíquete de suporte da Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) para atualizar o `mounts` e `disk` configuração do seu aplicativo. Ao enviar o ticket, indique as alterações de configuração necessárias e inclua uma versão atualizada de seu `.magento.app.yaml` arquivo.

## `relationships`

Define o mapeamento de serviços no aplicativo.

A relação `name` está disponível para o aplicativo no `MAGENTO_CLOUD_RELATIONSHIPS` variável de ambiente. A variável `<service-name>:<endpoint-name>` O relacionamento mapeia para os valores de nome e tipo definidos na variável `.magento/services.yaml` arquivo.

```yaml
relationships:
    <name>: "<service-name>:<endpoint-name>"
```

Veja a seguir um exemplo dos relacionamentos padrão:

```yaml
relationships:
    database: "mysql:mysql"
    redis: "redis:redis"
    opensearch: "opensearch:opensearch"
    rabbitmq: "rabbitmq:rabbitmq"
```

Consulte [Serviços](../services/services-yaml.md) para obter uma lista completa dos tipos de serviço e endpoints aceitos no momento.

## `mounts`

Um objeto cujas chaves são caminhos relativos à raiz do aplicativo. A montagem é uma área gravável no disco para arquivos. Veja a seguir uma lista padrão de montagens configuradas no `magento.app.yaml` arquivo usando o `volume_id[/subpath]` sintaxe:

```yaml
 # The mounts that will be performed when the package is deployed.
mounts:
    "var": "shared:files/var"
    "app/etc": "shared:files/etc"
    "pub/media": "shared:files/media"
    "pub/static": "shared:files/static"
```

O formato para adicionar sua montagem a esta lista é o seguinte:

```bash
"/public/sites/default/files": "shared:files/files"
```

- `shared`— compartilha um volume entre seus aplicativos em um ambiente.
- `disk`—Define o tamanho disponível para o volume compartilhado.

>[!NOTE]
>
>Para ambientes de preparo e produção profissionais, você deve [Enviar um tíquete de suporte da Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) para atualizar o `mounts` e `disk` configuração do seu aplicativo. Ao enviar o ticket, indique as alterações de configuração necessárias e inclua uma versão atualizada de seu `.magento.app.yaml` arquivo.

Você pode tornar a montagem da Web acessível adicionando-a à [`web`](web-property.md) bloco de locais.

>[!WARNING]
>
>Depois que o site tiver dados, não altere o `subpath` parte do nome da montagem. Esse valor é o identificador exclusivo do `files` área. Se você alterar esse nome, perderá todos os dados do site armazenados no local antigo.

## `access`

A variável `access` indica um nível mínimo de função de usuário que tem acesso SSH aos ambientes. As funções de usuário disponíveis são:

- `admin`—Pode alterar configurações e executar ações no ambiente; tem _colaborador_ e _visualizador_ direitos.
- `contributor`— pode enviar código para esse ambiente e ramificar-se dele; tem _visualizador_ direitos.
- `viewer`— Pode visualizar somente o ambiente.

A função de usuário padrão é `contributor`, que restringe o acesso SSH de usuários somente com _visualizador_ direitos. Você pode alterar a função de usuário para `viewer` para permitir o acesso SSH somente a usuários com _visualizador_ direitos:

```yaml
access:
    ssh: viewer
```
