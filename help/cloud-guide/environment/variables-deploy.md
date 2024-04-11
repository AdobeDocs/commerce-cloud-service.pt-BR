---
title: Implantar variáveis
description: Consulte a lista de variáveis de ambiente que controlam ações na fase de implantação do Adobe Commerce na infraestrutura em nuvem.
feature: Cloud, Configuration, Cache, Deploy, SCD, Storage, Search
recommendations: noDisplay, catalog
role: Developer
exl-id: 673880b5-830b-4837-ac0c-5fa5643ae34c
source-git-commit: b7307faf046884c13cba852df69d4fa9977e9a17
workflow-type: tm+mt
source-wordcount: '2185'
ht-degree: 0%

---

# Implantar variáveis

As seguintes _implantar_ as variáveis controlam ações na fase de implantação e podem herdar e substituir valores da [Variáveis globais](variables-global.md). Insira essas variáveis no `deploy` fase do `.magento.env.yaml` arquivo:

```yaml
stage:
  deploy:
    DEPLOY_VARIABLE_NAME: value
```

Para obter mais informações sobre como personalizar o processo de criação e implantação:

- [Configuração de implantação](configure-env-yaml.md)
- [Processo de implantação](../deploy/process.md)

## `CACHE_CONFIGURATION`

- **Padrão**—_Não definido_
- **Versão**—Adobe Commerce 2.1.4 e posterior

Configurar página Redis e cache padrão. Ao definir a variável `cm_cache_backend_redis` , você deve especificar o `server`, `port`, e `database` opções.

```yaml
stage:
  deploy:
    CACHE_CONFIGURATION:
      frontend:
        default:
          backend: file
        page_cache:
          backend: file
```

{{merge-options}}

O exemplo a seguir mescla novos valores com uma configuração existente:

```yaml
stage:
  deploy:
    CACHE_CONFIGURATION:
      _merge: true
      frontend:
        default:
          backend_options:
            database: 10
        page_cache:
          backend_options:
            database: 11
```

