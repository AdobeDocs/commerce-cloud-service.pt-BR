---
title: Exibir e gerenciar logs
description: Entenda os tipos de arquivos de log disponíveis na infraestrutura da nuvem e onde encontrá-los.
last-substantial-update: 2023-05-23T00:00:00Z
exl-id: d7f63dab-23bf-4b95-b58c-3ef9b46979d4
source-git-commit: 13e76d3e9829155995acbb72d947be3041579298
workflow-type: tm+mt
source-wordcount: '1024'
ht-degree: 0%

---

# Exibir e gerenciar logs

Os logs do Adobe Commerce em projetos de infraestrutura em nuvem são úteis para solucionar problemas relacionados a [criar e implantar ganchos](../application/hooks-property.md), serviços em nuvem e o aplicativo do Adobe Commerce.

Você pode visualizar os registros do sistema de arquivos, a variável [!DNL Cloud Console], e o `magento-cloud` CLI.

- **Sistema de arquivos**—O `/var/log` o diretório do sistema contém logs para todos os ambientes. A variável `var/log/` O diretório contém logs específicos do aplicativo exclusivos a um ambiente específico. Esses diretórios não são compartilhados entre nós em um cluster. Em ambientes de produção e preparo profissionais, você deve verificar os registros em cada nó.

- **[!DNL Cloud Console]**— você pode ver as informações de log de criação, implantação e pós-implantação no ambiente _messages_ lista.

- **CLI da nuvem**— É possível visualizar registros de ambientes locais usando o `magento-cloud log` ou registros de ambiente remoto usando o `magento-cloud ssh` comando.

## Locais de log

Os registros do sistema são armazenados nos seguintes locais:

- Integração: `/var/log/<log-name>.log`
- Estágios profissionais: `/var/log/platform/<project-ID>_stg/<log-name>.log`
- Produção Pro: `/var/log/platform/<project-ID>/<log-name>.log`

O valor de `<project-ID>` depende do projeto e se o ambiente é de Preparo ou Produção. Por exemplo, com uma ID de projeto de `yw1unoukjcawe`, o usuário do ambiente de preparo é `yw1unoukjcawe_stg` e o usuário do ambiente de produção for `yw1unoukjcawe`.

Usando esse exemplo, o log de implantação é: `/var/log/platform/yw1unoukjcawe_stg/deploy.log`

### Exibir logs de ambiente remoto

A maioria dos registros inclui eventos que ocorrem no ambiente remoto. Para o Pro, há vários nós e cada nó tem registros exclusivos. Use o seguinte para ver uma lista de todos os hosts:

```bash
magento-cloud ssh -p <project-ID> -e <environment-ID> --all
```

Exemplo de resposta:

```terminal
1.ent-project-environment-id@ssh.region.magento.cloud
2.ent-project-environment-id@ssh.region.magento.cloud
3.ent-project-environment-id@ssh.region.magento.cloud
```

**Para exibir uma lista de logs de ambientes remotos**:

```bash
magento-cloud ssh -e <environment-ID> "ls var/log"
```

Exemplo para Pro:

```bash
ssh 1.ent-project-environment-id@ssh.region.magento.cloud "ls var/log | grep error"
```

**Para ver um registro remoto**:

```bash
magento-cloud ssh -e <environment-ID> "cat var/log/cron.log"
```

Exemplo para Pro:

```bash
ssh 1.ent-project-environment-id@ssh.region.magento.cloud "cat var/log/cron.log"
```

>[!TIP]
>
>Para ambientes Pro, a rotação, compactação e remoção automáticas de registros são ativadas para arquivos de registro com um nome de arquivo fixo. Cada tipo de arquivo de log tem um padrão rotativo e uma duração. Os ambientes iniciais não têm rotação de log. Detalhes completos sobre a rotação de logs do ambiente e a duração de logs compactados podem ser encontrados em: `/etc/logrotate.conf` e `/etc/logrotate.d/<various>`

## Criar e implantar logs

Depois de enviar as alterações para o ambiente, você pode revisar o registro de cada gancho na `var/log/cloud.log` arquivo. O log contém mensagens de início e parada para cada gancho. No exemplo a seguir, as mensagens são &quot;`Starting post-deploy.`&quot; e &quot;`Post-deploy is complete.`&quot;

Verifique os carimbos de data e hora nas entradas do log e localize os logs para uma implantação específica. Este é um exemplo condensado de saída de log que você pode usar para solução de problemas:

