---
title: VCL personalizado para solicitações de bloqueio
description: Bloqueie solicitações recebidas pelo endereço IP usando uma lista de Controle de Acesso de Borda (ACL) com um trecho de VCL personalizado.
feature: Cloud, Configuration, Security
exl-id: 1f637612-3858-49d0-91f7-9b8823933cc9
source-git-commit: 0e9ace747cc56808108781e42b97c86756089818
workflow-type: tm+mt
source-wordcount: '961'
ht-degree: 0%

---

# VCL personalizado para solicitações de bloqueio

Você pode usar o módulo Fastly CDN para o Magento 2 a fim de criar uma ACL de Borda com uma lista de endereços IP que você deseja bloquear. Em seguida, você pode usar essa lista com um trecho VCL para bloquear solicitações recebidas. O código verifica o endereço IP da solicitação recebida. Se ele corresponder a um endereço IP incluído na lista de ACL, o Fastly bloqueará o acesso ao site e retornará um `403 Forbidden error`. Todos os outros endereços IP de clientes têm acesso permitido.

**Pré-requisitos:**

{{$include /help/_includes/vcl-snippet-prerequisites.md}}

- Lista de endereços IP de clientes a serem bloqueados

## Criar ACL de Borda para bloqueio de endereços IP de clientes

Você cria uma ACL de borda para definir a lista de endereços IP a serem bloqueados. Depois de criar a ACL, você pode usá-la em um trecho de VCL personalizado para gerenciar o acesso ao site de Preparo ou Produção.

Gerencie o acesso para sites de Preparo e Produção criando a ACL de borda com o mesmo nome em ambos os ambientes. O código de trecho VCL se aplica a ambos os ambientes.

1. Faça logon no Administrador.
1. Navegue até **Lojas** > Configurações > **Configuração** > **Avançado** > **Sistema** > **Cache de Página Inteira** > **Configuração do Fastly**.
1. Expanda a **ACL de borda** seção.
1. Clique em **Adicionar ACL** para criar uma lista. Para este exemplo, nomeie a lista &quot;incluir na lista de bloqueios arquivo&quot;.
1. Insira os valores do endereço IP na lista. Todos os endereços IP de cliente adicionados a esta lista estão bloqueados e não podem acessar o site.
1. Opcionalmente, selecione o **Negado** se necessário.

Você faz referência à ACL de borda pelo nome em seu código de trecho de VCL.

## Incluir na lista de bloqueios Criar o VCL personalizado para o arquivo de pesquisa

>[!NOTE]
>
>Este exemplo mostra aos usuários avançados como criar um trecho de código VCL para configurar regras de bloqueio personalizadas para fazer upload no serviço Fastly. Você pode configurar uma incluir na lista de bloqueios inclui na lista de permissões ou com base no país do Administrador da Adobe Commerce usando o menu [Bloqueio](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/BLOCKING.md) recurso disponível no módulo Fastly CDN para Magento 2.

Depois de definir a ACL de borda, você pode usá-la para criar o trecho VCL para bloquear o acesso aos endereços IP especificados na ACL. Você pode usar o mesmo trecho de VCL em ambientes de Preparo e Produção, mas deve fazer upload do trecho para cada ambiente separadamente.

O seguinte código de trecho de VCL personalizado (formato JSON) mostra a lógica para bloquear solicitações recebidas com um endereço IP de cliente que corresponda a um endereço na ACL de inclui na lista de bloqueios.

```json
{
  "name": "blocklist",
  "dynamic": "0",
  "type": "recv",
  "priority": "5",
  "content": "if ( client.ip ~ blocklist) { error 403 \"Forbidden\"; }"
}
```

Antes de criar um trecho com base neste exemplo, revise os valores para determinar se você precisa fazer alterações:

- `name`: Nome do trecho VCL. Neste exemplo, usamos o nome `blocklist`.

- `priority`: determina quando o trecho VCL é executado. A prioridade é `5` para executar imediatamente e verificar se uma solicitação de administrador vem de um endereço IP permitido. O trecho é executado antes de qualquer um dos trechos de VCL de Magento padrão (`magentomodule_*`) atribuíram uma prioridade de 50. Defina a prioridade para cada trecho personalizado acima ou abaixo de 50, dependendo de quando você deseja que seu trecho seja executado. Os trechos com números de prioridade mais baixa são executados primeiro.

