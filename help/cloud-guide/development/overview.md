---
title: Visão geral do desenvolvimento
description: Prepare-se para o desenvolvimento local com um projeto do Adobe Commerce na infraestrutura em nuvem.
role: Developer
feature: Cloud, Install
topic: Development
last-substantial-update: 2024-02-06T00:00:00Z
exl-id: d4452d7d-d3dc-4f8d-8bd7-76f05d89f545
source-git-commit: 99272d08a11f850a79e8e24857b7072d1946f374
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 0%

---

# Visão geral do desenvolvimento

Os ambientes remotos do Adobe Commerce na infraestrutura em nuvem são **Somente leitura**, incluindo todos os ambientes iniciais e todos os ambientes de integração Pro, preparo e produção. Em um ambiente de desenvolvimento local, você pode gravar e testar o código antes de enviá-lo para um ambiente de integração para testes e implantação adicionais em preparo e produção.

Antes de preparar o espaço de trabalho local, verifique se você tem [credenciais](../../get-started/prepare-workspace.md). O desenvolvimento local requer a instalação do PHP e do Composer, a menos que você opte por usar [Cloud Docker for Commerce](#docker-environment).

## Pacotes obrigatórios

O Adobe Commerce na infraestrutura em nuvem usa o Composer para gerenciar as dependências e as atualizações de projetos. Para o desenvolvimento local, você deve instalar as versões do PHP e do Composer que sejam compatíveis com o seu projeto na nuvem. Por exemplo, se estiver usando a variável [!DNL Commerce] 2.4.7, você pode ver que a variável [`.magento.app.yaml`](https://github.com/magento/magento-cloud/blob/2.4.7/.magento.app.yaml) usos do arquivo de configuração **PHP 8.3** e **Composer 2.7.2**.

O Composer instala as bibliotecas e dependências necessárias para o seu projeto na `vendor` diretório. Os seguintes arquivos do Composer necessários estão no diretório raiz do projeto:

- `composer.json`—Use o `composer.json` arquivo para gerenciar instalações e atualizações de produtos.
- `composer.lock`—O `composer.lock` O arquivo armazena um conjunto de dependências de versão exatas que satisfazem as restrições de versão de cada requisito para cada pacote na árvore de dependência do projeto.

**Comandos comuns:**

| Comando | Descrição |
|--------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------|
| `composer update` | Atualizações para as versões mais recentes das dependências refletidas na variável `composer.json` arquivo. Isso atualiza o `composer.lock` arquivo. |
| `composer install` | Lê o `composer.lock` arquivo para baixar dependências. É uma prática recomendada manter uma cópia atualizada do `composer.lock` no repositório do projeto. |

{style="table-layout:auto"}

Depois de adicionar, confirmar e enviar o código atualizado, o processo de implantação executa automaticamente o `composer install` durante o [fase de criação](../deploy/process.md#build-phase-build-phase).

### Metappackage da nuvem

O Adobe Commerce na infraestrutura em nuvem usa um metapackage que requer `magento/product-enterprise-edition`. Para obter as atualizações mais recentes da versão mais recente do Commerce, use a seguinte sintaxe de restrição:

```text
>=current_version <next_version
```

Por exemplo, para usar a versão mais recente do Adobe Commerce 2.4.7, defina `2.4.7` como a versão &quot;atual&quot; e `2.4.8` como a versão &quot;próxima&quot; na `composer.json` arquivo:

```text
"magento/magento-cloud-metapackage": ">=2.4.7 <2.4.8"
```

Os principais pacotes desse metapackage são os seguintes:

- **fornecedor/magento/ece-tools**—O `ece-tools` O pacote é compatível com o Adobe Commerce versão 2.1.4 e posterior para fornecer um conjunto avançado de recursos que você pode usar para gerenciar seu projeto do Adobe Commerce na infraestrutura em nuvem. Ele contém scripts e comandos do Adobe Commerce na infraestrutura em nuvem projetados para ajudar a gerenciar seu código e criar e implantar automaticamente seus projetos. Consulte a [`ece-tools` visão geral do pacote](../dev-tools/package-overview.md).
- **vendor/magento/product-enterprise-edition**— Esse metappackage requer componentes de aplicativos, incluindo módulos, estruturas, temas e muito mais.
- **fornecedor/fastly2/magento2**— esse módulo gerencia a CDN do Fastly e os serviços para os ambientes Pro Staging e Production e Starter Production. Consulte [Serviços Fastly](/help/cloud-guide/cdn/fastly.md#fastly-cdn-module-for-magento-2).
- **fornecedor/magento/module-paypal-on-boarding**—Este módulo fornece checkout do gateway de pagamento do PayPal conectando-se à sua conta de comerciante do PayPal. Consulte [Ferramenta de integração PayPal](../store/paypal.md).

>[!TIP]
>
>Consulte [Pacotes na nuvem do Adobe Commerce](/help/cloud-guide/release-notes/cloud-packages.md) no _Notas de versão do Commerce_ para obter uma lista de dependências e licenças de terceiros.

## Ambiente do Docker

Você pode usar a ferramenta Cloud Docker for Commerce para emular o Adobe Commerce em ambientes de produção e desenvolvimento de infraestrutura em nuvem para desenvolvimento local. O Cloud Docker para Commerce não requer que o PHP e o Composer sejam instalados localmente.

- [Desenvolvimento local com o Cloud Docker](https://developer.adobe.com/commerce/cloud-tools/docker/setup/) no site do Adobe Developer
- [Arquitetura do Docker e comandos comuns](../dev-tools/cloud-docker.md)
- [Notas de versão do Cloud Docker](../release-notes/cloud-docker.md)

>[!TIP]
>
>Para obter informações sobre como usar os serviços de hospedagem baseados em Git com o Adobe Commerce na infraestrutura em nuvem, consulte [Integrações](../integrations/overview.md).
