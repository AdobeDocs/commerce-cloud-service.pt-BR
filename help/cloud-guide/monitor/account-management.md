---
title: Gerenciamento de conta da New Relic
description: Saiba como acessar sua conta do New Relic e gerenciar o acesso, as integrações e o uso de ferramentas para seu projeto do Adobe Commerce na infraestrutura em nuvem.
feature: Cloud, Observability
role: Admin
exl-id: ee639e2e-4074-4384-8f68-152bc3bac93b
source-git-commit: 13e76d3e9829155995acbb72d947be3041579298
workflow-type: tm+mt
source-wordcount: '833'
ht-degree: 0%

---

# Gerenciamento de conta do New Relic

Quando o Adobe provisiona seu projeto de infraestrutura em nuvem, o Proprietário da licença recebe um email da New Relic com credenciais e instruções para acessar a conta da New Relic. Se você não recebeu o email, use o endereço de email do Proprietário da licença para redefinir a senha do New Relic.

## Gerenciar acesso do usuário

Uma conta do New Relic pode ter somente uma pessoa atribuída à função Proprietário. Se for necessário alterar o proprietário da conta, atribua a função de Administrador ao Proprietário atual e, em seguida, atribua a função de Proprietário a outro usuário. Consulte [Atualizar o proprietário da conta](https://docs.newrelic.com/docs/accounts/original-accounts-billing/original-users-roles/users-roles-original-user-model/) no _Documentação do New Relic_ para obter instruções.

Diretrizes para gerenciar o acesso ao New Relic:

- Os Proprietários do projeto e os usuários administradores podem adicionar e remover usuários da conta do New Relic.
- Não criar mais de cinco portas de acesso completo **Usuários**.
- Conceda acesso total somente a usuários que exijam estritamente acesso ao conjunto completo de recursos.
- Não existem orientações específicas sobre a **Restrito** usuários.

>[!TIP]
>
>Antes de atribuir a função Proprietário a um usuário, verifique se o usuário existe na conta do New Relic para o Adobe Commerce na infraestrutura em nuvem. Se for necessário adicionar o usuário a essa conta e um Proprietário ou Administrador da conta existente não puder ajudar, qualquer usuário com acesso à [Conta do Proprietário da Parceria Adobe](https://account.newrelic.com/accounts/1311131/users) O para New Relic pode adicionar usuários em nome do cliente.

Adicione pelo menos um **Admin** usuário para sua conta da New Relic que pode gerenciar todo o acesso, integrações e uso de ferramentas.

**Para acessar o Gerenciamento de usuários no New Relic**:

1. Faça logon no [Conta do New Relic](https://login.newrelic.com/login).

1. Selecione seu nome de usuário na navegação inferior esquerda.

1. Clique em **[!UICONTROL Administration]** e selecione uma das seguintes opções na lista:

   - **[!UICONTROL User management]** para adicionar um usuário e gerenciar usuários ativos e convites pendentes.

   - **[!UICONTROL Access management]** para gerenciar grupos de usuários, funções e contas.

Consulte [Gerenciamento de usuários](https://docs.newrelic.com/docs/accounts/accounts-billing/new-relic-one-user-management/user-management-ui-and-tasks/) no _New Relic_ documentação.

## Configurar o New Relic para o ambiente inicial

>[!NOTE]
>
>**Ambientes profissionais** são pré-configurados para usar serviços da New Relic e podem ignorar as instruções de habilitação e conexão. Se o APM do New Relic não estiver instalado nos ambientes de preparo e produção ou se o New Relic Infrastructure não estiver disponível no ambiente de produção, [enviar um tíquete de suporte da Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) para solicitar a instalação.

Para ambientes Iniciantes, você deve verificar o `.magento.app.yaml` arquivo para verificar se o `runtime` inclui a extensão do New Relic. Se a extensão não tiver sido configurada, adicione o seguinte:

> `.magento.app.yaml`

```yaml
runtime:
    extensions:
        - newrelic
```

### Aplicar chave de licença

Para conectar um ambiente em nuvem ao New Relic, adicione a chave de licença do New Relic ao ambiente.

- Para **Projetos Pro**, o Adobe adiciona a chave de licença aos ambientes de produção e preparo durante o processo de provisionamento. Você pode fazer logon no seu [Conta do New Relic](https://login.newrelic.com/login) para verificar a conectividade entre o site de infraestrutura em nuvem do Adobe Commerce e a New Relic.

- Para **Projetos iniciais**, você tem uma chave de licença do New Relic que suporta até _três_ ambientes. Você deve adicionar a chave manualmente às configurações do ambiente. Os ambientes iniciais não são pré-provisionados para usar o serviço do New Relic.

Para ambientes Iniciantes, habilite a integração do New Relic adicionando a chave de licença do New Relic à configuração do ambiente. Adicione a chave aos ambientes de armazenamento temporário e produção e a um outro ambiente de sua escolha. Somente a chave de licença do New Relic é necessária para a configuração. Você pode encontrar informações sobre opções de configuração adicionais na [Relatórios do New Relic](https://experienceleague.adobe.com/docs/commerce-admin/config/general/new-relic-reporting.html) tópico no _Guia do usuário do Adobe Commerce_.

{{redeploy-warning}}

>[!PREREQUISITES]
>
>- Credenciais de logon para a página da conta da Adobe Commerce ou para a licença da New Relic associada ao projeto
>- [Acesso de nível administrativo](../project/user-access.md) aos ambientes Iniciais para configurar
>- Credenciais para acessar o [Admin](https://experienceleague.adobe.com/docs/commerce-admin/systems/user-accounts/permissions.html) para o ambiente

**Para configurar o New Relic para ambientes iniciais**:

1. Encontre sua chave de licença do New Relic na [!DNL Cloud Console] ou a CLI da nuvem.

   **[!DNL Cloud Console]método**:

   - Abra o projeto na nuvem [página da conta](https://accounts.magento.cloud/user).

   - No _Projetos_ localize o projeto.

   - Clique em **Exibir detalhes** para obter informações sobre a infraestrutura do projeto.

   - Expanda a **Serviço New Relic** para exibir a chave de licença.

   - Copie a chave de licença.

   **Método da CLI da nuvem**:

   ```bash
   magento-cloud subscription:info services.newrelic
   ```

1. Adicione a chave de licença do New Relic a um ambiente usando o `magento-cloud` CLI.

   - Altere para o ambiente que precisa da chave de licença.
   - Atualize o valor da variável usando o seguinte `magento-cloud` Comando da CLI:

     ```bash
     magento-cloud variable:update php:newrelic.license --value <newrelic-license-key>
     ```

   Como opção, você pode adicioná-lo a partir da [Administrador de comércio](https://experienceleague.adobe.com/docs/commerce-admin/start/reporting/new-relic-reporting.html#step-3%3A-configure-your-store).

1. Faça logon no [Conta do New Relic](https://login.newrelic.com/login) para verificar se é possível visualizar dados do ambiente do Adobe Commerce. Consulte [Investigar o desempenho](investigate-performance.md).

### Remover chave de licença

Você só pode usar sua chave de licença do New Relic em três ambientes ativos. Se a chave estiver em uso em três ambientes, remova-a de um dos ambientes antes de adicioná-la a um ambiente diferente.

**Para remover chaves de licença de ambientes**:

1. Listar variáveis de ambiente.

   ```bash
   magento-cloud variable:list
   ```

   Exemplo de resposta:

   ```terminal
    +----------------------+-------------+----------------------+---------+
    | Name                 | Level       | Value                | Enabled |
    +----------------------+-------------+----------------------+---------+
    | php:newrelic.license | environment | newrelic-license-key | true    |
    +----------------------+-------------+----------------------+---------+
   ```

   >[!WARNING]
   >
   >Se você tiver adicionado a chave de licença como _projeto_ , você deve remover essa variável de nível de projeto. Uma variável de projeto adiciona a licença ao _a cada_ ramificação de ambiente criada, que pode consumir ou exceder o limite de licença. Para listar variáveis de projeto: `magento-cloud variable:list --level project`

1. Exclua a variável de licença.

   ```bash
   magento-cloud variable:delete php:newrelic.license
   ```
