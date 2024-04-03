---
title: serviço New Relic
description: Saiba mais sobre o serviço do New Relic disponível com seu projeto do Adobe Commerce na infraestrutura em nuvem.
feature: Cloud, Observability
last-substantial-update: 2023-09-06T00:00:00Z
exl-id: 613f0694-5338-4037-8ee4-ac5eca376159
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 0%

---

# Visão geral do serviço New Relic

Todos os projetos do Adobe Commerce na infraestrutura em nuvem incluem acesso ao serviço New Relic para ajudar a monitorar o desempenho e investigar eventos do [!DNL Commerce] infraestrutura de nuvem e aplicativos.

Os seguintes recursos do New Relic estão disponíveis para uso com ambientes de produção e de preparo:

- [APM do New Relic](#new-relic-apm) (Pro e Starter)
- [Infraestrutura New Relic](#new-relic-infrastructure) (somente Pro)
- [Gerenciamento de logs do New Relic](#new-relic-logs) (somente Pro)

>[!INFO]
>
>Outros recursos do New Relic não estão disponíveis em projetos do Adobe Commerce.

## APM do New Relic

[New Relic para APM (Application Performance Management, gerenciamento de desempenho de aplicativos)](https://docs.newrelic.com/introduction-apm/) O é um produto de análise de software que ajuda a analisar e melhorar as interações do aplicativo. O APM do New Relic está disponível para todos os projetos de infraestrutura em nuvem do Adobe Commerce e fornece os seguintes recursos:

- **Foco em transações específicas**— marcar e monitorar ativamente as principais ações do cliente em seu site, como adicionar ao carrinho, fazer check-out ou processar um pagamento.
- **Monitoramento de consulta de banco de dados**— localiza e monitora consultas a bancos de dados que afetam o desempenho.
- **Mapa do aplicativo**— visualiza todas as dependências de aplicativos no site, nas extensões e nos serviços externos.
- **[!DNL Apdex]pontuações**— avalie o desempenho e crie alertas que identificam problemas e o notificam quando ocorrem, como o desempenho do site afetado por uma promoção rápida ou um evento da Web. Consulte [Pontuação do Apdex](https://docs.newrelic.com/docs/apm/new-relic-apm/apdex/apdex-measure-user-satisfaction/).
- **Alertas gerenciados para o Adobe Commerce**-Use esta política de alertas da New Relic para monitorar o desempenho dos aplicativos e da infraestrutura com base nas práticas recomendadas do setor. Consulte [Monitore o desempenho com a política de alertas Managed alerts for Adobe Commerce](investigate-performance.md/#monitor-performance-with-managed-alerts).
- **Rastrear implantações**— monitora eventos de implantação e analisa seu impacto no desempenho geral. Consulte [Rastrear implantações](track-deployments.md).

Seu projeto de infraestrutura do Adobe Commerce na nuvem inclui o software para o serviço de APM da New Relic, juntamente com uma chave de licença. Não é necessário adquirir ou instalar nenhum software adicional.

## Infraestrutura New Relic

Os projetos profissionais incluem o [Infraestrutura New Relic (NRI)](https://docs.newrelic.com/docs/infrastructure/infrastructure-monitoring/get-started/get-started-infrastructure-monitoring/) serviço, que se conecta automaticamente aos dados do aplicativo e ao performance analytics para fornecer monitoramento dinâmico do servidor. Esse serviço está disponível em ambientes de produção e preparo profissionais.

## Gerenciamento de logs do New Relic

Todos os projetos de infraestrutura em nuvem incluem [Gerenciamento de logs do New Relic](log-management.md). O serviço é pré-configurado para agregar todos os dados de log de seus ambientes de preparo e produção e exibi-los em um painel de gerenciamento de log centralizado.
