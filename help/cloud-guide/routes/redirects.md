---
title: Redirecionamentos
description: Saiba como gerenciar regras de redirecionamento para seu projeto do Adobe Commerce na infraestrutura em nuvem.
feature: Cloud, Routes
exl-id: 7089a790-6341-4443-990a-df42091f0680
source-git-commit: 649c11b111aa9c9105e54908bf9c6f48741f10e4
workflow-type: tm+mt
source-wordcount: '646'
ht-degree: 0%

---

# Redirecionamentos

O gerenciamento de regras de redirecionamento é um requisito comum para aplicações web, especialmente nos casos em que você não deseja perder links recebidos que foram alterados ou removidos ao longo do tempo.

A seguir, é mostrado como gerenciar regras de redirecionamento no Adobe Commerce em projetos de infraestrutura em nuvem usando o `routes.yaml` arquivo de configuração. Se os métodos de redirecionamento discutidos neste tópico não funcionarem para você, você poderá usar cabeçalhos de cache para fazer a mesma coisa.

{{route-placeholder}}

## Atualizações em ambientes Pro

{{pro-self-service-warning}}

>[!WARNING]
>
>Para projetos de infraestrutura em nuvem do Adobe Commerce, configurar vários redirecionamentos e regravações não regex no `routes.yaml` arquivo pode causar problemas de desempenho. Se o seu `routes.yaml` O arquivo tem 32 KB ou mais, descarrega os redirecionamentos não regex e reescreve no Fastly. Consulte [Descarga de redirecionamentos não regex para Fastly em vez de Nginx (rotas)](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/offload-non-regex-redirects-to-fastly-instead-of-nginx-routes.html) no _Centro de ajuda do Adobe Commerce_.

## Redirecionamentos de rota inteira

Usando redirecionamentos de rota completa, você pode definir rotas simples usando o `routes.yaml` arquivo. Por exemplo, é possível redirecionar de um domínio apex para um `www` subdomínio como a seguir:

```yaml
http://{default}/:
    type: redirect
    to: http://www.{default}/
```

## Redirecionamentos de rota parcial

No `.magento/routes.yaml` você pode adicionar regras de redirecionamento parciais a rotas existentes com base na correspondência de padrões:

```yaml
http://{default}/:
    redirects:
        expires: 1d
        paths:
          "/from": { to: "http://example.com/" }
          "/regexp/(.*)/matching": { to: "http://example.com/$1", regexp: true }
```

Redirecionamentos parciais funcionam com qualquer tipo de rota, incluindo rotas servidas diretamente pelo aplicativo.

Duas chaves estão disponíveis em `redirects`:

- **expira em**—Opcional, especifica o tempo para armazenar o redirecionamento em cache no navegador. Exemplos de valores válidos incluem `3600s`, `1d`, `2w`, `3m`.

- **caminhos**—Um ou mais pares de valor-chave que especificam a configuração das regras de redirecionamento de rota parcial.

  Para cada regra de redirecionamento, a chave é uma expressão para filtrar caminhos de solicitação para redirecionamento. O valor é um objeto que especifica o destino do redirecionamento e as opções para o processamento do redirecionamento.

  O objeto de valor tem as seguintes propriedades:

  | Propriedade | Descrição |
  | ---------- | ----------- |
  | `to` | Obrigatório, um caminho absoluto parcial, URL com protocolo e host ou padrão que especifica o destino da regra de redirecionamento. |
  | `regexp` | Opcional, o padrão é `false`. Especifica se a chave de caminho deve ser interpretada como uma expressão regular PCRE. |
  | `prefix` | Especifica se o redirecionamento se aplica ao caminho e a todos os seus filhos ou apenas ao próprio caminho. O padrão é `true`. Este valor não será suportado se `regexp` é `true`. |
  | `append_suffix` | Determina se o sufixo é transportado com o redirecionamento. O padrão é `true`. Esse valor não será suportado se a variável `regexp` a chave é `true` ou* se a variável `prefix` a chave é `false`. |
  | `code` | Especifica o código do status HTTP. Os códigos de status válidos são [`301` (Movido Permanentemente)](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html#sec10.3.2), [`302`](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html#sec10.3.3), [`307`](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html#sec10.3.8), e [`308`](https://www.rfc-editor.org/rfc/rfc7238). O padrão é `302`. |
  | `expires` | Opcional, especifica o tempo para armazenar o redirecionamento em cache no navegador. O padrão é `expires` valor definido diretamente sob o `redirects` chave, mas nesse nível é possível ajustar a expiração do cache para redirecionamentos parciais individuais. |

## Exemplos de redirecionamentos de rota parcial

Os exemplos a seguir mostram como especificar redirecionamentos de rota parcial no `routes.yaml` arquivo usando vários `paths` opções de configuração.

### Correspondência de padrão de expressão regular

Use o formato a seguir para configurar solicitações de redirecionamento com base em uma expressão regular.

```yaml
http://{default}/:
    type: upstream
    redirects:
    paths:
        "/regexp/(.*)/match": { to: "http://example.com/$1", regexp: true }
```

Essa configuração filtra caminhos de solicitações em relação a uma expressão regular e redireciona solicitações correspondentes para `https://example.com`. Por exemplo, uma solicitação para `https://example.com/regexp/a/b/c/match` redireciona para `https://example.com/a/b/c`.

### Correspondência de padrão de prefixo

Use o formato a seguir para configurar solicitações de redirecionamento para caminhos que começam com um padrão de prefixo especificado.

```yaml
http://{default}/:
    type: upstream
    redirects:
    paths:
        "/from": { to: "https://{default}/to", prefix: true }
```

Essa configuração funciona da seguinte maneira:

- Redireciona solicitações que correspondem ao padrão `/from` ao caminho `http://{default}/to`.

- Redireciona solicitações que correspondem ao padrão `/from/another/path` para `https://{default}/to/another/path`.

- Se você alterar a variável `prefix` propriedade para `false`, solicitações que correspondem ao `/from` padrão acionam um redirecionamento, mas as solicitações que correspondem aos `/from/another/path` padrão do não.

### Correspondência de padrão de sufixo

Use o formato a seguir para configurar solicitações de redirecionamento que anexam o sufixo de caminho da solicitação ao destino:

```yaml
http://{default}/:
    type: upstream
    redirects:
    paths: "/from": { to: "https://{default}/to", append_suffix: false }
```

Essa configuração funciona da seguinte maneira:

- Redireciona solicitações que correspondem ao padrão `/from/path/suffix` ao caminho `https://{default}/to`.

- Se você alterar a variável `append_suffix` propriedade para `true`, em seguida, solicitações correspondentes `/from/path/suffix`  redirecionar para o caminho `https://{default}/to/path/suffix`.

### Configuração de cache específica de caminho

Use o formato a seguir para personalizar o tempo de armazenamento em cache de um redirecionamento de um caminho específico:

```yaml
http://{default}/:
    type: upstream
    redirects:
    expires: 1d
    paths:
        "/from": { to: "https://example.com/" }
        "/here": { to: "https://example.com/there", expires: "2w" }
```

Essa configuração funciona da seguinte maneira:

- Redireciona do primeiro caminho (`/from`) são armazenados em cache por um dia.

- Redireciona do segundo caminho (`/here`) são armazenados em cache por duas semanas.
