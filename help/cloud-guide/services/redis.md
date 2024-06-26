---
title: Configurar o serviço Redis
description: Saiba como configurar e otimizar o Redis como uma solução de cache de back-end para Adobe Commerce na infraestrutura em nuvem.
feature: Cloud, Cache, Services
exl-id: d6971875-d302-495a-ad10-a81c507c2bc9
source-git-commit: 1253d8357fd2554050d1775fefbc420a2097db5f
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 0%

---

# Configurar o serviço Redis

[Redis](https://redis.io) é uma solução de cache de back-end opcional que substitui o Zend Framework Zend_Cache_Backend_File, que o Adobe Commerce usa por padrão.

Consulte [Configurar Redis](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cache/redis/config-redis.html) no _Guia de configuração_.

{{service-instruction}}

**Para ativar o Redis**:

1. Adicione o nome e o tipo necessários à `.magento/services.yaml` arquivo.

   ```yaml
   myredis:
       type: redis:<version>
   ```

   Para fornecer sua própria configuração Redis, adicione um `core_config` chave em seu `.magento/services.yaml` arquivo:

   ```yaml
   cache:
       type: redis:<version>
   ```

1. Configure os relacionamentos no `.magento.app.yaml` arquivo.

   ```yaml
   runtime:
       extensions:
           - redis
   
   relationships:
       redis: "redis:redis"
   ```

1. Adicionar, confirmar e enviar por push as alterações de código.

   ```bash
   git add .magento/services.yaml .magento.app.yaml && git commit -m "Enable redis service" && git push origin <branch-name>
   ```

1. [Verificar as relações de serviço](services-yaml.md#service-relationships).

{{service-change-tip}}

## Usando a CLI Redis

Supondo que seu relacionamento com Redis seja nomeado `redis`, você poderá acessá-lo usando a `redis-cli` ferramenta.

1. Use o SSH para se conectar ao ambiente de integração com o Redis instalado e configurado.

1. Abra um túnel SSH para um host.

   ```bash
   redis-cli -h redis.internal
   ```

## Obter a versão do Redis instalada

Use o seguinte comando para obter a versão Redis instalada em um ambiente de integração:

```bash
redis-cli -h redis.internal info | grep version
```

Exemplo de resposta:

```terminal
redis_version:7.0.5
gcc_version:8.3.0
```

### Redes em preparo e produção profissionais

Para obter a versão do Redis instalada em um ambiente de armazenamento temporário ou de produção, use o `redis-server` comando:

```bash
redis-server -v
```

```terminal
Redis server v=7.0.5 ...
```

Use o seguinte comando para obter a configuração Redis instalada em um ambiente Pro Staging ou Production:

```bash
echo $MAGENTO_CLOUD_RELATIONSHIPS | base64 -d | json_pp
```

Exemplo de resposta:

```terminal
"redis" : [
    {
        "cluster" : "project-master-123abc4",
        "fragment" : null,
        "host" : "redis.internal",
        "host_mapped" : false,
        "hostname" : "oblahblahblahblahe.redis.service._.magentosite.cloud",
        "ip" : "169.254.10.10",
        "password" : null,
        "path" : null,
        "port" : 6379,
        "public" : false,
        "query" : {},
        "rel" : "redis",
        "scheme" : "redis",
        "service" : "redis",
        "type" : "redis:7.0.5",
        "username" : null
    }
]
```

## Solução de problemas do Redis

Consulte os seguintes artigos de suporte da Adobe Commerce para obter ajuda com a solução de problemas Redis:

- [Resgatar atraso de envio Login ou finalização de administração](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/redis-issue-delay-magento-admin-login-or-checkout.html)
- [Implementação do cache Redis estendido Adobe Commerce 2.3.5+](https://experienceleague.adobe.com/docs/commerce-operations/implementation-playbook/best-practices/planning/redis-service-configuration.html)
- [MDVA-30102: Cache Redis ficando cheio](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/support-tools/patches/v1-0-6/mdva-30102-magento-patch-redis-cache-getting-full.html)
- [Alertas gerenciados no Adobe Commerce: alerta de aviso de memória Redis](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/support-tools/managed-alerts/managed-alerts-on-magento-commerce-redis-memory-warning-alert.html)
- [Alertas gerenciados no Adobe Commerce: alerta crítico de memória Redis](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/support-tools/managed-alerts/managed-alerts-on-magento-commerce-redis-memory-critical-alert.html)
- [Solução de problemas do Redis](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/redis-troubleshooter.html)
