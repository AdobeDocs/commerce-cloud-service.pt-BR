---
title: Configurar o serviço MySQL
description: Saiba como gerenciar o serviço MySQL para armazenamento de dados persistente com o Adobe Commerce na infraestrutura em nuvem.
feature: Cloud, Services, Storage
exl-id: 70820d00-8b82-4b60-87e4-ea98fd7ffcb2
source-git-commit: 9be8d1e062ab3dba86bc4d9c9ee8b8ece33d5b75
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 1%

---

# Configurar o serviço MySQL

A variável `mysql` serviço de fornece armazenamento de dados persistente com base em [MariaDB](https://mariadb.com/) versões 10.2 a 10.4, que suportam a [XtraDB](https://docs.percona.com/percona-xtradb-cluster/8.0/index.html) mecanismo de armazenamento e recursos reimplementados do MySQL 5.6 e 5.7.

A reindexação no MariaDB 10.4 leva mais tempo em comparação com outras versões do MariaDB ou MySQL. Consulte [Indexadores](https://experienceleague.adobe.com/docs/commerce-operations/performance-best-practices/configuration.html#indexers) no _Práticas recomendadas de desempenho_ guia.

>[!WARNING]
>
>Tenha cuidado ao atualizar MariaDB da versão 10.1 para 10.2. MariaDB 10.1 é a última versão que suporta _XtraDB_ como mecanismo de armazenamento. MariaDB 10.2 usa _InnoDB_ para o mecanismo de armazenamento. Depois de atualizar da versão 10.1 para a 10.2, não é possível reverter a alteração. O Adobe Commerce é compatível com ambos os mecanismos de armazenamento; no entanto, você deve verificar as extensões e outros sistemas usados pelo seu projeto para garantir que eles sejam compatíveis com o MariaDB 10.2. Consulte [Alterações incompatíveis entre 10.1 e 10.2](https://mariadb.com/kb/en/upgrading-from-mariadb-101-to-mariadb-102/#incompatible-changes-between-101-and-102).

{{service-instruction}}

**Para ativar o MySQL**:

1. Adicione o nome, o tipo e o valor de disco necessário (em MB) à `.magento/services.yaml` arquivo.

   ```yaml
   mysql:
       type: mysql:<version>
       disk: 5120
   ```

   >[!TIP]
   >
   >Erros MySQL, como `PDO Exception: MySQL server has gone away`, pode ocorrer como resultado de espaço em disco insuficiente. Verifique se você alocou espaço em disco suficiente para o serviço no [`.magento/services.yaml`](services-yaml.md#disk) arquivo.

1. Configure os relacionamentos no `.magento.app.yaml` arquivo.

   ```yaml
   relationships:
       database: "mysql:mysql"
   ```

1. Adicionar, confirmar e enviar por push as alterações de código.

   ```bash
   git add .magento/services.yaml .magento.app.yaml && git commit -m "Enable mysql service" && git push origin <branch-name>
   ```

1. [Verificar as relações de serviço](services-yaml.md#service-relationships).

{{service-change-tip}}

## Configurar banco de dados MySQL

Você tem as seguintes opções ao configurar o banco de dados MySQL:

- **`schemas`**—Um schema define um banco de dados. O schema padrão é o `main` banco de dados.
- **`endpoints`**— Cada endpoint representa uma credencial com privilégios específicos. O endpoint padrão é `mysql`, que `admin` acesso à `main` banco de dados.
- **`properties`**—As propriedades são usadas para definir configurações adicionais de banco de dados.

Veja a seguir um exemplo básico de configuração no `.magento/services.yaml` arquivo:

```yaml
mysql:
    type: mysql:10.4
    disk: 5120
    configuration:
        properties:
            optimizer_switch: "rowid_filter=off"
            optimizer_use_condition_selectivity: 1
```

A variável `properties` no exemplo acima modifica o valor padrão `optimizer` configurações como [recomendado no guia de Práticas recomendadas de desempenho](https://experienceleague.adobe.com/docs/commerce-operations/performance-best-practices/configuration.html#indexers).

**Opções de configuração do MariaDB**:

| Opções | Descrição | Valor padrão |
| -------------------- | --------------------------------------------------- | ------------------ |
| `default_charset` | O conjunto de caracteres padrão. | utf8mb4 |
| `default_collation` | O agrupamento padrão. | utf8mb4_unicode_ci |
| `max_allowed_packet` | Tamanho máximo para pacotes, em MB. Intervalo `1` para `100`. | 16 |
| `optimizer_switch` | Defina valores para o otimizador de consultas. Consulte [Documentação do MariaDB](https://mariadb.com/kb/en/server-system-variables/#optimizer_switch). | |
| `optimizer_use_condition_selectivity` | Selecione as estatísticas usadas pelo otimizador. Intervalo `1` para `5`. Consulte [Documentação do MariaDB](https://mariadb.com/kb/en/server-system-variables/#optimizer_use_condition_selectivity). | 4 para 10.4 e posterior |

### Configurar vários usuários do banco de dados

Como opção, você pode configurar vários usuários com permissões diferentes para acessar o `main` banco de dados.

Por padrão, há um endpoint chamado `mysql` que tenha acesso de administrador ao banco de dados. Para configurar vários usuários do banco de dados, você deverá definir vários endpoints no `services.yaml` arquivo e declare as relações no `.magento.app.yaml` arquivo. Para ambientes de preparo e produção profissionais, [Enviar um tíquete de suporte da Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) para solicitar o usuário adicional.

Use uma matriz aninhada para definir os endpoints de acesso do usuário específico. Cada endpoint pode designar acesso a um ou mais schemas (bancos de dados) e diferentes níveis de permissão em cada um.

Os níveis de permissão válidos são:

- `ro`: somente consultas SELECT são permitidas.
- `rw`: consultas SELECT e INSERT, UPDATE e DELETE são permitidas.
- `admin`: Todas as consultas são permitidas, incluindo consultas DDL (CREATE TABLE, DROP TABLE e muito mais).

Por exemplo:

```yaml
mysql:
    type: mysql:10.4
    disk: 5120
    configuration:
        schemas:
            - main
        endpoints:
            admin:
                default_schema: main
                privileges:
                    main: admin
            reporter:
                privileges:
                    main: ro
            importer:
                privileges:
                    main: rw
        properties:
            optimizer_switch: "rowid_filter=off"
            optimizer_use_condition_selectivity: 1
```

No exemplo anterior, a variável `admin` O endpoint fornece acesso de nível administrativo à `main` banco de dados, a variável `reporter` O endpoint fornece acesso somente leitura e a variável `importer` O endpoint fornece acesso de leitura e gravação, o que significa:

- A variável `admin` O usuário tem controle total do banco de dados.
- A variável `reporter` o usuário tem somente privilégios SELECT.
- A variável `importer` O usuário possui os privilégios SELECT, INSERT, UPDATE e DELETE.

Adicione os endpoints definidos no exemplo acima à variável `relationships` propriedade do `.magento.app.yaml` arquivo. Por exemplo:

```yaml
relationships:
    database: "mysql:admin"
    databasereporter: "mysql:reporter"
    databaseimporter: "mysql:importer"
```

>[!NOTE]
>
>Se você configurar um usuário MySQL, não poderá usar o [`DEFINER`](https://dev.mysql.com/doc/refman/8.0/en/show-grants.html) mecanismo de controle de acesso para procedimentos e visualizações armazenados.

## Conectar ao banco de dados

O acesso direto ao banco de dados do MariaDB requer que você use um SSH para fazer logon no ambiente remoto da nuvem e se conectar ao banco de dados.

1. Use o SSH para fazer logon no ambiente remoto.

   ```bash
   magento-cloud ssh
   ```

1. Recupere as credenciais de logon do MySQL da `database` e `type` propriedades na [$MAGENTO_CLOUD_RELATIONSHIPS](../application/properties.md#relationships) variável.

   ```bash
   echo $MAGENTO_CLOUD_RELATIONSHIPS | base64 -d | json_pp
   ```

   ou

   ```bash
   php -r 'print_r(json_decode(base64_decode($_ENV["MAGENTO_CLOUD_RELATIONSHIPS"])));'
   ```

   Na resposta, localize as informações do MySQL. Por exemplo:

   ```json
   "database" : [
      {
         "password" : "",
         "rel" : "mysql",
         "hostname" : "nnnnnnnn.mysql.service._.magentosite.cloud",
         "service" : "mysql",
         "host" : "database.internal",
         "ip" : "###.###.###.###",
         "port" : 3306,
         "path" : "main",
         "cluster" : "projectid-integration-id",
         "query" : {
            "is_master" : true
         },
         "type" : "mysql:10.3",
         "username" : "user",
         "scheme" : "mysql"
      }
   ],
   ```

1. Conectar ao banco de dados.

   - Para Iniciante, use o seguinte comando:

     ```bash
     mysql -h database.internal -u <username>
     ```

   - Para Pro, use o seguinte comando com nome do host, número da porta, nome de usuário e senha recuperados do `$MAGENTO_CLOUD_RELATIONSHIPS` variável.

     ```bash
     mysql -h <hostname> -P <number> -u <username> -p'<password>'
     ```

>[!TIP]
>
>Você pode usar o `magento-cloud db:sql` para conectar ao banco de dados remoto e executar comandos SQL.

## Conectar ao banco de dados secundário

>[!IMPORTANT]
>
>Esse recurso está disponível somente nos clusters Pro Production e Staging.

Às vezes, você precisa se conectar ao banco de dados secundário para melhorar o desempenho do banco de dados ou resolver problemas de bloqueio do banco de dados. Se essa configuração for necessária, use `"port" : 3304` para estabelecer a conexão. Consulte a [Prática recomendada para configurar a conexão slave do MySQL](https://experienceleague.adobe.com/docs/commerce-operations/implementation-playbook/best-practices/planning/mysql-configuration.html) tópico no _Práticas recomendadas de implementação_ guia.

## Solução de problemas

Consulte os seguintes artigos de suporte da Adobe Commerce para obter ajuda com a solução de problemas do MySQL:

- [Verificando consultas e processos lentos MySQL](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/database/checking-slow-queries-and-processes-mysql.html)
- [Criar despejo de banco de dados na nuvem](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/create-database-dump-on-cloud.html)
- [Solução de problemas da Ferramenta de migração de dados](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/data-migration-tool-troubleshooting.html)
- [Atualização do Adobe Commerce: tabelas compactas para dinâmicas 2.2.x, 2.3.x para 2.4.x](https://experienceleague.adobe.com/docs/commerce-operations/implementation-playbook/best-practices/maintenance/commerce-235-upgrade-prerequisites-mariadb.html)
