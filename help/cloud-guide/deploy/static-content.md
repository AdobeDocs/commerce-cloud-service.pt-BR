---
title: Implantação de conteúdo estático
description: Saiba mais sobre as estratégias para implantar conteúdo estático, como imagens, scripts e CSS, no Adobe Commerce em projetos de infraestrutura em nuvem.
feature: Cloud, Build, Deploy, SCD
exl-id: e128d0d5-1326-44e5-a822-009e11ba105f
source-git-commit: 1253d8357fd2554050d1775fefbc420a2097db5f
workflow-type: tm+mt
source-wordcount: '707'
ht-degree: 0%

---

# Estratégias de implantação de conteúdo estático

A implantação de conteúdo estático (SCD) tem um impacto significativo no processo de implantação da loja, que depende do volume de conteúdo a ser gerado (como imagens, scripts, CSS, vídeos, temas, localidades e páginas da Web) e quando gerar o conteúdo. Por exemplo, a estratégia padrão gera conteúdo estático durante o [fase de implantação](process.md#deploy-phase-deploy-phase) quando o site está no modo de manutenção; no entanto, essa estratégia de implantação leva tempo para gravar o conteúdo diretamente no montado `pub/static` diretório. Você tem várias opções ou estratégias para ajudar a melhorar o tempo de implantação, dependendo das suas necessidades.

## Otimizar conteúdo JavaScript e HTML

Você pode usar o agrupamento e a minificação para criar conteúdo JavaScript e HTML otimizado durante a implantação de conteúdo estático.

### Reduzir conteúdo

Você pode melhorar o tempo de carregamento do SCD durante o processo de implantação se ignorar a cópia dos arquivos de exibição estáticos no `var/view_preprocessed` diretório e gerar _minificado_ HTML quando solicitado. Você pode ativar isso definindo o parâmetro [SKIP_HTML_MINIFICATION](../environment/variables-global.md#skiphtmlminification) variável de ambiente global para `true` no `.magento.env.yaml` arquivo.

>[!NOTE]
>
>Começando com o `ece-tools` pacote versão 2002.0.13, o valor padrão para a variável SKIP_HTML_MINIFICATION é definido como `true`.

Você pode salvar **mais** tempo de implantação e espaço em disco, reduzindo o número de arquivos de tema desnecessários. Por exemplo, é possível implantar o `magento/backend` tema em inglês e um tema personalizado em outros idiomas. É possível definir essas configurações de tema com o [SCD_MATRIX](../environment/variables-deploy.md#scdmatrix) variável de ambiente.

## Escolha de uma estratégia de implantação

As estratégias de implantação diferem com base na escolha de gerar conteúdo estático durante o _build_ fase, a _implantar_ ou _por demanda_. Como visto no gráfico a seguir, gerar conteúdo estático durante a fase de implantação é a opção menos ideal. Mesmo com o HTML minificado, cada arquivo de conteúdo deve ser copiado para o arquivo montado `~/pub/static` diretório, o que pode demorar muito. Gerar conteúdo estático sob demanda parece ser a escolha ideal. No entanto, se o arquivo de conteúdo não existir no cache gerado no momento em que é solicitado, o que adiciona tempo de carregamento à experiência do usuário. Portanto, gerar conteúdo estático durante a fase de criação é o ideal.

![Comparação de carregamento de SCD](../../assets/scd-load-times.png)

### Configuração do SCD na compilação

Gerar conteúdo estático durante a fase de criação com HTML minified é a configuração ideal para [**tempo de inatividade zero** implantações](reduce-downtime.md), também conhecida como **estado ideal**. Em vez de copiar arquivos para uma unidade montada, ele cria um link simbólico do `./init/pub/static` diretório.

A geração de conteúdo estático requer acesso a temas e localidades. O Adobe Commerce armazena temas no sistema de arquivos, que é acessível durante a fase de criação; no entanto, o Adobe Commerce armazena localidades no banco de dados. O banco de dados é _não_ disponíveis durante a fase de criação. Para gerar o conteúdo estático durante a fase de criação, é necessário usar o `config:dump` no campo `ece-tools` pacote para mover localidades para o sistema de arquivos. Ele lê os locais e os salva no `app/etc/config.php` arquivo.

**Para configurar o projeto para gerar o SCD na compilação**:

1. Na estação de trabalho local, altere para o diretório do projeto.
1. Use o SSH para fazer logon no ambiente remoto.

   ```bash
   magento-cloud ssh
   ```

1. Mova as localidades para o sistema de arquivos e, em seguida, atualize o [`config.php` arquivo](../development/commerce-version.md#create-a-configphp-file).

1. A variável `.magento.env.yaml` o arquivo de configuração deve conter os seguintes valores:

   - [SKIP_HTML_MINIFICATION](../environment/variables-global.md#skip_html_minification) é `true`
   - [SKIP_SCD](../environment/variables-build.md#skip_scd) no estágio de criação é `false`
   - [SCD_STRATEGY](../environment/variables-build.md#scd_strategy) é `compact`

1. Verifique a configuração do [Gancho pós-implantação](../application/hooks-property.md) no `.magento.app.yaml` arquivo.

1. Verifique suas configurações executando o [Assistente inteligente para o estado ideal](smart-wizards.md).

   ```bash
   php ./vendor/bin/ece-tools wizard:ideal-state
   ```

### Definição do SCD sob demanda

A geração de SCD sob demanda é ideal para um fluxo de trabalho de desenvolvimento no ambiente de integração. Ele diminui o tempo de implantação para que você possa revisar rapidamente suas implementações e executar testes de integração. Ativar o [SCD_ON_DEMAND](../environment/variables-global.md#scdondemand) variável de ambiente na etapa global do `.magento.env.yaml` arquivo. A variável SCD_ON_DEMAND substitui todas as outras configurações relacionadas ao SCD e apaga o conteúdo existente do `~/pub/static` diretório.

Ao usar a estratégia de solicitação de SCD, é útil pré-carregar o cache com as páginas que você espera solicitar, como a página inicial. Adicione a lista de páginas esperadas no [PÁGINAS_AQUECIDAS](../environment/variables-post-deploy.md#warmuppages) variável de ambiente no estágio de pós-implantação do `.magento.env.yaml` arquivo.

>[!WARNING]
>
>Não use a estratégia SCD on-demand no ambiente de produção.

### Ignorando SCD

Às vezes, você pode optar por ignorar completamente a geração de conteúdo estático. Você pode definir a variável [SKIP_SCD](../environment/variables-build.md#skipscd) variável de ambiente no estágio global para ignorar outras configurações relacionadas ao SCD. Isso não afeta o conteúdo existente no `~/pub/static` diretório.
