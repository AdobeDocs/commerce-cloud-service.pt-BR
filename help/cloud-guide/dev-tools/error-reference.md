---
title: Mensagens de erro do pacote ECE-Tools
description: Consulte uma lista de códigos de erro e mensagens que podem ocorrer durante os processos de criação, implantação e pós-implantação do Adobe Commerce na infraestrutura em nuvem.
recommendations: noDisplay
role: Developer
exl-id: d8cc8d49-32da-43cf-a105-aa56b5334000
source-git-commit: f8e35ecff4bcafda874a87642348e2d2bff5247b
workflow-type: tm+mt
source-wordcount: '2719'
ht-degree: 4%

---

# Mensagens de erro para ECE-Tools

Esta referência de mensagem de erro fornece informações para solucionar erros que podem ocorrer durante os processos de criação, implantação e pós-implantação do Adobe Commerce na infraestrutura em nuvem.

Todas as mensagens de erro críticas e de aviso que ocorrem durante a implantação são gravadas em ambos `var/log/cloud.log` e `/var/log/cloud.error.log` arquivos. O arquivo de log de erros da nuvem contém apenas erros da implantação mais recente. Um arquivo vazio indica uma implantação bem-sucedida sem erros.

No `cloud.error.log` cada entrada é formatada como uma sequência JSON para facilitar a análise:

```json
{"errorCode":1006,"stage":"build","step":"validate-config","suggestion":"No stores/website/locales found in config.php\n  To speed up the deploy process do the following:\n  1. Using SSH, log in to your Magento Cloud account\n  2. Run \"php ./vendor/bin/ece-tools config:dump\"\n  3. Using SCP, copy the app/etc/config.php file to your local repository\n  4. Add, commit, and push your changes to the app/etc/config.php file","title":"The configured state is not ideal","type":"warning"}
```

As mensagens de erro são categorizadas por um dos estágios de implantação: criação, implantação e pós-implantação. Cada seção fornece uma lista de erros associados com as seguintes informações para cada erro:

- **Código de erro**: o identificador atribuído pela Adobe Commerce para a mensagem de erro
- **Estágio**: indica se o erro ocorreu durante os estágios de compilação, implantação ou pós-implantação
- **Etapa**: indica a etapa do cenário de implantação que pode retornar o erro. Se a variável _Etapa_ estiver em branco, o erro será um erro geral que pode ser retornado por várias etapas ou durante operações de pré-processamento. Consulte [Implantação baseada em cenário](../deploy/scenario-based.md) para obter mais informações sobre as etapas de criação, implantação e pós-implantação.
- **Sugestão**: fornece orientação para solucionar problemas e resolver o erro
- **Título (Descrição do erro)**: uma descrição que resume a causa do erro
- **Tipo**: indica se o erro é crítico ou um aviso

<!-- Note: The error code tables in this file are auto-generated from source code. To request changes to error code descriptions or suggestions, submit a GitHub issue to the magento/ece-tools repository. -->

## Erros Críticos

Erros críticos indicam um problema com a configuração do projeto Adobe Commerce na infraestrutura em nuvem que causa falha na implantação, por exemplo, configuração incorreta, não compatível ou ausente para as configurações necessárias. Antes de implantar, é necessário atualizar a configuração para resolver esses erros.

### Fase de criação

