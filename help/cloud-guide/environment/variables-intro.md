---
title: Variáveis de ambiente
description: Consulte uma lista de variáveis de ambiente específicas do Adobe Commerce na infraestrutura em nuvem.
feature: Cloud, Build, Configuration, Deploy
exl-id: bfee2f69-93a6-4d26-bb9e-be8acc5673c3
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 0%

---

# Variáveis de ambiente

A infraestrutura do Adobe Commerce na nuvem permite atribuir variáveis de ambiente para substituir opções de configuração. A variável `ece-tools` O pacote define valores na variável `env.php` arquivo com base em valores de [Variáveis da nuvem](variables-cloud.md), variáveis definidas no [!DNL Cloud Console], e o `.magento.env.yaml` arquivo de configuração.

As variáveis de ambiente no `.magento.env.yaml` O arquivo personaliza o ambiente da nuvem, substituindo a configuração existente do Commerce. Se um valor padrão for `Not Set`, depois o `ece-tools` o pacote leva **NÃO** e utiliza o [!DNL Commerce] padrão ou o valor do `MAGENTO_CLOUD_RELATIONSHIPS` configuração. Se o valor padrão for definido, a variável `ece-tools` O pacote age para definir esse padrão.

Os tipos de variáveis de ambiente incluem:

- [ADMIN](variables-admin.md)—variables substitui as variáveis ADMIN do projeto
- [MAGENTO_CLOUD](variables-cloud.md)— variáveis específicas da infraestrutura em nuvem
- Variáveis usadas na variável `.magento.env.yaml` arquivo:
   - [Global](variables-global.md)—as variáveis afetam os estágios de criação, implantação e pós-implantação
   - [Build](variables-build.md)— variables controlam as ações de compilação
   - [Implantar](variables-deploy.md)—variables controlam ações de implantação
   - [Pós-implantação](variables-post-deploy.md)—variables controlam as ações após a implantação

As variáveis são _hierárquico_, o que significa que, se uma variável não for substituída, ela será herdada do ambiente principal.

Você pode definir [Variáveis de ADMINISTRAÇÃO](variables-admin.md) do [!DNL Cloud Console] ou usando a Adobe Commerce CLI. É possível gerenciar outras variáveis de ambiente no [`.magento.env.yaml`](configure-env-yaml.md) arquivo para gerenciar ações de criação e implantação em todos os seus ambientes, incluindo os de preparo e produção profissionais, sem exigir um tíquete de suporte.

>[!TIP]
>
>Os arquivos YAML diferenciam maiúsculas de minúsculas e não permitem tabulações. Tenha cuidado para usar recuo consistente em todo o `.magento.env.yaml` o arquivo ou sua configuração podem não funcionar conforme esperado. Os exemplos nesta documentação e no arquivo de amostra usam _dois espaços_ recuo. Use o [comando ece-tools validate](configure-env-yaml.md#validate-configuration-file) para verificar sua configuração.
