---
title: VCL personalizado para permitir solicitações
description: Filtre solicitações recebidas e permita o acesso por endereço IP para sites do Adobe Commerce com uma lista ACL do Fastly Edge e um trecho de VCL personalizado.
feature: Cloud, Configuration, Security
exl-id: a6ee958a-c3d3-47be-b2df-510707f551fc
source-git-commit: 13e76d3e9829155995acbb72d947be3041579298
workflow-type: tm+mt
source-wordcount: '848'
ht-degree: 0%

---

# VCL personalizado para permitir solicitações

Você pode usar uma lista ACL de borda do Fastly com um trecho de código VCL personalizado para filtrar solicitações recebidas e permitir o acesso pelo endereço IP. A lista de ACL especifica os endereços IP permitidos.

Crie um incluo na lista de permissões de atualização para limitar o acesso ao ambiente de preparo, de modo que somente as solicitações de endereços IP especificados para desenvolvedores internos e serviços externos aprovados sejam permitidos. Você também pode criar uma inclui na lista de permissões para proteger o acesso do Administrador aos ambientes de Preparo e Produção.

O exemplo a seguir mostra como usar um trecho de VCL personalizado com um [Lista de controle de acesso (ACL) do Fastly](https://docs.fastly.com/guides/access-control-lists/about-acls) para proteger o acesso do Administrador a um ambiente de projeto do Adobe Commerce na infraestrutura em nuvem. Quando você adiciona o trecho VCL personalizado ao ambiente na nuvem, o Fastly permite somente solicitações de endereços IP incluídos na ACL.

>[!TIP]
>
>Para ambientes de preparo e integração que não devem estar acessíveis publicamente, use a opção Controle de acesso HTTP disponível na [[!DNL Cloud Console]](../project/overview.md#access-the-project-web-interface) para gerenciar o acesso a todo o site por endereço IP.

**Pré-requisitos:**


{{$include /help/_includes/vcl-snippet-prerequisites.md}}

- Lista de endereços IP de clientes a serem incluídos no arquivo de inclui na lista de permissões

## Criar ACL de Borda para permitir endereços IP de clientes

As ACLs de borda criam listas de endereços IP para gerenciar o acesso ao seu site. Neste exemplo, você cria uma ACL de borda e adiciona a lista de endereços IP de clientes permitidos para acessar o administrador do ambiente do seu projeto.

{{admin-login-step}}

1. Clique em **Lojas** > Configurações > **Configuração** > **Avançado** > **Sistema**.

1. Expandir **Cache de Página Inteira** > **Configuração do Fastly** > **ACL de borda**.

1. Crie o contêiner de ACL:

   - Clique em **Adicionar ACL**.

   - No *Contêiner de ACL* insira um **Nome da ACL**—`allowlist`.

   - Selecionar **Ativar após a alteração** para implantar as alterações na versão da configuração do serviço Fastly que está editando.

   - Clique em **Carregar** para anexar a ACL à configuração do serviço Fastly.

1. Adicione a lista de endereços IP permitidos para acessar o Administrador:

   - Clique no ícone Configurações para a `allowlist` ACL.

   - Adicione e salve a variável *Valor de IP* para cada endereço IP do cliente.

   - Clique em **Cancelar** para retornar à página de configuração do sistema.

1. Clique em **Salvar configuração**.

1. Atualize o cache de acordo com a notificação na parte superior da página.

## Criar o trecho de VCL personalizado para proteger o acesso de Administrador

O seguinte código de trecho de VCL personalizado (formato JSON) mostra a lógica para filtrar solicitações para o Administrador e permitir acesso se o endereço IP do cliente corresponder a um endereço na `allowlist` ACL.

```json
{
  "name": "allowlist",
  "dynamic": "0",
  "type": "recv",
  "priority": "5",
  "content": "if ((req.url ~ \"^/admin\") && !(client.ip ~ allowlist) && !req.http.Fastly-FF) { error 403 \"Forbidden\"; }"
}
```

Antes [criação de um trecho personalizado](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/cdn/custom-vcl-snippets/fastly-vcl-allowlist.html#add-the-custom-vcl-snippet) a partir deste exemplo, revise os valores para determinar se você precisa fazer alterações. Em seguida, insira cada valor nos respectivos campos, como `type` no campo Tipo, `content` no campo Conteúdo.

- `name` — Nome do trecho VCL. Neste exemplo, `allowlist`.

- `priority` — Determina quando o trecho VCL é executado. A prioridade é `5` para executar imediatamente e verificar se uma solicitação de administrador vem de um endereço IP permitido. O trecho é executado antes de qualquer um dos trechos de VCL de Magento padrão (`magentomodule_*`) atribuíram uma prioridade de 50. Defina a prioridade para cada trecho personalizado acima ou abaixo de 50, dependendo de quando você deseja que seu trecho seja executado. Os trechos com números de prioridade mais baixa são executados primeiro.

- `type` — Especifica um local para inserir o trecho no código de VCL com versão. Este VCL é um `recv` tipo de trecho que adiciona o código do trecho à `vcl_recv` subrotina abaixo do código padrão do Fastly VCL e acima de qualquer objeto.

- `content` — O trecho de código VCL a ser executado. Neste exemplo, o código filtra solicitações para o Administrador e permite acesso se o endereço IP do cliente corresponder a um endereço no `allowlist` ACL. Se o endereço não corresponder, a solicitação será bloqueada com um `403 Forbidden` erro.

  Se o URL do seu administrador tiver sido alterado, substitua o valor de exemplo `/admin` com o URL do seu ambiente. Por exemplo, `/company-admin`.

Na amostra de código, a condição `!req.http.Fastly-FF` é importante ao usar [Blindagem de origem](fastly-custom-cache-configuration.md#configure-back-ends-and-origin-shielding). Não remova nem edite esse código.

Depois de revisar e atualizar o código do seu ambiente, use um dos métodos a seguir para adicionar o trecho de VCL personalizado à configuração do serviço Fastly:

- [Adicionar o trecho de VCL personalizado do Administrador](#add-the-custom-vcl-snippet). Esse método é recomendado se você puder acessar o Administrador. (Exige [Módulo Fastly CDN para o Magento 2 versão 1.2.58](fastly-configuration.md#upgrade) ou posteriormente.)

- Salve o exemplo de código JSON em um arquivo (por exemplo, `allowlist.json`) e [fazer upload usando a API Fastly](fastly-vcl-custom-snippets.md#manage-custom-vcl-snippets-using-the-api). Use esse método se não conseguir acessar o Administrador.

## Adicionar o trecho de VCL personalizado

{{admin-login-step}}

1. Clique em **Lojas** > Configurações > **Configuração** > **Avançado** > **Sistema**.

1. Expandir **Cache de Página Inteira** > **Configuração do Fastly** > **Trechos de VCL Personalizados**.

1. Clique em **Criar trecho personalizado**.

1. Adicione os valores do trecho de VCL:

   - **Nome** — `allowlist`

   - **Tipo** — `recv`

   - **Prioridade** — `5`

   - Adicione o **VCL** conteúdo do trecho:

     ```conf
     if ((req.url ~ "^/admin") && !(client.ip ~ allowlist) && !req.http.Fastly-FF) { error 403 "Forbidden";}
     ```

1. Clique em **Criar** para gerar o arquivo de trecho VCL com o padrão de nome `type_priority_name.vcl`, por exemplo `recv_5_allowlist.vcl`

1. Depois que a página for recarregada, clique em **Carregar VCL para Fastly** no *Configuração do Fastly* para adicionar o arquivo à configuração do serviço Fastly.

1. Depois que o upload for concluído, atualize o cache de acordo com a notificação na parte superior da página.

O Fastly valida a versão atualizada do código do VCL durante o processo de upload. Se a validação falhar, edite o trecho de VCL personalizado para corrigir o problema. Em seguida, carregue o VCL novamente.

{{$include /help/_includes/vcl-snippet-modify.md}}

{{$include /help/_includes/vcl-snippet-delete.md}}
