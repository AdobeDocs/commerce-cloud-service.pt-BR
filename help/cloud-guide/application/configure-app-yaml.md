---
title: Configurar implantação de aplicativo
description: Saiba como configurar as propriedades no arquivo de configuração do aplicativo que controlam a maneira como o aplicativo  [!DNL Commerce]  é compilado e implantado no ambiente de Nuvem.
feature: Cloud, Configuration, Build, Deploy
exl-id: 900da20d-98d2-4c9f-97ec-578aee775b55
source-git-commit: c9339137d957840a9ae33ed45950c613eea93660
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 0%

---

# Configurar implantação de aplicativo

O arquivo `.magento.app.yaml` controla como seu aplicativo compila e implanta. Embora o Adobe Commerce na infraestrutura em nuvem seja compatível com vários aplicativos por projeto, normalmente, um projeto tem um único aplicativo com o arquivo `.magento.app.yaml` na raiz do repositório.

O `.magento.app.yaml` tem muitos valores padrão, consulte [um arquivo `.magento.app.yaml` de exemplo](https://github.com/magento/magento-cloud/blob/master/.magento.app.yaml). Sempre revise o `.magento.app.yaml` da sua versão instalada. Esse arquivo pode diferir entre as versões do Adobe Commerce na infraestrutura em nuvem.

Use o arquivo `.magento.app.yaml` para definir os seguintes valores de configuração:

- [Propriedades](properties.md) — Defina valores de propriedade para a instância do aplicativo.
- [Propriedade de variáveis](variables-property.md) — Examine as variáveis de ambiente necessárias para a versão do aplicativo [!DNL Commerce].
- [configurações de PHP](php-settings.md)—Configure as opções de tempo de execução de PHP.
- [Definir Cache para Arquivos Estáticos](set-cache.md)—Defina o TTL de cache para sua mídia e arquivos estáticos.

>[!NOTE]
>
>O arquivo `.magento.app.yaml` é gerenciado localmente ou no repositório Git. A configuração só é lida para a finalidade do processo de implantação e criação e é removida após a conclusão da implantação, portanto, você não a encontrará no servidor.
