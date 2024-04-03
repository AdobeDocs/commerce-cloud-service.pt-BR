---
title: Configurar o serviço OpenSearch
description: Saiba como habilitar o serviço OpenSearch para Adobe Commerce na infraestrutura em nuvem.
feature: Cloud, Search, Services
exl-id: 10dc6367-3f90-4ab6-a84e-15e8c3b32a38
source-git-commit: d4c36b084094846cfad69adc2bffd567a58fab26
workflow-type: tm+mt
source-wordcount: '651'
ht-degree: 0%

---

# Configurar o serviço OpenSearch

A variável [OpenSearch](https://www.opensearch.org) service é uma bifurcação de código aberto do Elasticsearch 7.10.2, seguindo as alterações de licenciamento do Elasticsearch. Consulte a [OpenSource Project](https://github.com/opensearch-project) no GitHub.

{{elasticsearch-support}}

O OpenSearch permite extrair dados de qualquer fonte, qualquer formato e pesquisá-los e visualizá-los em tempo real.

- Pesquisas rápidas e avançadas em produtos do catálogo de produtos
- Os analisadores OpenSearch são compatíveis com vários idiomas
- Suporta palavras de interrupção e sinônimos
- A indexação não afeta os clientes até que a operação de reindexação seja concluída

{{service-instruction}}

>[!TIP]
>
>A Adobe recomenda que você sempre configure o OpenSearch para seu projeto do Adobe Commerce na infraestrutura em nuvem, mesmo que planeje configurar uma ferramenta de pesquisa de terceiros para seu aplicativo do Adobe Commerce. A configuração do OpenSearch fornece uma opção de fallback se a ferramenta de pesquisa de terceiros falhar.

**Para ativar o OpenSearch**:

1. Para ambientes de integração Starter e Pro, adicione o `opensearch` serviço para o `.magento/services.yaml` arquivo com a versão apropriada e espaço em disco alocado em MB. Nesse caso, a versão 2 é adequada. A versão secundária não é necessária porque a infraestrutura em nuvem usa a versão mais recente do OpenSearch.

   ```yaml
   opensearch:
       type: opensearch:2
       disk: 1024
   ```

   Para projetos Pro, você deve [Enviar um tíquete de suporte da Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) para alterar a versão do OpenSearch nos ambientes de Preparo e Produção.

1. Defina ou verifique o `relationships` propriedade na `.magento.app.yaml` arquivo.

   ```yaml
   relationships:
       opensearch: "opensearch:opensearch"
   ```

1. Adicionar, confirmar e enviar alterações de código.

   ```bash
   git add .magento/services.yaml .magento.app.yaml
   ```

   ```bash
   git commit -m "Enable OpenSearch"
   ```

   ```bash
   git push origin <branch-name>
   ```

   Para obter informações sobre como essas alterações afetam seus ambientes, consulte [Configurar serviços](services-yaml.md).

1. Depois que o processo de implantação for concluído, use o SSH para fazer logon no ambiente remoto.

   ```bash
   magento-cloud ssh
   ```

1. Reindexe o índice de pesquisa do catálogo.

   ```bash
   bin/magento indexer:reindex catalogsearch_fulltext
   ```

1. Limpe o cache.

   ```bash
   bin/magento cache:clean
   ```

{{service-change-tip}}

## Compatibilidade de software OpenSearch

Ao instalar ou atualizar o projeto de infraestrutura do Adobe Commerce na nuvem, sempre verifique a compatibilidade entre a versão do serviço OpenSearch e o [OpenSearch PHP](https://github.com/opensearch-project/opensearch-php) cliente para Adobe Commerce.

- **Primeira configuração**-Confirme se a versão do OpenSearch especificada no `services.yaml` O arquivo é compatível com o cliente OpenSearch PHP configurado para o Adobe Commerce.

- **Atualização do projeto**-Verifique se o cliente OpenSearch PHP na nova versão do aplicativo é compatível com a versão do serviço OpenSearch instalada na infraestrutura de nuvem.

O suporte à versão e compatibilidade do serviço é determinado por versões testadas e implantadas na infraestrutura da nuvem e, às vezes, difere das versões compatíveis com implantações locais do Adobe Commerce. Consulte [Requisitos do sistema](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/system-requirements.html) no _Guia de instalação_ para obter uma lista de versões compatíveis.

**Para verificar a compatibilidade do software OpenSearch**:

1. Na estação de trabalho local, altere para o diretório do projeto.

1. Mostrar os detalhes do OpenSearch para o ambiente ativo.

   ```bash
   magento-cloud relationships --property=opensearch
   ```

1. Como alternativa, você pode usar o SSH para fazer logon no ambiente remoto.

   ```bash
   magento-cloud ssh
   ```

1. Recupere os detalhes de conexão do serviço OpenSearch.

   ```bash
   vendor/bin/ece-tools env:config:show services
   ```

   Na resposta, localize o endereço IP e a porta do ponto final do serviço OpenSearch:

   ```terminal
   +------------------------------------------+--------------------------------------------------------+
   | opensearch:                                                                                       |
   +------------------------------------------+--------------------------------------------------------+
   | username                                 | null                                                   |
   | scheme                                   | http                                                   |
   | service                                  | opensearch                                             |
   | fragment                                 | null                                                   |
   | ip                                       | 169.254.220.11                                         |
   | hostname                                 | hostf75wi3sd24l.opensearch.service._.magentosite.cloud |
   | port                                     | 9200                                                   |
   | cluster                                  | projectID-develop-4ranwui                              |
   | host                                     | opensearch.internal                                    |
   | rel                                      | opensearch                                             |
   | path                                     | null                                                   |
   | query                                    |                                                        |
   | password                                 | null                                                   |
   | type                                     | opensearch:2                                           |
   | public                                   | false                                                  |
   | host_mapped                              | false                                                  |
   ```

1. Recuperar o serviço OpenSearch instalado `version:number` do ponto de extremidade de serviço.

   ```bash
   curl -XGET <opensearch-service-endpoint-ip-address>:9200
   ```

   ```terminal
   {
      "name" : "opensearch.0",
      "cluster_name" : "opensearch",
      "cluster_uuid" : "_yzaae6-ywSEW1MaAF8ZPWyQ",
      "version" : {
        "distribution" : "opensearch",
        "number" : "2.5.0",
        "build_type" : "deb",
        "build_hash" : "aaaaaaa",
        "build_date" : "2023-01-23T12:07:18.760675Z",
        "build_snapshot" : false,
        "lucene_version" : "9.4.2",
        "minimum_wire_compatibility_version" : "7.10.0",
        "minimum_index_compatibility_version" : "7.0.0"
   },
   "tagline" : "The OpenSearch Project: https://opensearch.org/"
   }
   ```

{{pro-update-service}}

## Reiniciar o serviço OpenSearch

Se precisar reiniciar o serviço OpenSearch, entre em contato com o suporte da Adobe Commerce.

## Configuração de pesquisa adicional

- Por padrão, a configuração de pesquisa para ambientes em nuvem é gerada novamente sempre que você implanta. Você pode usar o `SEARCH_CONFIGURATION` implante a variável para manter as configurações de pesquisa personalizadas entre as implantações. Consulte [Implantar variáveis](../environment/variables-deploy.md#search_configuration).

- Depois de configurar o serviço OpenSearch para o seu projeto, use a interface do Administrador para testar a conexão OpenSearch e personalizar as configurações OpenSearch para o Adobe Commerce.

### Adicionar plug-ins do OpenSearch

Opcionalmente, é possível adicionar plug-ins para o OpenSearch, adicionando o `configuration:plugins` para o serviço OpenSearch na `.magento/services.yaml` arquivo. Por exemplo, o código a seguir habilita os plug-ins de análise ICU e Análise fonética.

```yaml
opensearch:
    type: opensearch:2
    disk: 1024
    configuration:
        plugins:
            - analysis-icu
            - analysis-phonetic
```

Consulte a [OpenSearch Projeto](https://github.com/opensearch-project) para obter mais informações sobre plug-ins.

### Remover plug-ins do OpenSearch

Removendo as entradas de plug-in do `opensearch:` seção do `.magento/services.yaml` o arquivo faz **não** desinstalar ou desabilitar o serviço. Para desativar totalmente o serviço, você deve reindexar os dados do OpenSearch após remover os plug-ins da `.magento/services.yaml` arquivo. Este design evita a possível perda ou corrupção de dados que dependem desses plug-ins.

**Para remover os plug-ins do OpenSearch**:

1. Remova as entradas de plug-in OpenSearch da sua `.magento/services.yaml` arquivo.
1. Adicionar, confirmar e enviar por push as alterações de código.

   ```bash
   git add .magento/services.yaml
   ```

   ```bash
   git commit -m "Remove OpenSearch plugin"
   ```

   ```bash
   git push origin <branch-name>
   ```

1. Confirme o `.magento/services.yaml` alterações no repositório de nuvem.
1. Reindexe o índice de pesquisa do catálogo.

   ```bash
   bin/magento indexer:reindex catalogsearch_fulltext
   ```

1. Limpe o cache.

   ```bash
   bin/magento cache:clean
   ```
