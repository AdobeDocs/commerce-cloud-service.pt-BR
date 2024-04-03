---
title: Propriedade do firewall
description: Consulte exemplos sobre como configurar a propriedade de firewall no arquivo de configuração do aplicativo Commerce.
feature: Cloud, Configuration, Security
exl-id: f169c008-c62a-41b7-a98d-cccd81c7291a
source-git-commit: 74d88560db3b65294673a1e1827f9cea098d707a
workflow-type: tm+mt
source-wordcount: '844'
ht-degree: 0%

---

# Propriedade do firewall

>[!IMPORTANT]
>
>Somente projetos iniciais

Para projetos iniciais, a variável `firewall` propriedade adiciona um _saída_ para o aplicativo. Esse firewall não afeta as solicitações recebidas. Define qual `tcp` solicitações de saída podem _sair_ um site do Adobe Commerce. Isso é chamado de filtragem de saída. O firewall de saída filtra o que pode sair ou escapar do site. Limitar o que pode escapar adiciona uma poderosa ferramenta de segurança ao servidor.

## Políticas de restrição padrão

O firewall fornece duas políticas padrão para controlar o tráfego externo: `allow` e `deny`. A variável `allow` política _permite_ todo o tráfego de saída por padrão. E a variável `deny` política _nega_ todo o tráfego de saída por padrão. Porém, quando você adiciona uma regra, a política padrão é substituída e o firewall bloqueia **all** tráfego de saída não permitido pela regra.

Para os planos iniciais, a política padrão é definida como `allow`. Essa configuração garante que todo o tráfego de saída atual permaneça desbloqueado até que você adicione suas regras de filtragem de saída. A política padrão pode ser definida como `deny` mediante pedido.

**Para verificar sua política padrão**:

```bash
magento-cloud p:curl --project PROJECT_ID /settings | grep -i outbound
```

A menos que você tenha solicitado `deny` para sua política, o comando deve mostrar sua política definida como `allow`:

```terminal
"outbound_restrictions_default_policy": "allow"
```

>[!NOTE]
>
>**Principais pontos**: ao adicionar uma regra de saída, você bloqueia todo o tráfego de saída, exceto os domínios, endereços IP ou portas adicionados à regra. Portanto, é importante ter uma lista de saída completa definida e testada antes de adicioná-la ao site de produção.

## Opções de firewall

O exemplo de configuração a seguir no campo `.magento.app.yaml` O arquivo mostra todas as `firewall` opções que podem ser usadas para adicionar regras à filtragem de saída.

```yaml
firewall:
    outbound:
        - # Common accessed domains
            domains:
                - newrelic.com
                - fastly.com
                - magento.com
                - magentocommerce.com
                - google.com
            ports:
                - 80
                - 443
            protocol: tcp # Can be omitted from rules.

        - # Adobe Stock integration
            domains:
                - account.adobe.com
                - stock.adobe.com
                - console.adobe.io
            ports:
                - 80
                - 443

        - # Payment services
            domains:
                - braintreepayments.com
                - paypal.com
            ports:
                - 80
                - 443

        - # Shipping services
            domains:
                - ups.com
                - usps.com
                - fedex.com
                - dhl.com
            ports:
                - 80
                - 443

        - # Vertex Integrated Address Cleansing
            domains:
                - mgcsconnect.vertexsmb.com
            ports:
                - 80
                - 443

        - # New Relic networks
            ips:
                - 162.247.240.0/22 # US region accounts
                - 185.221.84.0/22 # EU region accounts
            ports:
                - 443

        - # New Relic endpoints
            domains:
                - collector.newrelic.com, # US region accounts
                - collector.eu01.nr-data.net # EU region accounts
            ports:
                - 443

        - # Fastly IP ranges
            ips:
                - 23.235.32.0/20
                - 43.249.72.0/22
                - 103.244.50.0/24
                - 103.245.222.0/23
                - 103.245.224.0/24
                - 104.156.80.0/20
                - 146.75.0.0/16
                - 151.101.0.0/16
                - 157.52.64.0/18
                - 167.82.0.0/17
                - 167.82.128.0/20
                - 167.82.160.0/20
                - 167.82.224.0/20
                - 172.111.64.0/18
                - 185.31.16.0/22
                - 199.27.72.0/21
                - 199.232.0.0/16
            ports:
                - 80
                - 443
```

## Regras de filtragem de saída

As configurações de firewall de saída são formadas por regras. Você pode definir quantas regras forem necessárias. Os requisitos para as regras são os seguintes.

**Cada regra:**

- Deve começar com um hífen (`-`). Adicionar um comentário na mesma linha ajuda a documentar e separar visualmente uma regra da próxima.
- Deve definir pelo menos uma das seguintes opções: `domains`, `ips`ou `ports`.
- Deve usar o `tcp` protocolo. Como esse é o protocolo padrão para todas as regras, você pode omiti-lo da regra.
- Pode definir `domains` ou `ips`, mas não ambos na mesma regra.
- Pode incluir `yaml` comentários (`#`) e quebras de linha para organizar os domínios, endereços IP e portas permitidas.

Cada regra usa as seguintes propriedades:

