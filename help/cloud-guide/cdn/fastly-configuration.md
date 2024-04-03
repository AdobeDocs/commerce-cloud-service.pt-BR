---
title: Configurar os serviços do Fastly
description: Saiba como configurar os serviços do Fastly para seu projeto no Adobe Commerce.
feature: Cloud, Configuration, Iaas, Cache, Security
exl-id: c53ff3bd-3df2-45fb-933e-d3b29f7edf4e
source-git-commit: 8a0523f1714b6ea41887e99b5c31294cf5e5255e
workflow-type: tm+mt
source-wordcount: '1961'
ht-degree: 0%

---

# Configurar os serviços do Fastly

O Fastly é necessário para o Adobe Commerce em ambientes de Preparo e Produção de infraestrutura em nuvem.

O Fastly funciona com o Varnish para fornecer recursos rápidos de armazenamento em cache e uma [Rede de entrega de conteúdo](https://glossary.magento.com/content-delivery-network) (CDN) para ativos estáticos. O Fastly também fornece um Firewall de Aplicativo Web (WAF) para proteger seu site e a infraestrutura da Nuvem. Para proteger seu site e sua infraestrutura em nuvem contra tráfego mal-intencionado e ataques, roteie todo o tráfego de entrada do site pelo Fastly.

>[!NOTE]
>
>O Fastly não está disponível em ambientes de integração.

Conclua as etapas a seguir para habilitar, configurar e testar o Fastly no início do processo de desenvolvimento do site para habilitar o acesso seguro ao site.

- Obter credenciais do Fastly para ambientes de preparo e produção
- Habilitar o cache Fastly CDN
- Carregar trechos de VCL do Fastly
- Atualizar a configuração do DNS para rotear o tráfego para o serviço Fastly
- Teste do armazenamento em cache Fastly

>[!NOTE]
>
>Depois de ativar e verificar a configuração inicial do Fastly, você pode personalizar a configuração. Por exemplo, você pode ativar opções adicionais, como otimização de imagem, módulos de borda e código de VCL personalizado. Consulte [Personalizar configuração do cache](fastly-custom-cache-configuration.md).

## Obter credenciais do Fastly

Durante o provisionamento do projeto, o Adobe adiciona o projeto à [Conta de serviço do Fastly](fastly.md#fastly-service-account-and-credentials) para Adobe Commerce na infraestrutura em nuvem e cria as credenciais da conta do Fastly para o Iniciador `master` e ambientes de produção e preparo profissionais. Cada ambiente tem credenciais exclusivas.

Você precisa das credenciais do Fastly para configurar os serviços do Fastly CDN no Administrador e enviar as solicitações da API do Fastly.

>[!NOTE]
>
>Com o Adobe Commerce na infraestrutura em nuvem, não é possível acessar diretamente o Fastly Admin. Use o administrador para revisar e atualizar a configuração do Fastly em seus ambientes. Se não conseguir resolver um problema usando os recursos do Fastly no Admin, envie um [Tíquete de suporte do Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket).

Use os métodos a seguir para localizar e salvar a ID de serviço e o token da API do Fastly no seu ambiente:

**Para ver suas credenciais do Fastly**:

O método de exibição de credenciais é diferente para projetos Pro e Starter.

- Diretório compartilhado montado em IaaS — Em projetos Pro, use SSH para se conectar ao servidor e obter as credenciais do Fastly no `/mnt/shared/fastly_tokens.txt` arquivo. Os ambientes de preparo e produção têm credenciais exclusivas. Você deve obter as credenciais para cada ambiente.

- Espaço de trabalho local — Na linha de comando, use o `magento-cloud` CLI para [lista e revisão](../environment/variables-cloud.md#viewing-environment-variables) Variáveis de ambiente do Fastly.

  ```bash
  magento-cloud variable:get -e <environment-ID>
  ```

- [!DNL Cloud Console]—Verifique as seguintes variáveis de ambiente no [Configuração do ambiente](../project/overview.md#configure-environment).

   - `CONFIG__DEFAULT__SYSTEM__FULL_PAGE_CACHE__FASTLY__FASTLY_API_KEY`

   - `CONFIG__DEFAULT__SYSTEM__FULL_PAGE_CACHE__FASTLY__FASTLY_SERVICE_ID`

>[!NOTE]
>
>Se não conseguir encontrar as credenciais do Fastly para os ambientes de Preparo ou Produção, entre em contato com o Adobe Customer Technical Advisor (CTA).

## Habilitar cache Fastly

Você precisa dos seguintes componentes para habilitar e configurar os serviços do Fastly:

- Versão mais recente da [CDN Fastly para o módulo Magento 2](fastly.md#fastly-cdn-module-for-magento-2) instalado nos ambientes de preparo e produção. Consulte [Atualizar o Fastly](#upgrade-the-fastly-module).

- [Credenciais do Fastly](#get-fastly-credentials) para Adobe Commerce em ambientes de preparo e produção de infraestrutura em nuvem

**Para ativar o armazenamento em cache do Fastly CDN no Armazenamento Temporário e na Produção**:

{{admin-login-step}}

1. Clique em **Lojas** > Configurações > **Configuração** > **Avançado** > **Sistema** e expandir **Cache de Página Inteira**.

   ![Expandir para selecionar Fastly](../../assets/cdn/fastly-menu.png)

1. No _Aplicativo de cache_ , remova a seleção de **Usar valor do sistema** e selecione **Fastly CDN** na lista suspensa.

   ![Escolher Fastly](../../assets/cdn/fastly-enable-admin.png)

1. Expandir **Configuração do Fastly** e [escolher opções de armazenamento em cache](https://github.com/fastly/fastly-magento2/blob/master/Documentation/CONFIGURATION.md#configure-the-module).

1. Após configurar as opções de armazenamento em cache, clique em **Salvar configuração** na parte superior da página.

1. Limpe o cache de acordo com a notificação.

1. Continue a configurar o Fastly navegando de volta para **Lojas** > **Configurações** > **Configuração** > **Avançado** > **Sistema** > **Configuração do Fastly**.

### Credenciais do Test Fastly

1. No Administrador, navegue até **Lojas** > Configurações > **Configuração** > **Avançado** > **Sistema** > **Configuração do Fastly**.

1. Se necessário, adicione o **ID de serviço do Fastly** e **Token de API** para o ambiente do projeto.

   ![Administrador de credenciais do Fastly](../../assets/cdn/fastly-credentials-admin-ui.png)

   >[!NOTE]
   >
   >Não selecione o link para criar o token da API do Fastly. Use o botão [Credenciais do Fastly (ID de serviço e token de API) fornecidas pelo Adobe](#get-fastly-credentials) fornecido pela Adobe.

1. Clique em **Testar credenciais**.

1. Se o teste tiver êxito, clique em **Salvar configuração** e, em seguida, limpe o cache.

   Se o teste falhar, verifique se os valores corretos da ID de serviço e do token da API correspondem às credenciais do ambiente atual.

   Se o teste falhar novamente, envie um tíquete de suporte da Adobe Commerce ou entre em contato com o representante da conta Adobe. Para projetos Pro, inclua os URLs para seus sites de Produção e Preparo. Para projetos iniciais, inclua os URLs dos `Master` e site de preparo.

>[!NOTE]
>
>Para obter instruções sobre como alterar as credenciais do token da API do Fastly para um ambiente de Preparo ou Produção, consulte [Alterar credenciais do Fastly](fastly.md#change-fastly-api-token).

### Carregar VCL para Fastly

Depois de habilitar o módulo Fastly, carregue o padrão [Código VCL](https://github.com/fastly/fastly-magento2/tree/master/etc/vcl_snippets) aos servidores Fastly. Este código fornece uma série de trechos de VCL que especificam as definições de configuração para habilitar o armazenamento em cache e outros serviços do Fastly CDN para sua infraestrutura do Adobe Commerce na nuvem.

>[!NOTE]
>
>Os serviços de cache do Fastly não funcionam até que você conclua o upload inicial do código do Fastly VCL para os sites de Preparo e Produção do Adobe Commerce.

**Para fazer upload do Fastly VCL**:

1. No _Configuração do Fastly_ clique em **Carregar VCL para Fastly** como mostra a figura a seguir.

   ![Carregar um VCL de Magento para o Fastly](../../assets/cdn/fastly-upload-vcl-admin.png)

1. Depois que o upload for concluído, atualize o cache de acordo com a notificação na parte superior da página.

## Provisionar certificados SSL/TLS

O Adobe fornece um certificado SSL/TLS validado pelo domínio para fornecer tráfego HTTPS seguro do Fastly. O Adobe fornece um certificado para cada ambiente Pro Production, Staging e Starter Production para proteger todos os domínios nesse ambiente. Para obter informações detalhadas sobre o certificado fornecido, consulte [Certificados SSL (TLS) do Adobe para Adobe Commerce na infraestrutura em nuvem](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/ssl-tls-certificates-for-magento-commerce-cloud-faq.html).

>[!NOTE]
>
>Você pode fornecer seu próprio certificado TLS ou SSL em vez de usar o certificado Let&#39;s Encrypt fornecido pelo Adobe. No entanto, esse processo requer trabalho adicional para configurar e manter. Para escolher essa opção, envie um tíquete de suporte da Adobe Commerce ou trabalhe com o Adobe para adicionar certificados personalizados e hospedados à sua Adobe Commerce em ambientes de infraestrutura em nuvem.

Para ativar os certificados SSL/TLS para ambientes Adobe Commerce, a automação do Adobe conclui as seguintes etapas:

- Valida a propriedade do domínio
- Provisiona um certificado Let&#39;s Encrypt SSL/TLS que cobre subdomínios e níveis superiores especificados para suas lojas
- Carrega o certificado para o ambiente de nuvem quando o site está ativo

Essa automação exige que você atualize a configuração de DNS do site para fornecer informações de validação de domínio. Uso **um** dos seguintes métodos:

- **Validação de DNS**-Para sites ativos, atualize sua configuração DNS com registros CNAME que apontem para o serviço Fastly
- **Registros CNAME de desafio ACME**- Atualize sua configuração de DNS com registros CNAME de desafio do ACME fornecidos pelo Adobe para cada domínio em seu ambiente

>[!TIP]
>
>Se você tiver um domínio de Produção que não esteja ativo, use os registros CNAME do desafio ACME para validação de domínio. Adicionar os registros à configuração de DNS antecipadamente permite que o Adobe provisione o certificado SSL/TLS com os domínios corretos antes da inicialização do site. Antes de iniciar a produção, você deve substituir esses registros de espaço reservado pelos registros CNAME fornecidos pelo Adobe.

Quando a validação do domínio for concluída, o Adobe provisionará o certificado Let&#39;s Encrypt TLS/SSL e o fará upload para os ambientes de preparo ou produção ativos. Esse processo pode levar até 12 horas. Recomendamos que você conclua as atualizações de configuração de DNS com vários dias de antecedência para evitar atrasos no desenvolvimento e na inicialização do site.

## Atualizar a configuração DNS com configurações de desenvolvimento

Durante o processo inicial de configuração do Fastly, você pode usar os seguintes URLs para configurar e testar o armazenamento em cache do Fastly nos ambientes de Preparo e Produção:

- Para preparo e produção profissionais:

   - `mcprod.<your-domain>.com`
   - `mcstaging.<your-domain>.com`

- Somente para produção inicial:

   - `mcprod.<your-domain>.com`

Esses URLs de pré-produção padrão ficam disponíveis após o provisionamento do projeto. O valor de `"your-domain"` é o nome de domínio especificado durante o processo de integração.

>[!NOTE]
>
>Não é possível especificar um domínio personalizado para um ambiente de não produção nos projetos iniciais.

Para rotear o tráfego dos URLs de armazenamento para o serviço Fastly, atualize a configuração do DNS. Ao atualizar a configuração, o Adobe provisiona automaticamente os certificados SSL/TLS necessários e faz o upload deles para os seus ambientes de nuvem. Esse provisionamento pode levar até 12 horas.

>[!NOTE]
>
>Quando estiver pronto para iniciar seu site de Produção, você deverá atualizar a configuração do DNS novamente para apontar seus domínios de produção para o serviço Fastly e concluir tarefas de configuração adicionais. Consulte [Lista de verificação de inicialização](../launch/checklist.md).

**Pré-requisitos:**

- Ative o módulo Fastly.
- Carregue o código padrão Fastly VCL.
- Forneça uma lista de domínios e subdomínios de nível superior para cada ambiente do Adobe ou envie um tíquete de suporte da Adobe Commerce.
- Aguarde a confirmação de que os domínios especificados foram adicionados aos ambientes da Nuvem.
- Em projetos iniciais, adicione os domínios à configuração do serviço Fastly. Consulte [Gerenciar domínios](fastly-custom-cache-configuration.md#manage-domains).
- Para obter informações sobre como atualizar a configuração do DNS, consulte [Registrador DNS](https://lookup.icann.org/) para obter o método correto para o serviço de domínio.

**Para atualizar a configuração de DNS para desenvolvimento**:

1. Aponte URLs de pré-produção para o serviço Fastly adicionando registros CNAME: `prod.magentocloud.map.fastly.net`, por exemplo:

   | Domínio ou Subdomínio | CNAME |
   |---------------------------|----------------------------------|
   | mcprod.your-domain.com | prod.magentocloud.map.fastly.net |
   | mcstaging.your-domain.com | prod.magentocloud.map.fastly.net |

   Quando os registros CNAME estão ativos, o Adobe provisiona certificados e faz upload dos certificados SSL/TLS.

   >[!NOTE]
   >
   >Se planeja usar domínios apex (`your-domain.com`) para o site de produção, você deve configurar os registros de endereço DNS (registros A) para apontar para os endereços IP do servidor Fastly. Consulte [Atualizar a configuração DNS com as configurações de produção](../launch/checklist.md#to-update-dns-configuration-for-site-launch).


1. Adicione registros CNAME de desafio do ACME para validação de domínio e pré-provisionamento de certificados SSL/TLS de produção, por exemplo:

   | Domínio ou Subdomínio | CNAME |
   |-------------------------------------------|-------------------------------------------|
   | _acme-challenge.your-domain.com | 0123456789abcdef.validation.magento.cloud |
   | _acme-challenge.www.your-domain.com | 9573186429stuvwx.validation.magento.com |
   | _acme-challenge.mystore.your-domain.com | 1234567898zxywvu.validation.magento.cloud |
   | _acme-challenge.subdomain.your-domain.com | 1098765743lmnopq.validation.magento.cloud |

   >[!NOTE]
   >
   >Os registros de desafio ACME neste exemplo são marcadores de posição que não têm como objetivo provisionar seus sites de preparo e produção do Adobe Commerce. Obtenha as informações corretas de registros de desafios do ACME para seu projeto entrando em contato com a Adobe.

   Depois de adicionar os registros CNAME, o Adobe valida os domínios e provisiona o certificado SSL/TLS para o ambiente. Ao atualizar a configuração de DNS para rotear o tráfego desses domínios para o serviço Fastly, o Adobe faz upload do certificado para o ambiente.

1. Atualize o URL básico do Adobe Commerce.

   - Use o SSH para fazer logon no ambiente de Produção do.

     ```bash
     magento-cloud ssh
     ```

   - Use a CLI da nuvem para alterar o URL de base da sua loja.

     ```bash
     php bin/magento setup:store-config:set --base-url="https://mcstaging.your-domain.com/"
     ```

   >[!NOTE]
   >
   >Como alternativa ao uso da CLI da nuvem, você pode atualizar o URL base no [Admin](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/site-store/store-urls.html)

1. Reinicie o navegador da Web.

1. Teste seu site.

## Teste do armazenamento em cache Fastly

Após concluir as alterações de configuração do DNS, use o [cURL](https://curl.se/) ferramenta de linha de comando para verificar se o cache do Fastly está funcionando.

**Para verificar os cabeçalhos de resposta**:

1. Em um terminal, use o seguinte `curl` comando para testar o URL do site ativo:

   ```bash
   curl -vo /dev/null -H Fastly-Debug:1 https://<live-URL>
   ```

   Se você não tiver definido uma rota estática ou concluído a configuração de DNS para os domínios no site ativo, use o `--resolve` sinalizador, que ignora a resolução de nome DNS.

   ```bash
   curl -vo /dev/null -H Fastly-Debug:1 --resolve <live-URL-hostname>:443:<live-IP-address>
   ```

1. Na resposta, verifique a [cabeçalhos](fastly-troubleshooting.md#check-cache-hit-and-miss-response-headers) para garantir o funcionamento do Fastly. Você deve ver os seguintes cabeçalhos exclusivos na resposta:

   ```http
   < Fastly-Magento-VCL-Uploaded: yes
   < X-Cache: HIT, MISS
   ```

Se os cabeçalhos não tiverem os valores corretos, consulte [Resolver erros encontrados nos cabeçalhos de resposta](fastly-troubleshooting.md#curl) para obter ajuda com a solução de problemas.

## Atualização do módulo Fastly

O Fastly atualiza o módulo CDN para Magento 2 para resolver problemas, aumentar o desempenho e fornecer novos recursos.
Recomendamos que você atualize o módulo Fastly nos ambientes de Preparo e Produção para o [versão mais recente](https://github.com/fastly/fastly-magento2/blob/master/VERSION).

Depois de atualizar o módulo, você deve fazer upload do código do VCL para aplicar as alterações na configuração do serviço Fastly.

>[!WARNING]
>
> Se você personalizou o código padrão do Fastly VCL com uma versão personalizada, a atualização do módulo Fastly substitui suas alterações. Se você tiver adicionado trechos de VCL personalizados com nomes exclusivos, essas alterações serão preservadas durante o processo de atualização. Como prática recomendada, atualize o ambiente de preparo e valide as alterações antes de aplicá-las ao ambiente de produção.

**Para verificar a versão do módulo CDN Fastly para o Magento 2**:

1. Altere para o diretório raiz do seu ambiente de nuvem.

1. Use o Composer para verificar a versão instalada.

   ```bash
   composer show *fastly*
   ```

1. Se a variável [versão mais recente](https://github.com/fastly/fastly-magento2/releases) não estiver instalado, conclua as etapas para atualizar o módulo Fastly.

**Para atualizar o módulo Fastly**:

1. No ambiente de integração local, use as seguintes informações do módulo para [atualização do módulo Fastly](../store/extensions.md#upgrade-an-extension).

   ```text
   module name: fastly/magento2
   repository: https://github.com/fastly/fastly-magento2.git
   ```

1. Envie suas atualizações para o ambiente de preparo.

1. Faça logon no Administrador para o ambiente de preparo para [carregar o código de VCL](#upload-vcl-to-fastly).

1. [Verificar os serviços do Fastly](fastly-troubleshooting.md#verify-or-debug-fastly-services) no site Preparo do Adobe Commerce.

Depois de verificar os serviços do Fastly no site de Preparo, repita o processo de atualização no ambiente de Produção.

>[!TIP]
>
> Se tiver problemas com os serviços Fastly nos ambientes do Adobe Commerce, consulte [Solução de problemas do Adobe Commerce Fastly](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/magento-fastly-troubleshooter.html).
