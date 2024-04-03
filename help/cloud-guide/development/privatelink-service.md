---
title: Serviço PrivateLink
description: Saiba como usar o serviço PrivateLink para estabelecer uma conexão segura entre uma nuvem privada e a plataforma de nuvem da Adobe Commerce na mesma região.
feature: Cloud, Iaas, Security
exl-id: b25548b8-312b-4a74-b242-f4e2ac6cf945
source-git-commit: 5b52157c6c623bb4c765a2d545919df79d81f1da
workflow-type: tm+mt
source-wordcount: '1609'
ht-degree: 0%

---

# Serviço PrivateLink

O Adobe Commerce na infraestrutura em nuvem oferece suporte à integração com o [AWS PrivateLink](https://aws.amazon.com/privatelink/) ou [Link privado do Azure](https://learn.microsoft.com/en-us/azure/private-link/) serviço. Você pode usar o PrivateLink para estabelecer comunicação segura e privada entre o Adobe Commerce em ambientes de infraestrutura em nuvem com serviços e aplicativos hospedados em sistemas externos. O aplicativo do Adobe Commerce e os sistemas externos devem ser acessíveis por meio de endpoints da Nuvem privada virtual (VPC) configurados na mesma plataforma de nuvem (AWS ou Azure) na mesma região de nuvem.

>[!TIP]
>
>O PrivateLink é melhor usado para proteger conexões para integrações não HTTP(S), como transferências de banco de dados ou arquivos. Se você planeja integrar seu aplicativo às APIs do Adobe Commerce, consulte como criar um [Adobe API Mesh](https://developer.adobe.com/graphql-mesh-gateway/gateway/create-mesh/) in _Malha de API para o Construtor de aplicativos Adobe Developer_.

## Recursos e suporte

A integração do serviço PrivateLink para projetos de infraestrutura em nuvem do Adobe Commerce inclui os seguintes recursos e suporte:

- Uma conexão segura entre uma Nuvem privada virtual (VPC) do cliente e o VPC do Adobe na mesma plataforma de nuvem (AWS ou Azure) na mesma região da Nuvem.
- Suporte para comunicação unidirecional ou bidirecional entre os serviços de endpoint disponíveis no Adobe e VPCs do cliente.
- Ativação de serviço:

   - Abra as portas necessárias no ambiente Adobe Commerce na infraestrutura em nuvem
   - Estabeleça a conexão inicial entre o cliente e os VPCs Adobe
   - Solução de problemas de conexão durante a ativação

## Limitação

- O suporte para PrivateLink está disponível somente em ambientes de produção e preparo profissionais. Não está disponível em ambientes locais ou de integração, nem em projetos iniciais.
- Não é possível estabelecer conexões SSH usando PrivateLink. Consulte [Habilitar chaves SSH](secure-connections.md).
- O suporte da Adobe Commerce não abrange a solução de problemas do AWS PrivateLink além da ativação inicial.
- Os clientes são responsáveis pelos custos associados ao gerenciamento de seu próprio VPC.
- Você não pode usar o protocolo HTTPS (porta 443) para se conectar ao Adobe Commerce na infraestrutura de nuvem pelo Link privado do Azure devido a [Fastly origin cloaking](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/faq/fastly-origin-cloaking-enablement-faq.html). Essa limitação não se aplica ao AWS PrivateLink.
- PrivateDNS não está disponível.

## Tipos de conexão PrivateLink

Há dois tipos de conexão PrivateLink disponíveis, mostrados no diagrama de rede a seguir, para estabelecer uma comunicação segura entre sua loja e sistemas externos hospedados fora do ambiente da nuvem.

![Diagrama de rede PrivateLink](../../assets/privatelink-architecture-diagram.png)

Escolha um dos tipos de conexão PrivateLink mais adequados para seus ambientes do Adobe Commerce na infraestrutura em nuvem:

- **PrivateLink Unidirecional**-Escolha essa configuração para recuperar dados com segurança de um Adobe Commerce no armazenamento de infraestrutura em nuvem.
- **Link privado bidirecional**-Escolha essa configuração para estabelecer conexões seguras de e para sistemas fora da Adobe Commerce no ambiente de infraestrutura em nuvem. A opção bidirecional requer duas conexões:

   - Uma conexão entre o VPC do cliente e o VPC do Adobe
   - Uma conexão entre o VPC Adobe e o VPC do cliente

>[!TIP]
>
>Trabalhe com seu administrador de rede ou provedor de plataforma na nuvem para obter ajuda sobre como selecionar o tipo de conexão PrivateLink ou ajuda sobre configuração e administração de VPC. Consulte Documentação do PrivateLink da plataforma de nuvem: [AWS PrivateLink](https://aws.amazon.com/privatelink/) ou [Link privado do Azure](https://learn.microsoft.com/en-us/azure/private-link/).

## Solicitar ativação do PrivateLink

>[!WARNING]
>
>A ativação do PrivateLink pode levar até _cinco_ dias úteis. O fornecimento de informações incompletas ou imprecisas pode atrasar o processo.

### Pré-requisitos

![check](../../assets/fix.svg) Uma conta de nuvem (AWS ou Azure) na mesma região da instância do Adobe Commerce na infraestrutura em nuvem.

![check](../../assets/fix.svg) Um VPC no ambiente do cliente que hospeda os serviços para se conectar por meio do PrivateLink. Consulte a documentação do AWS ou do Azure para obter ajuda com a configuração do VPC ou entre em contato com o administrador de rede.

![check](../../assets/fix.svg) Para conexões PrivateLink bidirecionais, você deve criar a configuração do serviço de ponto de extremidade para seu aplicativo ou serviço e criar um ponto de extremidade em seu ambiente VPC antes de solicitar a ativação do PrivateLink. Consulte [Configurar conexões bidirecionais do PrivateLink](#set-up-for-bidirectional-privatelink-connections).

Obtenha os seguintes dados necessários para a ativação do PrivateLink:

- **Número da conta da Customer Cloud** (AWS ou Azure) — Deve estar na mesma região que a instância do Adobe Commerce na infraestrutura em nuvem
- **Região da nuvem**—Forneça a região da nuvem em que a conta está hospedada para fins de verificação
- **Portas de serviços e comunicação**—O Adobe deve abrir portas para habilitar a comunicação de serviço entre VPCs, por exemplo, porta SQL 3306, porta SFTP 2222
- **ID do projeto**— Fornecer a ID do projeto do Adobe Commerce na infraestrutura em nuvem Pro. Você pode obter a ID do projeto e outras informações usando o seguinte [CLI da nuvem](../dev-tools/cloud-cli-overview.md) comando: `magento-cloud project:info`
- **Tipo de conexão**—Especificar unidirecional ou bidirecional para o tipo de conexão
- **Serviço de ponto de extremidade**—Para conexões PrivateLink bidirecionais, forneça o URL DNS para o serviço de endpoint VPC ao qual o Adobe deve se conectar, por exemplo: `com.amazonaws.vpce.<cloud-region>.vpce-svc-<service-id>`
- **Acesso concedido ao serviço de ponto de extremidade**—Para se conectar a um serviço externo, permita o acesso do serviço de ponto de extremidade à seguinte entidade de conta da AWS: `arn:aws:iam::402592597372:root`

  >[!WARNING]
  >
  >Se o acesso ao serviço de endpoint não for fornecido, a conexão PrivateLink bidirecional com o serviço no VPC será **não** adicionado, o que atrasa a configuração.

#### Pré-requisitos adicionais específicos da ativação do Azure Private Link

- Forneça a ID do cluster; usando SSH, faça logon no remoto e use o comando: `cat /etc/platform_cluster`
- Para que um serviço externo se conecte ao cluster Adobe Commerce Pro, é necessário:

   - Uma lista de portas no cluster Pro para expor ao novo Ponto de Extremidade Privado externo
   - Uma lista de IDs de assinatura do Azure para as conexões de Ponto de Extremidade Privado

- Para conectar seu cluster Adobe Commerce Pro a um serviço externo, você precisa:

   - Uma lista de IDs de recursos para os serviços de destino. As IDs de serviço de Link privado externo são semelhantes ao seguinte:

  ```text
  /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/privateLinkServices/{svcNameID}
  ```

### Fluxo de trabalho de ativação

O fluxo de trabalho a seguir descreve o processo de ativação da integração do PrivateLink com o Adobe Commerce na infraestrutura em nuvem.

1. **Cliente** envia um tíquete de suporte solicitando a ativação do PrivateLink com a linha de assunto `PrivateLink support for <company>`. Inclua o [dados necessários para a ativação](#prerequisites) no tíquete. O Adobe usa o tíquete Suporte para coordenar a comunicação durante o processo de ativação.

1. **Adobe** habilita o acesso da conta do cliente ao serviço de ponto de extremidade no VPC do Adobe.

   - Atualize a configuração do serviço de ponto de extremidade Adobe para aceitar solicitações iniciadas da conta do AWS ou do Azure do cliente.
   - Atualize o tíquete de Suporte para fornecer o nome de serviço do endpoint de VPC do Adobe ao qual se conectar, por exemplo `com.amazonaws.vpce.<cloud-region>.vpce-svc-<service-id>`.

1. **Cliente** adiciona o serviço de ponto de extremidade do Adobe à sua conta da nuvem (AWS ou Azure), o que aciona uma solicitação de conexão para o Adobe. Consulte a documentação da plataforma na nuvem para obter instruções:

   - Para o AWS, consulte [Aceitar e rejeitar solicitações de conexão de ponto de extremidade de interface].
   - Para o Azure, consulte [Gerenciar solicitações de conexão].

1. **Adobe** aprova a solicitação de conexão.

1. Após a aprovação da solicitação de conexão, **o cliente** [verifica a conexão](#test-vpc-endpoint-service-connection) entre o VPC deles e o VPC do Adobe.

1. Etapas adicionais para ativar conexões bidirecionais:

   - **Adobe** fornece o principal da conta Adobe (usuário raiz para a conta do AWS ou do Azure) e solicita acesso ao serviço de ponto de extremidade VPC do cliente.
   - **Cliente** habilita o acesso de Adobe ao serviço de endpoint no VPC do cliente. Isso pressupõe que o principal da conta Adobe tenha acesso a `arn:aws:iam::402592597372:root`, conforme descrito anteriormente na seção **Acesso concedido ao serviço de ponto de extremidade** pré-requisito.

      - Atualize a configuração do serviço de ponto de extremidade do cliente para aceitar solicitações iniciadas da conta Adobe. Consulte a documentação da plataforma na nuvem para obter instruções:

         - Para o AWS, consulte [Adicionar e remover permissões do serviço de ponto de extremidade].
         - Para o Azure, consulte [Gerenciar uma conexão de Ponto de Extremidade Privado]

      - Forneça ao Adobe o nome do serviço de ponto de extremidade para o VPC do cliente.

   - **Adobe** adiciona o serviço de ponto de extremidade do cliente à conta da plataforma Adobe (AWS ou Azure), o que aciona uma solicitação de conexão com o VPC do cliente.
   - **Cliente** aprova a solicitação de conexão do Adobe para concluir a configuração.
   - **Cliente** [verifica a conexão](#test-vpc-endpoint-service-connection) do VPC Adobe.

## Testar conexão de serviço de ponto de extremidade VPC

Você pode usar o aplicativo Telnet para testar a conexão com o serviço de ponto de extremidade VPC.

**Para testar a conexão com o serviço de ponto de extremidade VPC**:

1. No diretório raiz do projeto, **check-out** o ambiente de preparo ou produção configurado para acessar o serviço de ponto de extremidade PrivateLink.

   ```bash
   magento-cloud environment:checkout <environment-id>
   ```

1. Execute o seguinte comando CURL:

   ```bash
   curl -v telnet://<endpoint-service-dns-url>:<port>/
   ```

   Exemplo:

   ```terminal
   $ curl -v telnet://vpce-007ffnb9qkcnjgult-yfhmywqh.vpce-svc-083cqvm2ta3rxqat5v.us-east-1.vpce.amazonaws.com:80 -vvv
   ```

   Exemplo de resposta bem-sucedida:

   ```terminal
   * Rebuilt URL to: telnet://vpce-007ffnb9qkcnjgult-yfhmywqh.vpce-svc-083cqvm2ta3rxqat5v.us-east-1.vpce.amazonaws.com:80
   * Connected to vpce-0088d56482571241d-yfhmywqh.vpce-svc-083cqvm2ta3rxqat5v.us-east-1.vpce. amazonaws.com (191.210.82.246) port 80 (#0)
   ```

   Exemplo de resposta com falha:

   ```terminal
   Failed to connect to vpce-007ffnb9qkcnjgult-yfhmywqh.vpce-svc-083cqvm2ta3rxqat5v.ap-southeast-1.vpce.amazonaws.com port 80: Connection timed out
   * Closing connection 0
   ```

1. Verifique se o serviço está escutando na VM.

   ```bash
   netstat -na | grep <port>
   ```

1. Verifique o fluxo de pacotes.

   ```bash
   tcpdump -i <ethernet-interface> -tt -nn port <destination-port> and host <source-host>
   ```

   Verifique as seguintes configurações internas para garantir que a configuração seja válida:

   - Configurações de ponto de extremidade e serviços de ponto de extremidade
   - Configurações do Balanceador de Carga de Rede (NLB)
   - Os grupos de destino no NLB e verificar se estão íntegros
   - O URL do ponto de extremidade netcat/curl de cada VM (listado acima)

   Consulte os seguintes artigos para obter ajuda com a solução de problemas de conexão:

   - [AWS: solução de problemas de conexões de serviço de endpoint]
   - [Amazon: solução de problemas de conectividade do Azure Private Link]

   Se não conseguir resolver os erros, atualize o tíquete de Suporte da Adobe Commerce para solicitar ajuda para estabelecer a conexão.

## Alterar configuração do PrivateLink

[Enviar um tíquete de suporte da Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) para alterar uma configuração existente do PrivateLink. Por exemplo, você pode solicitar alterações como as seguintes:

- Remova a conexão PrivateLink do ambiente de produção ou preparo do Adobe Commerce na infraestrutura em nuvem Pro.
- Altere o número da conta da plataforma Customer Cloud para acessar o serviço de ponto de extremidade Adobe.
- Adicionar ou remover conexões PrivateLink do VPC do Adobe para outros serviços de endpoint disponíveis no ambiente VPC do cliente.

## Configurar conexões bidirecionais do PrivateLink

O VPC do cliente deve ter os seguintes recursos disponíveis para suportar conexões PrivateLink bidirecionais:

- Um NLB (Balanceador de Carga de Rede)
- Uma configuração de serviço de ponto de extremidade que permite o acesso a um aplicativo ou serviço do VPC do cliente
- Um [endpoint da interface] (AWS) ou [terminal privado] (Azure) que permite que o Adobe se conecte aos serviços de endpoint hospedados em seu VPC

Se esses recursos não estiverem disponíveis no VPC do cliente, você deverá fazer logon na conta da plataforma em nuvem para adicionar a configuração.

- Console VPC do Amazon- `https://console.aws.amazon.com/vpc/`
- Portal do Azure- `https://portal.azure.com`

Consulte a documentação da sua plataforma na nuvem para obter instruções de configuração do PrivateLink:

- **Documentação do AWS PrivateLink**
   - [Criar um Balanceador de Carga de Rede]
   - [Criar uma configuração de serviço de ponto de extremidade]
   - [Criar um ponto de extremidade de interface]
   - [Ciclo de vida do endpoint da interface]

- **Documentação do Azure PrivateLink**
   - [Criar um balanceador de carga]
   - [Fluxo de trabalho do Link privado do Azure]

<!--Link definitions-->

[Aceitar e rejeitar solicitações de conexão de ponto de extremidade de interface]: https://docs.aws.amazon.com/vpc/latest/userguide/accept-reject-endpoint-requests.html
[Adicionar e remover permissões do serviço de ponto de extremidade]: https://docs.aws.amazon.com/vpc/latest/userguide/add-endpoint-service-permissions.html
[Amazon: solução de problemas de conectividade do Azure Private Link]: https://docs.microsoft.com/en-us/azure/private-link/troubleshoot-private-link-connectivity
[AWS: solução de problemas de conexões de serviço de endpoint]: https://aws.amazon.com/premiumsupport/knowledge-center/connect-endpoint-service-vpc/
[Fluxo de trabalho do Link privado do Azure]: https://docs.microsoft.com/en-us/azure/private-link/private-link-service-overview#workflow
[Criar um balanceador de carga]: https://docs.microsoft.com/en-us/azure/load-balancer/quickstart-load-balancer-standard-public-portal
[Criar um Balanceador de Carga de Rede]: https://docs.aws.amazon.com/elasticloadbalancing/latest/network/create-network-load-balancer.html
[Criar uma configuração de serviço de ponto de extremidade]: https://docs.aws.amazon.com/vpc/latest/userguide/create-endpoint-service.html
[Criar um ponto de extremidade de interface]: https://docs.aws.amazon.com/vpc/latest/userguide/vpce-interface.html#create-interface-endpoint
[interface endpoint lifecycle]: https://docs.aws.amazon.com/vpc/latest/userguide/vpce-interface.html#vpce-interface-lifecycle
[endpoint da interface]: https://docs.aws.amazon.com/vpc/latest/userguide/vpce-interface.html
[Gerenciar uma conexão de Ponto de Extremidade Privado]: https://docs.microsoft.com/en-us/azure/private-link/manage-private-endpoint
[Gerenciar solicitações de conexão]: https://docs.microsoft.com/en-us/azure/private-link/private-link-service-overview#manage-your-connection-requests
[terminal privado]: https://docs.microsoft.com/en-us/azure/private-link/private-endpoint-overview
