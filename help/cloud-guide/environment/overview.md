---
title: Visão geral dos arquivos de configuração
description: Saiba mais sobre como configurar o ambiente de infraestrutura em nuvem para oferecer suporte à implantação e ao gerenciamento de sua loja personalizada do Adobe Commerce.
feature: Cloud, Configuration, Services, Iaas, Paas
exl-id: f469a0ec-e459-413f-9725-66a0fbf34f01
source-git-commit: 47b66d0d2bbff14e76ce49182a68d5e6c9fb13a7
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---

# Visão geral dos arquivos de configuração

Os ambientes do Adobe Commerce na infraestrutura em nuvem incluem contêineres com aplicativos, serviços e um banco de dados para fornecer um sistema completo para sua base de código e arquivos de aplicativo do Adobe Commerce.

Você pode definir configurações de aplicativo, rotas, criar e implantar ações e notificações para dar suporte aos ambientes do projeto usando os seguintes arquivos de configuração:

| Configuração | Nome do arquivo | Descrição |
| ------------- | -------- | ----------- |
| [Aplicativo](../application/configure-app-yaml.md) | `.magento.app.yaml` | Define como criar e implantar o Adobe Commerce, incluindo serviços, ganchos e trabalhos cron. |
| [Ambiente](configure-env-yaml.md) | `.magento.env.yaml` | Centraliza o gerenciamento de ações de criação e implantação em todos os seus ambientes, incluindo o armazenamento temporário e a produção profissionais, usando variáveis de ambiente. |
| [Rotas](../routes/routes-yaml.md) | `.magento/routes.yaml` | Configurar armazenamento em cache, redirecionamentos e inclusões do lado do servidor. |
| [Serviço](../services/services-yaml.md) | `.magento/services.yaml` | Define os serviços que a Adobe Commerce usa por nome e versão. Por exemplo, este arquivo pode incluir versões de MariaDB, extensões PHP, Redis, RabbitMQ e Elasticsearch ou OpenSearch. Você deve abrir um tíquete de suporte para enviar essas alterações para os ambientes de preparo e produção do plano Pro. |
| [Configurações do PHP](../application/php-settings.md#configure-php) | `php.ini` | Um arquivo opcional que pode ser adicionado ao projeto. As configurações contidas nesse arquivo são anexadas às mantidas pela infraestrutura de nuvem. |

{style="table-layout:auto"}

## Atualizações de configuração para ambientes Pro

Para ambientes de preparo e produção profissionais da infraestrutura em nuvem do Adobe Commerce, você pode atualizar muitas opções de configuração em seu ambiente de desenvolvimento local e confirmar as alterações para aplicá-las a esses ambientes. No entanto, você deve [Enviar um tíquete de suporte da Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) para atualizar as seguintes opções de configuração:

- Instalar ou atualizar serviços no `.magento/services.yaml` arquivo.
- Altere a configuração da variável `mounts` e `disk` propriedades na `.magento.app.yaml` arquivo.

{{pro-self-service-warning}}
