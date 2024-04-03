---
title: Propriedade de ganchos
description: Consulte exemplos sobre como configurar a propriedade de ganchos na [!DNL Commerce] arquivo de configuração do aplicativo.
feature: Cloud, Configuration, Build, Deploy
exl-id: d9561f09-5129-4b72-978e-2e3873e8efae
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 0%

---

# Propriedade de ganchos

Use o `hooks` seção para executar comandos do shell durante as fases de criação, implantação e pós-implantação:

- **`build`**— Execute comandos _antes_ empacotando seu aplicativo. Serviços, como o banco de dados ou Redis, não estão disponíveis, pois o aplicativo ainda não foi implantado. Adicionar comandos personalizados _antes_ o padrão `php ./vendor/bin/ece-tools` para que o conteúdo gerado de forma personalizada continue até a fase de implantação.

- **`deploy`**— Execute comandos _após_ empacotando e implantando seu aplicativo. Você pode acessar outros serviços neste ponto. Como o padrão `php ./vendor/bin/ece-tools` copia a variável `app/etc` no local correto, você deve adicionar comandos personalizados _após_ o comando deploy para evitar a falha de comandos personalizados.

- **`post_deploy`**— Execute comandos _após_ implantação do aplicativo e _após_ o contêiner começa a aceitar conexões. A variável `post_deploy` O hook limpa o cache e pré-carrega (aquece) o cache. É possível personalizar a lista de páginas usando o `WARM_UP_PAGES` na variável [Estágio de pós-implantação](../environment/variables-post-deploy.md). Embora não seja obrigatório, isso funciona em conjunto com a `SCD_ON_DEMAND` variável de ambiente.

O exemplo a seguir mostra a configuração padrão na variável `.magento.app.yaml` arquivo. Adicione comandos da CLI em `build`, `deploy`ou `post_deploy` seções _antes_ o `ece-tools` comando:

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

Além disso, é possível personalizar ainda mais a fase de criação usando o `generate` e `transfer` comandos para executar ações adicionais ao criar ou mover arquivos especificamente.

```yaml
hooks:
    # We run build hooks before your application has been packaged.
    build: |
        set -e
        php ./vendor/bin/ece-tools build:generate
        # php /path/to/your/script
        php ./vendor/bin/ece-tools build:transfer
```

- `set -e`—faz com que os ganchos falhem no primeiro comando com falha, em vez do comando final com falha.
- `build:generate`—aplica patches, valida a configuração, gera ID e gera conteúdo estático se o SCD estiver habilitado para a fase de criação.
- `build:transfer`—transfere o código gerado e o conteúdo estático para o destino final.

Os comandos são executados no aplicativo (`/app`). Você pode usar o `cd` comando para alterar o diretório. Os ganchos falharão se o comando final neles falhar. Para causar falha no primeiro comando com falha, adicione `set -e` até ao início do gancho.

**Para compilar arquivos Sass usando grunt**:

```yaml
dependencies:
    ruby:
        sass: "3.4.7"
    nodejs:
        grunt-cli: "~0.1.13"

hooks:
    build: |
        cd public/profiles/project_name/themes/custom/theme_name
        npm install
        grunt
        cd
        php ./vendor/bin/ece-tools build
```

Compilar arquivos Sass usando `grunt` antes da implantação de conteúdo estático, o que acontece durante a build. Coloque o `grunt` antes do comando `build` comando.

{{scenarios}}
