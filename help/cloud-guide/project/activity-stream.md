---
title: Fluxo de atividade
description: Saiba como ler o fluxo de atividades na [!DNL Cloud Console] ou a CLI da nuvem para Adobe Commerce na infraestrutura em nuvem.
last-substantial-update: 2024-02-06T00:00:00Z
exl-id: ffef5ab4-ef40-4073-adc8-a44c61c0d77b
source-git-commit: 85ff1283f773823ff2c6e6ab8f391fd5b4aa00e4
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 0%

---

# Fluxo de atividade

A visualização principal de cada ambiente exibe uma **Atividade** lista de eventos históricos semelhantes a um log do Git. A lista de Atividades é um fluxo dos eventos recentes para ambientes ativos. Veja a seguir uma lista dos tipos de atividades e seus ícones exibidos no fluxo de Atividades:

![Tipos de atividade](../../assets/activity-types.svg){width="500" align="center"}

## Exibir logs

Na lista Atividade, clique no ícone de status de uma atividade para exibir o log. Como alternativa, clique no link ![Mais](../../assets/icon-more.png){width="32"} (_mais_) para acessar mais opções de gerenciamento da atividade. A seguir, é mostrado um log curto que cria um backup. Você pode [usar a CLI da nuvem](#activity-stream-with-cloud-cli) para exibir o mesmo log.

![Exibição de log](../../assets/log-view.png)

## Gerenciar uma atividade

Algumas atividades estão em um _em execução_ ou _pendente_ status. Você pode agir em uma atividade em execução, como cancelar uma implantação em execução. As guias a seguir mostram dois métodos de cancelamento de uma atividade: [!DNL Cloud Console] ou a CLI da nuvem.

>[!BEGINTABS]

>[!TAB Console]

**Para cancelar uma atividade no[!DNL Cloud Console]**:

Você pode atuar em uma atividade em execução acessando o ![Mais](../../assets/icon-more.png){width="32"} (_mais_) e selecionando uma ação, como `Cancel` ou `View log`. Para este exemplo, selecione a variável **Cancelar** opção para interromper a atividade em execução.

Nem todas as atividades têm a opção de cancelamento. Por exemplo, a opção de cancelar a implantação do aplicativo aparece somente durante a _build_ fase. Depois que o aplicativo for movido para a _implantar_ não será mais possível cancelar a atividade. Consulte [Processo de implantação](../deploy/process.md) sobre as diferentes fases.

![Cancelar atividade](../../assets/activity-icons/cancel-activity.png){width="450" align="center"}

Se você tiver um terminal executando a atividade de implantação, cancelando no [!DNL Cloud Console] resulta no cancelamento no terminal:

![Atividade cancelada no terminal](../../assets/activity-icons/activity-cancelled.png){width="300"}

>[!TAB CLI]

**Para cancelar uma atividade na CLI da nuvem**:

1. Identifique as atividades em execução e selecione uma ID de atividade.

   ```bash
   magento-cloud activity:list --state=in_progress
   ```

1. Cancele a atividade usando a ID da atividade:

   ```bash
   magento-cloud activity:cancel wvl5wm7s5vkhy
   ```

>[!ENDTABS]

## Filtrar fluxo de atividade

A capacidade de filtrar a lista de atividades é útil quando você está procurando algo específico, como um backup ou um evento de mesclagem.

**Para filtrar a lista de atividades na variável[!DNL Cloud Console]**:

1. Selecione um ambiente e escolha a atividade **[!UICONTROL All]** exibir para incluir o histórico completo do evento.

1. Clique em ![Filtrar por](../../assets/icon-filterby.png){width="32"} e selecione o **[!UICONTROL Filter by]** opções:

   ![Filtrar atividades](../../assets/activity-filter.png)

1. Escolher a atividade **[!UICONTROL Recent]** exiba e redefina a lista.

## Exibir fluxo com a CLI da nuvem

A variável `magento-cloud` A CLI oferece a maioria das mesmas capacidades que a [!DNL Cloud Console]. A variável `activity` pode:

- `list` o fluxo de atividades para um ambiente
- `get` detalhes sobre uma atividade específica
- exibir o `log` para uma atividade específica
- `cancel` uma atividade

**Para exibir o fluxo de atividades com a CLI da nuvem**:

1. Listar as atividades do ambiente atual.

   ```bash
   magento-cloud activity:list
   ```

1. Cada atividade tem uma ID exclusiva. Selecione uma ID na lista anterior e visualize os detalhes dessa atividade.

   ```bash
   magento-cloud activity:get wvl5wm7s5vkhy
   ```

1. Exibir o log completo dessa atividade.

   ```bash
   magento-cloud activity:log wvl5wm7s5vkhy
   ```

   Exemplo de resposta:

   ```bash
   Activity ID: wvl5wm7s5vkhy
   Type: environment.backup
   Description: User created a backup of Master
   Created: 2023-09-08T14:03:33+00:00
   State: complete
   Log:
   Creating backup of master
   Created backup eg5pu63egt2dcojkljalzjdopa
   ```
