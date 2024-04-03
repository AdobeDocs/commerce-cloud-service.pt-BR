---
title: "Faça logon no [!DNL Cloud Console]"
description: Saiba mais sobre o [!DNL Cloud Console] para Adobe Commerce na infraestrutura em nuvem.
recommendations: noDisplay, catalog
last-substantial-update: 2024-02-06T00:00:00Z
exl-id: c19a36b6-e5e8-461c-a82c-68b7bf121999
source-git-commit: abe9aa36b907be8bdfdf42e6f28f1e1eac68fecf
workflow-type: tm+mt
source-wordcount: '389'
ht-degree: 0%

---


# Efetue logon no [!DNL Cloud Console]

A variável [!DNL Cloud Console] O fornece métodos interativos para criar, gerenciar e implantar o código do Commerce. A variável [!DNL Cloud Console] O é uma experiência mais moderna e fácil de usar, além de estabelecer a base para aprimoramentos futuros na interface.

[Faça logon no [!DNL Cloud Console]](https://console.adobecommerce.com) para visualizar sua lista de projetos.

![Lista de projetos](../assets/ui-allprojects-list.png)

## Recursos

Os recursos novos ou aprimorados incluem:

- Visão geral clara das características do projeto e do ambiente
- Fluxo de atividades com histórico classificável
- Gerenciamento manual de backup e histórico para projetos iniciais
- Exibições de log aprimoradas
- Listas classificáveis
- Formulários simples e orientação para adicionar integrações
- Conformidade com as Diretrizes de acessibilidade de conteúdo da Web (WCAG)

![[!DNL Cloud Console]](../assets/CloudConsole.svg)

Os recursos novos ou aprimorados são os seguintes:

| Recurso | Melhorias |
| -------------- | ----------------------------------- |
| [Fluxo de atividade](../cloud-guide/project/activity-stream.md) | Interaja com uma lista classificável de ações em execução, pendentes ou históricas. Selecione uma atividade e visualize logs ou cancele um build em execução. |
| [Visões gerais de projeto e ambiente](../cloud-guide/project/overview.md#project-overview) | Abra o projeto e veja a visão geral dos detalhes do projeto e a lista de ambientes. A visão geral do ambiente fornece mais detalhes sobre o status do ambiente, o acesso ao aplicativo e as atividades recentes. |
| [Formulários de integração](../cloud-guide/integrations/overview.md) | Use formulários simples e orientações para adicionar integrações, como notificações de Bitbucket ou Slack. |
| [Lista de projetos](../cloud-guide/project/overview.md#cloud-console) | A variável _Todos os projetos_ exibir lista todos os projetos aos quais você tem permissão de acesso. Você pode clicar em **[!UICONTROL Show filters]** e filtre sua lista de projetos por tipo, região ou plano. |
| [Opções de visibilidade variável](../cloud-guide/environment/variable-levels.md) | Limitar a visibilidade de uma variável de nível de projeto ou de ambiente durante a compilação ou o tempo de execução. |

<!-- The following are features yet to be activated:
| **Apps and services topology** | The Apps & Services topology is visible on Project and Environment views. This interactive diagram allows you to select a service and view the relationship details, such as name, type, version, port, and more. Click **[!UICONTROL View details]** to access the overview and configuration panel for each service. | -->

## Perguntas sobre o console

**_Onde posso encontrar o recurso Snapshots_**?

Para [!DNL Starter] projetos, o recurso Snapshots agora é chamado de _Backups_. Você pode criar um backup manual de sua [!DNL Starter] do ambiente [!DNL Cloud Console] ou crie um instantâneo da CLI da nuvem. Você deve ter uma função de Administrador para o ambiente.

Selecione um ambiente na barra de navegação do projeto. O ambiente deve estar ativo. Selecione o **[!UICONTROL Backups]** guia. Atualmente, essa opção não está disponível para ambientes Pro.

**_Onde é a lista de rotas configuradas para o ambiente_**?

Você pode encontrar a lista de rotas configuradas no _Serviços_ para um ambiente.

Selecione um ambiente na barra de navegação do projeto. Selecione o **[!UICONTROL Services]** guia. A variável **Roteador** visão geral exibe as rotas configuradas. Atualmente, não é possível adicionar uma rota a partir do novo [!DNL Cloud Console].

## Menu Conta

No canto superior direito, encontra-se o menu da conta. Clique na seta para baixo do menu e selecione **[!UICONTROL My Profile]**. No _Meu perfil_ exibir, você pode controlar os detalhes do usuário e as configurações de exibição, gerenciar [autenticação de segurança](../cloud-guide/project/user-access.md#user-authentication-requirements), [Tokens de API](../cloud-guide/project/user-access.md#create-an-api-token), e [Chaves SSH](../cloud-guide/development/secure-connections.md).
