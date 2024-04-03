---
title: Criar variáveis
description: Consulte a lista de variáveis de ambiente que controlam ações na fase de criação da infraestrutura do Adobe Commerce na nuvem.
feature: Cloud, Configuration, Build, SCD, Upgrade
recommendations: noDisplay, catalog
role: Developer
exl-id: 243aaa45-a5ef-4ed2-8800-3d0f07bf3740
source-git-commit: 7b9c6a4cd17069c25455195bd8f273664b8a29eb
workflow-type: tm+mt
source-wordcount: '920'
ht-degree: 0%

---

# Criar variáveis

As seguintes _build_ as variáveis controlam ações na fase de criação e podem herdar e substituir valores da variável [Variáveis globais](variables-global.md). Insira essas variáveis no `build` fase do `.magento.env.yaml` arquivo:

```yaml
stage:
  build:
    BUILD_VARIABLE_NAME: value
```

Para obter mais informações sobre como personalizar o processo de criação e implantação:

- [Configuração de implantação](configure-env-yaml.md)
- [Processo de implantação](../deploy/process.md)

As seguintes variáveis foram removidas na v2.2:

- `skip_di_clearing`
- `skip_di_compilation`

## `ERROR_REPORT_DIR_NESTING_LEVEL`

- **Padrão**—`1`
- **Versão**—Adobe Commerce 2.1.4 e posterior

Defina o nível de aninhamento de diretórios para salvar arquivos de relatório de erros, a fim de evitar o preenchimento do diretório de relatório com dezenas de milhares de arquivos, o que pode dificultar o gerenciamento e a revisão dos dados. O padrão dessa configuração é `1`. Normalmente, você não precisa alterar o valor padrão, a menos que tenha problemas ao gerenciar arquivos de relatório de erros no `<magento_root>/var/report/` diretório.

```yaml
stage:
  build:
    ERROR_REPORT_DIR_NESTING_LEVEL: 2
```

## `QUALITY_PATCHES`

- **Padrão**—_Não definido_
- **Versão**—Adobe Commerce 2.1.4 e posterior

Especifique uma lista de patches de qualidade do Adobe Commerce a serem aplicados durante a implantação.

```yaml
stage:
  build:
    QUALITY_PATCHES: [ ]
```

O exemplo a seguir especifica três patches a serem aplicados durante a implantação.

```yaml
stage:
  build:
    QUALITY_PATCHES:
      - MC-31387
      - MDVA-4567
      - MC-456345
```

Consulte [Aplicar patches](../development/apply-patches.md).

## `SCD_COMPRESSION_LEVEL`

- **Padrão**—`6`
- **Versão**—Adobe Commerce 2.1.4 e posterior