```terminal
Re-deploying environment project-integration-ID
  Executing post deploy hook for service `mymagento`
    [2019-01-03 19:44:11] NOTICE: Starting post-deploy.
    [2019-01-03 19:44:11] INFO: Validating configuration
    [2019-01-03 19:44:11] INFO: End of validation
    [2019-01-03 19:44:11] INFO: Enable cron
    [2019-01-03 19:44:11] INFO: Create backup of important files.
    [2019-01-03 19:44:11] INFO: Backup /app/app/etc/env.php.bak for /app/app/etc/env.php was created.
    [2019-01-03 19:44:11] INFO: Backup /app/app/etc/config.php.bak for /app/app/etc/config.php was created.
    [2019-01-03 19:44:11] INFO: php ./bin/magento cache:flush --ansi --no-interaction
    [2019-01-03 19:44:32] INFO: Warming up failed: http://integration-id-project.us.magentosite.cloud/
    [2019-01-03 19:44:32] NOTICE: Post-deploy is complete.
```

>[!TIP]
>
>Ao configurar o ambiente em nuvem, é possível definir [Slack baseado em log e notificações por email](../environment/set-up-notifications.md) para criar e implantar ações.

Os seguintes logs têm um local comum para todos os projetos na nuvem:

- **Log de implantação**: `var/log/cloud.log`
- **Último log de erros de implantação**: `var/log/cloud.error.log`
- **Log de depuração**: `var/log/debug.log`
- **Log de exceções**: `var/log/exception.log`
- **Log do sistema**: `var/log/system.log`
- **Log de suporte**: `var/log/support_report.log`
- **Relatórios**: `var/report/`

Embora o `cloud.log` O arquivo contém feedback de cada estágio do processo de implantação. Os logs criados pelo gancho de implantação são exclusivos de cada ambiente. O log de implantação específico do ambiente está nos seguintes diretórios:

- **Integração Starter e Pro**: `/var/log/deploy.log`
- **Estágio Pro**: `/var/log/platform/<project-ID>_stg/deploy.log`
- **Produção Pro**: `/var/log/platform/<project-ID>/deploy.log`

### Implantar log

O log de cada implantação concatena com a variável `deploy.log` arquivo. O exemplo a seguir imprime o log de implantação do ambiente atual no terminal:

```bash
magento-cloud log -e <environment-ID> deploy
```

Exemplo de resposta:

```terminal
Reading log file projectID-branchname-ID--mymagento@ssh.zone.magento.cloud:/var/log/'deploy.log'

[2023-04-24 18:58:03.080678] Launching command 'b'php ./vendor/bin/ece-tools run scenario/deploy.xml\n''.

[2023-04-24T18:58:04.129888+00:00] INFO: Starting scenario(s): scenario/deploy.xml (magento/ece-tools version: 2002.1.14, magento/magento2-base version: 2.4.6)
[2023-04-24T18:58:04.364714+00:00] NOTICE: Starting pre-deploy.
...
```

{{scd-timing-warning}}

### Log de erros

Mensagens de erro e de aviso geradas durante o processo de implantação são gravadas em ambos `var/log/cloud.log` e a variável `var/log/cloud.error.log` arquivos. O arquivo de log de erros da nuvem contém apenas erros e avisos da implantação mais recente. Um arquivo vazio indica uma implantação bem-sucedida sem erros.

