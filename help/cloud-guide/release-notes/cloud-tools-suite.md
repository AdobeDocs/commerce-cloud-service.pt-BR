---
title: Notas de versão do Cloud Tools Suite
description: Saiba mais sobre as melhorias mais recentes do conjunto de ferramentas da nuvem para o Adobe Commerce.
feature: Cloud, Release Notes
exl-id: 6a652e93-46a2-4590-97fc-fb5d114ece9a
source-git-commit: e04a9de8f0e31098f0cc2e47112f206c11a0e23b
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 1%

---

# Notas de versão do Commerce Cloud Tools Suite

Estas informações de versão detalham as melhorias mais recentes nos pacotes do Cloud Tools Suite for Commerce, que foram projetados para implantar e gerenciar instalações e atualizações do Adobe Commerce na plataforma Cloud.

| Notas de versão | Versão | Descrição | Origem |
| ----------------- |-----------| ---------------------------------------- | --------------------------- |
| [`ece-tools` pacote](ece-tools-package.md) | 2002.1.19 | Um conjunto de scripts e ferramentas projetado para gerenciar e implantar projetos na nuvem | [`magento/ece-tools`](https://github.com/magento/ece-tools/tree/2002.1) |
| [Patches da nuvem para o Commerce](cloud-patches.md) | 1.0.27 | Um conjunto de patches que melhoram a integração de todas as versões do Adobe Commerce com ambientes na nuvem. Este pacote inclui patches do Adobe Commerce e hotfixes disponíveis que são aplicados quando você usa o `ece-tools` para implantar | [`magento/magento-cloud-patches`](https://github.com/magento/magento-cloud-patches/tree/1.0.1) |
| [Cloud Docker for Commerce](cloud-docker.md) | 1.3.7 | Arquivos de funcionalidade e configuração para imagens do Docker para implantar o Adobe Commerce em um ambiente de nuvem local | [`magento/magento-cloud-docker`](https://github.com/magento/magento-cloud-docker/tree/1.0) |
| [Componentes na nuvem do Commerce](cloud-components.md) | 1.0.14 | Funcionalidade principal estendida do Adobe Commerce para sites implantados na infraestrutura em nuvem | [`magento/magento-cloud-components`](https://github.com/magento/magento-cloud-components/tree/1.0.2) |

Ao atualizar para ECE-Tools 2002.1.0 ou posterior, você atualiza automaticamente para as versões mais recentes dos outros pacotes, que são dependências para o `ece-tools` pacote. Consulte [Metappackage da nuvem](../development/overview.md#cloud-metapackage) para obter uma lista de dependências.
