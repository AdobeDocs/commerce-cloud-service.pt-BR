---
title: Manipuladores de log
description: Saiba como configurar manipuladores de log para o Adobe Commerce na infraestrutura da nuvem.
feature: Cloud, Logs, Configuration
role: Developer
exl-id: d3be7b6d-5778-4c32-865b-31bdb2852a23
source-git-commit: f8e35ecff4bcafda874a87642348e2d2bff5247b
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---

# Manipuladores de log

Você pode configurar manipuladores de log para enviar mensagens a um servidor de log remoto. Um manipulador de log envia registros de criação e implantação para outros sistemas, de forma semelhante à maneira como você envia registros para o Slack e email. Você pode ativar um _syslog_ manipulador, que é ideal para registrar mensagens relacionadas ao hardware, ou um manipulador GELF (Extended Log Format) de Graylog, que é ideal para registrar mensagens de aplicativos de software.

O exemplo a seguir configura esses dois manipuladores adicionando a configuração ao `.magento.env.yaml` arquivo. Para o nível mínimo de registro (`min_level`), consulte [Níveis de log](#log-levels).

```yaml
log:
  syslog:
    ident: "<syslog-ident>"
    facility: 8 # https://php.net/manual/en/network.constants.php
    min_level: "info"
    logopts: <syslog-logopts>

  syslog_udp:
    host: "<syslog-host>"
    port: <syslog-port>
    facility: 8  # https://php.net/manual/en/network.constants.php
    ident: "<syslog-ident>"
    min_level: "info"

  gelf:
    min_level: "info"
    use_default_formatter: true
    additional: # Some additional information for each log message
      project: "<some-project-id>"
      app_id: "<some-app-id>"
    transport:
      http:
        host: "<http-host>"
        port: <http-port>
        path: "<http-path>"
        connection_timeout: 60
      tcp:
        host: "<tcp-host>"
        port: <tcp-port>
        connection_timeout: 60
      udp:
        host: "<udp-host>"
        port: <udp-port>
        chunk_size: 1024
```

## Níveis de log

Os níveis de log determinam o nível de detalhes nas mensagens de notificação. As seguintes categorias de nível de log incluem todos os níveis de log abaixo dele. Por exemplo, uma variável `debug` O nível inclui o registro de cada nível, enquanto uma `alert` nível mostra apenas alertas e emergências.

- **depurar**— detailed debug information
- **informações**—eventos interessantes, como um login de usuário ou log SQL
- **aviso**— eventos normais, mas significativos
- **aviso**—ocorrências excepcionais que não sejam erros, como o uso de uma API obsoleta ou o uso inadequado de uma API
- **erro**—erros de tempo de execução que não exigem ação imediata
- **crítico**— condições críticas, como um componente indisponível do aplicativo ou uma exceção inesperada
- **alerta**—ação imediata necessária — como um site inativo ou o banco de dados indisponível — que aciona um alerta de SMS
- **emergência**— system está inutilizável