Especifica qual [gzip](https://www.gnu.org/software/gzip) nível de compactação (`0` para `9`) para usar ao compactar conteúdo estático; `0` desativa a compactação.

```yaml
stage:
  build:
    SCD_COMPRESSION_LEVEL: 4
```

## `SCD_COMPRESSION_TIMEOUT`

- **Padrão**—`600`
- **Versão**—Adobe Commerce 2.1.4 e posterior

Quando o tempo necessário para compactar os ativos estáticos excede o tempo limite de compactação, ele interrompe o processo de implantação. Defina o tempo máximo de execução, em segundos, para o comando static content compression.

```yaml
stage:
  build:
    SCD_COMPRESSION_TIMEOUT: 800
```

## `SCD_NO_PARENT`

- **Padrão**—`false`
- **Versão**—Adobe Commerce 2.4.2 e posterior

Defina como `true` para evitar a geração de conteúdo estático para temas principais durante a fase de criação.

Definir `SCD_NO_PARENT: false` durante a fase de criação, para que a geração de conteúdo estático para os temas principais não afete a implantação do site ou cause tempo de inatividade desnecessário. Consulte [Implantação de conteúdo estático](../deploy/static-content.md).

```yaml
stage:
  build:
    SCD_NO_PARENT: false
```

## `SCD_MATRIX`

- **Padrão**—_Não definido_
- **Versão**—Adobe Commerce 2.1.4 e posterior

Você pode configurar vários locais por tema. Essa personalização ajuda a acelerar o processo de criação, reduzindo o número de arquivos de tema desnecessários. Por exemplo, é possível criar a variável _magento/backend_ tema em inglês e um tema personalizado em outros idiomas.

O exemplo a seguir cria a variável `Magento/backend` tema com três localidades:

```yaml
stage:
  build:
    SCD_MATRIX:
      "Magento/backend":
        language:
          - en_US
          - fr_FR
          - af_ZA
```

O exemplo a seguir cria três temas com três localidades:

```yaml
stage:
  build:
    SCD_MATRIX:
      "Magento/backend":
        language:
          - en_US
          - fr_FR
          - af_ZA
      "Magento/blank":
        language:
          - en_US
          - fr_FR
          - af_ZA
      "Magento/luma":
        language:
          - en_US
          - fr_FR
          - af_ZA
```

Ou você pode optar por _não_ implantar um tema:

```yaml
stage:
  build:
    SCD_MATRIX:
      "Magento/backend": [ ]
```

## `SCD_MAX_EXECUTION_TIME`

- **Padrão**—_Não definido_
- **Versão**—Adobe Commerce 2.2.0 e posterior

Permite aumentar o tempo de execução máximo esperado para implantação de conteúdo estático.

Por padrão, o Adobe Commerce na infraestrutura em nuvem define a execução máxima esperada para 900 segundos, mas em alguns cenários pode ser necessário mais tempo para concluir a implantação de conteúdo estático para um projeto em nuvem.

```yaml
stage:
  build:
    SCD_MAX_EXECUTION_TIME: 3600
```

{{scd-timing-warning}}

## `SCD_STRATEGY`

- **Padrão**—`quick`
- **Versão**—Adobe Commerce 2.2.0 e posterior

Personalize o [estratégia de implantação](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/static-view/static-view-file-strategy.html) para conteúdo estático. Consulte [Implantar arquivos de exibição estáticos](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/static-view/static-view-file-deployment.html).

Usar estas opções _somente_ se você tiver mais de um local:

- `standard`—implanta todos os arquivos de visualização estáticos para todos os pacotes.
- `quick`—(_padrão_) minimiza o tempo de implantação.
- `compact`—preserva o espaço em disco no servidor. No Adobe Commerce versão 2.2.4 e anterior, essa configuração substitui o valor de `scd_threads` com um valor de `1`.

```yaml
stage:
  build:
    SCD_STRATEGY: "compact"
```

## `SCD_THREADS`

- **Padrão**— Automatic
- **Versão**—Adobe Commerce 2.1.4 e posterior

Define o número de threads para implantação de conteúdo estático. O valor padrão é definido com base na contagem de threads da CPU detectada e não excede um valor 4. Aumentar o número de threads acelera a implantação de conteúdo estático; diminuir o número de threads o torna mais lento. Você pode definir o valor da thread, por exemplo:

```yaml
stage:
  build:
    SCD_THREADS: 2
```

Para reduzir ainda mais o tempo de implantação, use [Gerenciamento de configurações](../store/store-settings.md) com o `scd-dump` para mover a implantação estática para a fase de criação.

## `SCD_USE_BALER`

- **Padrão**—_Não definido_
- **Versão**—Adobe Commerce 2.3.0 e posterior

[Baler](https://github.com/magento/baler) O verifica o código JavaScript gerado e cria um pacote JavaScript otimizado. Implantar o pacote otimizado em seu site pode reduzir o número de solicitações de rede ao carregar seu site e melhorar o tempo de carregamento da página.

Defina como `true` para executar o Baler após executar a implantação de conteúdo estático.

```yaml
stage:
  build:
    SCD_USE_BALER: true
```

>[!NOTE]
>
>Como Baler está na versão alfa, não é aconselhável usá-lo em ambientes de Produção.

## `SKIP_COMPOSER_DUMP_AUTOLOAD`

- **Padrão**— _Não definido_
- **Versão**—Adobe Commerce 2.1.4 e posterior

Defina como `true` para ignorar o `composer dump-autoload` durante a instalação do Cloud Docker. Essa variável só é relevante para contêineres do Cloud Docker com sistemas de arquivos graváveis. Nesses casos, ignorar o comando evita erros de outros comandos que tentam acessar o código do excluído `generated` diretório.

Quando o Adobe Commerce é executado `composer dump-autoload`, ele cria arquivos de carregamento automático com links para classes geradas na `generated` , que não é um problema em ambientes de produção com sistemas de arquivos somente leitura. No entanto, para instalações do Cloud Docker com sistemas de arquivos graváveis (criados apenas para teste e desenvolvimento usando o `./vendor/bin/ece-docker build:compose --with-test`), você pode executar o `bin/magento -n setup:upgrade` comando sem o `--keep-generated` que exclui a variável `generated` diretório. Se o diretório for excluído, a variável `composer dump-autoload` O comando falha porque o carregamento automático contém links para arquivos no diretório excluído.

```yaml
stage:
  build:
    SKIP_COMPOSER_DUMP_AUTOLOAD: true
```

## `SKIP_SCD`

- **Padrão**— _Não definido_
- **Versão**—Adobe Commerce 2.1.4 e posterior

Defina como `true` para ignorar a implantação de conteúdo estático durante a fase de criação.

Se você já implantar conteúdo estático durante a fase de criação com o [Gerenciamento de configurações](../store/store-settings.md), você pode ignorar a implantação de conteúdo estático para um teste de build rápido.

Na fase de criação, defina `SKIP_SCD: false` para que a criação de conteúdo estático ocorra durante a fase de criação, quando o processo não impactar a implantação do site ou causar tempo de inatividade desnecessário. Consulte [Implantação de conteúdo estático](../deploy/static-content.md).

```yaml
stage:
  build:
    SKIP_SCD: false
```

## `VERBOSE_COMMANDS`

- **Padrão**—_Não definido_
- **Versão**—Adobe Commerce 2.1.4 e posterior

Ative ou desative o [Symfony](https://symfony.com/doc/current/console/verbosity.html) depurar nível de detalhamento para `bin/magento` Comandos da CLI executados durante a fase de implantação.

>[!NOTE]
>
>Para usar VERBOSE_COMMANDS para controlar os detalhes na saída do comando para êxito e falha `bin/magento` Comandos CLI, você deve definir [MIN_LOGGING_LEVEL](variables-global.md#minlogginglevel) `debug`.

Escolha o nível de detalhes fornecido nos logs:

- `-v`= saída normal
- `-vv`= saída mais detalhada
- `-vvv` = saída detalhada ideal para depuração

```yaml
stage:
  build:
    VERBOSE_COMMANDS: "-vv"
```
