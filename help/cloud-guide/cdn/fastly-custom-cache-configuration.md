---
title: Personalizar configuração do cache
description: Saiba como revisar e personalizar as configurações de cache após a conclusão da configuração do serviço Fastly.
feature: Cloud, Configuration, Iaas, Cache
exl-id: f1fc85d4-7867-4bb5-9f11-bc8d2d80383b
source-git-commit: 8a0523f1714b6ea41887e99b5c31294cf5e5255e
workflow-type: tm+mt
source-wordcount: '1808'
ht-degree: 0%

---

# Personalizar configuração do cache

Depois de configurar e testar o serviço Fastly nos ambientes de Preparo e Produção, revise e personalize as configurações do cache. Por exemplo, você pode atualizar as configurações para permitir que forçar o TLS redirecione solicitações HTTP para o Fastly, atualizar as configurações de limpeza e habilitar a autenticação básica para proteger seu site com senha durante o desenvolvimento.

As seções a seguir fornecem uma visão geral e instruções para definir algumas configurações de cache. Encontre informações adicionais sobre as opções de configuração disponíveis no [Módulo CDN Fastly para Magento 2](https://github.com/fastly/fastly-magento2/tree/master/Documentation) documentação.

## Forçar TLS

O Fastly fornece o _Forçar TLS_ opção para redirecionar solicitações não criptografadas (HTTP) para o Fastly. Depois que o ambiente de preparo ou produção for provisionado com um [certificado SSL/TLS válido](fastly-configuration.md#provision-ssltls-certificates), é possível atualizar a configuração do Fastly no armazenamento para habilitar a opção Forçar TLS. Veja o Fastly [Forçar guia TLS](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/FORCE-TLS.md) no _Módulo CDN Fastly para Magento 2_ documentação.

>[!NOTE]
>
>A ativação da opção Forçar TLS é uma prática recomendada para o Adobe Commerce em lojas de infraestrutura em nuvem.

## Estender tempo limite do Fastly

A configuração do serviço Fastly especifica um período de tempo limite padrão de 180 segundos para solicitações HTTPS para o Administrador. Qualquer processamento de solicitação que exceda o período de tempo limite retorna um erro 503. Como resultado, você pode receber 503 erros em resposta a solicitações que exigem processamento demorado ou ao tentar executar operações em massa.

Para concluir ações em massa que levem mais de 3 minutos, altere o _Tempo limite do caminho do administrador_ value_ para evitar erros 503.

>[!NOTE]
>
>Para estender os parâmetros de tempo limite do Fastly para outros que não o Admin na interface do Fastly, consulte [Aumentar Tempos Limite para Trabalhos Longos](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/Edge-Modules/EDGE-MODULE-INCREASE-TIMEOUTS-LONG-JOBS.md).

**Para estender o tempo limite do Fastly para o Administrador**:

{{admin-login-step}}

1. Clique em **Lojas** > Configurações > **Configuração** > **Avançado** > **Sistema** e expandir **Cache de Página Inteira**.

1. No _Configuração do Fastly_ seção, expandir **Configuração avançada**.

1. Defina o **Tempo limite do caminho do administrador** em segundos. Esse valor não pode ser superior a 10 minutos (600 segundos).

1. Clique em **Salvar configuração** na parte superior da página.

1. Depois que a página for recarregada, selecione **Carregar VCL para Fastly** no _Configuração do Fastly_ seção.

O Fastly recupera o caminho do Administrador para gerar o arquivo VCL a partir do `app/etc/env.php` arquivo de configuração.

## Configurar opções de limpeza

O Fastly fornece vários tipos de opções de descarte na página Gerenciamento de cache de Magento, incluindo opções para descartar categoria de produto, ativos de produto e conteúdo. Quando ativado, o Fastly observa eventos para limpar automaticamente esses caches. Se você desativar uma opção de expurgação, poderá expurgar manualmente os caches do Fastly após finalizar as atualizações através da página Gerenciamento de Cache.

As opções de limpeza incluem:

- **Categoria de limpeza**-Limpa o conteúdo da categoria do produto (não o conteúdo do produto) quando você adiciona e atualiza um único produto. Talvez você queira manter essa opção desativada e ativar a opção Limpar produto, que limpa produtos e categorias de produtos.
- **Limpar produto**- Limpa todo o conteúdo do produto e da categoria do produto ao salvar uma única modificação em um produto. Ativar a opção Limpar produto pode ser útil para obter atualizações imediatamente para os clientes ao alterar um preço, adicionar uma opção de produto e quando o inventário de produto estiver esgotado.
- **Página Expurgar CMS**-Limpa o conteúdo da página ao atualizar e adicionar páginas ao Adobe Commerce CMS. Por exemplo, talvez você queira expurgar ao atualizar os Termos e condições ou a política de Devolução. Se você raramente fizer essas alterações, poderá desativar a limpeza automática.
- **Limpeza suave**- Define o conteúdo alterado como obsoleto e o limpa de acordo com o tempo obsoleto. Além dos tempos obsoletos, os clientes recebem conteúdo obsoleto, enquanto o Fastly atualiza o conteúdo em segundo plano.

![Configurar opções de limpeza](../../assets/cdn/fastly-purge-options.png)

**Para configurar as opções de limpeza do Fastly**:

1. No _Configuração do Fastly_ seção, expandir **Configuração avançada** para exibir as opções de expurgação.

1. Para cada opção de expurgação, selecione **Sim** para ativar a expurgação automática, ou **Não** para desativar a limpeza automática.

   Quando você desativa uma opção de expurgação, deve expurgar manualmente o cache para essa categoria da _Gerenciamento de cache_ página.

1. Clique em **Salvar configuração** na parte superior da página.

1. Depois que a página for recarregada, selecione **Carregar VCL para Fastly** no _Configuração do Fastly_ seção.

Para obter mais informações, consulte [as opções de configuração do Fastly](https://github.com/fastly/fastly-magento2/blob/21b61c8189971275589219d418332798efc7db41/Documentation/CONFIGURATION.md#further-configuration-options).

## Configurar manipulação de GeoIP

O módulo Fastly inclui o manuseio de GeoIP para redirecionar os visitantes automaticamente ou fornecer uma lista de lojas que correspondem ao código de país obtido. Se você já usa uma extensão para manipulação de GeoIP, talvez precise verificar os recursos com as opções do Fastly.

**Para configurar o manuseio de GeoIp**:

{{admin-login-step}}

1. Clique em **Lojas** > Configurações > **Configuração** > **Avançado** > **Sistema** e expandir **Cache de Página Inteira**.

1. No _Configuração do Fastly_ seção, expandir **Configuração avançada**.

1. Role para baixo e selecione **Sim** para **Habilitar GeoIP**. Opções adicionais de configuração são exibidas.

1. Para Ação GeoIP, selecione se o visitante for automaticamente redirecionado com **Redirecionar** ou forneceu uma lista de armazenamentos para seleção com **Caixa de diálogo**.

1. Para **Mapeamento de países**, selecione **Adicionar** para inserir um código de país de duas letras a ser mapeado com uma loja Adobe Commerce específica de uma lista.

   ![Adicionar mapas de países GeoIP](/help/assets/cdn/fastly-geo-code.png)

1. Clique em **Salvar configuração** na parte superior da página.

1. Após o recarregamento da página, selecione **Carregar VCL para Fastly** no _Configuração do Fastly_ seção.

>[!NOTE]
>
>A implementação atual do módulo Adobe Commerce Fastly GeoIP não oferece suporte a redirecionamentos entre vários sites.

A Fastly também fornece uma série de [recursos de VCL relacionados à geolocalização](https://developer.fastly.com/reference/vcl/variables/geolocation/) para codificação de geolocalização personalizada.

## Habilitar módulos do Fastly Edge

O Fastly Edge Modules é uma estrutura flexível que permite a definição de componentes de interface do usuário e do código VCL associado por meio de um modelo. Esses módulos facilitam a personalização e a extensão da configuração do serviço Fastly por meio da interface do usuário, em vez de usar trechos de VCL personalizados.

Os módulos de borda permitem habilitar funcionalidades específicas, como cabeçalhos CORS, substituições de mapas do site da nuvem e configurar a integração entre a loja do Adobe Commerce e outros CMSs ou back-ends.

Para acessar o menu Módulos de borda para exibir, configurar e gerenciar os módulos disponíveis, ative o _Habilitar módulos do Fastly Edge_ opção. Consulte [Módulos do Fastly Edge](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/Edge-Modules/EDGE-MODULES.md) na documentação do módulo CDN Fastly.

## Configurar back-ends e blindagem de origem

As configurações de back-end fornecem ajuste fino para o desempenho do Fastly com a blindagem Origin e tempos limite. A _back-end_ é um local específico (IP ou domínio) com o Origin shield configurado e tempo limite para verificação e fornecimento de conteúdo em cache.

_Blindagem de origem_ roteia todas as solicitações do armazenamento para um Ponto de Presença (POP) específico. Quando uma solicitação é recebida, o POP verifica o conteúdo em cache e o fornece. Se não for armazenado em cache, ele continuará para o POP do Shield e, em seguida, para o servidor de Origem, que armazena o conteúdo em cache. Os escudos reduzem o tráfego diretamente para a origem.

O código padrão do Fastly VCL especifica valores padrão para a blindagem de Origem e tempos limite para seu Adobe Commerce em sites de infraestrutura em nuvem. Em alguns casos, pode ser necessário modificar os valores padrão. Por exemplo, se você estiver recebendo erros de Time to First Byte (TTFB), talvez seja necessário ajustar a variável _tempo limite do primeiro byte_ valor.

>[!NOTE]
>
>Se o site exigir entrega funcional por meio de uma integração de back-end como [Wordpress](fastly-vcl-wordpress.md), personalize a configuração do serviço Fastly para adicionar o back-end e gerenciar os redirecionamentos da loja do Adobe Commerce para o Wordpress. Para obter detalhes, consulte [Módulos Fastly Edge - Outra integração CMS/Backend](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/Edge-Modules/EDGE-MODULE-OTHER-CMS-INTEGRATION.md) na documentação do módulo Fastly.

**Para analisar a configuração de backend**:

{{admin-login-step}}

1. Clique em **Lojas** > Configurações > **Configuração** > **Avançado** > **Sistema** e expandir **Cache de Página Inteira**.

1. Expanda a **Configuração do Fastly** seção.

1. Expandir **Configurações de backend** e selecione a engrenagem para verificar o back-end padrão. Uma modal é aberta mostrando as configurações atuais com opções para alterá-las.

   ![Modificar o back-end](../../assets/cdn/fastly-backend.png)

1. Selecione o **Blindagem** local (ou data center).

   A configuração padrão do Fastly para o seu projeto define o local mais próximo à região do Cloud Service. Se precisar alterá-lo, selecione um local próximo ao local padrão.

1. Modifique os valores de tempo limite (em microssegundos) para a conexão com a blindagem, tempo entre bytes e tempo para o primeiro byte. Recomendamos manter as configurações padrão de tempo limite.

1. Opcionalmente, selecione para **Ativar o back-end e a blindagem após editar ou salvar**.

1. Clique em **Carregar** para salvar suas alterações e carregá-las nos servidores do Fastly.

1. Em Admin, selecione **Salvar configuração**.

Para obter mais informações, consulte [Guia de configurações de backend](https://github.com/fastly/fastly-magento2/blob/21b61c8189971275589219d418332798efc7db41/Documentation/Guides/BACKEND-SETTINGS.md) na documentação do módulo Fastly.

## Autenticação básica

A autenticação básica é um recurso para proteger todas as páginas e ativos do site com um nome de usuário e uma senha. Nós **não recomendar** Ativação da autenticação básica no ambiente de produção. Você pode configurá-lo no ambiente de preparo para proteger seu site durante o processo de desenvolvimento. Consulte a [Guia de autenticação básica](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/BASIC-AUTH.md) na documentação do módulo CDN Fastly.

Se você adicionar acesso de usuário e habilitar a autenticação básica no ambiente de preparo, ainda será possível acessar o Administrador sem exigir credenciais adicionais.

## Criar trechos de VCL personalizados

O Fastly oferece suporte a uma versão personalizada do Varnish Configuration Language (VCL) para personalizar a configuração do serviço Fastly. Por exemplo, você pode permitir, bloquear ou redirecionar o acesso de usuários específicos ou endereços IP usando blocos de código VCL com dicionários de borda e de Lista de controle de acesso (ACL).

Para obter instruções sobre como criar trechos de VCL personalizados, dicionários de borda e ACLs, consulte [Trechos de VCL Fastly personalizados](fastly-vcl-custom-snippets.md).

>[!NOTE]
>
>Antes de adicionar código VCL personalizado, dicionários de borda e ACLs à configuração do módulo Fastly, verifique se o serviço de cache do Fastly funciona com a configuração padrão. Consulte [Configurar o Fastly](fastly-configuration.md).

## Gerenciar domínios

Para projetos Starter e Pro, você pode usar o [!UICONTROL Domains] opção para adicionar e gerenciar a configuração de domínio do Fastly para sua loja.

- Para projetos iniciais, vá para o URL do projeto no [!UICONTROL Domains] na guia [!DNL Cloud Console] para adicionar a URL do projeto.

- Para projetos Pro, envie um [Tíquete de suporte do Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) para adicionar o domínio à configuração do projeto na nuvem. A equipe de suporte também atualiza a configuração da conta do Adobe Commerce Fastly para adicionar o domínio.

**Para gerenciar a configuração de domínio do Fastly no Admin**:

{{admin-login-step}}

1. Selecionar **Lojas** > Configurações > **Configuração** > **Avançado** > **Sistema** e expandir **Cache de Página Inteira**.

1. No Admin _Configuração do Fastly_ , selecione **Domínios**.

1. Clique em **Gerenciar domínios** para abrir a página Domínios.

1. Adicione os nomes de nível superior e subdomínio para as lojas no ambiente de nuvem.

   Você só pode especificar domínios que já foram adicionados à sua configuração de infraestrutura na nuvem.

   ![Adicionar configuração de domínio Fastly para iniciar](../../assets/cdn/fastly-starter-activate-domain.png)

1. Clique em **Ativar** para atualizar a configuração do domínio Fastly.

>[!NOTE]
>
>Se o mesmo domínio tiver sido configurado em uma conta diferente do Fastly, você deverá enviar um tíquete de suporte do Adobe Commerce para solicitar a Delegação de Domínio antes de adicionar o domínio ao Adobe Commerce. Consulte [Várias contas do Fastly e domínios atribuídos](fastly.md#multiple-fastly-accounts-and-assigned-domains).

## Ativar modo de manutenção

Use o _Modo de manutenção_ opção para permitir acesso administrativo ao site a partir de endereços IP especificados, retornando uma página de erro para todas as outras solicitações.

**Para ativar o Modo de manutenção com acesso Administrativo**:

1. Abra o _Configuração do Fastly_ no Admin.

1. No _ACL de borda_ seção, atualize o `maint_allow` a ACL (Access Control List, lista de controle de acesso) com os endereços IP administrativos que podem acessar sua loja enquanto ela está no modo de manutenção.

   ![Atualizar lista de permissões do modo de manutenção de IP](../../assets/cdn/fastly-maint-allowlist.png)

1. No _Modo de manutenção_ , selecione **Ativar modo de manutenção**.

   Após habilitar o modo de manutenção, todo o tráfego será bloqueado, exceto as solicitações dos endereços IP no `maint_allowlist` ACL. Você pode atualizar o `maint_allowlist` para alterar os endereços IP na ACL.

   Para obter instruções detalhadas de configuração, consulte [Guia do Modo de manutenção](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/MAINTENANCE-MODE.md) na documentação do Fastly CDN para o módulo Magento 2.
