---
title: Configurar emails de saída
description: Saiba como habilitar emails de saída para o Adobe Commerce na infraestrutura em nuvem.
exl-id: 814fe2a9-15bf-4bcb-a8de-ae288fd7f284
source-git-commit: 59f82d891bb7b1953c1e19b4c1d0a272defb89c1
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 0%

---

# Configurar emails de saída

Você pode ativar e desativar os emails de saída para cada ambiente do [!DNL Cloud Console] ou na linha de comando. Permita que os emails de saída de ambientes de integração e de preparo enviem emails de autenticação de dois fatores ou redefinam senhas para usuários do projeto na nuvem.

Por padrão, os emails de saída são ativados nos ambientes de Produção e Preparo. No entanto, [!UICONTROL Enable outgoing emails] pode parecer desativado nas configurações do ambiente até que você defina a variável `enable_smtp` propriedade por meio da [linha de comando](#enable-emails-in-the-cli) ou [Cloud Console](outgoing-emails.md#enable-emails-in-the-cloud-console).

Atualização do [!UICONTROL enable_smtp] valor da propriedade por [linha de comando](#enable-emails-in-the-cli) também altera a [!UICONTROL Enable outgoing emails] configuração de valor para esse ambiente no Cloud Console.

{{redeploy-warning}}

## Ativar emails no Cloud Console

Use o **[!UICONTROL Outgoing emails]** alternar no _Configurar ambiente_ exibir para ativar ou desativar o suporte por email.

Se os emails de saída precisarem ser desativados ou reativados nos ambientes de Produção Pro ou de Preparo, você poderá enviar um [Tíquete de suporte do Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide).

>[!TIP]
>
>O status do email de saída pode não ser refletido para ambientes Pro no Cloud Console. Use o botão [linha de comando](#enable-emails-in-the-cli) para ativar e testar os emails de saída.

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

1. Verifique se o email foi selecionado pelo SendGrid.

   ```bash
   grep mail@example.com /var/log/mail.log
   ```
