---
title: Arquitetura dimensionada
description: Saiba mais sobre a arquitetura de camada dividida e como ela é dimensionada para atender à demanda.
feature: Cloud, Auto Scaling, Iaas, Logs
exl-id: c54d8772-b6cc-41cc-b1ab-bef7d6f13bf2
source-git-commit: 8a0523f1714b6ea41887e99b5c31294cf5e5255e
workflow-type: tm+mt
source-wordcount: '816'
ht-degree: 0%

---

# Arquitetura dimensionada

A infraestrutura em nuvem é dimensionada de acordo com os requisitos de recursos para alcançar maior eficiência. O Adobe Commerce na infraestrutura em nuvem monitora seus aplicativos e pode ajustar a capacidade para manter um desempenho estável e previsível. A conversão para essa arquitetura ajuda a mitigar problemas, como latência ou grandes picos no tráfego.

>[!NOTE]
>
>A arquitetura dimensionada está disponível para o Adobe Commerce em contas de infraestrutura em nuvem com o cluster Pro 48 ou superior.

## Arquitetura de nível dividido

Historicamente, a arquitetura Pro consistia em três nós, cada um contendo uma pilha de tecnologia completa. Agora, há uma infraestrutura escalável que fornece uma arquitetura hierárquica com um mínimo de seis nós: três nós para o banco de dados principal e serviços e três nós para o servidor Web. Essa arquitetura de nível dividido oferece a capacidade de dimensionar camadas independentemente para obter um equilíbrio ideal de desempenho.

### Camada de serviço

Há três nós de serviço para armazenamento de dados, cache e serviços: **OpenSearch** ou **Elasticsearch**, **MariaDB**, **Redis** e muito mais. Quando a camada de serviço se aproxima da capacidade, a única maneira de dimensionar é aumentar o tamanho do servidor, como aumentar a energia e a memória da CPU. A capacidade é limitada ao tamanho do nó disponível. Como o cluster de banco de dados foi projetado para alta disponibilidade, você não pode dimensionar horizontalmente de forma confiável com as tecnologias usadas.

![Escalonamento da camada de serviço](../../assets/scaling-service.png)

Considere um exemplo de que o tipo de instância do nó de serviço é _m5.2xlarge_ com RAM de 32 Gb. Um serviço, como o banco de dados, usa uma quantidade considerável de memória (30 Gb). Dimensionar para o próximo tamanho de instância disponível _m5.4xlarge_ O fornece RAM de 64 Gbit, o que dobra a memória e acomoda as necessidades crescentes do banco de dados.

Você pode otimizar ainda mais o desempenho da camada de serviço, roteando o tráfego com base no tipo de nó. Por padrão, o nó do banco de dados é isolado do tráfego da Web. Como exemplo, você pode optar por veicular o tráfego da Web no nó do banco de dados.

### Camada da Web

Há três nós da Web para processar solicitações e tráfego da Web: **php-fpm** e **NGINX**. Além do dimensionamento vertical ao aumentar a potência e a memória, a camada da Web pode ser dimensionada horizontalmente ao adicionar servidores da Web a um cluster existente quando constrito no nível do PHP. Consulte [Dimensionamento automático](autoscaling.md) para saber como os nós da web são dimensionados automaticamente.

![Escalonamento no nível da Web](../../assets/scaling-web.png)

Isso complementa o dimensionamento vertical fornecido pela camada de serviço. À medida que o nível de serviço é dimensionado em tamanho e capacidade para acomodar um banco de dados e uso de serviço cada vez maiores, o nível da Web é dimensionado em tamanho, energia e instâncias para acomodar um aumento nas solicitações de processo e requisitos de tráfego mais altos.

