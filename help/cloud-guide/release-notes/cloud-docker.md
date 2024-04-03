---
title: Pacote do Cloud Docker
description: Consulte uma lista das melhorias mais recentes no pacote do Cloud Docker.
feature: Cloud, Docker, Release Notes
recommendations: noDisplay, catalog
last-substantial-update: 2023-07-31T00:00:00Z
exl-id: 907d977f-2e9c-4553-a46b-000bc6a57b28
source-git-commit: 21754f2ee3df586cd03d57210741b36409ad2b36
workflow-type: tm+mt
source-wordcount: '3620'
ht-degree: 0%

---

# Pacote do Cloud Docker

A variável [`magento/magento-cloud-docker`](https://github.com/magento/magento-cloud-docker) O pacote de fornece funcionalidade e imagens do Docker para implantar o Adobe Commerce em um ambiente da nuvem local. Estas notas de versão descrevem os últimos aprimoramentos feitos neste pacote, que é um componente do [Cloud Tools Suite for Commerce](cloud-tools-suite.md).

A variável `magento/magento-cloud-docker` O pacote usa a seguinte sequência de versão: `<major>.<minor>.<patch>`

As notas de versão incluem:

- ![novo ícone](../../assets/new.svg) Novos recursos
- ![ícone corrigir](../../assets/fix.svg) Correções e aprimoramentos

<!--Add release notes below-->

## v1.3.6 {#latest}

Data de lançamento: 31 de julho de 2023

- ![novo ícone](../../assets/new.svg) **Nova versão do serviço adicionada**—OpenSearch 2.5
- ![novo ícone](../../assets/new.svg) **Ativar cache do Composer**—Agora é possível estender a configuração do Docker para habilitar a limpeza do cache do Composer ao iniciar o container do Docker. Consulte [Estender a configuração do Docker](https://developer.adobe.com/commerce/cloud-tools/docker/configure/extend-docker-configuration/) no _Cloud Docker for Commerce_ guia.

## v1.3.5

Data de lançamento: 10 de março de 2023

- ![novo ícone](../../assets/new.svg) **ionCube**—Adição da extensão ionCube para a imagem do PHP 8.1.
- ![novo ícone](../../assets/new.svg) **Adicionadas novas versões do serviço**—OpenSearch 2.3 e 2.4, PHP 8.2, Varnish 7.1.1.
- ![novo ícone](../../assets/new.svg) **Suporte avançado para PHP 8.2**—Correção de problemas de compatibilidade com determinadas versões do PHP 8.2.x para suportar o Commerce 2.4.6.
- ![ícone corrigir](../../assets/fix.svg) **Problema do compositor**—Correção de problemas que ocorriam após a atualização da versão do Composer nos contêineres do Docker.

## v1.3.4

Data de lançamento: 27 de outubro de 2022

- ![novo ícone](../../assets/new.svg) **Adição de novas imagens de verniz**—Imagens adicionadas para o Verniz 6.5, 7.0 e 7.1.<!-- MCLOUD-7879 -->

## v1.3.3

Data de lançamento: 13 de setembro de 2022

- ![novo ícone](../../assets/new.svg) **Suporte ao Apple M1 (ARM64)**—Adição de alterações nas imagens do Docker para habilitar o suporte à arquitetura Apple M1 (ARM64).<!-- MCLOUD-7989-2 MCLOUD-7989 -->
- ![ícone corrigir](../../assets/fix.svg) **Mailhog**—Correção de um problema em que o serviço Mailhog não capturava emails no modo de desenvolvedor.<!-- MCLOUD-8643 -->
- ![ícone corrigir](../../assets/fix.svg) **init-docker.sh**—Corrigido o validador de versões de serviço no `init-docker.sh` script.<!-- MCLOUD-8765 -->

## v1.3.2

Data de lançamento: 31 de março de 2022

- ![novo ícone](../../assets/new.svg) **Adição da imagem Elasticsearch 7.10**<!-- MCLOUD-8548 -->

## v1.3.1

Data de lançamento: 10 de março de 2022

- ![novo ícone](../../assets/new.svg) **Suporte ao PHP 8.1**—Suporte adicionado para PHP 8.1.
- ![novo ícone](../../assets/new.svg) **OpenSearch**—Imagens adicionadas do OpenSearch versões 1.1 e 1.2.
- ![novo ícone](../../assets/new.svg) **Composer 2.1**—Defina composer 2.1.x por padrão em imagens do PHP 8.x.
- ![novo ícone](../../assets/new.svg) **Melhorias nas imagens do PHP**—

   - Adição de imagens do PHP 8.1
   - Atualização do xDebug versão 3.1.2
   - xmlrpc 1.0.0RC3 atualizado

- ![ícone corrigir](../../assets/fix.svg) **Melhorias no Elasticsearch e OpenSearch**—Melhorias no Elasticsearch e no OpenSearch Dockerfiles; remoção da imagem Elasticsearch 5.2.
- ![ícone corrigir](../../assets/fix.svg) **Extensão de sódio**—Habilitou o `sodium` extensão por padrão em todas as imagens do PHP.
- ![ícone corrigir](../../assets/fix.svg) **Volume de cache do compositor**—Caminho fixo para o volume de cache do Composer para armazenar em cache os pacotes do Composer.
- ![ícone corrigir](../../assets/fix.svg) **Limitação de memória no nginx**—Limitação fixa da memória na imagem NGINX.

## v1.3.0

Data de lançamento: 25 de outubro de 2021

- ![ícone corrigir](../../assets/fix.svg) **Melhorar o fluxo de trabalho do modo Desenvolvedor**—Anteriormente, era necessário especificar o modo nas etapas de criação e implantação. Agora, a variável `--mode` opção no `build` a etapa determina o modo no `deploy` etapa. Não é mais necessário definir o modo após a implantação. Consulte [Modo de desenvolvedor](https://devdocs.magento.com/cloud/docker/docker-mode-developer.html).<!-- ACMP-1086 -->
- ![ícone corrigir](../../assets/fix.svg) **Melhorias no sistema de arquivos somente leitura**—<!-- ACMP-1106 -->
   - Correção de um problema que iniciava um contêiner PHP para configuração de email.
   - Pode usar variáveis de ambiente em arquivos INI.
   - Certifique-se de que os pontos de entrada do PHP não precisem de permissão de gravação.
- ![ícone corrigir](../../assets/fix.svg) **Atualizar nó**—Atualize a versão do Node fornecida; ao instalar o Node em imagens PHP-CLI, ele agora usa a versão LTS atual.<!-- ACMP-1539 -->
- ![ícone corrigir](../../assets/fix.svg) **Atualizar o Symfony**—Atualização das dependências de configuração do Symfony para compatibilidade com o Adobe Commerce 2.4.4.<!-- ACMP-1533 -->

## v1.2.4

Data de lançamento: 29 de julho de 2021

- ![novo ícone](../../assets/new.svg) **Novo `Zookeeper` container**—Adição de um [Contêiner Zookeeper](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#zookeeper-container) para gerenciar a configuração do provedor de bloqueio para projetos que não estão implantados na infraestrutura do Adobe Commerce na nuvem.<!--MCLOUD-8000-->

- ![novo ícone](../../assets/new.svg) **Adição de suporte para o Composer 2.0.**—Adição do Composer versão 2.0 ao arquivo de configuração do Composer para suportar atualizações do Composer 1.0 que está se aproximando do fim da vida útil.<!--MCLOUD-8003-->

## v1.2.3

Data de lançamento: 14 de junho de 2021

- ![novo ícone](../../assets/new.svg) **PHP 8.0 adicionado**—Atualização do PHP para a versão 8.0, permitindo que você aproveite todos os novos recursos e otimizações que o PHP 8.0 inclui.<!--MCLOUD-7941-->
- ![novo ícone](../../assets/new.svg) **Atualização para Vernish 6.6 e Elasticsearch 7.11.2**—Os links a seguir fornecem informações sobre a versão do [Cache de verniz 6.6](https://varnish-cache.org/releases/rel6.6.0.html#rel6-6-0) e Elasticsearch 7.11.2.<!--MCLOUD-7921-->
- ![novo ícone](../../assets/new.svg) **Adicionado `ioncube` extensão para imagem do PHP 7.4**—O `ioncube` Esta extensão foi adicionada novamente à imagem do PHP 7.4 depois de ter sido inicialmente excluída da atualização do PHP 7.3 para o PHP 7.4. *[Enviado por mattskr](https://github.com/magento/magento-cloud-docker/pull/314).*<!--PR #314-->
- ![novo ícone](../../assets/new.svg) **Adição de uma opção de sincronização de arquivo:`manual-native`**—O `manual-native` a opção de sincronização de arquivos fornece controle manual sobre a sincronização, o que fornece o melhor desempenho para ambientes macOS e Windows. Leia sobre como usar o `manual-native` opção em [Modo de desenvolvedor](https://devdocs.magento.com/cloud/docker/docker-mode-developer.html) e [Sincronização de dados em um ambiente de desenvolvedor do Docker](https://devdocs.magento.com/cloud/docker/docker-syncing-data.html#file-synchronization-options).<!--MCLOUD-7977-->
- ![novo ícone](../../assets/new.svg) **Exclusões de volume removidas de `up` e `down` comandos**—O `--volume` A opção foi removida da variável `bin/magento-docker up` e `bin/magento-docker down` comandos, substituídos pelo novo `bin/magento-docker init` com um aviso de perda de dados. Essa alteração ajuda a evitar a perda acidental de dados. *[Enviado por joeshelton-wagento](https://github.com/magento/magento-cloud-docker/pull/319).*<!--PR #319-->
- ![ícone corrigir](../../assets/fix.svg) **Atualizado `CN` valor do certificado gerado**— Removeu o codificado `CN` valor do Arquivo de docker. Esse valor criou um erro de certificado (`NET::ERR_CERT_INVALID`) que causou a `--host` opção para a variável `ece-docker build:compose` comando a ser ignorado.<!--MCLOUD-7934-->

## v1.2.2

Data de lançamento: 20 de abril de 2021

- ![novo ícone](../../assets/new.svg) **Atualizado `host.docker.internal` para ser independente de plataforma**— agora você pode criar os mesmos scripts Docker Compose para Ubuntu, Windows e macOS. O uso do Xdebug no Ubuntu não requer mais uma variável de ambiente separada. [Correção enviada por Igor Vitol](https://github.com/magento/magento-cloud-docker/pull/299).<!--Issue #298-->
- ![novo ícone](../../assets/new.svg) **Atualização de init-docker.sh**—Adição de `mounts` objeto para o `MAGENTO_CLOUD_APPLICATION` variável de ambiente. [Correção enviada por Chiranjeevi](https://github.com/magento/magento-cloud-docker/pull/299).<!--Issue #299-->
- ![novo ícone](../../assets/new.svg) **Atualização de init-docker.sh**—Atualizou o `init-docker.sh` script com o PHP 7.4 e versões Cloud Docker 1.2.1. [Correção enviada por David Manickam](https://github.com/magento/magento-cloud-docker/pull/300).<!--Issue #300-->
- ![novo ícone](../../assets/new.svg) **Sódio ativado por padrão**—Habilitou o `sodium` Extensão PHP por padrão dentro de imagens do PHP Docker.<!--MCLOUD-7548-->
- ![novo ícone](../../assets/new.svg) **`custom-registry`opção**—Adição de um `--custom-registry` opção para `php ./vendor/bin/ece-docker build:compose` comando para usar seu próprio registro de imagens.<!--MCLOUD-7476-->

  ```bash
  ./vendor/bin/ece-docker build:compose --custom-registry=my-registry.example.com
  ```

- ![novo ícone](../../assets/new.svg) **Versões antigas do Elasticsearch removidas**—Remoção das versões 1.7 e 2.4 do Elasticsearch das imagens do Elasticsearch.<!--MCLOUD-7504-->
- ![novo ícone](../../assets/new.svg) **Geração automática de certificados NGINX**—Remoção dos certificados existentes da imagem NGINX. Os certificados NGINX agora são gerados automaticamente com cada nova implantação para melhorar a segurança.<!--MCLOUD-7396-->
- ![ícone corrigir](../../assets/fix.svg) **Ativado`opcache.validate_timestamps`**—Habilitou o `opcache.validate_timestamps` Configuração do PHP por padrão no modo de desenvolvedor. A habilitação dessa configuração corrigiu o problema em que as alterações no sistema de arquivos não eram reconhecidas no Docker.<!--MCLOUD-7466-->
- ![ícone corrigir](../../assets/fix.svg) **Fixo`build:custom:compose`**—Corrigiu o `build:custom:compose` comando para emitir um erro quando os arquivos não puderem ser substituídos durante o processo de compilação. Gerar um erro evita situações em que `docker-compose up` pode estar usando os arquivos errados.<!--MCLOUD-7457-->
- ![ícone corrigir](../../assets/fix.svg) **Fixo `--sync_engine="native"` opção**—Correção do problema onde, no modo de produção (`--mode="production"`), o `--sync_engine="native"` opção não criaria entradas para pastas locais na variável `docker.composer.yml` arquivo.<!--MCLOUD-7254-->
- ![ícone corrigir](../../assets/fix.svg) **Correção de erros de validação de versão de serviço**—Versões de serviço adicionadas para [!DNL RabbitMQ], Elasticsearch e outros serviços para a `type` propriedade na `MAGENTO_CLOUD_RELATIONSHIP` variável. Adicionar essas versões à `relationships` variável corrigida os erros de validação que ocorriam durante a fase de implantação.<!--MCLOUD-7572-->

## v1.2.1

Data de lançamento: 21 de dezembro de 2020

- ![novo ícone](../../assets/new.svg) **Opções de comando do NGINX**—Adição de opções de comando de compilação para alterar o número de NGINX `worker_processes` e NGINX `worker_connections` para TLS e serviços da Web. A variável `worker_process` O parâmetro mantém a capacidade de definir o valor como `auto`. Exemplos: <!--MCLOUD-7259-->

  ```terminal
  ./vendor/bin/ece-docker build:compose --nginx-worker-processes=2
  ./vendor/bin/ece-docker build:compose --nginx-worker-connections=2048
  ```

- ![novo ícone](../../assets/new.svg) **Opção de comando TLS**—Adição da opção de comando build para criar uma configuração sem o serviço TLS. Exemplo: <!--MCLOUD-7259-->

  ```terminal
  ./vendor/bin/ece-docker build:compose --no-tls
  ```

- ![novo ícone](../../assets/new.svg) **Consumo de memória NGINX**—Redução da memória consumida pelo processo NGINX para TLS e serviços da Web.<!--MCLOUD-7259-->

- ![novo ícone](../../assets/new.svg) **Blackfire**—Desativação da extensão PHP do Blackfire por padrão na imagem do Cloud Docker.

- ![ícone corrigir](../../assets/fix.svg) **Contêiner PHP-FPM**—Corrigiu a verificação de integridade do contêiner PHP-FPM alterando o `WEB_PORT` de `80` para `8080`.<!--MCLOUD-7232-->

- ![ícone corrigir](../../assets/fix.svg) **Nomeação de volume inválida**—Correção de um erro com nome de volume inválido no modo de desenvolvedor.<!--MCLOUD-7442-->

- ![ícone corrigir](../../assets/fix.svg) **Porta NGINX upstream**—Atualização da imagem do Docker NGINX 1.19 para usar a porta 8080 e evitar um loop infinito. [Correção enviada por David Manickam](https://github.com/magento/magento-cloud-docker/pull/296).<!--Issue 295-->

## v1.2.0

Data de lançamento: 9 de novembro de 2020

- ![novo ícone](../../assets/new.svg) **Atualizações de contêiner—**

   - ![novo ícone](../../assets/new.svg) **Contêiner PHP-FPM**—Adição de suporte para a extensão gnupg PHP. [Correção enviada por G Arvind da Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/210).<!--MCLOUD-5981-->

   - ![ícone corrigir](../../assets/fix.svg) **Contêiner do banco de dados**—Corrigiu a verificação de integridade do container de banco de dados adicionando a senha de banco de dados necessária ao comando de verificação de integridade.<!--MCLOUD-7122-->

   - ![novo ícone](../../assets/new.svg) **contêiner Elasticsearch**

      - Adição de suporte ao Elasticsearch 7.9 para compatibilidade com versões futuras do Adobe Commerce.<!--MCLOUD-7190-->

      - **Configuração do plug-in do Elasticsearch**—Adição de suporte para usar as informações de configuração do plug-in Elasticsearch do `services.yaml` arquivo para gerar o `docker-compose.yaml` arquivo para um ambiente do Cloud Docker for Commerce. Consulte [plug-ins do Elasticsearch](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#elasticsearch-plugins).<!--MCLOUD-2789-->

      - **Suporte a plug-in do Elasticsearch**—Adição de suporte para os seguintes plug-ins do Elasticsearch: `analysis-icu`, `analysis-phonetic`, `analysis-stempel`, e `analysis-nori`. A variável `analysis-icu` e `analysis-phonetic` Os plug-ins do são instalados por padrão. É possível adicionar ou remover a variável `analysis-stempel` e `analysis-nori` plug-ins conforme necessário.<!--MCLOUD-2789-->

   - ![novo ícone](../../assets/new.svg) **Contêiner CLI**

      - **Executar comandos dentro de contêineres PHP do Docker**—Agora você pode usar a CLI do Cloud Docker para executar comandos dentro de containers PHP em seu ambiente Docker sem precisar instalar o PHP no host. Por exemplo, o comando a seguir cria a configuração:  `./bin/magento-docker php 7.3 vendor/bin/ece-docker build:compose`. Consulte [CLI do Cloud Docker](https://devdocs.magento.com/cloud/docker/docker-quick-reference.html#magento-cloud-docker-cli). [Correção enviada por G Arvind da Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/209).<!--MCLOUD-5982-->

      - Adição do OpenSSH-client aos contêineres da CLI do PHP. Agora, você pode usar o encaminhamento ssh-agent para o Composer se o `composer.json` O arquivo contém repositórios Git privados que exigem um cliente ssh para usar comandos do Composer.<!--MCLOUD-6008-->

   - ![ícone corrigir](../../assets/fix.svg) **Contêiner TLS**—Agora, a variável [Contêiner TLS](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#tls-container) baseia-se no `https://hub.docker.com/r/magento/magento-cloud-docker-nginx` Imagem do Docker em vez da imagem do CentOS. Essa alteração corrige problemas que causavam erros ao enviar solicitações HTTPS entre contêineres no ambiente do Cloud Docker.<!--MCLOUD-6469-->

   - ![novo ícone](../../assets/new.svg) **Contêiner de teste**—Adição de um contêiner de teste para teste de aplicativos e adição de `--with-test` opção para o Docker `build:compose` comando para criar o contêiner somente ao testar no ambiente do Docker. Consulte [teste de aplicativo](https://devdocs.magento.com/cloud/docker/docker-test-app-mftf.html).<!--MCLOUD-6394-->

   - ![novo ícone](../../assets/new.svg) **Contêiner FPM-XDEBUG**

      - ![novo ícone](../../assets/new.svg) **Configurar o Xdebug no Linux**—Adição de `--set-docker-host` opção para o `ece-docker build:compose` comando para configurar o `host.docker.internal` no contêiner Xdebug. Essa opção é necessária para usar o Xdebug em sistemas Linux. Consulte [Configurar Xdebug para Docker](https://devdocs.magento.com/cloud/docker/docker-development-debug.html).<!--MCLOUD-6430-->

      - ![ícone corrigir](../../assets/fix.svg) Correção da configuração da variável Xdebug para o PONTO DE ENTRADA do Docker para resolver `uninitialized "with_xdebug" variable` erros nos logs. [Correção apresentada por Florent Olivaud](https://github.com/magento/magento-cloud-docker/pull/218)<!--MCLOUD-6043-->

- ![novo ícone](../../assets/new.svg) **Alterações na configuração do Docker**

   - **Configuração MailHog**—Agora você pode usar o seguinte `ece-docker build:compose` opções de comando para desabilitar MailHog e especificar portas: `--no-mailhog`, `--mailhog-http-port`, e `--mailhog-smtp-port`. Consulte [Configurar email](https://devdocs.magento.com/cloud/docker/docker-config.html#set-up-email).<!--MCLOUD-6898, MCLOUD-6660-->

   - Para o Cloud Docker para Commerce 1.2.0 e posterior, o Adobe agora fornece imagens do Docker para cada versão de patch, e o gerador de configuração do Docker cria a configuração do Docker com uma versão de patch especificada, em vez de usar a mais recente. Anteriormente, o gerador de configuração do Docker criava a configuração usando a versão de patch mais recente, o que poderia quebrar o Cloud Docker para ambientes de comércio criados com uma versão anterior.<!--MCLOUD-7093-->

   - **Especificar imagens e versões personalizadas na configuração personalizada do Cloud Docker**—Atualizou o `build:custom:compose` comando com opções para especificar imagens e versões personalizadas ao gerar um arquivo de configuração de composição do Docker personalizado (`docker-compose.yaml`). Consulte [Criar uma configuração personalizada de composição do Docker](https://devdocs.magento.com/cloud/docker/docker-config-sources.html#build-a-custom-docker-compose-configuration). <!--MCLOUD-7089-->

   - Atualização da configuração do host Docker para expor a porta 443 para habilitar o acesso ao Adobe Commerce (`https://magento2.docker`) de todos os contêineres CLI. Você pode alterar a porta padrão adicionando a variável `--tls-port` opção ao gerar o arquivo de configuração do Docker.<!--MCLOUD-6806-->

- ![ícone corrigir](../../assets/fix.svg) Correção de um problema que causava a falha da build do Cloud Docker para Commerce se a variável `app/etc/env.php` arquivo existe.<!--MCLOUD-6732-->

- ![ícone corrigir](../../assets/fix.svg) Atualização da configuração de compilação para substituir volumes nomeados por volumes regulares a fim de evitar problemas ao implantar o Cloud Docker for Commerce no Linux ou no Subsistema do Windows para Linux (WSL2).<!--MCLOUD-6732-->

- ![ícone corrigir](../../assets/fix.svg) Atualização do Cloud Docker para testes funcionais do Commerce para oferecer suporte ao Composer 2.0.<!--MCLOUD-7183-->

## v1.1.2

Data de lançamento: 9 de setembro de 2020

- ![novo ícone](../../assets/new.svg) Suporte adicionado para o Elasticsearch 7.7<!--MCLOUD-6219-->

## v1.1.1

Data de lançamento: 5 de agosto de 2020

- ![ícone corrigir](../../assets/fix.svg) **Configuração de email atualizada**—Atualização da configuração padrão do Cloud Docker for Commerce para oferecer suporte ao serviço MailHog em vez de usar SendMail. Consulte [Configurar email](https://devdocs.magento.com/cloud/docker/docker-config.html#set-up-email).<!--MCLOUD-5624-->

- ![ícone corrigir](../../assets/fix.svg) Restaurada a biblioteca PS para a configuração de ambiente do Cloud Docker para corrigir `ps:  command not found` erros.<!--MCLOUD-6621-->

- ![ícone corrigir](../../assets/fix.svg) Atualização da configuração padrão do Cloud Docker for Commerce para remover a montagem automática do ponto de entrada do banco de dados e dos volumes do MariaDB para corrigir `Cannot create container for service db` erros que podem ocorrer ao iniciar o ambiente do Cloud Docker.

  Agora, você pode configurar o ambiente do Cloud Docker para montar os diretórios do banco de dados adicionando as seguintes opções à `ece-docker build:compose` comando: `--with-entry-point` e `with-mariadb-conf`. Consulte [Opções de configuração de serviço](https://devdocs.magento.com/cloud/docker/docker-containers.html#service-configuration-options).<!--MCLOUD-6424-->

- ![novo ícone](../../assets/new.svg) **Atualizações de comando da CLI**

| Ação | Comando |
| ------------------------------------------------------------------------------- | -------------------------------------------------------------- |
| Adicione um ponto de entrada ao contêiner do banco de dados para restaurar o banco de dados do backup | `./vendor/bin/ece-docker build:compose --db --with-entrypoint` |
| Adicionar um volume de configuração do MariaDB | `./vendor/bin/ece-docker build:compose --db --mariadb-conf` |

## v1.1.0

Data de lançamento: 25 de junho de 2020

- ![novo ícone](../../assets/new.svg) **Adição de suporte para a solução de desempenho de banco de dados dividido**— Agora você pode configurar e implantar uma loja usando a solução de desempenho de banco de dados Split no ambiente do Cloud Docker.<!--MCLOUD-3740-->

- ![novo ícone](../../assets/new.svg) **Suporte para implantação de Adobe Commerce e Magento Open Source**—Agora você pode usar o Cloud Docker for Commerce para implantar um ambiente de desenvolvimento local para projetos que não estão hospedados no Adobe Commerce na infraestrutura em nuvem.<!--MCLOUD-5667-->

- ![novo ícone](../../assets/new.svg) **Suporte para Blackfire.io**—Adição de suporte para usar o [Extensão do Blackfire.io](https://devdocs.magento.com/cloud/docker/docker-config-blackfire-io.html) para testes de desempenho automatizados. [Correção enviada por Adarsh Manickam da Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/202)<!--MCLOUD-5857-->

- ![novo ícone](../../assets/new.svg) **Atualizações de contêiner**

   - **Verniz**—Agora, o Varnish é o cache padrão ao implantar o Adobe Commerce em um ambiente do Cloud Docker usando uma versão compatível do modelo de aplicativo na nuvem. Consulte [Container de verniz](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#varnish-container).<!--MCLOUD-2634-->

   - Adição de `--no-varnish` opção para ignorar a instalação do serviço Vernish ao gerar o arquivo de configuração do Cloud Docker.<!--MCLOUD-2634-->

   - ![novo ícone](../../assets/new.svg) **Banco de dados**

      - Adição do suporte para o banco de dados MySQL. Agora, você pode configurar o ambiente do Cloud Docker com MariaDB ou MySQL. Consulte [Opções de configuração de serviço](https://devdocs.magento.com/cloud/docker/docker-containers.html#service-configuration-options).<!--MCLOUD-5691-->

      - Adição da capacidade de definir as configurações de incremento e deslocamento para replicação de banco de dados ao gerar o arquivo de composição do Docker. Consulte [Contêineres de serviço](https://devdocs.magento.com/cloud/docker/docker-containers.html#service-containers).<!--MCLOUD-5735-->

   - ![novo ícone](../../assets/new.svg) **PHP-FPM**

      - Suporte adicionado para o PHP 7.4. [Correção enviada por Mohanela Murugan da Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/198)<!--MCLOUD-198-->

      - Adição da capacidade de copiar um `php.ini` arquivo no diretório do projeto raiz para o ambiente Cloud Docker e aplique configurações personalizadas do PHP para os contêineres PHP-FPM e CLI. Consulte [Personalizar configurações do PHP](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#customize-php-settings). [Correção enviada por Mathew Beane da Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/130).<!--MCLOUD-6012-->

      - Adição de uma verificação de integridade do contêiner. [Correção enviada por Visanth Sampath da Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/188).<!--MCLOUD-5752-->

   - ![ícone corrigir](../../assets/fix.svg) **Node.js**—Atualização da versão padrão do Node.js da versão 8 para a versão 10 para melhorar a segurança. A versão 8 do Node.js está obsoleta e não é mais atualizada com correções de erros ou patches de segurança. [Correção enviada por Mohan Elamurugan da Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/183).<!--MCLOUD-5586-->

   - ![novo ícone](../../assets/new.svg) **Elasticsearch**

      - Suporte adicionado para o Elasticsearch 6.8, 7.2, 7.5 e 7.6.<!--MCLOUD-4050, MCLOUD-5855,MCLOUD-5860-->

      - Adição da capacidade de personalizar o [configuração do contêiner Elasticsearch](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#elasticsearch-container) ao gerar o arquivo de configuração de composição do Docker.<!--MCLOUD-3059-->

      - Adição de `--no-es` opção para as opções de configuração do serviço para gerar o arquivo de configuração Docker Compose. Use essa opção para ignorar a instalação do contêiner de Elasticsearch e usar a pesquisa MySQL. Essa opção é compatível somente com as versões 2.3.5 e anteriores do Adobe Commerce.<!--MCLOUD-3766-->

   - ![novo ícone](../../assets/new.svg) **Contêiner FPM-XDEBUG**—Adição de uma opção de configuração de serviço para instalar e configurar o Xdebug para depurar o PHP no ambiente do Cloud Docker. Consulte [Configurar Xdebug](https://devdocs.magento.com/cloud/docker/docker-development-debug.html).<!--MCLOUD-4098-->

- ![novo ícone](../../assets/new.svg) **Alterações na configuração do Docker**

   - Adição de verificações de integridade para os contêineres de serviço PHP-FPM, Redis, Elasticsearch e MySQL Docker.<!--MCLOUD-3335 and MCLOUD-5856-->

   - Alteração do modo de sincronização de arquivos padrão para `native` no Modo de desenvolvedor.<!--MCLOUD-3890 -->

   - Adição de informações de versão à imagem genérica do contêiner de serviço do Docker ao gerar o `docker-compose.yml` arquivo.<!--MCLOUD-3878-->

   - Aprimoramento da capacidade de lidar com grandes respostas do contêiner upstream de PHP-FPM ao aumentar o `fastcgi_buffers` para o servidor Nginx.<!--MCLOUD-5980-->

   - Desempenho aprimorado da sincronização de arquivos mutagen ao adicionar uma segunda sessão de sincronização para sincronizar arquivos no `vendor` diretório. Essa alteração impede que o mutagen fique paralisado durante o processo de sincronização de arquivos. [Correção enviada por Mathew Beane da Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/127).<!--MCLOUD-6010-->

   - ![novo ícone](../../assets/new.svg) **Atualizações de comando da CLI**

| Ação | Comando |
| -------- | --------------- |
| Limpar cache Redis | `bin/magento-docker flush-redis` |
| Limpar cache de verniz | `bin/magento-docker flush-varnish` |
| Ignorar instalação padrão do Verniz | `.vendor/bin/ece-docker build:compose --no-varnish`<!--MCLOUD-2634--> |
| [Personalizar opções de Elasticsearch](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#elasticsearch-container) | `.vendor/bin/ece-docker build:compose --es-env-var`<!--MCLOUD-3059--> |
| [Remover configuração de Elasticsearch](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#elasticsearch-container) | `.vendor/bin/ece-docker build:compose --no-es`<!--MCLOUD-3766--> |
| Configurar o contêiner de BD com o MySQL versão 5.6 ou 5.7 | `./vendor/bin/ece-docker build:compose --db <mysql-version-number> --db-image mysql`<!--MCLOUD-5691--> |
| Especificar URL de base personalizada | `./vendor/bin/ece-docker build:compose --host=<hostname> --port=<port-number>`<!--MCLOUD-3063--> |
| [Adicionar contêiner para configuração do Xdebug](https://devdocs.magento.com/cloud/docker/docker-development-debug.html) | `.vendor/bin/ece-docker build:compose --mode developer --sync-engine native --with-xdebug`<!--MCLOUD-4098--> |

- ![ícone corrigir](../../assets/fix.svg) Correção da configuração da sincronização de arquivos mutagen para impedir que o mutagen crie sessões obsoletas. [Correção enviada por Mathew Beane da Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/127).<!--MCLOUD-6010-->

- ![ícone corrigir](../../assets/fix.svg) Correção de um problema de configuração que causava erros de sintaxe no log de composição do Docker ao iniciar o container PHP-FPM. [Correção enviada por Mathew Beane da Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/129)<!--MCLOUD-3958-->

- ![ícone corrigir](../../assets/fix.svg) Correção de erros de conflito de volume que às vezes ocorriam ao usar vários ambientes do Docker. [Correção enviada por G Arvind da Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/168).

- ![ícone corrigir](../../assets/fix.svg) Correção de um problema que causava a `ece-docker build:compose` comando para falhar se a configuração incluir Blackfire.io. [Correção enviada por G Arvind da Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/199). <!--MCLOUD-5797-->

- ![ícone corrigir](../../assets/fix.svg) Atualização da configuração de imagem da CLI do PHP para evitar erros de memória insuficiente que ocorriam ao instalar vários pacotes usando o Cloud Docker for Commerce. [Correção enviada por Mohan Elamurugan da Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/197).*<!--MCLOUD-5818-->

- ![ícone corrigir](../../assets/fix.svg) Adição de suporte para vários usuários do MySQL no ambiente do Cloud Docker. Em versões anteriores, a variável `build:compose` falha na operação se a variável `magento.app.yaml` arquivo especificado para vários usuários do banco de dados. [Correção enviada por G Arvind da Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/181).<!--MCLOUD-5670-->

- ![ícone corrigir](../../assets/fix.svg) Removido `rsyslog` do Cloud Docker para contêineres PHP do Commerce para resolver problemas de compatibilidade que causavam notificações de aviso durante a implantação. O Cloud Docker não usa o utilitário rsyslog.<!--MCLOUD-6173-->

## v1.0.0

Data de lançamento: 5 de fevereiro de 2020

- ![novo ícone](../../assets/new.svg) **Criação de um pacote separado para entrega`Cloud Docker for Commerce`**—O código-fonte foi movido para fornecer o Cloud Docker para Commerce a partir do `ece-tools` repositório para o [novo `magento-cloud-docker` repositório](https://github.com/magento/magento-cloud-docker) para manter a qualidade do código e fornecer versões independentes. O novo pacote é uma dependência para ECE-Tools v2002.1.0 e posteriores.

  Ao atualizar as ferramentas ece, você também atualiza o `magento/magento-cloud-docker` pacote para a versão 1.0.0. Se você usou o Cloud Docker para Commerce com um `ece-tools` versão (2002.0.x), revise a [incompatibilidades anteriores](backward-incompatible-changes.md) e atualize seu projeto como scripts, comandos e processos, conforme necessário.

- ![novo ícone](../../assets/new.svg) **Adição do controle de versão às imagens do Docker**—Você deve atualizar o `magento/magento-cloud-docker` pacote para obter as imagens atualizadas.<!--MAGECLOUD-4737-->

- ![novo ícone](../../assets/new.svg) **Atualizações de contêiner**—

   - ![novo ícone](../../assets/new.svg) **Contêiner PHP-FPM**—

      - ![novo ícone](../../assets/new.svg) **Adição de suporte a Node.js**—Atualização da imagem PHP-FPM para suportar o nó, npm e os recursos grunt-cli dentro do recipiente PHP.<!--MAGECLOUD-3953-->

      - ![novo ícone](../../assets/new.svg) **Suporte adicionado para [ionCube](https://www.ioncube.com/)**—Atualização da configuração padrão do Docker para oferecer suporte ao ionCube no ambiente de desenvolvimento local do Docker.<!--MAGECLOUD-4354-->

   - ![novo ícone](../../assets/new.svg) **container da Web**—

      - ![novo ícone](../../assets/new.svg) **Personalizar configuração do NGINX**—Adição da capacidade de montar um personalizado `nginx.conf` para o ambiente do Cloud Docker for Commerce. Consulte [container da Web](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#web-container).<!--MAGECLOUD-4204-->

      - ![novo ícone](../../assets/new.svg) **Certificados NGINX gerados automaticamente**—O arquivo de configuração do Docker agora inclui a configuração para gerar automaticamente certificados NGINX para o contêiner da Web.<!--MAGECLOUD-4258-->

   - ![novo ícone](../../assets/new.svg) **Novo contêiner Selenium**—Adição de um [Contêiner de selênio](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#selenium-container) para suportar o teste de aplicativos Adobe Commerce usando o Magento Functional Testing Framework (MFTF).<!--MAGECLOUD-4040-->

   - ![novo ícone](../../assets/new.svg) **[!DNL RabbitMQ]suporte à versão**—Atualizou o [!DNL RabbitMQ] configuração de contêiner para oferecer suporte [!DNL RabbitMQ] versão 3.8.<!--MAGECLOUD-4674-->

   - ![ícone corrigir](../../assets/fix.svg) **Contêiner de banco de dados persistente**—O `magento-db: /var/lib/mysql` O volume do banco de dados agora persiste depois que você interrompe e remove a configuração do Docker e restaura quando você reinicia a configuração do Docker. Agora, você deve excluir manualmente o volume do banco de dados. Consulte [Contêineres de banco de dados].<!--MAGECLOUD-3978-->

   - ![novo ícone](../../assets/new.svg) **Contêiner TLS**—

      - ![novo ícone](../../assets/new.svg) **Atualização da imagem base do container para usar a imagem oficial**—O [Contêiner TLS em nuvem](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#tls-container) imagem agora é baseada no oficial `debian:jessie` Imagem do Docker.—<!--MAGECLOUD-4163-->

      - ![novo ícone](../../assets/new.svg) **Adição de suporte para o [Libra de Proxy de Terminação TLS]**—O [Arquivo de configuração Libra](https://github.com/magento/magento-cloud-docker/blob/1.0/images/tls/) adiciona as seguintes variáveis ENV para personalizar a configuração do Docker para o contêiner TLS:

         - **`TimeOut`**—Define o valor de tempo limite de Time to First Byte (TTFB). O valor padrão é de 300 segundos.

         - **`RewriteLocation`**—Determina se o proxy libra reescreve o local no URL da solicitação por padrão. O padrão é `0` para evitar que a regravação interrompa os redirecionamentos para sites externos, como um site SSO externo. [Fixação apresentada por Sorin Sugar](https://github.com/magento/magento-cloud-docker/pull/37)<!--MAGECLOUD-4061-->

      - ![novo ícone](../../assets/new.svg) Valor de tempo limite na configuração do contêiner TLS aumentado de 15 para 300 segundos. [Correção enviada por Mathew Beane da Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/78)<!--MAGECLOUD-4460-->

   - ![novo ícone](../../assets/new.svg) **Container de verniz**—

      - ![novo ícone](../../assets/new.svg) **Atualização da imagem base do container para usar a imagem oficial**—O [Contêiner de verniz da nuvem](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#varnish-container) baseia-se agora na avaliação oficial. `centos` Imagem do Docker.<!--MAGECLOUD-4163-->

      - ![novo ícone](../../assets/new.svg) **Configuração de tempo limite padrão aprimorada**-Adicionado `.first_byte_timeout` e `.between_bytes_timeout` configuração para o contêiner Verniz. Ambos os valores de tempo limite são padronizados como `300s` (5 minutos). [Correção enviada por Mathew Beane da Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/78)<!--MAGECLOUD-4460-->

      - ![ícone corrigir](../../assets/fix.svg) **Ignorar verniz durante sessões do Xdebug**—Atualização da configuração do contêiner Verniz para retornar `pass` em solicitações recebidas quando o Xdebug está ativado. Em versões anteriores, não era possível usar o Xdebug se o ambiente do Docker incluísse verniz. [Correção enviada por Mathew Beane da Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/111).<!--MAGECLOUD-4873-->

- ![novo ícone](../../assets/new.svg) **Alterações na configuração do Docker**—

   - ![novo ícone](../../assets/new.svg) **Gerenciar montagens e volumes do seu projeto**— adição da capacidade de gerenciar montagens e volumes ao iniciar um ambiente Docker para desenvolvimento local. Consulte [Compartilhamento de dados do projeto].<!--MAGECLOUD-3248-->

   - ![novo ícone](../../assets/new.svg) **Suporte para modo de ponte de rede**—Adição de suporte ao modo bridge de rede para habilitar conexões entre contêineres Docker na rede local.<!--MAGECLOUD-4165-->

   - ![novo ícone](../../assets/new.svg) **Contêiner Cron desabilitado por padrão**—Para melhorar o desempenho, o contêiner do Cron não é mais configurado por padrão quando você cria o ambiente do Docker. Você pode usar o `--with-cron` no comando de compilação do Docker para adicionar um contêiner Cron ao seu ambiente. Consulte [Gerenciamento de trabalhos cron](https://devdocs.magento.com/cloud/docker/docker-manage-cron-jobs.html).<!--MAGECLOUD-5181-->

   - ![novo ícone](../../assets/new.svg) **Parar de sincronizar arquivos de backup grandes**—Adição de despejos de BD e arquivos — ZIP, SQL, GZ e BZ2 — à lista de exclusão na `dist/docker-sync.yml` e `dist/mutagen.sh` arquivos. A sincronização de arquivos grandes (>1 GB) pode causar um período de inatividade e os arquivos de backup normalmente não exigem sincronização, pois podem ser gerados novamente.<!--MAGECLOUD-3979-->

- ![novo ícone](../../assets/new.svg) **Alterações de comando**—

   - ![ícone corrigir](../../assets/fix.svg) A variável foi renomeada `./bin/docker` arquivo para `./bin/magento-docker` para corrigir um problema que causava a quebra de alguns ambientes do Docker porque a variável `./bin/docker` O arquivo substitui arquivos binários existentes do Docker. Este é um [alteração incompatível com versões anteriores](backward-incompatible-changes.md) que requer atualizações nos scripts e comandos.<!-- MAGECLOUD-4038 -->

   - ![novo ícone](../../assets/new.svg) **Adição de uma opção de configuração de serviço para expor a porta do banco de dados ao host**—Use o `--expose-db-port= [Fix submitted by Adarsh Manickam from Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/101).<PORT>` opção para expor a porta do banco de dados ao host ao criar o `docker-compose.yml` arquivo: `bin/ece-docker build:compose --expose-db-port=<PORT>`<!--MAGECLOUD-4454-->

   - ![novo ícone](../../assets/new.svg) **Novo comando pós-implantação**—Anteriormente, os ganchos pós-implantação definidos no `.magento.app.yaml` arquivo executado automaticamente depois de implantar o Adobe Commerce em um contêiner do Cloud Docker usando o `cloud-deploy` comando. Agora, você deve emitir um relatório separado `cloud-post-deploy` comando para executar os ganchos pós-implantação após a implantação. Consulte as instruções atualizadas do Launch para [desenvolvedor](https://devdocs.magento.com/cloud/docker/docker-mode-developer.html) e [produção](https://devdocs.magento.com/cloud/docker/docker-mode-production.html) modo.<!--MAGECLOUD-3996-->

   - ![novo ícone](../../assets/new.svg) Adição de `--rm` opção para `./bin/magento-docker` comandos para construir e implantar contêineres. Isso remove o contêiner depois que a tarefa é concluída.<!--MAGECLOUD-4205-->

   - ![novo ícone](../../assets/new.svg) **Atualizações para `build:compose` comando**—

      - ![novo ícone](../../assets/new.svg) Adição de `--sync-engine="native"` opção para o `docker-build` comando para desativar a sincronização de arquivos ao gerar o arquivo de configuração Docker Compose no modo de desenvolvedor. Use essa opção ao desenvolver em sistemas Linux, que não exigem sincronização de arquivos para o desenvolvimento local do Docker. Consulte [Sincronização de dados no ambiente do Docker](https://devdocs.magento.com/cloud/docker/docker-syncing-data.html).<!--MCLOUD-3231, MCLOUD-3890-->

   - ![novo ícone](../../assets/new.svg) Alteração da configuração de sincronização de arquivos padrão de `docker-sync` para `native`. [Correção enviada por Mathew Beane da Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/124).<!--MAGECLOUD-5066-->

- ![novo ícone](../../assets/new.svg) **Melhorias na validação**—

   - ![novo ícone](../../assets/new.svg) Validação adicionada ao processo de implantação para ambientes de desenvolvimento do Docker local para verificar se a configuração do ambiente de nuvem inclui a chave de criptografia necessária para descriptografar o banco de dados. Agora, você receberá uma mensagem de erro no log se a configuração do ambiente não especificar um valor para a chave de criptografia.<!--MAGECLOUD-4423-->

   - ![novo ícone](../../assets/new.svg) Adição de uma verificação de integridade do contêiner ao serviço Elasticsearch para garantir que o serviço esteja pronto antes de continuar com o processamento de compilação e implantação. Se a verificação de integridade retornar um erro, o container será reiniciado automaticamente.<!--MAGECLOUD-4456-->
