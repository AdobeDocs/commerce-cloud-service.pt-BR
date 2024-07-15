---
source-git-commit: 6d8c082d78259f8f7adb0fb7f11ff4fcdb234124
workflow-type: tm+mt
source-wordcount: '4030'
ht-degree: 0%

---
# ece-tools

<!-- The template to render with above values -->
**Versão**: 2002.1.18

Esta referência contém 34 comandos disponíveis através da ferramenta de linha de comando `ece-tools`.
A lista inicial é gerada automaticamente usando o comando `ece-tools list` no Adobe Commerce na infraestrutura em nuvem.

>[!NOTE]
>
>Essa referência é gerada a partir da base de código do aplicativo. Para alterar o conteúdo, você pode atualizar o código-fonte para a implementação de comando correspondente no repositório [codebase](https://github.com/magento/magento-cloud-cli) e enviar suas alterações para revisão. Outra maneira é _Fornecer comentários_ (localizar o link no canto superior direito). Para obter as diretrizes de contribuição, consulte [Contribuições de código](https://developer.adobe.com/commerce/contributor/guides/code-contributions/).

## `_complete`

Comando interno para fornecer sugestões de conclusão de shell

```bash
ece-tools _complete [-s|--shell SHELL] [-i|--input INPUT] [-c|--current CURRENT] [-a|--api-version API-VERSION] [-S|--symfony SYMFONY]
```

### `--shell`, `-s`

O tipo de concha (&quot;bash&quot;, &quot;fish&quot;, &quot;zsh&quot;)

- Requer um valor

### `--input`, `-i`

Uma matriz de tokens de entrada (por exemplo, COMP_WORDS ou argv)

- Padrão: `[]`
- Requer um valor

### `--current`, `-c`

O índice da matriz &quot;input&quot; na qual o cursor está (por exemplo, COMP_CWORD)

- Requer um valor

### `--api-version`, `-a`

A versão da API do script de conclusão

- Requer um valor

### `--symfony`, `-S`

obsoleto

- Requer um valor

### `--help`, `-h`

Exibe a ajuda para o comando fornecido. Quando nenhum comando é fornecido, exibir ajuda para o comando de lista

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

Forçar (ou desativar — no- ansi) a saída ANSI

- Não aceita um valor

### `--no-ansi`

Negar a opção &quot;—ansi&quot;

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`, `-n`

Não faça nenhuma pergunta interativa

- Padrão: `false`
- Não aceita um valor


## `build`

Compila o aplicativo.

```bash
ece-tools build
```

### `--help`, `-h`

Exibe a ajuda para o comando fornecido. Quando nenhum comando é fornecido, exibir ajuda para o comando de lista

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

Forçar (ou desativar — no- ansi) a saída ANSI

- Não aceita um valor

### `--no-ansi`

Negar a opção &quot;—ansi&quot;

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`, `-n`

Não faça nenhuma pergunta interativa

- Padrão: `false`
- Não aceita um valor


## `completion`

Despejar o script de conclusão do shell

```bash
ece-tools completion [--debug] [--] [<shell>]
```


### `shell`

O tipo de shell (por exemplo, &quot;bash&quot;), o valor do var env &quot;$SHELL&quot; será usado se isso não for fornecido


### `--debug`

Analisar o log de depuração da conclusão

- Padrão: `false`
- Não aceita um valor

### `--help`, `-h`

Exibe a ajuda para o comando fornecido. Quando nenhum comando é fornecido, exibir ajuda para o comando de lista

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

Forçar (ou desativar — no- ansi) a saída ANSI

- Não aceita um valor

### `--no-ansi`

Negar a opção &quot;—ansi&quot;

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

Bancos de dados para backup. Valores Disponíveis: [vendas da cotação principal]. Se o valor do argumento não for especificado, os backups do banco de dados serão criados usando as credenciais armazenadas na variável de ambiente `MAGENTO_CLOUD_RELATIONSHIP` ou/e a propriedade `stage.deploy.DATABASE_CONFIGURATION` do arquivo de configuração .magento.env.yaml.

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

Exibe a ajuda para o comando fornecido. Quando nenhum comando é fornecido, exibir ajuda para o comando de lista

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

Forçar (ou desativar — no- ansi) a saída ANSI

- Não aceita um valor

### `--no-ansi`

Negar a opção &quot;—ansi&quot;

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

Exibe a ajuda para o comando fornecido. Quando nenhum comando é fornecido, exibir ajuda para o comando de lista

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

Forçar (ou desativar — no- ansi) a saída ANSI

- Não aceita um valor

### `--no-ansi`

Negar a opção &quot;—ansi&quot;

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

Exibe a ajuda para o comando fornecido. Quando nenhum comando é fornecido, exibir ajuda para o comando de lista

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

Forçar (ou desativar — no- ansi) a saída ANSI

- Não aceita um valor

### `--no-ansi`

Negar a opção &quot;—ansi&quot;

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`, `-n`

Não faça nenhuma pergunta interativa

- Padrão: `false`
- Não aceita um valor


## `list`

Listar comandos

```bash
ece-tools list [--raw] [--format FORMAT] [--short] [--] [<namespace>]
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

### `--short`

Para ignorar a descrição dos argumentos dos comandos

- Padrão: `false`
- Não aceita um valor

### `--help`, `-h`

Exibe a ajuda para o comando fornecido. Quando nenhum comando é fornecido, exibir ajuda para o comando de lista

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

Forçar (ou desativar — no- ansi) a saída ANSI

- Não aceita um valor

### `--no-ansi`

Negar a opção &quot;—ansi&quot;

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`, `-n`

Não faça nenhuma pergunta interativa

- Padrão: `false`
- Não aceita um valor


## `patch`

Aplica patches personalizados.

```bash
ece-tools patch
```

### `--help`, `-h`

Exibe a ajuda para o comando fornecido. Quando nenhum comando é fornecido, exibir ajuda para o comando de lista

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

Forçar (ou desativar — no- ansi) a saída ANSI

- Não aceita um valor

### `--no-ansi`

Negar a opção &quot;—ansi&quot;

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

Exibe a ajuda para o comando fornecido. Quando nenhum comando é fornecido, exibir ajuda para o comando de lista

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

Forçar (ou desativar — no- ansi) a saída ANSI

- Não aceita um valor

### `--no-ansi`

Negar a opção &quot;—ansi&quot;

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

Exibe a ajuda para o comando fornecido. Quando nenhum comando é fornecido, exibir ajuda para o comando de lista

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

Forçar (ou desativar — no- ansi) a saída ANSI

- Não aceita um valor

### `--no-ansi`

Negar a opção &quot;—ansi&quot;

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

Exibe a ajuda para o comando fornecido. Quando nenhum comando é fornecido, exibir ajuda para o comando de lista

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

Forçar (ou desativar — no- ansi) a saída ANSI

- Não aceita um valor

### `--no-ansi`

Negar a opção &quot;—ansi&quot;

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

Exibe a ajuda para o comando fornecido. Quando nenhum comando é fornecido, exibir ajuda para o comando de lista

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

Forçar (ou desativar — no- ansi) a saída ANSI

- Não aceita um valor

### `--no-ansi`

Negar a opção &quot;—ansi&quot;

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

Exibe a ajuda para o comando fornecido. Quando nenhum comando é fornecido, exibir ajuda para o comando de lista

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

Forçar (ou desativar — no- ansi) a saída ANSI

- Não aceita um valor

### `--no-ansi`

Negar a opção &quot;—ansi&quot;

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

Exibe a ajuda para o comando fornecido. Quando nenhum comando é fornecido, exibir ajuda para o comando de lista

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

Forçar (ou desativar — no- ansi) a saída ANSI

- Não aceita um valor

### `--no-ansi`

Negar a opção &quot;—ansi&quot;

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`, `-n`

Não faça nenhuma pergunta interativa

- Padrão: `false`
- Não aceita um valor


## `cloud:config:create`

Cria um arquivo `.magento.env.yaml` com a configuração de variável de compilação, implantação e pós-implantação especificada. Substitui qualquer arquivo `.magento,.env.yaml` existente.

```bash
ece-tools cloud:config:create <configuration>
```


### `configuration`

Configuração no formato JSON

- Obrigatório

### `--help`, `-h`

Exibe a ajuda para o comando fornecido. Quando nenhum comando é fornecido, exibir ajuda para o comando de lista

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

Forçar (ou desativar — no- ansi) a saída ANSI

- Não aceita um valor

### `--no-ansi`

Negar a opção &quot;—ansi&quot;

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`, `-n`

Não faça nenhuma pergunta interativa

- Padrão: `false`
- Não aceita um valor


## `cloud:config:update`

Atualiza o arquivo `.magento.env.yaml` existente com a configuração especificada. Cria o arquivo `.magento.env.yaml` se ele não existir.

```bash
ece-tools cloud:config:update <configuration>
```


### `configuration`

Configuração no formato JSON

- Obrigatório

### `--help`, `-h`

Exibe a ajuda para o comando fornecido. Quando nenhum comando é fornecido, exibir ajuda para o comando de lista

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

Forçar (ou desativar — no- ansi) a saída ANSI

- Não aceita um valor

### `--no-ansi`

Negar a opção &quot;—ansi&quot;

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`, `-n`

Não faça nenhuma pergunta interativa

- Padrão: `false`
- Não aceita um valor


## `cloud:config:validate`

Valida o arquivo de configuração `.magento.env.yaml`

```bash
ece-tools cloud:config:validate
```

### `--help`, `-h`

Exibe a ajuda para o comando fornecido. Quando nenhum comando é fornecido, exibir ajuda para o comando de lista

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

Forçar (ou desativar — no- ansi) a saída ANSI

- Não aceita um valor

### `--no-ansi`

Negar a opção &quot;—ansi&quot;

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

Exibe a ajuda para o comando fornecido. Quando nenhum comando é fornecido, exibir ajuda para o comando de lista

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

Forçar (ou desativar — no- ansi) a saída ANSI

- Não aceita um valor

### `--no-ansi`

Negar a opção &quot;—ansi&quot;

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

Exibe a ajuda para o comando fornecido. Quando nenhum comando é fornecido, exibir ajuda para o comando de lista

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

Forçar (ou desativar — no- ansi) a saída ANSI

- Não aceita um valor

### `--no-ansi`

Negar a opção &quot;—ansi&quot;

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

Exibe a ajuda para o comando fornecido. Quando nenhum comando é fornecido, exibir ajuda para o comando de lista

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

Forçar (ou desativar — no- ansi) a saída ANSI

- Não aceita um valor

### `--no-ansi`

Negar a opção &quot;—ansi&quot;

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

Exibe a ajuda para o comando fornecido. Quando nenhum comando é fornecido, exibir ajuda para o comando de lista

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

Forçar (ou desativar — no- ansi) a saída ANSI

- Não aceita um valor

### `--no-ansi`

Negar a opção &quot;—ansi&quot;

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

Exibe a ajuda para o comando fornecido. Quando nenhum comando é fornecido, exibir ajuda para o comando de lista

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

Forçar (ou desativar — no- ansi) a saída ANSI

- Não aceita um valor

### `--no-ansi`

Negar a opção &quot;—ansi&quot;

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

Exibe a ajuda para o comando fornecido. Quando nenhum comando é fornecido, exibir ajuda para o comando de lista

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

Forçar (ou desativar — no- ansi) a saída ANSI

- Não aceita um valor

### `--no-ansi`

Negar a opção &quot;—ansi&quot;

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

Exibe a ajuda para o comando fornecido. Quando nenhum comando é fornecido, exibir ajuda para o comando de lista

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

Forçar (ou desativar — no- ansi) a saída ANSI

- Não aceita um valor

### `--no-ansi`

Negar a opção &quot;—ansi&quot;

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

Exibe a ajuda para o comando fornecido. Quando nenhum comando é fornecido, exibir ajuda para o comando de lista

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

Forçar (ou desativar — no- ansi) a saída ANSI

- Não aceita um valor

### `--no-ansi`

Negar a opção &quot;—ansi&quot;

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

Exibe a ajuda para o comando fornecido. Quando nenhum comando é fornecido, exibir ajuda para o comando de lista

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

Forçar (ou desativar — no- ansi) a saída ANSI

- Não aceita um valor

### `--no-ansi`

Negar a opção &quot;—ansi&quot;

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

Exibe a ajuda para o comando fornecido. Quando nenhum comando é fornecido, exibir ajuda para o comando de lista

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

Forçar (ou desativar — no- ansi) a saída ANSI

- Não aceita um valor

### `--no-ansi`

Negar a opção &quot;—ansi&quot;

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

Exibe a ajuda para o comando fornecido. Quando nenhum comando é fornecido, exibir ajuda para o comando de lista

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

Forçar (ou desativar — no- ansi) a saída ANSI

- Não aceita um valor

### `--no-ansi`

Negar a opção &quot;—ansi&quot;

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

Exibe a ajuda para o comando fornecido. Quando nenhum comando é fornecido, exibir ajuda para o comando de lista

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

Forçar (ou desativar — no- ansi) a saída ANSI

- Não aceita um valor

### `--no-ansi`

Negar a opção &quot;—ansi&quot;

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

Exibe a ajuda para o comando fornecido. Quando nenhum comando é fornecido, exibir ajuda para o comando de lista

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

Forçar (ou desativar — no- ansi) a saída ANSI

- Não aceita um valor

### `--no-ansi`

Negar a opção &quot;—ansi&quot;

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

Exibe a ajuda para o comando fornecido. Quando nenhum comando é fornecido, exibir ajuda para o comando de lista

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

Forçar (ou desativar — no- ansi) a saída ANSI

- Não aceita um valor

### `--no-ansi`

Negar a opção &quot;—ansi&quot;

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

Exibe a ajuda para o comando fornecido. Quando nenhum comando é fornecido, exibir ajuda para o comando de lista

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

Forçar (ou desativar — no- ansi) a saída ANSI

- Não aceita um valor

### `--no-ansi`

Negar a opção &quot;—ansi&quot;

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

Exibe a ajuda para o comando fornecido. Quando nenhum comando é fornecido, exibir ajuda para o comando de lista

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

Forçar (ou desativar — no- ansi) a saída ANSI

- Não aceita um valor

### `--no-ansi`

Negar a opção &quot;—ansi&quot;

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

Exibe a ajuda para o comando fornecido. Quando nenhum comando é fornecido, exibir ajuda para o comando de lista

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

Forçar (ou desativar — no- ansi) a saída ANSI

- Não aceita um valor

### `--no-ansi`

Negar a opção &quot;—ansi&quot;

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`, `-n`

Não faça nenhuma pergunta interativa

- Padrão: `false`
- Não aceita um valor

