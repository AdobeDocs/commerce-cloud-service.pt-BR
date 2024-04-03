---
title: Configurar vários sites ou lojas
description: Saiba como configurar vários sites ou lojas para o Adobe Commerce na infraestrutura em nuvem.
feature: Cloud, Configuration, Routes, Site Navigation
exl-id: 16e932ef-f083-44d7-977f-0c78899e151a
source-git-commit: 85aa54af10e7ea44adde5403b69ff03d4a0c622f
workflow-type: tm+mt
source-wordcount: '1013'
ht-degree: 0%

---

# Configurar vários sites ou lojas

Você pode configurar o Adobe Commerce para ter vários sites ou lojas, como uma loja em inglês, uma loja em francês e uma loja em alemão. Consulte [Noções básicas sobre sites, lojas e visualizações de loja](best-practices.md#store-views).

>[!WARNING]
>
>Os dados do catálogo se expandem à medida que você aumenta o número de sites e lojas. Dependendo da arquitetura do projeto, os armazenamentos adicionais podem levar a um processo de indexação mais longo e tempos de resposta mais lentos para páginas de catálogo não armazenadas em cache. A Adobe recomenda que você monitore o desempenho do site com cuidado.

O processo para configurar vários armazenamentos depende da sua escolha entre usar domínios exclusivos ou compartilhados.

Vários armazenamentos com domínios exclusivos:

```terminal
https://first.store.com/
https://second.store.com/
```

Vários armazenamentos com o mesmo domínio:

```terminal
https://store.com/first/
https://store.com/second/
```

>[!TIP]
>
>Para adicionar uma visualização de loja à URL base do site, não é necessário criar vários diretórios. Consulte [Adicionar o código de armazenamento ao URL base](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/multi-sites/ms-admin.html) no _Guia de configuração_.

## Adicionar domínios

Domínios personalizados podem ser adicionados ao Pro Staging e a qualquer ambiente de produção; eles não podem ser adicionados a ambientes de integração.

O processo para adicionar um domínio depende do tipo de conta da Cloud:

- Para preparo e produção profissionais

  Adicione o novo domínio ao Fastly, consulte [Gerenciar domínios](../cdn/fastly-custom-cache-configuration.md#manage-domains)ou abra um tíquete de suporte para solicitar assistência. Além disso, você deve [Enviar um tíquete de suporte da Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) para solicitar novos domínios para serem adicionados a um cluster.

- Somente para produção inicial

  Adicione o novo domínio ao Fastly, consulte [Gerenciar domínios](../cdn/fastly-custom-cache-configuration.md#manage-domains)ou [Enviar um tíquete de suporte da Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) para solicitar assistência. Além disso, você deve adicionar o novo domínio à **Domínios** na guia [!DNL Cloud Console]: `https://<zone>.magento.cloud/projects/<project-ID>/edit`

## Configurar instalação local

Para configurar sua instalação local para usar várias lojas, consulte [Vários sites ou lojas][config-multiweb] no _Guia de configuração_.

Depois de criar e testar com êxito a instalação local para usar várias lojas, você deve preparar seu ambiente de integração:

1. **Configurar rotas ou locais**—especifica como os URLs de entrada são tratados pelo Adobe Commerce

   - [Rotas para domínios separados](#configure-routes-for-separate-domains)
   - [Locais para domínios compartilhados](#configure-locations-for-shared-domains)

1. **Configurar sites, lojas e visualizações de loja**—configurar usando a interface do usuário do Adobe Commerce Admin
1. **Modificar variáveis**—especifique os valores de `MAGE_RUN_TYPE` e `MAGE_RUN_CODE` variáveis no `magento-vars.php` arquivo
1. **Implantar e testar ambientes**—implantar e testar o `integration` ramificação

>[!TIP]
>
>Você pode usar um ambiente local para configurar vários sites ou lojas. Consulte as instruções do Cloud Docker para [Configurar vários sites ou lojas](https://developer.adobe.com/commerce/cloud-tools/docker/configure/multiple-sites/).

### Atualizações de configuração para ambientes Pro

{{pro-self-service-warning}}

### Configurar rotas para domínios separados

As rotas definem como processar URLs de entrada. Vários armazenamentos com domínios exclusivos exigem que você defina cada domínio no `routes.yaml` arquivo. A maneira como você configura as rotas depende de como você deseja que o site funcione.

**Para configurar rotas em um ambiente de integração**:

1. Na estação de trabalho local, abra o `.magento/routes.yaml` em um editor de texto.

1. Defina o domínio e os subdomínios. A variável `mymagento` o valor upstream é o mesmo valor que a propriedade name na variável `.magento.app.yaml` arquivo.

   ```yaml
   "http://{default}/":
       type: upstream
       upstream: "mymagento:http"
   
   "http://<second-site>.{default}/":
       type: upstream
       upstream: "mymagento:http"
   ```

1. Salve as alterações no `routes.yaml` arquivo.

1. Continue para [Configurar sites, lojas e visualizações de loja](#set-up-websites-stores-and-store-views).

### Configurar locais para domínios compartilhados

Onde a configuração de roteiros define como os URLs são processados, a variável `web` propriedade na `.magento.app.yaml` define como o aplicativo é exposto à web. Web _locais_ permita mais granularidade para solicitações recebidas. Por exemplo, se o domínio for `store.com`, você pode usar `/first` (site padrão) e `/second` para solicitações a dois armazenamentos diferentes que compartilham um domínio.

**Para configurar um novo local da Web**:

1. Criar um alias para a raiz (`/`). Neste exemplo, o alias é `&app` na linha 3.

   ```yaml
   web:
       locations:
           "/": &app
               # The public directory of the app, relative to its root.
               root: "pub"
               passthru: "/index.php"
               index:
               - index.php
               ...
   ```

1. Criar uma passagem para o site (`/website`) e faça referência à raiz usando o alias da etapa anterior.

   O alias permite `website` para acessar valores do local raiz. Neste exemplo, o site `passthru` está na linha 21.

   ```yaml
   web:
       locations:
           "/": &app
               # The public directory of the app, relative to its root.
               root: "pub"
               passthru: "/index.php"
               index:
               - index.php
               ...
           "/media":
               root: "pub/media"
               ...
           "/static":
               root: "pub/static"
               allow: true
               scripts: false
               passthru: "/front-static.php"
               rules:
                   ^/static/version\d+/(?<resource>.*)$:
                       passthru: "/static/$resource"
           "/<website>": *app
             ...
   ```

**Para configurar um local com um diretório diferente**:

1. Criar um alias para a raiz (`/`) e para o estático (`/static`) locais.

   ```yaml
   web:
       locations:
           "/": &root
               # The public directory of the app, relative to its root.
               root: "pub"
               passthru: "/index.php"
               index:
               - index.php
               ...
           "/static": &static
               root: "pub/static"
   ```

1. Crie um subdiretório para o site sob o `pub` diretório: `pub/<website>`

1. Copie o `pub/index.php` arquivo na `pub/<website>` e atualize o `bootstrap` caminho (`/../../app/bootstrap.php`).

   ```
   try {
       require __DIR__ . '/../../app/bootstrap.php';
   } catch (\Exception $e) { 
   ```

1. Crie uma passagem para o `index.php` arquivo.

   ```yaml
   web:
       locations:
           "/": &root
               # The public directory of the app, relative to its root.
               root: "pub"
               passthru: "/index.php"
               index:
               - index.php
               ...
           "/media":
               root: "pub/media"
               ...
           "/static": &static
               root: "pub/static"
               allow: true
               scripts: false
               passthru: "/front-static.php"
               rules:
                   ^/static/version\d+/(?<resource>.*)$:
                       passthru: "/static/$resource"
           "/<website>":
               <<: *root
               passthru: "<website>/index.php"
           "/<website>/static": *static
             ...
   ```

1. Confirme e envie por push os arquivos alterados.

   - `pub/<website>/index.php` (Se este arquivo estiver em `.gitignore`, o push pode exigir a opção force.)
   - `.magento.app.yaml`

### Configurar sites, lojas e visualizações de loja

No _Interface do administrador_, configurar seu Adobe Commerce **Sites**, **Lojas**, e **Armazenar visualizações**. Consulte [Configurar vários sites, lojas e visualizações de loja no Administrador](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/multi-sites/ms-admin.html) no _Guia de configuração_.

É importante usar o mesmo nome e código de seus sites, lojas e exibições de loja do Administrador ao configurar a instalação local. Esses valores são necessários ao atualizar a variável `magento-vars.php` arquivo.

### Modificar variáveis

Em vez de configurar um host virtual NGINX, passe o `MAGE_RUN_CODE` e `MAGE_RUN_TYPE` variáveis usando o `magento-vars.php` arquivo no diretório raiz do projeto.

**Para transmitir variáveis usando o `magento-vars.php` arquivo**:

1. Abra o `magento-vars.php` em um editor de texto.

   A variável [padrão `magento-vars.php` arquivo](https://github.com/magento/magento-cloud/blob/master/magento-vars.php) deve ser semelhante ao seguinte:

   ```php
   <?php
   // enable, adjust and copy this code for each store you run
   // Store #0, default one
   //if (isHttpHost("example.com")) {
   //    $_SERVER["MAGE_RUN_CODE"] = "default";
   //    $_SERVER["MAGE_RUN_TYPE"] = "store";
   //}
   function isHttpHost($host)
   {
       if (!isset($_SERVER['HTTP_HOST'])) {
           return false;
       }
       return $_SERVER['HTTP_HOST'] === $host;
   }
   ```

1. Mover o comentado `if` bloco para que seja _após_ o `function` não é mais comentado.

   ```php
   <?php
   // enable, adjust and copy this code for each store you run
   // Store #0, default one
   
   function isHttpHost($host)
   {
       if (!isset($_SERVER['HTTP_HOST'])) {
           return false;
       }
       return $_SERVER['HTTP_HOST'] ===  $host;
   }
   
   if (isHttpHost("example.com")) {
       $_SERVER["MAGE_RUN_CODE"] = "default";
       $_SERVER["MAGE_RUN_TYPE"] = "store";
   }
   ```

1. Substitua os seguintes valores na variável `if (isHttpHost("example.com"))` bloco:
   - `example.com`—com o URL de base do seu _site_
   - `default`—com o CÓDIGO exclusivo para o _site_ ou _exibição de loja_
   - `store`—com um dos seguintes valores:
      - `website`— load o _site_ na loja
      - `store`— load a _exibição de loja_ na loja

   Para vários sites usando domínios exclusivos:

   ```php
   <?php
   function isHttpHost($host)
   {
       if (!isset($_SERVER['HTTP_HOST'])) {
       return false;
       }
       return $_SERVER['HTTP_HOST'] ===  $host;
   }
   
   if (isHttpHost("second.store.com")) {
       $_SERVER["MAGE_RUN_CODE"] = "<second-site>";
       $_SERVER["MAGE_RUN_TYPE"] = "website";
   }elseif (isHttpHost("store.com")){
       $_SERVER["MAGE_RUN_CODE"] = "base";
       $_SERVER["MAGE_RUN_TYPE"] = "website";
   }
   ```

   Para vários sites com o mesmo domínio, é necessário verificar o _host_ e a variável _URI_:

   ```php
   <?php
   function isHttpHost($host)
   {
       if (!isset($_SERVER['HTTP_HOST'])) {
       return false;
       }
       return $_SERVER['HTTP_HOST'] ===  $host;
   }
   
   if (isHttpHost("store.com")) {
      $code = "base";
      $type = "website";
   
      $uri = explode('/', $_SERVER['REQUEST_URI']);
      if (isset($uri[1]) && $uri[1] == 'second') {
        $code = '<second-site>';
        $type = 'website';
      }
      $_SERVER["MAGE_RUN_CODE"] = $code;
      $_SERVER["MAGE_RUN_TYPE"] = $type;
   }
   ```

1. Salve as alterações no `magento-vars.php` arquivo.

### Implantar e testar no servidor de integração

Envie suas alterações para o ambiente de integração do Adobe Commerce na infraestrutura em nuvem e teste seu site.

1. Adicionar, confirmar e enviar alterações de código à ramificação remota.

   ```bash
   git add -A && git commit -m "Implement multiple sites" && git push origin <branch-name>
   ```

1. Aguarde a conclusão da implantação.

1. Após a implantação, abra o URL da loja em um navegador da web.

   Com um domínio exclusivo, use o formato: `http://<magento-run-code>.<site-URL>`

   Por exemplo, `http://french.master-name-projectID.us.magentosite.cloud/`

   Com um domínio compartilhado, use o formato: `http://<site-URL>/<magento-run-code>`

   Por exemplo, `http://master-name-projectID.us.magentosite.cloud/french/`

1. Teste seu site completamente e mescle o código ao `integration` para implantação adicional.

## Implantar para preparo e produção

Siga o processo de implantação para [implantação no armazenamento temporário e na produção](../deploy/staging-production.md). Para ambientes Starter e Pro, você usa o [!DNL Cloud Console] para enviar código por push entre ambientes.

A Adobe recomenda fazer testes completos no ambiente de preparo antes de enviá-los para o ambiente de produção. Faça alterações de código no ambiente de integração e comece o processo de implantação nos ambientes novamente.

<!-- link definitions -->

[config-multiweb]: https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/multi-sites/ms-overview.html
