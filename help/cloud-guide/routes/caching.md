---
title: Armazenamento em cache
description: Saiba como habilitar o armazenamento em cache de seu Adobe Commerce em ambientes de infraestrutura em nuvem.
feature: Cloud, Cache, Routes
exl-id: 4856aa94-2947-4dc8-b0d1-0960869dc39c
source-git-commit: 7b9c6a4cd17069c25455195bd8f273664b8a29eb
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 0%

---

# Armazenamento em cache

Você pode ativar o armazenamento em cache no ambiente do projeto de infraestrutura em nuvem. Se você desativar o armazenamento em cache, o Adobe Commerce fornecerá os arquivos diretamente.

{{route-placeholder}}

## Configurar armazenamento em cache

Ative o armazenamento em cache para sua aplicação configurando as regras de cache na `.magento/routes.yaml` do seguinte modo:

```yaml
http://{default}/:
    type: upstream
    upstream: php:php
    cache:
        enabled: true
        headers: [ "Accept", "Accept-Language", "X-Language-Locale" ]
        cookies: ["*"]
        default_ttl: 60
```

## Armazenamento em cache com base em rotas

Habilite o cache refinado configurando regras de cache para várias rotas separadamente, como mostra o exemplo a seguir:

```yaml
http://{default}/:
    type: upstream
    upstream: php:php
    cache:
        enabled: true

http://{default}/path/:
    type: upstream
    upstream: php:php
    cache:
        enabled: false

http://{default}/path/more/:
    type: upstream
    upstream: php:php
    cache:
        enabled: true
```

O exemplo anterior armazena em cache as seguintes rotas:

- `http://{default}/`
- `http://{default}/path/more/`
- `http://{default}/path/more/etc/`

E as seguintes rotas são **não** em cache:

- `http://{default}/path/`
- `http://{default}/path/etc/`

>[!NOTE]
>
>As expressões regulares em rotas são **não** compatível.

## Duração do cache

A duração do cache é determinada pelo parâmetro `Cache-Control` valor do cabeçalho de resposta. Se não `Cache-Control` estiver na resposta, o cabeçalho `default_ttl` é usada.

## Chave do cache

Para decidir como armazenar uma resposta em cache, o Adobe Commerce cria uma chave de cache que depende de vários fatores e armazena a resposta associada a essa chave. Quando uma solicitação vem com a mesma chave de cache, a resposta é reutilizada. Sua finalidade é semelhante ao HTTP [`Vary` cabeçalho](https://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.44).

Os parâmetros `headers` e `cookies` As chaves permitem alterar essa chave do cache.

O valor padrão para essas chaves é o seguinte:

```yaml
cache:
    enabled: true
    headers: ["Accept-Language", "Accept"]
    cookies: ["*"]
```

## Atributos de cache

### `enabled`

Quando definido como `true`, habilite o cache para esta rota. Quando definido como `false`, desabilite o cache para esta rota.

### `headers`

Define de quais valores a chave do cache deve depender.

Por exemplo, se a variável `headers` a chave é a seguinte:

```yaml
cache:
    enabled: true
    headers: ["Accept"]
```

Em seguida, o Adobe Commerce armazena em cache uma resposta diferente para cada valor do `Accept` cabeçalho HTTP.

### `cookies`

A variável `cookies` A chave define de quais valores a chave de cache deve depender.

Por exemplo:

```yaml
cache:
    enabled: true
    cookies: ["value"]
```

A chave do cache depende do valor da variável `value` cookie na solicitação.

Existe um caso especial se a `cookies` a chave tem o `["*"]` valor. Esse valor significa que qualquer solicitação com um cookie ignora o cache. Este é o valor padrão.

>[!NOTE]
>
>Não é possível usar curingas no nome do cookie. Use um nome de cookie preciso ou corresponda a todos os cookies com um asterisco (`*`). Por exemplo, `SESS*` ou `~SESS` estão atualmente **não** valores válidos.

Os cookies têm as seguintes restrições:

- É possível definir o máximo de **50 cookies** no sistema. Caso contrário, o aplicativo lança um `Unable to send the cookie. Maximum number of cookies would be exceeded` exceção.
- Um tamanho máximo de cookie é **4.096 bytes**. Caso contrário, o aplicativo lança um `Unable to send the cookie. Size of '%name' is %size bytes` exceção.

### `default_ttl`

Se a resposta não tiver um `Cache-Control` cabeçalho, a variável `default_ttl` A chave é usada para definir a duração do cache, em segundos. O valor padrão é `0`, o que significa que nada é armazenado em cache.
