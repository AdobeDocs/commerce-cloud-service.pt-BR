---
title: Configurar [!DNL Xdebug]
description: Saiba como configurar a extensão Xdebug para depurar o desenvolvimento de projetos do Adobe Commerce na infraestrutura em nuvem.
exl-id: bf2d32d8-fab7-439e-8df3-b039e53009d4
source-git-commit: 751456f50e7b017b47c2ff43e008c2d04a558d96
workflow-type: tm+mt
source-wordcount: '1747'
ht-degree: 0%

---

# Configurar Xdebug

[!DNL Xdebug] é uma extensão para depurar seu PHP. Embora você possa usar um IDE de sua escolha, o seguinte explica como configurar [!DNL Xdebug] e [!DNL PhpStorm] para depurar no ambiente local.

>[!NOTE]
>
>Você pode configurar [!DNL Xdebug] para ser executado no ambiente do Cloud Docker para depuração local sem alterar a configuração do projeto do Adobe Commerce na infraestrutura em nuvem. Consulte [Configurar Xdebug para Docker](https://developer.adobe.com/commerce/cloud-tools/docker/test/configure-xdebug/).

Para habilitar [!DNL Xdebug], você deve configurar um arquivo no repositório Git, configurar o IDE e configurar o encaminhamento de portas. É possível definir algumas configurações no `magento.app.yaml` arquivo. Após a edição, insira as alterações do Git em todos os ambientes de inicialização e integração Pro para habilitar [!DNL Xdebug]. [!DNL Xdebug] O já está disponível em ambientes de preparo e produção profissionais.

Depois de configurado, você pode depurar comandos CLI, solicitações da Web e código. Lembre-se de que todos os ambientes de infraestrutura em nuvem são somente leitura. Clonar o código no ambiente de desenvolvimento local para executar a depuração. Para ambientes de preparo e produção profissionais, consulte [instruções adicionais](#debug-for-pro-staging-and-production) para [!DNL Xdebug].

## Requisitos

Para executar e usar o [!DNL Xdebug], é necessário o URL SSH para o ambiente. Você pode localizar as informações por meio da [[!DNL Cloud Console]](../project/overview.md) ou seu [!DNL Cloud Onboarding UI].

## Configurar Xdebug

Para configurar [!DNL Xdebug], siga estas etapas:

- [Trabalhe em uma ramificação para enviar atualizações de arquivo](#get-started-with-a-branch)
- [Ativar [!DNL Xdebug] para ambientes](#enable-xdebug-in-your-environment)
- [Configurar o IDE](#configure-phpstorm)
- [Configurar encaminhamento de porta](#set-up-port-forwarding)

### Introdução a uma ramificação

Para adicionar [!DNL Xdebug], o Adobe recomenda trabalhar em [uma ramificação de desenvolvimento](../dev-tools/cloud-cli-overview.md#create-an-environment-branch).

### Ativar o Xdebug no seu ambiente

Você pode ativar [!DNL Xdebug] diretamente para todos os ambientes de Início e integração Pro. Essa etapa de configuração não é necessária para ambientes de produção e preparo profissionais. Consulte [Depuração para preparo e produção profissionais](#debug-for-pro-staging-and-production).

Para habilitar [!DNL Xdebug] para o seu projeto, adicione `xdebug` para o `runtime:extensions` seção do `.magento.app.yaml` arquivo.

**Para ativar o Xdebug**:

1. No terminal local, abra o `.magento.app.yaml` em um editor de texto.

1. No `runtime` seção, em `extensions`, adicionar `xdebug`. Por exemplo:

   ```yaml
   runtime:
       extensions:
           - redis
           - xsl
           - newrelic
           - sodium
           - xdebug
   ```

1. Salve as alterações no `.magento.app.yaml` e saia do editor de texto.

1. Adicione, confirme e envie as alterações para reimplantar o ambiente.

   ```bash
   git add -A
   ```

   ```bash
   git commit -m "Add xdebug"
   ```

   ```bash
   git push origin <environment-ID>
   ```

Quando implantados em ambientes iniciais e ambientes de integração Pro, [!DNL Xdebug] O agora está disponível. Continue configurando seu IDE. Para o PhpStorm, consulte [Configurar o PhpStorm](#configure-phpstorm).

### Configurar o PhpStorm

A variável [PhpStorm](https://www.jetbrains.com/phpstorm/) O IDE deve ser configurado para funcionar corretamente com [!DNL Xdebug].

**Para configurar o PhpStorm para funcionar com o Xdebug**:

1. No projeto PhpStorm, abra o **Configurações** painel.

   - _macOS_— Select **PhpStorm** > **Preferências**.
   - _Windows/Linux_— Select **Arquivo** > **Configurações**.

1. No _Configurações_ , expanda e localize o **Idiomas e estruturas** > **PHP** > **Servidores** seção.

1. Clique em **+** para adicionar uma configuração do servidor. O nome do projeto está em cinza na parte superior.

1. [Opcional] Defina as seguintes configurações para a nova configuração do servidor. Consulte [Nenhum servidor de depuração configurado](https://www.jetbrains.com/help/phpstorm/troubleshooting-php-debugging.html#no-debug-server-is-configured) no _PHPStorm_ documentação.

   - **Nome**—Digite o mesmo que o nome do host. Este valor deve corresponder ao valor do `PHP_IDE_CONFIG` variável em [Comandos CLI de depuração](#debug-cli-commands) para usar a CLI para depuração.
   - **Host**—Digite o nome do host.
   - **Porta**— Enter `443`.
   - **Depurador**— Select `Xdebug`.

1. Selecionar **Usar mapeamentos de caminho**. No _Arquivo/Diretório_ painel, a raiz do projeto para a variável `serverName` é exibido.

1. No **Caminho absoluto no servidor** clique no link **Editar** e adicione uma configuração com base no ambiente.

   - Para todos os ambientes iniciais e de integração Pro, o caminho remoto é `/app`.
   - Para ambientes de preparo e produção profissionais:

      - Produção: `/app/<project_code>/`
      - Estágios:  `/app/<project_code>_stg/`

1. Altere o [!DNL Xdebug] para 9000 no **Idiomas e estruturas** > **PHP** > **Depurar** > **Xdebug** > **Porta de depuração** painel.

1. Clique em **Aplicar**.

### Configurar encaminhamento de porta

Mapeie o `XDEBUG` conexão do servidor ao seu sistema local. Para fazer qualquer tipo de depuração, você deve encaminhar a porta 9000 do Adobe Commerce no servidor de infraestrutura em nuvem para o computador local. Consulte uma das seguintes seções:

- [Encaminhamento de portas no Mac ou UNIX](#port-forwarding-on-mac-or-unix)
- [Encaminhamento de porta no Windows](#port-forwarding-on-windows)

#### Encaminhamento de portas no Mac ou UNIX®

**Para configurar o encaminhamento de portas em um Mac ou em um ambiente UNIX®**:

1. Abra um terminal.

1. Use SSH para estabelecer a conexão.

   ```bash
   ssh -R 9000:localhost:9000 <ssh url>
   ```

   Use o `-v` (verboso) para que sempre que um soquete for conectado à porta que está sendo encaminhada ele seja exibido no terminal.

   Se um erro &quot;não é possível conectar&quot; ou &quot;não foi possível escutar a porta no remoto&quot; for exibido, pode haver outra sessão SSH ativa persistindo no servidor que está ocupando a porta 9000. Se essa conexão não estiver sendo usada, você poderá encerrá-la.

**Para solucionar problemas de conexão**:

1. Use o SSH para fazer logon no ambiente de integração remota, preparo ou produção.

1. Exibir uma lista de sessões SSH: `who`

1. Visualizar sessões SSH existentes por usuário. Tenha cuidado para não afetar um usuário que não seja você mesmo!

   - integração: os nomes de usuários são semelhantes ao `dd2q5ct7mhgus`
   - Estágios: os nomes de usuários são semelhantes aos `dd2q5ct7mhgus_stg`
   - Produção: nomes de usuário semelhantes a `dd2q5ct7mhgus`

1. Para uma sessão de usuário mais antiga que a sua, localize o valor do pseudoterminal (PTS), como `pts/0`.

1. Elimine a ID de processo (PID) correspondente ao valor PTS.

   ```bash
   ps aux | grep ssh
   kill <PID>
   ```

   Exemplo de resposta:

   ```terminal
   dd2q5ct7mhgus        5504  0.0  0.0  82612  3664 ?      S    18:45   0:00 sshd: dd2q5ct7mhgus@pts/0
   ```

   Para encerrar a conexão, digite um comando kill com o ID do processo (PID).

   ```bash
   kill 3664
   ```

#### Encaminhamento de porta no Windows

Para configurar o encaminhamento de portas (encapsulamento SSH) no Windows, você deve configurar o aplicativo de terminal do Windows. Este exemplo passa pela criação de um túnel SSH usando [Putty](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html). Você pode usar outros aplicativos, como o Cygwin. Para obter mais informações sobre outros aplicativos, consulte a documentação do fornecedor fornecida com esses aplicativos.

**Para configurar um túnel SSH no Windows usando o Putty**:

1. Se ainda não tiver feito isso, baixe [Putty](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html).

1. Comece o Putty.

1. No painel Categoria, clique em **Session**.

1. Insira as seguintes informações:

   - **Nome do host (ou endereço IP)** campo: insira o [URL SSH](../development/secure-connections.md#connect-to-a-remote-environment) para o servidor do Cloud
   - **Porta** campo: insira `22`

   ![Configurar Putty](../../assets/xdebug/putty-session.png)

1. No _Categoria_ clique em **Conexão** > **SSH** > **Túneis**.

1. Insira as seguintes informações:

   - **Porta de origem** campo: insira `9000`
   - **Destino** campo: insira `127.0.0.1:9000`
   - Clique em **Remoto**

1. Clique em **Adicionar**.

   ![Criar um túnel SSH no Putty](../../assets/xdebug/putty-tunnels.png)

1. No _Categoria_ clique em **Session**.

1. No **Sessões Salvas** insira um nome para este túnel SSH.

1. Clique em **Salvar**.

   ![Salve o túnel SSH](../../assets/xdebug/putty-session-save.png)

1. Para testar o túnel SSH, clique em **Carregar** e, em seguida, clique em **Abertura**.

   Se um erro &quot;não é possível conectar&quot; for exibido, verifique o seguinte:

   - Todas as configurações de Putty estão corretas
   - Você está executando o Putty na máquina em que suas chaves SSH privadas do Adobe Commerce na infraestrutura em nuvem estão localizadas

## Acesso SSH a ambientes Xdebug

Para iniciar a depuração, executar a configuração e muito mais, você precisa dos comandos SSH para acessar os ambientes. Você pode obter essas informações por meio da [[!DNL Cloud Console]](../development/secure-connections.md#use-an-ssh-command) e a planilha do projeto.

Para ambientes iniciais e de integração Pro, é possível usar o seguinte `magento-cloud` Comando da CLI para SSH nesses ambientes:

```bash
magento-cloud environment:ssh --pipe -e <environment-ID>
```

Para usar [!DNL Xdebug], SSH para o ambiente da seguinte forma:

```bash
ssh -R <xdebug listen port>:<host>:<xdebug listen port> <SSH-URL>
```

Por exemplo,

```bash
ssh -R 9000:localhost:9000 pwga8A0bhuk7o-mybranch@ssh.us.magentosite.cloud
```

## Depuração para preparo e produção profissionais

>[!NOTE]
>
>Em ambientes de preparo e produção profissionais, [!DNL Xdebug] está sempre disponível, pois esses ambientes têm uma configuração especial para [!DNL Xdebug]. Todas as solicitações normais da Web são roteadas para um processo PHP dedicado que não tem [!DNL Xdebug]. Portanto, essas solicitações são processadas normalmente e não estão sujeitas à degradação do desempenho quando [!DNL Xdebug] está carregado. Quando uma solicitação da Web é enviada com o [!DNL Xdebug] chave, ela é roteada para um processo PHP separado que tem [!DNL Xdebug] carregado.

Para usar [!DNL Xdebug] especificamente no ambiente de preparo e produção do plano Pro, você cria um túnel SSH separado e uma sessão da Web somente para os quais tem acesso. Esse uso difere do acesso típico, fornecendo acesso apenas a você e não a todos os usuários.

Você precisa do seguinte:

- Comandos SSH para acessar os ambientes. Você pode obter essas informações por meio da [[!DNL Cloud Console]](../project/overview.md) ou seu [!DNL Cloud Onboarding UI].
- A variável `xdebug_key` valor definido ao configurar os ambientes de Preparo e Pro.

  A variável `xdebug_key` O pode ser encontrado usando SSH para fazer logon no nó primário e executando:

  ```bash
  cat /etc/platform/*/nginx.conf | grep xdebug.sock | head -n1
  ```

**Para configurar um túnel SSH para um ambiente de preparo ou produção**:

1. Abra um terminal.

1. Limpe todas as sessões SSH para cada nó da Web do cluster.

   ```bash
   ssh USERNAME@CLUSTER.ent.magento.cloud 'rm /run/platform/USERNAME/xdebug.sock'
   ```

1. Configure o túnel SSH para o Xdebug para cada nó da Web do cluster.

   ```bash
   ssh -R /run/platform/USERNAME/xdebug.sock:localhost:9000 -N USERNAME@CLUSTER.ent.magento.cloud
   ```

**Para iniciar a depuração usando o URL do ambiente**:

1. Ativar depuração remota; visite o site no navegador e anexe o seguinte ao URL em que `KEY` é valor de `xdebug_key`.

   ```http
   ?XDEBUG_SESSION_START=KEY
   ```

   Esta etapa define o cookie que envia solicitações do navegador para acionar [!DNL Xdebug].

1. Conclua a depuração com [!DNL Xdebug].

1. Quando estiver pronto para encerrar a sessão, use o seguinte comando para remover o cookie e finalizar a depuração pelo navegador, onde `KEY` é valor de `xdebug_key`.

   ```http
   ?XDEBUG_SESSION_STOP=KEY
   ```

   >[!NOTE]
   >
   >A variável `XDEBUG_SESSION_START` passado por `POST` não são compatíveis.

## Comandos CLI de depuração

Esta seção aborda os comandos CLI de depuração.

Para depurar comandos da CLI:

1. SSH no servidor que você deseja depurar usando comandos CLI.

1. Crie as seguintes variáveis de ambiente:

   ```bash
   export XDEBUG_CONFIG='PHPSTORM'
   ```

   ```bash
   export PHP_IDE_CONFIG="serverName=<name of the server that is configured in PHPSTORM>"
   ```

   Essas variáveis são removidas quando a sessão SSH termina.

1. Iniciar depuração

   Em ambientes Starter e de integração Pro, execute o comando da CLI para depurar.
Você pode adicionar opções de tempo de execução, por exemplo:

   ```bash
   php -d xdebug.profiler_enable=On -d xdebug.max_nesting_level=9999 bin/magento cache:clean
   ```

   Em ambientes de preparo e produção profissionais, você deve especificar o caminho para a [!DNL Xdebug] O arquivo de configuração do PHP ao depurar comandos da CLI, por exemplo:

   ```bash
   php -c /etc/platform/USERNAME/php.xdebug.ini bin/magento cache:clean
   ```

## Depurar solicitações da Web

As etapas a seguir ajudam a depurar solicitações da Web.

1. No _Extensão_ clique em **Depurar** para ativar.

1. Clique com o botão direito do mouse, selecione o menu de opções e defina a chave do IDE como **PHPSTORM**.

1. Instale o [!DNL Xdebug] cliente no navegador. Configure e ative-o.

### Exemplo: configuração do Chrome

Esta seção discute como usar [!DNL Xdebug] no Chrome usando o [!DNL Xdebug] Extensão auxiliar. Para obter informações sobre [!DNL Xdebug] para outros navegadores, consulte a documentação do navegador.

**Para usar o Xdebug Helper com o Chrome**:

1. Criar um [Túnel SSH](#ssh-access-to-xdebug-environments) ao servidor da nuvem.

1. Instale o [Extensão Auxiliar Do Xdebug](https://chromewebstore.google.com/detail/eadndfjplgieldjbigjakmdgkmoaaaoc) na loja Chrome.

1. Ative a extensão no Chrome conforme mostrado na figura a seguir.

   ![Ativar a extensão Xdebug no Chrome](../../assets/xdebug/enable-chrome-ext.png)

1. No Chrome, clique com o botão direito do mouse no ícone verde auxiliar na barra de ferramentas do Chrome.

1. No menu pop-up, clique em **Opções**.

1. No _Chave IDE_ clique em **PhpStorm**.

1. Clique em **Salvar**.

   ![Opções do assistente do Xdebug](../../assets/xdebug/helper-options.png)

1. Abra o projeto PhpStorm.

1. Na barra de navegação superior, clique na guia **Iniciar escuta** ícone.

   Se a barra de navegação não for exibida, clique em **Exibir** > **Barra de navegação**.

1. No painel de navegação do PhpStorm, clique duas vezes no arquivo PHP para testar.

## Depurar código local

Devido aos ambientes somente leitura, você deve extrair código para a estação de trabalho local de um ambiente ou ramificação Git específica para executar a depuração.

O método que você escolher depende de você. Você tem as seguintes opções:

- Confira o código do Git e execute `composer install`

  Este método funciona a menos que `composer.json` O faz referência a packages em repositórios privados aos quais você não tem acesso. Este método resulta na obtenção de toda a base de código do Adobe Commerce.

- Copie o `vendor`, `app`, `pub`, `lib`, e `setup` diretórios

  Esse método resulta em ter todos os códigos que você pode testar. Dependendo de quantos ativos estáticos você tem, isso pode resultar em uma longa transferência com um grande volume de arquivos.

- Copie o `vendor` somente diretório

  Como a maioria do código está no estado `vendor` , esse método provavelmente resultará em um bom teste, embora não estejam testando toda a base de código.

**Para compactar arquivos e copiá-los no computador local**:

1. Use o SSH para fazer logon no ambiente remoto.

1. Compacte os arquivos.

   ```bash
   tar -czf /tmp/<file-name>.tgz <directory list>
   ```

   Por exemplo, para compactar o `vendor` somente diretório:

   ```bash
   tar -czf /tmp/vendor.tgz vendor
   ```

1. Em seu ambiente local, use o PhpStorm para compactar os arquivos.

   ```bash
   cd <phpstorm project root dir>
   ```

   ```bash
   rsync <SSH-URL>:/tmp/<file-name>.tgz .
   ```

   ```bash
   tar xzf <file-name>.tgz
   ```
