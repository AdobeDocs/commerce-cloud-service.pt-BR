---
title: Arquivo de notas de versão para ece-tools
description: Saiba mais sobre as melhorias arquivadas para as ferramentas ece.
hide: true
hidefromtoc: true
recommendations: noDisplay, noCatalog
exl-id: 96663d2f-ef00-4490-ad2e-06e8041b228e
source-git-commit: 8a0523f1714b6ea41887e99b5c31294cf5e5255e
workflow-type: tm+mt
source-wordcount: '7147'
ht-degree: 0%

---

# Arquivo de notas de versão para ece-tools

>[!NOTE]
>
>Estas notas de versão fornecem informações e atualizações para o `ece-tools` v2002.0.22 e posterior. Consulte [Notas de versão do Cloud Tools Suite](cloud-tools-suite.md) para obter as atualizações mais recentes para `ece-tools` e outros pacotes da nuvem.

## v2002.0.22

A variável `ece-tools` versão 2002.0.22 altera a estrutura do `ece-tools` pacote para dissociar a versão do `Adobe Commerce on cloud infrastructure` correções da versão ECE-Tools. A partir desta versão, os patches e as correções críticas serão entregues usando o [`magento/magento-cloud-patches`](https://github.com/magento/magento-cloud-patches) pacote, que é uma nova dependência para o `ece-tools` pacote. Fizemos essas alterações para reduzir a complexidade e agendar atualizações de versão e trabalhar com contribuições da comunidade.

- ![novo ícone](../../assets/new.svg) **Alterações ao pacote ECE-Tools**

   - ![novo ícone](../../assets/new.svg) Os patches do Adobe Commerce foram movidos do `ece-tools` empacotar para um novo [`magento/magento-cloud-patches`](https://github.com/magento/magento-cloud-patches) pacote do compositor.

   - ![novo ícone](../../assets/new.svg) Atualização do `composer.json` arquivo para o `ece-tools` pacote para adicionar uma dependência para o `magento/magento-cloud-patches` v1.0.0.

   - ![ícone corrigir](../../assets/fix.svg) Correção de um problema que causava a `ece-tools` processo de patch a ser interrompido ao aplicar conjuntos de patches sobre versões somente de segurança, a partir da versão 2.3.2-p2 e posterior. Esta questão foi introduzida pelo novo sistema de controlo da [patches somente de segurança](https://devdocs.magento.com/guides/v2.3/release-notes/bk-release-notes.html#security-only-patches).<!--MAGECLOUD-4661-->

- ![ícone corrigir](../../assets/fix.svg) **Patches e correções críticas**- Atualizar os ambientes de nuvem com `ece-tools` para aplicar os seguintes patches e correções críticas. Esses patches estão incluídos na variável `magento/magento-cloud-patches` v1.0.0.

   - ![ícone corrigir](../../assets/fix.svg) **Patches de segurança do Page Builder para as versões 2.3.1.x e 2.3.2.x**-Corrige um problema na visualização do Page Builder que permite que usuários não autenticados acessem alguns métodos de modelo que podem ser usados para acionar a execução de código arbitrário na rede (RCE), resultando em vazamentos de informações globais. Esse problema pode ocorrer ao usar versões não compatíveis do Page Builder com as versões 2.3.1 e 2.3.2 do Adobe Commerce.<!--MAGECLOUD-4649-->

   - ![ícone corrigir](../../assets/fix.svg) **Patches MSI**-Corrige problemas que causavam erros de indexação e problemas de desempenho ao usar configurações de inventário padrão para gerenciar o estoque.<!--MAGECLOUD-4428-->

   - ![ícone corrigir](../../assets/fix.svg) **Compatibilidade com versões anteriores de novas interfaces de email**-Corrige um problema de incompatibilidade com versões anteriores causado pela `Magento\Framework\Mail\EmailMessageInterface` Interface PHP introduzida no Adobe Commerce v2.3.3. No escopo deste patch, o novo `EmailMessageInterface` herda do antigo `MessageInterface`, e os módulos principais do Adobe Commerce são revertidos para depender do `MessageInterface`.<!--MAGECLOUD-4422-->

   - ![ícone corrigir](../../assets/fix.svg) **A paginação de catálogo não funciona no Elasticsearch 6.x**-Corrige um problema crítico na paginação de resultados de pesquisa que afeta clientes que usam o Elasticsearch 6.x como mecanismo de pesquisa de catálogo.<!--MAGECLOUD-4448-->

## v2002.0.21

- ![novo ícone](../../assets/new.svg) **Atualizações do Docker**—

   - ![novo ícone](../../assets/new.svg) **Novas imagens do Docker**—Compatível com as versões 2.3.3 e posteriores<!-- MAGECLOUD-3345 -->

      - PHP versão 7.3.<!-- MAGECLOUD-4017 -->

      - Cache de verniz 6.2.0<!-- MAGECLOUD-4017 -->

   - ![novo ícone](../../assets/new.svg) Adição de suporte para aplicar a configuração de gancho personalizado especificada em `.magento.app.yaml` no ambiente Docker. Anteriormente, o ambiente Docker era compatível apenas com a configuração de gancho padrão.<!-- MAGECLOUD-3505-->

   - ![novo ícone](../../assets/new.svg) Os arquivos ENV do Docker não são mais gerados durante a compilação do Docker e o `docker:config:convert` está obsoleto. Os dados correspondentes agora são armazenados no `docker-compose.yml` arquivo.<!-- MAGECLOUD-3816-->

   - ![novo ícone](../../assets/new.svg) **Imagem PHP atualizada**-Adição do Node.js à imagem do PHP Docker para oferecer suporte aos recursos node, npm e grunt-cli.<!-- MAGECLOUD-3953 -->

- ![novo ícone](../../assets/new.svg) **Atualizações de variável de ambiente**-

   - ![novo ícone](../../assets/new.svg) Adição de **LOCK_PROVIDER** implante a variável para configurar o provedor lock, o que impede a inicialização de trabalhos cron duplicados e grupos cron. Consulte a descrição da variável no [implantar variáveis](../environment/variables-deploy.md#lock_provider) tópico.<!-- MAGECLOUD-4052 -->

   - ![novo ícone](../../assets/new.svg) Adição de **CONSUMERS_WAIT_FOR_MAX_MESSAGES** variável de ambiente para configurar como os consumidores processam mensagens da fila de mensagens ao usar o `CRON_CONSUMERS_RUNNER` variável de ambiente para gerenciar trabalhos cron. Consulte a descrição da variável no [implantar variáveis](../environment/variables-deploy.md#consumers_wait_for_max_messages) tópico.<!-- MAGECLOUD-4071 -->

   - ![ícone corrigir](../../assets/fix.svg) Correção de um problema que pode causar erros de deadlock do banco de dados quando a variável `consumers_runner` o trabalho cron inicia várias instâncias do mesmo consumidor em nós diferentes. Agora, se você tiver ativado o [**CRON_CONSUMERS_RUNNER**](../environment/variables-deploy.md#cron_consumers_runner) implantar variável no seu ambiente, a variável `consumers_runner` o trabalho usa o `single-thread` opção para iniciar uma instância de cada consumidor em apenas um nó.<!-- MAGECLOUD-3913 -->

   - ![ícone corrigir](../../assets/fix.svg) Correção de um problema que afetava [**PÁGINAS_AQUECIDAS**](../environment/variables-post-deploy.md#warm_up_pages) funcionalidade que usa um URL de armazenamento padrão. Agora, se a variável `config:show:default-url` não é possível buscar um URL de base, então o URL da variável MAGENTO_CLOUD_ROUTES é usado.<!-- MAGECLOUD-3866 -->

- ![novo ícone](../../assets/new.svg) Atualização das informações de registro retornadas pela variável `module:refresh` comando. Agora, você pode ver uma lista detalhada de módulos habilitados na `cloud.log` arquivo.<!-- MAGECLOUD-2514 -->

- ![novo ícone](../../assets/new.svg) Aprimoramento da validação de compatibilidade de versão e notificações de aviso para problemas de compatibilidade entre a versão do Adobe Commerce e os serviços instalados, como Elasticsearch, [!DNL RabbitMQ], Redis e DB.<!-- MAGECLOUD-3535 -->

- ![novo ícone](../../assets/new.svg) Adição de suporte para RabitMQ versão 3.8.<!-- MAGECLOUD-4674-->

- ![novo ícone](../../assets/new.svg) Validações interativas atualizadas para compatibilidade de serviço a fim de refletir as versões compatíveis com os novos Adobe Commerce 2.3.3 e 2.2.10. Consulte [Requisitos do sistema](https://devdocs.magento.com/guides/v2.4/install-gde/system-requirements.html) no _Guia de instalação_ para versões recomendadas.<!-- MAGECLOUD-4018 -->

- ![ícone corrigir](../../assets/fix.svg) A mensagem de log retornada foi aprimorada quando o processo de gerenciamento do trabalho cron na fase de implantação tenta interromper um trabalho cron que já foi concluído para esclarecer que esse problema não é um erro. Alterado o nível de log de `INFO` para `DEBUG`.<!-- MAGECLOUD-3653-->

- ![ícone corrigir](../../assets/fix.svg) Correção de um problema ao executar o `setup:upgrade` comando que não interrompeu o processo de implantação quando ocorreu uma falha durante o `app:config:import` tarefa.<!-- MAGECLOUD-3806 -->

- ![novo ícone](../../assets/new.svg) Alterado o nível de log padrão do manipulador de arquivos para `debug` para reduzir a quantidade de detalhes no log exibido na variável [!DNL Cloud Console], enquanto ainda fornece informações detalhadas para depuração.<!-- MAGECLOUD-3871 -->

- ![ícone corrigir](../../assets/fix.svg) Correção de um problema que causava um erro com a implantação de conteúdo estático durante a criação. Após uma instalação e `ece-tools` despejo de configuração, ocorreu um erro se não houvesse local especificado para o usuário administrador no `config.php` arquivo. Agora, há um local padrão para o usuário administrador na variável `config.php` arquivo.<!-- MAGECLOUD-3957 -->

- ![ícone corrigir](../../assets/fix.svg) Corrigido um `Undefined index error` que ocorre quando um `magento-cloud` O comando da CLI falha em um ambiente não configurado com um URL seguro (https). Agora, o pacote ECE-Tools usa o URL de base (http) se o URL seguro não estiver disponível.<!-- MAGECLOUD-4009 -->

## v2002.0.20

- ![novo ícone](../../assets/new.svg) **Atualizações do Docker**—

   - ![novo ícone](../../assets/new.svg) Agora é possível executar o teste funcional usando o `ece-tools` no ambiente do Docker. Consulte [teste de aplicativo](https://devdocs.magento.com/cloud/docker/docker-test-magecloud-pkg-code.html).<!-- MAGECLOUD-3129/3684 -->

   - ![novo ícone](../../assets/new.svg) Suporte adicionado para configurar módulos PHP usando o `.magento.app.yaml` arquivo. Qualquer [Extensões PHP especificadas no `.magento.app.yaml` arquivo](https://devdocs.magento.com/cloud/project/magento-app-php-application.html#php-extensions) tornar-se disponível nos contêineres PHP do Docker.<!-- MAGECLOUD-3357 -->

   - ![novo ícone](../../assets/new.svg) Há novos comandos disponíveis para melhorar a experiência da linha de comando do Docker. Consulte a [`bin/magento-docker` seção da referência do Docker](https://devdocs.magento.com/cloud/docker/docker-quick-reference.html#magento-cloud-docker-cli).<!-- MAGECLOUD-3569 -->

   - ![novo ícone](../../assets/new.svg) Adição da capacidade de usar o Mutagen.io para sincronizar arquivos durante o desenvolvimento entre o host local e o Docker.<!-- MAGECLOUD-3559 -->

   - ![ícone corrigir](../../assets/fix.svg) Correção do caminho padrão ao usar o ambiente Docker. Agora, ao usar o SSH para fazer logon no contêiner do Docker, você estará na raiz do projeto no `/app` diretório, conforme esperado.<!-- MAGECLOUD-3582 -->

   - ![ícone corrigir](../../assets/fix.svg) Atualização da biblioteca do Sodium da versão 1.0.11 para a versão 1.0.18 e atualização da extensão Sodium PHP.<!-- MAGECLOUD-3832 -->

     >[!WARNING]
     >
     >Os clientes da Adobe Commerce em infraestrutura em nuvem devem [Enviar um tíquete de suporte da Adobe Commerce](https://support.magento.com/hc/en-us/articles/360000913794#submit-ticket) para atualizar o pacote libsódio em ambientes de produção e preparo Pro antes de atualizar para o Adobe Commerce 2.3.2. Atualmente, não é possível atualizar ambientes do Starter para o Adobe Commerce 2.3.2.

   - ![ícone corrigir](../../assets/fix.svg) Adição de `analysis-icu` e a variável `analysis-phonetic` Elasticsearch para todas as imagens do Docker.<!-- MAGECLOUD-3446 -->

   - ![ícone corrigir](../../assets/fix.svg) Validações aprimoradas: ao usar opções para o `docker:build` , você deve fornecer um valor ao usar uma opção. Além disso, foi adicionada a validação para a versão do Nó ao usar o `docker:build run` comando.<!-- MAGECLOUD-3486 & MAGECLOUD-3678 -->

- ![novo ícone](../../assets/new.svg) **Atualizações de variável de ambiente**—

   - ![novo ícone](../../assets/new.svg) Adição de suporte para prefixos de tabela de banco de dados usando o [Variável de ambiente DATABASE_CONFIGURATION](../environment/variables-deploy.md#database_configuration).<!-- MAGECLOUD-2901 -->

   - ![novo ícone](../../assets/new.svg) Adição de **FORCE_UPDATE_URLS** implante a variável para atualizar URLs base ao implantar em ambientes de produção e preparo Pro e Starter. Consulte a definição no [implantar variáveis](../environment/variables-deploy.md#force_update_urls) conteúdo.<!-- MAGECLOUD-3602 -->

   - ![novo ícone](../../assets/new.svg) Adição de **TFB_TESTED_PAGES** variável pós-implantação a ser configurada _Tempo até o Primeiro Byte_ A página testa para verificar o desempenho do aplicativo em sites implantados na infraestrutura em nuvem. Consulte a descrição da variável em [variáveis pós-implantação](../environment/variables-post-deploy.md).<!-- MAGECLOUD-3643 -->

   - ![ícone corrigir](../../assets/fix.svg) Correção de um problema com o SCD multithread, que causava falhas aleatórias na implantação de conteúdo estático. A solução alternativa envolvia definir o **SCD_THREADS** variável para `1`. Agora você pode aumentar a contagem, conforme necessário. Consulte as definições na [implantar variáveis](../environment/variables-deploy.md#scd_threads) e a variável [criar variáveis](../environment/variables-build.md#scd_threads).<!-- MAGECLOUD-3611 -->

   - ![ícone corrigir](../../assets/fix.svg) Você pode configurar o **PÁGINAS_AQUECIDAS** variável de ambiente para armazenar em cache páginas únicas, vários domínios e várias páginas. Consulte a definição expandida na [variáveis pós-implantação](../environment/variables-post-deploy.md#warm_up_pages) conteúdo.<!-- MAGECLOUD-3258 -->

- ![ícone corrigir](../../assets/fix.svg) Adição de `pub/static/.htaccess` para a lista de exclusões. [Correção apresentada por Björn Kraus da PHOENIX MEDIA GmbH](https://github.com/magento/ece-tools/pull/455).<!-- MAGECLOUD-3545/Github#455 -->

- ![ícone corrigir](../../assets/fix.svg) Correção de um erro quando todas as mensagens de validação eram exibidas como `Critical` se pelo menos um validador de nível crítico retornasse um erro.<!-- MAGECLOUD-3178 -->

- ![ícone corrigir](../../assets/fix.svg) Correção de um problema que causava uma falha de implantação se o URL de base não existisse no banco de dados.<!-- MAGECLOUD-3075 -->

- ![novo ícone](../../assets/new.svg) Adição de um novo **`env:config:show`comando** para o `ece-tools` pacote que exibe serviços, rotas ou variáveis de ambiente. Consulte [Serviços, rotas e variáveis](https://devdocs.magento.com/cloud/reference/ece-tools-reference.html#services-routes-and-variables). [Recurso enviado por Vladimir Kerkhoff](https://github.com/magento/ece-tools/pull/486).<!-- MAGECLOUD-3451 -->

- ![ícone corrigir](../../assets/fix.svg) Correção de um problema que causava um erro crítico ao tentar instalar o Adobe Commerce 2.2.6 ou anterior com o `ece-tools` desenvolver após a refatoração do shell.<!-- MAGECLOUD-3665 -->

- ![ícone corrigir](../../assets/fix.svg) Correção de um problema que causava a falha das instalações do Adobe Commerce 2.1.x e 2.2.x com um aviso sobre o uso de uma versão obsoleta do Carbon.<!-- MAGECLOUD-3704 -->

- ![ícone corrigir](../../assets/fix.svg) Diminuição da `cloud.log` nível de log para saída do shell de `info` para `debug`.<!-- MAGECLOUD-3277 -->

- ![ícone corrigir](../../assets/fix.svg) Adição de `--remove-definers (-d)` opção para o `ece-tools db-dump` comando para remover definidores do arquivo de despejo.<!-- MAGECLOUD-3510 -->

## v2002.0.19

- ![ícone corrigir](../../assets/fix.svg) Correção de um problema que substitui a `env.php` durante uma implantação, resultando em perda de configurações personalizadas. Essa atualização garante que o Adobe Commerce na infraestrutura em nuvem atualize as `env.php` com cada implantação, preservando as configurações personalizadas.<!-- MAGECLOUD-3668 -->

## v2002.0.18

- ![novo ícone](../../assets/new.svg) **Atualizações do Docker**—

   - ![novo ícone](../../assets/new.svg) Agora, o ambiente Docker é compatível com a configuração de cron definida no [propriedade crons do arquivo .magento.app.yaml](https://devdocs.magento.com/cloud/project/magento-app-properties.html#crons).<!-- MAGECLOUD-3150 -->

   - ![novo ícone](../../assets/new.svg) **Novo contêiner de Docker**—Adição de um [Contêiner de proxy de encerramento TLS](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#varnish-container) para facilitar a terminação SSL verniz em HTTPS.<!-- MAGECLOUD-2890 -->

   - ![novo ícone](../../assets/new.svg) **Nova imagem do Docker**—Adição de uma imagem Node.js para suportar Gulp e outros recursos, como o Teste de unidade JS do Jasmine.<!-- MAGECLOUD-3345 -->

   - ![novo ícone](../../assets/new.svg) **Modos de compilação do Docker**—Agora você pode optar por iniciar o ambiente Docker no [Modo de produção ou modo de desenvolvedor](https://devdocs.magento.com/cloud/docker/docker-launch.html#set-the-launch-mode). O modo de desenvolvedor oferece suporte ao desenvolvimento ativo com permissões completas de sistema de arquivos graváveis.<!-- MAGECLOUD-3152/3511 -->

   - ![ícone corrigir](../../assets/fix.svg) Correção de um problema que causava a falha da implantação do Docker com uma `Name or service not known` erro se o cache estiver configurado para um serviço não disponível. Agora, você pode remover um serviço do [`.magento/services.yaml` arquivo](https://devdocs.magento.com/cloud/project/services.html). O gerador de configuração do Docker atualiza o serviço no `docker/config.php.dist` arquivo automaticamente.<!-- MAGECLOUD-3369 -->

   - ![novo ícone](../../assets/new.svg) Adição de validações interativas para compatibilidade de serviço. Agora, se um serviço solicitado for incompatível com a versão do Adobe Commerce ou outros serviços, a variável _modo interativo_ solicita ao usuário uma mensagem e a opção de continuar. Consulte a [Versões de serviço](https://devdocs.magento.com/cloud/docker/docker-containers.html#service-containers) disponível para Docker. Use o `-n` para ignorar a interatividade para fins de CICD.<!-- MAGECLOUD-3251 -->

   - ![ícone corrigir](../../assets/fix.svg) Correção de um problema com a composição do Docker `db-dump` comando que apagou os despejos existentes.<!-- MAGECLOUD-3366 -->

   - ![ícone corrigir](../../assets/fix.svg) Correção de um problema que atribuía Redis `session`, `default`, e `page_cache` armazenamento em cache para a mesma ID de banco de dados.<!-- MAGECLOUD-3172 -->

- ![novo ícone](../../assets/new.svg) **Atualizações de variável de ambiente**—

   - ![novo ícone](../../assets/new.svg) O novo **ELASTICSUITE\_CONFIGURATION** A variável de ambiente mantém as configurações de serviço personalizadas entre as implantações. Consulte a definição no [implantar variáveis](../environment/variables-deploy.md#elasticsuite_configuration) conteúdo.<!-- MAGECLOUD-3205 -->

   - ![novo ícone](../../assets/new.svg) Adição de **SCD_MAX_EXECUTION_TIMEOUT** para que você possa aumentar o tempo para concluir a implantação do conteúdo estático do `.magento.env.yaml` arquivo. Consulte a definição no [implantar variáveis](../environment/variables-deploy.md#scd_max_execution_time), o [criar variáveis](../environment/variables-build.md#scd_max_execution_time), e o [variáveis globais](../environment/variables-global.md#scd_max_execution_time).<!-- MAGECLOUD-2822 -->

      - ![novo ícone](../../assets/new.svg) Adição de **MAGENTO_CLOUD_LOCKS_DIR** variável de ambiente para configurar o caminho para o ponto de montagem do provedor de bloqueio na infraestrutura de nuvem. O provedor de bloqueio impede a inicialização de trabalhos cron duplicados e grupos cron. Essa variável é compatível com o Adobe Commerce versão 2.2.5 e posterior e configurada automaticamente. Consulte a definição em [Variáveis da nuvem](../environment/variables-cloud.md).<!-- MAGECLOUD-3135 -->

      - ![ícone corrigir](../../assets/fix.svg) Alterou o **SCD_THREADS** valores padrão da variável de ambiente para determinar automaticamente o valor ideal com base na contagem de threads da CPU detectada. Consulte as definições atualizadas no [implantar variáveis](../environment/variables-deploy.md#scd_threads) e a variável [criar variáveis](../environment/variables-build.md#scd_threads).<!-- MAGECLOUD-3382 -->

- ![ícone corrigir](../../assets/fix.svg) Correção de um problema com uma correção para o Mecanismo de isolamento do banco de dados que causava um erro ao atualizar para o Adobe Commerce na infraestrutura em nuvem versão 2002.0.16.<!-- MAGECLOUD-3383 -->

- ![ícone corrigir](../../assets/fix.svg) Adição de uma correção que substitui o _Gráficos de imagem do Google_ com _Gráficos de imagens_. Consulte o artigo do DevBlog [Descontinuação e atualização dos Gráficos de imagem do Google para M1](https://community.magento.com/t5/Magento-DevBlog/Google-Image-Charts-deprecation-and-update-for-M1/ba-p/125006).<!-- MAGECLOUD-3456 -->

- ![ícone corrigir](../../assets/fix.svg) Adição da validação para o [variável SEARCH_CONFIGURATION](../environment/variables-deploy.md#search_configuration). A implantação falha quando a opção &quot;mecanismo&quot; não está definida e `_merge` não é obrigatório.<!-- MAGECLOUD-3470 -->

- ![ícone corrigir](../../assets/fix.svg) Correção de um problema que expunha dados confidenciais após a ocorrência de uma exceção. Agora, as informações confidenciais são mascaradas adequadamente.<!-- MAGECLOUD-3525 -->

- ![ícone corrigir](../../assets/fix.svg) Aprimoradas as configurações tolerantes a falhas do pacote de Magento Open Source. No caso de o Adobe Commerce não conseguir ler os dados do Redis `slave` instância, uma leitura é feita do Redis `master` instância. Consulte [REDIS_USE_SLAVE_CONNECTION](../environment/variables-deploy.md#redis_use_slave_connection).<!-- MAGECLOUD-2899 -->

## v2002.0.17

>[!NOTE]
>
>A variável `ece-tools` A versão 2002.0.17 inclui uma correção de segurança importante. Consulte [Recursos técnicos: Magento Open Source Patches](https://magento.com/tech-resources/download#download2288).

- ![novo ícone](../../assets/new.svg) **Atualizações de serviço**—Compatível com as seguintes versões do Adobe Commerce: 2.2.8 e posteriores 2.2.x, 2.3.1 e posteriores 2.3.x

   - Adição de suporte para o Elasticsearch versão 6.x.<!-- MAGECLOUD-3196 -->

   - Adição de suporte para Redis versão 5.0.

- ![novo ícone](../../assets/new.svg) **Novas imagens do Docker**—Adição dos seguintes serviços à build do Docker:

   - Elasticsearch 6.5<!-- MAGECLOUD-3196 -->

   - Redis 5.0<!-- MAGECLOUD-3223 -->

- ![novo ícone](../../assets/new.svg) **Nova variável de ambiente**—Anteriormente, havia um tempo limite codificado para compactação SCD. Agora você pode configurar o tempo limite de compactação SCD usando o **SCD_COMPRESSION_TIMEOUT** variável de ambiente. Consulte as definições na [criar variáveis](../environment/variables-build.md#scd_compression_timeout) e a variável [implantar variáveis](../environment/variables-deploy.md#scd_compression_timeout) conteúdo.<!-- MAGECLOUD-2870 -->

- ![ícone corrigir](../../assets/fix.svg) Adição de `--use-rewrites` opção para o comando install para que ele use regravações de servidor Web para links gerados na loja e acesso de administrador para melhorar a segurança e a experiência do cliente.<!-- MAGECLOUD-3246 -->

- ![ícone corrigir](../../assets/fix.svg) Adicionados carimbos de data e hora à `var/log/install_upgrade.log` para que ele mostre as datas dos eventos de instalação e atualização.<!-- MAGECLOUD-2895 -->

## v2002.0.16

- ![novo ícone](../../assets/new.svg) **Atualizações do Docker**—

   - Agora, a configuração de serviço padrão gerada no ambiente Docker é igual à configuração padrão no modelo Cloud.<!-- MAGECLOUD-3025 -->

   - Você pode enviar emails do seu ambiente do Docker usando o `sendmail` serviço.<!-- MAGECLOUD-2907 -->

   - Adicionada a capacidade de [configurar o Xdebug](https://devdocs.magento.com/cloud/docker/docker-development-debug.html) para depurar no ambiente do Cloud Docker.<!-- MAGECLOUD-2891 -->

   - Correção de um problema com permissões de serviço da Web ao gerar o `docker-compose.yml` arquivo.<!-- MAGECLOUD-2883 -->

- ![novo ícone](../../assets/new.svg) **Aprimoramento de atualização**—Adição da validação para confirmar que o `autoload` propriedade na `composer.json` o arquivo contém as alterações de configuração necessárias antes de atualizar para o Adobe Commerce v2.3. Consulte [Versão de atualização](https://devdocs.magento.com/cloud/project/project-upgrade.html).<!-- MAGECLOUD-2392 -->

- ![novo ícone](../../assets/new.svg) O processo de compactação na implantação de conteúdo estático agora inclui todos os ativos, gerados nativamente ou personalizados, e ocorre durante a fase de criação, no início da [`build:transfer` seção](https://devdocs.magento.com/cloud/project/magento-app-properties.html#hooks). Anteriormente, o processo de compactação ocorria antes da aplicação de minificação e agrupamento personalizados de ativos estáticos. [Correção apresentada por Rafael Garcia Lepper da Tryzens Limited](https://github.com/magento/ece-tools/pull/413).<!-- MAGECLOUD-3104 -->

- ![ícone corrigir](../../assets/fix.svg) Correção de um erro de conexão de banco de dados que ocorria durante a implantação imediatamente após a configuração de um relacionamento adicional de banco de dados e serviço. Além disso, essa correção soluciona um problema que ocorria durante o processo de configuração do Commerce Reporting for Starter. Para o Starter, essa atualização é &quot;obrigatória&quot; para usar os Relatórios do Commerce.<!-- MAGECLOUD-3035 -->

- ![ícone corrigir](../../assets/fix.svg) Correção de um problema de validação com a configuração do banco de dados que causava a falha do processo de implantação.<!-- MAGECLOUD-3003 -->

- ![ícone corrigir](../../assets/fix.svg) Atualização da restrição com a versão apropriada do `symfony/yaml` pacote a ser usado com [Constantes de PHP](https://devdocs.magento.com/cloud/project/magento-env-yaml.html#php-constants). A análise constante não funciona ao usar um `symfony/yaml` pacote anterior a 3.2. [Correção enviada por Vladimir Kerkhoff](https://github.com/magento/ece-tools/pull/404).<!-- MAGECLOUD-2956 -->

- ![novo ícone](../../assets/new.svg) **Verificação da configuração do ambiente**—Adição da validação para verificar a versão do PHP e avisar os usuários se eles não estiverem usando a versão mais recente recomendada.<!--MAGECLOUD-2903-->

- ![ícone corrigir](../../assets/fix.svg) Correção de um problema com o processamento de variáveis JSON malformadas. Agora, se uma variável JSON causar um erro de sintaxe, um aviso será exibido na `cloud.log` O arquivo e a implantação continuam usando a variável padrão.<!-- MAGECLOUD-2851 -->

- ![ícone corrigir](../../assets/fix.svg) Correção de um erro de conexão que ocorria durante a implantação imediatamente após a desativação do serviço Redis.<!-- MAGECLOUD-2747 -->

- ![novo ícone](../../assets/new.svg) **Registrando alterações em log**—Atualizou o [nível de log](../environment/log-handlers.md#log-levels) de `Info` para `Notice` para os seguintes eventos de processo de criação e implantação:<!--MAGECLOUD-2925-->

   - Início e término do processo de reconciliação dos módulos instalados no `composer.json` com definições de configuração compartilhadas no `app/etc/config.php` arquivo

   - Início e término do processo de validação de configuração

   - Início e término do `setup:di:compile` processo para geração de classes

- ![novo ícone](../../assets/new.svg) **Novas variáveis de ambiente**—

   - **[Variável de implantação RESOURCE_CONFIGURATION](../environment/variables-deploy.md#resource_configuration)**—Use essa variável para mapear um nome de recurso para uma conexão de banco de dados.<!-- MAGECLOUD-3026 & MAGECLOUD-2963-->

   - **[Variável global X_FRAME_CONFIGURATION](../environment/variables-global.md#x_frame_configuration)**—Use essa variável para alterar a variável `X-Frame-Options` configuração de cabeçalho para renderizar uma página do Adobe Commerce em uma `<frame>`, `<iframe>`ou `<object>`.<!-- MAGECLOUD-3048 -->

- ![ícone corrigir](../../assets/fix.svg) **Atualizações de variável de ambiente**—Alterou as seguintes variáveis de ambiente:

   - **[PÁGINAS_AQUECIDAS](../environment/variables-post-deploy.md)**—Adição da capacidade de pré-carregar o cache para páginas especificadas em todos os domínios definidos para uma loja da Adobe Commerce. Anteriormente, se o site estava configurado com vários domínios, o processo de pós-implantação não pré-carregava o cache das páginas especificadas em domínios não padrão e retornava o seguinte erro no log pós-implantação: `ERROR: Warming up failed: <uri>`<!-- MAGECLOUD-2466 -->

   - **SCD_COMPRESSION_LEVEL**—Atualização da documentação e da amostra `.magento.env.yaml` com os valores padrão corretos para o nível de compactação SCD. Consulte as definições na [criar variáveis](../environment/variables-build.md#scd_compression_level) e a variável [implantar variáveis](../environment/variables-deploy.md#scd_compression_level) conteúdo.<!-- MAGECLOUD-2823 -->

   - **SCD_EXCLUDE_THEMES**—Esta variável de ambiente está obsoleta. Use o [SCD_MATRIX](../environment/variables-build.md#scd_matrix) para controlar a configuração do tema.<!--MAGECLOUD-2882-->

   - **SCD\_MATRIX**—Correção do processo de validação para evitar um problema que ocorria quando SCD_MATRIX ignorava um valor de tema que continha caracteres maiúsculos e minúsculos. Consulte as definições na [criar variáveis](../environment/variables-build.md#scd_matrix) e a variável [implantar variáveis](../environment/variables-deploy.md#scd_matrix) conteúdo.<!-- MAGECLOUD-2904 -->

   - **Variáveis de ADMINISTRAÇÃO**—<!-- MAGECLOUD-2573/MAGECLOUD-2848 -->

      - Segurança aprimorada ao gerenciar credenciais para o usuário Administrador usando variáveis de ambiente. Não é mais possível usar as variáveis de ambiente ADMIN_EMAIL, ADMIN_USERNAME e ADMIN_PASSWORD para substituir credenciais de administrador durante atualizações. Se não conseguir acessar o painel Administração, use o _Esqueceu a senha_ recurso ou o `admin:user:create` Comando da CLI para criar um novo usuário administrador. Consulte [Acessar o painel de Administração](https://devdocs.magento.com/cloud/onboarding/onboarding-tasks.html#admin).

      - ADMIN_EMAIL não é mais necessário ao atualizar ou aplicar patches.

## v2002.0.15

- ![novo ícone](../../assets/new.svg) **Atualizações do Docker**—

   - Agora, o gerador de Docker usa os serviços especificados na variável `.magento.app.yaml` e `.magento/services.yaml` arquivos de configuração quando [criação do ambiente do Docker](https://devdocs.magento.com/cloud/docker/docker-config.html). Você pode escolher uma versão de serviço diferente usando parâmetros de build.<!-- MAGECLOUD-2888 -->

   - Adição da imagem do PHP 7.2 — Adição do suporte ao PHP 7.2 no Cloud Docker; atualização da [Configuração do Launch Docker](https://devdocs.magento.com/cloud/docker/docker-config.html) para incluir o `docker:build --php` opção para especificar a versão do PHP compatível com sua versão do Adobe Commerce.<!-- MAGECLOUD-2799 -->

   - Adição de um [Contêiner Cron](https://devdocs.magento.com/cloud/docker/docker-containers-cli.html#cron-container) baseado na imagem do PHP-CLI.<!-- MAGECLOUD-2565 -->

   - Adição dos seguintes serviços à build do Docker:

      - [!DNL RabbitMQ] 3.5 e 3.7<!-- MAGECLOUD-2567 & 2889-->

      - Elasticsearch 1.7, 2.4 e 5.2<!-- MAGECLOUD-2569 & 2887 -->

      - Redis 3.2 e 4.0<!-- MAGECLOUD-2886 -->

- ![novo ícone](../../assets/new.svg) **Configurar com constantes PHP**—Suporte adicionado para [Constantes de PHP](https://devdocs.magento.com/cloud/project/magento-env-yaml.html#php-constants) no `.magento.env.yaml` arquivo de configuração.<!-- MAGECLOUD- 2575 -->

- ![novo ícone](../../assets/new.svg) **Nova variável de ambiente**—Por padrão, somente o ambiente de produção tem o Google Analytics ativado. Você pode ativar Google Analytics nos ambientes de Preparo e Integração usando o  [Variável de ambiente ENABLE_GOOGLE_ANALYTICS](../environment/variables-deploy.md#enable_google_analytics).<!--MAGECLOUD-2879-->

- ![ícone corrigir](../../assets/fix.svg) Correção de um problema que removia as configurações personalizadas de cron do `env.php` após uma reimplantação. Agora, as configurações personalizadas do cron permanecem com segurança no `env.php` arquivo.<!-- MAGECLOUD-2923 -->

- ![ícone corrigir](../../assets/fix.svg) Correção de inconsistências nas mensagens e [níveis de log](../environment/log-handlers.md#log-levels) para as fases de criação, implantação e pós-implantação. Aumento dos níveis inicial e final da mensagem de log de **informações** para **aviso** para todas as fases e subfases. Adição das mensagens de log inicial e final, quando apropriado.<!-- MAGECLOUD-2919 -->

- ![ícone corrigir](../../assets/fix.svg) Correção de um problema envolvendo processos cron que impedia o início da fase de pós-implantação, quando configurada. Agora, se o gancho pós-implantação estiver ativado, os processos cron serão ativados novamente no início da fase pós-implantação.<!-- MAGECLOUD-2862 -->

- ![ícone corrigir](../../assets/fix.svg) Solução de um problema que impedia uma instalação bem-sucedida do Adobe Commerce ao especificar uma configuração de banco de dados personalizada. Anteriormente, o processo de instalação usava a configuração do banco de dados do [variável Magento_CLOUD_RELATIONSHIP](../environment/variables-cloud.md) mesmo que você tenha designado informações de conexão personalizadas na [Variável de ambiente DATABASE_CONFIGURATION](../environment/variables-deploy.md#database_configuration).<!--MAGECLOUD-2736-->

- ![ícone corrigir](../../assets/fix.svg) Corrigido o `config:dump` para que inclua cada local de site no `system` seção do `config.php` arquivo.<!--MAGECLOUD-2740-->

- ![ícone corrigir](../../assets/fix.svg) Correção de um problema que resultava em _aquecimento_ erros durante a fase de pós-implantação corrigindo a referência do URL de base de origem.<!--MAGECLOUD-2797-->

- ![ícone corrigir](../../assets/fix.svg) Correção de um problema que gerava arquivos incorretamente durante a `setup:di:compile` processo, que afetou o módulo Amazon Pay.<!--MAGECLOUD-2850-->

## v2002.0.14

- ![novo ícone](../../assets/new.svg) **Verificar Estado Ideal**—O `ideal-state` o assistente agora verifica a configuração atual durante cada implantação e fornece instruções claras para atualizar a configuração a fim de obter uma implantação mais rápida e sem tempo de inatividade.<!--MAGECLOUD-2372-->

- ![ícone corrigir](../../assets/fix.svg) **Conformidade com PCI**—Atualização dos protocolos de mensagens para o Adobe Commerce na infraestrutura em nuvem para exigir a versão 1.2 do TLS (Transport Layer Security) ao se conectar com serviços de mensagens de terceiros. Se você estiver usando um serviço de mensagem que não seja compatível com a versão 1.2 do TLS, será necessário atualizar seu serviço. Caso contrário, a seguinte mensagem de erro será exibida quando o aplicativo Adobe Commerce tentar se conectar ao servidor de mensagens para enviar um email: `Unable to connect via TLS`.<!--MAGECLOUD-2521-->

- ![novo ícone](../../assets/new.svg) **Aprimoramento na implantação**—Adição de validação para avisar os clientes se um ambiente de preparo ou produção tiver `dev`, `debug`ou `debug_logging` opções ativadas para evitar problemas de desempenho causados por atividade excessiva de registro.<!--MAGECLOUD-2517-->

- ![ícone corrigir](../../assets/fix.svg) **Correções de implantação**—

   - Agora o modo de manutenção é ativado no início da fase de implantação e desativado no final. Se a implantação falhar, o site permanecerá no modo de manutenção até que os problemas de implantação sejam resolvidos. Anteriormente, o site retornava ao modo de produção mesmo se a implantação falhasse.<!--MAGECLOUD-2603-->

      - As verificações de validação da fase de implantação foram retrabalhadas para fazer o downgrade do nível de erro para os seguintes problemas de implantação do `CRITICAL` para `WARNING` para que a implantação seja concluída. Anteriormente, esses problemas causavam falha na implantação.

      - A configuração do ambiente contém valores incorretos para variáveis de implantação ou de nuvem.

   - A versão do Elasticsearch na infraestrutura em nuvem é incompatível com a versão do módulo elasticsearch/elasticsearch compatível com o Adobe Commerce na infraestrutura em nuvem. Consulte a [artigo de solução de problemas do Elasticsearch](https://support.magento.com/hc/en-us/articles/360015758471-Deployment-fails-or-interrupts-with-cloud-log-error-Elasticsearch-version-is-not-compatible-with-current-version-of-magento) na Base de conhecimento de suporte da Adobe Commerce.<!--MAGECLOUD-2600-->

   - Correção de um problema com as definições de configuração compartilhadas no `app/etc/config.php` arquivo que causou `recursion detected` erros durante a implantação.<!--MAGECLOUD-2173-->

- ![ícone corrigir](../../assets/fix.svg) **Correções relacionadas ao Cron**—

   - Correção de um problema de agendamento do cron que impedia a execução de trabalhos se você especificasse uma frequência de cron diferente do padrão (1 minuto).<!--MAGECLOUD-2602-->

   - Correção de um problema na fase de implantação que permitia que trabalhos cron continuassem em execução durante a implantação, o que pode causar bloqueios de banco de dados e outros problemas críticos. Agora, todos os trabalhos cron são interrompidos antes de a fase de implantação começar e reiniciados após a conclusão da implantação.&lt;!—MAGECLOUD—2537—>

   - Correção do fluxo de trabalho do cron nas versões 2.2.x para desbloquear trabalhos cron congelados, de modo que possam ser interrompidos antes de iniciar a implantação. Anteriormente, um trabalho cron congelado causava a paralisação da implantação.<!--MAGECLOUD-2501-->

- ![ícone corrigir](../../assets/fix.svg) Alteração do formato de `config.php` arquivo gerado pelo `vendor/bin/ece-tools config:dump` comando para usar sintaxe de matriz curta e recuo de 4 espaços para estar em conformidade com os padrões de codificação do Adobe Commerce.<!--MAGECLOUD-2527-->

- ![ícone corrigir](../../assets/fix.svg) Correção de um erro de implantação que ocorre quando a variável `.magento.env.yaml` contém `{{ base_url }}` e `{{ unsecure_base_url }}` espaços reservados para configurações da web em vez da configuração de URL padrão de um projeto do Adobe Commerce na infraestrutura em nuvem./<!--MAGECLOUD-2607-->

## v2002.0.13

- ![novo ícone](../../assets/new.svg) **Habilitar implantação sem tempo de inatividade**— Agora o Adobe Commerce na infraestrutura em nuvem enfileira solicitações com as alterações necessárias no banco de dados durante a implantação e aplica as alterações assim que a implantação é concluída. As solicitações podem ser mantidas por até 5 minutos para garantir que nenhuma sessão seja perdida. Consulte [Opções de implantação de conteúdo estático para reduzir o tempo de inatividade da implantação na nuvem](https://support.magento.com/hc/en-us/articles/360004861194-Static-content-deployment-options-to-reduce-deployment-downtime-on-Cloud).<!--MAGECLOUD-2169-->

- ![novo ícone](../../assets/new.svg) **Composição do Docker para a nuvem**—Foram feitos os seguintes aprimoramentos no [Instalação e configuração do Docker](https://devdocs.magento.com/cloud/docker/docker-config.html) processo:

   - Adição de um comando—`docker:config:convert` para converter arquivos de configuração PHP para o formato Docker ENV para simplificar a configuração do ambiente. Agora, você copia os arquivos de configuração do PHP para o diretório Docker e os converte em arquivos ENV do Docker. Consulte [Iniciar Docker](https://devdocs.magento.com/cloud/docker/docker-config.html).<!--MAGECLOUD-2359-->

   - O processo de instalação do Adobe Commerce na infraestrutura em nuvem agora oferece suporte à implantação em sistemas de arquivos somente leitura e leitura/gravação para emular mais detalhadamente o sistema de arquivos em nuvem. Consulte [Configurar Docker](https://devdocs.magento.com/cloud/docker/docker-config.html).&lt;!—MAGECLOUD—2357—>

   - **Suporte ao serviço Redis**—Adição de uma imagem Redis, que é implantada em um contêiner Docker e configurada automaticamente para funcionar com sua instalação do Docker.&lt;!—MAGECLOUD—2442—>

   - Agora você tem o recurso de despejo de BD ao usar o Cloud Docker [container de banco de dados](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#database-container). Além disso, você pode [compartilhar arquivos](https://devdocs.magento.com/cloud/docker/docker-containers.html#sharing-data-between-host-machine-and-container) entre uma máquina host e um container usando o `docker/mnt` diretório.<!-- MAGECLOUD-2577 -->

   - **Suporte ao serviço de verniz**— Adição de uma imagem em verniz, que é implantada automaticamente em um contêiner Docker. Após a implantação, você pode configurar manualmente o Varnish de acordo com as práticas recomendadas da Adobe Commerce. Consulte [Configurar e usar verniz](https://devdocs.magento.com/guides/v2.3/config-guide/varnish/config-varnish.html).&lt;!—MAGECLOUD—2358—>

   - Acesso seguro ao site — Adição de suporte SSL para acessar sua loja da Adobe Commerce e o painel Administração.&lt;!—MAGECLOUD—2360—>

- ![ícone corrigir](../../assets/fix.svg) **Aprimoramento do suporte ao Adobe Commerce na extensão da infraestrutura em nuvem**—Rebaixamento do requisito de versão mínima para o pacote guzzlehttp/guzzle na infraestrutura do Adobe Commerce na nuvem [arquivo composer.json](https://devdocs.magento.com/cloud/reference/cloud-composer.html) para a versão 6.2, para que a `ece-tools` o pacote é compatível com mais extensões.<!--MAGECLOUD-2205-->

- ![novo ícone](../../assets/new.svg) **Aplicar alterações personalizadas ao aplicativo do Adobe Commerce durante a fase de criação**— dividimos a fase de criação em dois processos separados para que você possa usar ganchos para aplicar alterações personalizadas ao conteúdo estático gerado antes de empacotar o aplicativo para implantação. A variável _build:gerar_ O processo gera código, aplica patches e gera conteúdo estático. A variável _build:transferência_ process transfere o código gerado e o conteúdo estático para o destino final. Consulte [Ganchos de aplicativo](https://devdocs.magento.com/cloud/project/magento-app-properties.html#hooks).<!--MAGECLOUD-2363-->

- ![ícone corrigir](../../assets/fix.svg) **Verificações de configuração de ambiente**— validação aprimorada da configuração do ambiente para avisar os clientes sobre incompatibilidades de versão e erros de configuração antes de criar e implantar o Adobe Commerce na infraestrutura em nuvem.

   - Validação específica da versão adicionada para identificar variáveis e valores de ambiente sem suporte ou obsoletos.<!--MAGECLOUD-2183-->

   - Adição de uma verificação de compatibilidade de Elasticsearch para avisar os usuários sobre problemas de configuração de Elasticsearch. Agora, a implantação falhará se a versão do serviço Elasticsearch no servidor for incompatível com o Adobe Commerce. Anteriormente, a implantação era bem-sucedida mesmo se a versão do Elasticsearch fosse incompatível, o que causava problemas no catálogo de produtos após a implantação do site.<!--MAGECLOUD-2389-->

     Você pode resolver a incompatibilidade ao [envio de um tíquete de suporte](https://devdocs.magento.com/cloud/trouble/trouble.html) para atualizar o Elasticsearch para uma versão compatível ou alterar a configuração do Adobe Commerce para especificar uma versão compatível do cliente Elasticsearch PHP.

      - Para Adobe Commerce versão 2.1.x a 2.2.2, atualize o Elasticsearch para a versão 2.4.

      - Para Adobe Commerce versão 2.2.3 e posterior, atualize o Elasticsearch para a versão 5.2.

      - Se você tiver o Elasticsearch 1.x ou 2.x e não quiser fazer upgrade, atualize o requisito de versão de cliente do Adobe Commerce Elasticsearch PHP no composer.json para `"elasticsearch/elasticsearch": "~2.0"`.

   - Validação aprimorada de variáveis de ambiente para identificar definições de configuração que podem causar conflitos durante as fases de criação, implantação e pós-implantação. Por exemplo, uma mensagem de aviso será exibida durante o processo de instalação e atualização se a configuração global para implantação de conteúdo estático entrar em conflito com as configurações na fase de criação ou implantação.<!--MAGECLOUD-2156-->

- ![ícone corrigir](../../assets/fix.svg) **Atualizações de variável de ambiente**—Alterou as seguintes variáveis de ambiente:

   - **[variável global SKIP_HTML_MINIFICATION](../environment/variables-global.md#skip_html_minification)**—Alterou o valor padrão para `true` para ativar a minificação de conteúdo de HTML sob demanda, o que minimiza o tempo de inatividade ao implantar em ambientes de preparo e produção. Essa configuração é necessária para implantações sem tempo de inatividade.<!--MAGECLOUD-2435-->

   - **[variável de implantação CLEAN_STATIC_FILES](../environment/variables-deploy.md#clean_static_files)**—Adição da capacidade de gerenciar o processamento limpo de arquivos estáticos para o conteúdo estático gerado durante a fase de criação com base na configuração da variável de ambiente CLEAN_STATIC_FILES. Anteriormente, os arquivos de conteúdo estático gerados durante a fase de criação eram sempre limpos.<!--MAGECLOUD-1506-->

- ![ícone corrigir](../../assets/fix.svg) **Logs**—As seguintes alterações foram feitas para melhorar as mensagens de registro e reduzir o tamanho do registro:

   - As entradas de log de falha de implantação agora incluem a saída de comando das operações que causam as falhas, mesmo se a configuração do ambiente não especificar o log de nível de depuração. Consulte [`MIN_LOGGING_LEVEL`](../environment/variables-global.md#min_logging_level).<!--MAGECLOUD-2489-->

   - Adição de log para falhas de implantação que ocorrem quando fábricas geradas necessárias para algumas extensões não podem ser geradas corretamente porque o sistema de arquivos está em um estado somente leitura.<!--MAGECLOUD-2209-->

   - Redução do tamanho do log de implantação e correção de problemas de formatação causados por comandos de configuração que usam a barra de progresso interativa.<!--MAGECLOUD-2402-->

   - Eliminação de detalhamentos desnecessários e atualização dos níveis de prioridade para algumas instruções de log.<!--MAGECLOUD-2227-->

- ![ícone corrigir](../../assets/fix.svg) **Correções específicas do Cron**—

   - Alteradas as configurações padrão do trabalho cron para o tempo de vida do histórico, de 3d (4320 min) para 1h (60 min), para evitar problemas de desempenho e falhas de implantação que podem ocorrer quando a fila do cron é preenchida muito rapidamente.<!--MAGECLOUD-2427-->

   - Melhoria do processo de gerenciamento de trabalhos cron durante a fase de implantação para evitar bloqueios de bancos de dados e outros problemas críticos. Agora, todas as tarefas do cron são interrompidas durante a fase de implantação e reiniciadas após a conclusão da implantação.<!--MAGECLOUD-2445-->

   - Correção de um problema com o mecanismo de bloqueio para agendar consumidores iniciados por trabalhos cron nas versões 2.2.0 e posteriores do Adobe Commerce para impedir que trabalhos cron iniciem consumidores duplicados.<!--MAGECLOUD-2464-->

- ![ícone corrigir](../../assets/fix.svg) Correção de um problema com o [processo de compactação de conteúdo estático](../environment/variables-intro.md) (`gzip`) que causaram `not overwritten` e `no such file or directory` erros ao referenciar o arquivo compactado durante o processo de implantação.<!-- MAGECLOUD-2182-->

- ![ícone corrigir](../../assets/fix.svg) Correção de um problema que impedia a `php ./vendor/bin/ece-tools config:dump` para remover seções redundantes do `config.php` arquivo durante o processo de despejo se a localidade de armazenamento não for especificada. Agora é possível mover facilmente seus arquivos de configuração entre ambientes. Depois de atualizar para `ece-tools` v2002.0.13, gerar novamente mais antigo `config.php` arquivos com o aprimorado `config:dump` comando. Consulte [Gerenciamento de configurações para configurações de armazenamento](https://devdocs.magento.com/cloud/live/sens-data-over.html).<!--MAGECLOUD-2444-->

- ![ícone corrigir](../../assets/fix.svg) Correção de um problema que causava um erro durante a fase de implantação se a configuração de rota no `.magento/routes.yaml` redirecionamentos de arquivo de um [apex](https://blog.cloudflare.com/zone-apex-naked-domain-root-domain-cname-supp/) domínio para um `www` domínio.<!--MAGECLOUD-2556-->

- ![ícone corrigir](../../assets/fix.svg) Correção de um problema com o `_merge` opção para a variável [`SEARCH_CONFIGURATION`](../environment/variables-deploy.md#search_configuration) que causava resultados de mesclagem incorretos se você não incluísse a variável `engine` parâmetro na atualização do `.magento.env.yaml` arquivo de configuração. Agora, a operação de mesclagem substitui corretamente somente os valores especificados na `.magento.env.yaml` sem exigir que você defina o `engine` parâmetro.<!--MAGECLOUD-2520-->

- ![ícone corrigir](../../assets/fix.svg) Correção de um problema de configuração do Redis que ativava incorretamente o bloqueio de sessão para o Adobe Commerce nas versões 2.2.1 e posteriores da infraestrutura em nuvem, o que pode causar desempenho lento e tempos limite. Agora, o bloqueio de sessão é desativado por padrão. O problema foi causado por uma alteração no comportamento padrão do `disable_locking` introduzido na v1.3.4 do pacote do manipulador de sessão Redis. Consulte [pacote colinmollenhour/php-redis-session-abstract](https://github.com/colinmollenhour/php-redis-session-abstract).<!-- MAGECLOUD-2515-->

## v2002.0.12

- ![novo ícone](../../assets/new.svg) **Composição do Docker para a nuvem**—Adição de um comando—`docker:build`—para gerar um [Composição do Docker](https://devdocs.magento.com/cloud/docker/docker-config.html) configuração da nuvem `ece-tools` repositório.<!-- MAGECLOUD-2250 -->

- ![novo ícone](../../assets/new.svg) **Alterar localidades**—Agora é possível alterar o local de armazenamento sem o processo de exportação e importação de configuração. Enquanto o aplicativo estiver em produção e o SCD_ON_DEMAND estiver ativado, as opções de localidade de armazenamento e administração estarão disponíveis.<!-- MAGECLOUD-2019 -->

- ![novo ícone](../../assets/new.svg) <!-- MAGECLOU-1998 -->**Mapa do site e robôs**—Criou um [fluxo de trabalho](../store/robots-sitemap.md) para adicionar um `robots.txt` arquivo e gerar um `sitemap.xml` para uma única configuração de domínio sem exigir uma alteração na infraestrutura.

- ![novo ícone](../../assets/new.svg) **Assistentes**—Adição de dois [assistentes](../deploy/smart-wizards.md) para ajudar na configuração da nuvem:<!-- MAGECLOUD-1910 -->

   - `ideal-state`— configura o estado ideal para tempo de inatividade mínimo de implantação

   - `master-slave`—configurar o balanceamento de carga para o banco de dados e o Redis

- ![novo ícone](../../assets/new.svg) **Atualização de módulo**—Adição de um comando de Nuvem—`module:refresh`—para ativar módulos que foram desativados ou não, de forma semelhante à forma como é feito automaticamente durante uma criação.<!-- MAGECLOUD-1521 -->

- ![novo ícone](../../assets/new.svg) Adição da capacidade de optar por mesclar ou substituir a configuração de serviços usando o `_merge` opção em [CACHE](../environment/variables-deploy.md#cache_configuration), [SESSÃO](../environment/variables-deploy.md#session_configuration), [FILA](../environment/variables-deploy.md#queue_configuration), e [PESQUISAR](../environment/variables-deploy.md#search_configuration) configurações.<!-- MAGECLOUD-2105 -->

- ![novo ícone](../../assets/new.svg) **Arquivo de amostra de configuração de ambiente**—Adicionamos um `.magento.env.yaml` arquivo de amostra para o pacote ECE-Tools que inclui uma descrição detalhada e valores possíveis para cada variável de ambiente.<!-- MAGECLOUD-1908 -->

   - Também adicionamos uma validação profunda para o `.magento.env.yaml` configuração que evite falhas no processo de implantação causadas por valores inesperados. Quando ocorrer uma falha, você receberá uma mensagem de erro detalhada que começa com: `Environment configuration is not valid. Please correct .magento.env.yaml file with next suggestions:`<!-- MAGECLOUD-1907 -->

- ![novo ícone](../../assets/new.svg) Adição do seguinte [**Variáveis de ambiente**](../environment/variables-intro.md):

   - Agora é possível definir vários locais para cada tema usando o novo [SCD_MATRIX](../environment/variables-deploy.md#scd_matrix) variável de ambiente, que reduz a quantidade de arquivos de tema a serem implantados.<!-- MAGECLOUD-1501 -->

   - Adição de [DATABASE_CONFIGURATION](../environment/variables-deploy.md#database_configuration) variável de ambiente para personalizar as conexões do banco de dados para implantação.<!-- MAGECLOUD-2047 -->

   - O novo [MIN_LOGGING_LEVEL](../environment/variables-global.md#min_logging_level) A variável substitui o nível mínimo de log para todos os fluxos de saída sem fazer alterações no código.<!-- MAGECLOUD-2129 -->

- ![ícone corrigir](../../assets/fix.svg) Correção de um problema que causava tempo de inatividade entre as fases de implantação e pós-implantação. Agora, a fase de pós-implantação começa _imediatamente_ após o término da fase de implantação.

- ![ícone corrigir](../../assets/fix.svg) Correção de um problema que não limpava os trabalhos cron bem-sucedidos, aqueles com `status = success`, do cronograma.<!-- MAGECLOUD-2268 -->

- ![ícone corrigir](../../assets/fix.svg) Correção de um problema com o `post_deploy` gancho que limpou o cache na fase de implantação em vez da fase pós-implantação do projeto.<!-- MAGECLOUD-2113 -->

- ![ícone corrigir](../../assets/fix.svg) Correção de um problema ao usar SCD com várias localidades, que geravam a mesma `js-translation.json` arquivo para cada local.<!-- MAGECLOUD-2034 -->

- ![ícone corrigir](../../assets/fix.svg) Otimizou o `db:dump` no campo `ece-tools` para evitar o bloqueio de tabelas e aumentar a velocidade.<!-- MAGECLOUD-2033 -->

## v2002.0.11

>[!NOTE]
>
>A versão 2002.0.11 das ECE-Tools é necessária para a compatibilidade com a versão 2.2.4.

- ![novo ícone](../../assets/new.svg) **Configuração de conexões somente leitura para nós não mestres**—Esta versão adiciona a capacidade de configurar uma conexão somente leitura com um nó não mestre para receber tráfego somente leitura (para  [MariaDB](../environment/variables-deploy.md#mysql_use_slave_connection)).<!--MAGECLOUD-143 -->[Redis](../environment/variables-deploy.md#redis_use_slave_connection) e para <!--MAGECLOUD-143 -->

- ![novo ícone](../../assets/new.svg) **Assistente de configuração**—Adição de um assistente para ajudar a verificar sua configuração para implantação de conteúdo estático. Consulte [Assistentes inteligentes](../deploy/smart-wizards.md).<!--MAGECLOUD-1910 -->

- ![novo ícone](../../assets/new.svg) **Suporte ao Symfony Console**—Adição de suporte para o Symfony Console 4 com Adobe Commerce 2.3.<!-- MAGECLOUD-1966 -->

- ![ícone corrigir](../../assets/fix.svg) **Otimizações de agendamento do Cron**—Gerenciamento de fila e registro aprimorado para ajudar na depuração de problemas relacionados ao cron.<!-- MAGECLOUD-1607 -->

- ![ícone corrigir](../../assets/fix.svg) A validação da implantação falha se um `ADMIN_EMAIL` ou `ADMIN_USERNAME` O valor é igual ao de uma conta de administrador existente.<!-- MAGECLOUD-1221 -->

- ![ícone corrigir](../../assets/fix.svg) Remoção do suporte a SOLR para versões 2.2.x. As versões 2.1.x mantêm a capacidade de ativar a SOLR.<!-- MAGECLOUD-1282 -->

- ![ícone corrigir](../../assets/fix.svg) A primeira instalação dos ambientes de armazenamento temporário e produção de um projeto PRO agora inclui prefixos de índice diferentes para o Elasticsearch, a fim de evitar possíveis conflitos e identificar registros pertencentes a cada ambiente.<!-- MAGECLOUD-1489 -->

- ![ícone corrigir](../../assets/fix.svg) Correção de um problema que interrompeu a fase de criação da arquitetura herdada durante a implantação do conteúdo estático.<!-- MAGECLOUD-2021 -->

- ![ícone corrigir](../../assets/fix.svg) **Melhorias específicas do Cron**—Reformulação da implementação do cron:<!-- MAGECLOUD-1607 -->

   - Correção de um problema que fazia com que a fila do cron fosse preenchida rapidamente. Agora ele limpa os trabalhos cron desatualizados de uma maneira mais confiável.

   - A sequência de trabalhos cron foi reorganizada para que todos os trabalhos em threads separados fossem iniciados antes do grupo geral.

   - Melhoria no registro para melhor auxiliar na depuração de problemas do cron.

   - **NOTA**—Esta versão aborda muitos problemas relacionados ao cron. Se você usa atualmente alguns patches relacionados ao cron no _m2-hotfixes_, remova-as.

- ![ícone corrigir](../../assets/fix.svg) **Melhorias específicas do SCD**—

   - Você pode usar o `VERBOSE_COMMANDS` e a variável `SCD_COMPRESSION_LEVEL` variáveis de ambiente durante ambos _build_ e _implantar fases.<!-- MAGECLOUD-1819 -->

   - Correção de um problema que causava a falha da implantação com um erro aleatório ao encontrar um valor inesperado para o `SCD_COMPRESSION_LEVEL` variável de ambiente. A validação da configuração foi aprimorada para fornecer notificações significativas. Consulte [`SCD_COMPRESSION_LEVEL`](../environment/variables-build.md#scd_compression_level) para valores aceitáveis.<!-- MAGECLOUD-2043 -->

   - Correção do comportamento do `SCD_COMPRESSION_LEVEL` fluxo de configuração da variável de ambiente para que as substituições funcionem conforme esperado.<!-- MAGECLOUD-2044 -->

   - Correção de um problema que impedia a configuração do `SCD_THREADS` variável de ambiente no `.magento.env.yaml` arquivo _implantar_ estágio.<!-- MAGECLOUD-2046 -->

## v2002.0.10

- ![novo ícone](../../assets/new.svg) **Implantação de conteúdo estático (SCD)**— há um processo de implantação novo e alternativo para gerar conteúdo estático quando solicitado (sob demanda). Isso diminui o tempo de inatividade e melhora o manuseio de cache, gerando os ativos mais críticos.<!-- MAGECLOUD-1285 -->

   - **Nova variável de ambiente**—Adição de `SCD_ON_DEMAND` variável de ambiente global para gerar conteúdo estático quando solicitado.<!-- MAGECLOUD-1738 -->

   - **Gancho pós-implantação**—Adição de um `post_deploy` gancho para a `.magento.app.yaml` arquivo que limpa o cache e pré-carrega (aquece) o cache _após_ o contêiner começa a aceitar conexões. Ele está disponível somente para projetos Pro que contêm ambientes de Preparo e Produção na [!DNL Cloud Console] e para projetos iniciais. Embora não seja obrigatório, isso funciona em conjunto com a `SCD_ON_DEMAND` variável de ambiente.<!-- MAGECLOUD-1788 -->

- ![novo ícone](../../assets/new.svg) **Otimização**—Movimentação ou cópia otimizada de arquivos durante a implantação para melhorar a velocidade de implantação e reduzir cargas no sistema de arquivos.<!-- MAGECLOUD-1842 -->

- ![novo ícone](../../assets/new.svg) **Log de implantação**—Adição da capacidade de ativar manipuladores Syslog e Graylog Extended Log Format (GELF) para registros de saída durante o processo de implantação. Consulte [Manipuladores de registro](../environment/log-handlers.md).<!-- MAGECLOUD-1751 -->

- ![novo ícone](../../assets/new.svg) Adição do seguinte [**Variáveis de ambiente**](../environment/variables-intro.md):

   - `CRYPT_KEY`— Fornece uma chave criptográfica para outro ambiente ao mover um banco de dados.<!-- MAGECLOUD-1556 -->

   - `SKIP_HTML_MINIFICATION`—_Global_ variável de ambiente que ignora a cópia dos arquivos de exibição estáticos na `var/view_preprocessed` e gera um HTML minificado quando solicitado.<!-- MAGECLOUD-1621 and MAGECLOUD-1736-->

   - `SCD_ON_DEMAND`—_Global_ variável de ambiente para gerar conteúdo estático quando solicitado.<!-- MAGECLOUD-1738 -->

   - `WARM_UP_PAGES`—Você pode listar as páginas que serão usadas para pré-carregar o cache. Disponível no novo [Variáveis pós-implantação](../environment/variables-post-deploy.md).

- ![ícone corrigir](../../assets/fix.svg) Correção de um problema que envolvia um patch aplicado localmente quebrando a implantação em uma instância. Agora, o ECE-Tools pode detectar que um patch foi aplicado.<!-- MAGECLOUD-982 -->

- ![ícone corrigir](../../assets/fix.svg) Correção de um conflito entre o empacotamento do JavaScript e a funcionalidade GZIP. Agora, esses recursos funcionam corretamente juntos.<!-- MAGECLOUD-1735 -->

- ![ícone corrigir](../../assets/fix.svg) Correção de um problema que causava a falha de comandos ECE-Tools CLI ao usar versões anteriores do PHP 7.0.x.<!-- MAGECLOUD-1744 -->

- ![ícone corrigir](../../assets/fix.svg) Correção de um problema que impedia a implantação de conteúdo estático com a estratégia compacta em vários threads.<!-- MAGECLOUD-1822 -->

- ![ícone corrigir](../../assets/fix.svg) Correção de um problema de bloqueio de sessão Redis que causava um atraso de logon de Administrador. Além disso, a correção está disponível para a versão 2.1.x.<!-- MAGECLOUD-1853 -->

## v2002.0.9

>[!NOTE]
>
>Você deve [atualize o metappackage do Adobe Commerce na infraestrutura em nuvem](../dev-tools/install-package.md#update-the-metapackage) para obter esta e todas as atualizações futuras.

- ![novo ícone](../../assets/new.svg) **ece-tools**—O `ece-tools` O pacote do agora é compatível com o Adobe Commerce 2.1.x.<!-- MAGECLOUD-1086 -->

- ![novo ícone](../../assets/new.svg) **Configuração Redis**— Agora você pode [configurar Redis](../environment/variables-deploy.md#cache_configuration) armazenamento de página e cache padrão e da sessão Redis usando uma variável de ambiente.<!-- MAGECLOUD-1552 -->

- ![novo ícone](../../assets/new.svg) **Melhorias no serviço de Pesquisa, AMQP e Redis**— unificamos o fluxo de configuração do serviço para que ele agora se comporte da mesma maneira para todos os serviços. Editar manualmente o `env.php` o arquivo para configurar serviços não é mais suportado. Você deve usar variáveis de ambiente ou a variável `.magento.env.yaml` arquivo.<!-- MAGECLOUD-1437 -->

- ![ícone corrigir](../../assets/fix.svg) **Variáveis de ambiente**—

   - A utilização de `env:STATIC_CONTENT_THREADS` foi descontinuado e será removido em uma versão futura. Use o [SCD_THREADS](../environment/variables-deploy.md#scd_threads) em vez disso.<!-- MAGECLOUD-1507 -->

   - A variável `STATIC_CONTENT_EXCLUDE_THEMES` A variável de ambiente foi preterida. Você deve usar o `SCD_EXCLUDE_THEMES` variável de ambiente.<!-- MAGECLOUD-1640 -->

- ![ícone corrigir](../../assets/fix.svg) **Logs**— Simplificamos o registro em operações de patch incorporadas.<!-- MAGECLOUD-1674 -->

- ![ícone corrigir](../../assets/fix.svg) Removemos `developer` suporte ao modo e a `APPLICATION_MODE` porque estavam causando um comportamento inesperado.<!-- MAGECLOUD-1615 -->

- ![ícone corrigir](../../assets/fix.svg) Corrigimos um problema que estava causando falhas de implantação de conteúdo estático relacionadas ao Redis. Agora, a implantação de conteúdo estático de vários segmentos é executada conforme projetado.<!-- MAGECLOUD-1630 -->

- ![ícone corrigir](../../assets/fix.svg) Corrigimos um problema que impedia os usuários de salvar modificações em campos de configuração no Administrador, que são marcados como confidenciais após a execução da `app:config:dump` comando.<!-- MAGECLOUD-1175 -->

- ![ícone corrigir](../../assets/fix.svg) Adicionamos suporte para uma versão anterior do `symfony/yaml` para corrigir conflitos com alguns pacotes, que ainda não são compatíveis com a versão mais recente.<!-- MAGECLOUD-1674 -->

## v2002.0.8

>[!NOTE]
>
>Nós mesclamos `vendor/magento/ece-patches` com `vendor/magento/ece-tools` nesta versão. Não é mais necessário atualizar o `vendor/magento/ece-patches` separadamente.

**Novos recursos:**

- **Melhoria no registro**<!-- MAGECLOUD-1253 -MAGECLOUD-1495 -->
   - Melhoramos as mensagens de log para fornecer explicações melhores quando o processo de criação ou implantação substitui uma variável de ambiente.
   - Agora você pode visualizar o progresso da instalação e da atualização em tempo real. Siga o `install_update.log` arquivo para visualizar o progresso. Por exemplo,

     ```bash
     tail -f var/log/install_upgrade.log
     ```

- **Novo comando cron**—Agora é possível desbloquear tarefas cron travadas específicas em vez de interromper e reiniciar todas elas com o [`cron:unlock`](https://support.magento.com/hc/en-us/articles/360033099451) comando. Não disponível na versão 2.1.<!-- MAGECLOUD-1367 -->

- **Arquivo de configuração unificado**—Agora você pode configurar estágios de criação e implantação usando um [`.magento.env.yaml`](https://devdocs.magento.com/cloud/project/magento-env-yaml.html) arquivo.<!-- MAGECLOUD-1369 -->

- **Fazer backup dos arquivos de configuração**— agora, o processo de implantação cria automaticamente um backup do `app/etc/env.php` e `app/etc/config.php` arquivos de configuração após a implantação. Também adicionamos um [novo comando da CLI](https://support.magento.com/hc/en-us/articles/360033182871) para restaurar esses arquivos de configuração de um backup.<!-- MAGECLOUD-1372 -->

- **Solução de problemas de erros de validação**—Alteramos o comando que deve ser usado para resolver erros de validação quando `config.php` não contém dados suficientes para implantação de conteúdo estático. Anteriormente, a mensagem de erro instruía você a executar o `bin/magento app:config:dump`. Agora, você deve executar `php ./vendor/bin/ece-tools config:dump`.<!-- MAGECLOUD-1491 -->

- **Novas variáveis de ambiente**—Agora você pode usar variáveis de ambiente para conectar [pesquisa](../environment/variables-deploy.md#search_configuration) e [Baseado em AMQP](../environment/variables-deploy.md#queue_configuration) para o seu site.<!-- MAGECLOUD-1410 -->

- Implementamos o patch inteligente. Agora o pacote aplica patches com base não no Adobe Commerce na versão da infraestrutura de nuvem, mas na versão do pacote com patch.<!--MAGECLOUD-1090-->

**Problemas resolvidos:**

- Corrigimos um problema de registro que causava erros de criação.<!-- MAGECLOUD-1162 -->

- Corrigimos um problema que causava exceções de tempo limite ao executar implantações no modo interativo.<!-- MAGECLOUD-1389 -->

- Corrigimos um problema que causava erros ao usar a estratégia compacta para geração de conteúdo estático. Não disponível na versão 2.1.<!-- MAGECLOUD-1446 MAGECLOUD-1485-->

- Corrigimos um problema que impedia que o script de implantação identificasse corretamente os ambientes de preparo e produção.<!-- MAGECLOUD-1493 -->

- Corrigimos um problema que causava problemas de rede, que interrompiam conexões de banco de dados e causavam falhas durante o processo de instalação e atualização.<!-- MAGECLOUD-1520 -->

- Corrigimos um problema que impedia a exportação dos arquivos de configuração usando o `app:config:dump` mais de uma vez Não disponível na versão 2.1.<!--  MAGECLOUD-1567  -->

- Corrigimos uma sessão Redis _bloqueio_ problema que causou um _Admin_ atraso no logon. Não disponível na versão 2.1.<!--  MAGECLOUD-1582  -->

- Corrigimos um problema de implementação relacionado ao controle de versão que estava causando um conflito com outros módulos de correção baseados no Composer.<!-- MAGECLOUD-1450 -->

- Corrigimos um problema que causava problemas de memória do PHP durante a importação.<!-- MAGECLOUD-1310 -->

- Remoção de patch; correção de erro em `colinmollenhour/credis` v1.6 para habilitar o suporte para Adobe Commerce na infraestrutura em nuvem 2.2.1. Não disponível na versão 2.1.<!-- MAGECLOUD-1033 -->

## v2002.0.7

**Problemas resolvidos:**

- Removemos `var/view_preprocessed` symlinking para corrigir um problema que causava conflitos de minificação do JavaScript.<!-- MAGECLOUD-1454 -->

## v2002.0.6

**Problemas resolvidos:**

- Corrigimos um problema que estava causando `gzip` erros quando um nome de arquivo ou diretório contém espaços.<!-- MAGECLOUD-1413 -->

- Corrigimos um problema que impedia que os scripts de implantação reconhecessem e ativassem corretamente as dependências do módulo.<!-- MAGECLOUD-1424 -->

## v2002.0.5

**Novos recursos:**

- **Configurar um consumidor cron com uma variável de ambiente**—Agora você pode configurar os consumidores do CRON usando o novo `CRON_CONSUMERS_RUNNER` variável de ambiente.

- **Verificação de configuração**— Agora verificamos componentes críticos durante o processo de criação/implantação e interrompemos o processo se a verificação falhar, o que evita tempo de inatividade desnecessário devido ao local estar em modo de manutenção.

- **Criar/implantar notificações**—Adicionamos um arquivo de configuração que pode ser usado para [configurar notificações por Slack e/ou email](../environment/set-up-notifications.md) para criar/implantar ações em todos os seus ambientes.

- **Compactação de conteúdo estático**— Agora compactamos conteúdo estático usando [gzip](https://www.gnu.org/software/gzip/) durante as fases de criação e implantação. Essa compactação, combinada com a compactação Fastly, ajuda a reduzir o tamanho do armazenamento e aumentar a velocidade de implantação. Se necessário, é possível desativar a compactação usando uma [opção de compilação](../environment/variables-build.md) ou [implantar variável](../environment/variables-deploy.md). Consulte os seguintes tópicos para obter mais informações:

   - [Variáveis de ambiente de aplicativo](../application/variables-property.md)

   - [Desempenho de implantação de conteúdo estático](../deploy/static-content.md)

   - [Processo de implantação](https://devdocs.magento.com/cloud/reference/discover-deploy.html)

- **Gerenciamento de configuração**—Agora geramos automaticamente um `app/etc/config.php` arquivo no repositório Git durante a fase de criação, se ele ainda não existir. O arquivo gerado automaticamente inclui apenas uma lista de módulos e extensões. Se o arquivo já existir, a fase de criação continuará normalmente. Se você seguir [Gerenciamento de configurações](../store/store-settings.md) posteriormente, os comandos atualizam o arquivo sem exigir etapas adicionais. Consulte [Processo de implantação](https://devdocs.magento.com/cloud/reference/discover-deploy.html) para obter mais informações.

- **Despejos de banco de dados**—Adicionamos um `magento/ece-tools` Comando da CLI para criar despejos de banco de dados em todos os ambientes. Para ambientes de Produção de plano Pro, esse comando despeja apenas de um dos três nós de alta disponibilidade, portanto, os dados de produção gravados em um nó diferente durante o despejo podem não ser copiados. Recomendamos colocar o aplicativo no modo de manutenção antes de fazer um despejo de banco de dados em ambientes de Produção. Consulte [Gerenciamento de backup](https://devdocs.magento.com/cloud/project/project-webint-snap.html#db-dump) para obter mais informações.

- **Limitações do intervalo CRON levantadas**—O intervalo cron padrão para todos os ambientes provisionados nas regiões us-3, eu-3 e ap-3 é de 1 minuto. O intervalo cron padrão em todas as outras regiões é de 5 minutos para ambientes de Integração Pro e 1 minuto para ambientes de Preparo e Produção Pro. Para modificar seus trabalhos cron existentes, edite suas configurações em `.magento.app.yaml` ou crie um tíquete de suporte para ambientes de produção/preparo. Consulte [Configurar trabalhos cron](../application/crons-property.md#set-up-cron-jobs) para obter mais informações.

**Problemas resolvidos:**

- Corrigimos um problema que estava causando longos tempos de implantação porque o processo de implantação chamava o `cache-clean` operação antes da implantação de conteúdo estático.<!-- MAGECLOUD-1327 -->

- Corrigimos um problema que causava erros durante a etapa de geração de conteúdo estático da implantação em ambientes de produção.<!-- MAGECLOUD-1322 -->

- Corrigimos um problema que impedia alguns `magento/ece-tools` comandos de saída de registro para `stderr`.<!-- MAGECLOUD-1264 -->

- Corrigimos um problema que impedia valores de URL de base no `env.php` de ser atualizado em ramificações bifurcadas.<!-- MAGECLOUD-1242 -->

- Corrigimos um problema que causava a `magento setup:install` comando para adicionar um prefixo inseguro (`http://`) para proteger URLs básicos.<!-- MAGECLOUD-1171 -->

- Corrigimos um problema que impedia que erros de patch causassem falhas de implantação.<!-- MAGECLOUD-1170 -->

- Corrigimos um problema que impedia `ece-tools` de interromper a execução e lançar uma exceção se nenhum patch puder ser aplicado.<!-- MAGECLOUD-1152 -->

- Corrigimos um problema que causava erros ao carregar a loja após ativar a minificação de HTML no Administrador.<!-- MAGECLOUD-1138 -->

## v2002.0.4

**Problemas resolvidos:**

- Agora você pode [redefinir manualmente os trabalhos cron travados](https://support.magento.com/hc/en-us/articles/360033099451) usando um comando da CLI em todos os ambientes via acesso SSH. O processo de implantação redefine automaticamente os trabalhos cron.<!-- MAGECLOUD-1355 -->

## v2002.0.3

**Problemas resolvidos:**

- Corrigimos um problema que fazia com que as páginas expirassem porque o Redis demorava muito para ler/gravar. Agora você pode usar o `disable_locking` nas configurações Redis para evitar esse problema.<!-- MAGECLOUD-1311 -->

## v2002.0.2

**Problemas resolvidos:**

- A variável [!DNL RabbitMQ] O processo de configuração do agora obtém todos os parâmetros necessários automaticamente.<!-- MAGECLOUD-1246 -->

## v2002.0.1

**Novos recursos:**

- A infraestrutura do Adobe Commerce na nuvem agora é compatível com escopos e [estratégias de implantação de conteúdo estático](https://devdocs.magento.com/guides/v2.3/config-guide/cli/config-cli-subcommands-static-deploy-strategies.html). Adicionamos o `–s` parâmetro com uma configuração padrão de `quick` para a estratégia de implantação de conteúdo estático. É possível usar a variável de ambiente [SCD_STRATEGY](../environment/variables-deploy.md) para personalizar e usar essas estratégias com suas ações de criação e implantação. Essa variável é compatível com as opções `standard`, `quick`ou `compact`. Se você selecionar `compact`, substituímos o `STATIC_CONTENT_THREADS` valor com `1`, o que pode retardar a implantação, especialmente em ambientes de produção. Não disponível na versão 2.1.<!--- MAGECLOUD-1057 -->

- Criamos um arquivo de log em ambientes para capturar e compilar ações de criação e implantação. A variável `var/log/cloud.log` o arquivo está no diretório raiz do aplicativo.<!--- MAGECLOUD-1014 & MAGECLOUD-1023 -->

**Problemas resolvidos:**

- Refatorado o `ece-tools` para torná-lo compatível com o Adobe Commerce na infraestrutura em nuvem 2.2.0 e superior.<!-- MAGECLOUD-919 & MAGECLOUD-1030 -->

- Corrigimos um problema que estava impedindo `ece-tools` de interromper a execução e lançar uma exceção se nenhum patch puder ser aplicado.<!-- MAGECLOUD-1186 -->

- Corrigimos um problema que causava o lançamento de exceções quando a compilação de injeção de dependência (id) era ignorada durante compilações.<!-- MAGECLOUD-1047 & MAGECLOUD-1049 -->

- Corrigimos um problema que fazia com que o processo de implantação substituísse as configurações personalizadas de Redis na `env.php` arquivo.<!-- MAGECLOUD-1019 -->

- Corrigimos um problema que estava causando loops de redirecionamento devido a uma administração segura padrão.<!-- MAGECLOUD-1020 -->

## v2002.0.0

>[!WARNING]
>
>Este pacote não é mais compatível com outras versões do Adobe Commerce na infraestrutura em nuvem e **não deve** ser utilizado.

### Versão inicial

Versão inicial de `ece-tools` para Adobe Commerce na infraestrutura em nuvem 2.2.0.
