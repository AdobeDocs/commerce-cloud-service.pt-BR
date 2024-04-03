---
title: Alterações incompatíveis com versões anteriores
description: Saiba mais sobre compatibilidade com versões anteriores ao atualizar projetos existentes na nuvem.
feature: Cloud, Release Notes
recommendations: noDisplay, catalog
exl-id: 9847c565-6d59-429a-9593-c2eba5cf2da4
source-git-commit: f9edcc85c14354a2eddacbc5219557e107a367cb
workflow-type: tm+mt
source-wordcount: '791'
ht-degree: 0%

---

# Alterações incompatíveis com versões anteriores

Alterações incompatíveis com versões anteriores podem exigir o ajuste da Configuração e dos processos da nuvem para projetos existentes da nuvem ao atualizar para a versão mais recente do `ece-tools` pacote ou outro Pacote de ferramentas da nuvem para pacotes do Commerce.

## Alterações em `ece-tools` pacote

Algumas funcionalidades incluídas anteriormente no `ece-tools` O pacote agora é fornecido em pacotes separados. Esses pacotes são dependências do composer para `ece-tools`, que são instalados e atualizados automaticamente quando você instala ou atualiza as ferramentas ece.

A nova arquitetura não deve afetar seus processos de instalação ou atualização. No entanto, talvez seja necessário alterar alguns processos e sintaxe de comando ao trabalhar com o Adobe Commerce em um projeto de infraestrutura em nuvem. Para obter detalhes, analise as seguintes informações de alterações incompatíveis com versões anteriores e a [Notas de versão do Cloud Tools Suite](cloud-tools-suite.md).

### Alterações de requisito de versão de serviço

Alteramos o requisito mínimo de versão do PHP de 7.0.x para 7.1.x para projetos na nuvem que usam `ece-tools` v2002.1.0 e posterior. Se sua configuração de ambiente especifica o PHP 7.0, atualize o [configuração do php](../application/php-settings.md) no `.magento.app.yaml` arquivo.

>[!WARNING]
>
>Por causa da necessidade de mudar a versão do PHP, `ece-tools` O 2002.1.0 é compatível apenas com projetos do Adobe Commerce em infraestrutura em nuvem que executam o Adobe Commerce 2.1.15 ou posterior. Se o projeto usar uma versão anterior, você deverá [atualização](../development/commerce-version.md) antes de atualizar para `ece-tools` 2002.1.0

### Alterações na configuração do ambiente

A tabela a seguir fornece informações sobre variáveis de ambiente e outros arquivos de configuração de ambiente que foram removidos ou descontinuados no `ece-tools` v2002.1.0.