### `domains`

A variável `domains` permite uma lista de nomes de domínio totalmente qualificados (FQDN).

Se uma regra definir `domains` mas não `ports`, o firewall permite solicitações de domínio em qualquer porta.

### `ips`

A variável `ips` permite uma lista de endereços IP na notação CIDR. Você pode especificar endereços IP únicos ou intervalos de endereços IP.

Para especificar um único endereço IP, adicione a variável `/32` Prefixo CIDR até o final do endereço IP:

```terminal
172.217.11.174/32  # google.com
```

Para especificar um intervalo de endereços IP, use o [Intervalo IP para CIDR](https://ipaddressguide.com/cidr) calculadora.

Se uma regra definir `ips` mas não `ports`, o firewall permite solicitações de IP em qualquer porta.

### `ports`

A variável `ports` permite uma lista de portas de 1 a 65535. Para a maioria das regras no exemplo, portas `80` e `443` permitir solicitações HTTP e HTTPS. Mas para o New Relic, as regras só permitem acesso a domínios e endereços IP na porta `443`, conforme recomendado na documentação do New Relic em [Tráfego de rede](https://docs.newrelic.com/docs/new-relic-solutions/get-started/networks/#agents).

Se uma regra apenas definir `ports`, o firewall permite o acesso a todos os domínios e endereços IP para as portas definidas.

>[!NOTE]
>
>Porta `25`, a porta SMTP para enviar email, está sempre bloqueada, sem exceção.

### `protocol`

Como mencionado, o TCP é o protocolo padrão e único permitido para regras. UDP e suas portas não são permitidas. Por esse motivo, você pode omitir a variável `protocol` em todas as regras. Se quiser incluí-lo mesmo assim, defina o valor como `tcp`, conforme mostrado na primeira regra do exemplo.

## Localizar nomes de domínio para permitir

Para ajudar a identificar os domínios que serão incluídos nas regras de filtragem de saída, use o comando a seguir para analisar as configurações do servidor `dns.log` e mostrar uma lista de todas as solicitações de DNS registradas pelo site:

```shell
awk '($5 ~/query/)' /var/log/dns.log | awk '{print $6}' | sort | uniq -c | sort -rn
```

Esse comando também mostra solicitações DNS que foram feitas, mas bloqueadas, por suas regras de filtragem de saída. A saída não mostra quais domínios foram bloqueados, somente se as solicitações foram feitas. A saída não mostra solicitações feitas usando um endereço IP.

```terminal
Example output:

97 magento.com
93 magentocommerce.com
88 google.com
70 metadata.google.internal.0
70 metadata.google.internal
65 newrelic.com
56 fastly.com
17 mcprod-0vunku5xn24ip.ap-4.magentosite.cloud
6 advancedreporting.rjmetrics.com
```

Os domínios, ao contrário dos endereços IP, normalmente são mais específicos e seguros para a filtragem de saída. Por exemplo, se você adicionar um endereço IP para um serviço que usa um CDN, estará permitindo o endereço IP para o CDN, que pode ser usado por centenas ou milhares de outros domínios. Com um endereço IP, você pode permitir acesso de saída a milhares de outros servidores.

## Testar regras de filtragem de saída

Depois de coletar e configurar as regras de acesso para os domínios e endereços IP de que seu site precisa, é hora de enviar e testar o.

Para testar as regras de filtragem de saída:

1. Criar um script de shell de `curl` comandos para acessar os domínios e endereços IP nas regras. Inclua comandos que testam o acesso a domínios e endereços IP que devem ser bloqueados.

1. Configurar um `post_deploy` gancho no seu `.magento.app.yaml` arquivo para executar o script.

1. Envie seu `firewall` e o script de teste para o seu `integration` filial.

1. Examine o `post_deploy` saída do seu `curl` comandos.

1. Refine suas `firewall` regras, atualize seu `curl` criar script, confirmar, enviar e repetir.

### `curl` exemplo de script

```shell
# curl-tests-for-egress-filtering.sh

# Use the -v option to display connection details

# Check domain access
curl -v newrelic.com
curl -v fastly.com
curl -v magento.com
curl -v magentocommerce.com
curl -v google.com
curl -v account.adobe.com
curl -v stock.adobe.com
curl -v console.adobe.io
curl -v braintreepayments.com
curl -v paypal.com
curl -v ups.com
curl -v usps.com
curl -v fedex.com
curl -v dhl.com
curl -v devdocs.magento.com

# Check domain denials
curl -v amazon.com
curl -v facebook.com
curl -v twitter.com

# IP address access
...

# IP address denials
...
```

### `post_deploy` exemplo

```yaml
hooks:
    build: |
        set -e
        php ./vendor/bin/ece-tools run scenario/build/generate.xml
        php ./vendor/bin/ece-tools run scenario/build/transfer.xml
    deploy: "php ./vendor/bin/ece-tools run scenario/deploy.xml\n"
    post_deploy: |
        set -e
        php ./vendor/bin/ece-tools run scenario/post-deploy.xml
        echo "[$(date)] post-deploy hook end"
        ./curl-tests-for-egress-filtering.sh
        echo "[$(date)] curl finished"
```
