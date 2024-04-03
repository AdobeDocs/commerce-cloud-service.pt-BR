---
title: Propriedade de variáveis
description: Use a propriedade variables para personalizar as opções de configuração de armazenamento para o [!DNL Commerce] aplicação.
feature: Cloud, Configuration
exl-id: 5cd92fbb-8bff-48b1-9658-500140591344
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '72'
ht-degree: 0%

---

# Propriedade de variáveis

Você pode usar variáveis de ambiente baseadas em aplicativos para personalizar as configurações de armazenamento. Essas variáveis usam uma sintaxe específica. Consulte [Substituir definições de configuração](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/paths/override-config-settings.html) no _Guia de configuração_.

As seguintes variáveis de ambiente foram incluídas no `.magento.app.yaml` arquivos são necessários para versões específicas do [!DNL Commerce] aplicação.

Necessário para o Adobe Commerce 2.2.x a 2.3.x:

```yaml
variables:
    env:
        CONFIG__DEFAULT__PAYPAL_ONBOARDING__MIDDLEMAN_DOMAIN: 'payment-broker.magento.com'
        CONFIG__STORES__DEFAULT__PAYMENT__BRAINTREE__CHANNEL: 'Magento_Enterprise_Cloud_BT'
        CONFIG__STORES__DEFAULT__PAYPAL__NOTATION_CODE: 'Magento_Enterprise_Cloud'
```

Para o Adobe Commerce 2.4.x, defina as seguintes variáveis:

```yaml
variables:
    env:
        CONFIG__DEFAULT__PAYPAL_ONBOARDING__MIDDLEMAN_DOMAIN: 'payment-broker.magento.com'
        CONFIG__STORES__DEFAULT__PAYPAL__NOTATION_CODE: 'Magento_Enterprise_Cloud'
```