| Item | Substituição |
| -------- | ----------- |
| `SCD_EXCLUDE_THEMES` variável | [`SCD_MATRIX`](../environment/variables-build.md#scd_matrix) |
| `STATIC_CONTENT_THREADS` variável | [`SCD_THREADS`](../environment/variables-build.md#scd_threads) |
| `DO_DEPLOY_STATIC_CONTENT` variável | [`SKIP_SCD`](../environment/variables-build.md#skip_scd) |
| `STATIC_CONTENT_SYMLINK` variável | Nenhum. Agora, a build sempre cria um link simbólico para o diretório de conteúdo estático `pub/static`. |
| `build_options.ini` arquivo | Use o [`.magento.env.yaml`](../application/configure-app-yaml.md) arquivo para configurar variáveis de ambiente para gerenciar ações de criação e implantação em todos os ambientes.<p>Se você criar um ambiente em nuvem que inclua a variável `build_options.ini` arquivo, a criação falha. |

### Alterações no comando da CLI

A tabela a seguir resume as alterações de comando da CLI no ECE-Tools v2002.1.0 que podem exigir a atualização de comandos ou scripts.

| Comando | Substituição |
|-------- | ----------- |
| `m2-ece-build` | `vendor/bin/ece-tools build` |
| `m2-ece-deploy` | `vendor/bin/ece-tools deploy` |
| `m2-ece-scd-dump` | `vendor/bin/ece-tools config:dump` |
| `vendor/bin/ece-tools patch` | `vendor/bin/ece-patches apply` |
| `vendor/bin/ece-tools docker:build` | `vendor/bin/ece-docker build:compose` |
| `vendor/bin/ece-tools docker:config:convert` | `vendor/bin/ece-docker  image:generate:php` |

Em versões anteriores do ECE-Tools, `m2-ece-build` e `m2-ece-deploy` comandos para configurar ganchos de implantação no `.magento.app.yaml` arquivo. Ao atualizar para v2002.1.0, verifique a `hooks` configuração no `.magento.app.yaml` arquivo para os comandos obsoletos, e substitua-os se necessário.

## Alterações nos patches de nuvem

- **Remover patches baixados**-O `magento/magento-cloud-patches` pacote agrupa todos os patches disponíveis no [downloads de software](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/prerequisites/commerce.html) e as aplica automaticamente ao implantar na nuvem. Para evitar conflitos de patch após a atualização para ECE-Tools 2002.1.0 ou posterior, remova todos os patches fornecidos pelo Adobe que você baixou e adicionou ao projeto manualmente.

- **Atualização do comando aplicar patches**-Movemos o comando para aplicar patches do `vendor/bin/ece-tools` diretório para o `vendor/bin/ece-patches` diretório. Se você usar este comando para aplicar patches manualmente, use o novo caminho.

  > Aplicar patches manualmente

  ```bash
  php ./vendor/bin/ece-patches apply
  ```

## Alterações no Cloud Docker

- **O requisito mínimo de versão do PHP é agora o PHP 7.1**-Se o seu host do Cloud Docker for Commerce estiver executando uma versão anterior, atualize para o PHP v7.1 ou posterior.

- **Alterações no comando do Cloud Docker for Commerce**-

   - **Atualização do Cloud Docker para comandos do Commerce para operações de compilação do Docker**- Movemos os comandos do Cloud Docker for Commerce do `vendor/bin/ece-tools` diretório para o `vendor/bin/ece-docker` diretório. Atualize seus scripts e comandos para usar o novo caminho.

     Depois de atualizar para `ece-tools` 2002.1.0, use o seguinte comando para visualizar os `ece-docker` comandos.

     ```bash
     php ./vendor/bin/ece-docker list
     ```

   - **Atualização dos comandos docker-compose da nuvem**-Renomeamos o caminho para o arquivo de comando de `./bin/docker` para `./bin/magento-docker`. Atualize seus scripts e comandos para usar o novo caminho.

   - **O contêiner Cron não é mais incluído na configuração padrão do Docker**-Agora, você deve adicionar o `--with-cron` opção para o `ece-docker build:compose` comando para incluir o contêiner Cron na configuração do ambiente Docker. Consulte [Gerenciar trabalhos cron](https://developer.adobe.com/commerce/cloud-tools/docker/configure/manage-cron-jobs/) no _Cloud Docker for Commerce_ guia.

     Os scripts que geravam contêineres anteriormente com trabalhos cron agora estão sem o contêiner cron.

   - **Uso de contêineres temporários**-Em versões anteriores, os contêineres criados por `bin/magento-docker` operações de comando não foram removidas, portanto, você pode usá-las para outras operações. Agora, a variável `magento-docker` Os comandos do removem todos os contêineres criados após a conclusão do comando.

     Se quiser manter um contêiner criado por uma operação docker-compose, use o `docker-compose run` em vez do comando `bin/magento-docker` comando.

   - **Execução de ganchos pós-implantação**-O `cloud-deploy` O comando não executa mais ganchos pós-implantação. Use o novo `cloud-post-deploy` comando para executar ganchos pós-implantação após a implantação. Atualize seus scripts para adicionar o comando para executar ganchos pós-implantação.

     ```shell
     bin/magento-docker ece-deploy
     bin/magento-docker ece-post-deploy
     ```

     Como alternativa, se você usar `docker-compose` diretamente, execute o `docker-compose run deploy cloud-post-deploy` após o comando deploy.

- **Atualizando o banco de dados**-O container Banco de dados agora é armazenado no `magento-db` volume Docker persistente. Ao atualizar o ambiente do Docker, o banco de dados não é mais excluído automaticamente. Se necessário, use um dos comandos a seguir para removê-lo manualmente.

   - Remova o `magento-db` contêiner:

     ```bash
     docker volume rm magento-db
     ```

   - Remova todos os volumes associados ao desligar os contêineres Docker:

     ```bash
     docker-compose down -v
     ```

- **Substituir configurações de sincronização de arquivos para arquivos mortos e de backup**-Os arquivos de arquivamento e backup com as seguintes extensões não são mais sincronizados ao usar docker-sync ou mutagen: SQL, GZ, ZIP e BZ2. Você pode substituir a sincronização de arquivos padrão desses tipos de arquivos renomeando o arquivo para que termine com uma extensão diferente. Por exemplo: `synchronize-me.zip-backup`
