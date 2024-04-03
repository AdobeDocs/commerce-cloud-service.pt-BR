---
title: Configurar o serviço RabbitMQ
description: Saiba como habilitar o serviço RabbitMQ para gerenciar filas de mensagens para o Adobe Commerce na infraestrutura em nuvem.
feature: Cloud, Services
exl-id: 85794b8f-2260-4a6e-b5a6-a1b4c356594e
source-git-commit: d4c36b084094846cfad69adc2bffd567a58fab26
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 0%

---

# Configurar [!DNL RabbitMQ] serviço

A variável [Estrutura da Fila de Mensagens (MQF)](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/message-queues/message-queue-framework.html) O é um sistema da Adobe Commerce que permite [módulo](https://glossary.magento.com/module) para publicar mensagens em filas. Também define os consumidores que recebem as mensagens de forma assíncrona.

O MQF utiliza [RabbitMQ](https://www.rabbitmq.com/) como o agente de mensagens, que fornece uma plataforma escalável para enviar e receber mensagens. Também inclui um mecanismo para armazenar mensagens não entregues. [!DNL RabbitMQ] é baseado na especificação do protocolo AMQP 0.9.1.

>[!WARNING]
>
>Se preferir usar um serviço existente baseado em AMQP, como [!DNL RabbitMQ], em vez de depender do Adobe Commerce na infraestrutura em nuvem para criá-la para você, use o [`QUEUE_CONFIGURATION`](../environment/variables-deploy.md#queue_configuration) para conectá-la ao seu site.

{{service-instruction}}

**Para ativar o RabbitMQ**:

1. Adicione o nome, o tipo e o valor de disco necessário (em MB) à `.magento/services.yaml` juntamente com a versão instalada do RabbitMQ.

   ```yaml
   rabbitmq:
       type: rabbitmq:<version>
       disk: 1024
   ```

1. Configure os relacionamentos no `.magento.app.yaml` arquivo.

   ```yaml
   relationships:
       rabbitmq: "rabbitmq:rabbitmq"
   ```

1. Adicionar, confirmar e enviar por push as alterações de código.

   ```bash
   git add .magento/services.yaml .magento.app.yaml
   ```

   ```bash
   git commit -m "Enable RabbitMQ service"
   ```

   ```bash
   git push origin <branch-name>
   ```

1. [Verificar as relações de serviço](services-yaml.md#service-relationships).

{{service-change-tip}}

## Conectar-se ao RabbitMQ para depuração

Para fins de depuração, é útil se conectar diretamente a uma instância de serviço de uma das seguintes maneiras:

- Conectar-se a partir do ambiente de desenvolvimento local
- Conectar a partir do aplicativo
- Conectar a partir do aplicativo PHP

### Conectar-se a partir do ambiente de desenvolvimento local

1. Faça logon no `magento-cloud` CLI e projeto:

   ```bash
   magento-cloud login
   ```

1. Confira o ambiente com o RabbitMQ instalado e configurado.

   ```bash
   magento-cloud environment:checkout <environment-id>
   ```

1. Usar SSH para se conectar ao ambiente de nuvem:

   ```bash
   magento-cloud ssh
   ```

1. Recupere os detalhes de conexão e as credenciais de logon do RabbitMQ na [$MAGENTO_CLOUD_RELATIONSHIPS](../application/properties.md#relationships) Variável:

   ```bash
   echo $MAGENTO_CLOUD_RELATIONSHIPS | base64 -d | json_pp
   ```

   ou

   ```bash
   php -r 'print_r(json_decode(base64_decode($_ENV["MAGENTO_CLOUD_RELATIONSHIPS"])));'
   ```

   Na resposta, localize as informações do RabbitMQ, por exemplo:

   ```json
   {
      "rabbitmq" : [
         {
            "password" : "guest",
            "ip" : "246.0.129.2",
            "scheme" : "amqp",
            "port" : 5672,
            "host" : "rabbitmq.internal",
            "username" : "guest"
         }
      ]
   }
   ```

1. Ative o encaminhamento de porta local para o RabbitMQ.

   ```bash
   ssh -L <port-number>:rabbitmq.internal:<port-number> <project-ID>-<branch-ID>@ssh.us.magentosite.cloud
   ```

   Um exemplo de acesso à interface da Web de gerenciamento do RabbitMQ em `http://localhost:15672` é:

   ```bash
   ssh -L 15672:rabbitmq.internal:15672 <project-ID>-<branch-ID>@ssh.us.magentosite.cloud
   ```

1. Enquanto a sessão estiver aberta, você poderá iniciar um cliente RabbitMQ de sua escolha na estação de trabalho local, configurado para se conectar à `localhost:<portnumber>` usando as informações de número da porta, nome de usuário e senha da variável MAGENTO_CLOUD_RELATIONSHIPS.

### Conectar a partir do aplicativo

Para se conectar ao RabbitMQ em execução em um aplicativo, instale um cliente, como [amqp-utils](https://github.com/dougbarth/amqp-utils), como uma dependência de projeto no `.magento.app.yaml` arquivo.

Por exemplo,

```yaml
dependencies:
    ruby:
        amqp-utils: "0.5.1"
```

Quando você faz login em seu recipiente PHP, você digita qualquer `amqp-` comando disponível para gerenciar as filas.

### Conectar a partir do aplicativo PHP

Para conectar-se ao RabbitMQ usando seu aplicativo PHP, adicione um [biblioteca](https://glossary.magento.com/library) à árvore de origem.
