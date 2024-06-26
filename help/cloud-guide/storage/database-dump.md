---
title: Fazer backup do banco de dados
description: Saiba como usar as ferramentas ECE para criar um backup do banco de dados para um projeto de infraestrutura Adobe Commerce na nuvem.
feature: Cloud, Iaas, Storage
exl-id: 8a96effe-a587-4edf-b0c7-e73ca8d3b56c
source-git-commit: 4d790bff2ba5d02ef10de5c36a2f0d140e31a407
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 0%

---

# Fazer backup do banco de dados

É possível criar uma cópia do banco de dados usando o `ece-tools db-dump` comando sem capturar todos os dados do ambiente de serviços e montagens. Por padrão, esse comando cria backups no `/app/var/dump-main` diretório para todas as conexões de banco de dados especificadas na configuração do ambiente. A operação de despejo de BD alterna o aplicativo para o modo de manutenção, interrompe os processos de fila do consumidor e desabilita os trabalhos cron antes do início do despejo.

Considere as seguintes diretrizes para despejo de banco de dados:

- Para ambientes de produção, o Adobe recomenda concluir operações de despejo de banco de dados fora do horário de pico para minimizar as interrupções de serviço que ocorrem quando o site está no modo de manutenção.
- Se ocorrer um erro durante a operação de despejo, o comando exclui o arquivo de despejo para conservar espaço em disco. Revise os logs para obter detalhes (`var/log/cloud.log`).
- Para ambientes de produção Pro, esse comando descarta apenas do _um_ dos três nós de alta disponibilidade, portanto, os dados de produção gravados em um nó diferente durante o despejo podem não ser copiados. O comando gera um `var/dbdump.lock` arquivo para impedir que o comando seja executado em mais de um nó.
- Para um backup de todos os serviços do ambiente, a Adobe recomenda criar um [backup](snapshots.md).

Você pode optar por fazer backup de vários bancos de dados anexando os nomes dos bancos de dados ao comando. O exemplo a seguir faz backup de dois bancos de dados: `main` e `sales`:

```bash
php vendor/bin/ece-tools db-dump main sales
```

Use o `php vendor/bin/ece-tools db-dump --help` para obter mais opções:

- `--dump-directory=<dir>`—Escolha um diretório de destino para o dump de banco de dados
- `--remove-definers`—Remover instruções DEFINER do dump do banco de dados

**Para criar um dump de banco de dados no ambiente de armazenamento temporário ou de produção**:

1. [Usar SSH para fazer logon ou criar um túnel para conexão com o ambiente remoto](../development/secure-connections.md) que contém o banco de dados a ser copiado.

1. Liste os relacionamentos de ambiente e observe as informações de logon do banco de dados.

   ```bash
   echo $MAGENTO_CLOUD_RELATIONSHIPS | base64 -d | json_pp
   ```

   ou

   ```bash
   php -r 'print_r(json_decode(base64_decode($_ENV["MAGENTO_CLOUD_RELATIONSHIPS"]))->database);'
   ```

1. Crie um backup do banco de dados. Para escolher um diretório de destino para o dump de memória, use o `--dump-directory` opção.

   ```bash
   php vendor/bin/ece-tools db-dump -- main
   ```

   Exemplo de resposta:

   ```terminal
   The db-dump operation switches the site to maintenance mode, stops all active cron jobs and consumer queue processes, and disables cron jobs before starting the dump process.
   Your site will not receive any traffic until the operation completes.
   Do you wish to proceed with this process? (y/N)? y
   2020-01-28 16:38:08] INFO: Starting backup.
   [2020-01-28 16:38:08] NOTICE: Enabling Maintenance mode
   [2020-01-28 16:38:10] INFO: Trying to kill running cron jobs and consumers processes
   [2020-01-28 16:38:10] INFO: Running Magento cron and consumers processes were not found.
   [2020-01-28 16:38:10] INFO: Waiting for lock on db dump.
   [2020-01-28 16:38:10] INFO: Start creation DB dump for main database...
   [2020-01-28 16:38:10] INFO: Finished DB dump for main database, it can be found here: /tmp/qxmtlseakof6y/dump-main-1580229490.sql.gz
   [2020-01-28 16:38:10] INFO: Backup completed.
   [2020-01-28 16:38:11] NOTICE: Maintenance mode is disabled.
   ```

1. A variável `db-dump` comando cria um `dump-<timestamp>.sql.gz` arquivo no diretório remoto do projeto.

>[!TIP]
>
>Se quiser enviar esses dados para um ambiente específico, consulte [Migração de dados e arquivos estáticos](../deploy/staging-production.md#migrate-static-files).
