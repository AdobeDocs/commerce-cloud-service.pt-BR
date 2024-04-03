---
title: Lista de verificação de inicialização
description: Revise os itens da lista de verificação para o lançamento do site.
exl-id: 4525742e-18c5-40d1-975d-00ba3f3a51a0
source-git-commit: 5b0a691a4355f5eda31d42cd3da9925439dfb510
workflow-type: tm+mt
source-wordcount: '1104'
ht-degree: 0%

---

# Lista de verificação de inicialização

Antes de implantar no ambiente de produção, baixe o [Lista de verificação de inicialização](../../assets/adobe-commerce-cloud-prelaunch-checklist.pdf)e usá-lo com essas instruções para confirmar que você concluiu toda a configuração e teste necessários. Veja uma visão geral do processo completo de implantação para Starter e Pro em [Implante sua loja](../deploy/staging-production.md).

## Teste completo na produção

Consulte [Testar implantação](../test/staging-and-production.md) para testar todos os aspectos de seus sites, lojas e ambientes. Esses testes incluem a verificação do Fastly, os UAT (User Acceptance Tests, Testes de aceitação do usuário) e testes de desempenho.

## TLS e Fastly

O Adobe fornece um certificado Let&#39;s Encrypt SSL/TLS para cada ambiente. Este certificado é necessário para que o Fastly forneça tráfego seguro via HTTPS.

Para usar esse certificado, você deve atualizar a configuração de DNS para que o Adobe possa concluir a validação do domínio e aplicar o certificado ao seu ambiente. Cada ambiente tem um certificado exclusivo que cobre os domínios da Adobe Commerce em sites de infraestrutura em nuvem implantados nesse ambiente. Recomendamos concluir e atualizar as configurações durante o [Processo de configuração rápida](../cdn/fastly-configuration.md).

## Atualizar a configuração DNS com as configurações de produção

Quando estiver pronto para iniciar o site, você deverá atualizar a configuração do DNS para rotear o tráfego do ambiente de produção por meio do serviço Fastly.

**Pré-requisitos:**

