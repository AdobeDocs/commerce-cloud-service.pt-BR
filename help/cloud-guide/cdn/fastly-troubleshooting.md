---
title: Solução de problemas rápida
description: Saiba como solucionar problemas e gerenciar o módulo e os serviços do Fastly CDN para Adobe Commerce.
feature: Cloud, Configuration, Cache, Services
exl-id: e4c47035-cbad-4838-8d44-fa5eaaac42d1
source-git-commit: 1253d8357fd2554050d1775fefbc420a2097db5f
workflow-type: tm+mt
source-wordcount: '1834'
ht-degree: 0%

---

# Solução de problemas rápida

Use as informações a seguir para solucionar problemas e gerenciar o módulo Fastly CDN para o Magento 2 em seus ambientes de projeto do Adobe Commerce na infraestrutura em nuvem. Por exemplo, você pode investigar valores de cabeçalho de resposta e comportamento do armazenamento em cache para resolver problemas de serviço e desempenho do Fastly.

Em ambientes de produção e preparo profissionais, é possível usar [Logs do New Relic](../monitor/log-management.md) para exibir e analisar os dados de log do Fastly CDN e do WAF para solucionar erros e problemas de desempenho.

>[!NOTE]
>
>Para obter informações sobre a instalação e configuração do Fastly, consulte [Configurar o Fastly](fastly.md).

## Localizar ID de serviço do Fastly

Você precisa da ID de serviço do Fastly para configurar o Fastly no Admin ou para enviar solicitações da API do Fastly para obter configuração e solução de problemas avançadas do Fastly.

