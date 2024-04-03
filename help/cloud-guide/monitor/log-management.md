---
title: Gerenciamento de logs do New Relic
description: Saiba como usar o log do New Relic
feature: Cloud, Logs, Observability
exl-id: d8afb5c0-9727-4123-8944-81cd6ad7cbb7
source-git-commit: ebe1746ee9fd08480da5ad07d7f1f8299ad9af7e
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 0%

---

# Gerenciamento de logs do New Relic

Todos os projetos de infraestrutura em nuvem incluem [Gerenciamento de logs do New Relic](https://docs.newrelic.com/docs/logs/get-started/get-started-log-management/). O serviço é pré-configurado para agregar todos os dados de log de seus ambientes de preparo e produção e exibi-los em um painel de gerenciamento de log centralizado.

Os dados agregados incluem informações dos seguintes logs:

- Todos `ece-tools` e logs de aplicativo do `~/var/log` diretório
- Logs para serviços em nuvem do `var/log/platform/<project-ID>` diretório
- Fastly CDN e WAF

Quando seu projeto está conectado ao New Relic, você pode usar o serviço Logs da New Relic para concluir tarefas como as seguintes:

- Usar queries do New Relic para pesquisar dados de log agregados
- Visualizar dados de log por meio do aplicativo New Relic Logs
- Criar gráficos, painéis e alertas personalizados
- Solucionar problemas de desempenho a partir de um único painel

## Exibir e analisar dados de log

Use o aplicativo de Logs do New Relic para pesquisar os dados de log agregados e solucionar problemas de erros de aplicativo, infraestrutura, CDN e WAF. Você pode criar gráficos, painéis e alertas usando dados de registro coletados dos serviços de infraestrutura e APM da New Relic.

**Para usar o aplicativo Logs do New Relic**:

1. Faça logon no [Conta do New Relic](https://login.newrelic.com/login).

1. Selecionar **Logs** no menu de navegação do Explorer.

1. Verifique se a sua conta está selecionada na parte superior da _Todos os logs_ exibição.

1. Selecione um intervalo de tempo para a consulta de Logs.

1. Para analisar os dados de log de infraestrutura dos serviços em nuvem (logs do `~/var/log/`), digite a sequência de consulta `has: "filePath"` no _Pesquisar logs_ campo. Em seguida, clique em **[!UICONTROL Query logs]**.

   Os nomes dos arquivos de log são armazenados no `filePath` coluna, com caminhos completos para o arquivo de log.

   ![Dados de log do serviço New Relic do projeto em nuvem](../../assets/new-relic/var-log-query.png)

1. Para revisar os dados de log do Fastly, insira a string de consulta `has: "client_ip"` no _Pesquisar logs_ campo. Em seguida, clique em **[!UICONTROL Query logs]**.

1. Para filtrar os resultados do Fastly log por código de país, clique em **[!UICONTROL Add column]** e selecione **[!UICONTROL geo_country_code]**.

   ![Filtro de atributo de log CDN do New Relic para projetos em nuvem](../../assets/new-relic/fastly-countrycode-filter.png)

>[!TIP]
>
>Você pode salvar a visualização da consulta na _Visualizações salvas_ lista suspensa. Clique em **[!UICONTROL Create new]**, forneça um nome, selecione opções e clique em **[!UICONTROL Save view]**.
>
>Consulte [Introdução ao gerenciamento de logs](https://docs.newrelic.com/docs/logs/get-started/get-started-log-management/) e [Introdução à linguagem de consulta do New Relic](https://docs.newrelic.com/docs/query-your-data/nrql-new-relic-query-language/get-started/introduction-nrql-new-relics-query-language/) no _Documentação do New Relic_ local.
