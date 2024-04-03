---
title: Integração com o GitHub
description: Saiba como integrar seu projeto do Adobe Commerce na infraestrutura em nuvem com o GitHub.
feature: Cloud, Integration
last-substantial-update: 2023-05-25T00:00:00Z
exl-id: 5305452f-4c8d-438c-ac78-e2e1ec2f8cd9
source-git-commit: 4d32fc596064f01eaefe3ee509a655837fa846de
workflow-type: tm+mt
source-wordcount: '924'
ht-degree: 0%

---

# Integração com o GitHub

A integração do GitHub permite gerenciar o Adobe Commerce em ambientes de infraestrutura em nuvem diretamente do repositório do GitHub. A integração gerencia o conteúdo já existente no GitHub e é sincronizada com o repositório de código da infraestrutura em nuvem do Adobe Commerce. Em essência, o repositório de código se torna um espelho do repositório GitHub.

{{private-repository}}

Essa integração permite:

- Criar um ambiente ao criar uma ramificação
- Reimplante o ambiente ao mesclar uma solicitação de pull
- Excluir o ambiente ao excluir a ramificação

Você deve obter um token do GitHub e um webhook para continuar o processo.

## Pré-requisitos

- Acesso de administrador ao projeto de infraestrutura em nuvem do Adobe Commerce
- Repositório do GitHub
- Token de acesso pessoal do GitHub

## Gerar um token do GitHub

Crie um token de acesso pessoal clássico nas configurações do desenvolvedor do GitHub. Você deve ser membro de um grupo com acesso de gravação ao repositório do GitHub para poder _push_ no repositório. Inclua os seguintes escopos ao criar o token:

- `admin:repo_hook`—Criar ganchos da Web
- `repo`—Integrar ao seu repositório
- `read:org`—Integrar ao repositório organizacional

Consulte [GitHub: Create](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token).

## Preparar seu repositório

Clonar seu projeto Adobe Commerce na infraestrutura em nuvem de um ambiente existente e migrar as ramificações do projeto para um novo repositório GitHub vazio, preservando os mesmos nomes de ramificação. É necessário **crítico** para reter uma árvore Git idêntica, de modo que você não perca ambientes ou ramificações existentes no projeto do Adobe Commerce na infraestrutura em nuvem.

1. No terminal, faça logon no projeto Adobe Commerce na infraestrutura da nuvem.

   ```bash
   magento-cloud login
   ```

1. Liste os projetos e copie a ID do projeto.

   ```bash
   magento-cloud project:list
   ```

1. Clona o projeto em seu ambiente local.

   ```bash
   magento-cloud project:get <project-ID>
   ```

