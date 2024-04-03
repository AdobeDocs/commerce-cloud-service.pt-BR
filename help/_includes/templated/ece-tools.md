---
source-git-commit: 28aaae20fa03f31107bcd3fb569350a68842b152
workflow-type: tm+mt
source-wordcount: '3125'
ht-degree: 0%

---
# ece-tools

<!-- The template to render with above values -->
**Versão**: 2002.1.14

Esta referência contém 32 comandos disponíveis através do `ece-tools` ferramenta de linha de comando.
A lista inicial é gerada automaticamente usando o `ece-tools list` comando no Adobe Commerce na infraestrutura em nuvem.

>[!NOTE]
>
>Essa referência é gerada a partir da base de código do aplicativo. Para alterar o conteúdo, você pode atualizar o código-fonte para a implementação do comando correspondente no [codebase](https://github.com/magento/magento-cloud-cli) repositório e enviar suas alterações para revisão. Outra maneira é _Envie seus comentários_ (localize o link no canto superior direito). Para obter diretrizes de contribuição, consulte [Contribuições de código](https://developer.adobe.com/commerce/contributor/guides/code-contributions/).

## `build`

Compila o aplicativo.

```bash
ece-tools build
```

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--quiet`, `-q`

Não enviar nenhuma mensagem

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens: 1 para saída normal, 2 para saída mais detalhada e 3 para depuração

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--ansi`

Forçar saída ANSI

- Padrão: `false`
- Não aceita um valor

### `--no-ansi`

Desabilitar saída ANSI

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`, `-n`

Não faça nenhuma pergunta interativa

- Padrão: `false`
- Não aceita um valor


## `db-dump`

Cria backups do banco de dados.

```bash
ece-tools db-dump [-d|--remove-definers] [-a|--dump-directory DUMP-DIRECTORY] [--] [<databases>...]
```


### `databases`

Bancos de dados para backup. Valores Disponíveis: [vendas da cotação principal]. Se o valor do argumento não for especificado, os backups do banco de dados serão criados usando as credenciais armazenadas na `MAGENTO_CLOUD_RELATIONSHIP` variável de ambiente ou/e a variável `stage.deploy.DATABASE_CONFIGURATION` propriedade do arquivo de configuração .magento.env.yaml.

- Padrão: `[]`

- Matriz

### `--remove-definers`, `-d`

Remover definidores do dump do banco de dados

- Padrão: `false`
- Não aceita um valor

### `--dump-directory`, `-a`

Usar diretório alternativo para salvar o despejo

- Requer um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--quiet`, `-q`

Não enviar nenhuma mensagem

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens: 1 para saída normal, 2 para saída mais detalhada e 3 para depuração

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--ansi`

Forçar saída ANSI

- Padrão: `false`
- Não aceita um valor

### `--no-ansi`

Desabilitar saída ANSI

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`, `-n`

Não faça nenhuma pergunta interativa

- Padrão: `false`
- Não aceita um valor


## `deploy`

Implanta o aplicativo.

```bash
ece-tools deploy
```

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--quiet`, `-q`

Não enviar nenhuma mensagem

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens: 1 para saída normal, 2 para saída mais detalhada e 3 para depuração

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--ansi`

Forçar saída ANSI

- Padrão: `false`
- Não aceita um valor

### `--no-ansi`

Desabilitar saída ANSI

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`, `-n`

Não faça nenhuma pergunta interativa

- Padrão: `false`
- Não aceita um valor


## `help`

Exibir a ajuda de um comando

```bash
ece-tools help [--format FORMAT] [--raw] [--] [<command_name>]
```


### `command_name`

O nome do comando

- Padrão: `help`


### `--format`

O formato de saída (txt, xml, json ou md)

- Padrão: `txt`
- Requer um valor

### `--raw`

Para gerar a ajuda do comando raw

- Padrão: `false`
- Não aceita um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--quiet`, `-q`

Não enviar nenhuma mensagem

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens: 1 para saída normal, 2 para saída mais detalhada e 3 para depuração

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--ansi`

Forçar saída ANSI

- Padrão: `false`
- Não aceita um valor

### `--no-ansi`

Desabilitar saída ANSI

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`, `-n`

Não faça nenhuma pergunta interativa

- Padrão: `false`
- Não aceita um valor


## `list`

Listar comandos

```bash
ece-tools list [--raw] [--format FORMAT] [--] [<namespace>]
```


### `namespace`

O nome do namespace


### `--raw`

Para gerar a lista de comandos raw

- Padrão: `false`
- Não aceita um valor

### `--format`

O formato de saída (txt, xml, json ou md)

- Padrão: `txt`
- Requer um valor


## `patch`

Aplica patches personalizados.

```bash
ece-tools patch
```

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--quiet`, `-q`

Não enviar nenhuma mensagem

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens: 1 para saída normal, 2 para saída mais detalhada e 3 para depuração

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--ansi`

Forçar saída ANSI

- Padrão: `false`
- Não aceita um valor

### `--no-ansi`

Desabilitar saída ANSI

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`, `-n`

Não faça nenhuma pergunta interativa

- Padrão: `false`
- Não aceita um valor


## `post-deploy`

Executa operações após a implantação.

```bash
ece-tools post-deploy
```

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--quiet`, `-q`

Não enviar nenhuma mensagem

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens: 1 para saída normal, 2 para saída mais detalhada e 3 para depuração

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--ansi`

Forçar saída ANSI

- Padrão: `false`
- Não aceita um valor

### `--no-ansi`

Desabilitar saída ANSI

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`, `-n`

Não faça nenhuma pergunta interativa

- Padrão: `false`
- Não aceita um valor


## `run`

Executar cenário(s).

```bash
ece-tools run <scenario>...
```


### `scenario`

Cenário(s)

- Padrão: `[]`

- Obrigatório
- Matriz

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--quiet`, `-q`

Não enviar nenhuma mensagem

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens: 1 para saída normal, 2 para saída mais detalhada e 3 para depuração

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--ansi`

Forçar saída ANSI

- Padrão: `false`
- Não aceita um valor

### `--no-ansi`

Desabilitar saída ANSI

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`, `-n`

Não faça nenhuma pergunta interativa

- Padrão: `false`
- Não aceita um valor


## `backup:list`

Mostra a lista de arquivos de backup.

```bash
ece-tools backup:list
```

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--quiet`, `-q`

Não enviar nenhuma mensagem

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens: 1 para saída normal, 2 para saída mais detalhada e 3 para depuração

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--ansi`

Forçar saída ANSI

- Padrão: `false`
- Não aceita um valor

### `--no-ansi`

Desabilitar saída ANSI

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`, `-n`

Não faça nenhuma pergunta interativa

- Padrão: `false`
- Não aceita um valor


## `backup:restore`

Restaure arquivos de configuração importantes. Execute backup:list para mostrar a lista de arquivos de backup.

```bash
ece-tools backup:restore [-f|--force] [--file [FILE]]
```

### `--force`, `-f`

Substituir arquivos existentes durante a restauração de um backup

- Padrão: `false`
- Não aceita um valor

### `--file`

Um caminho de recuperação de arquivo específico

- Aceita um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--quiet`, `-q`

Não enviar nenhuma mensagem

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens: 1 para saída normal, 2 para saída mais detalhada e 3 para depuração

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--ansi`

Forçar saída ANSI

- Padrão: `false`
- Não aceita um valor

### `--no-ansi`

Desabilitar saída ANSI

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`, `-n`

Não faça nenhuma pergunta interativa

- Padrão: `false`
- Não aceita um valor


## `build:generate`

Gera todos os arquivos necessários para o estágio de criação.

```bash
ece-tools build:generate
```

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--quiet`, `-q`

Não enviar nenhuma mensagem

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens: 1 para saída normal, 2 para saída mais detalhada e 3 para depuração

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--ansi`

Forçar saída ANSI

- Padrão: `false`
- Não aceita um valor

### `--no-ansi`

Desabilitar saída ANSI

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`, `-n`

Não faça nenhuma pergunta interativa

- Padrão: `false`
- Não aceita um valor


## `build:transfer`

Transfere os arquivos gerados para o diretório init.

```bash
ece-tools build:transfer
```

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--quiet`, `-q`

Não enviar nenhuma mensagem

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens: 1 para saída normal, 2 para saída mais detalhada e 3 para depuração

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--ansi`

Forçar saída ANSI

- Padrão: `false`
- Não aceita um valor

### `--no-ansi`

Desabilitar saída ANSI

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`, `-n`

Não faça nenhuma pergunta interativa

- Padrão: `false`
- Não aceita um valor


## `cloud:config:create`

Cria um `.magento.env.yaml` com a configuração de variável de build, implantação e pós-implantação especificada. Substitui qualquer existente `.magento,.env.yaml` arquivo.

```bash
ece-tools cloud:config:create <configuration>
```


### `configuration`

Configuração no formato JSON

- Obrigatório

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--quiet`, `-q`

Não enviar nenhuma mensagem

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens: 1 para saída normal, 2 para saída mais detalhada e 3 para depuração

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--ansi`

Forçar saída ANSI

- Padrão: `false`
- Não aceita um valor

### `--no-ansi`

Desabilitar saída ANSI

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`, `-n`

Não faça nenhuma pergunta interativa

- Padrão: `false`
- Não aceita um valor


## `cloud:config:update`

Atualiza o existente `.magento.env.yaml` com a configuração especificada. Cria `.magento.env.yaml` arquivo se ele não existir.

```bash
ece-tools cloud:config:update <configuration>
```


### `configuration`

Configuração no formato JSON

- Obrigatório

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--quiet`, `-q`

Não enviar nenhuma mensagem

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens: 1 para saída normal, 2 para saída mais detalhada e 3 para depuração

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--ansi`

Forçar saída ANSI

- Padrão: `false`
- Não aceita um valor

### `--no-ansi`

Desabilitar saída ANSI

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`, `-n`

Não faça nenhuma pergunta interativa

- Padrão: `false`
- Não aceita um valor


## `cloud:config:validate`

Valida `.magento.env.yaml` arquivo de configuração

```bash
ece-tools cloud:config:validate
```

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--quiet`, `-q`

Não enviar nenhuma mensagem

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens: 1 para saída normal, 2 para saída mais detalhada e 3 para depuração

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--ansi`

Forçar saída ANSI

- Padrão: `false`
- Não aceita um valor

### `--no-ansi`

Desabilitar saída ANSI

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`, `-n`

Não faça nenhuma pergunta interativa

- Padrão: `false`
- Não aceita um valor


## `config:dump`

Configuração de despejo para implantação de conteúdo estático.

```bash
ece-tools config:dump
```


```bash
ece-tools dump
```

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--quiet`, `-q`

Não enviar nenhuma mensagem

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens: 1 para saída normal, 2 para saída mais detalhada e 3 para depuração

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--ansi`

Forçar saída ANSI

- Padrão: `false`
- Não aceita um valor

### `--no-ansi`

Desabilitar saída ANSI

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`, `-n`

Não faça nenhuma pergunta interativa

- Padrão: `false`
- Não aceita um valor


## `cron:disable`

Desative todos os processos do Magento cron e encerre todos os processos em execução.

```bash
ece-tools cron:disable
```

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--quiet`, `-q`

Não enviar nenhuma mensagem

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens: 1 para saída normal, 2 para saída mais detalhada e 3 para depuração

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--ansi`

Forçar saída ANSI

- Padrão: `false`
- Não aceita um valor

### `--no-ansi`

Desabilitar saída ANSI

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`, `-n`

Não faça nenhuma pergunta interativa

- Padrão: `false`
- Não aceita um valor


## `cron:enable`

Habilita processos de cron Magento.

```bash
ece-tools cron:enable
```

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--quiet`, `-q`

Não enviar nenhuma mensagem

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens: 1 para saída normal, 2 para saída mais detalhada e 3 para depuração

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--ansi`

Forçar saída ANSI

- Padrão: `false`
- Não aceita um valor

### `--no-ansi`

Desabilitar saída ANSI

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`, `-n`

Não faça nenhuma pergunta interativa

- Padrão: `false`
- Não aceita um valor


## `cron:kill`

Encerra todos os processos Magento cron.

```bash
ece-tools cron:kill
```

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--quiet`, `-q`

Não enviar nenhuma mensagem

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens: 1 para saída normal, 2 para saída mais detalhada e 3 para depuração

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--ansi`

Forçar saída ANSI

- Padrão: `false`
- Não aceita um valor

### `--no-ansi`

Desabilitar saída ANSI

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`, `-n`

Não faça nenhuma pergunta interativa

- Padrão: `false`
- Não aceita um valor


## `cron:unlock`

Desbloqueie trabalhos cron que ficaram no estado &quot;em execução&quot;.

```bash
ece-tools cron:unlock [--job-code [JOB-CODE]]
```

### `--job-code`

Código do trabalho do Cron a ser desbloqueado.

- Padrão: `[]`
- Aceita vários valores

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--quiet`, `-q`

Não enviar nenhuma mensagem

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens: 1 para saída normal, 2 para saída mais detalhada e 3 para depuração

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--ansi`

Forçar saída ANSI

- Padrão: `false`
- Não aceita um valor

### `--no-ansi`

Desabilitar saída ANSI

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`, `-n`

Não faça nenhuma pergunta interativa

- Padrão: `false`
- Não aceita um valor


## `dev:generate:schema-error`

Gera o arquivo dist/error-codes.md do arquivo schema.error.yaml.

```bash
ece-tools dev:generate:schema-error
```

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--quiet`, `-q`

Não enviar nenhuma mensagem

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens: 1 para saída normal, 2 para saída mais detalhada e 3 para depuração

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--ansi`

Forçar saída ANSI

- Padrão: `false`
- Não aceita um valor

### `--no-ansi`

Desabilitar saída ANSI

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`, `-n`

Não faça nenhuma pergunta interativa

- Padrão: `false`
- Não aceita um valor


## `dev:git:update-composer`

Atualiza o compositor para implantação do Git.

```bash
ece-tools dev:git:update-composer
```

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--quiet`, `-q`

Não enviar nenhuma mensagem

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens: 1 para saída normal, 2 para saída mais detalhada e 3 para depuração

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--ansi`

Forçar saída ANSI

- Padrão: `false`
- Não aceita um valor

### `--no-ansi`

Desabilitar saída ANSI

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`, `-n`

Não faça nenhuma pergunta interativa

- Padrão: `false`
- Não aceita um valor


## `env:config:show`

Exibir variáveis de ambiente de configuração de nuvem codificadas.

```bash
ece-tools env:config:show [<variable>...]
```


### `variable`

Variáveis de ambiente a serem exibidas, opções possíveis: serviços, rotas, variáveis

- Padrão: `[]`

- Matriz

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--quiet`, `-q`

Não enviar nenhuma mensagem

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens: 1 para saída normal, 2 para saída mais detalhada e 3 para depuração

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--ansi`

Forçar saída ANSI

- Padrão: `false`
- Não aceita um valor

### `--no-ansi`

Desabilitar saída ANSI

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`, `-n`

Não faça nenhuma pergunta interativa

- Padrão: `false`
- Não aceita um valor


## `error:show`

Exibe informações sobre o erro por id de erro ou informações sobre todos os erros da última implantação.

```bash
ece-tools error:show [-j|--json] [--] [<error-code>]
```


### `error-code`

Código de erro, se não for passado o comando exibir informações sobre todos os erros da última implantação


### `--json`, `-j`

Usado para obter resultado no formato JSON

- Padrão: `false`
- Não aceita um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--quiet`, `-q`

Não enviar nenhuma mensagem

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens: 1 para saída normal, 2 para saída mais detalhada e 3 para depuração

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--ansi`

Forçar saída ANSI

- Padrão: `false`
- Não aceita um valor

### `--no-ansi`

Desabilitar saída ANSI

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`, `-n`

Não faça nenhuma pergunta interativa

- Padrão: `false`
- Não aceita um valor


## `module:refresh`

Atualiza a configuração para ativar módulos recém-adicionados.

```bash
ece-tools module:refresh
```

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--quiet`, `-q`

Não enviar nenhuma mensagem

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens: 1 para saída normal, 2 para saída mais detalhada e 3 para depuração

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--ansi`

Forçar saída ANSI

- Padrão: `false`
- Não aceita um valor

### `--no-ansi`

Desabilitar saída ANSI

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`, `-n`

Não faça nenhuma pergunta interativa

- Padrão: `false`
- Não aceita um valor


## `schema:generate`

Gera o arquivo *.dist do esquema.

```bash
ece-tools schema:generate
```

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--quiet`, `-q`

Não enviar nenhuma mensagem

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens: 1 para saída normal, 2 para saída mais detalhada e 3 para depuração

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--ansi`

Forçar saída ANSI

- Padrão: `false`
- Não aceita um valor

### `--no-ansi`

Desabilitar saída ANSI

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`, `-n`

Não faça nenhuma pergunta interativa

- Padrão: `false`
- Não aceita um valor


## `wizard:ideal-state`

Verifica o estado ideal de configuração.

```bash
ece-tools wizard:ideal-state
```

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--quiet`, `-q`

Não enviar nenhuma mensagem

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens: 1 para saída normal, 2 para saída mais detalhada e 3 para depuração

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--ansi`

Forçar saída ANSI

- Padrão: `false`
- Não aceita um valor

### `--no-ansi`

Desabilitar saída ANSI

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`, `-n`

Não faça nenhuma pergunta interativa

- Padrão: `false`
- Não aceita um valor


## `wizard:master-slave`

Verifica a configuração do master-slave.

```bash
ece-tools wizard:master-slave
```

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--quiet`, `-q`

Não enviar nenhuma mensagem

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens: 1 para saída normal, 2 para saída mais detalhada e 3 para depuração

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--ansi`

Forçar saída ANSI

- Padrão: `false`
- Não aceita um valor

### `--no-ansi`

Desabilitar saída ANSI

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`, `-n`

Não faça nenhuma pergunta interativa

- Padrão: `false`
- Não aceita um valor


## `wizard:scd-on-build`

Verifica o SCD na configuração da build.

```bash
ece-tools wizard:scd-on-build
```

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--quiet`, `-q`

Não enviar nenhuma mensagem

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens: 1 para saída normal, 2 para saída mais detalhada e 3 para depuração

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--ansi`

Forçar saída ANSI

- Padrão: `false`
- Não aceita um valor

### `--no-ansi`

Desabilitar saída ANSI

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`, `-n`

Não faça nenhuma pergunta interativa

- Padrão: `false`
- Não aceita um valor


## `wizard:scd-on-demand`

Verifica a configuração de SCD por demanda.

```bash
ece-tools wizard:scd-on-demand
```

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--quiet`, `-q`

Não enviar nenhuma mensagem

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens: 1 para saída normal, 2 para saída mais detalhada e 3 para depuração

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--ansi`

Forçar saída ANSI

- Padrão: `false`
- Não aceita um valor

### `--no-ansi`

Desabilitar saída ANSI

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`, `-n`

Não faça nenhuma pergunta interativa

- Padrão: `false`
- Não aceita um valor


## `wizard:scd-on-deploy`

Verifica o SCD na configuração de implantação.

```bash
ece-tools wizard:scd-on-deploy
```

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--quiet`, `-q`

Não enviar nenhuma mensagem

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens: 1 para saída normal, 2 para saída mais detalhada e 3 para depuração

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--ansi`

Forçar saída ANSI

- Padrão: `false`
- Não aceita um valor

### `--no-ansi`

Desabilitar saída ANSI

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`, `-n`

Não faça nenhuma pergunta interativa

- Padrão: `false`
- Não aceita um valor


## `wizard:split-db-state`

Verifica a capacidade de dividir o banco de dados e se o banco de dados já foi dividido ou não.

```bash
ece-tools wizard:split-db-state
```

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--quiet`, `-q`

Não enviar nenhuma mensagem

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens: 1 para saída normal, 2 para saída mais detalhada e 3 para depuração

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--ansi`

Forçar saída ANSI

- Padrão: `false`
- Não aceita um valor

### `--no-ansi`

Desabilitar saída ANSI

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`, `-n`

Não faça nenhuma pergunta interativa

- Padrão: `false`
- Não aceita um valor

