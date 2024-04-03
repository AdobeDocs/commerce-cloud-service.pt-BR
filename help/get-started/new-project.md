---
title: Provisionamento do Commerce na nuvem
description: Saiba como preparar um Adobe Customer Technical Advisor para provisionar seu Adobe Commerce em um projeto de infraestrutura em nuvem.
recommendations: noDisplay, catalog
role: Admin
exl-id: cfb354b0-c255-4b6e-94aa-c5a6bf7230d6
source-git-commit: 89c57a486545d6165e0407f913f4fa4cf6c95abe
workflow-type: tm+mt
source-wordcount: '728'
ht-degree: 0%

---

# Pré-requisitos de provisionamento do Commerce na nuvem

Vamos começar e inicializar seu projeto do Commerce na infraestrutura em nuvem.

Antes de o Adobe provisionar seu Commerce em ambientes de projeto em nuvem, é recomendável considerar as estratégias a seguir e preparar respostas para sua primeira consulta com a equipe de conta do Adobe. Use as seguintes seções como lista de verificação para ajudá-lo a se preparar para a conversa com um consultor técnico do cliente para provisionar um projeto em nuvem:

## Definição de domínio

**Pergunta 1**: _Que domínio ou domínios você pretende usar para a inicialização do site?_

Prepare-se para integrar os serviços Fastly e nginx definindo seus domínios e subdomínios de nível superior para os ambientes Pro Staging e Production. Após a configuração inicial, só é possível adicionar domínios enviando um tíquete de suporte da Adobe Commerce. Portanto, recomenda-se que as informações de domínio estejam prontas.

Exemplos para domínios de produção e de preparo:

- `www.your-store.com`
- `your-store.com`
- `mcprod.your-store.com`
- `mcstaging.your-store.com`

Consulte [Configurar vários sites ou lojas](../cloud-guide/store/multiple-sites.md) no _Commerce na infraestrutura em nuvem_ guia para obter orientação adicional sobre vários domínios ou domínios únicos.

## Domínio de email transacional

**Pergunta 2**: _Qual(is) domínio(s) você pretende usar para emails transacionais?_

O Adobe Commerce na nuvem usa o serviço proxy SendGrid SMTP (Simple Mail Transfer Protocol), que fornece autenticação de email de saída e serviços de monitoramento de reputação. O SendGrid envia emails transacionais em seu nome, portanto, requer informações de domínio.

Exemplo do domínio SendGrid: `example@your-store.com`

Consulte [Serviço de e-mail SendGrid](../cloud-guide/project/sendgrid.md) no _Commerce na infraestrutura em nuvem_ guia para obter mais orientação sobre emails transacionais e configurações de domínio.

## Alocação de armazenamento

**Pergunta 3**: _Quanto do armazenamento contratado você planeja alocar para upload de arquivos e para banco de dados?_

O Adobe Commerce na infraestrutura em nuvem usa o armazenamento para a estrutura de arquivos, a indexação de pesquisa e o banco de dados. Você pode subdividir o armazenamento conforme necessário, começando com 10 GB para cada partição.

A quantidade de armazenamento que você contratou para seu projeto de nuvem representa o armazenamento total para cada ambiente. Por exemplo, se você comprou 50 GB de espaço de armazenamento, terá 50 GB de armazenamento para cada ambiente. Há 50 GB de armazenamento separado para produção, preparo e cada ambiente de integração, respectivamente.

Você pode aumentar seu armazenamento contratado a qualquer momento. Para ambientes de produção e preparo profissionais, você deve enviar um tíquete de suporte da Adobe Commerce para alterar a alocação de espaço em disco. Um aumento de tamanho dos ambientes de produção Pro e de preparo só pode ocorrer em determinados intervalos. Dependendo do uso atual do espaço em disco, a equipe de suporte pode recomendar o aumento da alocação de espaço em disco em um mínimo de 10 GB. Depois de alocado, o aumento do armazenamento para preparo e produção profissionais pode **não** ser revertido.

Consulte [Gerenciar espaço em disco](../cloud-guide/storage/manage-disk-space.md) no _Commerce na infraestrutura em nuvem_ guia.

## Região do Cloud Service

**Pergunta 4**: _Qual região do Cloud Service é mais conveniente para sua proximidade?_

Escolha a base Amazon Web Services (AWS) ou Microsoft Azure as your Infrastructure as a Service (IaaS) para seus projetos Adobe Commerce on cloud infrastructure Pro. Cada provedor de serviços opera em várias regiões e fornece várias zonas de disponibilidade. Selecione uma região conveniente para sua localização e reduza a possibilidade de latência e custos mais altos.

Consulte [um mapa das regiões de nuvem do Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-operations/implementation-playbook/infrastructure/cloud/regions.html) no _Manual de implementação_.

## Serviço de conexão

**Pergunta 5**: _Você precisa de um serviço PrivateLink? Em caso afirmativo, em que região está a conexão PrivateLink?_

A infraestrutura do Adobe Commerce na nuvem oferece suporte à integração com o serviço Link privado do AWS ou Link privado do Azure. Embora esse serviço seja opcional, o PrivateLink é usado para estabelecer comunicação segura e privada entre ambientes de infraestrutura em nuvem com serviços e aplicativos hospedados em sistemas externos.

É importante considerar sua estratégia do Cloud Service (AWS ou Azure) para que a instância do Adobe Commerce possa ser acessada na mesma região. Consulte [Serviço PrivateLink](../cloud-guide/development/privatelink-service.md) no _Commerce na infraestrutura em nuvem_ para obter mais esclarecimentos sobre a acessibilidade regional.

## Inicialização do site do Target

**Pergunta 6**: _Qual é a data de lançamento prevista?_

O lançamento de um site requer configuração iterativa e teste para garantir o sucesso do lançamento do site. Definir uma data limite ajuda você e sua equipe de conta do Adobe a se prepararem para as atividades finais e de pré-lançamento, que incluem uma chamada para coordenar as etapas finais.

Consulte a [Visão geral do site do Launch](../cloud-guide/launch/overview.md) no _Commerce na infraestrutura em nuvem_ Guia para analisar o processo completo e baixar uma cópia da lista de verificação do Launch.

>[!TIP]
>
> Dê uma olhada no portal na nuvem e acesse seu novo projeto.
>
>**Próxima etapa**: [Integração com o Commerce](onboarding.md)