| Código de erro | Etapa de criação | Descrição do erro (Título) | Ação sugerida |
| - | - | - | - |
| 2 |  | Não é possível gravar no `./app/etc/env.php` arquivo | O script de implantação não pode fazer as alterações necessárias no `/app/etc/env.php` arquivo. Verifique as permissões do sistema de arquivos. |
| 3 |  | A configuração não está definida no `schema.yaml` arquivo | A configuração não está definida no `./vendor/magento/ece-tools/config/schema.yaml` arquivo. Verifique se o nome da variável de configuração está correto e se está definido. |
| 4 |  | Falha ao analisar o `.magento.env.yaml` arquivo | A variável `./.magento.env.yaml` formato de arquivo inválido. Use um analisador YAML para verificar a sintaxe e corrigir erros. |
| 5 |  | Não foi possível ler o `.magento.env.yaml` arquivo | Não foi possível ler o `./.magento.env.yaml` arquivo. Verifique as permissões do arquivo. |
| 6 |  | Não foi possível ler o `.schema.yaml` arquivo | Não foi possível ler o `./vendor/magento/ece-tools/config/magento.env.yaml` arquivo. Verificar permissões de arquivo e reimplantar (`magento-cloud environment:redeploy`). |
| 7 | módulos de atualização | Não é possível gravar no `./app/etc/config.php` arquivo | O script de implantação não pode fazer as alterações necessárias no `/app/etc/config.php` arquivo. Verifique as permissões do sistema de arquivos. |
| 8 | validate-config | Não é possível ler o `composer.json` arquivo | Não foi possível ler o `./composer.json` arquivo. Verifique as permissões do arquivo. |
| 9 | validate-config | O Composer.json não tem a seção de carregamento automático necessária | Obrigatório `autoload` está faltando na seção `composer.json` arquivo. Compare a seção de carregamento automático com a `composer.json` no modelo em nuvem e adicione a configuração ausente. |
| 10 | validate-config | O arquivo `.magento.env.yaml` contém uma opção que não é declarada no esquema ou uma opção configurada com um valor ou estágio inválido | A variável `./.magento.env.yaml` o arquivo contém configuração inválida. Verifique o log de erros para obter informações detalhadas. |
| 11 | módulos de atualização | Falha no comando: `/bin/magento module:enable --all` | Tentar executar `composer update` localmente. Em seguida, confirme e envie por push a atualização `composer.lock` arquivo. Verifique também o `cloud.log` para obter mais informações. Para obter uma saída de comando mais detalhada, adicione a variável `VERBOSE_COMMANDS: '-vvv'` opção para o `.magento.env.yaml` arquivo. |
| 12 | apply-patches | Falha ao aplicar patch |  |
| 13 | set-report-dir-nested-level | Não é possível gravar no arquivo `/pub/errors/local.xml` |  |
| 14 | copy-sample-data | Falha ao copiar arquivos de dados de amostra |  |
| 15 | compile-id | Falha no comando: `/bin/magento setup:di:compile` | Verifique a `cloud.log` para obter mais informações. Adicionar `VERBOSE_COMMANDS: '-vvv'` em `.magento.env.yaml` para obter uma saída de comando mais detalhada. |
| 16 | dump-autoload | Falha no comando: `composer dump-autoload` | A variável `composer dump-autoload` falha no comando. Verifique a `cloud.log` para obter mais informações. |
| 17 | enfardador | O comando a ser executado `Baler` Falha no empacotamento do para JavaScript | Verifique a `SCD_USE_BALER` para verificar se o módulo Baler está configurado e ativado para empacotamento de JS. Se você não precisar do módulo Baler, defina `SCD_USE_BALER: false`. |
| 18 | compress-static-content | O utilitário necessário não foi encontrado (tempo limite, bash) |  |
| 19 | deploy-static-content | Comando `/bin/magento setup:static-content:deploy` falhou | Verifique a `cloud.log` para obter mais informações. Para obter uma saída de comando mais detalhada, adicione a variável `VERBOSE_COMMANDS: '-vvv'` opção para o `.magento.env.yaml` arquivo. |
| 20 | compress-static-content | Falha na compactação de conteúdo estático | Verifique a `cloud.log` para obter mais informações. |
| 21 | backup-data: conteúdo estático | Falha ao copiar o conteúdo estático para o `init` diretório | Verifique a `cloud.log` para obter mais informações. |
| 22 | backup-data: writable-dirs | Falha ao copiar alguns diretórios graváveis para o `init` diretório | Falha ao copiar diretórios graváveis para o `./init` pasta. Verifique as permissões do sistema de arquivos. |
| 23 |  | Não é possível criar um objeto do agente de log |  |
| 24 | backup-data: conteúdo estático | Falha ao limpar o `./init/pub/static/` diretório | Falha ao limpar `./init/pub/static` pasta. Verifique as permissões do sistema de arquivos. |
| 25 |  | Não é possível localizar o pacote do Composer | Se você instalou a versão do aplicativo do Adobe Commerce diretamente do repositório do GitHub, verifique se `DEPLOYED_MAGENTO_VERSION_FROM_GIT` A variável de ambiente está configurada. |
| 26 | validate-config | Remova a configuração do módulo de Braintree Magento que não é mais suportada no Adobe Commerce e no Magento Open Source 2.4 e versões posteriores. | O suporte para o módulo Braintree não está mais incluído no Commerce 2.4.0 e versões posteriores. Remova a variável CONFIG_STORES_DEFAULT_PAYMENT_BRAINTREE_CHANNEL da seção Variáveis de `.magento.app.yaml` arquivo. Para suporte ao pagamento de Braintree, use uma extensão oficial da Commerce Marketplace. |

