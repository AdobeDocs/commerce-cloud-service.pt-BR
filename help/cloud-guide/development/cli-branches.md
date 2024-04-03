---
title: Gerenciar ramificações com a CLI
description: Saiba como gerenciar as ramificações de ambiente para o Adobe Commerce na infraestrutura em nuvem usando a CLI da nuvem.
role: Developer
feature: Cloud, Install
exl-id: a871c7e2-4506-4a05-8fc2-fc5ef2afe609
source-git-commit: 13e76d3e9829155995acbb72d947be3041579298
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 0%

---

# Gerenciar ramificações com a CLI

Para instalar o `magento-cloud` CLI, consulte a seção [Referência da CLI da nuvem](../dev-tools/cloud-cli-overview.md). Depois de instalar o `magento-cloud` CLI e configurar chaves SSH para acesso remoto à sua infraestrutura em nuvem, você pode usar `magento-cloud` Comandos da CLI para gerenciar os ambientes de seus projetos. Para obter informações sobre a arquitetura do ambiente, consulte [Arquitetura inicial](../architecture/starter-architecture.md) ou [Arquitetura Pro](../architecture/pro-architecture.md).

Para gerenciar ramificações e ambientes com o [!DNL Cloud Console], consulte [Gerenciar ramificações com o [!DNL Cloud Console]](../project/console-branches.md).

## Usar comandos da CLI

A variável `magento-cloud` Os comandos da CLI são semelhantes aos comandos do Git. Você pode usá-los para se conectar ao seu projeto e gerenciar seus ambientes. Embora seja possível executar os comandos a partir de qualquer diretório, é recomendável executá-los a partir de um diretório do projeto. Quando executado a partir de um diretório de projeto, você pode omitir o `-p <project-ID>` parâmetro. Consulte a [Referência da CLI da nuvem](../dev-tools/cloud-cli-overview.md).

## Clonar o projeto

As instruções a seguir usam uma combinação de `magento-cloud` Comandos CLI e Git para clonar seu projeto em sua estação de trabalho local. Para ver uma lista completa de `magento-cloud` Comandos da CLI, use o `magento-cloud list` comando.

