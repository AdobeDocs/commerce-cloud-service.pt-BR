---
title: Integração com bitbucket
description: Saiba como integrar seu projeto do Adobe Commerce na infraestrutura em nuvem com o Bitbucket.
feature: Cloud, Integration
exl-id: cd3cffbe-268f-429b-a2ea-0306159f4a6b
source-git-commit: 13e76d3e9829155995acbb72d947be3041579298
workflow-type: tm+mt
source-wordcount: '1020'
ht-degree: 0%

---

# Integração com bitbucket

Você pode configurar o repositório do Bitbucket para criar e implantar automaticamente um ambiente quando você envia alterações de código. Essa integração sincroniza o repositório Bitbucket com a conta do Adobe Commerce na infraestrutura em nuvem.

{{private-repository}}

## Pré-requisitos

- Acesso de administrador ao projeto de infraestrutura em nuvem do Adobe Commerce
- [`magento-cloud` CLI](../dev-tools/cloud-cli-overview.md) em seu ambiente local
- Uma conta do Bitbucket
- Acesso de administrador ao repositório do Bitbucket
- Uma chave de acesso SSH para o repositório Bitbucket

## Preparar seu repositório

Clonar seu projeto Adobe Commerce na infraestrutura em nuvem de um ambiente existente e migrar as ramificações do projeto para um novo repositório vazio de buckets, preservando os mesmos nomes de ramificações. É necessário **crítico** para reter uma árvore Git idêntica, de modo que você não perca ambientes ou ramificações existentes no projeto do Adobe Commerce na infraestrutura em nuvem.

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

