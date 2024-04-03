---
title: Implantar para preparo e produção
description: Saiba como implantar seu Adobe Commerce no código de infraestrutura em nuvem nos ambientes de preparo e produção para testes adicionais.
feature: Cloud, Console, Deploy, SCD, Storage
exl-id: 4b82289f-ee04-4b14-a0ed-7a8a19fc6a6a
source-git-commit: 13e76d3e9829155995acbb72d947be3041579298
workflow-type: tm+mt
source-wordcount: '1289'
ht-degree: 0%

---

# Implantar para preparo e produção

O processo de implantação e ativação começa com o desenvolvimento, continua com o armazenamento temporário e termina com a ativação na produção. O Adobe oferece uma solução completa de ambiente para garantir configurações consistentes. Todo ambiente suporta acesso direto de URL à loja e acesso de Admin e SSH para comandos da CLI.

Quando estiver pronto para implantar seu armazenamento, você deve concluir a implantação e o teste no ambiente de preparo antes de implantar na produção. Esta seção fornece instruções e informações detalhadas sobre o processo de criação e implantação, migração de dados e conteúdo e testes.

>[!TIP]
>
>O Adobe recomenda criar um [backup](../storage/snapshots.md) do ambiente antes das implantações.

Além disso, você pode ativar [Rastrear implantações com o New Relic](../monitor/track-deployments.md) para monitorar eventos de implantação e ajudá-lo a analisar o desempenho entre implantações.

## Fluxo de implantação inicial

O Adobe recomenda criar um `staging` ramificação da `master` para oferecer melhor suporte ao desenvolvimento e à implantação do seu plano inicial. Em seguida, dois de seus quatro ambientes ativos estarão prontos: `master` para produção e `staging` para Preparo.

Para obter informações detalhadas do processo, consulte [Iniciar desenvolvimento e implantação do fluxo de trabalho](../architecture/starter-develop-deploy-workflow.md).

## Fluxo de implantação Pro

O Pro vem com um grande ambiente de integração com duas ramificações ativas, uma global `master` ramificações, ramificações de armazenamento temporário e produção. Quando você cria seu projeto, o código está pronto para ramificar, desenvolver e enviar para a criação e implantação do site. Embora o ambiente de integração possa ter muitas ramificações, o ambiente de preparo e produção têm apenas uma ramificação para cada ambiente.

Para obter informações detalhadas do processo, consulte [Fluxo de trabalho Pro Develop and Deploy](../architecture/pro-develop-deploy-workflow.md).

## Implantar código para preparo

O ambiente de preparo fornece um ambiente de quase produção que inclui um banco de dados, um servidor da Web e todos os serviços, inclusive o Fastly e o New Relic. É possível enviar, mesclar e implantar totalmente por meio do [[!DNL Cloud Console]](../project/overview.md) ou [Comandos da CLI da nuvem](../dev-tools/cloud-cli-overview.md) por meio de um aplicativo de terminal.

### Implantar código com o [!DNL Cloud Console]

A variável [!DNL Cloud Console] O fornece recursos para criar, gerenciar e implantar código em ambientes de Integração, Preparo e Produção para planos Starter e Pro.

**Para projetos Pro, implante a ramificação de integração no preparo**:

1. [Fazer logon](https://accounts.magento.cloud) ao seu projeto.
1. Selecione o `integration` filial.
1. Selecione o **Mesclar** opção para implantar em Preparo.

   ![Mesclar](../../assets/button-merge.png){width="150"}

1. Concluir tudo [teste](../test/staging-and-production.md) no ambiente de armazenamento temporário.
1. Quando a Preparação estiver pronta, selecione a variável **Mesclar** opção para implantar na produção.

**Para Iniciante, implante a ramificação de desenvolvimento no preparo**:

1. [Fazer logon](https://accounts.magento.cloud) ao seu projeto.
1. Selecione a ramificação do código preparado.
1. Selecione o **Mesclar** opção para implantar em Preparo.

   ![Mesclar](../../assets/button-merge.png){width="150"}

1. Concluir tudo [teste](../test/staging-and-production.md) no ambiente de armazenamento temporário.
1. Quando a Preparação estiver pronta, selecione a variável **Mesclar** opção de implantação para produção (`master`).

### Implantar código com a linha de comando

A CLI da nuvem fornece comandos para implantar código. Você precisa de acesso SSH e Git para o seu projeto.

#### Etapa 1: implantar e testar o ambiente de integração

1. Depois de fazer logon no projeto, verifique o ambiente de integração:

   ```bash
   magento-cloud environment:checkout <environment-ID>
   ```

1. Sincronizar o ambiente de integração local com o ambiente remoto:

   ```bash
   magento-cloud environment:synchronize <environment-ID>
   ```

1. Crie um instantâneo do ambiente como um backup:

   ```bash
   magento-cloud snapshot: create -e <environment-ID>
   ```

1. Atualize o código na sua ramificação local, conforme necessário.

1. Adicionar, confirmar e enviar alterações para o ambiente.

   ```bash
   git add -A && git commit -m "Commit message" && git push origin <environment-ID>
   ```

1. Concluir o teste no local.

#### Etapa 2: mesclar alterações no armazenamento temporário e implantar

1. Confira o Ambiente de preparo:

   ```bash
   magento-cloud environment:checkout <environment-ID>
   ```

1. Sincronizar o ambiente de preparo local com o ambiente remoto:

   ```bash
   magento-cloud environment:synchronize <environment-ID>
   ```

1. Crie um instantâneo do ambiente como um backup:

   ```bash
   magento-cloud snapshot: create -e <environment-ID>
   ```

1. Mescle o ambiente de integração com o ambiente de preparo para implantar:

   ```bash
   magento-cloud environment:merge <integration-ID>
   ```

1. Concluir o teste no local.

#### Etapa 3: implantar para produção

1. Confira, sincronize e crie um instantâneo do seu ambiente de produção local.

1. Mescle o ambiente de preparo com a produção para implantar:

   ```bash
   magento-cloud environment:merge <staging-ID>
   ```

1. Concluir o teste no local.

## Migrar arquivos estáticos

[Arquivos estáticos](https://experienceleague.adobe.com/docs/commerce-operations/operational-playbook/glossary.html) são armazenados em `mounts`. Há dois métodos para migrar arquivos de um local de montagem de origem, como o ambiente local, para um local de montagem de destino. Ambos os métodos usam o `rsync` , mas o Adobe recomenda o uso do `magento-cloud` CLI para mover arquivos entre os ambientes local e remoto. E o Adobe recomenda usar o `rsync` ao mover arquivos de uma origem remota para um local remoto diferente.

### Migrar arquivos usando a CLI

Você pode usar o `mount:upload` e `mount:download` Comandos da CLI para migrar arquivos entre os ambientes local e remoto. Ambos os comandos usam o `rsync` , mas os comandos da CLI fornecem opções e prompts personalizados para o ambiente de infraestrutura em nuvem do Adobe Commerce. Por exemplo, se você usar o comando simples sem opções, a CLI solicitará que você selecione a montagem ou as montagens para upload ou download.

```bash
magento-cloud mount:download
```

Exemplo de resposta:

```terminal
Enter a number to choose a mount to download from:
  [0] app/etc
  [1] pub/static
  [2] var
  [3] pub/media
  [4] All mounts
 > 3

Target directory: ~/pub/media/

Downloading files from the remote mount pub/media to pub/media

Are you sure you want to continue? [Y/n] Y
```

**Para fazer upload de arquivos de um local `pub/media/` pasta para o local remoto `pub/media/` pasta do ambiente atual**:

```bash
magento-cloud mount:upload --source /path/to/project/pub/media/ --mount pub/media/
```

Exemplo de resposta:

```terminal
Uploading files from pub/media to the remote mount pub/media

Are you sure you want to continue? [Y/n] Y

  building file list ...   done
  ./
  sample-file.jpeg

  sent 8.43K bytes  received 48 bytes  3.39K bytes/sec
  total size is 154.57K  speedup is 18.23
```

Use o `--help` opção para a variável `mount:upload` e `mount:download` comandos para ver mais opções. Por exemplo, há uma variável `--delete` opção para remover arquivos irrelevantes durante a migração.

### Migrar arquivos usando rsync

Como alternativa, você pode usar o `rsync` para migrar arquivos.

```bash
rsync -azvP <source> <destination>
```

Esse comando usa as seguintes opções:

- `a`-arquivamento
- `z`-compactar arquivos durante a migração
- `v`-verboso
- `P`- progresso parcial

Consulte [rsync](https://linux.die.net/man/1/rsync) ajuda.

>[!NOTE]
>
>Para transferir mídia diretamente de ambientes remotos para remotos, você deve habilitar o encaminhamento de agente SSH. Consulte [Orientação do GitHub](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/using-ssh-agent-forwarding).

**Migrar arquivos estáticos diretamente de ambientes remotos para remotos (abordagem rápida)**:

1. Use SSH para fazer logon no ambiente de origem. Não use o `magento-cloud` CLI. Usar o `-A` opção é importante porque permite o encaminhamento da conexão do agente de autenticação.

   >[!TIP]
   >
   >Para encontrar o **Acesso SSH** link em seu [!DNL Cloud Console], selecione o ambiente e clique em **Acessar site**.

   ```bash
   ssh -A <environment_ssh_link@ssh.region.magento.cloud>
   ```

1. Use o `rsync` comando para copiar o `pub/media` de seu ambiente de origem para um ambiente remoto diferente.

   ```bash
   rsync -azvP pub/media/ <destination_environment_ssh_link@ssh.region.magento.cloud>:pub/media/
   ```

1. Faça logon em outro ambiente remoto para verificar se os arquivos foram migrados com êxito.

## Migrar o banco de dados

>[!WARNING]
>
>As operações de importação e exportação de banco de dados podem demorar muito, o que pode afetar o desempenho e a disponibilidade do site. Agende operações de importação e exportação fora do horário de pico para evitar desempenho lento ou paralisações nos sites de produção.

>[!BEGINSHADEBOX]

**Pré-requisito:** Um despejo de banco de dados (consulte a Etapa 3) deve incluir acionadores de banco de dados. Para descarregá-los, confirme se você tem a [Privilégio ACIONADOR](https://dev.mysql.com/doc/refman/5.7/en/privileges-provided.html#priv_trigger).

>[!IMPORTANT]
>
>O banco de dados do ambiente de integração é estritamente para teste de desenvolvimento e pode incluir dados que você não deseja migrar para Preparo e Produção.

Para implantações de integração contínua, o Adobe **não recomenda** migração de dados da integração para o armazenamento temporário e a produção. Você pode passar nos dados de teste ou substituir dados importantes. Todas as configurações vitais são passadas usando o [arquivo de configuração](../store/store-settings.md) e `setup:upgrade` durante a criação e implantação.

>[!ENDSHADEBOX]

Adobe **recomenda** Migração de dados da produção para o armazenamento temporário para testar totalmente seu site e armazená-lo em um ambiente de quase produção com todos os serviços e configurações.

>[!NOTE]
>
>Para transferir mídia diretamente de ambientes remotos para remotos, é necessário habilitar o encaminhamento do agente ssh, consulte [Orientação do GitHub](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/using-ssh-agent-forwarding).

### Fazer backup do banco de dados

É uma prática recomendada criar um backup do banco de dados. O procedimento a seguir utiliza a orientação do [Fazer backup do banco de dados](../storage/database-dump.md).

**Para fazer dump do banco de dados**:

1. [Usar SSH para fazer logon no ambiente remoto](../development/secure-connections.md#use-an-ssh-command) que contém o banco de dados a ser copiado.

1. Liste os relacionamentos de ambiente e observe as informações de logon do banco de dados.

   ```bash
   php -r 'print_r(json_decode(base64_decode($_ENV["MAGENTO_CLOUD_RELATIONSHIPS"]))->database);'
   ```

   Para Preparo e Produção Pro, o nome do banco de dados está no campo `MAGENTO_CLOUD_RELATIONSHIPS` (normalmente o mesmo que o nome do aplicativo e o nome de usuário).

1. Crie um backup do banco de dados. Para escolher um diretório de destino para o dump de memória, use o `--dump-directory` opção.

   Para ambientes iniciais e de integração Pro, use `main` como o nome do banco de dados:

   ```bash
   php vendor/bin/ece-tools db-dump main
   ```

   Opções de despejo:
   - `--dump-directory=<dir>`—Escolha um diretório de destino para o dump de banco de dados
   - `--remove-definers`—Remover instruções DEFINER do dump do banco de dados

1. Embora o método ECE-Tools seja preferido, outro método é criar um arquivo de despejo de banco de dados usando MySQL nativo no formato GZIP.

   ```bash
   mysqldump -h <database-host> --user=<database-username> --password=<password> --single-transaction --triggers <database-name> | gzip - > /tmp/database.sql.gz
   ```

   Se você tiver configurado a autenticação de dois fatores no ambiente de destino, é melhor excluir tabelas 2FA relacionadas para evitar a reconfiguração após a migração do banco de dados:

   ```bash
   mysqldump -h <database-host> --user=<database-username> --password=<password> --single-transaction --triggers --ignore-table=<database-name>.tfa_user_config --ignore-table=<database-name>.tfa_country_codes <database-name> | gzip - > /tmp/database.sql.gz
   ```

1. Tipo `logout` para encerrar a conexão SSH.

### Remover e recriar o banco de dados

Ao importar dados, você deve eliminar e criar um banco de dados.

**Para eliminar e recriar o banco de dados**:

1. Estabelecer um [Túnel SSH](../development/secure-connections.md#ssh-tunneling) ao ambiente remoto.

1. Conectar ao serviço de banco de dados.

   ```bash
   mysql --host=127.0.0.1 --user='<database-username>' --pass='<user-password>' --database='<name>' --port='<port>'
   ```

1. No `MariaDB [main]>` , solte o banco de dados.

   Para integração Starter e Pro:

   ```shell
   drop database main;
   ```

   Para produção:

   ```shell
   drop database <cluster-id>;
   ```

   Para Preparo:

   ```shell
   drop database <cluster-ID_stg>;
   ```

1. Recrie o banco de dados.

   Para integração Starter e Pro:

   ```shell
   create database main;
   ```

   Importar para produção:

   ```shell
   zcat <cluster-ID>.sql.gz | sed -e 's/DEFINER[ ]*=[ ]*[^*]*\*/\*/' | mysql -h 127.0.0.1 -p -u <database-username> <database-name>;
   ```

   Importar para Preparo:

   ```shell
   zcat <cluster-ID_stg>.sql.gz | sed -e 's/DEFINER[ ]*=[ ]*[^*]*\*/\*/' | mysql -h 127.0.0.1 -p -u <database-username> <database-name>;
   ```