Você pode exibir o arquivo de log usando o [SSH da CLI da nuvem](#view-remote-environment-logs)ou você pode usar ECE-Tools para mostrar os erros com sugestões:

```bash
magento-cloud ssh -e <environment-ID> "./vendor/bin/ece-tools error:show"
```

Exemplo de resposta:

```terminal
errorCode: 1001
stage: build
step: validate-config
suggestion: Please run the following commands:
1. bin/magento module:enable --all
2. git add -f app/etc/config.php
3. git commit -m 'Adding config.php'
4. git push
title: File app/etc/config.php does not exist
type: warning
---------------

errorCode: 1006
stage: build
step: validate-config
suggestion: Your application does not have the "post_deploy" hook enabled.
  In order to minimize downtime, add the following to ".magento.app.yaml":
  hooks:
      post_deploy: |
          php ./vendor/bin/ece-tools run scenario/post-deploy.xml
title: The configured state is not ideal
type: warning
```

A maioria das mensagens de erro contém uma descrição e uma ação sugerida. Use o [Referência da mensagem de erro para ECE-Tools](../dev-tools/error-reference.md) para consultar o código de erro e obter mais orientações. Para obter mais orientações, use o [Solução de problemas de implantação do Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/deployment/magento-deployment-troubleshooter.html).

## Logs do aplicativo

Assim como os logs de implantação, os logs de aplicativos são exclusivos para cada ambiente:

| Arquivo de log | Integração do Starter e do Pro | Descrição |
| ------------------- | --------------------------- | ------------------------------------------------- |
| **Implantar log** | `/var/log/deploy.log` | Atividade de [gancho de implantação](../application/hooks-property.md). |
| **Log pós-implantação** | `/var/log/post_deploy.log` | Atividade de [gancho pós-implantação](../application/hooks-property.md). |
| **Log do Cron** | `/var/log/cron.log` | Saída de trabalhos cron. |
| **Log de acesso do Nginx** | `/var/log/access.log` | Na inicialização do Nginx, erros de HTTP para diretórios ausentes e tipos de arquivos excluídos. |
| **Log de erros do Nginx** | `/var/log/error.log` | Mensagens de inicialização úteis para depurar erros de configuração associados ao Nginx. |
| **Log de acesso do PHP** | `/var/log/php.access.log` | Solicitações para o serviço PHP. |
| **Log FPM do PHP** | `/var/log/app.log` | |

Para ambientes de preparo e produção Pro, os logs de implantação, pós-implantação e cron estão disponíveis somente no primeiro nó do cluster:

| Arquivo de log | Estágio Pro | Produção Pro |
| ------------------- | --------------------------------------------------- | ----------------------------------------------- |
| **Implantar log** | Somente o primeiro nó:<br>`/var/log/platform/<project-ID>_stg/deploy.log` | Somente o primeiro nó:<br>`/var/log/platform/<project-ID>/deploy.log` |
| **Log pós-implantação** | Somente o primeiro nó:<br>`/var/log/platform/<project-ID>_stg/post_deploy.log` | Somente o primeiro nó:<br>`/var/log/platform/<project-ID>/post_deploy.log` |
| **Log do Cron** | Somente o primeiro nó:<br>`/var/log/platform/<project-ID>_stg/cron.log` | Somente o primeiro nó:<br>`/var/log/platform/<project-ID>/cron.log` |
| **Log de acesso do Nginx** | `/var/log/platform/<project-ID>_stg/access.log` | `/var/log/platform/<project-ID>/access.log` |
| **Log de erros do Nginx** | `/var/log/platform/<project-ID>_stg/error.log` | `/var/log/platform/<project-ID>/error.log` |
| **Log de acesso do PHP** | `/var/log/platform/<project-ID>_stg/php.access.log` | `/var/log/platform/<project-ID>/php.access.log` |
| **Log FPM do PHP** | `/var/log/platform/<project-ID>_stg/php5-fpm.log` | `/var/log/platform/<project-ID>/php5-fpm.log` |

### Arquivos de log arquivados

Os registros de aplicativos são compactados e arquivados uma vez por dia e mantidos por um ano. Os logs compactados são nomeados usando uma ID exclusiva que corresponde à `Number of Days Ago + 1`. Por exemplo, em ambientes de produção Pro, um log de acesso do PHP para 21 dias no passado é armazenado e nomeado da seguinte maneira:

```terminal
/var/log/platform/<project-ID>/php.access.log.22.gz
```

Os arquivos de log arquivados são sempre armazenados no diretório onde o arquivo original estava localizado antes da compactação.

>[!NOTE]
>
>**Implantar** e **Pós-implantação** os arquivos de registro não são rotacionados e arquivados. Todo o histórico de implantação é gravado nesses arquivos de log.

## Logs de serviço

Como cada serviço é executado em um contêiner separado, os logs do serviço não estão disponíveis no ambiente de integração. A infraestrutura do Adobe Commerce na nuvem fornece acesso ao container do servidor Web somente no ambiente de integração. Os seguintes locais de registro de serviço são para os ambientes de produção e preparo profissionais:

- **Log Redis**: `/var/log/platform/<project-ID>_stg/redis-server-<project-ID>_stg.log`
- **log de Elasticsearch**: `/var/log/elasticsearch/elasticsearch.log`
- **Log de coleta de lixo Java**: `/var/log/elasticsearch/gc.log`
- **Log de email**: `/var/log/mail.log`
- **Log de erros do MySQL**: `/var/log/mysql/mysql-error.log`
- **Log lento do MySQL**: `/var/log/mysql/mysql-slow.log`
- **Log do RabbitMQ**: `/var/log/rabbitmq/rabbit@host1.log`

Os logs de serviço são arquivados e salvos por períodos diferentes, dependendo do tipo de log. Por exemplo, os registros MySQL têm o tempo de vida mais curto, removido após sete dias.

>[!TIP]
>
>Os locais do arquivo de log na arquitetura dimensionada dependem do tipo de nó. Consulte [Registra locais na arquitetura dimensionada](../architecture/scaled-architecture.md#log-locations) tópico.

## Dados de log para produção e preparo profissionais

Em ambientes de produção e preparo profissionais, use [Gerenciamento de logs do New Relic](../monitor/log-management.md) integrado ao seu projeto para gerenciar dados de log agregados de todos os logs associados ao seu projeto do Adobe Commerce na nuvem.

O aplicativo de logs do New Relic fornece um painel de gerenciamento de log centralizado para solucionar problemas e monitorar o Adobe Commerce em ambientes de produção e preparo de infraestrutura em nuvem. O painel também fornece acesso aos dados de log para os serviços Fastly CDN, Image Otimization e Web application firewall (WAF). Consulte [Serviços da New Relic](../monitor/new-relic-service.md).
