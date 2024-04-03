---
title: Adicionar mapa do site e robôs de mecanismo de pesquisa
description: Saiba como adicionar o mapa do site e os robôs do mecanismo de pesquisa ao Adobe Commerce na infraestrutura em nuvem.
feature: Cloud, Configuration, Search, Site Navigation
exl-id: b98f43fa-1878-466d-8ea0-1e7207af8b60
source-git-commit: ee1db75c73c086e0ea54e1a7591ca7f2b4d2b36d
workflow-type: tm+mt
source-wordcount: '517'
ht-degree: 0%

---

# Adicionar mapa do site e robôs de mecanismo de pesquisa

Uma tentativa de gerar e gravar a variável `sitemap.xml` ao diretório raiz resulta no seguinte erro:

```terminal
Please make sure that "/" is writable by the web-server.
```

Com o Adobe Commerce na infraestrutura em nuvem, você só pode gravar em diretórios específicos, como `var`, `pub/media`, `pub/static`ou `app/etc`. Ao gerar a variável `sitemap.xml` usando o painel Admin, você deve especificar o `/media/` caminho.

Não é necessário gerar um `robots.txt` arquivo porque gera a variável `robots.txt` conteúdo sob demanda e o armazena no banco de dados. Você pode exibir o conteúdo no seu navegador com o `<domain.your.project>/robots.txt` ou `<domain.your.project>/robots` link.

Isso requer o ECE-Tools versão 2002.0.12 e posterior com uma atualização `.magento.app.yaml` arquivo. Veja um exemplo dessas regras na [repositório da magento-cloud](https://github.com/magento/magento-cloud/blob/master/.magento.app.yaml#L43-L49).

**Para gerar uma `sitemap.xml` arquivo na versão 2.2 e posterior**:

1. Acesse o Admin.
1. No _Marketing_ clique em **Mapa do site** no _SEO e pesquisa_ seção.
1. No _Mapa do site_ clique em **Adicionar mapa do site**.
1. No _Novo mapa de sites_ digite os seguintes valores:

   - **Nome do arquivo**:`sitemap.xml`
   - **Caminho**:`/media/`

1. Clique em **Salvar e gerar**. O novo mapa do site fica disponível no _Mapa do site_ grade.
1. Clique no caminho no campo _Link para o Google_ coluna.

**Para adicionar conteúdo à `robots.txt` arquivo**:

1. Acesse o Admin.
1. No _Conteúdo_ clique em **Configuração** no _Design_ seção.
1. No _Configuração de design_ clique em **Editar** para o site na _Ação_ coluna.
1. No _Site principal_ clique em **Robôs do mecanismo de pesquisa**.
1. Atualize o **Editar instrução personalizada de robots.txt** campo.
1. Clique em **Salvar configuração**.
1. Verifique se `<domain.your.project>/robots.txt` arquivo ou `<domain.your.project>/robots` URL no seu navegador.

>[!NOTE]
>
>Se a variável `<domain.your.project>/robots.txt` arquivo gera um `404 error`, [Enviar um tíquete de suporte da Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) para remover o redirecionamento de `/robots.txt` para `/media/robots.txt`.

## Regravar usando o trecho Fastly VCL

Se você tiver domínios diferentes e precisar de mapas de site separados, poderá criar uma VCL para rotear para o mapa de site apropriado. Gerar o `sitemap.xml` no painel Admin, conforme descrito acima, crie um trecho Fastly VCL personalizado para gerenciar o redirecionamento. Consulte [Trechos de VCL Fastly personalizados](../cdn/fastly-vcl-custom-snippets.md).

>[!NOTE]
>
> Você pode fazer upload de trechos de VCL personalizados na interface do usuário do Administrador ou usando a API do Fastly. Consulte [Exemplos e tutoriais de trechos de VCL personalizados](../cdn/fastly-vcl-custom-snippets.md#example-vcl-snippet-code).

### Use um trecho Fastly VCL para redirecionar

Criar um trecho de VCL personalizado para substituir o caminho por `sitemap.xml` para `/media/sitemap.xml` usando o `type` e `content` pares de valor-chave.

```json
{
  "name": "sitemapxml_rewrite",
  "dynamic": "0",
  "type": "recv",
  "priority": "90",
  "content": "if ( req.url.path ~ \"^/?sitemap.xml$\" ) { set req.url = \"/media/sitemap.xml\"; }"
}
```

O exemplo a seguir demonstra como reescrever o caminho para `robots.txt` e `sitemap.xml` para `/media/robots.txt` e `/media/sitemap.xml`

```json
{
  "name": "sitemaprobots_rewrite",
  "dynamic": "0",
  "type": "recv",
  "priority": "90",
  "content": "if ( req.url.path ~ \"^/?sitemap.xml$\" ) { set req.url = \"/media/sitemap.xml\"; } else if (req.url.path ~ \"^/?robots.txt$\") { set req.url = \"/media/robots.txt\";}"
}
```

**Para usar um trecho de VCL do Fastly para um redirecionamento de domínio específico**:

Criar um `pub/media/domain_robots.txt` arquivo, onde o domínio é `domain.com`e use o próximo trecho VCL:

```json
{
  "name": "domain_robots",
  "dynamic": "0",
  "type": "recv",
  "priority": "90",
  "content": "if ( req.url.path == \"/robots.txt\" ) { if ( req.http.host ~ \"(domain).com$\" ) { set req.url = \"/media/\" re.group.1 \"_robots.txt\"; }}"
}
```

As rotas de trecho do VCL `http://domain.com/robots.txt` e apresenta o `pub/media/domain_robots.txt` arquivo.

Para configurar um redirecionamento para `robots.txt` e `sitemap.xml` em um único trecho, crie `pub/media/domain_robots.txt` e `pub/media/domain_sitemap.xml` arquivos, onde o domínio é `domain.com` e use o próximo trecho VCL:

```json
{
  "name": "domain_sitemaprobots",
  "dynamic": "0",
  "type": "recv",
  "priority": "90",
  "content": "if ( req.url.path == \"/robots.txt\" ) { if ( req.http.host ~ \"(domain).com$\" ) { set req.url = \"/media/\" re.group.1 \"_robots.txt\"; }} else if ( req.url.path == \"/sitemap.xml\" ) { if ( req.http.host ~ \"(domain).com$\" ) {  set req.url = \"/media/\" re.group.1 \"_sitemap.xml\"; }}"
}
```

No `sitemap` admin config, você deve especificar o local do arquivo usando `pub/media/` em vez de `/`.

### Configurar indexação por mecanismo de pesquisa

Para ativar `robots.txt` personalizações, você deve ativar o **A indexação por mecanismos de pesquisa está Ativada para`<environment-name>`** nas configurações do projeto.

![Use o [!DNL Cloud Console] para gerenciar ambientes](../../assets/robots-indexing-by-search-engine.png)

>[!NOTE]
>
>Se você estiver usando o PWA Studio e não conseguir acessar o sistema `robots.txt` arquivo, adicionar `robots.txt` para o [Nome da frente ➡ Incluir na lista de permissões](https://github.com/magento/magento2-upward-connector#front-name-allowlist) em **Lojas** > Configuração > **Geral** > **Web** > Configuração de PWA ASCENDENTE.
