---
title: Definir cache para arquivos estáticos
description: Saiba como definir opções de armazenamento em cache no arquivo de configuração do aplicativo  [!DNL Commerce] .
feature: Cloud, Configuration, Cache, SCD
exl-id: ca6db004-47fc-45ea-b8db-c0ecc3c2136b
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '113'
ht-degree: 0%

---

# Definir cache para arquivos estáticos

O TTL (tempo de vida útil) de cache para seus arquivos de mídia e estáticos está definido no arquivo de configuração `.magento.app.yaml` usando a chave `expires`.

>[!NOTE]
>
>Antes de atualizar o ambiente de Produção, é importante testar as alterações no ambiente de Preparo. [Envie um tíquete de Suporte da Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) para obter ajuda para atualizar a configuração nesses ambientes.

1. Especifique o tempo de TTL (em segundos) na propriedade [`web` ](web-property.md) do arquivo `.magento.app.yaml`. Você pode adicionar a chave `expires` em `locations` ou em `"/media"` e `"/static"`.

   Para evitar que o cache expire, use o par de valor-chave `expires: -1`. Consulte o exemplo a seguir:

   ```yaml
   # The configuration of app when it is exposed to the web.
   web:
     locations:
       "/media":
         ...
         expires: -1
   
       "/static":
         ...
         expires: -1
   ```

1. Adicionar, confirmar e enviar por push as alterações de código.

   ```bash
   git add -A && git commit -m "Set cache TTL for static files" && git push origin <branch-name>
   ```