1. Adicione seu repositório Bitbucket como remoto.

   ```bash
   git remote add origin git@bitbucket.org:<user-name>/<repo-name>.git
   ```

   O nome padrão da conexão remota pode ser `origin` ou `magento`. Se `origin` existe, você pode escolher um nome diferente ou pode renomear ou excluir a referência existente. Consulte [documentação do git-remote](https://git-scm.com/docs/git-remote).

1. Verifique se você adicionou o controle remoto do Bitbucket corretamente.

   ```bash
   git remote -v
   ```

   Resposta esperada:

   ```terminal
   origin git@bitbucket.org:<user-name>/<repo-name>.git (fetch)
   origin git@bitbucket.org:<user-name>/<repo-name>.git (push)
   ```

1. Envie os arquivos do projeto para o novo repositório Bitbucket. Lembre-se de manter todos os nomes de ramificação iguais.

   ```bash
   git push -u origin master
   ```

   Se você estiver começando com um novo repositório de buckets, talvez precise usar o `-f` , pois o repositório remoto não corresponde à sua cópia local.

1. Verifique se o repositório Bitbucket contém todos os arquivos de projeto.

## Criar um consumidor OAuth

A integração do Bitbucket requer uma [Consumidor do OAuth](https://support.atlassian.com/bitbucket-cloud/docs/use-oauth-on-bitbucket-cloud/). Você precisa do OAuth `key` e `secret` deste consumidor para concluir a próxima seção.

**Para criar um consumidor OAuth em um bucket**:

1. Faça logon no [Bitbucket](https://id.atlassian.com/login) conta.

1. Clique em **Configurações** > **Gerenciamento de acesso** > **OAuth**.

1. Clique em **Adicionar consumidor** e configure-a da seguinte maneira:

   ![Configuração do consumidor OAuth do Bitbucket](../../assets/oauth-consumer-config.png)

   >[!WARNING]
   >
   >Um válido **URL de retorno** não é obrigatório, mas você deve inserir um valor nesse campo para concluir a integração com êxito.

1. Clique em **Salvar**.

1. Clique no consumidor **Nome** para revelar seu OAuth `key` e `secret`.

1. Copiar seu OAuth `key` e `secret` para configurar a integração.

## Configurar a integração

1. No terminal, navegue até o projeto de infraestrutura do Adobe Commerce na nuvem.

1. Crie um arquivo temporário chamado `bitbucket.json` e adicione o seguinte, substituindo as variáveis entre colchetes angulares pelos seus valores:

   ```json
   {
     "type": "bitbucket",
     "repository": "<bitbucket-user-name/bitbucket-repo-name>",
     "app_credentials": {
       "key": "<oauth-consumer-key>",
       "secret": "<oauth-consumer-secret>"
     },
     "prune_branches": true,
     "fetch_branches": true,
     "build_pull_requests": true,
     "resync_pull_requests": true
   }
   ```

   >[!TIP]
   >
   >Certifique-se de usar o nome do repositório Bitbucket e não o URL. A integração falha se você usar um URL.

1. Adicione a integração ao seu projeto usando o `magento-cloud` Ferramenta CLI.

   >[!WARNING]
   >
   >O comando a seguir substitui _all_ no seu projeto Adobe Commerce on cloud infrastructure, codifique o código do seu repositório Bitbucket. Isso inclui todas as ramificações, incluindo a `production` filial. Essa ação acontece instantaneamente e não pode ser desfeita. Como prática recomendada, é importante clonar todas as ramificações do projeto Adobe Commerce na infraestrutura em nuvem e enviá-las para o repositório Bitbucket **antes** adicionar a integração do Bitbucket.

   ```bash
   magento-cloud project:curl -p '<project-ID>' /integrations -i -X POST -d "$(< bitbucket.json)"
   ```

   Isso retorna uma resposta HTTP longa com cabeçalhos. Uma integração bem-sucedida retorna um código de status 200 ou 201. Um status 400 ou superior indica que ocorreu um erro.

1. Exclua o temporário `bitbucket.json` arquivo.

1. Verifique a integração do projeto.

   ```bash
   magento-cloud integrations -p <project-ID>
   ```

   ```terminal
   +----------+-----------+--------------------------------------------------------------------------------+
   | ID       | Type      | Summary                                                                        |
   +----------+-----------+--------------------------------------------------------------------------------+
   | <int-id> | bitbucket | Repository: bitbucket_Account/magento-int                                      |
   |          |           | Hook URL:                                                                      |
   |          |           | https://magento-url.cloud/api/projects/<project-id>/integrations/<int-id>/hook |
   +----------+-----------+--------------------------------------------------------------------------------+
   ```

   Anote o **URL de gancho** para configurar um webhook no BitBucket.

### Adicionar um webhook no BitBucket

Para comunicar eventos (como push) com o servidor Git da Nuvem, é necessário ter um webhook para o repositório do BitBucket. O método de configuração de uma integração Bitbucket detalhado nesta página, quando seguido corretamente, cria automaticamente um webhook. É importante verificar o webhook para evitar a criação de várias integrações.

1. Faça logon no [Bitbucket](https://id.atlassian.com/login) conta.

1. Clique em **Repositórios** e selecione seu projeto.

1. Clique em **Configurações do repositório** > **Fluxo de trabalho** > **Webhooks**.

1. Verifique o webhook antes de continuar.

   Se o gancho estiver ativo, ignore as etapas restantes e [Testar a integração](#test-the-integration). O gancho deve ter um nome semelhante a **&quot;Adobe Commerce na infraestrutura em nuvem &lt;project_id>&quot;** e um formato de URL de gancho semelhante a: `https://<zone>.magento.cloud/api/projects/<project_id>/integrations/<id>/hook`

1. Clique em **Adicionar webhook**.

1. No _Adicionar novo webhook_ editar os seguintes campos:

   - **Título**: Integração do Adobe Commerce
   - **URL**: Use o URL do gancho do seu `magento-cloud` lista de integração
   - **Triggers**: o padrão é uma variável básica _Push de repositório_

1. Clique em **Salvar**.

### Testar a integração

Após configurar a integração do Bitbucket, é possível verificar se a integração está operacional usando o `magento-cloud` CLI:

```bash
magento-cloud integration:validate
```

Ou você pode testá-lo enviando uma simples alteração para o seu repositório Bitbucket.

1. Criar um arquivo de teste.

   ```bash
   touch test.md
   ```

1. Confirme e envie a alteração para o repositório Bitbucket.

   ```bash
   git add . && git commit -m "Testing Bitbucket integration" && git push
   ```

1. Faça logon no [[!DNL Cloud Console]](../project/overview.md) e verifique se a mensagem de confirmação é exibida e se o projeto está sendo implantado.

   ![Testar a integração do Bitbucket](../../assets/bitbucket-integration.png)

## Criar uma ramificação de nuvem

A integração do Bitbucket não pode ativar novos ambientes no projeto de infraestrutura do Adobe Commerce na nuvem. Se você criar um ambiente com o Bitbucket, deverá ativá-lo manualmente. Para evitar essa etapa extra, é prática recomendada criar ambientes usando o `magento-cloud` Ferramenta CLI ou o [!DNL Cloud Console].

**Para ativar uma ramificação criada com o Bitbucket**:

1. Use o `magento-cloud` CLI para enviar a ramificação.

   ```bash
   magento-cloud environment:push from-bitbucket
   ```

   ```terminal
   Pushing from-bitbucket to the new environment from-bitbucket
   Activate from-bitbucket after pushing? [Y/n] y
   Parent environment [master]: integration
   --- (Validation and activation messages)
   ```

1. Verifique se o ambiente está ativo.

   ```bash
   magento-cloud environment:list
   ```

   ```terminal
   Your environments are:
   +---------------------+----------------+--------+
   | ID                  | Name           | Status |
   +---------------------+----------------+--------+
   | master              | Master         | Active |
   |  integration        | integration    | Active |
   |    from-bitbucket * | from-bitbucket | Active |
   +---------------------+----------------+--------+
   * - Indicates the current environment
   ```

Depois de criar um ambiente, você pode enviar a ramificação correspondente para o repositório remoto do Bitbucket usando comandos Git comuns. Alterações subsequentes na ramificação no Bitbucket criam e implantam automaticamente o ambiente.

## Remover a integração

Você pode remover com segurança a integração do Bitbucket do seu projeto sem afetar o código.

**Para remover a integração do Bitbucket**:

1. No terminal, faça logon no projeto Adobe Commerce na infraestrutura da nuvem.

1. Liste suas integrações. Você precisa da ID de integração do Bitbucket para concluir a próxima etapa.

   ```bash
   magento-cloud integration:list
   ```

1. Exclua a integração.

   ```bash
   magento-cloud integration:delete <int-ID>
   ```

Além disso, você pode remover a integração do Bitbucket fazendo logon em sua conta do Bitbucket e revogando a concessão OAuth na conta _Configurações_ página.

## Integração do servidor de bitbucket

Para usar a integração do servidor Bitbucket, você precisa do seguinte:

- [Token de acesso do bitbucket](https://confluence.atlassian.com/bitbucketserver/http-access-tokens-939515499.html)—Gerar um token que concede ao Project `read` acesso e repositório `admin` acesso
- [URL do servidor Bitbucket](https://confluence.atlassian.com/bitbucketserver/specify-the-bitbucket-base-url-776640392.html)—Adicione o URL de base da sua instância do Bitbucket

Embora você possa usar a CLI da nuvem para percorrer as etapas de integração do servidor Bitbucket, o comando completo é semelhante ao seguinte:

```bash
magento-cloud integration:add --type=bitbucket_server --base-url=<bitbucket-url> --username=<username> --token=<bitbucket-access-token> --project=<project-ID>
```

Use o comando de ajuda para obter mais requisitos e opções de uso: `magento-cloud integration:add --help`
