---
title: Acessar o painel de administração do Commerce
description: Saiba como acessar o painel Administrador do Commerce.
recommendations: noDisplay, catalog
exl-id: 9a8a0a49-b108-48bd-b413-ec9431370c06
source-git-commit: 85ff1283f773823ff2c6e6ab8f391fd5b4aa00e4
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---

# Acessar o painel de administração do Commerce

Os usuários que têm acesso administrativo ao painel Administrador do Commerce podem adicionar usuários, configurar serviços da loja, concluir o trabalho de configuração e personalização da loja e muito mais.

Para um novo projeto, a primeira etapa depois de receber o email de boas-vindas é proteger o acesso de Administrador ao projeto, alterando a senha na conta de Proprietário da licença. O nome de usuário padrão dessa conta é o endereço de email do Proprietário da licença.

Você pode submeter uma solicitação de alteração de senha usando um dos seguintes métodos:

- Localize o email de boas-vindas enviado ao endereço de email do Proprietário da licença, siga o link e altere sua senha.

- Copie o URL de armazenamento da [[!DNL Cloud Console]](../cloud-guide/project/overview.md) em um navegador. Em seguida, anexar `/admin` ao final do URL para abrir a página de logon. Clique em **Esqueceu a senha?** para enviar uma solicitação de alteração de senha ao endereço de email do Proprietário da licença.

Depois de enviar a solicitação de alteração de senha, verifique se há notificação de redefinição de senha no seu email. Se você não receber o email, verifique sua pasta de spam.

>[!TIP]
>
>Se a redefinição de senha falhar ou você não conseguir fazer logon no painel de Administração, um usuário com acesso de administrador poderá se conectar ao projeto usando SSH e adicionar um usuário administrador usando o `admin:user:create` comando CLI. Consulte [Criar, editar ou desbloquear uma conta de administrador](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/tutorials/admin.html) no _Guia de instalação_.
