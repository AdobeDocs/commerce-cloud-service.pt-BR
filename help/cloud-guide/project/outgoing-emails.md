---
title: Configurar emails de saída
description: Saiba como habilitar emails de saída para o Adobe Commerce na infraestrutura em nuvem.
exl-id: 814fe2a9-15bf-4bcb-a8de-ae288fd7f284
source-git-commit: 13e76d3e9829155995acbb72d947be3041579298
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 0%

---

# Configurar emails de saída

Você pode ativar e desativar os emails de saída para cada ambiente do [!DNL Cloud Console] ou na linha de comando. Permita que os emails de saída de ambientes de integração e de preparo enviem emails de autenticação de dois fatores ou redefinam senhas para usuários do projeto na nuvem.

Por padrão, o email de saída é ativado em ambientes de Produção. A variável [!UICONTROL Enable outgoing emails] pode parecer desativado nas configurações do ambiente, independentemente do status, até que você defina a [`enable_smtp` propriedade](#enable-emails-in-the-cli).

{{redeploy-warning}}

## Ativar emails no [!DNL Cloud Console]

Use o **[!UICONTROL Outgoing emails]** alternar no _Configurar ambiente_ exibir para ativar ou desativar o suporte por email.

**Para gerenciar o suporte de email do[!DNL Cloud Console]**:

1. Faça logon no [[!DNL Cloud Console]](https://console.adobecommerce.com).
1. Selecione um projeto na lista _Todos os projetos_ lista.
1. No painel Projeto, clique no ícone de configuração no canto superior direito.
1. Clique em **[!UICONTROL Environments]** e selecione um ambiente específico na lista.
1. Para ativar ou desativar os emails de saída, alterne _Ativar emails de saída_ **Ligado** ou **Desligado**.

   ![Habilitar configuração de email de saída](../../assets/outgoing-emails.png)

Depois de alterar a configuração, o ambiente é criado e implantado com a nova configuração.

## Habilitar emails na CLI

Você pode alterar a configuração de email de um ambiente ativo usando o `magento-cloud` CLI `environment:info` comando para definir o `enable_smtp` propriedade. Habilitar o SMTP atualiza o `MAGENTO_CLOUD_SMTP_HOST` com o endereço IP do host SMTP para enviar e-mails.

**Para gerenciar suporte a email na linha de comando**:

1. Na estação de trabalho local, altere para o diretório do projeto.

1. Verifique a configuração de email de saída do ambiente.

   ```bash
   magento-cloud environment:info -e <environment-id> | grep enable_smtp
   ```

1. Altere a configuração de suporte por email definindo o `enable_smtp` variável de ambiente para `true` ou `false`.

   ```bash
   magento-cloud environment:info --refresh -e <environment-id> enable_smtp true
   ```

   Aguarde a criação e a implantação do ambiente.

1. Use um SSH para fazer logon no ambiente remoto.

1. Verifique se o email funciona; envie um email de teste para um endereço que você possa verificar.

   ```bash
   php -r 'mail("mail@example.com", "test message", "just testing", "From: tester@example.com");'
   ```
