---
title: '[!DNL ECE-Tools] Pacote'
description: Saiba mais sobre o [!DNL ECE-Tools] e como ele ajuda a gerenciar e implantar o Adobe Commerce.
exl-id: 5583a685-29c5-4de5-8d2e-94cff5ff37ab
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 0%

---

# Pacote de ferramentas ECE

A variável [!DNL ECE-Tools] pacote é um conjunto de scripts e ferramentas projetados para gerenciar e implantar o [!DNL Commerce] aplicação. A variável `ece-tools` o pacote simplifica muitos processos, como o gerenciamento de trabalhos cron, a verificação da configuração do projeto e a aplicação de patches de Adobe e hot fixes. Você pode visualizar e contribuir com a [open-source [!DNL ECE-Tools] repositório de código no GitHub][ece-repo].

{{ece-tools-package}}

A variável `ece-tools` O pacote é compatível com o Adobe Commerce, a partir da versão 2.1.4, e contém scripts e comandos do Adobe Commerce na infraestrutura em nuvem projetados para ajudar a gerenciar seu código e criar e implantar automaticamente seus projetos.

A lista a seguir mostra os `ece-tools` comandos:

```bash
php ./vendor/bin/ece-tools list
```

## Criar e implantar

A variável `ece-tools` o pacote contém comandos para executar operações nos estágios de criação, implantação e pós-implantação da inicialização do Adobe Commerce no aplicativo de infraestrutura em nuvem. Por exemplo, a variável `php ./vendor/bin/ece-tools build` inicia o processo de criação do aplicativo.

Por padrão, essas `ece-tools` os comandos estão na [propriedade de ganchos](../application/hooks-property.md) do `.magento.app.yaml` arquivo de configuração.

## Gerador de configuração do Docker

A variável `ece-tools` o pacote inclui uma dependência para o [magento/magento-cloud-docker] que fornece arquivos de funcionalidade e configuração para imagens do Docker para iniciar um ambiente de desenvolvimento do Docker para Adobe Commerce na infraestrutura em nuvem. Você também pode executar o Cloud Docker for Commerce como um pacote independente. Consulte [Desenvolvimento de docker](../dev-tools/cloud-docker.md).

## Serviços, rotas e variáveis

Você pode usar o `ece-tools` pacote para exibir informações detalhadas sobre o codificado na Base64 [Variáveis da nuvem](../environment/variables-cloud.md) usado em qualquer ambiente de nuvem. O comando a seguir mostra todos os serviços, rotas e variáveis.

```bash
php ./vendor/bin/ece-tools env:config:show
```

Para exibir um conjunto específico de informações, use o seguinte formato:

```bash
php ./vendor/bin/ece-tools env:config:show <option>
```

- `services`—Exibe os dados de relacionamento do `MAGENTO_CLOUD_RELATIONSHIPS` variável de ambiente, definida na variável `services.yaml` arquivo.
- `routes`—Exibe as rotas configuradas para o projeto usando o `MAGENTO_CLOUD_ROUTES` variável de ambiente.
- `variables`—Exibe as variáveis configuradas para o projeto usando o `MAGENTO_CLOUD_VARIABLES` variável de ambiente.

Exemplo de saída para o `services` opção:

```terminal
Magento Cloud Services:
+-----------------------------------+----------------------------------+
| Service Configuration             | Value                            |
+-----------------------------------+----------------------------------+
| database:                                                            |
+-----------------------------------+----------------------------------+
| host                              | 127.0.0.1                        |
| password                          | <password>                       |
| port                              | 3306                             |
+-----------------------------------+----------------------------------+
| opensearch:                                                          |
+-----------------------------------+----------------------------------+
| host                              | 127.0.0.1                        |
| port                              | 9200                             |
...
```

## Verificar a configuração do ambiente

Há um conjunto de comandos de verificação disponíveis para ajudar a avaliar a configuração do seu projeto. Consulte [Assistentes inteligentes](../deploy/smart-wizards.md) no _Otimizar implantação_ para obter uma descrição detalhada de cada comando do assistente. A variável `wizard:ideal-state` é executado automaticamente durante a fase de criação. Para verificar o estado ideal do projeto:

```bash
php ./vendor/bin/ece-tools wizard:ideal-state
```

>[!NOTE]
>
>Você deve executar o `wizard:ideal-state` no ambiente de nuvem remoto. O comando sempre retorna a variável `The configured state is not ideal` erro ao ser executado no ambiente de desenvolvimento local.

Saída de exemplo:

```terminal
Ideal state is configured
```

Consulte [Notas de versão das ferramentas ece](../release-notes/cloud-tools-suite.md).

## Patches de Adobe e patches personalizados

A variável `ece-tools` o pacote inclui uma dependência para o [magento/magento-cloud-patches] que fornece patches de Adobe e hot fixes que melhoram a integração de todas as versões do Adobe Commerce com ambientes na nuvem e oferecem suporte à entrega rápida de correções críticas. O &quot;também fornece patches personalizados que você adiciona ao projeto de infraestrutura do Adobe Commerce na nuvem. Consulte [Aplicar patches](../development/apply-patches.md).

<!-- link definitions -->

[ece-repo]: https://github.com/magento/ece-tools
[magento/magento-cloud-docker]: https://github.com/magento/magento-cloud-docker
[magento/magento-cloud-patches]: https://github.com/magento/magento-cloud-patches
