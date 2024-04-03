---
title: Gerenciar acesso do usuário
description: Saiba como gerenciar o acesso de usuários ao Adobe Commerce em projetos e ambientes de infraestrutura em nuvem.
role: Admin
feature: Cloud, Roles/Permissions
last-substantial-update: 2023-06-27T00:00:00Z
topic: Security
exl-id: 3357a3ea-bf86-4a65-95d1-6b24f1152248
source-git-commit: 13e76d3e9829155995acbb72d947be3041579298
workflow-type: tm+mt
source-wordcount: '1441'
ht-degree: 0%

---

# Gerenciar acesso do usuário

Os projetos do Adobe Commerce em infraestrutura em nuvem usam acesso com base em funções. Há duas funções disponíveis no nível do projeto:

- **Administrador do projeto**—Acesso de gravação a todos os ambientes de projeto e gerenciamento de usuários, código de push e atualização das configurações do projeto.
- **Visualizador de projetos**— acesso somente para visualização a todos os ambientes de projeto.

Visualizadores de projeto não podem executar tarefas em nenhum ambiente; no entanto, você pode conceder aos visualizadores do projeto acesso de gravação a um tipo de ambiente específico.

O acesso no nível do ambiente é baseado no tipo de ambiente: produção, preparo e desenvolvimento. Conceder um usuário _visualizador_ permissão para _desenvolvimento_ ambientes significa que eles podem visualizar **all** ambientes de desenvolvimento no projeto. A tabela a seguir esclarece as habilidades concedidas a cada nível de permissão:

| Nível de permissão | Access | Acesso SSH |
| ------------------ | ----------- | :----------: |
| **Admin** | Executar tarefas de administrador, como alterar configurações, enviar código, executar tarefas e gerenciamento de ramificações, incluindo mesclagem com o ambiente pai | Sim |
| **Colaborador** | Enviar código e ramificar o ambiente; não é possível alterar as configurações ou executar ações | Sim |
| **Visualizador** | Acesso somente para visualização ao tipo de ambiente | Não |
| **Sem acesso** | Sem acesso ao tipo de ambiente | Não |

{style="table-layout:auto"}

É possível adicionar usuários e atribuir funções usando a `magento-cloud` CLI ou o [!DNL Cloud Console].

>[!BEGINSHADEBOX]

**Pré-requisitos:**

