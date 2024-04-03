---
title: CLI da nuvem
description: Saiba mais sobre a CLI da magento-cloud e como ela ajuda você a gerenciar ambientes de desenvolvimento locais para seu projeto de infraestrutura do Adobe Commerce na nuvem.
exl-id: 70dddd62-0269-4af4-bd2a-1a4fbf11a131
source-git-commit: 13e76d3e9829155995acbb72d947be3041579298
workflow-type: tm+mt
source-wordcount: '741'
ht-degree: 0%

---


# CLI da nuvem

A variável `magento-cloud` A ferramenta CLI permite que desenvolvedores e administradores de sistema gerenciem projetos e ambientes na nuvem, executem rotinas e executem tarefas de automação. A variável `magento-cloud` A CLI amplia os recursos e a funcionalidade do [[!DNL Cloud Console]](../../get-started/cloud-console.md). Depois de instalar o `magento-cloud` A CLI na estação de trabalho local permite que você a use para gerenciar os ambientes de integração do Adobe Commerce na infraestrutura em nuvem Starter e Pro.

**Para instalar o `magento-cloud` CLI**:

1. Na estação de trabalho local, altere para o diretório onde você pretende clonar o projeto na nuvem e onde a variável [proprietário do sistema de arquivos](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/prerequisites/file-system/configure-permissions.html) tem _gravação_ acesso.

1. Instale o `magento-cloud` CLI.

   ```bash
   curl -sS https://accounts.magento.cloud/cli/installer | php
   ```

1. Adicionar `magento-cloud` CLI para o perfil bash.

   ```bash
   export PATH=$PATH:$HOME/.magento-cloud/bin
   ```

1. Recarregue o perfil bash atualizado.

   ```bash
   . ~/.bash_profile
   ```

1. Para iniciar a CLI, chame `magento-cloud` e insira suas credenciais da Conta da nuvem quando solicitado.

   ```bash
   magento-cloud
   ```

   ```terminal
   Welcome to Magento Cloud!
   Please log in using your Magento Cloud account.
   Your email address or username:
   ```

1. Verifique se `magento-cloud` está no seu caminho. O exemplo a seguir lista os comandos disponíveis.

   ```bash
   magento-cloud list
   ```

## Comandos comuns

O Adobe projetou esses comandos para gerenciar ambientes de integração na nuvem e recomenda que você execute o `magento-cloud` CLI de um diretório de projeto para que você possa omitir o `-p <project-ID>` parâmetro.

A seguinte lista de `magento-cloud` Os comandos da CLI incluem apenas as opções necessárias. Você pode usar o `--help` com qualquer comando para ver mais informações.

| Comando | Descrição |
| ------------------------------------ | -------------------------------------------------- |
| `magento-cloud login` | Faça logon no projeto. |
| `magento-cloud list` | Liste os comandos disponíveis para a ferramenta CLI. |
| `magento-cloud environment:list` | Listar os ambientes no projeto atual. |
| `magento-cloud environment:checkout` | Confira um ambiente existente. |
| `magento-cloud environment:merge -e` | Mesclar alterações neste ambiente com seu pai. |
| `magento-cloud variables` | Variáveis de lista neste ambiente. |
| `magento-cloud ssh` | Use o SSH para se conectar ao ambiente remoto. |
| `magento-cloud url` | Abra a loja do Adobe Commerce em um navegador. |
| `magento-cloud web` | Abra o [!DNL Cloud Console]. |

## Comandos de ambiente

O ambiente _name_ é diferente do ambiente _ID_ somente se você usar espaços ou letras maiúsculas no nome do ambiente. Uma ID de ambiente consiste em todas as letras minúsculas, números e símbolos permitidos. Letras maiúsculas em um nome de ambiente são convertidas em minúsculas na ID; espaços em um nome de ambiente são convertidos em traços.

Um nome de ambiente _não é possível_ inclui caracteres reservados para o shell do Linux ou para expressões regulares. Os caracteres proibidos incluem chaves (`{ }`), parênteses, asterisco (`*`), colchetes angulares (`< >`), e comercial (`&`), porcentagem (`%`) e outros caracteres.