- [Configurar e testar o Fastly no ambiente de desenvolvimento](../cdn/fastly-configuration.md#)

- A configuração do ambiente de produção foi atualizada com todos os domínios necessários

  Normalmente, você trabalha com o Consultor técnico do cliente para adicionar todos os domínios e subdomínios de nível superior necessários às lojas. Para adicionar ou alterar os domínios do seu ambiente de produção, [Enviar um tíquete de suporte da Adobe Commerce](https://support.magento.com/hc/en-us/articles/360019088251). Aguarde a confirmação de que a configuração do projeto foi atualizada.

  Em projetos iniciais, você deve adicionar os domínios ao seu projeto. Consulte [Gerenciar domínios](../cdn/fastly-custom-cache-configuration.md#manage-domains).

- Certificado SSL/TLS provisionado para seus ambientes de produção.

  Se você adicionou os registros de desafio ACME para seus domínios de produção durante o processo de configuração do Fastly, o Adobe faz upload do certificado SSL/TLS para o ambiente de produção automaticamente ao atualizar a configuração do DNS para direcionar o tráfego para o serviço Fastly. Se você não pré-provisionou o certificado ou se atualizou seus domínios, o Adobe deve concluir a validação do domínio e provisionar o certificado, o que pode levar até 12 horas.

### Para atualizar a configuração DNS para a inicialização do site:

1. Atualize a seguinte configuração de DNS para o site de produção:

   - Defina todos os redirecionamentos necessários, especialmente se você estiver migrando de um site existente

   - Definir o registro de recurso raiz da região para endereçar o nome do host

   - Diminua o valor do TTL (Time-to-Live) para atualizar informações de DNS a fim de apontar os clientes para o armazenamento de produção correto

     Recomendamos um valor TTL significativamente menor ao alternar o registro DNS. Esse valor informa ao DNS por quanto tempo armazenar o registro DNS em cache. Quando encurtado, ele atualiza o DNS mais rapidamente. Por exemplo, você pode alterar o valor de TTL de três dias para 10 minutos ao atualizar seu site. Observe que a redução do valor de TTL adiciona carga à infraestrutura DNS. Restaure o valor anterior e mais alto após a inicialização do site.


1. Adicionar registros CNAME para apontar os subdomínios do seu ambiente de produção para o serviço Fastly `prod.magentocloud.map.fastly.net`, por exemplo:

   | Domínio ou Subdomínio | CNAME |
   | ----------------------- | -------------------------------- |
   | `www.<domain-name>.com` | prod.magentocloud.map.fastly.net |
   | `mystore.<domain-name>.com` | prod.magentocloud.map.fastly.net |

1. Se necessário, adicione registros A para mapear o domínio apex (`<domain-name>.com`) para os seguintes endereços IP Fastly:

   | Domínio apex | NOME |
   | --------------- | ----------------- |
   | `<domain-name>.com` | `151.101.1.124` |
   | `<domain-name>.com` | `151.101.65.124` |
   | `<domain-name>.com` | `151.101.129.124` |
   | `<domain-name>.com` | `151.101.193.124` |

>[!IMPORTANT]
>
>As instruções de DNS em [RFC1034](https://www.rfc-editor.org/rfc/rfc1912) (**seção 2.4**) declaram que:
>_Um registro CNAME não pode coexistir com outros dados. Em outras palavras, se suzy.podunk.xx for um pseudônimo de sue.podunk.xx, você não poderá ter também um registro MX para suzy.podunk.edu, um registro A ou até mesmo um registro TXT._
>
>Por esse motivo, os registros DNS devem ser do tipo `CNAME` para subdomínios e tipo `A` para domínios apex (domínios raiz). Descartar essa regra pode causar interrupções no serviço de email ou na propagação do DNS, pois você perde a capacidade de adicionar outros registros, como MX ou NS. Alguns provedores de DNS podem contornar isso usando personalizações internas, mas seguir o padrão garante estabilidade e flexibilidade (como a alteração do provedor de DNS).

1. Atualize o URL base.

   - Use o SSH para fazer logon no ambiente de Produção do.

     ```bash
     magento-cloud ssh -e production
     ```

   - Use a CLI para alterar o URL de base da sua loja.

     ```bash
     php bin/magento setup:store-config:set --base-url="https://www.<domain-name>.com/"
     ```

   **NOTA**: também é possível atualizar o URL base no Admin. Consulte [Armazenar URLs](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/site-store/store-urls.html) no _Guia da experiência de compras e lojas do Adobe Commerce_.

1. Aguarde alguns minutos para que o site seja atualizado.

1. Teste seu site.

## Verificar configuração de produção

Faça uma aprovação final para validar a configuração de Produção para um ou mais armazenamentos. Você pode atualizar a configuração no ambiente de Produção. Se as configurações forem somente leitura, talvez seja necessário abrir uma conexão SSH e usar comandos CLI para alterar a configuração ou fazer alterações de configuração em seu ambiente local. Após concluir as atualizações, é possível implantar as alterações nos ambientes de preparo e produção.

Os itens a seguir são alterações e verificações recomendadas:

- [Teste de email de saída concluído](../project/outgoing-emails.md)

- [Configuração segura para credenciais de Administrador e URL de Administração Base](https://docs.magento.com/user-guide/stores/security-admin.html)

- [Otimizar todas as imagens para a Web](../cdn/fastly-image-optimization.md)

- [Verificar configurações de minificação para HTML, JavaScript e CSS](../deploy/static-content.md)

## Verificar o armazenamento em cache Fastly

- Teste e verifique se o Fastly caching está funcionando corretamente no local de Produção. Para testes e verificações detalhados, consulte [Teste rápido](../test/staging-and-production.md#check-fastly-caching).

- [Verifique se a versão mais recente do módulo CDN Fastly para Commerce está instalada em seu ambiente de Produção](../cdn/fastly-configuration.md#upgrade-the-fastly-module)

- [Verifique se a versão mais recente do código do Fastly VCL foi carregada](../cdn/fastly-configuration.md#upload-vcl-to-fastly)

## Teste de desempenho

Recomendamos que você analise a [Kit de ferramentas de desempenho](https://github.com/magento/magento2/tree/2.4/setup/performance-toolkit) como parte do processo de preparação para o pré-lançamento.

Você também pode testar usando as seguintes opções de terceiros:

- [Cerco](https://www.joedog.org/siege-home/): software de modelagem e teste de tráfego para levar sua loja ao limite. Acesse seu site com um número configurável de clientes simulados. O Cerco é compatível com autenticação básica, cookies, HTTP, HTTPS e protocolos FTP.

- [Jmeter](https://jmeter.apache.org/): excelente teste de carga para ajudar a medir o desempenho em picos de tráfego, como em vendas de flash. Crie testes personalizados para executar no site.

- [New Relic](https://support.newrelic.com/s/) (fornecido): ajuda a localizar processos e áreas do site que causam desempenho lento com o tempo rastreado gasto por ação, como transmitir dados, consultas, Redis e muito mais.

- [WebPageTest](https://www.webpagetest.org/) e [PKingdom](https://www.pingdom.com/): a análise em tempo real do tempo de carregamento das páginas do site com diferentes locais de origem. PKingdom pode custar uma taxa. WebPageTest é uma ferramenta gratuita.

## Configuração de segurança

- [Configurar a verificação de segurança](overview.md#set-up-the-security-scan-tool)

- [Configuração segura para o usuário administrador](https://docs.magento.com/user-guide/stores/security-admin.html)

- [Configuração segura do URL do administrador](https://docs.magento.com/user-guide/stores/store-urls-custom-admin.html)

- [Remova os usuários que não estão mais no projeto Adobe Commerce na infraestrutura em nuvem](../project/user-access.md)

- [Configurar autenticação de dois fatores](https://devdocs.magento.com/guides/v2.4/security/two-factor-authentication.html)

## Monitoramento de desempenho

Você pode usar os serviços da New Relic para monitorar o desempenho em ambientes Pro e Starter. Em contas de plano Pro, fornecemos os alertas gerenciados para a política de alertas da Adobe Commerce para monitorar o desempenho do aplicativo e da infraestrutura usando agentes de APM e infraestrutura da New Relic. Para obter detalhes sobre o uso desses serviços, consulte [Monitorar o desempenho com alertas gerenciados](../monitor/investigate-performance.md#monitor-performance-with-managed-alerts).

### Próxima etapa

[Etapas de inicialização](steps.md)
