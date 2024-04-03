---
source-git-commit: 8f1ed3067f6daed897151052c8b9f987d3df3a50
workflow-type: tm+mt
source-wordcount: '93'
ht-degree: 0%

---
# Incluir arquivo para excluir VCL personalizado do Fastly

## Excluir o trecho de VCL personalizado

1. [Fazer logon](/help/get-started/onboarding.md#access-your-admin-panel) para o Administrador.

1. Clique em **Lojas** > **Configurações** > **Configuração** > **Avançado** > **Sistema**.

1. Expandir **Cache de Página Inteira** > **Configuração do Fastly** > **Trechos de VCL Personalizados**.

   ![Gerenciar trechos de VCL personalizados](/help/assets/cdn/fastly-manage-snippets.png)

1. No _Ação_ clique no ícone de lixeira ao lado do trecho a ser excluído.

1. Na próxima janela modal, clique em **DELETE** e ativar uma nova versão.

>[!WARNING]
>
>A variável _Trechos de VCL personalizados_ A opção da interface do usuário mostra apenas os trechos adicionados pelo Administrador do Adobe Commerce. Se você adicionar trechos usando a API Fastly, use a API para [gerenciá-los](/help/cloud-guide/cdn/fastly-vcl-custom-snippets.md#manage-vcl-using-the-api).
