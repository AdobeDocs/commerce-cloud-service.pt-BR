---
title: Configurar serviços
description: Saiba como configurar serviços usados pelo Adobe Commerce na infraestrutura em nuvem.
feature: Cloud, Configuration, Services
exl-id: 48091c10-c53f-4aad-afbe-b4516653bda1
source-git-commit: 4d790bff2ba5d02ef10de5c36a2f0d140e31a407
workflow-type: tm+mt
source-wordcount: '1007'
ht-degree: 0%

---

# Configurar serviços

A variável `services.yaml` O arquivo define os serviços compatíveis e usados pelo Adobe Commerce na infraestrutura em nuvem, como MySQL, Redis e Elasticsearch ou OpenSearch. Não é necessário assinar provedores de serviços externos. Este arquivo está no estado `.magento` diretório do seu projeto.

O script de implantação usa os arquivos de configuração no `.magento` diretório para provisionar o ambiente com os serviços configurados. Um serviço se torna disponível para o seu aplicativo se estiver incluído na [`relationships`](../application/properties.md#relationships) propriedade do `.magento.app.yaml` arquivo. A variável `services.yaml` o arquivo contém o _type_ e _disco_ valores. O tipo de serviço define o serviço _name_ e _version_.

Alterar uma configuração de serviço faz com que uma implantação provisione o ambiente com os serviços atualizados, o que afeta os seguintes ambientes:

- Todos os ambientes iniciais, incluindo ambientes de produção `master`
- Ambientes de integração Pro

{{pro-update-service}}

## Serviços padrão e compatíveis

A infraestrutura em nuvem é compatível com os seguintes serviços e os implanta:

- [MySQL](mysql.md)
- [Redis](redis.md)
- [RabbitMQ](rabbitmq.md)
- [Elasticsearch](elasticsearch.md)
- [OpenSearch](opensearch.md)

É possível exibir versões padrão e valores de disco na versão atual, [padrão `services.yaml` arquivo](https://github.com/magento/magento-cloud/blob/master/.magento/services.yaml). A amostra a seguir mostra a `mysql`, `redis`, `opensearch` ou `elasticsearch`, e `rabbitmq` serviços definidos na `services.yaml` arquivo de configuração:

```yaml
mysql:
    type: mysql:10.4
    disk: 5120

redis:
    type: redis:6.2

opensearch:
    type: opensearch:2  # minor version not required; uses latest
    disk: 1024

rabbitmq:
    type: rabbitmq:3.9
    disk: 1024
```

## Valores de serviço

Você deve fornecer a ID de serviço e a configuração do tipo de serviço `type: <name>:<version>`. Se o serviço usar armazenamento persistente, você deverá fornecer um valor de disco.

Usar o seguinte formato:

```yaml
<service-id>:
    type: <name>:<version>
    disk: <value-MB>
```

### `service-id`

A variável `service-id` value identifica o serviço no projeto. Você só pode usar caracteres alfanuméricos em minúsculas: `a` para `z` e `0` para `9`, como `redis`.

Este _service-id_ o valor é usado no [`relationships`](../application/properties.md#relationships) propriedade do `.magento.app.yaml` arquivo de configuração:

```yaml
relationships:
    redis: "<name>:redis"
```

Você pode nomear várias instâncias de cada tipo de serviço. Por exemplo, você pode usar várias instâncias Redis — uma para sessão e outra para cache.

```yaml
redis:
    type: redis:<version>

redis2:
    type: redis:<version>
```

Renomear um serviço no `services.yaml` arquivo **remove permanentemente** o seguinte:

- O serviço existente antes de criar um serviço com o novo nome especificado.
- Todos os dados existentes para o serviço são removidos. A Adobe recomenda que você [fazer backup do ambiente inicial](../storage/snapshots.md) antes de alterar o nome de um serviço existente.

### `type`

A variável `type` value especifica o nome e a versão do serviço. Por exemplo:

```yaml
mysql:
    type: mysql:10.4
```

### `disk`

A variável `disk` value especifica o tamanho do armazenamento de disco persistente (em MB) a ser alocado para o serviço. Os serviços que usam armazenamento persistente, como o MySQL, devem fornecer um valor de disco. Os serviços que usam memória em vez de armazenamento persistente, como Redis, não exigem um valor de disco.

```yaml
mysql:
    type: mysql:10.4
    disk: 5120
```

A quantidade de armazenamento padrão atual por projeto é de 5 GB ou 512 0 MB. Você pode distribuir essa quantidade entre seu aplicativo e cada um de seus serviços.

## Relacionamentos de serviço

Em projetos de infraestrutura em nuvem do Adobe Commerce, o [relacionamentos](../application/properties.md#relationships) configurado no `.magento.app.yaml` determinam quais serviços estão disponíveis para o seu aplicativo.

Você pode recuperar os dados de configuração de todos os relacionamentos de serviço do [`$MAGENTO_CLOUD_RELATIONSHIPS`](../environment/variables-cloud.md) variável de ambiente. Os dados de configuração incluem o nome, o tipo e a versão do serviço, juntamente com todos os detalhes de conexão necessários, como o número da porta e as credenciais de logon.

**Para verificar relações no ambiente local**:

1. No ambiente local, mostrar as relações do ambiente ativo.

   ```bash
   magento-cloud relationships
   ```

1. Confirme a `service` e `type` da resposta. A resposta fornece informações de conexão, como endereço IP e número da porta.

   >Resposta de amostra abreviada

   ```terminal
   redis:
       -
   ...
           type: 'redis:7.0'
           port: 6379
   elasticsearch:
       -
   ...
           type: 'opensearch:2'
           port: 9200
   database:
       -
   ...
           type: 'mysql:10.6'
           port: 3306
   ```

**Para verificar relacionamentos em ambientes remotos**:

1. Use o SSH para fazer logon no ambiente remoto.

1. Listar os dados de configuração de relacionamentos para todos os serviços configurados no ambiente.

   ```bash
   echo $MAGENTO_CLOUD_RELATIONSHIPS | base64 -d | json_pp
   ```

   ou use o seguinte `ece-tools` comando para exibir relacionamentos:

   ```bash
   php ./vendor/bin/ece-tools env:config:show services
   ```

1. Confirme a `service` e `type` da resposta. A resposta fornece informações de conexão, como endereço IP e número da porta, além de quaisquer credenciais de nome de usuário e senha necessárias.

## Versões de serviço

O suporte à versão do serviço e à compatibilidade do Adobe Commerce na infraestrutura em nuvem é determinado pelas versões implantadas e testadas na infraestrutura em nuvem e, às vezes, difere das versões compatíveis com implantações locais do Adobe Commerce. Consulte [Requisitos do sistema](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/system-requirements.html) no _Instalação_ guia para obter uma lista de dependências de software de terceiros que o Adobe testou com versões específicas do Adobe Commerce e do Magento Open Source.

### Verificações de EOL de software

Durante o processo de implantação, a variável `ece-tools` O pacote verifica as versões de serviço instaladas em relação às datas de fim da vida útil (EOL) de cada serviço.

- Se uma versão do serviço estiver dentro de três meses da data EOL, uma notificação será exibida no log de implantação.
- Se a data EOL estiver no passado, uma notificação de aviso será exibida.

Para manter a segurança da loja, atualize as versões de software instaladas antes que elas atinjam o fim da vida útil. É possível revisar as datas de EOL na [ece-tools `eol.yaml` arquivo](https://github.com/magento/ece-tools/blob/develop/config/eol.yaml).

### Migrar para o OpenSearch

{{elasticsearch-support}}

Para a versão 2.4.4 e posterior do Adobe Commerce, consulte [Configurar o serviço OpenSearch](opensearch.md).

## Alterar versão do serviço

É possível atualizar a versão do serviço instalada para compatibilidade com a versão do Adobe Commerce implantada no ambiente de nuvem.

Não é possível fazer o downgrade da versão de serviço de um serviço instalado diretamente. No entanto, é possível criar um serviço com a versão necessária. Consulte [Fazer downgrade da versão do serviço](#downgrade-version).

### Atualizar versão do serviço instalado

Você pode atualizar a versão do serviço instalado atualizando a configuração do serviço no `services.yaml` arquivo.

1. Altere o [`type`](#type) valor do serviço na `.magento/services.yaml` arquivo:

   > Definição do serviço original

   ```yaml
   mysql:
       type: mysql:10.3
       disk: 2048
   ```

   > Definição de serviço atualizada

   ```yaml
   mysql:
       type: mysql:10.4
       disk: 5120
   ```

1. Adicionar, confirmar e enviar por push as alterações de código.

   ```bash
   git add .magento/services.yaml
   ```

   ```bash
   git commit -m "Upgrade MySQL from MariaDB 10.3 to 10.4."
   ```

   ```bash
   git push origin <branch-name>
   ```

### Versão de downgrade

Não é possível fazer o downgrade de um serviço instalado diretamente. Você tem duas opções:

1. Renomeie um serviço existente com a nova versão, que remove o serviço e os dados existentes, e adiciona um novo.

1. Crie um serviço e salve os dados do serviço existente.

Ao alterar a versão do serviço, você deve atualizar a configuração do serviço no `services.yaml` e atualize os relacionamentos na variável `.magento.app.yaml` arquivo.

**Para fazer downgrade de uma versão de serviço renomeando um serviço existente**:

1. Renomeie o serviço existente na `.magento/services.yaml` e altere a versão.

   >[!WARNING]
   >
   >A renomeação de um serviço existente o substitui e exclui todos os dados. Se precisar manter os dados, crie um serviço em vez de renomear o existente.

   Por exemplo, para fazer o downgrade da versão do MariaDB para o _mysql_ serviço da versão 10.4 para 10.3, altere a versão existente _service-id_ e _type_ configuração.

   > Original `services.yaml` definição

   ```yaml
   mysql:
       type: mysql:10.4
       disk: 5120
   ```

   > Novo `services.yaml` definição

   ```yaml
   mysql2:
        type: mysql:10.3
        disk: 5120
   ```

1. Atualizar as relações no `.magento.app.yaml` arquivo.

   > Original `.magento.app.yaml` configuração

   ```yaml
   relationships:
       database: "mysql:mysql"
   ```

   > Atualizado `.magento.app.yaml` configuração

   ```yaml
   relationships:
       database: "mysql2:mysql"
   ```

1. Adicionar, confirmar e enviar por push as alterações de código.

**Para fazer downgrade de um serviço criando um serviço**:

1. Adicione uma definição de serviço à `services.yaml` para o seu projeto com a especificação de versão rebaixada. Consulte _mysql2_ no exemplo a seguir:

   > services.yaml

   ```yaml
   mysql:
       type: mysql:10.4
       disk: 5120
   mysql2:
       type: mysql:10.3
       disk: 5120
   ```

1. Altere a configuração de relacionamentos na variável `.magento.app.yaml` arquivo para usar o novo serviço.

   > Original `.magento.app.yaml` configuração

   ```yaml
   relationships:
       database: "mysql:mysql"
   ```

   > Novo `.magento.app.yaml` configuração

   ```yaml
   relationships:
       database: "mysql2:mysql"
   ```

1. Adicionar, confirmar e enviar por push as alterações de código.
