---
title: Ativar o módulo B2B
description: Saiba como habilitar o módulo empresa a empresa para Adobe Commerce na infraestrutura em nuvem.
feature: Cloud, B2B
exl-id: 01d02ea0-1e7d-4608-adbf-1dad7f5e2182
source-git-commit: bb7a866b1896a8a43d01ad3f83dc655bcf383374
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 0%

---

# Ativar o módulo B2B

Se seus clientes forem empresas, você poderá instalar o módulo B2B para Adobe Commerce para estender seu projeto Adobe Commerce on cloud infrastructure Pro para acomodar um modelo B2B para empresas. Embora este tópico forneça informações específicas para instalar e configurar o módulo B2B para o Adobe Commerce na infraestrutura em nuvem, você pode encontrar informações B2B adicionais nos seguintes guias:

- [Guia do desenvolvedor B2B do Adobe Commerce](https://developer.adobe.com/commerce/webapi/rest/b2b/)
- [Guia do usuário B2B do Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-admin/b2b/guide-overview.html)

>[!TIP]
>
>Como B2B é um módulo para Adobe Commerce na infraestrutura em nuvem, a Adobe recomenda que você implante seu aplicativo Adobe Commerce em uma integração ou ambiente de preparo antes de começar.

## Instalar módulo B2B

A Adobe recomenda trabalhar em uma ramificação de desenvolvimento ao adicionar o módulo B2B ao seu projeto. Se você não tiver uma ramificação, consulte [Criar uma ramificação para desenvolvimento](../development/cli-branches.md#create-a-branch-for-development). Ao instalar o módulo B2B, a variável `Magento_B2b` o nome do módulo é inserido automaticamente no `app/etc/config.php` arquivo. Não há necessidade de editar o arquivo diretamente.

**Para instalar o módulo B2B**:

1. Na estação de trabalho local, altere para o diretório do projeto.

1. Criar ou dar baixa em uma ramificação de desenvolvimento.

1. Adicione o módulo B2B à `require` seção do `composer.json` arquivo.

   ```bash
   composer require magento/extension-b2b --no-update
   ```

1. Atualize as dependências do projeto.

   ```bash
   composer update
   ```

1. Adicionar, confirmar e enviar alterações de código.

   ```bash
   git add -A
   ```

   ```bash
   git commit -m "Install the B2B module."
   ```

   ```bash
   git push origin <branch-name>
   ```

1. Após a conclusão da build e implantação, use o SSH para fazer logon no ambiente remoto e verificar se o módulo B2B está instalado.

   ```bash
   bin/magento module:status Magento_B2b
   ```

   Um nome de extensão usa o formato: `<VendorName>_<ComponentName>`.

   Exemplo de resposta:

   ```terminal
   Magento_B2b : Module is enabled
   ```

   Se encontrar erros de implantação, consulte [Recuperação de falha de componente](../deploy/recover-failed-deployment.md).

## Ativar o módulo B2B

Quando você instala o módulo B2B usando o Composer, o processo de implantação ativa automaticamente o módulo. Se você já tiver o módulo B2B instalado, poderá ativar ou desativar o módulo usando a CLI

Ative o módulo B2B:

```bash
bin/magento module:enable Magento_B2b
```

Exemplo de resposta:

```terminal
The following modules have been enabled:
- Magento_B2b

Cache cleared successfully.
Generated classes cleared successfully. Please run the 'setup:di:compile' command to generate classes.
Info: Some modules might require static view files to be cleared. To do this, run 'module:enable' with the --clear-static-content option to clear them.
```

Consulte [Gerenciar extensões](extensions.md).

## Configurar o módulo B2B

Depois de instalar o módulo B2B para Adobe Commerce, você deve [iniciar os consumidores de mensagem](https://experienceleague.adobe.com/docs/commerce-admin/b2b/install.html#start-message-consumers) para que você possa ativar o _Catálogo compartilhado_ e você deverá [ativar os recursos B2B](https://experienceleague.adobe.com/docs/commerce-admin/b2b/enable-basic-features.html).