>[!IMPORTANT]
>
>Alguns comandos do Git não podem concluir uma ação no projeto Adobe Commerce na infraestrutura em nuvem. Por exemplo, você pode criar uma ramificação usando um comando Git, mas não pode criar e ativar um novo ambiente. Você deve criar um ambiente usando o `magento-cloud environment:branch <branch-name>` comando para que o ambiente se torne _ativo_. Como alternativa, você pode usar o [!DNL Cloud Console] para criar ambientes ativos. Consulte [Referência da CLI da nuvem](../dev-tools/cloud-cli-overview.md#git-commands).

**Para clonar um projeto `master` ambiente**:

1. Efetue login na sua estação de trabalho local com uma [proprietário do sistema de arquivos](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/prerequisites/file-system/configure-permissions.html) conta.

1. Alterar para o servidor Web ou host virtual _docroot_ diretório.

1. Fazer logon usando o `magento-cloud` CLI.

   ```bash
   magento-cloud login
   ```

1. Liste seus projetos.

   ```bash
   magento-cloud project:list
   ```

1. Clonar um projeto.

   ```bash
   magento-cloud project:get <project-ID>
   ```

   Quando solicitado, forneça um nome de diretório.

1. Altere para a variável `magento2` diretório.

1. Listar ambientes disponíveis para o projeto.

   ```bash
   magento-cloud environment:list
   ```

   >[!IMPORTANT]
   >
   >A variável `magento-cloud environment:list` exibe hierarquias de ambiente, enquanto o comando `git branch` O comando não permite.

1. Busque as ramificações remotas.

   ```bash
   git fetch origin
   ```

1. Obter código atualizado.

   ```bash
   git pull origin <environment-ID>
   ```

>[!TIP]
>
>Consulte [Integrações](../integrations/overview.md) para obter informações sobre como usar os serviços de hospedagem baseados em Git com o Adobe Commerce na infraestrutura em nuvem.

## Criar uma ramificação para desenvolvimento

Depois de clonar o projeto e atualizar a configuração da conta de administrador do Adobe Commerce, você pode ramificar para desenvolvimento. Conforme dito anteriormente, você deve criar um ambiente usando o `magento-cloud environment:branch <branch-name>` ou o comando [!DNL Cloud Console] para que o ambiente se torne _ativo_.

- Para [Início](../architecture/starter-develop-deploy-workflow.md#clone-and-branch), considere criar uma ramificação para `staging`, em seguida, crie uma ramificação de desenvolvimento com base no `staging` filial.
- Para [Pro](../architecture/pro-develop-deploy-workflow.md#development-workflow), criar ramificações de desenvolvimento com base no `Integration` filial.

**Para criar uma ramificação de desenvolvimento**:

1. Na estação de trabalho local, altere para o diretório do projeto.

1. Crie um ambiente com base na ramificação recomendada para o fluxo de trabalho do projeto.

   ```bash
   magento-cloud branch <new-environment-name> integration
   ```

1. Atualizar dependências.

   ```bash
   composer --no-ansi --no-interaction install --no-progress --prefer-dist --optimize-autoloader
   ```

1. [_opcional_] Criar um [backup](../storage/snapshots.md) do ambiente.

### Mesclar uma ramificação

Após concluir o desenvolvimento, mescle esta ramificação com a principal:

1. Confirmar e enviar alterações de código:

   ```bash
   git add -A && git commit -m "Add message here"
   ```

   ```bash
   git push origin <branch-name>
   ```

1. Mesclar com o ambiente pai:

   ```bash
   magento-cloud environment:merge <environment-ID>
   ```

### Excluir um ambiente

Exclua um ambiente somente se tiver certeza de que ele não é mais necessário. Não é possível recuperar um ambiente depois de excluí-lo.

>[!WARNING]
>
>Não é possível excluir o `master` de qualquer projeto.

Você precisa ser um administrador de projeto, um administrador de ambiente ou um Proprietário da conta para executar esta tarefa. Consulte [Gerenciar o acesso do usuário aos projetos na nuvem](../project/user-access.md).

Quando você exclui um ambiente, ele é definido como _inativo_. O código ainda está disponível na ramificação Git, mas não contém mais os serviços ou o banco de dados. Para excluir o ambiente completamente, você também deve excluir a ramificação Git remota correspondente.

**Para excluir um ambiente**:

1. Na estação de trabalho local, altere para o diretório do projeto.

1. Buscar atualizações do servidor remoto.

   ```bash
   git fetch
   ```

1. Exclua a ramificação do ambiente.

   ```bash
   magento-cloud environment:delete <environment-ID>
   ```

   Como opção, é possível excluir mais de um ambiente de cada vez, adicionando várias IDs de ambiente ao comando de exclusão.

   ```bash
   magento-cloud environment:delete <environment-1-ID> <environment-2-ID>
   ```

1. Responda às solicitações para excluir o ambiente local e o ambiente remoto correspondente.

   ```terminal
   The environment <environment-ID> is currently active: deleting it will delete all associated data.
   Are you sure you want to delete the environment <environment-ID>? [Y/n]
   ```

   A exclusão do ambiente o coloca em uma _inativo_ estado.

   ```terminal
   Delete the remote Git branch too? [Y/n]
   ```

   Excluir a ramificação Git remota remove o ambiente do projeto.

1. Aguarde a exclusão do ambiente.

   ```terminal
   Deleting environment <environment-ID>
   Waiting for the activity...
     Deleting environment <project-id>-<environment-ID>-xxxxxx
   
     [============================]  1 min (complete)
   Activity ID succeeded
   Deleted remote Git branch <environment-ID>
   Run git fetch --prune to remove deleted branches from your local cache.
   ```

>[!TIP]
>
>Para ativar um ambiente inativo, use o `magento-cloud environment:activate` comando.

## Interagir com ambientes remotos

Depois que você [configurar chaves SSH](../development/secure-connections.md), você pode [conectar-se do espaço de trabalho local a um ambiente remoto](../development/secure-connections.md#connect-to-a-remote-environment) e interagir com os serviços do projeto e modificar as configurações.
