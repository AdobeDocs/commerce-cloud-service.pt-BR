---
title: Firewall de Aplicativo Web (WAF)
description: Saiba como o serviço Fastly WAF detecta, registra e bloqueia tráfego de solicitação mal-intencionado antes que ele possa danificar a rede ou os sites do Adobe Commerce.
feature: Cloud, Configuration, Security
exl-id: 40bfe983-7f32-4155-ae77-7cd18866f6e2
source-git-commit: 6b01bf91c3bf63ba268d0f8e10e19db4cb355997
workflow-type: tm+mt
source-wordcount: '824'
ht-degree: 0%

---

# Firewall de Aplicativo Web (WAF)

Desenvolvido pela Fastly, o serviço de firewall de aplicativo web (WAF) para o Adobe Commerce na infraestrutura em nuvem detecta, registra e bloqueia tráfego de solicitação mal-intencionado antes que possa danificar seus sites ou a rede. O serviço WAF está disponível somente em ambientes de produção.

O serviço WAF oferece os seguintes benefícios:

- **Conformidade com o PCI**— a ativação do WAF garante que as vitrines da Adobe Commerce nos ambientes de produção atendam aos requisitos de segurança do PCI DSS 6.6.
- **Política WAF padrão**— A política padrão do WAF, configurada e mantida pelo Fastly, fornece uma coleção de regras de segurança personalizadas para proteger seus aplicativos Web do Adobe Commerce contra uma grande variedade de ataques, incluindo ataques de injeção, entradas mal-intencionadas, script entre sites, filtragem de dados, violações de protocolo HTTP e outros [Dez Principais OWASP](https://owasp.org/www-project-top-ten/) ameaças à segurança.
- **Integração e habilitação de WAF**— o Adobe implanta e ativa a política WAF padrão no ambiente de produção em 2 a 3 semanas após o provisionamento ser concluído.
- **Suporte a operações e manutenção**—
   - O Adobe e o Fastly configuram e gerenciam seus registros e alertas para o serviço WAF.
   - O Adobe tria tíquetes de suporte ao cliente relacionados a problemas de serviço do WAF que bloqueiam o tráfego legítimo como problemas de Prioridade 1.
   - As atualizações automatizadas para a versão do serviço WAF garantem cobertura imediata para explorações novas ou em evolução. Consulte [Manutenção e atualizações do WAF](#waf-maintenance-and-updates).

>[!TIP]
>
>Para obter informações adicionais sobre como manter a conformidade com o PCI para sua Adobe Commerce em lojas de infraestrutura em nuvem, consulte [Conformidade com o PCI](https://business.adobe.com/products/magento/pci-compliance.html).

## Ativação do WAF

O Adobe habilita o serviço WAF em novas contas dentro de 2 a 3 semanas após o provisionamento ser concluído. O WAF é implementado por meio do serviço Fastly CDN. Não é necessário instalar ou manter nenhum hardware ou software.

>[!NOTE]
>
>Antes de usar o serviço WAF, todo o tráfego externo para o projeto Adobe Commerce na infraestrutura em nuvem deve ser roteado pelo serviço Fastly. Consulte [Configurar o Fastly](fastly-configuration.md).

## Como funciona

O serviço WAF integra-se ao Fastly e usa a lógica do cache no serviço Fastly CDN para filtrar o tráfego nos nós globais do Fastly. Ativamos o serviço WAF no ambiente de produção com uma política WAF padrão baseada em [Regras de segurança do Mod do Trustwave SpiderLabs](https://github.com/owasp-modsecurity/ModSecurity) e as dez principais ameaças à segurança da OWASP.

O serviço WAF filtra o tráfego HTTP e HTTPS (solicitações GET e POST) em relação ao conjunto de regras WAF e bloqueia o tráfego mal-intencionado ou não compatível com regras específicas. O serviço filtra somente o tráfego associado à origem que tenta atualizar o cache. Como resultado, interrompemos a maioria do tráfego de ataques no cache do Fastly, protegendo seu tráfego de origem de ataques mal-intencionados. Ao processar apenas o tráfego de origem, o serviço WAF preserva o desempenho do cache, introduzindo apenas uma latência estimada de 1,5 a 20 milissegundos para cada solicitação não armazenada em cache.

## Solução de problemas de solicitações bloqueadas

Quando o serviço WAF está ativado, ele filtra todo o tráfego da Web e administrativo em relação às regras WAF e bloqueia qualquer solicitação da Web que acione uma regra. Quando uma solicitação é bloqueada, o solicitante vê um padrão `403 Forbidden` página de erro que inclui uma ID de referência para o evento de bloqueio.

![Página de erro do WAF](../../assets/cdn/fastly-waf-403-error.png)

Você pode personalizar esta página de resposta de erro no Admin. Consulte [Personalizar a página de resposta do WAF](fastly-custom-response.md#customize-the-waf-error-page).

Se a página de administrador ou loja do Adobe Commerce retornar um `403 Forbidden` página de erro em resposta a uma solicitação de URL legítima, envie uma [Tíquete de suporte do Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket). Copie a ID de referência da página de resposta de erro e cole-a na descrição do ticket.

## Manutenção e atualizações do WAF

O Fastly mantém e atualiza o conjunto de regras do WAF com base em atualizações de regras de terceiros comerciais, pesquisas do Fastly e fontes abertas. O Fastly atualiza as regras publicadas em uma política, conforme necessário, ou quando alterações nas regras estão disponíveis em suas respectivas fontes. Além disso, o Fastly pode adicionar regras que correspondam às classes de regras publicadas na instância do WAF de qualquer serviço, após a ativação do serviço WAF. Essas atualizações garantem cobertura imediata para explorações novas ou em evolução.

Adobe e Fastly gerencie o processo de atualização para garantir que as regras do WAF novas ou modificadas funcionem efetivamente no ambiente de Produção antes que as atualizações sejam implantadas no modo de bloqueio.

## Limitação

O serviço WAF padrão desenvolvido pelo Fastly não é compatível com os seguintes recursos:

- Proteção contra malware ou mitigação de bot — considere usar [listas de controle de acesso](./fastly-vcl-allowlist.md) ou um serviço de terceiros.
- Limitação de taxa — Consulte [Limite de taxa](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/RATE-LIMITING.md) na documentação do Fastly ou consulte [Limitação de taxa](https://developer.adobe.com/commerce/webapi/get-started/rate-limiting/) no _API da Web do Commerce_ seção de segurança.
- Configurar um endpoint de registro para o cliente — Consulte [Serviço PrivateLink](../development/privatelink-service.md) como alternativa.

Embora o serviço WAF não permita bloquear ou permitir o tráfego com base em endereços IP, você pode adicionar listas de controle de acesso (ACL) e trechos de VCL personalizados ao serviço Fastly para especificar os endereços IP e a lógica de VCL para bloquear ou permitir o tráfego. Consulte [Trechos de VCL Fastly personalizados](fastly-vcl-custom-snippets.md).

A filtragem de solicitações TCP, UDP ou ICMP não é suportada pelo serviço WAF. No entanto, essa funcionalidade é fornecida pela proteção DDoS integrada incluída no serviço Fastly CDN. Consulte [Proteção de DDoS](fastly.md#ddos-protection).
