---
title: Visão geral dos serviços Fastly
description: Saiba como os serviços do Fastly incluídos com o Adobe Commerce na infraestrutura em nuvem ajudam a otimizar e proteger as operações de entrega de conteúdo nos sites do Adobe Commerce.
feature: Cloud, Configuration, Iaas, Paas, Cache, Security, Services
exl-id: dc4500bf-f037-47f0-b7ec-5cd1291f73a1
source-git-commit: 13e76d3e9829155995acbb72d947be3041579298
workflow-type: tm+mt
source-wordcount: '1392'
ht-degree: 0%

---

# Visão geral dos serviços Fastly

>[!WARNING]
>
>Para manter a conformidade com o PCI para sites Adobe Commerce implantados na plataforma Cloud, configure o Fastly na sua ramificação principal do Starter, nos ambientes Pro Production e Pro Staging. Se você usa o Adobe Commerce em uma implantação headless, recomendamos usar o Fastly para armazenar em cache as respostas do GraphQL. Consulte [Armazenamento em cache com o Fastly](https://developer.adobe.com/commerce/webapi/graphql/usage/caching/#caching-with-fastly) no *Guia do desenvolvedor do GraphQL*.

O Fastly fornece os seguintes serviços para otimizar e proteger as operações de entrega de conteúdo para o Adobe Commerce em projetos de infraestrutura na nuvem. Esses serviços estão incluídos com o Adobe Commerce na infraestrutura em nuvem sem custo adicional.

- **Rede de entrega de conteúdo (CDN)**—Serviço baseado em verniz que armazena em cache páginas do site, ativos, CSS e muito mais, em data centers de back-end configurados por você. À medida que os clientes acessam o site e as lojas, as solicitações acessam o Fastly para carregar as páginas em cache mais rapidamente. O serviço CDN fornece os seguintes recursos:

- **Gerenciamento de cache**— armazena páginas do site em cache, ativos, CSS e muito mais, em data centers de back-end configurados por você para reduzir a carga e os custos de largura de banda

   - Uso [Trechos de VCL personalizados Fastly](fastly-vcl-custom-snippets.md) (Compatível com verniz 2.1) para modificar como o armazenamento em cache responde a solicitações

   - Configurar [Suporte a serviços GeoIP](fastly-custom-cache-configuration.md#configure-geoip-handling)

   - [Forçar solicitações não criptografadas para TLS](fastly-custom-cache-configuration.md#force-tls)

   - [Personalizar tempo limite do Fastly](fastly-custom-cache-configuration.md#extend-fastly-timeout) configurações para impedir respostas 503 em solicitações de operação em massa

   - Criar [páginas de resposta de erro personalizadas](fastly-custom-response.md)

- **Segurança**— depois de ativar os serviços Fastly nos sites da Adobe Commerce, recursos de segurança adicionais estão disponíveis para proteger seus sites e sua rede:

   - [Firewall de Aplicativo Web](fastly-waf-service.md) (WAF)—Serviço de firewall de aplicativo Web gerenciado que fornece proteção compatível com PCI para bloquear tráfego mal-intencionado antes que possa danificar sua produção Adobe Commerce em sites de infraestrutura em nuvem e rede. O serviço WAF está disponível somente em ambientes Pro e Starter Production.

   - [Proteção de DDoS (Negação de Serviço Distribuído)](#ddos-protection)— proteção DDoS integrada contra ataques comuns como Ping of Death, ataques Smurf e outros ataques de inundação baseados em ICMP.

   - [Certificados SSL/TLS](fastly-configuration.md#provision-ssltls-certificates)—O serviço Fastly requer um certificado SSL/TLS para veicular o tráfego seguro por HTTPS.

     A Adobe Commerce fornece um certificado Let&#39;s Encrypt SSL/TLS validado pelo domínio para cada ambiente de preparo e produção. A Adobe Commerce conclui a validação de domínio e o provisionamento de certificados durante o processo de configuração do Fastly.

- **Cloaking de origem**—Impede que o tráfego ignore o Fastly WAF e oculta os endereços IP de seus servidores de origem para protegê-los contra acesso direto e ataques de DDoS.

  O cloaking de origem é ativado por padrão nos projetos de produção do Adobe Commerce em infraestrutura em nuvem Pro. Para habilitar o cloaking de origem no Adobe Commerce em projetos de produção de iniciador da infraestrutura em nuvem, envie um [Tíquete de suporte do Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket). Se você tiver tráfego que não exija armazenamento em cache, é possível personalizar a configuração do serviço Fastly para permitir solicitações para [ignorar o cache do Fastly](fastly-vcl-bypass-to-origin.md).

- **[Otimização de imagem](fastly-image-optimization.md)**— descarrega o processamento de imagens e o redimensionamento da carga para o serviço Fastly para que os servidores possam processar pedidos e conversões com mais eficiência.

- **[Logs do Fastly CDN e WAF](../monitor/new-relic-service.md#new-relic-log-management)**— Para projetos Pro do Adobe Commerce na infraestrutura em nuvem, você pode usar o serviço New Relic Logs para revisar e analisar os dados de log do Fastly CDN e do WAF.

## Módulo Fastly CDN para Magento 2

Os serviços do Fastly para Adobe Commerce na infraestrutura em nuvem usam o [Módulo Fastly CDN para Magento 2] instalado nos seguintes ambientes: Preparo e produção Pro, Produção inicial (`master` filial).

No provisionamento inicial ou na atualização de seu projeto do Adobe Commerce, o Adobe instala a versão mais recente do módulo Fastly CDN em seus ambientes de Preparo e Produção. Quando o Fastly lança atualizações no módulo, você recebe notificações no Administrador para seus ambientes. A Adobe recomenda atualizar seus ambientes para usar a versão mais recente. Consulte [Atualizar o Fastly](fastly-configuration.md#upgrade-the-fastly-module).

## Conta de serviço e credenciais do Fastly

Adobe Os negócios em projetos de infraestrutura em nuvem não exigem uma conta dedicada do Fastly ou um proprietário de conta. Em vez disso, cada ambiente de preparo e produção tem credenciais exclusivas do Fastly (token da API e ID de serviço) para configurar e gerenciar os serviços do Fastly no Admin. Você também precisa das credenciais para enviar solicitações da API do Fastly.

Durante o provisionamento do projeto, o Adobe adiciona o projeto à conta de serviço do Fastly para Adobe Commerce na infraestrutura de nuvem e adiciona as credenciais do Fastly à configuração para os ambientes de Preparo e Produção. Consulte [Obter credenciais do Fastly](fastly-configuration.md#get-fastly-credentials).

### Alterar o token da API do Fastly

Envie um tíquete de Suporte da Adobe Commerce para alterar a credencial do token da API do Fastly. Ao receber o novo token, atualize o ambiente de preparo ou produção para usar o novo token.

**Para alterar a credencial do token da API do Fastly**:

1. [Enviar um tíquete de suporte da Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) solicitação de novas credenciais da API do Fastly.

   Inclua sua ID de projeto do Adobe Commerce na infraestrutura em nuvem e os ambientes que exigem uma nova credencial.

1. Depois de receber o novo token de API, atualize o valor do token de API no [Configuração de credenciais do Fastly](fastly-configuration.md#test-the-fastly-credentials) no Administrador ou no [[!DNL Cloud Console] variáveis de ambiente](../project/overview.md#configure-environment).

1. [Testar a nova credencial](fastly-configuration.md#test-the-fastly-credentials).

1. Depois de atualizar a credencial, envie um tíquete de suporte da Adobe Commerce para excluir o token da API antiga.

### Várias contas do Fastly e domínios atribuídos

O Fastly permite atribuir um domínio apex e subdomínios associados a um serviço e a uma conta do Fastly. Se você tiver uma conta existente do Fastly que vincula o mesmo ápice e subdomínios usados para o site do Adobe Commerce, terá as seguintes opções:

- Remova o apex e os subdomínios da conta existente antes de solicitar as credenciais de serviço do Fastly para os ambientes do projeto do Adobe Commerce na infraestrutura em nuvem. Consulte [Trabalhar com domínios] na documentação do Fastly.

  Use essa opção para vincular o domínio apex e todos os subdomínios à conta de serviço do Fastly para Adobe Commerce na infraestrutura de nuvem.

- Envie um tíquete de suporte do Adobe Commerce para solicitar a delegação de domínio para que o apex e os subdomínios possam ser vinculados a contas diferentes.

  Use essa opção se você tiver um domínio apex com vários subdomínios para sites do Adobe Commerce Adobe Commerce e de terceiros, e quiser vincular esses subdomínios a diferentes contas do Fastly.

#### Solicitar delegação de domínio

*Cenário 1:*

O domínio apex (`testweb.com` e `www.testweb.com`) está vinculado a uma conta existente do Fastly. Você tem um projeto do Adobe Commerce na infraestrutura em nuvem configurado com os seguintes subdomínios: `mcstaging.testweb.com` e `mcprod.testweb.com`. Você não deseja mover o domínio apex para a conta do serviço Fastly para o Adobe Commerce na infraestrutura de nuvem.

Enviar um [Tíquete de suporte do Fastly] solicitar que os subdomínios sejam delegados da conta existente do Fastly para a conta do Fastly para o Adobe Commerce na infraestrutura da nuvem. Inclua a ID do projeto do Adobe Commerce no tíquete.

Após a conclusão da delegação, os subdomínios do projeto podem ser adicionados à conta de serviço do Fastly para Adobe Commerce na infraestrutura da nuvem. Consulte [Obter credenciais do Fastly](fastly-configuration.md#get-fastly-credentials).

*Cenário 2:*

O domínio apex (`testweb.com` e `www.testweb.com`) está vinculado à conta do serviço Adobe Commerce on cloud infrastructure Fastly. Você deseja gerenciar os serviços do Fastly para `service.testweb.com` e `product-updates.testweb.com` subdomínios de uma conta diferente do Fastly.

Envie um tíquete de Suporte da Adobe Commerce solicitando que os subdomínios sejam delegados da conta de serviço Fastly na infraestrutura em nuvem do Adobe Commerce para a conta Fastly. Inclua a ID de serviço da conta do Fastly no ticket.

## Proteção de DDoS

A proteção DDOS é integrada ao serviço Fastly CDN. Depois de ativar os serviços do Fastly nos sites do Adobe Commerce, o Fastly filtra todo o tráfego da Web e administrativo para detectar e bloquear possíveis ataques.

- Para ataques direcionados à camada 3 ou 4, o serviço Fastly filtra o tráfego com base na porta e no protocolo, inspecionando somente solicitações HTTP ou HTTPS. ICMP, UDP e outros ataques iniciados pela rede são descartados em nossa borda de rede. Isso inclui ataques de reflexão e amplificação, que usam serviços UDP como SSDP ou NTP. Ao fornecer esse nível de proteção, bloqueamos efetivamente vários ataques comuns como Ping of Death, ataques Smurf e outras inundações baseadas em ICMP.

  O Fastly gerencia os ataques no nível de TCP na camada do cache. Essa estratégia fornece a escala e o contexto necessários por cliente para lidar com um ataque de inundação de SYN e suas muitas variantes, incluindo pilha de TCP, ataques de recursos e ataques de TLS nos sistemas Fastly.

- O Fastly também fornece proteção contra ataques de Camada 7. Se sua loja estiver com problemas de desempenho e você suspeitar de um ataque de DDoS de camada 7, envie um tíquete de suporte da Adobe Commerce. O Adobe pode criar e aplicar regras personalizadas ao serviço Fastly para inspecionar e filtrar solicitações mal-intencionadas com base no cabeçalho, carga útil ou uma combinação de atributos que identificam o tráfego de ataque. Consulte [Verificação de ataques de DDoS] e [Como bloquear tráfego mal-intencionado] no *Centro de ajuda do Adobe Commerce*.

<!--Link definitions-->

[Caching with Fastly]: https://developer.adobe.com/commerce/webapi/graphql/usage/caching/#caching-with-fastly

[Verificação de ataques de DDoS]: https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/checking-for-ddos-attack-from-cli.html

[Módulo Fastly CDN para Magento 2]: https://github.com/fastly/fastly-magento2

[Tíquete de suporte do Fastly]: https://docs.fastly.com/products/support-description-and-sla#support-requests

[Como bloquear tráfego mal-intencionado]: https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/block-malicious-traffic-for-magento-commerce-on-fastly-level.html

[Trabalhar com domínios]: https://docs.fastly.com/en/guides/working-with-domains
