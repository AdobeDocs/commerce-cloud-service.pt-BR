---
title: Arquitetura em nuvem do Commerce
description: Saiba como as arquiteturas de projeto Starter e Pro contrastam com a infraestrutura do Commerce on Cloud.
feature: Cloud, Iaas, Paas
topic: Architecture
recommendations: noDisplay
exl-id: 37cd6733-c10a-4d06-b784-171da576f9fc
source-git-commit: 1253d8357fd2554050d1775fefbc420a2097db5f
workflow-type: tm+mt
source-wordcount: '745'
ht-degree: 0%

---

# Arquitetura em nuvem do Commerce

A infraestrutura do Adobe Commerce na nuvem tem um plano Starter e um Pro. Cada plano tem uma arquitetura exclusiva para orientar o processo de desenvolvimento e implantação do Adobe Commerce. Tanto o plano Starter quanto a arquitetura de plano Pro implantam bancos de dados, servidores da Web e servidores de cache em vários ambientes para testes completos e, ao mesmo tempo, oferecem suporte à integração contínua.

Para comparação, cada plano inclui os seguintes recursos de infraestrutura e produtos compatíveis.

|          | Início | Pro |
| -------- | --------------------| ------------------ |
| Recursos principais | <ul><li>[Todos os recursos do Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-operations/release/features.html)</li><li>Ferramenta de integração do PayPal</li><li>[Relatórios do Commerce](https://business.adobe.com/products/magento/business-intelligence.html?_ga=2.85288604.442698376.1665067470-1322106587.1655147209)</li></ul> | <ul><li>[Todos os recursos do Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-operations/release/features.html)</li><li>Ferramenta de integração do PayPal</li><li>[Relatórios do Commerce](https://business.adobe.com/products/magento/business-intelligence.html?_ga=2.85288604.442698376.1665067470-1322106587.1655147209)</li><li>[Módulo B2B](https://business.adobe.com/products/magento/b2b-ecommerce.html?_ga=2.105948422.442698376.1665067470-1322106587.1655147209)</li></ul> |
| Infraestrutura e implantação | <ul><li>Ferramentas de integração contínua na nuvem com usuários ilimitados</li><li>Fastly Content Delivery Network (CDN), Image Otimization (IO) e segurança adicional com amplas concessões de largura de banda. O serviço Web Application Firewall (WAF) está disponível somente em ambientes de produção.</li><li>[New Relic](../monitor/new-relic-service.md) APM (Monitoramento de desempenho) em 3 ramificações: `master` e 2 de sua escolha<br>Ambientes de produção, preparo e desenvolvimento da Platform as a Service (PaaS) (4 ambientes ativos totais) otimizados para o Adobe Commerce</li><li>Filtragem de saída (firewall de saída)</li></ul> | <ul><li>Ferramentas de integração contínua na nuvem com usuários ilimitados</li><li>Fastly Content Delivery Network (CDN), Image Otimization (IO) e segurança adicional com amplas concessões de largura de banda. O serviço Web Application Firewall (WAF) está disponível somente em ambientes de produção.</li><li>[New Relic](../monitor/new-relic-service.md) Infraestrutura em produção + APM (Monitoramento de desempenho) em preparo e produção. A variável [Política de alertas gerenciados](../monitor/investigate-performance.md#monitor-performance-with-managed-alerts) O para Adobe Commerce implementa as práticas recomendadas de monitoramento para notificá-lo proativamente sobre problemas de aplicativos e infraestrutura que afetam o desempenho do local.</li><li>Baseado em plataforma como um serviço (PaaS) [Desenvolvimento da integração](pro-architecture.md#integration-environment) ambientes (2 ambientes ativos totais) otimizados para o Adobe Commerce</li><li>Infraestrutura como um serviço (IaaS) — infraestrutura virtual dedicada para ambientes de preparo e produção</li></ul> |
| Infraestrutura de alta disponibilidade | | [Arquitetura de alta disponibilidade](pro-architecture.md#redundant-hardware) com uma configuração de três servidores na Infraestrutura como um serviço (IaaS) subjacente para fornecer confiabilidade e disponibilidade de nível empresarial |
| Hardware dedicado | | Hardware isolado e dedicado na infraestrutura subjacente como um serviço (IaaS) para fornecer níveis ainda mais altos de confiabilidade e disponibilidade |
| Suporte por email 24 horas por dia, 7 dias por semana | Suporte de e-mail e monitoramento 24 horas por dia, 7 dias por semana, para o aplicativo principal e a infraestrutura em nuvem | Suporte de e-mail e monitoramento 24 horas por dia, 7 dias por semana, para o aplicativo principal e a infraestrutura em nuvem |
| Um CTA (Customer Technical Advisor) dedicado | | Gerenciamento de conta técnica dedicado para o período de lançamento inicial, começando com sua assinatura até o lançamento inicial do site |
| Complementos\* | <ul><li>[Módulo B2B](https://business.adobe.com/products/magento/b2b-ecommerce.html)</li></ul> |

\* _Disponível por uma taxa adicional_

## Projetos iniciais

A variável [Arquitetura do plano inicial](starter-architecture.md) O tem quatro ambientes:

- **Integração**— O ambiente de integração fornece dois ambientes testáveis. Cada ambiente inclui uma ramificação Git ativa, um banco de dados, um servidor da Web, armazenamento em cache, alguns serviços, variáveis de ambiente e configurações.

- **Estágios**—Conforme o código e as extensões passam nos testes, você pode mesclar `integration` ramificação para o ambiente de preparo, que se torna o ambiente de teste de pré-produção. Inclui a `staging` ramificação ativa, banco de dados, servidor Web, armazenamento em cache, serviços de terceiros, variáveis de ambiente, configurações e serviços, como Fastly e New Relic.

- **Produção**—Quando o código está pronto e testado, todo o código é mesclado ao `master` para implantação no site ativo de produção. Esse ambiente inclui suas `master` ramificação, banco de dados, servidor Web, armazenamento em cache, serviços de terceiros, variáveis de ambiente e configurações.

- **Inativo**—Você tem um número ilimitado de ramificações inativas.

## Projetos Pro

A variável [Arquitetura de plano Pro](pro-architecture.md) tem uma `master` com três ambientes:

- **Integração**— o ambiente de integração fornece um ambiente testável que inclui um banco de dados, servidor da Web, armazenamento em cache, alguns serviços, variáveis de ambiente e configurações. Você pode desenvolver, implantar e testar seu código antes de mesclar ao ambiente de preparo.

   - _Inativo_—Você pode ter um número ilimitado de ramificações inativas com base no `integration` ambiente, mas apenas uma ramificação ativa (sem incluir `integration` ).

- **Estágios**— o ambiente de preparo é para testes de pré-produção e inclui um banco de dados, servidor da Web, armazenamento em cache, serviços de terceiros, variáveis de ambiente, configurações e serviços, como o Fastly.

- **Produção**— o ambiente de produção inclui uma arquitetura de três nós e alta disponibilidade para seus dados, serviços, armazenamento em cache e armazenamento. A produção é o ambiente de armazenamento público e ativo com variáveis de ambiente, configurações e serviços de terceiros.

## Software e serviços compatíveis

O Adobe Commerce na infraestrutura em nuvem usa:

- Sistema operacional: Debian GNU/Linux
- Servidor da Web: Nginx
- Banco de dados: MySQL (MariaDB)
- Rede de entrega de conteúdo (CDN): Fastly CDN

Você pode configurar os seguintes serviços:

- [PHP](../application/php-settings.md)
- [MySQL](../services/mysql.md)
- [Redis](../services/redis.md)
- [RabbitMQ](../services/rabbitmq.md)
- [Elasticsearch](../services/elasticsearch.md)
- [OpenSearch](../services/opensearch.md)

{{elasticsearch-support}}

>[!NOTE]
>
>Consulte [Requisitos do sistema](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/system-requirements.html) no _Guia de instalação_ para versões recomendadas.

O módulo Fastly CDN é usado para serviços de CDN e cache em ambientes de preparo e produção. Consulte [Configurar os serviços do Fastly](../cdn/fastly.md).

Para obter informações sobre como configurar as versões de software a serem usadas na implementação, consulte os seguintes arquivos de configuração do Adobe Commerce na infraestrutura em nuvem:

- [Configuração do aplicativo (.magento.app.yaml)](../application/configure-app-yaml.md)
- [Configuração de ambiente (.magento.env.yaml)](../environment/configure-env-yaml.md)
- [Configuração de rotas (route.yaml)](../routes/routes-yaml.md)
- [Configuração de serviços (services.yaml)](../services/services-yaml.md)
