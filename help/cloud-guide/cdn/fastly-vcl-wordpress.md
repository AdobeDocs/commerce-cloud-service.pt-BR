---
title: Redirecionar solicitações para um back-end do CMS
description: Saiba como redirecionar solicitações recebidas de uma loja do Adobe Commerce para um site do WordPress separado usando o módulo Fastly edge.
feature: Cloud, Configuration, Routes
exl-id: 5bd9c56f-4412-4643-89b6-590a8ec65ac0
source-git-commit: 7a181af2149eef7bfaed4dd4d256b8fa19ae1dda
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 0%

---

# Redirecionar solicitações para um back-end do CMS

Redirecione solicitações de entrada de um armazenamento do Adobe Commerce para um site do WordPress separado usando o Fastly Edge Module _Other CMS/backend integration_ com um Edge Dictionary. Você pode seguir um processo semelhante para rotear novamente as solicitações para outros back-end do CMS.

Use os Módulos do Fastly Edge para criar e carregar o código de VCL personalizado do Administrador, em vez de gravar manualmente o código de VCL e carregá-lo usando a API do Fastly.

>[!NOTE]
>
>Recomendamos adicionar configurações personalizadas de VCL a um ambiente de preparo, onde você possa testá-las antes de atualizar a configuração do serviço Fastly no ambiente de Produção.

**Pré-requisitos**

{{$include /help/_includes/vcl-snippet-prerequisites.md}}

**Para rotear novamente as solicitações do Adobe Commerce para o WordPress**:

1. Ative os módulos Fastly Edge no ambiente de preparo ou produção.

   - Faça logon no Administrador.

   - Navegue até **Lojas** > Configurações > **Configuração** > **Avançado** > **Sistema** > **Cache de Página Inteira** > **Configuração Rápida** > **Configuração Avançada**.

   - Defina o valor de **Módulos do Fastly Edge** para **Sim**.

   - Salve a configuração.

1. Identifique os caminhos de URL para redirecionar para o back-end do WordPress.

1. Conclua as tarefas a seguir para configurar o serviço Fastly e criar o código VCL personalizado para rotear solicitações para o back-end do WordPress.

   - Crie um Dicionário Edge que especifica os caminhos a serem redirecionados da loja Adobe Commerce para o back-end.

   - Adicione o back-end do WordPress à configuração do serviço Fastly e anexe a condição de solicitação para as substituições de URL.

   - Configure o _Outro módulo Edge de integração CMS/back-end_ para lidar com substituições de URL do Adobe Commerce para o back-end do WordPress.

     Para obter instruções detalhadas, consulte [Fastly Edge Modules - Other CMS/Backend integration](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/Edge-Modules/EDGE-MODULE-OTHER-CMS-INTEGRATION.md) no _Fastly CDN module for Magento 2_ documentation.

1. Depois de atualizar a configuração do serviço Fastly, teste seu armazenamento no Adobe Commerce para garantir que as solicitações de URL especificadas para o WordPress sejam roteadas novamente corretamente.