A variável `magento-cloud environment:list` exibe hierarquias de ambiente, enquanto `git branch` não. Se você tiver ambientes aninhados, use o seguinte:

```bash
magento-cloud environment:list
```

### Reimplantação do ambiente

Acione uma reimplantação sem usar um push. Verifique e confirme o ambiente para reimplantação. Não use a reimplantação se houver uma build em um estado pendente.

```bash
magento-cloud environment:redeploy
```

Exemplo de resposta:

```terminal
Are you sure you want to redeploy the environment <environment-name>? [Y/n]
```

{{redeploy-warning}}

## Comandos do Git

Você pode notar que alguns desses comandos são semelhantes aos comandos do Git. A variável `magento-cloud` Os comandos do se conectam diretamente ao projeto da Nuvem baseada em Git com recursos adicionais. Se você criar uma ramificação sem usar a variável `magento-cloud` A CLI não é &quot;ativada&quot; e não é criada automaticamente quando você envia alterações para o ambiente remoto. A variável `magento-cloud` O comando CLI inclui ativação.

Para criar uma ramificação, use o `magento-cloud` para que a ramificação seja ativada.

```bash
magento-cloud environment:branch <new-name> <parent-branch>
```

Para status da filial:

- Use o `magento-cloud env` comando para exibir uma lista das ramificações de ambiente e seu status: ativo ou inativo.
- Use o `magento-cloud environment:activate` comando para ativar uma ramificação de ambiente.

Envie uma confirmação do Git vazia para acionar uma implantação. Por exemplo:

```bash
git commit --allow-empty -m "redeploy" && git push <branch-name>
```

Algumas ações, como adicionar um usuário, não resultam na implantação.

### Criar uma ramificação de ambiente

As etapas a seguir demonstram o uso dos comandos CLI e Git alternadamente para gerenciar o ambiente local:

1. Na estação de trabalho local, altere para o diretório do projeto.

1. Alterne para a [proprietário do sistema de arquivos](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/prerequisites/file-system/configure-permissions.html).

1. Faça logon no projeto.

   ```bash
   magento-cloud login
   ```

1. Liste seus projetos.

   ```bash
   magento-cloud project:list
   ```

1. Listar ambientes no projeto. Todos os ambientes incluem uma ramificação Git ativa que contém seu código, banco de dados, variáveis de ambiente, configurações e serviços.

   ```bash
   magento-cloud environment:list
   ```

   >[!NOTE]
   >
   >É importante usar a variável `magento-cloud environment:list` porque exibe hierarquias de ambiente, enquanto o comando `git branch` O comando não permite.

1. Busque ramificações de origem para obter o código mais recente.

   ```bash
   git fetch origin
   ```

1. Fazer check-out ou alternar para uma ramificação e um ambiente específicos.

   ```bash
   magento-cloud environment:checkout <environment-ID>
   ```

   Os comandos do Git só verificam a ramificação Git. A variável `magento-cloud checkout` O comando verifica a ramificação e alterna para o ambiente ativo.

   >[!TIP]
   >
   >É possível criar uma ramificação de ambiente usando a variável `magento-cloud environment:branch <environment-name> <parent-environment-ID>` sintaxe de comando. Pode levar algum tempo adicional para criar e ativar uma ramificação de ambiente.

1. Use a ID de ambiente para enviar qualquer código atualizado para o local. Isso não será necessário se a ramificação do ambiente for nova.

   ```bash
   git pull origin <environment-ID>
   ```

1. (_Opcional_) Criar um [instantâneo](../storage/snapshots.md) do ambiente como um backup.

   ```bash
   magento-cloud snapshot:create -e <environment-ID>
   ```

## Atualizar a CLI

A variável `magento-cloud` A CLI verifica as atualizações disponíveis ao fazer logon, mas você pode verificar atualizações usando o `self:update` comando. Se houver uma atualização disponível, siga as instruções para atualizar a CLI.

Se o seu `magento-cloud` A CLI está atualizada, você verá a seguinte resposta:

```bash
magento-cloud update
```

```terminal
Checking for Magento Cloud CLI updates (current version: X.XX.X)
No updates found
```
