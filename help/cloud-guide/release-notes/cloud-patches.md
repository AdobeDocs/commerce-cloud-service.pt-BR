---
title: Patches da nuvem para o Commerce
description: Consulte uma lista das melhorias mais recentes no pacote de Patches na nuvem.
recommendations: noDisplay, catalog
last-substantial-update: 2024-01-16T00:00:00Z
exl-id: ae6b511b-a37d-4776-9a5e-ad7d9f9f6611
source-git-commit: 1e06545340cb63df483d1db5b2a890499e99e6d3
workflow-type: tm+mt
source-wordcount: '2175'
ht-degree: 0%

---

# Patches da nuvem para o Commerce

A variável [Patches da nuvem](https://github.com/magento/magento-cloud-patches) O pacote do fornece um conjunto de patches necessários que melhoram a integração de todas as versões do Adobe Commerce com ambientes na nuvem e oferecem suporte à entrega rápida de correções críticas.

O pacote Cloud Patches for Commerce é uma dependência do pacote ECE-Tools e é instalado e atualizado ao instalar ou atualizar o pacote ECE-Tools. Você também pode usar e gerenciar Patches da nuvem para o Commerce como um pacote independente para aplicar patches a um projeto do Adobe Commerce que não esteja na plataforma da nuvem. Estas notas de versão descrevem as melhorias mais recentes neste pacote.

>[!TIP]
>
>Para garantir que seu projeto tenha todos os patches necessários, atualize para o [versão mais recente das ferramentas ece](../dev-tools/update-package.md).

>[!NOTE]
>
>Consulte [Aplicar patches](../development/apply-patches.md) para obter instruções sobre como aplicar patches aos projetos.

A variável `magento/magento-cloud-patches` O pacote usa a seguinte sequência de versão: `<major>.<minor>.<patch>`

<!--Add release notes below-->

## v1.0.25 {#latest}

Data de lançamento: 16 de janeiro de 2024

- **Melhorias no cache**-Este patch melhora a eficiência do cache de layout, reduzindo significativamente o uso de memória, para as versões 2.4.4 e posteriores do Adobe Commerce.<!-- MCLOUD-11514 -->
- **Melhorias nos trabalhos do CRON**-Este patch corrige o problema em que os trabalhos perdidos aguardam desnecessariamente bloqueios de trabalhos cron para as versões 2.4.4 e posteriores do Adobe Commerce.<!-- MCLOUD-11329 -->

## v1.0.24

Data de lançamento: 15 de setembro de 2023

- **Aprimoramento de desempenho**-Este patch corrige um problema que afeta o desempenho ao reduzir o número de vezes que as mesmas configurações de implantação são carregadas para o Adobe Commerce 2.4.6 para 2.4.6-p1<!-- MCLOUD-10604 -->

## v1.0.23

Data de lançamento: 31 de julho de 2023

- **Remoção do patch MCLOUD-10604**-Este patch foi movido para QPT.<!-- MCLOUD-10736 -->

## v1.0.22

Data de lançamento: 19 de junho de 2023

- **Assistente/saída aprimorado do QPT CLI**—Adição de um aviso ao assistente/saída QPT CLI que o lembrará de verificar os detalhes e requisitos do patch se houver dependências.<!-- ACP2E-1963 -->
- **Patches adicionados para o Commerce 2.4.6:**
   - Corrigido o `regexp cache tag` validação.<!-- MCLOUD-10226 -->
   - Desempenho aprimorado reduzindo o número de vezes que as mesmas configurações de implantação são carregadas.<!-- MCLOUD-10604 -->
- **Adição de patches para o Commerce 2.3.7 a 2.4.6**—Correção de um problema que causava um incremento de um valor aleatório em vez de um incremento de 1 para o `catalog_product_entity_*` tabelas.<!-- MCLOUD-10032 -->
- **Adição de patches para o Commerce 2.4.0 a 2.4.6**—Correção de um erro informando que `The file can't be deleted. Warning!unlink: No such file or directory`, que ocorreu ao limpar o cache JS/CSS do Administrador.<!-- MCLOUD-10279 -->

## v1.0.21

Data de lançamento: 10 de março de 2023

- **Suporte avançado para PHP 8.2**—Correção de problemas de compatibilidade com determinadas versões do PHP 8.2.x para suportar o Commerce 2.4.6.

## v1.0.20

Data de lançamento: 27 de outubro de 2022

- **Adição de patch de melhorias no cache L2**—Este patch corrige um problema na liberação do cache L2 local para as versões 2.4.0 e 2.4.1 do Commerce.<!-- MCLOUD-7845 -->

## v1.0.19

Data de lançamento: 13 de setembro de 2022

- **Suporte avançado para PHP 8.1**—Correção de problemas de compatibilidade com determinadas versões do PHP 8.1.x.

## v1.0.18

Data de lançamento: 11 de agosto de 2022

Patch crítico para o Adobe Commerce 2.4.5:

- **Problema com pedidos usando pagamentos Braintree**—Este patch soluciona um problema crítico que impedia os administradores de fazer novos pedidos ou repedidos.<!-- MCLOUD-9137 -->

Consulte [O administrador não pode criar pedido/reordenação quando o pagamento Braintree está ativado](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/known-issues-patches-attached/admin-cant-create-order-reorder-when-braintree-payment-enabled.html).

## v1.0.17

Data de lançamento: 24 de maio de 2022

Correção de restrições para patches de segurança no `patches.json` arquivo.

## v1.0.16

Data de lançamento: 31 de março de 2022

Patch crítico para o Adobe Commerce 2.3.3-p1 e versões posteriores:

Patches atualizados para resolver um **crítico** vulnerabilidade que resulta na execução de código remoto não autenticado.<!-- MCLOUD-8479 -->

Consulte [Boletim de segurança do Adobe APSB22-12](https://helpx.adobe.com/security/products/magento/apsb22-12.html).

## v1.0.15

Data de lançamento: 10 de março de 2022

- **Suporte ao PHP 8.1**—Adição de suporte para PHP 8.1 e remoção do suporte para PHP 7.0 e 7.1.
- **Adição de patch para o Adobe Commerce 2.3.3**—Moeda fixa exibida na página do produto.

## v1.0.14

Data de lançamento: 13 de fevereiro de 2022

Patch crítico para o Adobe Commerce 2.3.3-p1 e versões posteriores:

Adição de um patch para resolver um problema **crítico** vulnerabilidade que resulta na execução de código remoto não autenticado.<!-- MCLOUD-8461 -->

Consulte [Boletim de segurança do Adobe APSB22-12](https://helpx.adobe.com/security/products/magento/apsb22-12.html).

## v1.0.13

Data de lançamento: 25 de outubro de 2021

- **Atualizar monólogo**—Atualização da versão mínima necessária para o `monolog` empacotar para `^2.3`.<!-- ACMP-1263 -->
- **Método PHP incompatível**—Corrigido método incompatível de PHP para Adobe Commerce versões 2.4.3 e 2.3.7-p1.<!-- AC-384 -->
- **Erro de PHP**—Correção de um `PHP error 'Undefined variable: errorMessage' ...` erro que ocorreu ao tentar aplicar um patch.<!-- ACP2E-138 -->

## v1.0.12

Data de lançamento: 12 de agosto de 2021

Patch crítico para Adobe Commerce 2.4.3 e 2.3.7-p1:

- **Problema com a limitação de taxa da API**— Esse patch corrige um limite de taxa padrão que impedia que APIs da Web processassem solicitações com mais de 20 itens em um array. Este patch aumenta o valor padrão do limite de taxa. Consulte a Adobe Commerce [Notas de versão do 2.4.3](https://devdocs.magento.com/guides/v2.4/release-notes/commerce-2-4-3.html#apply-mc-43048__set_rate_limits__243patch-to-address-issue-with-api-rate-limiting) e a variável [Notas de versão do 2.3.7](https://devdocs.magento.com/guides/v2.3/release-notes/2-3-7-p1.html#apply-mc-43048__set_rate_limits__237-p1patch-to-address-issue-with-api-rate-limiting).<!-- MC-43048 -->

## v1.0.11

Data de lançamento: 29 de julho de 2021

- **Correção de um problema causado pela aplicação do patch de navegação em camadas B2B**—Para clientes que aplicaram o patch de navegação em camadas B2B, essa correção resolve um `Undefined offset` erro que é exibido na página Pesquisar após alternar a exibição da Loja.<!--MCLOUD-5287-->

- **Correção de checkout do Paypal**—Corrige um problema do Adobe Commerce 2.3.7 com o PayPal Express, no qual o preço do pedido inserido anteriormente é exibido.<!--MC-42674-->

- **Suporte à categoria de patch**— Adição de suporte para o processamento de categorias de patch e origens atribuídas a Patches de qualidade. As categorias permitem que os clientes usem filtros e classificação para encontrar patches mais rapidamente ao usar o [Ferramenta Correções de qualidade](https://github.com/magento/quality-patches) e a Ferramenta de análise do site (SWAT). <!--MC-38577-->

## v1.0.10

Data de lançamento: 10 de maio de 2021

- **Compatibilidade com o Adobe Commerce 2.3.7**—Conflito resolvido de dependências do composer para instalação no Adobe Commerce 2.3.7.<!--MC-42131-->
- **Correção de um problema causado pela aplicação de um patch agrupado várias vezes**—A aplicação de um patch agrupado (um que inclua outros patches obsoletos) mais de uma vez pode reverter os pacotes obsoletos incluídos. Agora, todos os patches são aplicados apenas uma vez. Tentar aplicar o mesmo pacote novamente mostra uma mensagem de que o patch já foi aplicado.<!--MC-41912-->
- **Correção de navegação em camadas B2B**—Correção de outro problema que impedia que a navegação em camadas mostrasse todas as opções do produto quando o usuário ativava o Catálogo compartilhado B2B.<!--MCLOUD-7742-->

## v1.0.9

Data de lançamento: 1 de fevereiro de 2021

- **Correção de navegação em camadas B2B**—Correção do problema que impedia que a navegação em camadas mostrasse todas as opções de produto quando o Catálogo compartilhado B2B era ativado.<!--MCLOUD-6923-->
- **Compatibilidade com o PHP 7.4**—Correção de um problema de compatibilidade de patches de nuvem com o PHP 7.4.<!--MCLOUD-7367-->
- **Patches obsoletos se tornam visíveis**—Correção de um problema de patches em nuvem em que os patches obsoletos se tornam visíveis na tabela de patches após a aplicação de um patch de substituição que contém todo o conteúdo do patch obsoleto. Isso pode acontecer se você aplicar um patch que combinou vários outros patches.<!--MC-40626-->
- **Falhas silenciosas ao aplicar patches**—Correção de um problema de correções de nuvem em que a variável `git apply` silenciosamente, o comando falhou ao aplicar patches em alguns ambientes.<!--MC-40529-->

## v1.0.8

Data de lançamento: 14 de outubro de 2020

- **Atualizações de compatibilidade do magento/magento-cloud-patches**—Atualizou o `symfony` e `semver` restrições de versão no `composer.json` para compatibilidade com o Adobe Commerce 2.4.1 e versões posteriores.<!--MCLOUD-7111-->

## v1.0.7

Data de lançamento: 14 de outubro de 2020

- **Patches Redis para Adobe Commerce 2.3.0 a 2.3.5, 2.4.0**—Atualização dos patches do Redis para oferecer suporte à adição de produtos a uma categoria ao implementar um cache de nível 2. <!--MCLOUD-6659-->

- **patch de VBE Braintree**—Corrige um problema que gerava um erro quando um Administrador tentava exibir um Relatório de liquidação de Braintree. <!--MCLOUD-6684-->

- Agora, a variável `ece-patches apply` usa o Unix `patch` comando para aplicar patches se o Git não estiver disponível no sistema host. <!--MCLOUD-7069-->

## v1.0.6

Data de lançamento:

- **Patches Redis para Adobe Commerce 2.3.0 - 2.3.4**— otimize a comunicação e melhore o desempenho
   - Reduza o tamanho das transferências de rede entre Redis e Adobe Commerce
   - Corrigir condições de corrida em operações de carregamento e gravação do Redis
   - Reescreva o adaptador de cache base para manipular erros ao salvar
   - Diminuir o consumo de Redis da CPU<!--MCLOUD-6139-->

- **Patches Redis para Adobe Commerce 2.3.0 - 2.3.5**—Melhore o desempenho e corrija erros
   - Corrija a implementação de Cache lock para evitar bloqueios infinitos
   - Melhorar o mecanismo de bloqueio atual
   - Implementar bloqueios assinados para impedir o desbloqueio de solicitações paralelas
   - Corrija o seguinte erro que ocorre na operação de gravação do Redis: `OOM command not allowed when used memory > maxmemory`
   - Corrigir o processamento para limpar o cache ao `cat_p` tag executada durante atualizações de produto<!--MCLOUD-6110-->

- Correção de um problema que causava um erro ao aplicar a `amzn/amazon-pay-module` correção para o Adobe Commerce em projetos de infraestrutura em nuvem com o Adobe Commerce v2.2.6 ou 2.3.5, que não incluem esse módulo. Agora, o processo de patch ignora o `amzn/amazon-pay-module` patch se o módulo não estiver instalado.<!--MCLOUD-6588-->

## v1.0.5

Data de lançamento: 26 de junho de 2020

- **Melhorias no desempenho do Redis**—Adiciona recursos de otimização do Redis às versões 2.3.3 e 2.3.4 do Adobe Commerce. Essas correções foram incluídas na versão 2.3.5 do Adobe Commerce. Consulte [Aumentos de desempenho](https://devdocs.magento.com/guides/v2.3/release-notes/release-notes-2-3-5-commerce.html#performance-boosts) no _Notas de versão do Adobe Commerce 2.3.5_.<!--MCLOUD-5771-->

- **Enriquecimento de log do New Relic**—Adiciona a interface do processador do Monolog necessária para oferecer suporte a melhorias nos recursos de registro do New Relic introduzidos nos Componentes da nuvem do Commerce, versão 1.0.4. Este patch é necessário para implantar o Adobe Commerce 2.1.x. Se o patch não for aplicado, ocorrerá uma falha na build durante o `di:compile` processo.<!--MCLOUD-6029-->

## v1.0.4

Data de lançamento: 12 de maio de 2020

- **Checkout de pagamento do Amazon**—Corrige um problema no widget de pagamento do Amazon Pay que impedia os clientes de alterar o método de pagamento no _Revisão e Pagamentos_ etapa durante o processo de finalização.<!--MCLOUD-5930-->

- **Exibição do produto na página Categoria**—Corrige um problema que impedia a exibição de produtos na página de categoria no _Mostrar todas as páginas_ exibição.<!--MCLOUD-5684-->

- **Upload de imagem do Page Builder**—Corrige um problema na interface do Page Builder que às vezes causava o seguinte erro ao carregar imagens na galeria de imagens: `Destination folder is not writable or does not exist`<!--MCLOUD-5837-->

- **Suprimir avisos desnecessários de geração de mapa de site**— Adiciona uma nova tentativa quando ocorrem erros durante a geração do mapa de site e ignora a notificação por email do cliente nos casos em que os erros podem ser recuperados automaticamente.<!--MCLOUD-3025-->

- **Aprimoramento de desempenho do site**—Corrige um problema de desempenho com o `Magento\Framework\App\DeploymentConfig\Reader::load` que periodicamente experimentaram longos tempos de carregamento que afetaram o desempenho do site. <!--MCLOUD-5650-->

- Atualização da atribuição de patch para patches do método de pagamento para direcionar os módulos de pagamento em vez do pacote base de Magento (magento/magento2-base) para que os patches de pagamento sejam aplicados somente se os módulos de pagamento existirem.<!--MCLOUD-5666-->

- Atualização de patches para compatibilidade com o Magento Open Source.<!--MCLOUD-5701-->

## v1.0.3

Data de lançamento: 28 de abril de 2020

- Adição de uma correção para o patch &quot;O FPC está sendo desativado durante as implantações&quot; para oferecer suporte ao Adobe Commerce 2.3.5.

## v1.0.2

Data de lançamento: 27 de fevereiro de 2020

Esta versão inclui os seguintes patches e correções críticas:

- **Atualizações de compatibilidade do magento/magento-cloud-patches**

   - Atualização do `symfony` e `semver` restrições de versão no `composer.json` para compatibilidade com o Adobe Commerce 2.4 e versões posteriores.<!--MAGECLOUD-5127-->

   - Restrições atualizadas no `composer.json` para compatibilidade com o `ece-tools` Versões 2002.0.22 e posteriores 2002.0.x.

- **Check-out do PayPal Express**—Publicado em 12 de fevereiro de 2020, este patch resolve um problema que afeta pedidos feitos com o Check-out do PayPal Express, onde o endereço de envio do pedido especifica uma região do país que foi inserida manualmente no campo de texto em vez de selecionada no menu suspenso na página Envio. Consulte a descrição completa do patch na página de download de patches.

- **Correção de implantação de aplicativo**—Adição de um patch para corrigir um problema que desativava o cache de página inteira durante o processo de implantação. Este patch se aplica ao Adobe Commerce 2.3.2 e versões posteriores.

- **Parâmetro de escopo para API assíncrona/em massa**—Atualização deste patch para corrigir um erro de sintaxe no `composer.json` arquivo. Este patch se aplica ao Magento Open Source 2.3.1 e 2.3.2. Consulte a descrição completa do patch na página de download de patches.

## v1.0.1

Data de lançamento: 6 de fevereiro de 2020

Incluímos todos os patches Magento Open Source 2.x da página de downloads de software na versão magento/magento-cloud-patches v1.0.1. Se você tiver copiado patches no projeto anteriormente, remova-os para evitar conflitos.

Esta versão inclui os seguintes patches e correções críticas:

- **Corrija bloqueios de cron e melhore o bloqueio de cron**—

   - Corrige um problema em que alguns trabalhos cron não eram executados devido a um valor de status incorreto no `cron_schedule` tabela. Agora, usamos a estrutura Adobe Commerce lock para verificar e atualizar o status do trabalho cron em vez de usar o `cron_schedule` tabela. Os trabalhos do CRON que terminaram com um status de erro são repetidos durante a próxima execução do CRON, em vez de aguardarem 24 horas.

   - Adiciona um _tentar novamente_ operação para evitar bloqueios durante atualizações dos dados na `cron_schedule` tabela.

- **Atualizado `magento/magento-cloud-patches` para incluir todos os patches disponíveis para o Magento Open Source 2.x**—Atualização do pacote magento/magento-cloud-patches para incluir todos os patches Magento Open Source 2.x disponíveis na página de downloads de software. Se você tiver copiado patches de Magento Open Source para o projeto Adobe Commerce na infraestrutura em nuvem anteriormente, remova-os para evitar conflitos.<!--MAGECLOUD-4606-->

- **Correção de paginação do catálogo Elasticsearch** —Substituição do patch de paginação do catálogo de Elasticsearch fornecido na magento/magento-cloud-patches v1.0 por uma correção mais eficaz.<!--MAGECLOUD-4847-->

- **Patches do Page Builder**—No Cloud Patches for Commerce 1.0.0, agrupamos patches do Page Builder para lidar com uma vulnerabilidade conhecida de execução remota de código (RCE) do Page Builder, com a correção inicial baseada no Adobe Commerce 2.3.3. Atualizamos esses patches com uma implementação mais estável baseada no Adobe Commerce 2.3.4., que inclui várias otimizações para corrigir o problema.<!--MAGECLOUD-4884-->

  Se você tiver o pacote magento/magento-cloud-patches 1.0.0, ainda estará protegido contra problemas de vulnerabilidade do RCE no Page Builder. Se você atualizar para 1.0.1 ou posterior, terá uma implementação melhor da mesma correção.

## v1.0.0

Data de lançamento: 14 de novembro de 2019

Esta é a primeira versão do [`magento/magento-cloud-patches`](https://github.com/magento/magento-cloud-patches) pacote, que é uma nova dependência para o `ece-tools` versão do pacote 2002.0.22 ou versões posteriores.

Esta versão inclui os seguintes patches e correções críticas:

- **Patches de segurança do Page Builder para as versões 2.3.1.x e 2.3.2.x**—Corrige um problema na visualização do Page Builder que permite que usuários não autenticados acessem alguns métodos de modelo que podem ser usados para acionar a execução de código arbitrário na rede (RCE), resultando em vazamentos de informações globais. Esse problema pode ocorrer ao usar versões não compatíveis do Page Builder com as versões 2.3.1 e 2.3.2 do Adobe Commerce.<!--MAGECLOUD-4649-->

- **Patches MSI**—Corrige problemas que causavam erros de indexação e problemas de desempenho ao usar configurações de inventário padrão para gerenciar o estoque.<!--MAGECLOUD-4428-->

- **Compatibilidade com versões anteriores de novas interfaces de email**-Corrige um problema de incompatibilidade com versões anteriores causado pela `Magento\Framework\Mail\EmailMessageInterface` Interface PHP introduzida no Adobe Commerce v2.3.3. No escopo deste patch, o novo `EmailMessageInterface` herda do antigo `MessageInterface`, e os módulos principais do Adobe Commerce são revertidos para depender do `MessageInterface`.<!--MAGECLOUD-4422-->

- **A paginação de catálogo não funciona no Elasticsearch 6.x**—Corrige um problema crítico na paginação de resultados de pesquisa que afeta clientes que usam o Elasticsearch 6.x como mecanismo de pesquisa de catálogo.<!--MAGECLOUD-4448-->