1. Adicione seu repositório GitHub como remoto.

   ```bash
   git remote add origin git@github.com:<user-name>/<repo-name>.git
   ```

   O nome padrão da conexão remota pode ser `origin` ou `magento`. Se `origin` existe, você pode escolher um nome diferente ou pode renomear ou excluir a referência existente. Consulte [documentação do git-remote](https://git-scm.com/docs/git-remote).

1. Verifique se você adicionou o controle remoto do GitHub corretamente.

   ```bash
   git remote -v
   ```

   Resposta esperada:

   ```terminal
   origin git@github.com:<user-name>/<repo-name>.git (fetch)
   origin git@github.com:<user-name>/<repo-name>.git (push)
   ```

1. Envie os arquivos do projeto para o novo repositório do GitHub. Lembre-se de manter todos os nomes de ramificação iguais.

   ```bash
   git push -u origin master
   ```

   Se você estiver começando com um novo repositório GitHub, talvez seja necessário usar o `-f` , pois o repositório remoto não corresponde à sua cópia local.

1. Verifique se o repositório GitHub contém todos os arquivos do projeto.

## Habilitar a integração do GitHub

Antes de começar, o código do projeto e os ambientes devem estar no repositório do GitHub. Depois de habilitar a integração, o repositório GitHub se torna a fonte de código. Se você enviar as alterações do código para o original `magento` repositório, ele é substituído pela integração quando você envia alterações de código para o repositório GitHub.

O código a seguir habilita a integração do GitHub e fornece um URL de carga útil para ser usado ao criar um webhook.

>[!WARNING]
>
>O comando a seguir substitui _all_ no seu projeto Adobe Commerce on cloud infrastructure com o código do seu repositório GitHub, que inclui todas as ramificações, incluindo a `production` filial. Essa ação acontece instantaneamente e não pode ser desfeita. Como prática recomendada, é importante clonar todas as ramificações do projeto Adobe Commerce na infraestrutura em nuvem e enviá-las para o repositório GitHub **antes** adicionar a integração do GitHub.

Você pode optar por percorrer os prompts da CLI usando `magento-cloud integration:add` ou você pode criar o comando de integração com as seguintes opções:

| Opção | Obrigatório? | Descrição |
| ----------------------- | --------- | --------------------------------- |
| `--base-url` | Sim | O URL base da instalação do servidor, que pode ser `https://github.com/` ou um personalizado. Omita esta opção se seu repositório estiver hospedado com GitHub público. |
| `--token` | Sim | O token de acesso pessoal gerado para o GitHub |
| `--repository` | Sim | O nome do repositório: `owner-or-organisation/repository` |
| `--build-pull-requests` | Opcional | Instrui o Adobe Commerce na infraestrutura em nuvem a implantar depois de mesclar uma solicitação de pull (`true` por padrão) |
| `--fetch-branches` | Opcional | Faz com que o Adobe Commerce na infraestrutura em nuvem rastreie ramificações e implante depois de atualizar uma ramificação (`true` por padrão) |
| `--prune-branches` | Opcional | Excluir ramificações que não existem no local remoto (`true` por padrão) |

Há muito mais opções e você pode vê-las usando a opção de ajuda:

```bash
magento-cloud integration:add --help
```

**Para habilitar a integração com o GitHub**:

1. Habilite a integração.

   ```bash
   magento-cloud integration:add --type=github --project=<project-ID> --token=<your-GitHub-token> {--repository=USER/REPOSITORY | --repository=ORGANIZATION/REPOSITORY} [--build-pull-requests={true|false} --fetch-branches={true|false}
   ```

   **Exemplo 1**: habilite a integração do GitHub para um repositório pessoal e privado:

   ```bash
   magento-cloud integration:add --type=github --project=ov58dlacU2e --base-url=https://github.com --token=<token> --repository=myUserName/myrepo
   ```

   **Exemplo 2**: habilite a integração do GitHub para um repositório de organização:

   ```bash
   magento-cloud integration:add --type=github --project=ov58dlacU2e --base-url=https://github.com --token=<token> --repository=Magento/teamrepo
   ```

1. Digite as informações necessárias quando solicitado.

1. Copie o **URL da carga** exibido pela saída de retorno.

   ```terminal
   Created integration <integration-ID> (type: github)
   Repository: myUserName/myrepo
   Build PRs: yes
   Fetch branches: yes
   Payload URL: https://us.magento.cloud/api/projects/<project-id>/integrations/wO8a0eoamxwcg/hook
   ```

## Adicionar o webhook no GitHub

Para comunicar eventos (como push) com o servidor Git da nuvem, você deve criar um webhook para o repositório GitHub:

1. No repositório do GitHub, clique na guia **Configurações** guia.

1. Na barra de navegação esquerda, clique em **Webhooks**.

1. No _Webhooks_ clique em **Adicionar webhook**.

1. No _Webhooks/Adicionar webhook_ formulário, edite os seguintes campos:

   - **URL da carga**: insira o URL retornado quando você ativou a integração do GitHub.
   - **Tipo de conteúdo**: Escolher **application/json** da lista.
   - **Segredo**: Insira um segredo de verificação.
   - **Quais eventos você gostaria de acionar este webhook?**: Selecionar **Envie-me tudo**.
   - Selecione o **Ativo** caixa de seleção

1. Clique em **Adicionar webhook**.

## Testar a integração

Após configurar a integração do GitHub, é possível verificar se a integração está operacional usando o `magento-cloud` CLI:

```bash
magento-cloud integration:validate
```

Ou você pode testá-lo enviando uma simples alteração ao seu repositório GitHub.

1. Criar um arquivo de teste.

   ```bash
   touch test.md
   ```

1. Confirme e envie a alteração para seu repositório GitHub.

   ```bash
   git add . && git commit -m "Testing GitHub integration" && git push
   ```

1. Faça logon no [[!DNL Cloud Console]](../project/overview.md) e verifique se a mensagem de confirmação é exibida e se o projeto está sendo implantado.

## Remover a integração

Você pode remover com segurança a integração do GitHub do seu projeto sem afetar o código.

**Para remover a integração do GitHub**:

1. No terminal, faça logon no projeto Adobe Commerce na infraestrutura da nuvem.

1. Liste suas integrações. Você precisa da ID de integração do GitHub para concluir a próxima etapa.

   ```bash
   magento-cloud integration:list
   ```

1. Exclua a integração.

   ```bash
   magento-cloud integration:delete <int-ID>
   ```

Além disso, é possível remover a integração do GitHub fazendo logon em sua conta GitHub e removendo o gancho da Web na _Webhooks_ guia do repositório _Configurações_.
