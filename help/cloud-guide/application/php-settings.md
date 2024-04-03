---
title: Configurações do PHP
description: Saiba mais sobre as configurações ideais do PHP para a configuração de aplicativos do Commerce na infraestrutura em nuvem.
feature: Cloud, Configuration, Extensions
exl-id: b4180265-f7a1-48e4-8c23-27835253e171
source-git-commit: 9b3772cf640ebc56063434e1aa8acb1ec51dc63c
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 0%

---

# Configurações do PHP

Você pode escolher qual [versão do PHP](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/system-requirements.html) para executar no seu `.magento.app.yaml` arquivo:

```yaml
name: mymagento
type: php:<version>
```

>[!TIP]
>
>Se estiver atualizando para o PHP 8.1 e posterior, remova o JSON do [`runtime: extensions:` propriedade](properties.md#runtime) no `.magento.app.yaml` arquivo e reimplantar. A extensão JSON vem instalada no ambiente de nuvem desde o PHP 8.0.

## Configurar PHP

Você pode personalizar as configurações do PHP para o seu ambiente usando um `php.ini` arquivo anexado à configuração mantida pelo Adobe Commerce.

No repositório, adicione o `php.ini` para a raiz do aplicativo (a raiz do repositório).

>[!TIP]
>
>A configuração incorreta das configurações do PHP pode causar problemas, portanto, somente administradores avançados devem definir essas opções.

### Aumentar limite de memória do PHP

Para aumentar o limite de memória do PHP, adicione a seguinte configuração ao `php.ini` arquivo:

```ini
memory_limit = 1G
```

Para depuração, aumente o valor para 2G.

### Otimizar a configuração do realpath_cache

Defina o seguinte `realpath_cache` para melhorar o desempenho dos aplicativos.

```conf
;
; Increase realpath cache size
;
realpath_cache_size = 10M

;
; Increase realpath cache ttl
;
realpath_cache_ttl = 7200
```

Essas configurações permitem que processos PHP armazenem em cache caminhos para arquivos em vez de pesquisá-los para cada carregamento de página. Consulte [Ajuste de desempenho](https://www.php.net/manual/en/ini.core.php) na documentação do PHP.

>[!NOTE]
>
>Para obter uma lista das definições de configuração do PHP recomendadas, consulte [Configurações necessárias do PHP](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/prerequisites/php-settings.html) no _Guia de instalação_.

### Verificar configurações personalizadas de PHP

Depois de pressionar o `php.ini` alterações no ambiente da nuvem, você pode verificar se a configuração personalizada do PHP foi adicionada ao seu ambiente. Por exemplo, use SSH para fazer logon no ambiente remoto e exibir o arquivo usando algo semelhante ao seguinte:

```bash
cat /etc/php/<php-version>/fpm/php.ini
```

>[!WARNING]
>
>Se você usar o Cloud Docker for Commerce para desenvolvimento local, consulte [Contêineres de serviço do Docker](https://developer.adobe.com/commerce/cloud-tools/docker/containers/service/#fpm-container) para obter informações sobre como usar um personalizado `php.ini` em um ambiente Docker.

## Habilitar extensões

Você pode ativar ou desativar extensões PHP no `runtime:extension` seção. Além disso, as extensões especificadas ficam disponíveis nos contêineres PHP do Docker.

>[!IMPORTANT]
>
>Antes de habilitar extensões, é importante entender que a versão do PHP deve ser compatível com o sistema operacional que hospeda o projeto. Seu ambiente de projeto pode exigir uma atualização do SO pela equipe de infraestrutura antes de você poder continuar.

Exemplo em `.magento.app.yaml` arquivo:

```yaml
runtime:
    extensions:
        - sockets
        - sodium
        - ssh2
    disabled_extensions:
        - bcmath
        - bz2
        - calendar
        - exif
```

Use SSH para fazer login em um ambiente e listar as extensões do PHP.

```bash
php -m
```

Para obter detalhes sobre uma extensão específica do PHP, consulte [Lista de extensões do PHP](https://www.php.net/manual/en/extensions.alphabetical.php).

A tabela a seguir mostra as extensões compatíveis do PHP ao implantar o Adobe Commerce na plataforma na nuvem.

| Extensões padrão | Extensões instaladas<br>que não pode ser desinstalado | Extensões que podem ser instalados<br>e desinstalado conforme necessário |
| ------------------ | --------------------- | --------------------- |
| `bcmath`<br>`bz2`<br>`calendar`<br>`exif`<br>`gd`<br>`gettext`<br> `intl`<br> `mysqli`<br> `openswoole`<br> `pcntl`<br> `pdo_mysql`<br> `soap`<br> `sockets`<br>  `sysvmsg`<br> `sysvsem`<br> `sysvshm`<br> `opcache`<br> `zip` | `ctype`<br> `curl`<br>`date`<br> `dom`<br> `fileinfo`<br> `filter`<br> `ftp`<br> `hash`<br> `iconv`<br> `json`<br> `mbstring`<br> `mysqlnd`<br> `openssl`<br> `pcre`<br> `pdo`<br> `pdo_sqlite`<br> `phar`<br>`posix`<br> `readline`<br> `session`<br> `sqlite3`<br> `tokenizer`<br> `xml`<br> `xmlreader`<br> `xmlwriter`<br> | `geoip`<br>`gmp`<br> `igbinary`<br> `imagick`<br> `imap`<br> `ioncube` <br>`ldap`<br> `mailparse`<br> `mcrypt`<br> `msgpack`<br> `mysqli`<br> `oauth`<br> `pdo_mysql`<br> `propro`<br> `pspell`<br> `raphf`<br> `recode`<br> `redis`<br> `shmop` `sockets`<br> `sodium`<br> `ssh2`<br>`tidy`<br> `xdebug`<br> `xmlrpc`<br> `xsl`<br> `yaml` |

Os requisitos do módulo do PHP estão vinculados à versão do Adobe Commerce. Consulte [Requisitos do PHP](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/prerequisites/php-settings.html).

### Suporte à extensão

Para projetos Pro, as seguintes extensões exigem suporte adicional para instalação:

- `sourceguardian`

Por exemplo, para configurar o PHP para executar somente scripts protegidos pelo SourceGuardian em todos os ambientes, a seguinte opção deve ser configurada na variável `php.ini` arquivo:

```ini
[SourceGuardian]
sourceguardian.restrict_unencoded = "1"
```

Consulte [seção 3.5 da documentação do SourceGuardian](https://sourceguardian.com/demofiles/files/SourceGuardian%20for%20Linux%20User%20Manual.pdf). _Este é um link para um PDF_.

[Enviar um tíquete de suporte da Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) para obter ajuda com a instalação dessas extensões PHP em todos os ambientes de produção e ambientes de preparo profissional. Inclua o atualizado `.magento/services.yaml` arquivo, `.magento.app.yaml` arquivo com a versão atualizada do PHP e quaisquer extensões adicionais do PHP. Para alterações em um ambiente de Produção em tempo real, você deve fornecer um aviso mínimo de 48 horas. Pode levar até 48 horas para a equipe de infraestrutura da nuvem atualizar seu projeto.

>[!WARNING]
>
>O PHP compilado com debug não é suportado e o teste pode entrar em conflito com [!DNL XDebug] ou [!DNL XHProf]. Desative essas extensões ao ativar o teste. O teste entra em conflito com algumas extensões PHP como [!DNL Pinba] ou IonCube.
