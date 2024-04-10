---
title: Atualizar versão do Commerce
description: Saiba como atualizar a versão do Adobe Commerce no projeto de infraestrutura em nuvem.
feature: Cloud, Upgrade
exl-id: 87821007-4979-4a20-940b-aa3c82c192d8
source-git-commit: 99272d08a11f850a79e8e24857b7072d1946f374
workflow-type: tm+mt
source-wordcount: '1439'
ht-degree: 0%

---

# Atualizar versão do Commerce

Você pode atualizar a base de código do Adobe Commerce para uma versão mais recente. Antes de atualizar o projeto, revise o [Requisitos do sistema](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/system-requirements.html) no _Instalação_ guia para os requisitos de versão de software mais recentes.

Dependendo da configuração do seu projeto, suas tarefas de atualização podem incluir o seguinte:

- Serviços de atualização — como MariaDB (MySQL), OpenSearch, RabbitMQ e Redis — para compatibilidade com novas versões do Adobe Commerce.
- Converta um arquivo de gerenciamento de configuração mais antigo.
- Atualize o `.magento.app.yaml` arquivo com novas configurações para ganchos e variáveis de ambiente.
- Atualize extensões de terceiros para a versão mais recente com suporte.
- Atualize o `.gitignore` arquivo.

{{upgrade-tip}}

{{pro-update-service}}

## Atualizar a partir de versões anteriores

Se você estiver iniciando uma atualização de uma versão do Commerce anterior à 2.1, algumas restrições na base de código do Adobe Commerce podem afetar sua capacidade de _atualizar_ para uma versão específica das ferramentas ECE ou para _atualização_ para a próxima versão compatível do Commerce. Use a tabela a seguir para determinar o melhor caminho:

