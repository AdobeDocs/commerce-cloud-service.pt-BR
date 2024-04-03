---
title: '[!DNL Onboarding] para o Commerce'
description: Acesse sua conta da nuvem e configure um projeto do Adobe Commerce na infraestrutura em nuvem.
role: Admin
recommendations: noDisplay, catalog
exl-id: c6b768d7-d835-4a8d-aad9-1c0324f7570d
source-git-commit: abe9aa36b907be8bdfdf42e6f28f1e1eac68fecf
workflow-type: tm+mt
source-wordcount: '760'
ht-degree: 0%

---

# [!DNL Onboarding] para o Commerce

Depois que o Adobe ativa uma assinatura do Commerce na infraestrutura em nuvem, o acesso inicial ao projeto e ao código fica disponível somente para a pessoa designada como o Proprietário da licença (Proprietário da conta).

O Proprietário da licença é a pessoa de sua empresa ou organização financeira que gerencia pagamentos e outras transações relacionadas ao negócio para a conta do Adobe Commerce na infraestrutura em nuvem. Essa pessoa serve como ponto de contato com o Adobe. Se precisar alterar o Proprietário da licença em sua conta, entre em contato com a Equipe de conta do Adobe.

Para integrar rapidamente seu projeto e começar a desenvolver seu site para implantação em tempo real, você deve concluir a configuração e [!DNL onboarding] tarefas. Normalmente, o Proprietário da licença inicia o processo protegendo o acesso de Administrador e criando usuários de Administração técnica que podem ajudar com o trabalho de configuração, personalização e desenvolvimento.

## Cadastrar-se em uma conta na nuvem

Se você não tiver uma conta do Adobe Commerce na infraestrutura em nuvem, entre em contato com [Vendas]. Quando você se inscreve, o Adobe cria sua conta e envia um email de boas-vindas que fornece instruções sobre como acessar a interface do projeto. O email contém um link para que você possa fazer logon em sua conta e concluir a configuração inicial do projeto.

### Nuvem [!DNL Onboarding] IU

A página Projeto do Adobe Commerce na infraestrutura em nuvem no ([!DNL Onboarding] UI) fornece uma lista de verificação de Introdução para configurar o projeto e os serviços, determinar o acesso e começar a desenvolver. No OBUI, você pode:

- Adicione um Administrador técnico, um superusuário que pode gerenciar seu projeto e ramificações
- Acesse o ambiente do projeto, incluindo um link para a [!DNL Cloud Console]
- Concluir uma lista de verificação de teste de aceitação rápida do usuário (UAT) com links para outros testes

**Para abrir a página do projeto**:

1. Faça logon no [Conta de cliente do Adobe Commerce](https://account.magento.com/customer/account/login).

1. No _Minha conta_ clique no link **[!UICONTROL Commerce]** para ver os projetos na sua conta.

1. Clique em **Exibir página do projeto** no [seção Projetos](https://cloud.magento.com/cloud/project/).

1. Clique no nome do projeto e abra a página Projeto na nuvem ([!DNL Onboarding] UI).

   ![Página do projeto OBUI](../assets/onboarding-ui.png)

   Navegue pelo portal para obter informações úteis e opções para começar a planejar seu projeto, desenvolver o código e se preparar para o UAT e o lançamento do site.

## Acessar projeto e adicionar usuários

O Proprietário da licença pode adicionar contas de usuário para fornecer acesso a código, gerenciar ramificações, inserir tíquetes e ambientes de suporte. Essas contas de usuário podem incluir especialistas internos em desenvolvimento, consultores e soluções.

Normalmente, o único usuário que o Proprietário da licença deve criar é o _Administrador técnico_. O Administrador técnico precisa de uma conta de usuário com acesso de administrador para criar contas de usuário para desenvolvedores, definir permissões de ambiente e gerenciar todas as ramificações e ambientes. O administrador técnico pode ser um desenvolvedor, um consultor e [Parceiro de soluções Adobe](https://business.adobe.com/products/magento/partners.html)ou a si mesmo.

Você pode criar um Administrador técnico por meio do Portal do projeto, no [!DNL Cloud Console]ou na linha de comando usando o `magento-cloud` CLI.

### Registro do usuário

Você só pode adicionar usuários registrados à sua Adobe Commerce em projetos e ambientes de infraestrutura em nuvem. Se você tiver um novo usuário, peça a ele para [registrar-se em uma conta](https://account.magento.com/customer/account/login/) e para fornecer o endereço de email associado ao perfil da conta.

### Acesso à conta compartilhada

O Proprietário da licença pode configurar o acesso compartilhado para a conta. O acesso compartilhado permite que funcionários confiáveis e provedores de serviços usem a central de ajuda para enviar e rastrear tíquetes de suporte relacionados à sua Adobe Commerce em projetos de infraestrutura em nuvem. Para obter instruções de configuração, consulte [Acesso compartilhado] artigo na Central de ajuda.

### [!DNL Cloud Console]

Você pode usar o [[!DNL Cloud Console]](cloud-console.md) para gerenciar seu projeto, adicionar contas de usuário e começar a desenvolver sua loja. O Proprietário da licença, os usuários dos Administradores técnicos e os desenvolvedores podem usar o [!DNL Cloud Console] para gerenciar todos os ambientes e ramificações, variáveis de ambiente, configurações de ambiente e rotas.

**Para acessar o[!DNL Cloud Console]**:

1. Efetue logon no [Minha conta](https://account.magento.com/customer/account/login).

1. No _Minha conta_ clique no link **[!UICONTROL Commerce]** para ver os projetos na sua conta.

1. Clique em **Projetos** e selecione um projeto.

1. Clique em **Acesso à infraestrutura** e clique em **Acesso ao Projeto (Interface do Usuário da Web)**.

   ![Portal de projetos na nuvem](../assets/obui-project-access.png)

## Inscrever-se para obter o status do Adobe

Obtenha atualizações sobre o Adobe Commerce em ambientes de plataforma de infraestrutura em nuvem e serviços relacionados do [Página de status].

A página fornece um status para componentes e serviços do Adobe Commerce, seguido de notificações sobre relatórios de incidentes, atualizações de serviço, interrupções planejadas e manutenção programada. Qualquer pessoa que trabalhe no seu projeto pode assinar o site de status da Adobe Commerce para receber notificações e atualizações de eventos por email ou Slack. Você pode personalizar a assinatura do status do Adobe para rastrear produtos específicos por regiões e eventos.

>[!TIP]
>
> Abra o novo [!DNL Cloud Console] e exibir atividades de projeto e ambiente.
>
>**Próxima etapa**: [Fazer logon no Console Cl[!DNL ] oud](cloud-console.md)

<!-- link definitions -->

[Vendas]: https://business.adobe.com/products/magento/get-demo.html
[Acesso compartilhado]: https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#shared-access
[Página de status]: https://status.adobe.com/products/503473
