---
title: Configurar implantação de aplicativo
description: Saiba como configurar as propriedades no arquivo de configuração do aplicativo que controlam a forma como o [!DNL Commerce] O aplicativo é criado e implantado no ambiente de nuvem.
feature: Cloud, Configuration, Build, Deploy
exl-id: 900da20d-98d2-4c9f-97ec-578aee775b55
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 0%

---

# Configurar implantação de aplicativo

A variável `.magento.app.yaml` O arquivo controla a maneira como o aplicativo cria e implanta. Embora o Adobe Commerce na infraestrutura em nuvem seja compatível com vários aplicativos por projeto, normalmente, um projeto tem um único aplicativo com o `.magento.app.yaml` arquivo na raiz do repositório.

A variável `.magento.app.yaml` tem muitos valores padrão, consulte [uma amostra `.magento.app.yaml` arquivo](https://github.com/magento/magento-cloud/blob/master/.magento.app.yaml). Sempre revisar o `.magento.app.yaml` para a versão instalada. Esse arquivo pode diferir entre as versões do Adobe Commerce na infraestrutura em nuvem.

Use o `.magento.app.yaml` arquivo para definir os seguintes valores de configuração:

- [Propriedades](properties.md)—Definir valores de propriedade para a instância do aplicativo.
- [Propriedade de variáveis](variables-property.md)—Analisar as variáveis de ambiente necessárias para o [!DNL Commerce] versão do aplicativo.
- [Configurações do PHP](php-settings.md)—Configura as opções do PHP em tempo de execução.
- [Definir Cache Para Arquivos Estáticos](set-cache.md)—Defina o TTL de cache para seus arquivos estáticos e de mídia.
