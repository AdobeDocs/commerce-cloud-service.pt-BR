---
title: Conexões seguras
description: Saiba como aplicar chaves SSH ao projeto Adobe Commerce na infraestrutura em nuvem e fazer logon em ambientes remotos.
role: Developer
feature: Cloud, Security
topic: Security
exl-id: b5780e8e-e3da-4b10-8ca3-2778085acd4a
source-git-commit: 13e76d3e9829155995acbb72d947be3041579298
workflow-type: tm+mt
source-wordcount: '976'
ht-degree: 0%

---

# Conexões seguras com ambientes remotos

O Secure Shell (SSH) é um protocolo comum usado para fazer logon com segurança em servidores e sistemas remotos. Você pode usar o SSH para acessar seus ambientes remotos para gerenciar o aplicativo do Adobe Commerce e acessar logs de ambientes remotos. O Adobe só oferece suporte a conexões FTP seguras (sFTP) usando sua chave pública SSH. Conexões FTP não são suportadas.

## Gerar um par de chaves SSH

Crie um par de chaves SSH em cada máquina e espaço de trabalho que exija acesso ao código-fonte e aos ambientes do projeto. A chave SSH permite que você se conecte ao GitHub para gerenciar o código-fonte e se conectar aos servidores da nuvem sem precisar fornecer constantemente seu nome de usuário e senha. Consulte [Conexão com o GitHub com SSH](https://docs.github.com/en/authentication/connecting-to-github-with-ssh) para obter mais instruções sobre como criar um par de chaves SSH.

- A variável _chave pública_ O é seguro para fornecer acesso a um site, SSH e sFTP.
- A variável _chave privada_ permanece privado na estação de trabalho.

>[!CAUTION]
>
>**Nunca compartilhe sua chave privada.** Não adicione-o a um tíquete, copie-o em um bate-papo ou anexe-o a emails.

## Adicionar uma chave pública SSH à sua conta

Depois de adicionar sua chave pública SSH à conta do Adobe Commerce na infraestrutura em nuvem, reimplante todos os ambientes ativos em sua conta para instalar a chave.

Você pode adicionar chaves SSH à sua conta usando um dos seguintes métodos: Cloud CLI ou [!DNL Cloud Console].

>[!BEGINTABS]

>[!TAB CLI]

### Adicione sua chave SSH usando a CLI da nuvem

1. Na estação de trabalho local, altere para o diretório do projeto.

1. Faça logon no projeto:

   ```bash
   magento-cloud login
   ```

1. Adicione a chave pública.

   ```bash
   magento-cloud ssh-key:add ~/.ssh/id_rsa.pub
   ```

>[!TIP]
>
>Você pode listar e excluir chaves SSH usando os comandos da CLI da nuvem `ssh-key:list` e `ssh-key:delete`.

>[!TAB Console]

### Adicione sua chave SSH usando o [!DNL Cloud Console]

**Para adicionar uma chave SSH a um novo projeto**:

1. Faça logon no [[!DNL Cloud Console]](https://console.adobecommerce.com).

1. Clique em **[!UICONTROL No SSH key]**. Esse ícone fica à direita do campo de comando e é visível quando o projeto não contém uma chave SSH.

1. Copie e cole o conteúdo da sua chave SSH pública no **Chave pública** campo.

1. Siga os prompts restantes.

**Para adicionar uma chave SSH ao seu perfil na nuvem**:

1. Faça logon no [[!DNL Cloud Console]](https://console.adobecommerce.com).

1. No menu de conta superior direito, clique em **Meu perfil**.

1. No _Chaves SSH_ clique em **Adicionar chave pública**.

1. No _Adicionar uma chave SSH_ formulário, dê à sua chave um **Título** e cole a chave SSH pública no **Chave** campo.

1. Clique em **Salvar**.

>[!ENDTABS]

## Conectar-se a um ambiente remoto

Você pode se conectar a um ambiente remoto usando o `magento-cloud` CLI ou um comando SSH. A variável `magento-cloud` Os comandos da CLI só podem ser usados em ambientes de integração Starter e Pro.

### Usar a CLI da nuvem

**Para fazer logon em um ambiente de integração remota**:

1. Na estação de trabalho local, altere para o diretório do projeto.

1. Listar os ambientes nesse projeto.

   ```bash
   magento-cloud environment:list -p <project-ID>
   ```

1. Use o SSH para fazer logon no ambiente remoto.

   ```bash
   magento-cloud ssh -p <project-ID> -e <environment-ID>
   ```

### Usar um comando SSH

A variável [!DNL Cloud Console] inclui uma lista de comandos de acesso à Web e SSH para cada ambiente.

**Para copiar o comando SSH**:

1. Faça logon no [[!DNL Cloud Console]](https://console.adobecommerce.com).

1. Selecione um projeto na lista _Todos os projetos_ lista.

1. Selecione um ambiente.

1. Clique em **[!UICONTROL SSH]**.

1. No _SSH_ clique no botão copiar para copiar o comando SSH completo para a área de transferência.

1. Abra um terminal e cole o comando SSH para criar uma conexão.

   ```bash
   ssh abcdefg123abc-branch-a12b34c--mymagento@ssh.us-2.magento.cloud
   ```

>[!TIP]
>
>Para ambientes de preparo e produção Pro, o comando SSH pode ser semelhante a:
>
>```bash
>ssh <node>.ent-<project-ID>-<environment>-<user-ID>@ssh.<region>.magento.com
>```

## sFTP

A infraestrutura do Adobe Commerce na nuvem é compatível com o acesso a seus ambientes usando sFTP (FTP seguro) com autenticação SSH. Use um cliente compatível com autenticação de chave SSH para sFTP e use sua chave SSH pública. Sua chave SSH pública deve ser adicionada ao ambiente de destino. Para ambientes iniciais e de integração Pro, você pode [adicione-o por meio da variável [!DNL Cloud Console]](#add-your-ssh-key-using-the-project-web-interface).

As conexões sFTP somente leitura são _não_ compatível; o acesso sFTP é fornecido com _gravação_ permissão por padrão.

Ao configurar o sFTP, use as informações do comando do ambiente de acesso SSH: `<project-id>-<environment-id>--<app-name>@ssh<cloud-host>`

- **Nome de usuário**: Todo o conteúdo antes do `@` no destino de acesso SSH.
- **Senha**: Não é necessário ter uma senha para sFTP. O acesso sFTP usa a autenticação de chave SSH.
- **Host**: Todo o conteúdo depois de `@` no seu acesso SSH.
- **Porta**: 22, que é a porta SSH padrão.
- **SSH** Chave privada: se necessário, forneça a localização da sua chave privada para o cliente sFTP. Por padrão, as chaves privadas são armazenadas no `~/.ssh` diretório.

Dependendo do cliente, opções adicionais podem ser necessárias para concluir a autenticação SSH para sFTP. Revise a documentação do cliente selecionado.

Para **Ambientes iniciais e ambientes de integração Pro**, você também pode considerar [adicionar um `mount`](../application/properties.md#mounts) para obter acesso a um diretório específico. Você adicionaria a montagem ao seu `.magento.app.yaml` arquivo. Para obter uma lista de diretórios graváveis, consulte [Estrutura de projeto](../project/file-structure.md). Esse ponto de montagem só funciona nesses ambientes.

Para **Ambientes profissionais de preparo e produção**, se você não tiver acesso SSH ao ambiente, deverá [enviar um tíquete de suporte da Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) para solicitar acesso ao sFTP e um ponto de montagem para acessar a pasta específica, por exemplo, `pub/media`.

>[!NOTE]
>Para Preparo e produção profissionais, se a conexão sFTP for para um _genérico_ usuário que faz **não** precisa ser [adicionado ao projeto na nuvem](../project/user-access.md), você deve [enviar um tíquete de suporte da Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) com o seu **público** chave anexada. **Nunca forneça sua chave SSH privada.**

## Tunelamento SSH

Você pode usar o tunelamento SSH para se conectar a um serviço do ambiente de desenvolvimento local como se o serviço fosse local. Antes do encapsulamento, configure o [SSH](#add-an-ssh-public-key-to-your-account).

Use um aplicativo de terminal para fazer logon e emitir comandos.

```bash
magento-cloud login
```

Verifique se algum túnel está aberto usando.

```bash
magento-cloud tunnel:list
```

Para construir um túnel, você deve conhecer a [nome do aplicativo](../application/properties.md#name). Você pode verificar o nome do aplicativo usando a CLI:

```bash
magento-cloud apps
```

### Configurar o túnel SSH

```bash
magento-cloud tunnel:open -e <environment-ID> --app <app-name>
```

Por exemplo, para abrir um túnel para a `sprint5` em um projeto com um aplicativo chamado `mymagento`, insira

```bash
magento-cloud tunnel:open -e sprint5 --app mymagento
```

Exemplo de resposta:

```terminal
SSH tunnel opened on port 30004 to relationship: redis
SSH tunnel opened on port 30005 to relationship: database
Logs are written to: /home/magento_user/.magento/tunnels.log

List tunnels with: magento-cloud tunnels
View tunnel details with: magento-cloud tunnel:info
Close tunnels with: magento-cloud tunnel:close
```

**Para exibir informações sobre o túnel**:

```bash
magento-cloud tunnel:info -e <environment-ID>
```

### Conectar-se a serviços

Depois de estabelecer um túnel SSH, você pode se conectar a serviços como se estivessem sendo executados localmente. Por exemplo, para se conectar ao banco de dados, use o seguinte comando:

```bash
mysql --host=127.0.0.1 --user='<database-username>' --pass='<user-password>' --database='<name>' --port='<port>'
```
