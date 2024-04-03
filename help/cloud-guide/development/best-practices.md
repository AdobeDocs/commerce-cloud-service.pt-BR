---
title: Práticas recomendadas para atualizar seu projeto
description: Consulte uma lista de práticas recomendadas para atualizar os arquivos do projeto.
feature: Cloud, Best Practices, Upgrade
exl-id: 7d0a2627-e4c5-46b4-9e6c-24d20fa4f92f
source-git-commit: c61d711b1041ecf76ec6468cd225a34fd77c24b1
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 0%

---

# Práticas recomendadas para atualizar seu projeto

Siga as práticas recomendadas para builds e implantação e use o [Atualizações e patches](../development/commerce-version.md) fluxo de trabalho para atualizar seu aplicativo. Use as diretrizes a seguir para planejar seu trabalho de atualização e pós-atualização:

- **Fazer backup do projeto**-Antes de atualizar o Adobe Commerce e qualquer extensão de terceiros ou personalizada, faça backup do banco de dados em ambientes de integração, preparo e produção. Consulte [Fazer backup do banco de dados](../development/commerce-version.md#project-backup).

- **Verificar problemas de compatibilidade**-

   - Verifique se todos os temas personalizados são compatíveis com a nova versão do Adobe Commerce

   - Depois de atualizar extensões de terceiros e personalizadas, use o `magento-cloud local:build` comando para validar as dependências do Composer antes de implantar.

   - Revise as notas de versão e a documentação de extensão do Adobe Commerce para garantir que você implementou qualquer solução alternativa ou alteração de configuração necessária para resolver problemas funcionais conhecidos e bugs relacionados à versão e extensões atualizadas do Adobe Commerce.

   - Verifique se as versões instaladas do serviço são compatíveis com a nova versão do Adobe Commerce e atualize os serviços conforme necessário. Consulte [Serviços](../services/services-yaml.md).

   - Teste seu banco de dados para resolver qualquer problema introduzido pelas atualizações da versão e das extensões do Adobe Commerce.

   - Faça as atualizações necessárias nas configurações específicas do ambiente antes de implantar no ambiente remoto.

   - Certifique-se de que a versão do serviço de pesquisa é compatível com a versão do cliente PHP. Consulte [Configurar Elasticsearch](../services/elasticsearch.md) ou [Configurar OpenSearch](../services/opensearch.md).

- **Verificar a conectividade do banco de dados e o armazenamento disponível em ambientes remotos**-

   - Use o SSH para fazer logon no servidor remoto e verificar a conexão com o banco de dados MySQL. Consulte [Conectar ao banco de dados](../services/mysql.md#connect-to-the-database).

   - Verificar o armazenamento disponível no ambiente remoto - Use o `disk free` comando para exibir e gerenciar o espaço em disco disponível nos ambientes na nuvem. Consulte [Gerenciar espaço em disco](../storage/manage-disk-space.md).

      - Verifique o tamanho do banco de dados atualizado e verifique se `services.yaml` o arquivo tem espaço em disco suficiente alocado.

      - Libere espaço em disco - Limpe o cache e limpe a `/log` e `/tmp` diretórios antes da implantação.

- **Planeje e execute uma atualização bem-sucedida em ambientes locais e de integração, antes de implantar no ambiente de preparo**-Após a atualização, teste sua implantação e resolva quaisquer problemas.

- **Mesclar código para Preparo e, em seguida, para Produção**- Testar e resolver quaisquer problemas no ambiente de preparo antes de enviar as alterações para o ambiente de produção.

- **Concluir tarefas pós-atualização**-

   - Use o SSH para fazer logon no servidor remoto e verifique o seguinte:

      - Verifique o status do indexador e reindexe conforme necessário. Consulte [Gerenciar os indexadores](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/manage-indexers.html) no _Guia de configuração_.

      - Verifique a `cron` logs e o `cron_schedule` tabela no banco de dados Adobe Commerce para verificar o status do cron e executar novamente os trabalhos cron, conforme necessário.
Consulte [Logs](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs.html#logging) no _Guia de configuração_.

   - Conclua o UAT de teste de aceitação do usuário pós-atualização em ambientes de preparo e produção e corrija quaisquer problemas relacionados a atualizações de extensões personalizadas e de terceiros.