Considere um exemplo de que o tipo de instância do nó da Web é _C5.2xlarge com oito CPUs e 16 Gb de RAM_. O número de solicitações ao site aumentou bastante. Você pode adicionar um nó C5.2xlarge para lidar com o aumento nos processos php-fpm ou pode alterar cada tipo de instância para _C5.4xlarge com 16 CPUs e 32 Gb de RAM_. A adição de um nó reduz o risco de capacidade insuficiente de sobretensão.

## Estrutura de projeto

No mínimo, os projetos Pro com arquitetura Scaled têm seis nós disponíveis.

- 3 nós da Web c5.2xlarge (8 CPUs, 16 Gbit RAM)

- 3 nós de serviço m5.2xlarge (8 CPUs, 32 Gb RAM)

Entretanto, cada projeto é exclusivo e requer o monitoramento do desempenho para analisar adequadamente o gerenciamento de recursos. Cada conta inclui a variável [serviço New Relic](../monitor/new-relic-service.md), que se conecta automaticamente aos dados de aplicativos e à análise de desempenho para fornecer monitoramento dinâmico do servidor. Especificamente, você pode usar o serviço New Relic para monitorar a utilização da CPU e da RAM para determinar quais nós exigem recursos adicionais. À medida que um recurso atinge a capacidade ou você nota uma degradação no desempenho com base na análise, é possível criar uma solicitação para dimensionar sua infraestrutura para atender à demanda.

### Acesso SSH

Determinados arquivos e logs, como o `/app/<project-id>/var/log` não são compartilhados entre nós. Cada nó tem um acesso SSH exclusivo. Você não pode usar o `magento-cloud` CLI para fazer logon nos nós da Web ou do serviço, mas você pode encontrar os endereços de nó na lista de Acesso SSH na [!DNL Cloud Console].

```bash
ssh <node>.<project-ID>-<environment>-<user-ID>@ssh.<region>.magento.com
```

- `node` 1 a 3 — Endereços para acessar os nós de serviço

- `node` 4 a _n_—Endereços para acessar os nós da Web

>[!TIP]
>
>Depois de fazer logon, é possível confirmar a ID do servidor e a função: nós de serviço usam a _unificado_ e os nós da Web usam a função _web_ função.

Exemplo de resposta ao fazer logon em uma **nó de serviço** inclui o _unificado_ função:

```terminal
 __  __                   _          ___ _             _
|  \/  |__ _ __ _ ___ _ _| |_ ___   / __| |___ _  _ __| |
| |\/| / _` / _` / -_) ' \  _/ _ \ | (__| / _ \ || / _` |
|_|  |_\__,_\__, \___|_||_\__\___/  \___|_\___/\_,_\__,_|
            |___/

 Welcome to Magento Cloud.

 This is server unique-server-id, role project-id:unified.

project-id@server-id:~$
```

Exemplo de resposta ao fazer logon em uma **nó da web** inclui o _web_ função:

```terminal
 __  __                   _          ___ _             _
|  \/  |__ _ __ _ ___ _ _| |_ ___   / __| |___ _  _ __| |
| |\/| / _` / _` / -_) ' \  _/ _ \ | (__| / _ \ || / _` |
|_|  |_\__,_\__, \___|_||_\__\___/  \___|_\___/\_,_\__,_|
            |___/

 Welcome to Magento Cloud.

 This is server unique-server-id, role project-id:web.

project-id@server-id:~$
```

### Locais de log

Os locais dos logs variam um pouco dependendo do nó. Por exemplo, um log de banco de dados, como o **Log de erros do MySQL**, está disponível em um nó de serviço (`/var/log/mysql/mysql-error.log`), mas não está disponível em um nó da Web.

Cada conta Pro inclui a variável [Serviço de logs do New Relic](../monitor/new-relic-service.md), que se conecta automaticamente aos dados de registro do aplicativo para fornecer gerenciamento dinâmico de registros. Os dados de log agregados de todos os nós são exibidos no aplicativo de Logs do New Relic para que você possa solucionar problemas de desempenho em nós específicos de um único painel.