### Implantar estágio

| Código de erro | Implantar etapa | Descrição do erro (Título) | Ação sugerida |
| - | - | - | - |
| 101 | pré-implantação: cache | Configuração de cache incorreta (porta ou host ausente) | A configuração de cache não tem os parâmetros obrigatórios `server` ou `port`. Verifique a `cloud.log` para obter mais informações. |
| 102 |  | Não é possível gravar no `./app/etc/env.php` arquivo | O script de implantação não pode fazer as alterações necessárias no `/app/etc/env.php` arquivo. Verifique as permissões do sistema de arquivos. |
| 103 |  | A configuração não está definida no `schema.yaml` arquivo | A configuração não está definida no `./vendor/magento/ece-tools/config/schema.yaml` arquivo. Verifique se o nome da variável de configuração está correto e se está definido. |
| 104 |  | Falha ao analisar o `.magento.env.yaml` arquivo | A configuração não está definida no `./vendor/magento/ece-tools/config/schema.yaml` arquivo. Verifique se o nome da variável de configuração está correto e se está definido. |
| 105 |  | Não foi possível ler o `.magento.env.yaml` arquivo | Não foi possível ler o `./.magento.env.yaml` arquivo. Verifique as permissões do arquivo. |
| 106 |  | Não foi possível ler o `.schema.yaml` arquivo |  |
| 107 | pré-implantação: clean-redis-cache | Falha ao limpar o cache Redis | Falha ao limpar o cache Redis. Verifique se a configuração do cache Redis está correta e se o serviço Redis está disponível. Consulte [Configurar serviço Redis](../services/redis.md). |
| 108 | pré-implantação: set-production-mode | Comando `/bin/magento maintenance:enable` falhou | Verifique a `cloud.log` para obter mais informações. Para obter uma saída de comando mais detalhada, adicione a variável `VERBOSE_COMMANDS: '-vvv'` opção para o `.magento.env.yaml` arquivo. |
| 109 | validate-config | Configuração de banco de dados incorreta | Verifique se `DATABASE_CONFIGURATION` está configurada corretamente. |
| 110 | validate-config | Configuração de sessão incorreta | Verifique se `SESSION_CONFIGURATION` está configurada corretamente. A configuração deve conter pelo menos o `save` parâmetro. |
| 111 | validate-config | Configuração de pesquisa incorreta | Verifique se `SEARCH_CONFIGURATION` está configurada corretamente. A configuração deve conter pelo menos o `engine` parâmetro. |
| 112 | validate-config | Configuração de recurso incorreta | Verifique se `RESOURCE_CONFIGURATION` está configurada corretamente. A configuração deve conter pelo menos `connection` parâmetro. |
| 113 | validate-config:elasticsuite-integridade | O ElasticSuite está instalado, mas o serviço Elasticsearch não está disponível | Verifique se `SEARCH_CONFIGURATION` a variável de ambiente está configurada corretamente e verifique se o serviço Elasticsearch está disponível. |
| 114 | validate-config:elasticsuite-integridade | O ElasticSuite está instalado, mas outro mecanismo de pesquisa é usado | O ElasticSuite está instalado, mas outro mecanismo de pesquisa está configurado. Atualize o `SEARCH_CONFIGURATION` variável de ambiente para habilitar o Elasticsearch e verificar a configuração do serviço de Elasticsearch no `services.yaml` arquivo. |
| 115 |  | Falha na execução da consulta ao banco de dados |  |
| 116 | instalação-atualização: configuração | Comando `/bin/magento setup:install` falhou | Verifique a `cloud.log` e `install_upgrade.log` para obter mais informações. Para obter uma saída de comando mais detalhada, adicione a variável `VERBOSE_COMMANDS: '-vvv'` opção para o `.magento.env.yaml` arquivo. |
| 117 | install-update: config-import | Comando `app:config:import` falhou | Verifique a `cloud.log` para obter mais informações. Para obter uma saída de comando mais detalhada, adicione a variável `VERBOSE_COMMANDS: '-vvv'` opção para o `.magento.env.yaml` arquivo. |
| 118 |  | O utilitário necessário não foi encontrado (tempo limite, bash) |  |
| 119 | install-update: deploy-static-content | Comando `/bin/magento setup:static-content:deploy` falhou | Verifique a `cloud.log` para obter mais informações. Para obter uma saída de comando mais detalhada, adicione a variável `VERBOSE_COMMANDS: '-vvv'` opção para o `.magento.env.yaml` arquivo. |
| 120 | compress-static-content | Falha na compactação de conteúdo estático | Verifique a `cloud.log` para obter mais informações. |
| 121 | deploy-static-content:generate | Não é possível atualizar a versão implantada | Não é possível atualizar o `./pub/static/deployed_version.txt` arquivo. Verifique as permissões do sistema de arquivos. |
| 122 | clean-static-content | Falha ao limpar arquivos de conteúdo estático |  |
| 123 | install-update: split-db | Comando `/bin/magento setup:db-schema:split` falhou | Verifique a `cloud.log` para obter mais informações. Para obter uma saída de comando mais detalhada, adicione a variável `VERBOSE_COMMANDS: '-vvv'` opção para o `.magento.env.yaml` arquivo. |
| 124 | clean-view-preprocessed | Falha ao limpar o `var/view_preprocessed` pasta | Não foi possível limpar o `./var/view_preprocessed` pasta. Verifique as permissões do sistema de arquivos. |
| 125 | install-update: reset-password | Falha ao atualizar o `/var/credentials_email.txt` arquivo | Falha ao atualizar o `/var/credentials_email.txt` arquivo. Verifique as permissões do sistema de arquivos. |
| 126 | install-update: update | Comando `/bin/magento setup:upgrade` falhou | Verifique a `cloud.log` e `install_upgrade.log` para obter mais informações. Para obter uma saída de comando mais detalhada, adicione a variável `VERBOSE_COMMANDS: '-vvv'` opção para o `.magento.env.yaml` arquivo. |
| 127 | clean-cache | Comando `/bin/magento cache:flush` falhou | Verifique a `cloud.log` para obter mais informações. Para obter uma saída de comando mais detalhada, adicione a variável `VERBOSE_COMMANDS: '-vvv'` opção para o `.magento.env.yaml` arquivo. |
| 128 | disable-maintenance-mode | Comando `/bin/magento maintenance:disable` falhou | Verifique a `cloud.log` para obter mais informações. Adicionar `VERBOSE_COMMANDS: '-vvv'` em `.magento.env.yaml` para obter uma saída de comando mais detalhada. |
| 129 | install-update: reset-password | Não é possível ler o modelo de redefinição de senha |  |
| 130 | install-update: cache_type | Falha no comando: `php ./bin/magento cache:enable` | Comando `php ./bin/magento cache:enable` é executado somente quando o Adobe Commerce foi instalado, mas `./app/etc/env.php` O arquivo estava ausente ou vazio no início da implantação. Verifique a `cloud.log` para obter mais informações. Adicionar `VERBOSE_COMMANDS: '-vvv'` em `.magento.env.yaml` para obter uma saída de comando mais detalhada. |
| 131 | install-update | A variável `crypt/key` o valor da chave não existe no `./app/etc/env.php` ou o `CRYPT_KEY` variável de ambiente de nuvem | Esse erro ocorre se a variável `./app/etc/env.php` arquivo não estiver presente quando a implantação do Adobe Commerce começar ou se `crypt/key` valor indefinido. Se você migrou o banco de dados de outro ambiente, recupere o valor da chave de criptografia desse ambiente. Em seguida, adicione o valor ao [CRYPT_KEY](../environment/variables-deploy.md#crypt_key) variável de ambiente de nuvem no seu ambiente atual. Consulte [Adicione a chave de criptografia Magento](../development/authentication-keys.md). Se você tiver removido acidentalmente o `./app/etc/env.php` , use o seguinte comando para restaurá-lo a partir dos arquivos de backup criados de uma implantação anterior: `./vendor/bin/ece-tools backup:restore` CLI.&quot; |
| 132 |  | Não é possível conectar-se ao serviço Elasticsearch | Verifique se há credenciais de Elasticsearch válidas e se o serviço está em execução |
| 137 |  | Não é possível conectar ao serviço OpenSearch | Verifique se há credenciais OpenSearch válidas e se o serviço está em execução |
| 133 | validate-config | Remova a configuração do módulo de Braintree Magento que não é mais suportada no Adobe Commerce ou Magento Open Source 2.4 e versões posteriores. | O suporte para o módulo de Braintree não está mais incluído no Adobe Commerce ou Magento Open Source 2.4.0 e posteriores. Remova a variável CONFIG_STORES_DEFAULT_PAYMENT_BRAINTREE_CHANNEL da seção Variáveis de `.magento.app.yaml` arquivo. Para suporte a Braintree, use uma extensão oficial de Pagamentos de Braintree do Commerce Marketplace. |
| 134 | validate-config | O Adobe Commerce e o Magento Open Source 2.4.0 exigem a instalação do serviço de Elasticsearch | Instalar serviço de Elasticsearch |
| 138 | validate-config | O Adobe Commerce e o Magento Open Source 2.4.4 exigem a instalação do serviço OpenSearch ou Elasticsearch | Instalar serviço OpenSearch |
| 135 | validate-config | O mecanismo de pesquisa deve ser definido como Elasticsearch para Adobe Commerce e Magento Open Source >= 2.4.0 | Verifique a variável SEARCH_CONFIGURATION para o `engine` opção. Se estiver configurado, remova a opção ou defina o valor como &quot;elasticsearch&quot;. |
| 136 | validate-config | O banco de dados dividido foi removido a partir do Adobe Commerce e do Magento Open Source 2.5.0. | Se você usar o banco de dados dividido, será necessário reverter ou migrar para um único banco de dados ou usar uma abordagem alternativa. |
| 139 | validate-config | Mecanismo de pesquisa incorreto | Esta versão do Adobe Commerce ou Magento Open Source não é compatível com OpenSearch. Você deve usar o versões 2.3.7-p3, 2.4.3-p2 ou superior |

### Estágio de pós-implantação

| Código de erro | Etapa pós-implantação | Descrição do erro (Título) | Ação sugerida |
| - | - | - | - |
| 201 | is-deploy-failed | Falha no estágio de implantação |  |
| 202 |  | A variável `./app/etc/env.php` o arquivo não é gravável | O script de implantação não pode fazer as alterações necessárias no `/app/etc/env.php` arquivo. Verifique as permissões do sistema de arquivos. |
| 203 |  | A configuração não está definida no `schema.yaml` arquivo | A configuração não está definida no `./vendor/magento/ece-tools/config/schema.yaml` arquivo. Verifique se o nome da variável de configuração está correto e se está definido. |
| 204 |  | Falha ao analisar o `.magento.env.yaml` arquivo | A variável `./.magento.env.yaml` formato de arquivo inválido. Use um analisador YAML para verificar a sintaxe e corrigir erros. |
| 205 |  | Não foi possível ler o `.magento.env.yaml` arquivo | Verifique as permissões do arquivo. |
| 206 |  | Não foi possível ler o `.schema.yaml` arquivo |  |
| 207 | aquecimento | Falha ao aquecer algumas páginas |  |
| 208 | tempo para o primeiro byte | Falha ao testar o tempo até o primeiro byte (TTFB) |  |
| 227 | clean-cache | Comando `/bin/magento cache:flush` falhou | Verifique a `cloud.log` para obter mais informações. Adicionar `VERBOSE_COMMANDS: '-vvv'` em `.magento.env.yaml` para obter uma saída de comando mais detalhada. |

### Geral

| Código de erro | Etapa geral | Descrição do erro (Título) | Ação sugerida |
| - | - | - | - |
| 243 |  | A configuração não está definida no `schema.yaml` arquivo | Verifique se o nome da variável de configuração está correto e se foi definido. |
| 244 |  | Falha ao analisar o `.magento.env.yaml` arquivo | A variável `./.magento.env.yaml` formato de arquivo inválido. Use um analisador YAML para verificar a sintaxe e corrigir erros. |
| 245 |  | Não foi possível ler o `.magento.env.yaml` arquivo | Não foi possível ler o `./.magento.env.yaml` arquivo. Verifique as permissões do arquivo. |
| 246 |  | Não foi possível ler o `.schema.yaml` arquivo |  |
| 247 |  | Não é possível gerar um módulo para eventos | Verifique a `cloud.log` para obter mais informações. |
| 248 |  | Não é possível habilitar um módulo para eventos | Verifique a `cloud.log` para obter mais informações. |

## Erros de Aviso

Erros de aviso indicam um problema com a configuração do projeto Commerce na infraestrutura em nuvem, como configurações incorretas, obsoletas, sem suporte ou ausentes para recursos opcionais que podem afetar o funcionamento do site. Embora um aviso não cause falha na implantação, você deve revisar as mensagens de aviso e atualizar a configuração para resolvê-las.

### Fase de criação

| Código de erro | Etapa de criação | Descrição do erro (Título) | Ação sugerida |
| - | - | - | - |
| 1001 | validate-config | O arquivo app/etc/config.php não existe |  |
| 1002 | validate-config | O .O arquivo /build_options.ini não é mais suportado |  |
| 1003 | validate-config | A seção de módulos está ausente no arquivo de configuração compartilhado |  |
| 1004 | validate-config | A configuração não é compatível com esta versão do Commerce |  |
| 1005 | validate-config | Opções de SCD ignoradas |  |
| 1006 | validate-config | O estado configurado não é ideal |  |
| 1007 | enfardador | O agrupamento Baler JS não pode ser usado |  |

### Implantar estágio

| Código de erro | Implantar etapa | Descrição do erro (Título) | Ação sugerida |
| - | - | - | - |
| 2001 | pré-implantação:cache | O cache está configurado para um serviço Redis que não está disponível. Configuração ignorada. |  |
| 2002 | validate-config | O estado configurado não é ideal |  |
| 2003 | validate-config | O valor de nível de aninhamento de diretório para o relatório de erros não foi configurado |  |
| 2004 | validate-config | Configuração inválida no .arquivo /pub/errors/local.xml. |  |
| 2005 | validate-config | Os dados do administrador são usados para criar um usuário administrador apenas durante a instalação inicial. Quaisquer alterações nos dados de Admin são ignoradas durante o processo de atualização. | Após a instalação inicial, é possível remover os dados do administrador da configuração. |
| 2006 | validate-config | O usuário administrador não foi criado, pois o email do administrador não foi definido | Após a instalação, é possível criar um usuário administrador manualmente: use o ssh para se conectar ao seu ambiente. Em seguida, execute o `bin/magento admin:user:create` comando. |
| 2007 | validate-config | Atualizar versão do php para a versão recomendada |  |
| 2008 | validate-config | O suporte a Solr foi descontinuado no Adobe Commerce e no Magento Open Source 2.1. |  |
| 2009 | validate-config | O Solr não é mais suportado pelo Adobe Commerce e Magento Open Source 2.2 ou posterior. |  |
| 2010 | validate-config | O serviço de Elasticsearch é instalado na camada de infraestrutura, mas não é usado como um mecanismo de pesquisa. | Considere remover o serviço de Elasticsearch da camada de infraestrutura para otimizar o uso de recursos. |
| 2011 | validate-config | A versão do serviço Elasticsearch na camada de infraestrutura não é compatível com a versão atual do módulo elasticsearch/elasticsearch, usado pelo aplicativo Adobe Commerce. |  |
| 2012 | validate-config | A configuração atual não é compatível com esta versão do Adobe Commerce |  |
| 2013 | validate-config | Opções de SCD ignoradas porque o processo de implantação não foi executado na fase de compilação |  |
| 2014 | validate-config | A configuração contém variáveis ou valores obsoletos |  |
| 2015 | validate-config | A configuração do ambiente não é válida |  |
| 2016 | validate-config | A configuração do tipo JSON não pode ser decodificada |  |
| 2017 | validate-config | A configuração atual não é compatível com esta versão do Adobe Commerce |  |
| 2018 | validate-config | Alguns serviços passaram no fim da vida útil |  |
| 2019 | validate-config | A opção de configuração de pesquisa MySQL está obsoleta | Em vez disso, use Elasticsearch. |
| 2029 | validate-config | O banco de dados dividido foi descontinuado no Adobe Commerce e no Magento Open Source 2.4.2 e será removido na versão 2.5. | Se você usar o banco de dados dividido que você deve começar a planejar para reverter ou migrar para um único banco de dados ou usar uma abordagem alternativa. |
| 2020 | install-update | A instalação do Adobe Commerce foi concluída, mas a variável `app/etc/env.php` arquivo de configuração ausente ou vazio. | Os dados necessários são restaurados das configurações do ambiente e do arquivo .magento.env.yaml. |
| 2021 | install-update:db-connection | Para bancos de dados divididos, use conexões personalizadas |  |
| 2022 | install-update:db-connection | Você alterou para uma configuração de banco de dados incompatível com a conexão subordinada. |  |
| 2023 | install-update:split-db | A habilitação de um banco de dados dividido será ignorada. |  |
| 2024 | install-update:split-db | A variável SPLIT_DB não tem a configuração para tipos de conexão divididos. |  |
| 2025 | install-update:split-db | Conexão subordinada não definida. |  |
| 2026 | pré-implantação:restaurar-gravável-dirs | Falha ao restaurar alguns dados gerados durante a fase de compilação para os diretórios montados | Verifique a `cloud.log` para obter mais informações. |
| 2027 | validate-config:image-mode-variable | O valor de modo da variável de ambiente MAGE_MODE não é suportado | Remova a variável de ambiente MAGE_MODE ou altere seu valor para &quot;produção&quot;. O Adobe Commerce na infraestrutura em nuvem é compatível somente com o modo de &quot;produção&quot;. |
| 2028 | armazenamento remoto | Não foi possível habilitar o armazenamento remoto. | Verifique as credenciais do armazenamento remoto. |
| 2030 | validate-config | Os serviços Elasticsearch e OpenSearch são instalados na camada de infraestrutura. O Adobe Commerce e o Magento Open Source 2.4.4 e superior usam OpenSearch por padrão | Considere remover o serviço Elasticsearch ou OpenSearch da camada de infraestrutura para otimizar o uso de recursos. |

### Estágio de pós-implantação

| Código de erro | Etapa pós-implantação | Descrição do erro (Título) | Ação sugerida |
| - | - | - | - |
| 3001 | validate-config | O log de depuração está ativado no Adobe Commerce | Para economizar espaço em disco, não ative o log de depuração para seus ambientes de produção. |
| 3002 | aquecimento | Não é possível buscar URLs de armazenamento |  |
| 3003 | aquecimento | Não é possível buscar o url da loja |  |
| 3004 | backup | Não é possível criar arquivos de backup |  |

### Geral

| Código de erro | Etapa geral | Descrição do erro (Título) | Ação sugerida |
| - | - | - | - |
| 4001 |  | Não é possível obter a contagem de processadores do sistema: |  |
