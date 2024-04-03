---
title: Definir cache para arquivos estáticos
description: Saiba como definir opções de armazenamento em cache no [!DNL Commerce] arquivo de configuração do aplicativo.
feature: Cloud, Configuration, Cache, SCD
exl-id: ca6db004-47fc-45ea-b8db-c0ecc3c2136b
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '113'
ht-degree: 0%

---

# Definir cache para arquivos estáticos

O TTL (time-to-live) do cache para sua mídia e arquivos estáticos é definido no `.magento.app.yaml` arquivo de configuração usando o `expires` chave.

>[!NOTE]
>
>Antes de atualizar o ambiente de Produção, é importante testar as alterações no ambiente de Preparo. [Enviar um tíquete de suporte da Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) para obter ajuda com a atualização da configuração nesses ambientes.

1. Especifique o tempo de TTL (em segundos) no [`web` propriedade](web-property.md) do `.magento.app.yaml` arquivo. Você pode adicionar o `expires` chave em `locations` ou sob `"/media"` e `"/static"`.

   Para evitar que o cache expire, use o `expires: -1` par de valor-chave. Consulte o exemplo a seguir:

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