- `type`: Especifica o tipo de trecho de VCL que determina o local do trecho no código de VCL gerado. Neste exemplo, usamos `recv`, que insere o código VCL no `vcl_recv` sub-rotina, abaixo do VCL em chapa e acima de quaisquer objetos. Consulte a [Referência de trecho do Fastly VCL](https://docs.fastly.com/api/config#api-section-snippet) para obter a lista de tipos de snippet.

- `content`: o trecho de código VCL a ser executado, que verifica o endereço IP do cliente. Se o IP estiver na ACL de borda, ele será bloqueado para acesso com um `403 Forbidden` erro para todo o site. Todos os outros endereços IP de clientes têm acesso permitido.

Depois de revisar e atualizar o código do seu ambiente, use um dos métodos a seguir para adicionar o trecho de VCL personalizado à configuração do serviço Fastly:

- [Adicionar o trecho de VCL personalizado do Administrador](#add-the-custom-vcl-snippet). Esse método é recomendado se você puder acessar o Administrador. (Exige [Versão 1.2.58 do Fastly](fastly-configuration.md#upgrade-fastly-module) ou posteriormente.)

- Salve o exemplo de código JSON em um arquivo (por exemplo, `blocklist.json`) e [fazer upload usando a API Fastly](fastly-vcl-custom-snippets.md#manage-custom-vcl-snippets-using-the-api). Use esse método se não conseguir acessar o Administrador.

## Adicionar o trecho de VCL personalizado

{{admin-login-step}}

1. Clique em **Lojas** > Configurações > **Configuração** > **Avançado** > **Sistema**.

1. Expandir **Cache de Página Inteira** > **Configuração do Fastly** > **Trechos de VCL Personalizados**.

1. Clique em **Criar trecho personalizado**.

1. Adicione os valores do trecho de VCL:

   - **Nome** — `blocklist`

   - **Tipo** — `recv`

   - **Prioridade** — `5`

   - Adicione o **VCL** conteúdo do trecho:

     ```conf
     if ( client.ip ~ blocklist) { error 403 "Forbidden"; }
     ```

1. Clique em **Criar** para gerar o arquivo de trecho VCL com o padrão de nome `type_priority_name.vcl`, por exemplo `recv_5_blocklist.vcl`

1. Depois que a página for recarregada, clique em **Carregar VCL para Fastly** no *Configuração do Fastly* para adicionar o arquivo à configuração do serviço Fastly.

1. Após os uploads, atualize o cache de acordo com a notificação na parte superior da página.

O Fastly valida a versão atualizada do código do VCL durante o processo de upload. Se a validação falhar, edite o trecho de VCL personalizado para corrigir o problema. Em seguida, carregue o VCL novamente.

## Exemplos adicionais de VCL para solicitações de bloqueio

Os exemplos a seguir mostram como bloquear solicitações usando instruções condition em vez de uma lista ACL.

>[!WARNING]
>
>Nesses exemplos, o código do VCL é formatado como uma carga JSON que pode ser salva em um arquivo e enviada em uma solicitação da API Fastly. Você pode enviar o [Trecho VCL do Administrador](#add-the-custom-vcl-snippet)ou como uma sequência de caracteres JSON usando a API Fastly. Para impedir a validação ao usar a API Fastly com uma cadeia de caracteres JSON, você deve usar uma barra invertida para escapar caracteres especiais.

Consulte [Uso de trechos de VCL dinâmicos](https://docs.fastly.com/vcl/vcl-snippets/) na documentação do Fastly VCL.

### Amostra de código VCL: Bloco por código de país

Este exemplo usa o código de país ISO 3166-1 de dois caracteres para o país associado ao endereço IP.

```json
{
  "name": "blockbycountrycode",
  "dynamic": "0",
  "type": "recv",
  "priority": "5",
  "content": "if ( client.geo.country_code == \"HK\" ) { error 405 \"Not allowed\";}"
}
```

>[!NOTE]
>
>Em vez de usar um trecho de VCL personalizado, você pode usar o Fastly [Bloqueio](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/BLOCKING.md) recurso no Administrador do Adobe Commerce na infraestrutura em nuvem para configurar o bloqueio por código do país ou uma lista de códigos do país.

### Amostra de código VCL: cabeçalho de solicitação Bloquear por Agente do Usuário HTTP

```json
{
  "name": "blockbyuseragent",
  "dynamic": "0",
  "type": "recv",
  "priority": "5",
  "content": "if ( req.http.User-Agent ~ \"(UCBrowser|MQQBrowser|LieBaoFast|Mb2345Browser)\" ) {error 405 \"Not allowed\";}"
}
```

{{automate-vcl-snippet-deployment}}

{{$include /help/_includes/vcl-snippet-modify.md}}

{{$include /help/_includes/vcl-snippet-delete.md}}
