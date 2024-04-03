---
title: Fluxo de trabalho do projeto Pro
description: Saiba como usar os fluxos de trabalho de desenvolvimento e implantação do Pro.
feature: Cloud, Iaas, Paas
exl-id: 103e90d5-2ef2-4fef-845c-439344666b00
source-git-commit: 08f43a3b0a50cdb2a5e8a45bd2e2448bc6dbca2b
workflow-type: tm+mt
source-wordcount: '782'
ht-degree: 0%

---

# Fluxo de trabalho do projeto Pro

O projeto Pro inclui um único repositório Git com uma `master` e três ambientes principais:

1. **Produção** ambiente para iniciar e manter o site ativo
1. **Estágios** ambiente para testes com todos os serviços
1. **Integração** ambiente para desenvolvimento e teste

![Lista de ambientes profissionais](../../assets/pro-environments.png)

Esses ambientes são `read-only`, aceitando alterações de código implantado de ramificações enviadas pelo seu espaço de trabalho local. Consulte [Arquitetura Pro](pro-architecture.md) para obter uma visão geral completa dos ambientes Pro. Consulte [[!DNL Cloud Console]](../project/overview.md#cloud-console) para obter uma visão geral da lista de ambientes Pro na visualização projeto.

O gráfico a seguir demonstra o fluxo de trabalho de desenvolvimento e implantação do Pro, que usa uma abordagem simples de ramificação Git. Você [desenvolver](#development-workflow) código usando uma ramificação ativa com base na variável `integration` ambiente, _push_ e _puxando_ O código do muda de e para a ramificação remota Ativa. Você implanta o código verificado ao _mesclagem_ a ramificação remota para a ramificação base, que ativa uma ramificação [criar e implantar](#deployment-workflow) para esse ambiente.

![Visualização de alto nível do fluxo de trabalho de desenvolvimento da arquitetura Pro](../../assets/pro-dev-workflow.png)

## Fluxo de trabalho de desenvolvimento

O ambiente de integração fornece uma base única `integration` ramificação contendo seu Adobe Commerce no código de infraestrutura em nuvem. Você pode criar uma ramificação de ambiente ativa adicional. Isso permite até duas ramificações ativas implantadas nos contêineres do Platform as a service (PaaS). Não há limite para o número de ambientes inativos.

{{enhanced-integration-envs}}

Os ambientes de projeto oferecem suporte a um processo de integração flexível e contínuo. Comece clonando o `integration` ramificação para a pasta local do projeto. Crie uma ramificação ou várias ramificações, desenvolva novos recursos, configure alterações, adicione extensões e implante atualizações:

- **Buscar** alterações de `integration`

- **Ramificação** de `integration`

- **Desenvolver** em uma estação de trabalho local, incluindo [!DNL Composer] atualizações

- **Push** alterações no código remoto e validação

- **Mesclar** para `integration` e teste

Com uma ramificação de código desenvolvida e os arquivos de configuração correspondentes, as alterações de código estão prontas para serem mescladas ao `integration` para testes mais abrangentes. A variável `integration` O ambiente também é melhor para:

- **Integração de serviços de terceiros**— Nem todos os serviços estão disponíveis no ambiente PaaS.

- **Gerar arquivos de gerenciamento de configuração**—Algumas definições de configuração são _Somente leitura_ em um ambiente implantado.

- **Configuração da loja**—Você deve definir totalmente todas as configurações de armazenamento usando o ambiente de integração. Você pode encontrar o **URL do Administrador da Loja** no _integração_ exibição de ambiente no _[!DNL Cloud Console]_.

## Fluxo de trabalho de implantação

Sempre que você envia código de sua estação de trabalho local para o ambiente remoto ou mescla o código para uma ramificação de ambiente, os scripts de criação e implantação geram um novo código e provisionam os serviços configurados para o ambiente remoto.

Criar ações de script:

- O site no ambiente de destino continua a ser executado durante uma criação

- Verificar e executar o Adobe Commerce em patches e hotfixes de infraestrutura em nuvem

- Compilar código com um log de criação e implantação

- Verifique o Gerenciamento de Configuração, a implantação de conteúdo estático ocorre durante esta fase

- Criar ou usar uma slug de código inalterado para acelerar o processo

- Provisionar todos os serviços e aplicativos de back-end

Implantar ações de script:

- Colocar o site no ambiente de destino em um _Manutenção_ modo

- Implantar conteúdo estático se não for concluído durante a compilação

- Instalar ou atualizar o Adobe Commerce na infraestrutura em nuvem

- Configurar roteamento para tráfego

Após o processo de criação e implantação, sua loja volta a ficar online com as alterações e configurações de código mais recentes. Consulte [Processo de implantação](../deploy/process.md).

### Mesclar para integração

Combine todas as alterações de código verificadas mesclando a ramificação de desenvolvimento ativa na base `integration` filial. Você pode testar todas as alterações no `integration` antes de promover alterações no ambiente de preparo.

### Mesclar para preparo

O armazenamento temporário é um ambiente de pré-produção que fornece todos os serviços e configurações o mais próximo possível do ambiente de produção. Sempre enviar as alterações de código do `integration` para o `staging` para que você possa realizar testes completos com todos os serviços. Na primeira vez que usar o ambiente de preparo, você deverá configurar serviços, como [Fastly CDN](../cdn/fastly.md) e [New Relic](../monitor/new-relic-service.md). Configure gateways de pagamento, envio, notificações e outros serviços essenciais com sandbox ou credenciais de teste.

É melhor testar completamente cada serviço, verificar suas ferramentas de teste de desempenho e executar o teste de UAT como administrador e como cliente, até sentir que sua loja está pronta para o ambiente de produção. Consulte [Implante sua loja](../deploy/staging-production.md).

### Mesclar para produção

Após testes completos no ambiente de preparo, mescle-o ao ambiente de produção e teste completamente usando credenciais ativas. No momento em que você iniciar o site de produção, os clientes deverão ser capazes de concluir as compras e os administradores deverão ser capazes de gerenciar a loja em tempo real. Consulte os seguintes tópicos para obter uma apresentação detalhada e clara sobre como implantar sua loja e colocar em funcionamento:

- [Implante sua loja](../deploy/staging-production.md)
- [Lançamento do site](../launch/overview.md)

### Mesclar para Mestre Global

Sempre enviar uma cópia do código de produção para a Global `master` caso haja uma necessidade emergente de depurar o ambiente de produção sem interromper os serviços.

Fazer **não** criar uma ramificação a partir de Global `master`. Use o `integration` para criar ramificações novas e ativas para desenvolvimento e correções.