- Um usuário registrado com uma Adobe ID. Um usuário deve [registrar-se para uma conta Adobe](https://account.adobe.com) e depois [inicializar a conta da nuvem](https://console.adobecommerce.com) antes de adicioná-los a um projeto na nuvem.
- Um usuário atribuiu a **Admin** A função não pode gerenciar usuários com o `magento-cloud` CLI. Somente os usuários que recebem a função **Proprietário da conta** A função pode gerenciar usuários.

>[!ENDSHADEBOX]

## Gerenciar usuários com a CLI

Use o `magento-cloud` CLI para gerenciar usuários e integrar a sistemas automatizados:

- `magento-cloud user:add`- adicionar um usuário ao projeto
- `magento-cloud user:delete`- excluir um usuário
- `magento-cloud user:list [users]`-listar usuários de projeto
- `magento-cloud user:role`-exibir ou alterar a função de usuário
- `magento-cloud user:update`- atualizar a função do usuário em um projeto

Os exemplos a seguir usam o `magento-cloud` CLI para adicionar um usuário, configurar funções, modificar atribuições de projetos e atribuir funções de usuário.

**Para adicionar um usuário e atribuir funções**:

1. Use o `magento-cloud` CLI para adicionar o usuário.

   ```bash
   magento-cloud user:add
   ```

   >[!IMPORTANT]
   >
   >O usuário deve ter uma Adobe ID; consulte a [pré-requisitos](#add-users-and-manage-access).

1. Siga as instruções: especifique o endereço de email do usuário, defina as funções de projeto e de ambiente e adicione o usuário.

   > Exemplos de prompts

   ```terminal
   Enter the user's email address: alice@example.com
   
   Email address: alice@example.com
   
   The user's project role can be admin (a) or viewer (v).
   
   Project role (default: viewer) [a/v]: viewer
   
   The user's environment type role(s) can be admin (a), viewer (v), contributor (c) or none (n).
   
   Role on type development (default: none) [a/v/c/n]: none
   Role on type production (default: none) [a/v/c/n]: admin
   Role on type staging (default: none) [a/v/c/n]: admin
   
   Adding the user alice@example.com to (project_id):
   Project role: viewer
     Role on type production: admin
     Role on type staging: admin
   
   Are you sure you want to add this user? [Y/n] y
   Adding the user to the project
   ```

   Depois de adicionar o usuário, o Adobe envia um email para o endereço especificado com instruções para acessar o projeto Adobe Commerce na infraestrutura em nuvem.

### Exibir a função de projeto de um usuário

```bash
magento-cloud user:get alice@example.com
```

>Exemplo de resposta:

```terminal
Current role(s) of User (alice@example.com) on Production (project_id):
  Project role: admin
```

### Adicionar um usuário a vários ambientes

Para adicionar um usuário como `viewer` em um `Production` ambiente e como um `contributor` em um `Integration` ambiente:

```bash
magento-cloud user:add alice@example.com -r production:v -r integration:c
```

### Atualizar permissões de ambiente do usuário

Para atualizar as permissões de ambiente do usuário para `admin` no `Production` ambiente:

```bash
magento-cloud user:update alice@example.com -r production:a
```

## Gerenciar usuários no [!DNL Cloud Console]

Você pode usar o [[!DNL Cloud Console]](../../get-started/cloud-console.md) para adicionar permissões e usar o _Editar_ recurso para modificar permissões de um usuário existente.

>[!IMPORTANT]
>
>O usuário deve ter uma Adobe ID; consulte a [pré-requisitos](#add-users-and-manage-access).

### Adicionar um usuário ao projeto

1. Faça logon no [[!DNL Cloud Console]](https://console.adobecommerce.com/).

1. Selecione um projeto na lista _Todos os projetos_ lista.

1. No painel Projeto, clique no ícone de configuração no canto superior direito.

1. Em _Configurações do projeto_, clique em **[!UICONTROL Access]**.

1. No _Access_ clique em **[!UICONTROL Add]**.

1. Conclua o _[!UICONTROL Add User]_formulário:

   - Insira o endereço de email do usuário.

   - **[!UICONTROL Project admin]**—concede direitos de administrador a todas as configurações e tipos de ambiente.

   - **[!UICONTROL Environment types and permissions]**—conceder acesso e níveis de permissão específicos a determinados tipos de ambientes. _Sem acesso_, _Admin_ (alterar configurações, executar ação, mesclar código), _Colaborador_ (código push) ou _Visualizador_ (exibir apenas).

   >[!TIP]
   >
   >Somente um **Administrador do projeto** O pode gerenciar usuários em qualquer ambiente. Para conceder a um usuário acesso ao **Access** guia, outro **Administrador do projeto** ou o **Proprietário da conta** deve atribuir a esse usuário a função **Administrador do projeto** função.

1. Clique em **[!UICONTROL Add User]**.

1. Depois de adicionar usuários, implante novamente todos os ambientes para aplicar as alterações. Adicionar um usuário não aciona uma implantação automaticamente. A reimplantação é uma etapa importante para garantir que o usuário possa acessar um ambiente usando SSH.

Depois de adicionar o usuário, o Adobe envia um email para o endereço especificado com instruções para acessar o projeto Adobe Commerce na infraestrutura em nuvem.

## Requisitos de autenticação do usuário

Para maior segurança, o Adobe fornece imposição de autenticação multifator (MFA) no nível do projeto para exigir autenticação de dois fatores (TFA) para acesso SSH ao código-fonte e aos ambientes do projeto da infraestrutura em nuvem do Adobe Commerce. Consulte [Habilitar MFA para SSH](multi-factor-authentication.md).

Quando a imposição de MFA é habilitada em um projeto de infraestrutura do Adobe Commerce na nuvem, todos os usuários com acesso SSH a um ambiente nesse projeto devem habilitar o TFA em sua conta do Adobe Commerce na infraestrutura da nuvem. Para processos automatizados, você pode criar um usuário de máquina e um token de API para autenticar na linha de comando.

Depois de adicionar um usuário a um projeto na nuvem, peça para o usuário revisar as configurações de segurança da conta e adicionar as seguintes configurações de segurança, conforme necessário:

- **Ativar TFA**— atenda aos padrões de segurança e conformidade configurando a autenticação de dois fatores. Projetos configurados com [Imposição de MFA](multi-factor-authentication.md) exigir o TFA em contas que usam SSH para acessar os projetos.

- **Habilitar chaves SSH**— Os usuários que exigem acesso ao Adobe Commerce em repositórios de código-fonte de infraestrutura em nuvem devem habilitar chaves SSH em suas contas. Consulte [Conexões seguras](../development/secure-connections.md).

- **Criar um token de API**—Os usuários devem gerar um token de API usado para acessar SSH a um ambiente. Você precisa do token para habilitar fluxos de trabalho de autenticação para processos automatizados.

  Em projetos com imposição de MFA ativada, você deve usar o token da API para autenticar solicitações de acesso SSH de contas automatizadas. O token permite que processos automatizados ignorem workflows de autenticação que exigem o TFA.

### Ativar o TFA para contas na nuvem

O Adobe Commerce na infraestrutura em nuvem é compatível com o TFA usando qualquer um dos seguintes aplicativos:

- [Autenticador do Google (Android/iPhone)](https://support.google.com/accounts/answer/1066447?hl=en)
- [Authy (Android/iPhone)](https://authy.com/features/)
- [FreeOTP (Android)](https://play.google.com/store/apps/details?id=org.fedorahosted.freeotp)
- [GAuth Authenticator (Firefox OS, desktop, outros)](https://github.com/gbraad-apps/gauth)

As instruções para instalar o aplicativo autenticador e habilitar o TFA estão disponíveis no _Configurações da conta_ página no [!DNL Cloud Console].

**Para habilitar o TFA em sua conta de usuário**:

1. Efetue logon no [sua conta](https://console.adobecommerce.com).

1. No menu de conta superior direito, clique em **[!UICONTROL My Profile]**.

1. No _Segurança_ clique em **[!UICONTROL Set up application]**.

1. Se você não tiver um aplicativo autenticador aprovado no dispositivo móvel, use as instruções vinculadas para instalar um.

1. Adicione a conta Adobe Commerce na infraestrutura em nuvem ao aplicativo autenticador.

   - No dispositivo móvel, abra o aplicativo autenticador. Em seguida, adicione o código de configuração ao aplicativo.

   - No [!UICONTROL **[!UICONTROL TFA set up - Application]**] digite o código TFA do seu dispositivo móvel na caixa **[!UICONTROL Application verification code]** campo.

   - Clique em **[!UICONTROL Verify and save]**.

     Se o código for válido, o Adobe enviará uma notificação ao endereço de email da conta confirmando que a conta agora tem o TFA.

1. Opcional. Ativar _Navegador confiável_ configurações para armazenar o código de autenticação em cache no navegador por 30 dias.

   Essa configuração reduz o número de desafios de autenticação durante o logon no projeto.

1. Clique em **Salvar** ou **Ignorar**.

1. Salve os códigos de recuperação.

   - No _Configuração do TFA - Recuperação_ página de códigos, copie e salve os códigos de recuperação para poder fazer logon no projeto do Adobe Commerce na infraestrutura em nuvem quando não for possível acessar o dispositivo móvel ou o aplicativo de autenticação.

   - Copie os códigos de recuperação para outro local ou anote-os caso perca o acesso ao dispositivo ou ao aplicativo de autenticação.

   - Clique em **Salvar** para salvar os códigos em sua conta de modo que você possa visualizá-los e gerenciá-los nas configurações de segurança da conta.

     >[!WARNING]
     >
     >Se você perder o acesso a uma conta com o TFA e não tiver a lista de códigos de recuperação, entre em contato com o administrador do projeto ou [Enviar um tíquete de suporte da Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) para redefinir o aplicativo TFA.

1. Após concluir a configuração do TFA, clique em **Salvar** para atualizar sua conta.

1. Autentique sua sessão atual com o TFA.

   - Faça logout da sua conta.
   - Faça logon com seu nome de usuário e senha.
   - Quando solicitado, insira o código TFA para a variável `accounts.magento.cloud` entrada do aplicativo autenticador no dispositivo móvel.

### Gerenciar códigos de configuração e recuperação do TFA

Você pode gerenciar a configuração do TFA para uma conta do Adobe Commerce na infraestrutura em nuvem na _Segurança_ seção no _Meu perfil_ página.

1. Efetue logon no [sua conta](https://console.adobecommerce.com).

1. No menu de conta superior direito, clique em **[!UICONTROL My Profile]**.

1. No _Meu perfil_ clique no link **[!UICONTROL Security]** guia.

1. Use os links disponíveis para atualizar as configurações do TFA para sua conta do Adobe Commerce na infraestrutura em nuvem:

   - Desativar TFA
   - Redefinir o aplicativo autenticador
   - Adicionar ou remover navegadores confiáveis
   - Exibir ou atualizar códigos de recuperação do TFA em sua conta

### Criar um token de API

Um token de API pode ser trocado por um token de acesso OAuth 2, que pode ser usado para autenticar solicitações.

Em projetos que têm a imposição de MFA habilitada, você deve ter um token de API para habilitar o acesso SSH para usuários de máquina e processos automatizados.

>[!IMPORTANT]
>
>Valores de token da API do Protect para sua conta. Não exponha o valor em amostras de código, capturas de tela ou comunicações inseguras entre cliente e servidor. Além disso, não exponha o valor no código-fonte armazenado em repositórios públicos.

**Para criar um token de API**:

1. Efetue logon no [sua conta](https://console.adobecommerce.com).

1. No menu de conta superior direito, clique em **[!UICONTROL My Profile]**.

1. No _Meu perfil_ clique no link **[!UICONTROL API tokens]** guia.

1. Clique em **[!UICONTROL Create API token]** e insira um nome, por exemplo, especifique um nome que corresponda ao usuário do computador ou ao processo automatizado que usa o token da API.

   ![Tokens de API](../../assets/api-token-name.png)

1. Clique em **[!UICONTROL Create API token]**.
