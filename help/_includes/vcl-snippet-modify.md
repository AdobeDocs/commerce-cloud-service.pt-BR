---
source-git-commit: 2d902a3926c6bbc6a9dc8afcbd667eddeaf3be7e
workflow-type: tm+mt
source-wordcount: '112'
ht-degree: 0%

---
# Incluir arquivo para modificar o VCL personalizado para o Fastly

## Modificar o trecho de VCL personalizado

1. [Fazer logon](/help/get-started/onboarding.md#access-your-admin-panel) para o Administrador.

1. Clique em **Lojas** > **Configurações** > **Configuração** > **Avançado** > **Sistema**.

1. Expandir **Cache de Página Inteira** > **Configuração do Fastly** > **Trechos de VCL Personalizados**.

   ![Gerenciar trechos de VCL personalizados](/help/assets/cdn/fastly-manage-snippets.png)

1. No _Ação_ clique no ícone de configurações ao lado do trecho a ser editado.

1. Depois que a página for recarregada, clique em **Carregar VCL para Fastly** no _Configuração do Fastly_ seção.

1. Depois que o upload for concluído, atualize o cache de acordo com a notificação na parte superior da página.

>[!WARNING]
>
>A variável _Trechos de VCL personalizados_ A opção da interface do usuário mostra apenas os trechos adicionados pelo Administrador do Adobe Commerce. Se você adicionar trechos usando a API Fastly, use a API para [gerenciá-los](/help/cloud-guide/cdn/fastly-vcl-custom-snippets.md#manage-custom-vcl-snippets-using-the-api).
