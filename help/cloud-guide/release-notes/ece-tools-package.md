---
title: Notas de versão do ECE-Tools
description: Consulte uma lista das melhorias mais recentes no pacote ECE-Tools.
recommendations: noDisplay, catalog
last-substantial-update: 2024-01-16T00:00:00Z
exl-id: a464b940-c56e-4a7c-9948-559539e25361
source-git-commit: f2aa4aa183298d829d27c4641f21acef1514d312
workflow-type: tm+mt
source-wordcount: '2887'
ht-degree: 0%

---

# Notas de versão do ECE-Tools

A variável [ece-tools](https://github.com/magento/ece-tools) O pacote do é um conjunto de scripts e ferramentas criados para gerenciar e implantar projetos na nuvem. Estas notas de versão descrevem os últimos aprimoramentos feitos neste pacote, que faz parte da [Cloud Tools Suite for Commerce](cloud-tools-suite.md).

>[!NOTE]
>
>Consulte [Atualizar ECE-Tools](../dev-tools/update-package.md) para obter informações sobre como atualizar para a versão mais recente do `ece-tools` pacote.

A variável `ece-tools` O pacote usa a seguinte sequência de controle de versão: `200<major>.<minor>.<patch>`

As notas de versão incluem:

- ![novo ícone](../../assets/new.svg) Novos recursos
- ![ícone corrigir](../../assets/fix.svg) Correções e aprimoramentos

<!--Add release notes below-->

## v2002.1.17 {#latest}

Data de lançamento: 16 de janeiro de 2024

- ![ícone corrigir](../../assets/fix.svg) **Validador para Elasticsearch e OpenSearch**—Correção do validador que gerava uma mensagem enganosa para instalar um serviço de pesquisa quando o LiveSearch estava habilitado.<!-- MCLOUD-10167 -->
- ![ícone corrigir](../../assets/fix.svg) **Aviso de implantação**—Correção de um problema que resultava em avisos de implantação sobre pastas não vazias.<!-- MCLOUD-8958 -->

## v2002.1.16

Data de lançamento: 16 de outubro de 2023

- ![novo ícone](../../assets/new.svg) **Variável de ambiente global ENABLE_WEBHOOKS**—Adição de [ENABLE_WEBHOOKS](../environment/variables-global.md#enable_webhooks) variável global para usar com webhooks do Commerce para se conectar a um endpoint externo, como a ação de tempo de execução do App Builder ou um sistema de gerenciamento de inventário de terceiros.

## v2002.1.15

Data de lançamento: 31 de julho de 2023

- ![ícone corrigir](../../assets/fix.svg) **Códigos de erro**—Esquema de código de erro atualizado e gerador de documento de código de erro.
- ![ícone corrigir](../../assets/fix.svg) **Validador para modelo Redis personalizado**-Atualização do validador para modelos de back-end Redis personalizados. [Consulte o exemplo de configuração de cache](../environment/variables-deploy.md#cache_configuration).
- ![ícone corrigir](../../assets/fix.svg) **Validador para RabbitMQ**- Adição de suporte para o RabbitMQ 3.11
- ![ícone corrigir](../../assets/fix.svg) **Corrigido o link errado**-Corrigido o link errado para a documentação de integração no modelo de email de boas-vindas.

## v2002.1.14

Data de lançamento: 10 de março de 2023

- ![novo ícone](../../assets/new.svg) **PHP**—Suporte adicionado para PHP 8.2.
- ![novo ícone](../../assets/new.svg) **Validadores de serviços**—Validadores atualizados para os serviços necessários do Commerce 2.4.6: MariaDB 10.6, Redis 7.0, PHP 8.2, OpenSearch 2.x e RabbitMQ 3.9.
- ![ícone corrigir](../../assets/fix.svg) **ece-tools db-dump**—Correção de um problema que causava a `db-dump` operação para parar prematuramente.

## v2002.1.13

Data de lançamento: 27 de outubro de 2022

- ![novo ícone](../../assets/new.svg) **Adição de suporte para Eventos Adobe I/O para Adobe Commerce**. Os desenvolvedores de extensão agora podem usar o [Eventos Adobe I/O](https://developer.adobe.com/events/docs/) para enviar informações de eventos de comércio de instâncias da Nuvem para seus aplicativos escritos para [Construtor de aplicativos Adobe](https://developer.adobe.com/app-builder/docs/overview/). Os eventos do Adobe I/O para Adobe Commerce estão na Visualização do parceiro.<!-- CEXT-932 -->
- ![novo ícone](../../assets/new.svg) **Validador para configuração do OPcache**—Adição de um validador para verificar a configuração do OPcache quanto a caminhos excluídos.<!-- MCLOUD-9485 -->
- ![ícone corrigir](../../assets/fix.svg) **Correção de um problema com a configuração do cache do GraphQL**—Agora o ECE-Tools mantém o GraphQL `id_salt` valor em `cache` configuração no `app/etc/env.php` arquivo.<!-- MCLOUD-9486 -->

## v2002.1.12

Data de lançamento: 13 de setembro de 2022

- ![novo ícone](../../assets/new.svg) **Ativar`synchronous_replication`**— ECE- Tools `synchronous_replication=>true` no `app/etc/env.php` arquivo quando `MYSQL_USE_SLAVE_CONNECTION` está ativado. Essa configuração afeta somente o Commerce 2.4.6+. Consulte a `MYSQL_USE_SLAVE_CONNECTION` descrição da variável no [Implantar variáveis](../environment/variables-deploy.md#mysql_use_slave_connection).<!-- MCLOUD-9142 -->
- ![novo ícone](../../assets/new.svg) **OpenSearch**—Adição de funcionalidade para configurar e definir o `opensearch` para a próxima versão 2.4.6 do Adobe Commerce. Consulte [Configurar o serviço OpenSearch](../services/opensearch.md).<!-- MCLOUD-9236 -->

## v2002.1.11

Data de lançamento: 4 de agosto de 2022

- ![ícone corrigir](../../assets/fix.svg) **Validador e OpenSearch do ElasticSuite**—Correção do problema do validador de verificação de integridade do ElasticSuite quando o OpenSearch é instalado.<!-- MCLOUD-8767 -->
- ![ícone corrigir](../../assets/fix.svg) **Retornar tipos para comandos de implantação**—Tipos de retorno fixos para comandos de implantação.<!-- AC-3208 -->
- ![ícone corrigir](../../assets/fix.svg) **[!DNL RabbitMQ]problema com a nova instalação do Commerce 2.4.5**—Fixo [!DNL RabbitMQ] problema de falha na instalação do novo Commerce 2.4.5.<!-- MCLOUD-9059 -->

## v2002.1.10

Data de lançamento: 31 de março de 2022

- ![ícone corrigir](../../assets/fix.svg) **Elasticsearch 7.10**—Atualização dos validadores para oferecer suporte à versão 7.10 do Elasticsearch.<!-- MCLOUD-8548 -->

## v2002.1.9

Data de lançamento: 10 de março de 2022

- ![novo ícone](../../assets/new.svg) **OpenSearch**—Adição de suporte ao OpenSearch para Adobe Commerce versões 2.4.4, 2.4.3-p2 e 2.3.7-p3.<!-- MCLOUD-8296 -->
- ![novo ícone](../../assets/new.svg) **PHP**—Suporte adicionado para PHP 8.1.
- ![ícone corrigir](../../assets/fix.svg) **symfony/process**—Adição da compatibilidade com o symfony/process ^5.3.<!-- MCLOUD-8283 -->

- ![novo ícone](../../assets/new.svg) **Vários processos do consumidor**—Adição de um `multiple_processes` para que você possa especificar o número de processos a serem gerados para cada consumidor. Consulte a `CRON_CONSUMERS_RUNNER` descrição da variável no [Implantar variáveis](../environment/variables-deploy.md#cron_consumers_runner).<!-- MCLOUD-8295 -->
- ![novo ícone](../../assets/new.svg) **Esquema OpenSearch e caminho completo do host**— Adição da capacidade de configurar um esquema de Elasticsearch e um caminho completo do host.
- ![ícone corrigir](../../assets/fix.svg) **AWS S3**—Alteração do método de ativação do AWS S3.
- ![ícone corrigir](../../assets/fix.svg) **Corrigir leitor de driver_options**—Adição da leitura da configuração driver_options para conexão de BD do `env.php` arquivo por `ece-tools` para validadores.<!-- MCLOUD-8420 -->

## v2002.1.8

Data de lançamento: 25 de outubro de 2021

- ![novo ícone](../../assets/new.svg) **Local de despejo alternativo**—Adição de `--dump-directory` opção para que você possa escolher um diretório de destino para um dump de DB. Agora `/app/var/dump-main` é o diretório de destino padrão para um despejo de BD. Consulte [Gerenciamento de backup: descarte seu banco de dados](../storage/database-dump.md)<!-- MCLOUD-8063 -->
- ![ícone corrigir](../../assets/fix.svg) **Atualizar monólogo**—Atualização da versão mínima necessária para o `monolog` empacotar para `^2.3`.<!-- ACMP-1263 -->
- ![ícone corrigir](../../assets/fix.svg) **Atualizar o Symfony**—Atualização das dependências do Symfony para compatibilidade com o Adobe Commerce 2.4.4.<!-- ACMP-1533 -->
- ![ícone corrigir](../../assets/fix.svg) **Recurso/resolver carregamento automático**—Correção de um problema ao implantar em um ambiente de integração e visualizar a `CRITICAL: [9] Required configuration is missed in autoload section of composer.json file.` erro.<!-- https://github.com/magento/ece-tools/pull/799 -->

## v2002.1.7

Data de lançamento: 29 de julho de 2021

**Atualizações de configuração**—

- ![novo ícone](../../assets/new.svg) Adição de suporte para o Composer 2.0.<!--MCLOUD-8003-->

- ![ícone corrigir](../../assets/fix.svg) **Requisitos do compositor atualizados para`symphony/console`**—Atualização do ECE-Tools `composer.json` requisitos de versão para o `symphony/console` para corrigir um problema que causava a `di:compile` comandos para falhar com o seguinte erro: `Incompatible argument type: Required type: int. Actual type: string`<!--MC-42919-->

- ![ícone corrigir](../../assets/fix.svg) Atualização das verificações de software do fim da vida útil (`eol.yaml`) para incluir o Elasticsearch 7.9.x.<!--MCLOUD-7938-->

## v2002.1.6

Data de lançamento: 20 de abril de 2021

- ![novo ícone](../../assets/new.svg) **Credenciais de autenticação Redis**—Adição da capacidade de ler credenciais de autorização do Redis a partir do `relationships` propriedade durante a fase de implantação.<!--MCLOUD-7694-->

- ![novo ícone](../../assets/new.svg) **credenciais de autorização do Elasticsearch**—Adição da capacidade de ler as credenciais de autorização do Elasticsearch do `relationships` propriedade durante a fase de implantação.<!--MCLOUD-7695-->

- ![novo ícone](../../assets/new.svg) **Serviço dedicado de armazenamento de sessão**—Adicionado `redis-session` como uma segunda opção para armazenamento de sessão. Você pode usar o `redis-session` serviço para armazenar informações da sessão e usar o `redis` para que o cache forneça melhor desempenho.<!--MCLOUD-7698-->

- ![novo ícone](../../assets/new.svg) **Mensagens SPLIT_DB obsoletas**—Adição de aviso de validador e mensagens críticas para o obsoleto `SPLIT_DB` opção para Adobe Commerce 2.4.2 e sua remoção no Adobe Commerce 2.5.0.<!--MCLOUD-7806-->

- ![ícone corrigir](../../assets/fix.svg) **Versão do Elasticsearch de relacionamentos**—Validador de serviço fixo para recuperar a versão correta do Elasticsearch do `relationships` propriedades no Cloud Docker e em ambientes de integração.<!--MCLOUD-7572-->

- ![ícone corrigir](../../assets/fix.svg) **Validação flexível da porta Redis**—O Redis agora pode validar a porta em uma conexão de cache personalizada a partir do `server` URL. Por exemplo, você pode adicionar o número da porta ao URL do servidor da seguinte maneira: `server: 'tcp://rfs-store-simple-page-cache:26379'`. Isso ajuda a evitar erros de validação nos quais o `port` opção está ausente ou incorreta.<!--MCLOUD-7722-->

- ![ícone corrigir](../../assets/fix.svg) **Atualização para o Adobe Commerce 2.4.2**—Correção do problema que exigia que os usuários executassem manualmente `bin/magento setup:upgrade` para tornar seus sites operacionais após a atualização para o Adobe Commerce 2.4.2.<!--MCLOUD-7776-->

## v2002.1.5

Data de lançamento: 1 de fevereiro de 2021

- ![novo ícone](../../assets/new.svg) **Armazenamento remoto**—Adição de `REMOTE_STORAGE` variável de ambiente para habilitar Projetos na nuvem para armazenamento remoto de arquivos de mídia usando um serviço de armazenamento, como o AWS S3. Essa opção de configuração faz parte do pacote ECE-Tools, mas não é compatível com o Adobe Commerce na infraestrutura em nuvem.<!--MCLOUD-7153-->

- ![novo ícone](../../assets/new.svg) **Novo `cloud:config:validate` comando**— Adicionado comando `php vendor/bin/ece-tools cloud:config:validate` para validar o `.magento.env.yaml` antes de enviar as alterações para o ambiente de nuvem remoto.<!--MCLOUD-7120-->

- ![novo ícone](../../assets/new.svg) **Liberando o opcache**—Suporte adicionado para o `opcache.enable_cli` Opção PHP para liberar o OPcache antes de executar o gancho de implantação. Essa configuração redefine a configuração do cache para garantir que as definições de configuração atuais sejam aplicadas em cada implantação.<!--MCLOUD-7015-->

- ![novo ícone](../../assets/new.svg) **Validação do Aurora DB**—Atualização da validação do serviço de banco de dados para que seja compatível com o banco de dados Aurora.<!--MCLOUD-7269-->

- ![novo ícone](../../assets/new.svg) **Nova variável de ambiente SCD_NO_PARENT**—Adição de `SCD_NO_PARENT` Variável de ambiente (para Adobe Commerce >=2.4.2) para gerenciar a geração de conteúdo estático para temas principais.<!--MCLOUD-7284-->

- ![ícone corrigir](../../assets/fix.svg) **Limites e comandos de memória**—Correção de um problema em que `php vendor/bin/ece-tools` comandos não funcionariam se o tamanho do `cloud.log` arquivo excedeu o limite de memória do PHP. Em vez de ler todo o `cloud.log` na memória, agora lemos apenas um subconjunto menor de dados do arquivo de log.<!--MCLOUD-7275--><!--MCLOUD-7400-->

- ![ícone corrigir](../../assets/fix.svg) **Conexões de banco de dados personalizadas**—Correção de um `.magento.env.yaml` problema de configuração em que conexões de banco de dados personalizadas são definidas para `DATABASE_CONFIGURATION` não foram utilizados. As configurações de conexão não eram adicionadas a `app/etc/env.php`.<!--MCLOUD-7426-->

- ![ícone corrigir](../../assets/fix.svg) **Logs de erros vazios**—Correção de um problema que causava a falha de implantações se a variável `cloud.error.log` estava vazio.<!--MCLOUD-7296-->

- ![ícone corrigir](../../assets/fix.svg) **Validação do MariaDB 10.3**—Validação corrigida do MariaDB 10.3 para Adobe Commerce 2.3.6-p1.<!--MCLOUD-7416-->

- ![ícone corrigir](../../assets/fix.svg) **Cache:log de liberação**—Entradas de log aprimoradas para indicar o início e o término do `cache:flush` etapa.<!--MCLOUD-7503-->

## v2002.1.4

Data de lançamento: 19 de novembro de 2020

- ![ícone corrigir](../../assets/fix.svg) Correção de um problema que causava falha na implantação quando o mecanismo de pesquisa especificado no `SEARCH_CONFIGURATION` a variável de ambiente é um valor diferente de `elasticsearch`.<!--MCLOUD-7283-->

## v2002.1.3

Data de lançamento: 9 de novembro de 2020

**Atualizações da infraestrutura**—

- ![novo ícone](../../assets/new.svg) Adição do suporte a ECE-Tools para o plug-in somente leitura `pub/static` diretório quando o conteúdo estático estiver definido para implantação no estágio de criação.<!--MC-37699-->

- ![novo ícone](../../assets/new.svg) Adição de suporte para o Elasticsearch 7.9 e Redis 6 para compatibilidade com versões futuras do Adobe Commerce.<!--MCLOUD-7191-->

- ![ícone corrigir](../../assets/fix.svg) Atualização do ECE-Tools `composer.json` para adicionar uma dependência necessária à Ferramenta de correções de qualidade. Isso corrige uma dependência circular que existia entre os pacotes ECE-Tools e magento-cloud-patches.<!--MCLOUD-6910-->

**Melhorias na validação e registro**—

- ![novo ícone](../../assets/new.svg) Adição da validação do mecanismo de pesquisa para garantir que `elasticsearch` está definido para Adobe Commerce na infraestrutura em nuvem 2.4 e posterior. Se a validação falhar, a implantação será interrompida com uma mensagem de erro crítica que sugere correções para o problema. Consulte [Erros Críticos, Estágio de Implantação](../dev-tools/error-reference.md#deploy-stage).<!--MCLOUD-6937-->

- ![novo ícone](../../assets/new.svg) Adição da validação de Elasticsearch para verificar a compatibilidade entre a versão do serviço de Elasticsearch e a versão do Adobe Commerce.<!--MCLOUD-7193-->

- ![novo ícone](../../assets/new.svg) Atualização da mensagem de erro de compatibilidade de Elasticsearch para mostrar as versões de Elasticsearch compatíveis com o módulo Elasticsearch Adobe Commerce. A mensagem de erro agora fornece as versões específicas do Elasticsearch a serem instaladas na infraestrutura em nuvem para que sejam compatíveis com o módulo do Elasticsearch usado pela versão do Adobe Commerce. Consulte [Erros de aviso, estágio de implantação](../dev-tools/error-reference.md#deploy-stage-1).<!--MCLOUD-6698-->

- ![novo ícone](../../assets/new.svg) Adição de erros de aviso `2026` e `2027` para inválido `MAGE_MODE` configuração da variável de ambiente. O único valor válido é `production`. Antes dessa correção, `MAGE_MODE` pode ser definido como `developer` sem erros de implantação, apenas para causar erros posteriormente ao tentar gravar em arquivos somente leitura. Consulte [Erros de Aviso](../dev-tools/error-reference.md#warning-errors).<!--MCLOUD-6708-->

- ![ícone corrigir](../../assets/fix.svg) Correção da validação para os serviços Redis, RabbitMQ e MySQL para garantir que essas versões sejam compatíveis com a versão do Adobe Commerce. Versões válidas desses serviços agora são gravadas no `cloud.log`.<!--MCLOUD-7098-->

- ![ícone corrigir](../../assets/fix.svg) Atualização do `cloud.log` para incluir o limite de solicitações simultâneas para envio de solicitações durante o aquecimento do cache. Esse valor é configurado na variável [WARM_UP_CONCURRENCY](../environment/variables-post-deploy.md#warm_up_concurrency) variável pós-implantação.<!--MCLOUD-5563-->

**Atualizações de comando da CLI**—

- ![novo ícone](../../assets/new.svg) Comandos CLI adicionados (`cloud:config:create` e `cloud:config:update`) para criar e atualizar a `.magento.env.yaml` arquivo com uma configuração que pode incluir uma ou mais variáveis de build, implantação e pós-implantação. Consulte [Criar arquivo de configuração da CLI](../environment/configure-env-yaml.md#create-configuration-file-from-cli).<!--MCLOUD-7072-->

**Atualizações de variável de ambiente**—

- ![novo ícone](../../assets/new.svg) Adição de [SKIP_COMPOSER_DUMP_AUTOLOAD](../environment/variables-build.md#skip_composer_dump_autoload) variável de build. Configuração da variável para `true` impede o aplicativo de executar o `composer dump-autoload` durante a instalação do Cloud Docker for Commerce. A variável só é relevante para o Cloud Docker para contêineres do Commerce com sistemas de arquivos graváveis (criados para teste e desenvolvimento usando `./vendor/bin/ece-docker build:compose --with-test`). Com essas instalações, ignorando o `composer dump-autoload` impede erros ao executar outros comandos que tentam acessar arquivos de um arquivo excluído `generated` diretório.<!--MCLOUD-6939-->

## v2002.1.2

Data de lançamento: 5 de agosto de 2020

**Melhorias na validação e registro**—

- ![novo ícone](../../assets/new.svg) Adição de `schema.error.yaml` arquivo que inclui todas as notificações de erro e aviso que podem ocorrer durante o processo de criação, implantação e pós-implantação, juntamente com sugestões para resolver os erros. As informações desse arquivo também estão disponíveis no _Guia da nuvem do Commerce_. Consulte [Referência de mensagem de erro para ece-tools](../dev-tools/error-reference.md).<!--MCLOUD-5878-->

- ![novo ícone](../../assets/new.svg) Alteração do log de erros da nuvem (`/var/log/cloud.error.log`) entradas no formato JSON para facilitar a análise programática do log.<!--MCLOUD-5879-->

- ![novo ícone](../../assets/new.svg) Adição de verificações de erros para criar, implantar e pós-implantar o processamento e aprimoramento das verificações existentes:

   - Código de erro 2026 — Falha ao restaurar alguns dados gerados durante a fase de compilação para os diretórios montados

   - Código de erro 3004 — Não é possível criar arquivos de backup

   - Código de erro 102 — Adição de verificações adicionais para problemas que ocorrem quando a variável `env.php` o arquivo não é gravável <!--MCLOUD-6221-->

- ![novo ícone](../../assets/new.svg) Adição de **QUALITY_PATCH** variável de ambiente para especificar um ou mais patches de qualidade a serem aplicados durante o processo de implantação. Consulte [Criar variáveis](../environment/variables-build.md#quality_patches).<!--MCLOUD-6375-->

## v2002.1.1

Data de lançamento: 25 de junho de 2020

- ![novo ícone](../../assets/new.svg) **Atualizações da infraestrutura**—

   - ![novo ícone](../../assets/new.svg) **Melhorias no registro**—Melhor recurso de rastreamento de registros atribuindo códigos de saída a erros críticos de implantação e expondo os códigos de saída em notificações de mensagens de erro e eventos de log. Consulte [Referência de mensagem de erro para ece-tools](../dev-tools/error-reference.md).<!-- MCLOUD-5637, 5531-->

   - ![novo ícone](../../assets/new.svg) Melhoria do processo de despejos de banco de dados (`vendor/bin/ece-tools db-dump`) e mensagens de log atualizadas para esclarecer que a operação de despejo de banco de dados alterna o aplicativo para o modo de manutenção, interrompe os processos da fila do consumidor e desativa os trabalhos cron antes do início do despejo.<!--MCLOUD-5324, MCLOUD-2062-->

   - ![ícone corrigir](../../assets/fix.svg) Correção de um problema para garantir que o URL do projeto seja atualizado corretamente ao implantar em ambientes de Preparo e Produção. Agora, `ece-tools` usa o URL da rota com a variável `primary:true` atributo definido na configuração de rota do projeto. Consulte [Implantar variáveis](../environment/variables-deploy.md#update_urls).<!--MCLOUD-5883-->

   - ![ícone corrigir](../../assets/fix.svg) Atualização do `generate.xml` fluxo de trabalho do cenário de criação para aplicar patches. Os patches devem ser aplicados antes para atualizar o Adobe Commerce e corrigir qualquer problema que possa causar o `di:compile` e `module:refresh` etapas para falhar.<!--MCLOUD-5941-->

   - ![ícone corrigir](../../assets/fix.svg) Correção de um problema no processo de instalação que retornava incorretamente a variável `Crypt key missing` erro. A variável `crypt/key` é gerado automaticamente durante a instalação.<!--MCLOUD-6120-->

- ![novo ícone](../../assets/new.svg) **Atualizações de serviço**—

   - ![novo ícone](../../assets/new.svg) Suporte adicionado para PHP 7.4 e MariaDB 10.4.<!--MAGECLOUD-2957, MCLOUD-4144-->

- ![novo ícone](../../assets/new.svg) **Atualizações de variável de ambiente**—

   - ![novo ícone](../../assets/new.svg) Adição de **SCD_USE_BALER** para ativar o módulo Baler para empacotamento de JavaScript durante o processo de criação da infraestrutura em nuvem do Adobe Commerce. Consulte a descrição da variável no [criar variáveis](../environment/variables-build.md#scd_use_baler).<!-- MCLOUD-3456, MCLOUD-3457-->

   - ![novo ícone](../../assets/new.svg) Adição de **REDIS_BACK-END** variável de ambiente para configurar o modelo de back-end Redis para cache Redis para Adobe Commerce 2.3.5 ou posterior. Consulte a descrição da variável no [implantar variáveis](../environment/variables-deploy.md#redis_backend).<!--MCLOUD-5721, MCLOUD-5865-->

- ![novo ícone](../../assets/new.svg) **Atualizações de comando da CLI**—

   - ![novo ícone](../../assets/new.svg) Atualização dos seguintes comandos CLI com uma opção para registro mais detalhado:

      - `app:config:dump`
      - `app:config:import`
      - `module:enable`

     O nível de registro para cada chamada é determinado pela configuração do [`VERBOSE_COMMANDS`](../environment/variables-build.md#verbose_commands) na variável `.magento.env.yaml` arquivo.<!--MCLOUD-3503-->

- ![novo ícone](../../assets/new.svg) **Melhorias na validação**—

   - ![novo ícone](../../assets/new.svg) **Verificações de compatibilidade do Elasticsearch 7.x**—Atualização da validação de Elasticsearch para as verificações de compatibilidade de software do Elasticsearch 7.x.<!--MCLOUD-5542-->

   - ![novo ícone](../../assets/new.svg) **Verificações de versão de serviço e validação de EOL atualizadas**—Validação atualizada para verificar as versões do serviço instalado em relação aos requisitos do Adobe Commerce 2.4.<!--MCLOUD-6144-->

   - ![ícone corrigir](../../assets/fix.svg) Correção de um problema de validação para que a seguinte mensagem de aviso de pós-implantação fosse exibida somente se a variável `post-deploy` a configuração do gancho está ausente no `.magento.app.yaml` arquivo:

     ```text
     Your application does not have the "post_deploy" hook enabled.
     ```

     <!--MCLOUD-4077-->

   - ![novo ícone](../../assets/new.svg) **Adição da validação para dependências do Zend Framework**—Adição da validação de dependência de compositor para o Zend Framework que migrou para o projeto Laminas. Se as dependências necessárias estiverem ausentes, a seguinte mensagem de erro será exibida durante o processo de criação.

     ```text
     Required configuration is missing from the autoload section of the composer.json file.
     Add ("Laminas\Mvc\Controller\Zend\": "setupsrc/ Zend/Mvc/Controller/") to
     the `autoload -> psr-4` section. Then, re-run the "composer update" command locally, and
     commit the updated composer.json and composer.lock files.
     ```

     Consulte [Verificar as dependências do Zend Framework](../development/commerce-version.md#verify-zend-framework-composer-dependencies).<!--MCLOUD-4094-->

   - ![novo ícone](../../assets/new.svg) **Validação adicionada para `env.php` arquivo e dados**—Adição de verificações para o `env.php` arquivos e dados durante o processo de instalação e atualização.<!--MCLOUD-5991-->

      - Se a variável `env.php` arquivo estiver ausente na instalação, e a variável `crypt/key` o valor não está especificado no `.magento.app.yaml` falha na implantação com a seguinte notificação:

        ```text
        The crypt/key key value does not exist in the ./app/etc/env.php file or the CRYPT_KEY cloud environment variable``Missing crypt key for upgrading Magento`.
        ```

      - Se a instalação não incluir a variável `env.php` arquivo ou a configuração contiver apenas um tipo de cache, a variável `cron:enable` é executado durante o processo de atualização para restaurar o arquivo com todos os `cache_types`. A notificação a seguir é adicionada ao log:

        ```text
        Magento state indicated as installed but configuration file app/etc/env.php was empty or did not exist.
        Required data will be restored from environment configurations and from the .magento.env.yaml file.
        ```

## v2002.1.0

Data de lançamento: 6 de fevereiro de 2020

- ![novo ícone](../../assets/new.svg) **Atualizações da infraestrutura**—

   - ![novo ícone](../../assets/new.svg) **Adição de pacote separado para o Cloud Docker for Commerce**—Dissociação do pacote Docker do `ece-tools` pacote para manter a qualidade do código e fornecer versões independentes. Atualizações e correções relacionadas ao `ece-tools` são gerenciados no [magento-cloud-docker](https://github.com/magento/magento-cloud-docker) Repositório GitHub.<!--MAGECLOUD-2927-->

   - ![novo ícone](../../assets/new.svg) **Recursos de patch atualizados**—A funcionalidade de correção foi movida do pacote ECE-Tools para um [magento-cloud-patches](https://github.com/magento/magento-cloud-patches) pacote. Durante a implantação, `ece-tools` O usa o novo pacote para aplicar patches. Consulte [Notas de versão de patches de nuvem](cloud-patches.md).<!--MAGECLOUD-4567-->

   - ![novo ícone](../../assets/new.svg) **Dependências atualizadas do Composer**—Atualizou o `composer.json` arquivo para Adobe Commerce na infraestrutura em nuvem com uma dependência para o `magento/magento-cloud-docker` pacote. Agora, `ece-tools` inclui dependências para todos os pacotes no [`Cloud Tools Suite for Commerce`](cloud-tools-suite.md). Esses pacotes são instalados e atualizados automaticamente ao instalar ou atualizar `ece-tools`.

- ![novo ícone](../../assets/new.svg) **Suporte para implantações baseadas em cenário**—<!--MAGECLOUD-4101-->

   - ![novo ícone](../../assets/new.svg) Agora é possível personalizar os processos de criação, implantação e pós-implantação usando arquivos de configuração XML para substituir ou personalizar a configuração padrão.

   - ![novo ícone](../../assets/new.svg) **Alterou o `hooks` configuração no`.magento.app.yaml`**—Atualizamos o `hooks` formato de configuração para suportar implantações baseadas em cenários. O formato herdado da versão anterior das ECE-Tools 2002.0.x ainda é suportado. No entanto, é necessário atualizar para o novo formato para usar o recurso de implantação baseada em cenário. Consulte [Implantações baseadas em cenário](../deploy/scenario-based.md#add-scenarios-using-build-and-deploy-hooks).

>[!NOTE]
>
>Antes de atualizar para a versão ECE-Tools 2002.1.0, reveja o [alterações incompatíveis com versões anteriores](backward-incompatible-changes.md) para saber mais sobre alterações que podem exigir a atualização da configuração ou dos processos do projeto Adobe Commerce na infraestrutura em nuvem.

- ![novo ícone](../../assets/new.svg) **Atualizações de serviço**—

   - ![novo ícone](../../assets/new.svg) Suporte adicionado para o PHP 7.3.<!--MAGECLOUD-4022-->

   - ![novo ícone](../../assets/new.svg) Adição de suporte para o RabbitMQ 3.8.<!--MAGECLOUD-4674-->

   - ![novo ícone](../../assets/new.svg) Validação adicionada para verificar as versões do serviço instaladas em relação à data EOL de cada serviço. Agora, os clientes recebem uma notificação se uma versão do serviço estiver dentro de três meses da data EOL, e um aviso se a data EOL estiver no passado.<!--MAGECLOUD-4076-->

   - ![ícone corrigir](../../assets/fix.svg) Correção de um problema de configuração de Elasticsearch para garantir que as configurações corretas de Elasticsearch fossem definidas em todos os ambientes.<!--MAGECLOUD-4474-->

>[!NOTE]
>
>Consulte [Versões de serviço](../services/services-yaml.md#service-versions) para obter uma lista dos serviços usados no Adobe Commerce na infraestrutura em nuvem e a compatibilidade de suas versões com o modelo da nuvem.

- ![novo ícone](../../assets/new.svg) **Atualizações de variável de ambiente**—

   - ![novo ícone](../../assets/new.svg) Ampliou a funcionalidade do `WARM_UP_PAGES` variável de ambiente para suportar o pré-carregamento de cache de páginas de produto específicas. Consulte a definição expandida na [variáveis pós-implantação](../environment/variables-post-deploy.md#warm_up_pages) tópico.<!--MAGECLOUD-4444-->

   - ![novo ícone](../../assets/new.svg) Adição de `ERROR_REPORT_DIR_NESTING_LEVEL` para simplificar o gerenciamento de dados de relatórios de erros no `<magento_root>/var/report/` diretório. Consulte a descrição da variável no [criar variáveis](../environment/variables-build.md#error_report_dir_nesting_level) tópico.

   - ![ícone corrigir](../../assets/fix.svg) Remoção da `SCD_EXCLUDE_THEMES`, `STATIC_CONTENT_THREADS`,`DO_DEPLOY_STATIC_CONTENT`, e `STATIC_CONTENT_SYMLINK` variáveis de ambiente. Consulte [Alterações incompatíveis com versões anteriores](backward-incompatible-changes.md#environment-configuration-changes).<!--MAGECLOUD-4407, MAGECLOUD-3873-->

   - ![ícone corrigir](../../assets/fix.svg) Correção de um problema no processo de configuração do Elastic Suite para que a configuração padrão seja substituída conforme esperado ao configurar o `ELASTICSUITE_CONFIGURATION` implantar variável sem o `_merge` opção.<!--MAGECLOUD-4388-->

- ![novo ícone](../../assets/new.svg) **Atualizações de comando da CLI**—

   - ![novo ícone](../../assets/new.svg) **Novo comando cron**— Agora é possível gerenciar manualmente o processamento de cron no ambiente de infraestrutura Adobe Commerce em nuvem usando o `cron:disable` e `cron:enable` comandos. Use o comando disable para interromper todos os processos cron ativos e desativar todos os trabalhos cron. Use o comando enable para reativar os processos do cron quando estiver pronto. Consulte [Desabilitar trabalhos cron](../application/crons-property.md#disable-cron-jobs).

   - ![novo ícone](../../assets/new.svg) **Relatório de erros aprimorado**—Adição de um melhor registro para falhas de comando CLI que ocorrem durante o processamento de ECE-Tools.<!--MAGECLOUD-4849-->

   - ![novo ícone](../../assets/new.svg) **Remover comandos de build obsoletos**— Os seguintes comandos de build foram removidos: `m2-ece-build`, `m2-ece-deploy`, `m2-ece-scd-dump`e renomeado `ece-tools docker` comandos para `ece-docker`. Consulte [Alterações incompatíveis com versões anteriores](backward-incompatible-changes.md)<!--MAGECLOUD-4392-->

- ![novo ícone](../../assets/new.svg) Remoção do obsoleto `build_options.ini` arquivo e adição da validação para falhar a criação, se o arquivo existir. Use o [.magento.env.yaml](../environment/configure-env-yaml.md) arquivo para configurar as opções de compilação.

- ![ícone corrigir](../../assets/fix.svg) Correção de um problema que causava a falha do processo de criação quando a variável `config.php` O arquivo está vazio.<!--MAGECLOUD-4127-->

## 2002.0.23

Data de lançamento: 27 de fevereiro de 2020

- ![ícone corrigir](../../assets/fix.svg) Correção de um problema de compatibilidade com o `ece-tools` Versões 2002.0.x que impediam a geração de conteúdo estático sob demanda de ser concluída com êxito no modo de produção.

## Versões anteriores

Consulte a [arquivo de notas de versão](cloud-release-archive.md) para a versão 2002.0.22 e anterior.