O exemplo a seguir usa o [Recurso de pré-carregamento Redis](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cache/redis/redis-pg-cache.html#redis-preload-feature) conforme definido na _Guia de configuração_:

```yaml
stage:
  deploy:
    CACHE_CONFIGURATION:
      _merge: true
      frontend:
        default:
          id_prefix: '061_'
          backend_options:
            preload_keys:
              - '061_EAV_ENTITY_TYPES:hash'
              - '061_GLOBAL_PLUGIN_LIST:hash'
              - '061_DB_IS_UP_TO_DATE:hash'
              - '061_SYSTEM_DEFAULT:hash'
```

Para usar um personalizado [REDIS_BACK-END](#redis_backend) (não apenas da lista de permissões), defina o `_custom_redis_backend` opção para `true` para ativar a validação correta, como no exemplo a seguir:

```yaml
stage:
  deploy:
    CACHE_CONFIGURATION:
      frontend:
        default:
          _custom_redis_backend: true
          backend: '\CustomRedisModel'
```

## `CLEAN_STATIC_FILES`

- **Padrão**—`true`
- **Versão**—Adobe Commerce 2.1.4 e posterior

Ativa ou desativa a limpeza [arquivos de conteúdo estático](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/static-view/static-view-file-deployment.html) gerado durante a fase de compilação ou implantação. Usar o valor padrão _true_ em desenvolvimento como uma prática recomendada.

- **`true`**— Remove todo o conteúdo estático existente antes de implantar o conteúdo estático atualizado.
- **`false`**— a implantação somente substitui arquivos de conteúdo estático existentes se o conteúdo gerado contiver uma versão mais recente.

Se você modificar o conteúdo estático por meio de um processo separado, defina o valor como _false_.

```yaml
stage:
  deploy:
    CLEAN_STATIC_FILES: false
```

Falha ao limpar arquivos de exibição estáticos antes da implantação pode causar problemas se você implantar atualizações em arquivos existentes sem remover as versões anteriores. Por causa de [fallback de arquivo estático](https://developer.adobe.com/commerce/frontend-core/guide/caching/#clean-static-files-cache) regras, operações de fallback podem exibir o arquivo errado se o diretório contiver várias versões do mesmo arquivo.

## `CRON_CONSUMERS_RUNNER`

- **Padrão**—`cron_run = false`, `max_messages = 1000`
- **Versão**—Adobe Commerce 2.2.0 e posterior

Use essa variável de ambiente para confirmar se as filas de mensagens estão em execução após uma implantação.

- `cron_run`—Um valor booleano que ativa ou desativa a variável `consumers_runner` trabalho cron (padrão = `false`).
- `max_messages`—Um número que especifica o número máximo de mensagens que cada consumidor deve processar antes de terminar (padrão = `1000`). Você pode definir o valor como `0` para impedir o consumidor de rescindir o contrato.
- `consumers`—Uma matriz de strings especificando quais consumidores executar. Uma matriz vazia é executada _all_ consumidores.

- `multiple_processes`-Um número que especifica o número de processos a serem gerados para cada consumidor. Compatível com o Commerce **2.4.4** ou superior.

>[!NOTE]
>
>Para retornar uma lista de filas de mensagens `consumers`, execute o `./bin/magento queue:consumers:list` no ambiente remoto.

Exemplo de matriz que executa propriedades `consumers` e a variável `multiple_processes` para gerar para cada consumidor:

```yaml
stage:
  deploy:
    CRON_CONSUMERS_RUNNER:
      cron_run: true
      max_messages: 1000
      consumers:
        - example_consumer_1
        - example_consumer_2
-     multiple_processes:
        example_consumer_1: 4
        example_consumer_2: 3
```

Exemplo de uma matriz vazia que executa tudo `consumers`:

```yaml
stage:
  deploy:
    CRON_CONSUMERS_RUNNER:
      cron_run: true
      max_messages: 1000
      consumers: []
```

Por padrão, o processo de implantação substitui todas as configurações no `env.php` arquivo. Consulte [Gerenciar filas de mensagens](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/message-queues/manage-message-queues.html) no _Guia de configuração do Commerce_ para Adobe Commerce no local.

## `CONSUMERS_WAIT_FOR_MAX_MESSAGES`

- **Padrão**—`false`
- **Versão**—Adobe Commerce 2.2.0 e posterior

Configurar como `consumers` processar mensagens da fila de mensagens escolhendo uma das seguintes opções:

- `false`—`Consumers` processar as mensagens disponíveis na fila, fechar a conexão TCP e encerrar. `Consumers` não espere até que mensagens adicionais entrem na fila, mesmo que o número de mensagens processadas seja menor que o `max_messages` valor especificado na variável `CRON_CONSUMERS_RUNNER` implantar variável.

- `true`—`Consumers` continuar a processar mensagens da fila de mensagens até atingir o número máximo de mensagens (`max_messages`) especificados na `CRON_CONSUMERS_RUNNER` implante a variável antes de fechar a conexão TCP e encerrar o processo do consumidor. Se a fila ficar vazia antes de atingir `max_messages`, o consumidor aguarda mais mensagens chegarem.

>[!WARNING]
>
>Se você usar trabalhadores para executar `consumers` em vez de usar um trabalho cron, defina essa variável como true.

```yaml
stage:
  deploy:
    CONSUMERS_WAIT_FOR_MAX_MESSAGES: false
```

## `CRYPT_KEY`

- **Padrão**—_Não definido_
- **Versão**—Adobe Commerce 2.1.4 e posterior

>[!WARNING]
>
>Defina o `CRYPT_KEY` por meio do [!DNL Cloud Console] em vez de `.magento.env.yaml` arquivo para evitar a exposição da chave no repositório de código-fonte do seu ambiente. Consulte [Definir variáveis de ambiente e projeto](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/project/overview.html#configure-environment).

Ao mover o banco de dados de um ambiente para outro sem um processo de instalação, você precisará das informações criptográficas correspondentes. O Adobe Commerce usa o valor da chave de criptografia definido no [!DNL Cloud Console] como o `crypt/key` valor no `env.php` arquivo.

## `DATABASE_CONFIGURATION`

- **Padrão**—_Não definido_
- **Versão**—Adobe Commerce 2.1.4 e posterior

Se você tiver definido um banco de dados na variável [propriedade de relacionamentos](../application/properties.md#relationships) do `.magento.app.yaml` arquivo, você pode personalizar suas conexões de banco de dados para implantação.

```yaml
stage:
  deploy:
    DATABASE_CONFIGURATION:
      some_config: 'some_value'
```

{{merge-options}}

O exemplo a seguir mescla novos valores com uma configuração existente:

```yaml
stage:
  deploy:
    DATABASE_CONFIGURATION:
      some_config: 'some_new_value'
      _merge: true
```

Além disso, é possível configurar um prefixo de tabela.

>[!WARNING]
>
>Se você não usar a opção de mesclagem com o prefixo da tabela, deverá fornecer as configurações de conexão padrão ou a validação da implantação falhará.

O exemplo a seguir usa o `ece_` prefixo da tabela com configurações de conexão padrão em vez de usar o `_merge` opção:

```yaml
stage:
  deploy:
    DATABASE_CONFIGURATION:
      connection:
        default:
          username: user
          host: host
          dbname: magento
          password: password
      table_prefix: 'ece_'
```

Saída de exemplo:

```terminal
MariaDB [main]> SHOW TABLES;
+-------------------------------------+
| Tables_in_main                      |
+-------------------------------------+
| ece_admin_passwords                 |
| ece_admin_system_messages           |
| ece_admin_user                      |
| ece_admin_user_session              |
| ece_adminnotification_inbox         |
| ece_amazon_customer                 |
| ece_authorization_rule              |
| ece_cache                           |
| ece_cache_tag                       |
| ece_captcha_log                     |
...
```

## `ELASTICSUITE_CONFIGURATION`

- **Padrão**—_Não definido_
- **Versão**—Adobe Commerce 2.2.0 e posterior

Mantém personalizações [!DNL Elastic Suite] configurações de serviço entre implantações e o usa na seção &quot;system/default/sorriso_elasticsuite_core_base_settings&quot; da página principal [!DNL Elastic Suite] configuração. Se a variável [!DNL Elastic Suite] o pacote composer está instalado e é configurado automaticamente.

```yaml
stage:
  deploy:
    ELASTICSUITE_CONFIGURATION:
      es_client:
        servers: 'remote-host:9200'
      indices_settings:
        number_of_shards: 1
        number_of_replicas: 0
```

{{merge-options}}

O exemplo a seguir mescla um novo valor com a configuração existente:

```yaml
stage:
  deploy:
    ELASTICSUITE_CONFIGURATION:
      indices_settings:
        number_of_shards: 3
        number_of_replicas: 2
      _merge: true
```

**Limitações conhecidas**:

- Alteração do mecanismo de pesquisa para qualquer tipo diferente de `elasticsuite` causa uma falha de implantação acompanhada por um erro de validação apropriado
- A remoção do serviço de Elasticsearch causa uma falha de implantação acompanhada de um erro de validação apropriado

>[!NOTE]
>
>Para obter detalhes sobre o uso ou a solução de problemas do [!DNL Elastic Suite] com o Adobe Commerce, consulte a [[!DNL Elastic Suite] documentação](https://github.com/Smile-SA/elasticsuite).

## `ENABLE_GOOGLE_ANALYTICS`

- **Padrão**—`false`
- **Versão**—Adobe Commerce 2.1.4 e posterior

Ativa e desativa Google Analytics ao implantar em ambientes de Preparo e Integração. Por padrão, Google Analytics é verdadeiro somente para o ambiente de Produção. Defina esse valor como `true` para ativar Google Analytics nos ambientes Preparo e Integração.

- **`true`**— Ativa Google Analytics em ambientes de preparo e integração.
- **`false`**—Desativa Google Analytics em ambientes de preparo e integração.

Adicione o `ENABLE_GOOGLE_ANALYTICS` variável de ambiente para o `deploy` etapa no `.magento.env.yaml` arquivo:

```yaml
stage:
  deploy:
    ENABLE_GOOGLE_ANALYTICS: true
```

>[!NOTE]
>
>O processo de implantação sempre ativa Google Analytics em ambientes de produção.

## `FORCE_UPDATE_URLS`

- **Padrão**—`true`
- **Versão**—Adobe Commerce 2.1.4 e posterior

Na implantação em ambientes Pro ou Starter de preparo e produção, essa variável substitui os URLs de base do Adobe Commerce no banco de dados pelos URLs do projeto especificados pelo [`MAGENTO_CLOUD_ROUTES`](variables-cloud.md) variável. Use esta configuração para substituir o comportamento padrão do [UPDATE_URLS](#update_urls) implantar variável, que é ignorada ao implantar em ambientes de preparo ou produção.

```yaml
stage:
  deploy:
    FORCE_UPDATE_URLS: true
```

## `LOCK_PROVIDER`

- **Padrão**—`file`
- **Versão**—Adobe Commerce 2.2.5 e posterior

O provedor de bloqueio impede a inicialização de trabalhos cron duplicados e grupos cron. Use o `file` bloquear o provedor no ambiente de produção. Os ambientes iniciais e o ambiente de integração Pro não usam a variável [MAGENTO_CLOUD_LOCKS_DIR](variables-cloud.md) variável, então `ece-tools` aplica o `db` bloquear o provedor automaticamente.

```yaml
stage:
  deploy:
    LOCK_PROVIDER: "db"
```

Consulte [Configurar o bloqueio](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/tutorials/lock-provider.html) no _Guia de instalação_.

## `MYSQL_USE_SLAVE_CONNECTION`

- **Padrão**—`false`
- **Versão**—Adobe Commerce 2.1.4 e posterior

>[!TIP]
>
>A variável `MYSQL_USE_SLAVE_CONNECTION` A variável só é compatível com ambientes de cluster Adobe Commerce em preparo de infraestrutura em nuvem e Production Pro e não é compatível com projetos iniciais.

O Adobe Commerce pode ler vários bancos de dados de forma assíncrona. Defina como `true` para usar automaticamente uma _somente leitura_ conexão com o banco de dados para receber tráfego somente leitura em um nó não mestre. Essa conexão melhora o desempenho por meio do balanceamento de carga, pois somente um nó lida com o tráfego de leitura-gravação. Defina como `false` para remover qualquer matriz de conexão somente leitura existente do `env.php` arquivo.

```yaml
stage:
  deploy:
    MYSQL_USE_SLAVE_CONNECTION: true
```

Quando a variável `MYSQL_USE_SLAVE_CONNECTION` está definida como `true`, o `synchronous_replication` está definido como `true` por padrão, no campo `env.php` arquivo nos ambientes Pro Staging e Production. Quando a variável `MYSQL_USE_SLAVE_CONNECTION` está definida como `false`, o `synchronous_replication` parâmetro não configurado.

## `QUEUE_CONFIGURATION`

- **Padrão**—_Não definido_
- **Versão**—Adobe Commerce 2.1.4 e posterior

Use essa variável de ambiente para manter configurações de serviço AMQP personalizadas entre implantações. Por exemplo, se você preferir usar um serviço de fila de mensagens existente, em vez de depender da infraestrutura de nuvem para criá-lo, use o `QUEUE_CONFIGURATION` variável de ambiente para conectá-la ao seu site:

```yaml
stage:
  deploy:
    QUEUE_CONFIGURATION:
      amqp:
        host: test.host
        port: 1234
      amqp2:
        host: test.host2
        port: 12345
      mq:
        host: mq.host
        port: 1234
```

{{merge-options}}

O exemplo a seguir mescla novos valores com uma configuração existente:

```yaml
stage:
  deploy:
    QUEUE_CONFIGURATION:
      _merge: true
      amqp:
        host: changed1.host
        port: 5672
      amqp2:
        host: changed2.host2
        port: 12345
      mq:
        host: changedmq.host
        port: 1234
```

## `REDIS_BACKEND`

- **Padrão**—`Cm_Cache_Backend_Redis`
- **Versão**—Adobe Commerce 2.3.0 e posterior

Especifica a configuração do modelo de back-end para o cache Redis.

O Adobe Commerce versão 2.3.0 e posterior inclui os seguintes modelos de back-end:

- `Cm_Cache_Backend_Redis`
- `\Magento\Framework\Cache\Backend\Redis`
- `\Magento\Framework\Cache\Backend\RemoteSynchronizedCache`

O exemplo de como definir `REDIS_BACKEND`

```yaml
stage:
  deploy:
    REDIS_BACKEND: '\Magento\Framework\Cache\Backend\RemoteSynchronizedCache'
```

>[!NOTE]
>
>Se você especificar `\Magento\Framework\Cache\Backend\RemoteSynchronizedCache` como o modelo de back-end do Redis para habilitar [Cache L2](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cache/level-two-cache.html), `ece-tools` O gera a configuração do cache automaticamente. Veja um exemplo [arquivo de configuração](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cache/level-two-cache.html#configuration-example) no _Guia de configuração do Adobe Commerce_. Para substituir a configuração de cache gerada, use o [CACHE_CONFIGURATION](#cache_configuration) implantar variável.

## `REDIS_USE_SLAVE_CONNECTION`

- **Padrão**—`false`
- **Versão**—Adobe Commerce 2.1.16 e posterior

>[!WARNING]
>
>Fazer _não_ habilitar essa variável em um [arquitetura dimensionada](../architecture/scaled-architecture.md) projeto. Isso causa erros de conexão Redis. Os escravos Redis ainda estão ativos, mas não são usados para leituras Redis. Como alternativa, a Adobe recomenda o uso do Adobe Commerce 2.3.5 ou posterior, a implementação de uma nova configuração de back-end Redis e o armazenamento em cache L2 para Redis.

>[!TIP]
>
>A variável `REDIS_USE_SLAVE_CONNECTION` A variável só é compatível com ambientes de cluster Adobe Commerce em preparo de infraestrutura em nuvem e Production Pro e não é compatível com projetos iniciais.

O Adobe Commerce pode ler várias instâncias de Redis de forma assíncrona. Defina como `true` para usar automaticamente uma _somente leitura_ conexão com uma instância Redis para receber tráfego somente leitura em um nó não mestre. Essa conexão melhora o desempenho por meio do balanceamento de carga, pois somente um nó lida com o tráfego de leitura-gravação. Defina como `false` para remover qualquer matriz de conexão somente leitura existente do `env.php` arquivo.

```yaml
stage:
  deploy:
    REDIS_USE_SLAVE_CONNECTION: true
```

Você deve ter um serviço Redis configurado no `.magento.app.yaml` e no campo `services.yaml` arquivo.

[ECE-Tools versão 2002.0.18](../release-notes/cloud-release-archive.md#v2002018) e mais tarde usa configurações mais tolerantes a falhas. Se o Adobe Commerce não conseguir ler os dados do Redis _slave_ instância, em seguida, lê os dados do Redis _master_ instância.

A conexão somente leitura não está disponível para uso no ambiente de integração ou se você usar o [`CACHE_CONFIGURATION` variável](#cache_configuration).

## `RESOURCE_CONFIGURATION`

- **Padrão**— Not set
- **Versão**—Adobe Commerce 2.1.4 e posterior

Mapeia um nome de recurso para uma conexão de banco de dados. Essa configuração corresponde à variável `resource` seção do `env.php` arquivo.

{{merge-options}}

O exemplo a seguir mescla novos valores com uma configuração existente:

```yaml
stage:
  deploy:
    RESOURCE_CONFIGURATION:
      _merge: true
      default_setup:
        connection: default
```

## `SCD_COMPRESSION_LEVEL`

- **Padrão**—`4`
- **Versão**—Adobe Commerce 2.1.4 e posterior

Especifica qual [gzip](https://www.gnu.org/software/gzip) nível de compactação (`0` para `9`) para usar ao compactar conteúdo estático; `0` desativa a compactação.

```yaml
stage:
  deploy:
    SCD_COMPRESSION_LEVEL: 5
```

## `SCD_COMPRESSION_TIMEOUT`

- **Padrão**—`600`
- **Versão**—Adobe Commerce 2.1.4 e posterior

Quando o tempo necessário para compactar os ativos estáticos excede o tempo limite de compactação, ele interrompe o processo de implantação. Defina o tempo máximo de execução, em segundos, para o comando static content compression.

```yaml
stage:
  deploy:
    SCD_COMPRESSION_TIMEOUT: 800
```

## `SCD_MATRIX`

- **Padrão**—_Não definido_
- **Versão**—Adobe Commerce 2.1.4 e posterior

Você pode configurar vários locais por tema. Essa personalização acelera o processo de implantação, reduzindo o número de arquivos de tema desnecessários. Por exemplo, é possível implantar o _magento/backend_ tema em inglês e um tema personalizado em outros idiomas.

O exemplo a seguir implanta o `Magento/backend` tema com três localidades:

```yaml
stage:
  deploy:
    SCD_MATRIX:
      "magento/backend":
        language:
          - en_US
          - fr_FR
          - af_ZA
```

Além disso, você pode optar por _não_ implantar um tema:

```yaml
stage:
  deploy:
    SCD_MATRIX:
      "magento/backend": [ ]
```

## `SCD_MAX_EXECUTION_TIME`

- **Padrão**—_Não definido_
- **Versão**—Adobe Commerce 2.2.0 e posterior

Permite aumentar o tempo de execução máximo esperado para implantação de conteúdo estático.

Por padrão, o Adobe Commerce define a execução máxima esperada para 900 segundos, mas em alguns cenários, pode ser necessário mais tempo para concluir a implantação do conteúdo estático para um projeto na nuvem.

```yaml
stage:
  deploy:
    SCD_MAX_EXECUTION_TIME: 3600
```

{{scd-timing-warning}}

## `SCD_NO_PARENT`

- **Padrão**—`false`
- **Versão**—Adobe Commerce 2.4.2 e posterior

Na fase de implantação, defina `SCD_NO_PARENT: true` para que a geração de conteúdo estático para temas principais não ocorra durante a fase de implantação. Essa configuração minimiza o tempo de implantação e evita o tempo de inatividade do site que pode ocorrer se a compilação de conteúdo estático falhar durante a implantação. Consulte [Implantação de conteúdo estático](../deploy/static-content.md).

```yaml
stage:
  deploy:
    SCD_NO_PARENT: true
```

## `SCD_STRATEGY`

- **Padrão**—`quick`
- **Versão**—Adobe Commerce 2.2.0 e posterior

Permite personalizar o [estratégia de implantação](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/static-view/static-view-file-strategy.html) para conteúdo estático. Consulte [Implantar arquivos de exibição estáticos](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/static-view/static-view-file-deployment.html).

Usar estas opções _somente_ se você tiver mais de um local:

- `standard`—implanta todos os arquivos de visualização estáticos para todos os pacotes.
- `quick`—(_padrão_) minimiza o tempo de implantação.
- `compact`—preserva o espaço em disco no servidor. No Adobe Commerce versão 2.2.4 e anterior, essa configuração substitui o valor de `scd_threads` com um valor de `1`.

```yaml
stage:
  deploy:
    SCD_STRATEGY: "compact"
```

## `SCD_THREADS`

- **Padrão**— Automatic
- **Versão**—Adobe Commerce 2.1.4 e posterior

Define o número de threads para implantação de conteúdo estático. O valor padrão é definido com base na contagem de threads da CPU detectada e não excede um valor 4. Aumentar o número de threads acelera a implantação de conteúdo estático; diminuir o número de threads o torna mais lento. Você pode definir o valor da thread, por exemplo:

```yaml
stage:
  deploy:
    SCD_THREADS: 2
```

Para reduzir ainda mais o tempo de implantação, use [Gerenciamento de configurações](../store/store-settings.md) com o `scd-dump` para mover a implantação estática para a fase de criação.

## `SEARCH_CONFIGURATION`

- **Padrão**—_Não definido_
- **Versão**—Adobe Commerce 2.1.4 e posterior

Use essa variável de ambiente para manter configurações personalizadas do serviço de pesquisa entre implantações. Por exemplo:

Configuração de Elasticsearch:

```yaml
stage:
  deploy:
    SEARCH_CONFIGURATION:
      engine: elasticsearch
      elasticsearch_server_hostname: http://elasticsearch.internal
      elasticsearch_server_port: '9200'
      elasticsearch_index_prefix: magento2
      elasticsearch_server_timeout: '15'
```

Configuração do OpenSearch (para Commerce 2.4.6 e posterior):

```yaml
stage:
  deploy:
    SEARCH_CONFIGURATION:
      engine: opensearch
      opensearch_server_hostname: 'http://opensearch.internal'
      opensearch_server_port: '9200'
      opensearch_index_prefix: 'magento2'
      opensearch_server_timeout: '15'
```

{{merge-options}}

O exemplo a seguir mescla um novo valor com a configuração existente:

```yaml
stage:
  deploy:
    SEARCH_CONFIGURATION:
      engine: elasticsearch
      elasticsearch_server_port: '9200'
      _merge: true
```

## `SESSION_CONFIGURATION`

- **Padrão**—_Não definido_
- **Versão**—Adobe Commerce 2.1.4 e posterior

Configurar o armazenamento de sessão Redis. Exige o `save`, `redis`, `host`, `port`, e `database` opções para a variável de armazenamento da sessão. Por exemplo:

```yaml
stage:
  deploy:
    SESSION_CONFIGURATION:
      redis:
        bot_first_lifetime: 100
        bot_lifetime: 10001
        database: 0
        disable_locking: 1
        host: redis.internal
        max_concurrency: 10
        max_lifetime: 10001
        min_lifetime: 100
        port: 6379
      save: redis
```

{{merge-options}}

O exemplo a seguir mescla um novo valor com a configuração existente:

```yaml
stage:
  deploy:
    SESSION_CONFIGURATION:
      _merge: true
      redis:
        max_concurrency: 10
```

## `SKIP_SCD`

- **Padrão**— _Não definido_
- **Versão**—Adobe Commerce 2.1.4 e posterior

Defina como `true` para ignorar a implantação de conteúdo estático durante a fase de implantação.

Na fase de implantação, defina `SKIP_SCD: true` para que a criação do conteúdo estático não ocorra durante a fase de implantação. Essa configuração minimiza o tempo de implantação e evita o tempo de inatividade do site que pode ocorrer se a compilação de conteúdo estático falhar durante a implantação. Consulte [Implantação de conteúdo estático](../deploy/static-content.md).

```yaml
stage:
  deploy:
    SKIP_SCD: true
```

## `UPDATE_URLS`

- **Padrão**—`true`
- **Versão**—Adobe Commerce 2.1.4 e posterior

Na implantação, substitua os URLs de base do Adobe Commerce no banco de dados pelos URLs do projeto especificados pelo [`MAGENTO_CLOUD_ROUTES`](variables-cloud.md) variável. Essa configuração é útil para desenvolvimento local, em que os URLs básicos são configurados para o ambiente local. Quando você implanta em um ambiente de nuvem, os URLs são atualizados para que você possa acessar sua vitrine e o administrador usando os URLs do projeto.

Se for necessário atualizar os URLs ao implantar em ambientes Pro ou Starter Staging e Production, use o [`FORCE_UPDATE_URLS`](#force_update_urls) variável.

```yaml
stage:
  deploy:
    UPDATE_URLS: false
```

## `VERBOSE_COMMANDS`

- **Padrão**—_Não definido_
- **Versão**—Adobe Commerce 2.1.4 e posterior

Ative ou desative o [Symfony](https://symfony.com/doc/current/console/verbosity.html) depurar nível de detalhamento para `bin/magento` Comandos da CLI executados durante a fase de implantação.

>[!NOTE]
>
>Para usar a configuração VERBOSE_COMMANDS para controlar os detalhes na saída do comando para êxito e falha `bin/magento` Comandos CLI, você deve definir [MIN_LOGGING_LEVEL](variables-global.md#minlogginglevel) `debug`.

Escolha o nível de detalhes fornecido nos logs:

- `-v`= saída normal
- `-vv`= saída mais detalhada
- `-vvv` = saída detalhada ideal para depuração

```yaml
stage:
  deploy:
    VERBOSE_COMMANDS: "-vv"
```
