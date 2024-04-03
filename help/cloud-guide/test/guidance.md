---
title: Orientação de testes
description: Leia sobre os tipos de teste e as práticas recomendadas para iniciar o Adobe Commerce na infraestrutura em nuvem.
exl-id: 1d7897a2-af97-46ab-89c0-2ec54284190e
source-git-commit: aae285d85188bfadd73d5b4e1fea16afa5beb117
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 0%

---

# Orientação de testes

Depois de configurar e personalizar seu projeto do Adobe Commerce na infraestrutura em nuvem, é uma prática recomendada testar seu aplicativo completamente antes de iniciar o site da loja. O teste ajuda a gerenciar adequadamente as expectativas do tamanho do cluster e a dimensionar adequadamente para as necessidades futuras dos negócios.

## Teste funcional

Durante o desenvolvimento, é importante realizar testes funcionais completos no projeto de infraestrutura em nuvem do Adobe Commerce. Consulte a seguinte orientação para executar testes funcionais no ambiente do Docker:

- **Teste de aplicativo**—Use o [Quadro de ensaio funcional Magento (MFTF)](https://developer.adobe.com/commerce/cloud-tools/docker/test/application-testing/) para testes de aplicativos no ambiente do Cloud Docker.

- **Teste de código**—Use o [Estrutura de teste de coerção para PHP](https://developer.adobe.com/commerce/cloud-tools/docker/test/code-testing/) para validar o código que se destina a contribuir para repositórios de packages em nuvem.

## Práticas recomendadas antes do lançamento

Considere os seguintes tipos de teste como prática recomendada a ser executada antes do lançamento do site:

- **Teste de carga**—Realize um teste de carga para entender o comportamento do sistema sob a carga esperada. Por exemplo, teste um número simultâneo de usuários ativos no aplicativo, fazendo com que cada usuário execute um número específico de transações dentro da duração definida. Esse teste revela o tempo de resposta de transações importantes e essenciais aos negócios, como o comportamento do banco de dados ou do servidor de aplicativos. Um teste de carga pode ajudar a identificar gargalos.

- **Teste de esforço**— desafie os limites máximos de capacidade dentro do sistema para determinar se ele tem desempenho suficiente quando a carga atual está bem acima do máximo esperado.

- **Verificação de segurança**—Adobe fornece um serviço gratuito [Ferramenta de verificação de segurança](../launch/overview.md#set-up-the-security-scan-tool) para seus sites.

- **Ensaio de penetração**—É um ataque cibernético simulado autorizado em um sistema de computador projetado para avaliar a segurança do sistema. O teste de penetração ajuda a identificar deficiências ou vulnerabilidades, incluindo a possibilidade de as partes não autorizadas obterem acesso a dados e características do sistema.

>[!WARNING]
>
>Os clientes não têm permissão para realizar avaliações de segurança da infraestrutura da AWS ou dos próprios serviços da AWS. Se você descobrir um problema de segurança em qualquer um dos serviços da AWS observado na sua avaliação de segurança, [entre em contato com o AWS Security](mailto:aws-security@amazon.com) imediatamente. Consulte [Políticas do cliente da AWS para testes de penetração](https://aws.amazon.com/security/penetration-testing/).