Se o Fastly estiver habilitado no ambiente do projeto, você poderá obter a ID do serviço do Administrador. Consulte [Obter credenciais do Fastly](fastly-configuration.md#get-fastly-credentials).

Desenvolvedores e usuários avançados de VCL podem usar o VCL personalizado para recuperar a ID de serviço usando a variável Fastly `req.service_id`. Por exemplo, é possível adicionar a variável `req.service_id` à diretiva de log personalizado no VCL para capturar o valor da ID de serviço:

```json
log {"syslog"} req.service_id {" my_logging_endpoint_name :: "}
```

Você pode usar o mesmo VCL para ambientes de produção e de preparo. Consulte [Como configurar vcl_log](https://support.fastly.com/hc/en-us/community/posts/360040447172-How-to-configure-vcl-log).

## Problemas de desempenho do site, limpeza e cache

Use a lista a seguir para identificar e solucionar problemas relacionados à configuração do serviço Fastly para seu ambiente do Adobe Commerce na infraestrutura em nuvem.

- **O menu Armazenar não é exibido nem funciona**—Você pode estar usando um link ou link temporário diretamente para o servidor de origem em vez de usar o URL do site ativo, ou você usou `-H "host:URL"` em um [comando cURL](#check-live-site-through-fastly). Se você ignorar o Fastly no servidor de origem, o menu principal não funcionará e cabeçalhos incorretos serão exibidos para permitir o armazenamento em cache no lado do navegador.

- **A navegação superior não funciona**—A navegação superior depende do processamento ESI (Edge Side Includes) que é ativado ao fazer upload dos trechos padrão do Magento Fastly VCL. Se a navegação não estiver funcionando, [fazer upload do Fastly VCL](fastly-configuration.md#upload-vcl-to-fastly) e verifique novamente o site.

- **A localização geográfica/GeoIP não funciona**— Os trechos padrão do Magento Fastly VCL anexam o código do país ao URL. Se o código do país não estiver funcionando, [fazer upload do Fastly VCL](fastly-configuration.md#upload-vcl-to-fastly) e verifique novamente o site.

- **As páginas não estão em cache**—Por padrão, o Fastly não armazena páginas com o `Set-Cookies` cabeçalho. O Adobe Commerce define cookies mesmo em páginas armazenáveis em cache (TTL > 0). O VCL padrão do Magento Fastly remove esses cookies nas páginas que podem ser armazenadas em cache. Se as páginas não estiverem armazenando em cache, [fazer upload do Fastly VCL](fastly-configuration.md#upload-vcl-to-fastly) e verifique novamente o site.

  Esse problema também poderá ocorrer se um bloco de página em um modelo for marcado como não armazenável em cache. Nesse caso, o problema provavelmente é causado por um módulo de terceiros ou uma extensão bloqueando ou removendo os cabeçalhos do Adobe Commerce. Para resolver o problema, consulte [O X-Cache contém apenas MISS, sem HIT](#x-cache-contains-only-miss-no-hit).

- **As solicitações de limpeza estão falhando**—O Fastly retorna o seguinte erro ao enviar uma solicitação de limpeza:

  ```text
  The purge request was not processed successfully.
  ```

  Esse problema pode ser causado por um dos seguintes:

   - Credenciais Fastly inválidas na configuração do serviço Fastly para o ambiente do projeto do Adobe Commerce na infraestrutura em nuvem
   - Código inválido em um trecho de VCL personalizado

  Para resolver o problema, consulte [Erro ao limpar o cache do Fastly na Nuvem](https://support.magento.com/hc/en-us/articles/115001853194-Error-purging-Fastly-cache-on-Cloud-The-purge-request-was-not-processed-successfully-) na Central de ajuda do Adobe Commerce.

## Erros 503 do Fastly

Se o Fastly retornar o erro de tempo limite 503, verifique os logs de erro e a página de erro 503 para identificar a causa raiz.

>[!NOTE]
>
>Se o tempo limite ocorrer durante a execução de operações em massa, você poderá [estender o tempo limite do Fastly para o Administrador](fastly-custom-cache-configuration.md#extend-fastly-timeout).

Se você receber um erro 503, verifique o log de erros do ambiente de Produção ou Preparo e o log de acesso php para solucionar o problema.

**Para verificar os logs de erros**:

- [Log de erros](../test/log-locations.md#application-logs)

  ```text
  /var/log/platform/<project-ID>/error.log
  ```

  Este log inclui todos os erros do aplicativo ou mecanismo PHP, por exemplo `memory_limit` ou `max_execution_time exceeded` erros. Se você não encontrar nenhum erro relacionado ao Fastly, verifique o log de acesso do PHP.

- Log de acesso do PHP

  ```text
  /var/log/platform/<project-ID>/php.access.log
  ```

  Procure no log respostas HTTP 200 para o URL que retornou o erro 503. Se você encontrar a resposta 200, significa que o Adobe Commerce retornou a página sem erros. Isso indica que o problema pode ter ocorrido após o intervalo que excede o `first_byte_timeout` valor definido na configuração do serviço Fastly.

Quando ocorre um erro 503, o Fastly retorna o motivo na página de erro e manutenção. Talvez não seja possível ver o motivo se você adicionou código para um [página de resposta personalizada](fastly-custom-response.md). Para exibir o código de motivo na página de erro padrão, é possível remover o código de HTML da página de erro personalizada.

**Para verificar a página de erro do Fastly 503**:

{{admin-login-step}}

1. Clique em **Lojas** > **Configurações** > **Configuração** > **Avançado** > **Sistema**.

1. No painel direito, expanda **Cache de Página Inteira**.

1. No **Configuração do Fastly** seção, expandir **Páginas sintéticas personalizadas** como mostra a figura a seguir.

   ![Página de erro 503 personalizada](../../assets/cdn/fastly-custom-synthetic-pages-edit-html.png)

1. Clique em **Definir HTML**.

1. Remova o código personalizado. Você pode salvá-lo em um programa de texto para adicioná-lo novamente mais tarde.

1. Clique em **Carregar** para enviar as atualizações ao Fastly.

1. Clique em **Salvar configuração** na parte superior da página.

1. Reabra o URL que causou o erro 503. O Fastly retorna uma página de erro com o motivo, como mostrado no exemplo a seguir.

   ![Erro Fastly](../../assets/cdn/fastly-503-example.png)

## Apex e subdomínios já associados a uma conta do Fastly

Se o domínio apex e os subdomínios do seu projeto do Adobe Commerce na infraestrutura em nuvem já estiverem associados a uma conta existente do Fastly com uma ID de Serviço atribuída, você não poderá iniciar o até atualizar a configuração do Fastly:

- Atualize a configuração de apex e subdomínio na conta existente do Fastly. Consulte [Várias contas do Fastly e domínios atribuídos](fastly.md#domain).

- [Ativar e configurar o Fastly](fastly-configuration.md#enable-fastly-caching) e conclua o [Configuração de DNS](../launch/checklist.md#update-dns-configuration-with-production-settings)

## Verificar ou depurar os serviços do Fastly

Você pode solucionar problemas de desempenho ou de cache de um site do Adobe Commerce na infraestrutura em nuvem testando os URLs do site e examinando os valores do cabeçalho retornados na resposta.

### Verifique o site ao vivo pelo Fastly

Use a API Fastly para verificar o  `Fastly-Magento-VCL-Uploaded` e `X-Cache` cabeçalhos de resposta retornados do site ativo.

As solicitações da API Fastly são transmitidas por meio da extensão Fastly para obter uma resposta dos servidores de origem. Se a resposta retornar cabeçalhos incorretos, teste o [servidores de origem diretamente](#bypass-fastly-cache-to-check-adobe-commerce-sites).

**Para verificar os cabeçalhos de resposta**:

1. Em um terminal, use o seguinte `curl` comando para testar o URL do site ativo:

   ```bash
   curl https://<live URL> -vo /dev/null -H Fastly-Debug:1
   ```

   Se você não tiver definido uma rota estática ou concluído a configuração de DNS para os domínios no site ativo, use o `--resolve` sinalizador, que ignora a resolução de nome DNS.

   ```bash
   curl -svo /dev/null --resolve '<your_hostname>:443:<IP-address-of-cache-node>' <https-URL>
   ```

   >[!NOTE]
   >
   >Para usar este comando com o `--resolve` , você deve ter o TLS ativado com o Fastly por meio de um certificado SSL/TLS e localizar o endereço IP do nó de cache.

1. Na resposta, verifique a [cabeçalhos](#check-cache-hit-and-miss-response-headers) para garantir o funcionamento do Fastly. Você deve ver os seguintes cabeçalhos exclusivos na resposta:

   ```http
   < Fastly-Magento-VCL-Uploaded: yes
   < X-Cache: HIT, MISS
   ```

Se os cabeçalhos não tiverem os valores corretos, consulte as seguintes informações:

- [Verificar upload de VCL](#fastly-vcl-has-not-been-uploaded)

- [O X-Cache contém apenas MISS, sem HIT](#x-cache-contains-only-miss-no-hit)

### Ignorar o cache do Fastly para verificar os sites do Adobe Commerce

Se o serviço Fastly retornar cabeçalhos incorretos, você poderá criar um trecho VCL que permitirá enviar solicitações que ignoram o cache do Fastly. Consulte [Ignorar cache Fastly](fastly-vcl-bypass-to-origin.md).

Depois de adicionar o trecho VCL, use comandos cURL para enviar solicitações ao servidor de origem a partir do endereço IP especificado. Em seguida, verifique se há erros nas respostas.

### Verificar cabeçalhos de resposta MISS e HIT do cache

Verifique se a resposta retornada contém as seguintes informações:

- Inclui o `X-Magento-Tags` cabeçalho

- O valor de `Fastly-Module-Enabled` o cabeçalho é `Yes` ou o número da versão do Fastly para o módulo CDN Magento 2 instalado no ambiente do projeto

- [Cache-Control: max-age](https://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9) é maior que 0

- [Pragma](https://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.32) a configuração é `cache`

O seguinte trecho da saída do comando cURL mostra os valores corretos para o `Pragma`, `X-Magento-Tags`, e `Fastly-Module-Enabled` cabeçalhos:

```terminal
* STATE: INIT => CONNECT handle 0x600057800; line 1402 (connection #-5000)
* Rebuilt URL to: https://www.mymagento.biz.c.sv7gVom4qrpek.ent.magento.cloud/
* Added connection 0. The cache now contains 1 members
* Trying 192.0.2.31...
* STATE: CONNECT => WAITCONNECT handle 0x600057800; line 1455 (connection #0)

% Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
0     0    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     0* Connected to www.mymagento.biz.c.sv7gVom4qrpek.ent.magento.cloud (54.229.163.31) port 443 (#0)

* STATE: WAITCONNECT => SENDPROTOCONNECT handle 0x600057800; line 1562 (connection #0)
  0     0    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     0* ALPN, offering h2

... portion omitted for brevity ...

< Set-Cookie: mage-messages=%5B%5D; expires=Wed, 22-Nov-2017 17:39:58 GMT; Max-Age=31536000; path=/
< Pragma: cache
< Expires: Wed, 23 Nov 2016 17:39:56 GMT
< Cache-Control: max-age=86400, public, s-maxage=86400, stale-if-error=5, stale-while-revalidate=5
< X-Magento-Tags: cb_welcome_popup store cb cb_store_info_mobile cb_header_promotional_bar cb_store_info cb_discount-promo-bar cpg_2 cb_83 cb_81 cb_84 cb_85 cb_86 cb_87 cb_88 cb_89 p5646 catalog_product p5915 p6040 p6197 p6227 p7095 p6109 p6122 p6331 p7592 p7651 p7690
< Fastly-Module-Enabled: yes
< Strict-Transport-Security: max-age=31536000
    < Content-Security-Policy: upgrade-insecure-requests
    < X-Content-Type-Options: nosniff
    < X-XSS-Protection: 1; mode=block
    < X-Frame-Options: SAMEORIGIN
    < X-Platform-Server: i-dff64b52
    <
    * STATE: PERFORM => DONE handle 0x600057800; line 1955 (connection #0)
    * multi_done
      0     0    0     0    0     0      0      0 --:--:--  0:00:02 --:--:--     0
    * Connection #0 to host www.mymagento.biz.c.sv7gVom4qrpek.ent.magento.cloud left intact
```

>[!NOTE]
>
>Para obter informações detalhadas sobre ocorrências e erros, consulte [Noções básicas sobre cabeçalhos MISS e HIT de cache com serviços protegidos](https://docs.fastly.com/guides/performance-tuning/understanding-cache-hit-and-miss-headers-with-shielded-services) na documentação do Fastly.

### Resolver erros encontrados em cabeçalhos de resposta

Esta seção fornece sugestões para resolver erros retornados ao verificar cabeçalhos de resposta usando a API do Fastly.

#### O módulo Fastly não está habilitado

Se o módulo Fastly não estiver habilitado (`Fastly-Module-Enabled: no`) ou se o cabeçalho estiver ausente, [usar SSH para fazer logon](../development/secure-connections.md#connect-to-a-remote-environment) ao projeto. Em seguida, execute o seguinte comando para verificar o status do módulo.

```bash
php bin/magento module:status Fastly_Cdn
```

Com base no status retornado, use as instruções a seguir para atualizar a configuração do Fastly.

- `Module does not exist`—Se o módulo não existir [instalar e configurar](https://github.com/fastly/fastly-magento2/blob/master/Documentation/INSTALLATION.md) o Módulo CDN Fastly para Magento 2 em uma ramificação de integração. Após a conclusão da instalação, habilite e configure o módulo. Consulte [Configurar o Fastly](fastly-configuration.md).

- `Module is disabled`—Se o módulo Fastly estiver desativado, atualize a configuração do ambiente em um `integration` no ambiente local para ativá-la. Em seguida, insira as alterações em Preparo e produção. Consulte [Gerenciar extensões](../store/extensions.md#install-an-extension).

  Se você usar [Gerenciamento de configurações](../store/store-settings.md#configure-store), verifique o status do módulo CDN Fastly no `app/etc/config.php` antes de enviar as alterações para o ambiente de produção ou de preparo.

  Se o módulo não estiver ativado (`Fastly_CDN => 0`) no `config.php` exclua o arquivo e execute o seguinte comando para atualizar `config.php` com as configurações mais recentes.

  ```bash
  bin/magento magento-cloud:scd-dump
  ```

#### O Fastly VCL não foi carregado

Se o Fastly VCL não tiver sido carregado (`Fastly-Magento-VCL-Uploaded`: `false`), use o *Carregar VCL* opção no Admin para carregá-lo. Consulte [Carregar trechos de VCL do Fastly](fastly-configuration.md#upload-vcl-to-fastly).

#### O X-Cache contém apenas MISS, sem HIT

Se a variável `X-Cache` o cabeçalho contém `HIT` (`HIT, HIT` ou `HIT, MISS`), indica que o Fastly retorna o conteúdo em cache com êxito.

Se a variável `X-Cache` o cabeçalho é `MISS, MISS` e não contém `HIT`, execute o `curl` para garantir que a página não tenha sido removida recentemente do cache.

Se você obtiver o mesmo resultado, use o [`curl` comandos](#check-live-site-through-fastly) e verifique a [cabeçalhos de resposta](#check-cache-hit-and-miss-response-headers):

- `Pragma` é `cache`
- `X-Magento-Tags` existe
- `Cache-Control: max-age` é maior que 0

Se o problema persistir, outra extensão provavelmente redefinirá esses cabeçalhos. Repita o procedimento a seguir no ambiente de preparo, desativando todas as extensões e reativando cada uma para determinar qual extensão está redefinindo os cabeçalhos. Depois de identificar a extensão que está causando o problema, você deve desabilitá-la no ambiente de Produção.

**Para identificar uma extensão que redefine cabeçalhos de resposta:**

{{admin-login-step}}

1. Navegue até **Lojas** > **Configurações** > **Configuração** > **Avançado** > **Avançado**.

1. No *Desabilitar Saída de Módulos* no painel direito, localize todas as extensões e desative-as.

1. Clique em **Salvar configuração**.

1. Clique em **Sistema** > **Ferramentas** > **Gerenciamento de cache**.

1. Clique em **Liberar cache de Magento**.

1. Complete as etapas a seguir para cada extensão que possa causar problemas com os cabeçalhos do Fastly:

   - Ative uma extensão de cada vez, salve a configuração e limpe o cache do Adobe Commerce.

   - Execute o [`curl` comandos](#check-live-site-through-fastly) para verificar a [cabeçalhos de resposta](#check-cache-hit-and-miss-response-headers).

   Repita esse processo para cada extensão. Se os cabeçalhos de resposta do Fastly não forem mais exibidos, você identificou a extensão que está causando problemas com o Fastly.

Depois de identificar a extensão que está redefinindo os cabeçalhos do Fastly, entre em contato com o desenvolvedor da extensão para obter assistência adicional. Não podemos fornecer correções ou atualizações para fazer com que extensões de terceiros funcionem com o armazenamento em cache do Fastly.

## Reverter configuração do Fastly

Se as atualizações de trecho de VCL personalizado ou outras alterações de configuração do Fastly fizerem com que um site de infraestrutura na nuvem do Adobe Commerce interrompa ou retorne erros, use a API do Fastly [ativar](https://docs.fastly.com/api/config#version_0b79ae1ba6aee61d64cc4d43fed1e0d5) para reverter para uma versão anterior do VCL. Não é possível reverter a versão do VCL a partir do Administrador.

**Para reverter a versão do VCL**:

1. Para obter uma lista das versões de VCL disponíveis para um serviço, execute o seguinte comando

   ```bash
   curl -H "Fastly-Key: <FASTLY_API_TOKEN>" -H "Accept: application/json" https://api.fastly.com/service/<FASTLY_SERVICE_ID>/version
   ```

1. Execute o seguinte comando para alterar a versão do VCL ativo para uma versão especificada.

   ```bash
   curl -H "Fastly-Key: <FASTLY_API_TOKEN>" -H "Content-Type: application/x-www-form-urlencoded" -H "Accept: application/json" -X PUT https://api.fastly.com/service/<FASTLY_SERVICE_ID>/version/<VERSION_ID>/activate
   ```

Para obter detalhes sobre como usar a API do Fastly para revisar e gerenciar o VCL, consulte [Gerenciar VCL usando a API](fastly-vcl-custom-snippets.md#manage-custom-vcl-snippets-using-the-api).