| Versão atual | Caminho de atualização |
| ----------------- | ------------ |
| 2.1.3 e anterior | Atualize o Adobe Commerce para a versão 2.1.4 ou posterior antes de continuar. Em seguida, execute um [atualização única para instalar o ECE-Tools](../dev-tools/install-package.md). |
| 2.1.4 - 2.1.14 | [Atualizar ECE-Tools](../dev-tools/update-package.md) pacote.<br>Consulte as notas de versão do [2002.0.9](../release-notes/cloud-release-archive.md#v200209) e versões posteriores 2002.0.x. |
| 2.1.15 - 2.1.16 | [Atualizar ECE-Tools](../dev-tools/update-package.md) pacote.<br>Consulte as notas de versão do[2002.0.9](../release-notes/cloud-release-archive.md#v200209) e depois. |
| 2.2.x e posterior | [Atualizar ECE-Tools](../dev-tools/update-package.md) pacote.<br>Consulte as notas de versão do[2002.0.8](../release-notes/cloud-release-archive.md#v200208) e depois. |

{style="table-layout:auto"}

{{ece-tools-package}}

## Gerenciamento de configuração

Versões anteriores do Adobe Commerce, como 2.1.4 ou posterior a 2.2.x ou posterior, usavam um `config.local.php` arquivo para Gerenciamento de configuração. Adobe Commerce versão 2.2.0 e posteriores usam o `config.php` arquivo, que funciona exatamente como o `config.local.php` arquivo, mas ele tem definições de configuração diferentes que incluem uma lista de módulos ativados e opções de configuração adicionais.

Ao atualizar de uma versão mais antiga, você deve migrar a `config.local.php` arquivo para usar o mais recente `config.php` arquivo. Use as etapas a seguir para fazer backup do arquivo de configuração e criar um.

**Para criar uma variável temporária `config.php` arquivo**:

1. Criar uma cópia de `config.local.php` arquivo e nomeie-o `config.php`.

1. Adicionar este arquivo à `app/etc` pasta do seu projeto.

1. Adicione e confirme o arquivo na ramificação.

1. Envie o arquivo para a ramificação de integração.

1. Continue com o processo de atualização.

>[!WARNING]
>
>Depois da atualização, você poderá remover o `config.php` e gere um novo arquivo completo. Você só pode excluir este arquivo para substituí-lo desta vez. Depois de gerar um novo, conclua `config.php` não é possível excluir o arquivo para gerar um novo. Consulte [Gerenciamento de configuração e implantação de pipeline](../store/store-settings.md).

### Verificar dependências do Zend Framework Composer

Ao atualizar para o **2.3.x ou posterior a partir de 2.2.x**, verifique se as dependências do Zend Framework foram adicionadas ao `autoload` propriedade do `composer.json` para apoiar o processo Laminas. Este plug-in suporta novos requisitos para o Zend Framework, que migrou para o projeto Laminas. Consulte [Migração do Zend Framework para o Projeto Laminas](https://community.magento.com/t5/Magento-DevBlog/Migration-of-Zend-Framework-to-the-Laminas-Project/ba-p/443251) no _DevBlog Magento_.

**Para verificar a `auto-load:psr-4` configuração**:

1. Na estação de trabalho local, altere para o diretório do projeto.

1. Confira a ramificação de integração.

1. Abra o `composer.json` em um editor de texto.

1. Verifique a `autoload:psr-4` seção para a implementação do gerenciador de plug-ins Zend para dependência de controladores.

   ```json
    "autoload": {
       "psr-4": {
          "Magento\\Framework\\": "lib/internal/Magento/Framework/",
          "Magento\\Setup\\": "setup/src/Magento/Setup/",
          "Magento\\": "app/code/Magento/",
          "Zend\\Mvc\\Controller\\": "setup/src/Zend/Mvc/Controller/"
       },
   }
   ```

1. Se a dependência Zend estiver ausente, atualize o `composer.json` arquivo:

   - Adicione a seguinte linha à `autoload:psr-4` seção.

     ```json
     "Zend\\Mvc\\Controller\\": "setup/src/Zend/Mvc/Controller/"
     ```

   - Atualize as dependências do projeto.

     ```bash
     composer update
     ```

   - Adicionar, confirmar e enviar alterações de código.

     ```bash
     git add -A
     ```

     ```bash
     git commit -m "Add Zend plugin manager implementation for controllers dependency for Laminas support"
     ```

     ```bash
     git push origin <branch-name>
     ```

   - Mescle as alterações no ambiente de preparo e, em seguida, na produção.

## Arquivos de configuração

Antes de atualizar o aplicativo, você deve atualizar os arquivos de configuração do projeto para levar em conta as alterações nas configurações padrão do Adobe Commerce na infraestrutura em nuvem ou no aplicativo. Os padrões mais recentes podem ser encontrados na [repositório GitHub da magento-cloud](https://github.com/magento/magento-cloud).

### .magento.app.yaml

Sempre revise os valores contidos na variável [.magento.app.yaml](../application/configure-app-yaml.md) arquivo para a versão instalada, pois controla a maneira como o aplicativo é criado e implantado na infraestrutura em nuvem. O exemplo a seguir é para a versão 2.4.7 e usa o Composer 2.7.2. A variável `build: flavor:` não é usada para o Composer 2.x; consulte [Instalação e uso do Composer 2](../application/properties.md#installing-and-using-composer-2).

**Para atualizar o `.magento.app.yaml` arquivo**:

1. Na estação de trabalho local, altere para o diretório do projeto.

1. Abra e edite o `magento.app.yaml` arquivo.

1. Atualize as opções do PHP.

   ```yaml
   type: php:8.3
   
   build:
       flavor: none
   dependencies:
       php:
           composer/composer: '2.7.2'
   ```

1. Modifique o `hooks` propriedade `build` e `deploy` comandos.

   ```yaml
   hooks:
       # We run build hooks before your application has been packaged.
       build: |
           set -e
           composer install
           php ./vendor/bin/ece-tools run scenario/build/generate.xml
           php ./vendor/bin/ece-tools run scenario/build/transfer.xml
       # We run deploy hook after your application has been deployed and started.
       deploy: |
           php ./vendor/bin/ece-tools run scenario/deploy.xml
       # We run post deploy hook to clean and warm the cache. Available with ECE-Tools 2002.0.10.
       post_deploy: |
           php ./vendor/bin/ece-tools run scenario/post-deploy.xml
   ```

1. Adicione as variáveis de ambiente a seguir ao final do arquivo.

   Para o Adobe Commerce 2.2.x a 2.3.x-

   ```yaml
   variables:
       env:
           CONFIG__DEFAULT__PAYPAL_ONBOARDING__MIDDLEMAN_DOMAIN: 'payment-broker.magento.com'
           CONFIG__STORES__DEFAULT__PAYMENT__BRAINTREE__CHANNEL: 'Magento_Enterprise_Cloud_BT'
           CONFIG__STORES__DEFAULT__PAYPAL__NOTATION_CODE: 'Magento_Enterprise_Cloud'
   ```

   Para o Adobe Commerce 2.4.x-

   ```yaml
   variables:
       env:
           CONFIG__DEFAULT__PAYPAL_ONBOARDING__MIDDLEMAN_DOMAIN: 'payment-broker.magento.com'
           CONFIG__STORES__DEFAULT__PAYPAL__NOTATION_CODE: 'Magento_Enterprise_Cloud'
   ```

1. Salve o arquivo. Não confirme ou envie alterações para o ambiente remoto ainda.

1. Continue com o processo de atualização.

### composer.json

Antes da atualização, sempre verifique se as dependências no `composer.json` são compatíveis com a versão do Adobe Commerce.

**Para atualizar o `composer.json` arquivo do Adobe Commerce versão 2.4.4 e posterior**:

1. Adicione o seguinte `allow-plugins` para o `config` seção:

   ```json
   "config": {
      "allow-plugins": {
         "dealerdirect/phpcodesniffer-composer-installer": true,
         "laminas/laminas-dependency-plugin": true,
         "magento/*": true
      }
   },
   ```

1. Adicione o seguinte plug-in à `require` seção:

   ```json
   "require": {
       "magento/composer-root-update-plugin": "^2.0.3"
   },
   ```

1. Adicione o seguinte componente à `extra:component_paths` seção:

   ```json
   "extra": {
      "component_paths": {
         "tinymce/tinymce": "lib/web/tiny_mce_5"
      },
   },
   ```

1. Salve o arquivo. Não confirme ou envie alterações para sua ramificação ainda.

1. Continue com o processo de atualização.

## Backup do projeto

Recomendamos criar um backup do seu projeto antes de uma atualização. Use as etapas a seguir para fazer backup dos ambientes de integração, de preparo e de produção.

**Para fazer backup do banco de dados e do código do ambiente de integração**:

1. Crie um backup local do banco de dados remoto.

   ```bash
   magento-cloud db:dump
   ```

   >[!NOTE]
   >
   >A variável `magento-cloud db:dump` executa o [mysqldump](https://dev.mysql.com/doc/refman/8.0/en/mysqldump.html) com o comando `--single-transaction` sinalizador, que permite fazer backup do banco de dados sem bloquear as tabelas.

1. Faça backup do código e da mídia.

   ```bash
   php bin/magento setup:backup --code [--media]
   ```

   Opcionalmente, é possível omitir `[--media]` se você tiver um grande número de arquivos estáticos que já estão no controle de origem.

**Para fazer backup do banco de dados do ambiente de preparo ou produção antes da implantação**:

1. Use o SSH para fazer logon no ambiente remoto.

1. Criar um [dump do banco de dados](../storage/database-dump.md). Para escolher um diretório de destino para o dump de memória, use o `--dump-directory` opção.

   ```bash
   vendor/bin/ece-tools db-dump
   ```

   A operação de despejo cria uma `dump-<timestamp>.sql.gz` arquive o arquivo no diretório remoto do projeto. Consulte [Fazer backup do banco de dados](../storage/database-dump.md).

## Atualização de aplicativo

Revise o [versões do serviço](../services/services-yaml.md#service-versions) informações sobre os requisitos mais recentes de versão de software antes de atualizar seu aplicativo.

**Para atualizar a versão do aplicativo**:

1. Na estação de trabalho local, altere para o diretório do projeto.

1. Defina a versão de atualização usando o [sintaxe de restrição de versão](overview.md#cloud-metapackage).

   ```bash
   composer require "magento/magento-cloud-metapackage":">=CURRENT_VERSION <NEXT_VERSION" --no-update
   ```

   >[!NOTE]
   >
   >Você deve usar a sintaxe de restrição de versão para atualizar com êxito o `ece-tools` pacote. É possível encontrar a restrição de versão no `composer.json` arquivo para a versão do [modelo de aplicativo](https://github.com/magento/magento-cloud/blob/master/composer.json) que você está usando para a atualização.

1. Atualize o projeto.

   ```bash
   composer update
   ```

1. Adicionar, confirmar e enviar alterações de código.

   ```bash
   git add -A
   ```

   ```bash
   git commit -m "Upgrade"
   ```

   ```bash
   git push origin <branch-name>
   ```

   `git add -A` O é necessário para adicionar todos os arquivos alterados ao controle do código-fonte devido à forma como o Composer realiza marshaling nos pacotes base. Ambos `composer install` e `composer update` empacotar arquivos do pacote base (`magento/magento2-base` e `magento/magento2-ee-base`) na raiz do pacote.

   Os arquivos que o Composer empacota pertencem à nova versão do Adobe Commerce, para substituir a versão desatualizada desses mesmos arquivos. Atualmente, o empacotamento está desativado no Adobe Commerce, portanto, você deve adicionar os arquivos empacotados ao controle do código-fonte.

1. Aguarde a conclusão da implantação.

1. Verifique a atualização em seu ambiente de integração, preparo ou produção usando SSH para fazer logon e verificar a versão.

   ```bash
   php bin/magento --version
   ```

### Criar um arquivo config.php

Tal como mencionado no [Gerenciamento de configuração](#configuration-management), após a atualização, você deverá criar um arquivo atualizado `config.php` arquivo. Conclua todas as alterações adicionais de configuração por meio do Administrador no ambiente de integração.

**Para criar um arquivo de configuração específico do sistema**:

1. No terminal, use um comando SSH para gerar o `/app/etc/config.php` para o ambiente.

   ```bash
   ssh <SSH-URL> "<Command>"
   ```

   Por exemplo, para Pro, para executar o `scd-dump` no `integration` filial:

   ```bash
   ssh <project-id-integration>@ssh.us.magentosite.cloud "php vendor/bin/ece-tools config:dump"
   ```

1. Transfira o `config.php` para suas estações de trabalho locais usando `rsync` ou `scp`. Você só pode adicionar este arquivo à ramificação localmente.

   ```bash
   rsync <SSH-URL>:app/etc/config.php ./app/etc/config.php
   ```

1. Adicionar, confirmar e enviar alterações de código.

   ```bash
   git add app/etc/config.php && git commit -m "Add system-specific configuration" && git push origin master
   ```

   Isso gera uma atualização `/app/etc/config.php` arquivo com uma lista de módulos e definições de configuração.

>[!WARNING]
>
>Para uma atualização, você exclui o `config.php` arquivo. Depois que esse arquivo for adicionado ao código, você deverá **não** excluí-lo. Se precisar remover ou editar configurações, edite o arquivo manualmente.

### Atualizar extensões

Revise suas páginas de extensão e módulo de terceiros no Marketplace ou outros sites da empresa e verifique o suporte para o Adobe Commerce e o Adobe Commerce na infraestrutura em nuvem. Se for necessário atualizar extensões e módulos de terceiros, a Adobe recomenda trabalhar em uma nova ramificação de integração com as extensões desativadas.

**Para verificar e atualizar suas extensões**:

1. Crie uma ramificação na estação de trabalho local.

1. Desative as extensões conforme necessário.

1. Quando disponível, baixar atualizações de extensão.

1. Instale a atualização conforme documentado pela documentação de terceiros.

1. Ative e teste a extensão.

1. Adicione, confirme e envie as alterações de código para o remoto.

1. Encaminhar e testar no ambiente de integração.

1. Encaminhar para o ambiente de preparo para testar em um ambiente de pré-produção.

A Adobe recomenda que você atualize seu ambiente de produção _antes_ incluindo as extensões atualizadas no processo de inicialização do site.

>[!NOTE]
>
>Quando você atualiza a versão do seu aplicativo, o processo de atualização é atualizado para a versão mais recente do [Módulo CDN Fastly](../cdn/fastly.md#fastly-cdn-module-for-magento-2) automaticamente.

## Solução de problemas de atualização

Se a atualização falhar, você receberá uma mensagem de erro no navegador indicando que não é possível acessar sua loja ou o painel Administrador:

```terminal
There has been an error processing your request
Exception printing is disabled by default for security reasons.
  Error log record number: <error-number>
```

**Para resolver o erro**:

1. Na estação de trabalho local, altere para o diretório do projeto.

1. Use o SSH para fazer logon no ambiente remoto.

   ```bash
   magento-cloud ssh
   ```

1. Abra o `./app/var/report/<error number>` arquivo.

1. [Examinar os logs](../test/log-locations.md) e determine a origem do problema.

1. Adicionar, confirmar e enviar alterações de código.

   ```bash
   git add -A && git commit -m "Fixed deployment failure" && git push origin <branch-name>
   ```
