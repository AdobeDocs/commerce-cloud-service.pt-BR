---
source-git-commit: c160be020d855983eaf7a06d04cee6e27819b2a0
workflow-type: tm+mt
source-wordcount: '21467'
ht-degree: 0%

---
# magento-cloud (Adobe Commerce na infraestrutura em nuvem)

<!-- The template to render with above values -->
**Versão**: 1.46.1

Esta referência contém 119 comandos disponíveis através do `magento-cloud` ferramenta de linha de comando.
A lista inicial é gerada automaticamente usando o `magento-cloud list` comando no Adobe Commerce na infraestrutura em nuvem.

>[!NOTE]
>
>Essa referência é gerada a partir da base de código do aplicativo. Para alterar o conteúdo, você pode atualizar o código-fonte para a implementação do comando correspondente no [codebase](https://github.com/magento/magento-cloud-cli) repositório e enviar suas alterações para revisão. Outra maneira é _Envie seus comentários_ (localize o link no canto superior direito). Para obter diretrizes de contribuição, consulte [Contribuições de código](https://developer.adobe.com/commerce/contributor/guides/code-contributions/).

## `clear-cache`

Limpe o cache da CLI

```bash
magento-cloud cc
```

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `decode`

Decodifique uma string codificada como MAGENTO_CLOUD_VARIABLES

```bash
magento-cloud decode [-P|--property PROPERTY] [--] <value>
```


### `value`

O valor da variável a ser decodificado

- Obrigatório

### `--property`, `-P`

A propriedade a ser exibida na variável

- Requer um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `docs`

Abrir a documentação online

```bash
magento-cloud docs [--browser BROWSER] [--pipe] [--] [<search>]...
```


### `search`

Pesquisar termo(s)

- Padrão: `[]`

- Matriz

### `--browser`

O navegador a ser usado para abrir o URL. Defina 0 para nenhum.

- Requer um valor

### `--pipe`

Transfira o URL para o stdout.

- Padrão: `false`
- Não aceita um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `help`

Exibe a ajuda para um comando

```bash
magento-cloud help [--format FORMAT] [--raw] [--] [<command_name>]
```


### `command_name`

O nome do comando

- Padrão: `help`


### `--format`

O formato de saída (txt, json ou md)

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

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `list`

Comandos de Listas

```bash
magento-cloud list [--raw] [--format FORMAT] [--all] [--] [<namespace>]
```


### `command`

O comando a ser executado

- Obrigatório

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

### `--all`

Mostrar todos os comandos, incluindo os ocultos

- Padrão: `false`
- Não aceita um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `multi`

Executar um comando em vários projetos

```bash
magento-cloud multi [-p|--projects PROJECTS] [--continue] [--sort SORT] [--reverse] [--] <cmd> (<cmd>)...
```


### `cmd`

O comando a ser executado

- Padrão: `[]`

- Obrigatório
- Matriz

### `--projects`, `-p`

Uma lista de IDs de projeto, separadas por vírgulas e/ou espaço em branco

- Requer um valor

### `--continue`

Continuar executando comandos mesmo se uma exceção for encontrada

- Padrão: `false`
- Não aceita um valor

### `--sort`

Uma propriedade pela qual classificar a lista de opções do projeto

- Padrão: `title`
- Requer um valor

### `--reverse`

Inverter a ordem das opções do projeto

- Padrão: `false`
- Não aceita um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `web`

Abrir o projeto na interface do usuário da Web

```bash
magento-cloud web [--browser BROWSER] [--pipe] [-p|--project PROJECT] [-e|--environment ENVIRONMENT]
```

### `--browser`

O navegador a ser usado para abrir o URL. Defina 0 para nenhum.

- Requer um valor

### `--pipe`

Transfira o URL para o stdout.

- Padrão: `false`
- Não aceita um valor

### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--environment`, `-e`

A ID do ambiente. Use &quot;.&quot; para selecionar o ambiente padrão do projeto.

- Requer um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `activity:cancel`

Cancelar uma atividade

```bash
magento-cloud activity:cancel [-t|--type TYPE] [-x|--exclude-type EXCLUDE-TYPE] [-a|--all] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--] [<id>]
```


### `id`

A ID da atividade. O padrão é a atividade cancelável mais recente.


### `--type`, `-t`

Filtrar por tipo (ao selecionar uma atividade padrão). Os valores podem ser divididos por vírgulas (por exemplo, &quot;a,b,c&quot;) e/ou espaços em branco. Os caracteres % ou * podem ser usados como curinga para o tipo, por exemplo, &#39;%var%&#39; para selecionar atividades relacionadas a variáveis.

- Padrão: `[]`
- Requer um valor

### `--exclude-type`, `-x`

Excluir por tipo (ao selecionar uma atividade padrão). Os valores podem ser divididos por vírgulas (por exemplo, &quot;a,b,c&quot;) e/ou espaços em branco. Os caracteres % ou * podem ser usados como curinga para excluir tipos.

- Padrão: `[]`
- Requer um valor

### `--all`, `-a`

Verificar atividades recentes em todos os ambientes (ao selecionar uma atividade padrão)

- Padrão: `false`
- Não aceita um valor

### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--environment`, `-e`

A ID do ambiente. Use &quot;.&quot; para selecionar o ambiente padrão do projeto.

- Requer um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `activity:get`

Exibir informações detalhadas sobre uma única atividade

```bash
magento-cloud activity:get [-P|--property PROPERTY] [-t|--type TYPE] [-x|--exclude-type EXCLUDE-TYPE] [--state STATE] [--result RESULT] [-i|--incomplete] [-a|--all] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT] [--] [<id>]
```


### `id`

A ID da atividade. O padrão é a atividade mais recente.


### `--property`, `-P`

A propriedade a ser exibida

- Requer um valor

### `--type`, `-t`

Filtrar por tipo (ao selecionar uma atividade padrão). Os valores podem ser divididos por vírgulas (por exemplo, &quot;a,b,c&quot;) e/ou espaços em branco. Os caracteres % ou * podem ser usados como curinga para o tipo, por exemplo, &#39;%var%&#39; para selecionar atividades relacionadas a variáveis.

- Padrão: `[]`
- Requer um valor

### `--exclude-type`, `-x`

Excluir por tipo (ao selecionar uma atividade padrão). Os valores podem ser divididos por vírgulas (por exemplo, &quot;a,b,c&quot;) e/ou espaços em branco. Os caracteres % ou * podem ser usados como curinga para excluir tipos.

- Padrão: `[]`
- Requer um valor

### `--state`

Filtrar por estado (ao selecionar uma atividade padrão): in_progress, pending, complete ou canceled. Os valores podem ser divididos por vírgulas (por exemplo, &quot;a,b,c&quot;) e/ou espaços em branco.

- Padrão: `[]`
- Requer um valor

### `--result`

Filtrar por resultado (ao selecionar uma atividade padrão): sucesso ou falha

- Requer um valor

### `--incomplete`, `-i`

Incluir somente atividades incompletas (ao selecionar uma atividade padrão). Esta é uma abreviação de \&lt;info>—state=em_andamento,pendente\&lt;/info>

- Padrão: `false`
- Não aceita um valor

### `--all`, `-a`

Verificar atividades recentes em todos os ambientes (ao selecionar uma atividade padrão)

- Padrão: `false`
- Não aceita um valor

### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--environment`, `-e`

A ID do ambiente. Use &quot;.&quot; para selecionar o ambiente padrão do projeto.

- Requer um valor

### `--format`

O formato de saída: table, csv, tsv ou plain

- Padrão: `table`
- Requer um valor

### `--columns`, `-c`

Colunas a serem exibidas. Os caracteres % ou * podem ser usados como curinga. Os valores podem ser divididos por vírgulas (por exemplo, &quot;a,b,c&quot;) e/ou espaços em branco.

- Padrão: `[]`
- Requer um valor

### `--no-header`

Não gerar saída do cabeçalho da tabela

- Padrão: `false`
- Não aceita um valor

### `--date-fmt`

O formato de data (como uma string de formato de data do PHP)

- Padrão: `c`
- Requer um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `activity:list`

Obter uma lista de atividades para um ambiente ou projeto

```bash
magento-cloud activities [-t|--type TYPE] [-x|--exclude-type EXCLUDE-TYPE] [--limit LIMIT] [--start START] [--state STATE] [--result RESULT] [-i|--incomplete] [-a|--all] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT]
```

### `--type`, `-t`

Filtrar atividades por tipo Os valores podem ser divididos por vírgulas (por exemplo, &quot;a,b,c&quot;) e/ou espaços em branco. A primeira parte do nome da atividade pode ser omitida. Por exemplo, &quot;cron&quot; pode selecionar atividades &quot;environment.cron&quot;. Os caracteres % ou * podem ser usados como curinga, por exemplo, &#39;%var%&#39; para selecionar atividades relacionadas a variáveis.

- Padrão: `[]`
- Requer um valor

### `--exclude-type`, `-x`

Excluir atividades por tipo. Os valores podem ser divididos por vírgulas (por exemplo, &quot;a,b,c&quot;) e/ou espaços em branco. A primeira parte do nome da atividade pode ser omitida. Por exemplo, &quot;cron&quot; pode excluir atividades &quot;environment.cron&quot;. Os caracteres % ou * podem ser usados como curinga para excluir tipos.

- Padrão: `[]`
- Requer um valor

### `--limit`

Limitar o número de resultados exibidos

- Padrão: `10`
- Requer um valor

### `--start`

Somente atividades criadas antes desta data serão listadas

- Requer um valor

### `--state`

Filtrar atividades por estado: in_progress, pending, complete ou canceled. Os valores podem ser divididos por vírgulas (por exemplo, &quot;a,b,c&quot;) e/ou espaços em branco.

- Padrão: `[]`
- Requer um valor

### `--result`

Filtrar atividades por resultado: sucesso ou falha

- Requer um valor

### `--incomplete`, `-i`

Listar apenas atividades incompletas

- Padrão: `false`
- Não aceita um valor

### `--all`, `-a`

Listar atividades em todos os ambientes

- Padrão: `false`
- Não aceita um valor

### `--format`

O formato de saída: table, csv, tsv ou plain

- Padrão: `table`
- Requer um valor

### `--columns`, `-c`

Colunas a serem exibidas. Colunas disponíveis: id*, created*, description*, progress*, state*, result*, completed, ambientes, type (* = colunas padrão). O caractere &quot;+&quot; pode ser usado como um espaço reservado para as colunas padrão. Os caracteres % ou * podem ser usados como curinga. Os valores podem ser divididos por vírgulas (por exemplo, &quot;a,b,c&quot;) e/ou espaços em branco.

- Padrão: `[]`
- Requer um valor

### `--no-header`

Não gerar saída do cabeçalho da tabela

- Padrão: `false`
- Não aceita um valor

### `--date-fmt`

O formato de data (como uma string de formato de data do PHP)

- Padrão: `c`
- Requer um valor

### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--environment`, `-e`

A ID do ambiente. Use &quot;.&quot; para selecionar o ambiente padrão do projeto.

- Requer um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `activity:log`

Exibir o log de uma atividade

```bash
magento-cloud activity:log [--refresh REFRESH] [-t|--timestamps] [--type TYPE] [-x|--exclude-type EXCLUDE-TYPE] [--state STATE] [--result RESULT] [-i|--incomplete] [-a|--all] [--date-fmt DATE-FMT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--] [<id>]
```


### `id`

A ID da atividade. O padrão é a atividade mais recente.


### `--refresh`

Intervalo de atualização da atividade (segundos). Defina como 0 para desativar a atualização.

- Padrão: `3`
- Requer um valor

### `--timestamps`, `-t`

Exibir um carimbo de data e hora ao lado de cada mensagem

- Padrão: `false`
- Não aceita um valor

### `--type`

Filtrar por tipo (ao selecionar uma atividade padrão). Os valores podem ser divididos por vírgulas (por exemplo, &quot;a,b,c&quot;) e/ou espaços em branco. Os caracteres % ou * podem ser usados como curinga para o tipo, por exemplo, &#39;%var%&#39; para selecionar atividades relacionadas a variáveis.

- Padrão: `[]`
- Requer um valor

### `--exclude-type`, `-x`

Excluir por tipo (ao selecionar uma atividade padrão). Os valores podem ser divididos por vírgulas (por exemplo, &quot;a,b,c&quot;) e/ou espaços em branco. Os caracteres % ou * podem ser usados como curinga para excluir tipos.

- Padrão: `[]`
- Requer um valor

### `--state`

Filtrar por estado (ao selecionar uma atividade padrão): in_progress, pending, complete ou canceled. Os valores podem ser divididos por vírgulas (por exemplo, &quot;a,b,c&quot;) e/ou espaços em branco.

- Padrão: `[]`
- Requer um valor

### `--result`

Filtrar por resultado (ao selecionar uma atividade padrão): sucesso ou falha

- Requer um valor

### `--incomplete`, `-i`

Incluir somente atividades incompletas (ao selecionar uma atividade padrão). Esta é uma abreviação de \&lt;info>—state=em_andamento,pendente\&lt;/info>

- Padrão: `false`
- Não aceita um valor

### `--all`, `-a`

Verificar atividades recentes em todos os ambientes (ao selecionar uma atividade padrão)

- Padrão: `false`
- Não aceita um valor

### `--date-fmt`

O formato de data (como uma string de formato de data do PHP)

- Padrão: `c`
- Requer um valor

### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--environment`, `-e`

A ID do ambiente. Use &quot;.&quot; para selecionar o ambiente padrão do projeto.

- Requer um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `app:config-get`

Exibir a configuração de um aplicativo

```bash
magento-cloud app:config-get [-P|--property PROPERTY] [--refresh] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [-i|--identity-file IDENTITY-FILE]
```

### `--property`, `-P`

A propriedade de configuração a ser exibida

- Requer um valor

### `--refresh`

Se o cache deve ser atualizado

- Padrão: `false`
- Não aceita um valor

### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--environment`, `-e`

A ID do ambiente. Use &quot;.&quot; para selecionar o ambiente padrão do projeto.

- Requer um valor

### `--app`, `-A`

O nome do aplicativo remoto

- Requer um valor

### `--identity-file`, `-i`

[Opção obsoleta, não é mais usada]

- Requer um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `app:list`

Listar aplicativos no projeto

```bash
magento-cloud apps [--refresh] [--pipe] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header]
```

### `--refresh`

Se o cache deve ser atualizado

- Padrão: `false`
- Não aceita um valor

### `--pipe`

Gerar uma lista somente de nomes de aplicativos

- Padrão: `false`
- Não aceita um valor

### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--environment`, `-e`

A ID do ambiente. Use &quot;.&quot; para selecionar o ambiente padrão do projeto.

- Requer um valor

### `--format`

O formato de saída: table, csv, tsv ou plain

- Padrão: `table`
- Requer um valor

### `--columns`, `-c`

Colunas a serem exibidas. Colunas disponíveis: nome*, tipo*, disco, caminho, tamanho (* = colunas padrão). O caractere &quot;+&quot; pode ser usado como um espaço reservado para as colunas padrão. Os caracteres % ou * podem ser usados como curinga. Os valores podem ser divididos por vírgulas (por exemplo, &quot;a,b,c&quot;) e/ou espaços em branco.

- Padrão: `[]`
- Requer um valor

### `--no-header`

Não gerar saída do cabeçalho da tabela

- Padrão: `false`
- Não aceita um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `auth:api-token-login`

Fazer logon na Magento Cloud usando um token de API

```bash
magento-cloud auth:api-token-login
```

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `auth:browser-login`

Fazer logon na Magento Cloud por meio de um navegador

```bash
magento-cloud login [-f|--force] [--browser BROWSER] [--pipe]
```

### `--force`, `-f`

Fazer logon novamente, mesmo que já tenha feito logon

- Padrão: `false`
- Não aceita um valor

### `--browser`

O navegador a ser usado para abrir o URL. Defina 0 para nenhum.

- Requer um valor

### `--pipe`

Transfira o URL para o stdout.

- Padrão: `false`
- Não aceita um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `auth:info`

Exibir as informações da sua conta

```bash
magento-cloud auth:info [--no-auto-login] [-P|--property PROPERTY] [--refresh] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--] [<property>]
```


### `property`

A propriedade da conta a ser exibida


### `--no-auto-login`

Ignora o logon automático. Nada será gerado se não estiver conectado e o código de saída será 0, assumindo que não há outros erros.

- Padrão: `false`
- Não aceita um valor

### `--property`, `-P`

A propriedade da conta a ser exibida (sintaxe alternativa)

- Requer um valor

### `--refresh`

Se o cache deve ser atualizado

- Padrão: `false`
- Não aceita um valor

### `--format`

O formato de saída: table, csv, tsv ou plain

- Padrão: `table`
- Requer um valor

### `--columns`, `-c`

Colunas a serem exibidas. Os caracteres % ou * podem ser usados como curinga. Os valores podem ser divididos por vírgulas (por exemplo, &quot;a,b,c&quot;) e/ou espaços em branco.

- Padrão: `[]`
- Requer um valor

### `--no-header`

Não gerar saída do cabeçalho da tabela

- Padrão: `false`
- Não aceita um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `auth:logout`

Faça logout da Magento Cloud

```bash
magento-cloud logout [-a|--all] [--other]
```

### `--all`, `-a`

Fazer logoff de todas as sessões locais

- Padrão: `false`
- Não aceita um valor

### `--other`

Fazer logoff de outras sessões locais

- Padrão: `false`
- Não aceita um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `blackfire:setup`

Configurar a integração do Blackfire.io para o projeto

```bash
magento-cloud blackfire:setup [--server_id SERVER_ID] [--server_token SERVER_TOKEN] [-p|--project PROJECT] [-W|--no-wait] [--wait]
```

### `--server_id`

A ID do servidor

- Requer um valor

### `--server_token`

O token do servidor

- Requer um valor

### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--no-wait`, `-W`

Não aguarde a conclusão da operação

- Padrão: `false`
- Não aceita um valor

### `--wait`

Aguardar a conclusão da operação (padrão)

- Padrão: `false`
- Não aceita um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `certificate:add`

Adicionar um certificado SSL ao projeto

```bash
magento-cloud certificate:add [--cert CERT] [--key KEY] [--chain CHAIN] [-p|--project PROJECT] [-W|--no-wait] [--wait]
```

### `--cert`

O caminho para o arquivo de certificado

- Requer um valor

### `--key`

O caminho para o arquivo de chave privada do certificado

- Requer um valor

### `--chain`

O caminho para o arquivo da cadeia de certificados

- Padrão: `[]`
- Requer um valor

### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--no-wait`, `-W`

Não aguarde a conclusão da operação

- Padrão: `false`
- Não aceita um valor

### `--wait`

Aguardar a conclusão da operação (padrão)

- Padrão: `false`
- Não aceita um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `certificate:delete`

Excluir um certificado do projeto

```bash
magento-cloud certificate:delete [-p|--project PROJECT] [-W|--no-wait] [--wait] [--] <id>
```


### `id`

A ID do certificado (ou o início dela)

- Obrigatório

### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--no-wait`, `-W`

Não aguarde a conclusão da operação

- Padrão: `false`
- Não aceita um valor

### `--wait`

Aguardar a conclusão da operação (padrão)

- Padrão: `false`
- Não aceita um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `certificate:get`

Exibir um certificado

```bash
magento-cloud certificate:get [-P|--property PROPERTY] [--date-fmt DATE-FMT] [-p|--project PROJECT] [--] <id>
```


### `id`

A ID do certificado (ou o início dela)

- Obrigatório

### `--property`, `-P`

A propriedade do certificado a ser exibida

- Requer um valor

### `--date-fmt`

O formato de data (como uma string de formato de data do PHP)

- Padrão: `c`
- Requer um valor

### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `certificate:list`

Listar certificados de projeto

```bash
magento-cloud certificates [--domain DOMAIN] [--exclude-domain EXCLUDE-DOMAIN] [--issuer ISSUER] [--only-auto] [--no-auto] [--ignore-expiry] [--only-expired] [--no-expired] [--pipe-domains] [--date-fmt DATE-FMT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT]
```

### `--domain`

Filtrar por nome de domínio (pesquisa que não diferencia maiúsculas de minúsculas)

- Requer um valor

### `--exclude-domain`

Excluir certificados, correspondendo pelo nome de domínio (pesquisa que não diferencia maiúsculas de minúsculas)

- Requer um valor

### `--issuer`

Filtrar por emissor

- Requer um valor

### `--only-auto`

Mostrar apenas certificados autoprovisionados

- Padrão: `false`
- Não aceita um valor

### `--no-auto`

Mostrar apenas certificados adicionados manualmente

- Padrão: `false`
- Não aceita um valor

### `--ignore-expiry`

Mostrar certificados expirados e não expirados

- Padrão: `false`
- Não aceita um valor

### `--only-expired`

Mostrar apenas certificados expirados

- Padrão: `false`
- Não aceita um valor

### `--no-expired`

Mostrar apenas certificados não expirados (padrão)

- Padrão: `false`
- Não aceita um valor

### `--pipe-domains`

Retornar apenas uma lista de nomes de domínio cobertos pelos certificados

- Padrão: `false`
- Não aceita um valor

### `--date-fmt`

O formato de data (como uma string de formato de data do PHP)

- Padrão: `c`
- Requer um valor

### `--format`

O formato de saída: table, csv, tsv ou plain

- Padrão: `table`
- Requer um valor

### `--columns`, `-c`

Colunas a serem exibidas. Colunas disponíveis: criado, domínios, expires, id, emissor. Os caracteres % ou * podem ser usados como curinga. Os valores podem ser divididos por vírgulas (por exemplo, &quot;a,b,c&quot;) e/ou espaços em branco.

- Padrão: `[]`
- Requer um valor

### `--no-header`

Não gerar saída do cabeçalho da tabela

- Padrão: `false`
- Não aceita um valor

### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `commit:get`

Mostrar detalhes da confirmação

```bash
magento-cloud commit:get [-P|--property PROPERTY] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--date-fmt DATE-FMT] [--] [<commit>]
```


### `commit`

O SHA de confirmação. Isso também pode aceitar os sufixos &quot;HEAD&quot; e acento circunflexo (^) ou til (~) para confirmações principais.

- Padrão: `HEAD`


### `--property`, `-P`

A propriedade de confirmação a ser exibida.

- Requer um valor

### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--environment`, `-e`

A ID do ambiente. Use &quot;.&quot; para selecionar o ambiente padrão do projeto.

- Requer um valor

### `--date-fmt`

O formato de data (como uma string de formato de data do PHP)

- Padrão: `c`
- Requer um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `commit:list`

Listar confirmações

```bash
magento-cloud commits [--limit LIMIT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT] [--] [<commit>]
```


### `commit`

O SHA de Git commit inicial. Isso também pode aceitar os sufixos &quot;HEAD&quot; e acento circunflexo (^) ou til (~) para confirmações principais.


### `--limit`

O número de confirmações a serem exibidas.

- Padrão: `10`
- Requer um valor

### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--environment`, `-e`

A ID do ambiente. Use &quot;.&quot; para selecionar o ambiente padrão do projeto.

- Requer um valor

### `--format`

O formato de saída: table, csv, tsv ou plain

- Padrão: `table`
- Requer um valor

### `--columns`, `-c`

Colunas a serem exibidas. Colunas disponíveis: author, date, sha, summary. Os caracteres % ou * podem ser usados como curinga. Os valores podem ser divididos por vírgulas (por exemplo, &quot;a,b,c&quot;) e/ou espaços em branco.

- Padrão: `[]`
- Requer um valor

### `--no-header`

Não gerar saída do cabeçalho da tabela

- Padrão: `false`
- Não aceita um valor

### `--date-fmt`

O formato de data (como uma string de formato de data do PHP)

- Padrão: `c`
- Requer um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `db:dump`

Criar um dump local do banco de dados remoto

```bash
magento-cloud db:dump [--schema SCHEMA] [-f|--file FILE] [-d|--directory DIRECTORY] [-z|--gzip] [-t|--timestamp] [-o|--stdout] [--table TABLE] [--exclude-table EXCLUDE-TABLE] [--schema-only] [--charset CHARSET] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [-r|--relationship RELATIONSHIP] [-i|--identity-file IDENTITY-FILE]
```

### `--schema`

O esquema a ser descarregado. Omitir o uso do schema padrão (geralmente &quot;principal&quot;).

- Requer um valor

### `--file`, `-f`

Um nome de arquivo personalizado para o despejo

- Requer um valor

### `--directory`, `-d`

Um diretório personalizado para o despejo

- Requer um valor

### `--gzip`, `-z`

Compactar o despejo usando gzip

- Padrão: `false`
- Não aceita um valor

### `--timestamp`, `-t`

Adicionar um carimbo de data e hora ao nome do arquivo de despejo

- Padrão: `false`
- Não aceita um valor

### `--stdout`, `-o`

Saída para STDOUT em vez de um arquivo

- Padrão: `false`
- Não aceita um valor

### `--table`

Tabela(s) a serem incluídas

- Padrão: `[]`
- Requer um valor

### `--exclude-table`

Tabela(s) a ser excluída(s)

- Padrão: `[]`
- Requer um valor

### `--schema-only`

Despejar apenas esquemas, sem dados

- Padrão: `false`
- Não aceita um valor

### `--charset`

A codificação do conjunto de caracteres para o despejo

- Requer um valor

### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--environment`, `-e`

A ID do ambiente. Use &quot;.&quot; para selecionar o ambiente padrão do projeto.

- Requer um valor

### `--app`, `-A`

O nome do aplicativo remoto

- Requer um valor

### `--relationship`, `-r`

O relacionamento de serviço a ser usado

- Requer um valor

### `--identity-file`, `-i`

Uma identidade SSH (chave privada) para usar

- Requer um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `db:size`

Estimar o uso do disco de um banco de dados

```bash
magento-cloud db:size [-B|--bytes] [-C|--cleanup] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [-r|--relationship RELATIONSHIP] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-i|--identity-file IDENTITY-FILE]
```

### `--bytes`, `-B`

Mostrar tamanhos em bytes.

- Padrão: `false`
- Não aceita um valor

### `--cleanup`, `-C`

Verificar se as tabelas podem ser limpas e mostrar recomendações (somente InnoDb).

- Padrão: `false`
- Não aceita um valor

### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--environment`, `-e`

A ID do ambiente. Use &quot;.&quot; para selecionar o ambiente padrão do projeto.

- Requer um valor

### `--app`, `-A`

O nome do aplicativo remoto

- Requer um valor

### `--relationship`, `-r`

O relacionamento de serviço a ser usado

- Requer um valor

### `--format`

O formato de saída: table, csv, tsv ou plain

- Padrão: `table`
- Requer um valor

### `--columns`, `-c`

Colunas a serem exibidas. Colunas disponíveis: max, percent_used, used. Os caracteres % ou * podem ser usados como curinga. Os valores podem ser divididos por vírgulas (por exemplo, &quot;a,b,c&quot;) e/ou espaços em branco.

- Padrão: `[]`
- Requer um valor

### `--no-header`

Não gerar saída do cabeçalho da tabela

- Padrão: `false`
- Não aceita um valor

### `--identity-file`, `-i`

Uma identidade SSH (chave privada) para usar

- Requer um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `db:sql`

Executar SQL no banco de dados remoto

```bash
magento-cloud sql [--raw] [--schema SCHEMA] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [-r|--relationship RELATIONSHIP] [-i|--identity-file IDENTITY-FILE] [--] [<query>]
```


### `query`

Uma instrução SQL a ser executada


### `--raw`

Produzir saída bruta, não tabular

- Padrão: `false`
- Não aceita um valor

### `--schema`

O esquema a ser usado. Omitir o uso do schema padrão (geralmente &quot;principal&quot;). Transmita uma string vazia para não usar nenhum esquema.

- Requer um valor

### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--environment`, `-e`

A ID do ambiente. Use &quot;.&quot; para selecionar o ambiente padrão do projeto.

- Requer um valor

### `--app`, `-A`

O nome do aplicativo remoto

- Requer um valor

### `--relationship`, `-r`

O relacionamento de serviço a ser usado

- Requer um valor

### `--identity-file`, `-i`

Uma identidade SSH (chave privada) para usar

- Requer um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `domain:add`

Adicionar um novo domínio ao projeto

```bash
magento-cloud domain:add [--cert CERT] [--key KEY] [--chain CHAIN] [--attach ATTACH] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] <name>
```


### `name`

O nome do domínio

- Obrigatório

### `--cert`

O caminho para o arquivo de certificado deste domínio

- Requer um valor

### `--key`

O caminho para o arquivo de chave privada do certificado fornecido.

- Requer um valor

### `--chain`

O caminho para o(s) arquivo(s) da cadeia de certificados do certificado fornecido

- Padrão: `[]`
- Requer um valor

### `--attach`

O domínio de produção que este substitui nas rotas do ambiente. Necessário para domínios de ambiente de não produção.

- Requer um valor

### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--environment`, `-e`

A ID do ambiente. Use &quot;.&quot; para selecionar o ambiente padrão do projeto.

- Requer um valor

### `--no-wait`, `-W`

Não aguarde a conclusão da operação

- Padrão: `false`
- Não aceita um valor

### `--wait`

Aguardar a conclusão da operação (padrão)

- Padrão: `false`
- Não aceita um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `domain:delete`

Excluir um domínio do projeto

```bash
magento-cloud domain:delete [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] <name>
```


### `name`

O nome do domínio

- Obrigatório

### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--environment`, `-e`

A ID do ambiente. Use &quot;.&quot; para selecionar o ambiente padrão do projeto.

- Requer um valor

### `--no-wait`, `-W`

Não aguarde a conclusão da operação

- Padrão: `false`
- Não aceita um valor

### `--wait`

Aguardar a conclusão da operação (padrão)

- Padrão: `false`
- Não aceita um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `domain:get`

Mostrar informações detalhadas de um domínio

```bash
magento-cloud domain:get [-P|--property PROPERTY] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--] [<name>]
```


### `name`

O nome do domínio


### `--property`, `-P`

A propriedade de domínio a ser exibida

- Requer um valor

### `--format`

O formato de saída: table, csv, tsv ou plain

- Padrão: `table`
- Requer um valor

### `--columns`, `-c`

Colunas a serem exibidas. Os caracteres % ou * podem ser usados como curinga. Os valores podem ser divididos por vírgulas (por exemplo, &quot;a,b,c&quot;) e/ou espaços em branco.

- Padrão: `[]`
- Requer um valor

### `--no-header`

Não gerar saída do cabeçalho da tabela

- Padrão: `false`
- Não aceita um valor

### `--date-fmt`

O formato de data (como uma string de formato de data do PHP)

- Padrão: `c`
- Requer um valor

### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--environment`, `-e`

A ID do ambiente. Use &quot;.&quot; para selecionar o ambiente padrão do projeto.

- Requer um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `domain:list`

Obter uma lista de todos os domínios

```bash
magento-cloud domains [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT] [-e|--environment ENVIRONMENT]
```

### `--format`

O formato de saída: table, csv, tsv ou plain

- Padrão: `table`
- Requer um valor

### `--columns`, `-c`

Colunas a serem exibidas. Colunas disponíveis: name*, ssl*, created_at*, registered_name, replacement_for, type, updated_at (* = colunas padrão). O caractere &quot;+&quot; pode ser usado como um espaço reservado para as colunas padrão. Os caracteres % ou * podem ser usados como curinga. Os valores podem ser divididos por vírgulas (por exemplo, &quot;a,b,c&quot;) e/ou espaços em branco.

- Padrão: `[]`
- Requer um valor

### `--no-header`

Não gerar saída do cabeçalho da tabela

- Padrão: `false`
- Não aceita um valor

### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--environment`, `-e`

A ID do ambiente. Use &quot;.&quot; para selecionar o ambiente padrão do projeto.

- Requer um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `domain:update`

Atualizar um domínio

```bash
magento-cloud domain:update [--cert CERT] [--key KEY] [--chain CHAIN] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] <name>
```


### `name`

O nome do domínio

- Obrigatório

### `--cert`

O caminho para o arquivo de certificado deste domínio

- Requer um valor

### `--key`

O caminho para o arquivo de chave privada do certificado fornecido.

- Requer um valor

### `--chain`

O caminho para o(s) arquivo(s) da cadeia de certificados do certificado fornecido

- Padrão: `[]`
- Requer um valor

### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--environment`, `-e`

A ID do ambiente. Use &quot;.&quot; para selecionar o ambiente padrão do projeto.

- Requer um valor

### `--no-wait`, `-W`

Não aguarde a conclusão da operação

- Padrão: `false`
- Não aceita um valor

### `--wait`

Aguardar a conclusão da operação (padrão)

- Padrão: `false`
- Não aceita um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `environment:activate`

Ativar um ambiente

```bash
magento-cloud environment:activate [--parent PARENT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<environment>]...
```


### `environment`

Os ambientes a serem ativados

- Padrão: `[]`

- Matriz

### `--parent`

Definir um novo ambiente principal antes da ativação

- Requer um valor

### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--environment`, `-e`

A ID do ambiente. Use &quot;.&quot; para selecionar o ambiente padrão do projeto.

- Requer um valor

### `--no-wait`, `-W`

Não aguarde a conclusão da operação

- Padrão: `false`
- Não aceita um valor

### `--wait`

Aguardar a conclusão da operação (padrão)

- Padrão: `false`
- Não aceita um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `environment:branch`

Ramificar um ambiente

```bash
magento-cloud branch [--title TITLE] [--type TYPE] [--no-clone-parent] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<id>] [<parent>]
```


### `id`

A ID (nome da ramificação) do novo ambiente


### `parent`

O pai do novo ambiente


### `--title`

O título do novo ambiente

- Requer um valor

### `--type`

O tipo do novo ambiente

- Requer um valor

### `--no-clone-parent`

Não clonar os dados do ambiente pai

- Padrão: `false`
- Não aceita um valor

### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--environment`, `-e`

A ID do ambiente. Use &quot;.&quot; para selecionar o ambiente padrão do projeto.

- Requer um valor

### `--no-wait`, `-W`

Não aguarde a conclusão da operação

- Padrão: `false`
- Não aceita um valor

### `--wait`

Aguardar a conclusão da operação (padrão)

- Padrão: `false`
- Não aceita um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `environment:checkout`

Confira um ambiente

```bash
magento-cloud checkout [-i|--identity-file IDENTITY-FILE] [--] [<id>]
```


### `id`

A ID do ambiente a ser verificado. Por exemplo: &quot;sprint2&quot;


### `--identity-file`, `-i`

Uma identidade SSH (chave privada) para usar

- Requer um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `environment:delete`

Excluir um ou mais ambientes

```bash
magento-cloud environment:delete [--delete-branch] [--no-delete-branch] [--type TYPE] [-t|--only-type ONLY-TYPE] [--exclude EXCLUDE] [--exclude-type EXCLUDE-TYPE] [--inactive] [--merged] [--allow-delete-parent] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<environment>]...
```


### `environment`

Os ambientes a serem excluídos. Os caracteres % ou * podem ser usados como curinga. Os valores podem ser divididos por vírgulas (por exemplo, &quot;a,b,c&quot;) e/ou espaços em branco.

- Padrão: `[]`

- Matriz

### `--delete-branch`

Excluir ramificações Git para ambientes inativos, sem confirmação

- Padrão: `false`
- Não aceita um valor

### `--no-delete-branch`

Não excluir ramificações Git (ambientes inativos)

- Padrão: `false`
- Não aceita um valor

### `--type`

Excluir todos os ambientes de um tipo (adicionando a qualquer outro selecionado) Os valores podem ser divididos por vírgulas (por exemplo, &quot;a,b,c&quot;) e/ou espaços em branco.

- Padrão: `[]`
- Requer um valor

### `--only-type`, `-t`

Somente os ambientes de exclusão de um tipo específico de Valores podem ser divididos por vírgulas (por exemplo, &quot;a,b,c&quot;) e/ou espaços em branco.

- Padrão: `[]`
- Requer um valor

### `--exclude`

Ambiente(s) a não excluir. Os caracteres % ou * podem ser usados como curinga. Os valores podem ser divididos por vírgulas (por exemplo, &quot;a,b,c&quot;) e/ou espaços em branco.

- Padrão: `[]`
- Requer um valor

### `--exclude-type`

Os tipos de ambiente dos quais não excluir valores podem ser divididos por vírgulas (por exemplo, &quot;a,b,c&quot;) e/ou espaços em branco.

- Padrão: `[]`
- Requer um valor

### `--inactive`

Excluir todos os ambientes inativos (adicionando a quaisquer outros selecionados)

- Padrão: `false`
- Não aceita um valor

### `--merged`

Excluir todos os ambientes mesclados (adicionando a qualquer outro selecionado)

- Padrão: `false`
- Não aceita um valor

### `--allow-delete-parent`

Permitir que ambientes com filhos sejam excluídos

- Padrão: `false`
- Não aceita um valor

### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--environment`, `-e`

A ID do ambiente. Use &quot;.&quot; para selecionar o ambiente padrão do projeto.

- Requer um valor

### `--no-wait`, `-W`

Não aguarde a conclusão da operação

- Padrão: `false`
- Não aceita um valor

### `--wait`

Aguardar a conclusão da operação (padrão)

- Padrão: `false`
- Não aceita um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `environment:http-access`

Atualizar configurações de acesso HTTP para um ambiente

```bash
magento-cloud httpaccess [--access ACCESS] [--auth AUTH] [--enabled ENABLED] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait]
```

### `--access`

Restrição de acesso no formato &quot;permissão:endereço&quot;. Use 0 para limpar todos os endereços.

- Padrão: `[]`
- Requer um valor

### `--auth`

Credenciais de autenticação Básicas do HTTP no formato &quot;nome de usuário:senha&quot;. Use 0 para limpar todas as credenciais.

- Padrão: `[]`
- Requer um valor

### `--enabled`

Se o controle de acesso deve ser ativado: 1 para ativar, 0 para desativar

- Requer um valor

### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--environment`, `-e`

A ID do ambiente. Use &quot;.&quot; para selecionar o ambiente padrão do projeto.

- Requer um valor

### `--no-wait`, `-W`

Não aguarde a conclusão da operação

- Padrão: `false`
- Não aceita um valor

### `--wait`

Aguardar a conclusão da operação (padrão)

- Padrão: `false`
- Não aceita um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `environment:info`

Ler ou definir propriedades de um ambiente

```bash
magento-cloud environment:info [--refresh] [--date-fmt DATE-FMT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<property>] [<value>]
```


### `property`

O nome da propriedade


### `value`

Definir um novo valor para a propriedade


### `--refresh`

Se o cache deve ser atualizado

- Padrão: `false`
- Não aceita um valor

### `--date-fmt`

O formato de data (como uma string de formato de data do PHP)

- Padrão: `c`
- Requer um valor

### `--format`

O formato de saída: table, csv, tsv ou plain

- Padrão: `table`
- Requer um valor

### `--columns`, `-c`

Colunas a serem exibidas. Os caracteres % ou * podem ser usados como curinga. Os valores podem ser divididos por vírgulas (por exemplo, &quot;a,b,c&quot;) e/ou espaços em branco.

- Padrão: `[]`
- Requer um valor

### `--no-header`

Não gerar saída do cabeçalho da tabela

- Padrão: `false`
- Não aceita um valor

### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--environment`, `-e`

A ID do ambiente. Use &quot;.&quot; para selecionar o ambiente padrão do projeto.

- Requer um valor

### `--no-wait`, `-W`

Não aguarde a conclusão da operação

- Padrão: `false`
- Não aceita um valor

### `--wait`

Aguardar a conclusão da operação (padrão)

- Padrão: `false`
- Não aceita um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `environment:init`

Inicializar um ambiente a partir de um repositório Git público

```bash
magento-cloud environment:init [--profile PROFILE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] <url>
```


### `url`

Um URL para um repositório Git

- Obrigatório

### `--profile`

O nome do perfil

- Requer um valor

### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--environment`, `-e`

A ID do ambiente. Use &quot;.&quot; para selecionar o ambiente padrão do projeto.

- Requer um valor

### `--no-wait`, `-W`

Não aguarde a conclusão da operação

- Padrão: `false`
- Não aceita um valor

### `--wait`

Aguardar a conclusão da operação (padrão)

- Padrão: `false`
- Não aceita um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `environment:list`

Obter uma lista de ambientes

```bash
magento-cloud environments [-I|--no-inactive] [--pipe] [--refresh REFRESH] [--sort SORT] [--reverse] [--type TYPE] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT]
```

### `--no-inactive`, `-I`

Não mostrar ambientes inativos

- Padrão: `false`
- Não aceita um valor

### `--pipe`

Gerar uma lista simples de IDs de ambiente.

- Padrão: `false`
- Não aceita um valor

### `--refresh`

Se a lista deve ser atualizada.

- Padrão: `1`
- Requer um valor

### `--sort`

Uma propriedade para classificar por

- Padrão: `title`
- Requer um valor

### `--reverse`

Classificar em ordem inversa (descendente)

- Padrão: `false`
- Não aceita um valor

### `--type`

Filtrar a lista por tipos de ambiente. Os valores podem ser divididos por vírgulas (por exemplo, &quot;a,b,c&quot;) e/ou espaços em branco.

- Padrão: `[]`
- Requer um valor

### `--format`

O formato de saída: table, csv, tsv ou plain

- Padrão: `table`
- Requer um valor

### `--columns`, `-c`

Colunas a serem exibidas. Colunas disponíveis: id*, title*, status*, type*, created, machine_name, updated (* = colunas padrão). O caractere &quot;+&quot; pode ser usado como um espaço reservado para as colunas padrão. Os caracteres % ou * podem ser usados como curinga. Os valores podem ser divididos por vírgulas (por exemplo, &quot;a,b,c&quot;) e/ou espaços em branco.

- Padrão: `[]`
- Requer um valor

### `--no-header`

Não gerar saída do cabeçalho da tabela

- Padrão: `false`
- Não aceita um valor

### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `environment:logs`

Ler logs de um ambiente

```bash
magento-cloud log [--lines LINES] [--tail] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [-I|--instance INSTANCE] [--] [<type>]
```


### `type`

O tipo de log, por exemplo, &quot;acesso&quot; ou &quot;erro&quot;


### `--lines`

O número de linhas a serem exibidas

- Padrão: `100`
- Requer um valor

### `--tail`

Continuamente rastrear o log

- Padrão: `false`
- Não aceita um valor

### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--environment`, `-e`

A ID do ambiente. Use &quot;.&quot; para selecionar o ambiente padrão do projeto.

- Requer um valor

### `--app`, `-A`

O nome do aplicativo remoto

- Requer um valor

### `--worker`

Um nome de trabalhador

- Requer um valor

### `--instance`, `-I`

Uma ID de instância

- Requer um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `environment:merge`

Mesclar um ambiente

```bash
magento-cloud merge [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<environment>]
```


### `environment`

O ambiente a ser mesclado


### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--environment`, `-e`

A ID do ambiente. Use &quot;.&quot; para selecionar o ambiente padrão do projeto.

- Requer um valor

### `--no-wait`, `-W`

Não aguarde a conclusão da operação

- Padrão: `false`
- Não aceita um valor

### `--wait`

Aguardar a conclusão da operação (padrão)

- Padrão: `false`
- Não aceita um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `environment:pause`

Pausar um ambiente

```bash
magento-cloud environment:pause [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait]
```

### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--environment`, `-e`

A ID do ambiente. Use &quot;.&quot; para selecionar o ambiente padrão do projeto.

- Requer um valor

### `--no-wait`, `-W`

Não aguarde a conclusão da operação

- Padrão: `false`
- Não aceita um valor

### `--wait`

Aguardar a conclusão da operação (padrão)

- Padrão: `false`
- Não aceita um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `environment:push`

Enviar código para um ambiente

```bash
magento-cloud push [--target TARGET] [-f|--force] [--force-with-lease] [-u|--set-upstream] [--activate] [--parent PARENT] [--type TYPE] [--no-clone-parent] [-W|--no-wait] [--wait] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-i|--identity-file IDENTITY-FILE] [--] [<source>]
```


### `source`

A referência de origem: um nome de ramificação ou hash de confirmação

- Padrão: `HEAD`


### `--target`

O nome da ramificação de destino. O padrão é a ramificação atual.

- Requer um valor

### `--force`, `-f`

Permitir atualizações não rápidas

- Padrão: `false`
- Não aceita um valor

### `--force-with-lease`

Permitir atualizações não rápidas se a ramificação de rastreamento remoto estiver atualizada

- Padrão: `false`
- Não aceita um valor

### `--set-upstream`, `-u`

Defina o ambiente de destino como upstream para a ramificação de origem. Isso também definirá o projeto de destino como remoto para o repositório local.

- Padrão: `false`
- Não aceita um valor

### `--activate`

Ativar o ambiente antes de enviar

- Padrão: `false`
- Não aceita um valor

### `--parent`

Definir o novo ambiente principal (usado somente com — ativate)

- Requer um valor

### `--type`

Definir o tipo de ambiente (usado somente com —ativate )

- Requer um valor

### `--no-clone-parent`

Não clonar os dados da ramificação pai (usados somente com — ativate)

- Padrão: `false`
- Não aceita um valor

### `--no-wait`, `-W`

Não aguarde a conclusão da operação

- Padrão: `false`
- Não aceita um valor

### `--wait`

Aguardar a conclusão da operação (padrão)

- Padrão: `false`
- Não aceita um valor

### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--environment`, `-e`

A ID do ambiente. Use &quot;.&quot; para selecionar o ambiente padrão do projeto.

- Requer um valor

### `--identity-file`, `-i`

Uma identidade SSH (chave privada) para usar

- Requer um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `environment:redeploy`

Reimplantação de um ambiente

```bash
magento-cloud redeploy [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait]
```

### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--environment`, `-e`

A ID do ambiente. Use &quot;.&quot; para selecionar o ambiente padrão do projeto.

- Requer um valor

### `--no-wait`, `-W`

Não aguarde a conclusão da operação

- Padrão: `false`
- Não aceita um valor

### `--wait`

Aguardar a conclusão da operação (padrão)

- Padrão: `false`
- Não aceita um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `environment:relationships`

Mostrar relações de um ambiente

```bash
magento-cloud relationships [-P|--property PROPERTY] [--refresh] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [-i|--identity-file IDENTITY-FILE] [--] [<environment>]
```


### `environment`

O ambiente


### `--property`, `-P`

A propriedade de relacionamento a ser exibida

- Requer um valor

### `--refresh`

Se os relacionamentos devem ser atualizados

- Padrão: `false`
- Não aceita um valor

### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--environment`, `-e`

A ID do ambiente. Use &quot;.&quot; para selecionar o ambiente padrão do projeto.

- Requer um valor

### `--app`, `-A`

O nome do aplicativo remoto

- Requer um valor

### `--identity-file`, `-i`

Uma identidade SSH (chave privada) para usar

- Requer um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `environment:resume`

Retomar um ambiente pausado

```bash
magento-cloud environment:resume [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait]
```

### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--environment`, `-e`

A ID do ambiente. Use &quot;.&quot; para selecionar o ambiente padrão do projeto.

- Requer um valor

### `--no-wait`, `-W`

Não aguarde a conclusão da operação

- Padrão: `false`
- Não aceita um valor

### `--wait`

Aguardar a conclusão da operação (padrão)

- Padrão: `false`
- Não aceita um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `environment:scp`

Copiar arquivos de e para um ambiente usando scp

```bash
magento-cloud scp [-r|--recursive] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [-I|--instance INSTANCE] [-i|--identity-file IDENTITY-FILE] [--] [<files>]...
```


### `files`

Arquivos para copiar. Use o prefixo remote: para definir locais remotos.

- Padrão: `[]`

- Matriz

### `--recursive`, `-r`

Copiar recursivamente diretórios inteiros

- Padrão: `false`
- Não aceita um valor

### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--environment`, `-e`

A ID do ambiente. Use &quot;.&quot; para selecionar o ambiente padrão do projeto.

- Requer um valor

### `--app`, `-A`

O nome do aplicativo remoto

- Requer um valor

### `--worker`

Um nome de trabalhador

- Requer um valor

### `--instance`, `-I`

Uma ID de instância

- Requer um valor

### `--identity-file`, `-i`

Uma identidade SSH (chave privada) para usar

- Requer um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `environment:ssh`

SSH para o ambiente atual

```bash
magento-cloud ssh [--pipe] [--all] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [-I|--instance INSTANCE] [-i|--identity-file IDENTITY-FILE] [--] [<cmd>]...
```


### `cmd`

Um comando a ser executado no ambiente.

- Padrão: `[]`

- Matriz

### `--pipe`

Saída somente do URL SSH.

- Padrão: `false`
- Não aceita um valor

### `--all`

Saída de todos os URLs SSH (para cada aplicativo).

- Padrão: `false`
- Não aceita um valor

### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--environment`, `-e`

A ID do ambiente. Use &quot;.&quot; para selecionar o ambiente padrão do projeto.

- Requer um valor

### `--app`, `-A`

O nome do aplicativo remoto

- Requer um valor

### `--worker`

Um nome de trabalhador

- Requer um valor

### `--instance`, `-I`

Uma ID de instância

- Requer um valor

### `--identity-file`, `-i`

Uma identidade SSH (chave privada) para usar

- Requer um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `environment:synchronize`

Sincronizar o código e/ou os dados de um ambiente a partir de seu pai

```bash
magento-cloud sync [--rebase] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<synchronize>]...
```


### `synchronize`

O que sincronizar: &quot;código&quot;, &quot;dados&quot; ou ambos

- Padrão: `[]`

- Matriz

### `--rebase`

Sincronizar código rebaseando em vez de mesclar

- Padrão: `false`
- Não aceita um valor

### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--environment`, `-e`

A ID do ambiente. Use &quot;.&quot; para selecionar o ambiente padrão do projeto.

- Requer um valor

### `--no-wait`, `-W`

Não aguarde a conclusão da operação

- Padrão: `false`
- Não aceita um valor

### `--wait`

Aguardar a conclusão da operação (padrão)

- Padrão: `false`
- Não aceita um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `environment:url`

Obter os URLs públicos de um ambiente

```bash
magento-cloud url [-1|--primary] [--browser BROWSER] [--pipe] [-p|--project PROJECT] [-e|--environment ENVIRONMENT]
```

### `--primary`, `-1`

Retornar apenas o URL da rota principal

- Padrão: `false`
- Não aceita um valor

### `--browser`

O navegador a ser usado para abrir o URL. Defina 0 para nenhum.

- Requer um valor

### `--pipe`

Transfira o URL para o stdout.

- Padrão: `false`
- Não aceita um valor

### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--environment`, `-e`

A ID do ambiente. Use &quot;.&quot; para selecionar o ambiente padrão do projeto.

- Requer um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `environment:xdebug`

Abrir um túnel para o Xdebug no ambiente

```bash
magento-cloud xdebug [--port PORT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [-I|--instance INSTANCE] [-i|--identity-file IDENTITY-FILE]
```

### `--port`

A porta local

- Padrão: `9000`
- Requer um valor

### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--environment`, `-e`

A ID do ambiente. Use &quot;.&quot; para selecionar o ambiente padrão do projeto.

- Requer um valor

### `--app`, `-A`

O nome do aplicativo remoto

- Requer um valor

### `--worker`

Um nome de trabalhador

- Requer um valor

### `--instance`, `-I`

Uma ID de instância

- Requer um valor

### `--identity-file`, `-i`

Uma identidade SSH (chave privada) para usar

- Requer um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `integration:activity:get`

Exibir informações detalhadas sobre uma única atividade de integração

```bash
magento-cloud integration:activity:get [-P|--property PROPERTY] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT] [--] [<integration>] [<activity>]
```


### `integration`

Uma ID de integração. Deixe em branco para escolher em uma lista.


### `activity`

A ID da atividade. O padrão é a atividade de integração mais recente.


### `--property`, `-P`

A propriedade a ser exibida

- Requer um valor

### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--environment`, `-e`

[Opção obsoleta, não usada]

- Requer um valor

### `--format`

O formato de saída: table, csv, tsv ou plain

- Padrão: `table`
- Requer um valor

### `--columns`, `-c`

Colunas a serem exibidas. Os caracteres % ou * podem ser usados como curinga. Os valores podem ser divididos por vírgulas (por exemplo, &quot;a,b,c&quot;) e/ou espaços em branco.

- Padrão: `[]`
- Requer um valor

### `--no-header`

Não gerar saída do cabeçalho da tabela

- Padrão: `false`
- Não aceita um valor

### `--date-fmt`

O formato de data (como uma string de formato de data do PHP)

- Padrão: `c`
- Requer um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `integration:activity:list`

Obter uma lista de atividades para uma integração

```bash
magento-cloud int:act [--type TYPE] [-x|--exclude-type EXCLUDE-TYPE] [--limit LIMIT] [--start START] [--state STATE] [--result RESULT] [-i|--incomplete] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--] [<id>]
```


### `id`

Uma ID de integração. Deixe em branco para escolher em uma lista.


### `--type`

Filtrar atividades por tipo. Os valores podem ser divididos por vírgulas (por exemplo, &quot;a,b,c&quot;) e/ou espaços em branco.

- Padrão: `[]`
- Requer um valor

### `--exclude-type`, `-x`

Excluir atividades por tipo. Os valores podem ser divididos por vírgulas (por exemplo, &quot;a,b,c&quot;) e/ou espaços em branco. Os caracteres % ou * podem ser usados como curinga para excluir tipos.

- Padrão: `[]`
- Requer um valor

### `--limit`

Limitar o número de resultados exibidos

- Padrão: `10`
- Requer um valor

### `--start`

Somente atividades criadas antes desta data serão listadas

- Requer um valor

### `--state`

Filtrar atividades por estado. Os valores podem ser divididos por vírgulas (por exemplo, &quot;a,b,c&quot;) e/ou espaços em branco.

- Padrão: `[]`
- Requer um valor

### `--result`

Filtrar atividades por resultado

- Requer um valor

### `--incomplete`, `-i`

Listar apenas atividades incompletas

- Padrão: `false`
- Não aceita um valor

### `--format`

O formato de saída: table, csv, tsv ou plain

- Padrão: `table`
- Requer um valor

### `--columns`, `-c`

Colunas a serem exibidas. Colunas disponíveis: id*, created*, description*, type*, state*, result*, completed (* = colunas padrão). O caractere &quot;+&quot; pode ser usado como um espaço reservado para as colunas padrão. Os caracteres % ou * podem ser usados como curinga. Os valores podem ser divididos por vírgulas (por exemplo, &quot;a,b,c&quot;) e/ou espaços em branco.

- Padrão: `[]`
- Requer um valor

### `--no-header`

Não gerar saída do cabeçalho da tabela

- Padrão: `false`
- Não aceita um valor

### `--date-fmt`

O formato de data (como uma string de formato de data do PHP)

- Padrão: `c`
- Requer um valor

### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--environment`, `-e`

[Opção obsoleta, não usada]

- Requer um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `integration:activity:log`

Exibir o log de uma atividade de integração

```bash
magento-cloud integration:activity:log [-t|--timestamps] [--date-fmt DATE-FMT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--] [<integration>] [<activity>]
```


### `integration`

Uma ID de integração. Deixe em branco para escolher em uma lista.


### `activity`

A ID da atividade. O padrão é a atividade de integração mais recente.


### `--timestamps`, `-t`

Exibir um carimbo de data e hora ao lado de cada mensagem

- Padrão: `false`
- Não aceita um valor

### `--date-fmt`

O formato de data (como uma string de formato de data do PHP)

- Padrão: `c`
- Requer um valor

### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--environment`, `-e`

[Opção obsoleta, não usada]

- Requer um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `integration:add`

Adicionar uma integração ao projeto

```bash
magento-cloud integration:add [--type TYPE] [--base-url BASE-URL] [--bitbucket-url BITBUCKET-URL] [--username USERNAME] [--token TOKEN] [--key KEY] [--secret SECRET] [--license-key LICENSE-KEY] [--server-project SERVER-PROJECT] [--repository REPOSITORY] [--build-merge-requests BUILD-MERGE-REQUESTS] [--build-pull-requests BUILD-PULL-REQUESTS] [--build-draft-pull-requests BUILD-DRAFT-PULL-REQUESTS] [--build-pull-requests-post-merge BUILD-PULL-REQUESTS-POST-MERGE] [--build-wip-merge-requests BUILD-WIP-MERGE-REQUESTS] [--merge-requests-clone-parent-data MERGE-REQUESTS-CLONE-PARENT-DATA] [--pull-requests-clone-parent-data PULL-REQUESTS-CLONE-PARENT-DATA] [--resync-pull-requests RESYNC-PULL-REQUESTS] [--fetch-branches FETCH-BRANCHES] [--prune-branches PRUNE-BRANCHES] [--resources-init RESOURCES-INIT] [--url URL] [--shared-key SHARED-KEY] [--file FILE] [--events EVENTS] [--states STATES] [--environments ENVIRONMENTS] [--excluded-environments EXCLUDED-ENVIRONMENTS] [--from-address FROM-ADDRESS] [--recipients RECIPIENTS] [--channel CHANNEL] [--routing-key ROUTING-KEY] [--category CATEGORY] [--index INDEX] [--sourcetype SOURCETYPE] [--protocol PROTOCOL] [--syslog-host SYSLOG-HOST] [--syslog-port SYSLOG-PORT] [--facility FACILITY] [--message-format MESSAGE-FORMAT] [--auth-mode AUTH-MODE] [--auth-token AUTH-TOKEN] [--verify-tls VERIFY-TLS] [--header HEADER] [-p|--project PROJECT] [-W|--no-wait] [--wait]
```

### `--type`

O tipo de integração (&#39;bitbucket&#39;, &#39;bitbucket_server&#39;, &#39;github&#39;, &#39;gitlab&#39;, &#39;webhook&#39;, &#39;health.email&#39;, &#39;health.pagerDuty&#39;, &#39;health.slack&#39;, &#39;health.webhook&#39;, &#39;httplog&#39;, &#39;script&#39;, &#39;newrelic&#39;, &#39;splunk&#39;, &#39;sumologic&#39;, &#39;syslog&#39;)

- Requer um valor

### `--base-url`

O URL de base da instalação do servidor

- Requer um valor

### `--bitbucket-url`

O URL base da instalação do Servidor Bitbucket

- Requer um valor

### `--username`

O nome de usuário do servidor Bitbucket

- Requer um valor

### `--token`

Um token de autenticação ou acesso para a integração

- Requer um valor

### `--key`

Uma chave de consumidor OAuth de Bitbucket

- Requer um valor

### `--secret`

Um segredo do consumidor OAuth do Bitbucket

- Requer um valor

### `--license-key`

A chave de licença dos logs do New Relic

- Requer um valor

### `--server-project`

O projeto (por exemplo, &quot;namespace/repo&quot;)

- Requer um valor

### `--repository`

O repositório a ser rastreado (por exemplo, &quot;proprietário/repositório&quot;)

- Requer um valor

### `--build-merge-requests`

GitLab: criar solicitações de mesclagem como ambientes

- Padrão: `true`
- Requer um valor

### `--build-pull-requests`

Criar cada solicitação de pull como um ambiente

- Padrão: `true`
- Requer um valor

### `--build-draft-pull-requests`

Criar solicitações de pull de rascunho

- Padrão: `true`
- Requer um valor

### `--build-pull-requests-post-merge`

Criar solicitações pull com base em seu estado pós-mesclagem

- Padrão: `false`
- Requer um valor

### `--build-wip-merge-requests`

GitLab: criar solicitações de mesclagem WIP

- Padrão: `true`
- Requer um valor

### `--merge-requests-clone-parent-data`

GitLab: clonar dados para solicitações de mesclagem

- Padrão: `true`
- Requer um valor

### `--pull-requests-clone-parent-data`

Clonar os dados do ambiente pai para solicitações de pull

- Padrão: `true`
- Requer um valor

### `--resync-pull-requests`

Sincronizar novamente os dados do ambiente de solicitação de pull em cada build

- Padrão: `false`
- Requer um valor

### `--fetch-branches`

Buscar todas as ramificações remotas (como ambientes inativos)

- Padrão: `true`
- Requer um valor

### `--prune-branches`

Excluir ramificações que não existem no local remoto

- Padrão: `true`
- Requer um valor

### `--resources-init`

Os recursos a serem usados ao inicializar um novo serviço (&#39;minimum&#39;, &#39;default&#39;, &#39;manual&#39;, &#39;parent&#39;)

- Requer um valor

### `--url`

O endpoint do URL ou da API para a integração

- Requer um valor

### `--shared-key`

Webhook: a chave secreta compartilhada JWS

- Requer um valor

### `--file`

O nome de um arquivo local que contém o script a ser carregado

- Requer um valor

### `--events`

Uma lista de eventos nos quais agir, por exemplo, environment.push

- Padrão: `*`
- Requer um valor

### `--states`

Uma lista de estados nos quais agir; por exemplo, pendente, em_andamento, concluído

- Padrão: `complete`
- Requer um valor

### `--environments`

As IDs de ambiente a serem incluídas

- Padrão: `*`
- Requer um valor

### `--excluded-environments`

As IDs de ambiente a serem excluídos

- Padrão: `[]`
- Requer um valor

### `--from-address`

[Opcional] Personalizar do endereço para emails de alerta

- Requer um valor

### `--recipients`

Os endereços de email dos destinatários

- Padrão: `[]`
- Requer um valor

### `--channel`

O canal Slack

- Requer um valor

### `--routing-key`

A chave de roteamento PagerDuty

- Requer um valor

### `--category`

A categoria Lógica Sumo, usada para filtragem

- Requer um valor

### `--index`

O índice do Splunk

- Requer um valor

### `--sourcetype`

O tipo de origem do evento Splunk

- Requer um valor

### `--protocol`

Protocolo de transporte do Syslog (&#39;tcp&#39;, &#39;udp&#39;, &#39;tls&#39;)

- Padrão: `tls`
- Requer um valor

### `--syslog-host`

Host Syslog relay/collector

- Requer um valor

### `--syslog-port`

Porta de relé/coletor do Syslog

- Requer um valor

### `--facility`

Instalação do Syslog

- Padrão: `1`
- Requer um valor

### `--message-format`

Formato de mensagem do Syslog (&#39;rfc3164&#39; ou &#39;rfc5424&#39;)

- Padrão: `rfc5424`
- Requer um valor

### `--auth-mode`

Modo de autenticação (&quot;prefix&quot; ou &quot;structured_data&quot;)

- Padrão: `prefix`
- Requer um valor

### `--auth-token`

Token de autenticação

- Requer um valor

### `--verify-tls`

Se a verificação do certificado HTTPS deve ser habilitada (recomendado)

- Padrão: `true`
- Requer um valor

### `--header`

Cabeçalho(s) HTTP para usar em solicitações POST. Separe os nomes e os valores com dois pontos (:).

- Padrão: `[]`
- Requer um valor

### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--no-wait`, `-W`

Não aguarde a conclusão da operação

- Padrão: `false`
- Não aceita um valor

### `--wait`

Aguardar a conclusão da operação (padrão)

- Padrão: `false`
- Não aceita um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `integration:delete`

Excluir uma integração de um projeto

```bash
magento-cloud integration:delete [-p|--project PROJECT] [-W|--no-wait] [--wait] [--] [<id>]
```


### `id`

A ID de integração. Deixe em branco para escolher em uma lista.


### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--no-wait`, `-W`

Não aguarde a conclusão da operação

- Padrão: `false`
- Não aceita um valor

### `--wait`

Aguardar a conclusão da operação (padrão)

- Padrão: `false`
- Não aceita um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `integration:get`

Exibir detalhes de uma integração

```bash
magento-cloud integration:get [-P|--property [PROPERTY]] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT] [--] [<id>]
```


### `id`

Uma ID de integração. Deixe em branco para escolher em uma lista.


### `--property`, `-P`

A propriedade de integração a ser exibida

- Aceita um valor

### `--format`

O formato de saída: table, csv, tsv ou plain

- Padrão: `table`
- Requer um valor

### `--columns`, `-c`

Colunas a serem exibidas. Os caracteres % ou * podem ser usados como curinga. Os valores podem ser divididos por vírgulas (por exemplo, &quot;a,b,c&quot;) e/ou espaços em branco.

- Padrão: `[]`
- Requer um valor

### `--no-header`

Não gerar saída do cabeçalho da tabela

- Padrão: `false`
- Não aceita um valor

### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `integration:list`

Exibir uma lista de integrações de projeto

```bash
magento-cloud integrations [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT]
```

### `--format`

O formato de saída: table, csv, tsv ou plain

- Padrão: `table`
- Requer um valor

### `--columns`, `-c`

Colunas a serem exibidas. Colunas disponíveis: id, resumo, tipo. Os caracteres % ou * podem ser usados como curinga. Os valores podem ser divididos por vírgulas (por exemplo, &quot;a,b,c&quot;) e/ou espaços em branco.

- Padrão: `[]`
- Requer um valor

### `--no-header`

Não gerar saída do cabeçalho da tabela

- Padrão: `false`
- Não aceita um valor

### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `integration:update`

Atualizar uma integração

```bash
magento-cloud integration:update [--type TYPE] [--base-url BASE-URL] [--bitbucket-url BITBUCKET-URL] [--username USERNAME] [--token TOKEN] [--key KEY] [--secret SECRET] [--license-key LICENSE-KEY] [--server-project SERVER-PROJECT] [--repository REPOSITORY] [--build-merge-requests BUILD-MERGE-REQUESTS] [--build-pull-requests BUILD-PULL-REQUESTS] [--build-draft-pull-requests BUILD-DRAFT-PULL-REQUESTS] [--build-pull-requests-post-merge BUILD-PULL-REQUESTS-POST-MERGE] [--build-wip-merge-requests BUILD-WIP-MERGE-REQUESTS] [--merge-requests-clone-parent-data MERGE-REQUESTS-CLONE-PARENT-DATA] [--pull-requests-clone-parent-data PULL-REQUESTS-CLONE-PARENT-DATA] [--resync-pull-requests RESYNC-PULL-REQUESTS] [--fetch-branches FETCH-BRANCHES] [--prune-branches PRUNE-BRANCHES] [--resources-init RESOURCES-INIT] [--url URL] [--shared-key SHARED-KEY] [--file FILE] [--events EVENTS] [--states STATES] [--environments ENVIRONMENTS] [--excluded-environments EXCLUDED-ENVIRONMENTS] [--from-address FROM-ADDRESS] [--recipients RECIPIENTS] [--channel CHANNEL] [--routing-key ROUTING-KEY] [--category CATEGORY] [--index INDEX] [--sourcetype SOURCETYPE] [--protocol PROTOCOL] [--syslog-host SYSLOG-HOST] [--syslog-port SYSLOG-PORT] [--facility FACILITY] [--message-format MESSAGE-FORMAT] [--auth-mode AUTH-MODE] [--auth-token AUTH-TOKEN] [--verify-tls VERIFY-TLS] [--header HEADER] [-p|--project PROJECT] [-W|--no-wait] [--wait] [--] [<id>]
```


### `id`

A ID da integração a ser atualizada


### `--type`

O tipo de integração (&#39;bitbucket&#39;, &#39;bitbucket_server&#39;, &#39;github&#39;, &#39;gitlab&#39;, &#39;webhook&#39;, &#39;health.email&#39;, &#39;health.pagerDuty&#39;, &#39;health.slack&#39;, &#39;health.webhook&#39;, &#39;httplog&#39;, &#39;script&#39;, &#39;newrelic&#39;, &#39;splunk&#39;, &#39;sumologic&#39;, &#39;syslog&#39;)

- Requer um valor

### `--base-url`

O URL de base da instalação do servidor

- Requer um valor

### `--bitbucket-url`

O URL base da instalação do Servidor Bitbucket

- Requer um valor

### `--username`

O nome de usuário do servidor Bitbucket

- Requer um valor

### `--token`

Um token de autenticação ou acesso para a integração

- Requer um valor

### `--key`

Uma chave de consumidor OAuth de Bitbucket

- Requer um valor

### `--secret`

Um segredo do consumidor OAuth do Bitbucket

- Requer um valor

### `--license-key`

A chave de licença dos logs do New Relic

- Requer um valor

### `--server-project`

O projeto (por exemplo, &quot;namespace/repo&quot;)

- Requer um valor

### `--repository`

O repositório a ser rastreado (por exemplo, &quot;proprietário/repositório&quot;)

- Requer um valor

### `--build-merge-requests`

GitLab: criar solicitações de mesclagem como ambientes

- Padrão: `true`
- Requer um valor

### `--build-pull-requests`

Criar cada solicitação de pull como um ambiente

- Padrão: `true`
- Requer um valor

### `--build-draft-pull-requests`

Criar solicitações de pull de rascunho

- Padrão: `true`
- Requer um valor

### `--build-pull-requests-post-merge`

Criar solicitações pull com base em seu estado pós-mesclagem

- Padrão: `false`
- Requer um valor

### `--build-wip-merge-requests`

GitLab: criar solicitações de mesclagem WIP

- Padrão: `true`
- Requer um valor

### `--merge-requests-clone-parent-data`

GitLab: clonar dados para solicitações de mesclagem

- Padrão: `true`
- Requer um valor

### `--pull-requests-clone-parent-data`

Clonar os dados do ambiente pai para solicitações de pull

- Padrão: `true`
- Requer um valor

### `--resync-pull-requests`

Sincronizar novamente os dados do ambiente de solicitação de pull em cada build

- Padrão: `false`
- Requer um valor

### `--fetch-branches`

Buscar todas as ramificações remotas (como ambientes inativos)

- Padrão: `true`
- Requer um valor

### `--prune-branches`

Excluir ramificações que não existem no local remoto

- Padrão: `true`
- Requer um valor

### `--resources-init`

Os recursos a serem usados ao inicializar um novo serviço (&#39;minimum&#39;, &#39;default&#39;, &#39;manual&#39;, &#39;parent&#39;)

- Requer um valor

### `--url`

O endpoint do URL ou da API para a integração

- Requer um valor

### `--shared-key`

Webhook: a chave secreta compartilhada JWS

- Requer um valor

### `--file`

O nome de um arquivo local que contém o script a ser carregado

- Requer um valor

### `--events`

Uma lista de eventos nos quais agir, por exemplo, environment.push

- Padrão: `*`
- Requer um valor

### `--states`

Uma lista de estados nos quais agir; por exemplo, pendente, em_andamento, concluído

- Padrão: `complete`
- Requer um valor

### `--environments`

As IDs de ambiente a serem incluídas

- Padrão: `*`
- Requer um valor

### `--excluded-environments`

As IDs de ambiente a serem excluídos

- Padrão: `[]`
- Requer um valor

### `--from-address`

[Opcional] Personalizar do endereço para emails de alerta

- Requer um valor

### `--recipients`

Os endereços de email dos destinatários

- Padrão: `[]`
- Requer um valor

### `--channel`

O canal Slack

- Requer um valor

### `--routing-key`

A chave de roteamento PagerDuty

- Requer um valor

### `--category`

A categoria Lógica Sumo, usada para filtragem

- Requer um valor

### `--index`

O índice do Splunk

- Requer um valor

### `--sourcetype`

O tipo de origem do evento Splunk

- Requer um valor

### `--protocol`

Protocolo de transporte do Syslog (&#39;tcp&#39;, &#39;udp&#39;, &#39;tls&#39;)

- Padrão: `tls`
- Requer um valor

### `--syslog-host`

Host Syslog relay/collector

- Requer um valor

### `--syslog-port`

Porta de relé/coletor do Syslog

- Requer um valor

### `--facility`

Instalação do Syslog

- Padrão: `1`
- Requer um valor

### `--message-format`

Formato de mensagem do Syslog (&#39;rfc3164&#39; ou &#39;rfc5424&#39;)

- Padrão: `rfc5424`
- Requer um valor

### `--auth-mode`

Modo de autenticação (&quot;prefix&quot; ou &quot;structured_data&quot;)

- Padrão: `prefix`
- Requer um valor

### `--auth-token`

Token de autenticação

- Requer um valor

### `--verify-tls`

Se a verificação do certificado HTTPS deve ser habilitada (recomendado)

- Padrão: `true`
- Requer um valor

### `--header`

Cabeçalho(s) HTTP para usar em solicitações POST. Separe os nomes e os valores com dois pontos (:).

- Padrão: `[]`
- Requer um valor

### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--no-wait`, `-W`

Não aguarde a conclusão da operação

- Padrão: `false`
- Não aceita um valor

### `--wait`

Aguardar a conclusão da operação (padrão)

- Padrão: `false`
- Não aceita um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `integration:validate`

Validar uma integração existente

```bash
magento-cloud integration:validate [-p|--project PROJECT] [--] [<id>]
```


### `id`

Uma ID de integração. Deixe em branco para escolher em uma lista.


### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `local:build`

Criar o projeto atual localmente

```bash
magento-cloud build [-a|--abslinks] [-s|--source SOURCE] [-d|--destination DESTINATION] [-c|--copy] [--clone] [--run-deploy-hooks] [--no-clean] [--no-archive] [--no-backup] [--no-cache] [--no-build-hooks] [--no-deps] [--working-copy] [--concurrency CONCURRENCY] [--lock] [--] [<app>]...
```


### `app`

Especificar aplicativos a serem compilados

- Padrão: `[]`

- Matriz

### `--abslinks`, `-a`

Usar links absolutos

- Padrão: `false`
- Não aceita um valor

### `--source`, `-s`

O diretório de origem. O padrão é a raiz do projeto atual.

- Requer um valor

### `--destination`, `-d`

O destino, ao qual a raiz da Web de cada aplicativo será vinculada. Padrão: _www

- Requer um valor

### `--copy`, `-c`

Copie para um diretório de build, em vez de criar symlinking a partir da origem

- Padrão: `false`
- Não aceita um valor

### `--clone`

Usar o Git para clonar o HEAD atual no diretório de compilação

- Padrão: `false`
- Não aceita um valor

### `--run-deploy-hooks`

Executar ganchos deploy e/ou post_deploy

- Padrão: `false`
- Não aceita um valor

### `--no-clean`

Não remover compilações antigas

- Padrão: `false`
- Não aceita um valor

### `--no-archive`

Não criar ou usar um arquivo morto de compilação

- Padrão: `false`
- Não aceita um valor

### `--no-backup`

Não fazer backup da build anterior

- Padrão: `false`
- Não aceita um valor

### `--no-cache`

Desativar armazenamento em cache

- Padrão: `false`
- Não aceita um valor

### `--no-build-hooks`

Não executar ganchos pós-compilação

- Padrão: `false`
- Não aceita um valor

### `--no-deps`

Não instalar as dependências de compilação localmente

- Padrão: `false`
- Não aceita um valor

### `--working-copy`

Drush: use o Git para clonar um repositório de cada módulo Drupal em vez de simplesmente baixar uma versão

- Padrão: `false`
- Não aceita um valor

### `--concurrency`

Drush: defina o número de projetos simultâneos que serão processados ao mesmo tempo

- Padrão: `4`
- Requer um valor

### `--lock`

Drush: criar ou atualizar um arquivo de bloqueio (disponível somente com a versão 7+ do Drush)

- Padrão: `false`
- Não aceita um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `local:dir`

Encontrar a raiz do projeto local

```bash
magento-cloud dir [<subdir>]
```


### `subdir`

O subdiretório a ser localizado (&quot;local&quot;, &quot;web&quot; ou &quot;compartilhado&quot;)


### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `metrics:all`

\&lt;fg white=&quot;&quot; bg=&quot;red&quot;> BETA \&lt;/> Mostra as métricas de CPU, disco e memória de um ambiente

```bash
magento-cloud metrics [-B|--bytes] [-r|--range RANGE] [-i|--interval INTERVAL] [--to TO] [-1|--latest] [-s|--service SERVICE] [--type TYPE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT]
```

### `--bytes`, `-B`

Mostrar tamanhos em bytes

- Padrão: `false`
- Não aceita um valor

### `--range`, `-r`

O intervalo de tempo. As métricas serão carregadas por essa duração até a hora de término (—para). Você pode especificar unidades: horas (h), minutos (m) ou segundos (s). Mínimo \&lt;comment>5m\&lt;/comment>, máximo \&lt;comment>8h\&lt;/comment> ou mais (dependendo do projeto), padrão \&lt;comment>10m\&lt;/comment>.

- Requer um valor

### `--interval`, `-i`

O intervalo. O padrão é uma divisão do intervalo. Você pode especificar unidades: horas (h), minutos (m) ou segundos (s). Mínimo \&lt;comment>1m\&lt;/comment>.

- Requer um valor

### `--to`

A hora final. O padrão é agora.

- Requer um valor

### `--latest`, `-1`

Mostrar apenas o último ponto de dados único

- Padrão: `false`
- Não aceita um valor

### `--service`, `-s`

Filtrar por nome de serviço ou aplicativo Os caracteres % ou * podem ser usados como curinga.

- Padrão: `[]`
- Requer um valor

### `--type`

Filtrar por tipo de serviço (se — service não for fornecido). A versão não é necessária. Os caracteres % ou * podem ser usados como curinga.

- Padrão: `[]`
- Requer um valor

### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--environment`, `-e`

A ID do ambiente. Use &quot;.&quot; para selecionar o ambiente padrão do projeto.

- Requer um valor

### `--format`

O formato de saída: table, csv, tsv ou plain

- Padrão: `table`
- Requer um valor

### `--columns`, `-c`

Colunas a serem exibidas. Colunas disponíveis: timestamp*, serviço*, cpu_percent*, mem_percent*, disk_percent*, tmp_disk_percent*, cpu_limit, cpu_used, disk_limit, disk_used, inodes_limit, inodes_percent, inodes_used, mem_limit, mem_used, tmp_disk_limit, tmp_disk_used, tmp_inodes_limit, tmp_inodes_percent, tmp_inodes_used, type (* = colunas padrão). O caractere &quot;+&quot; pode ser usado como um espaço reservado para as colunas padrão. Os caracteres % ou * podem ser usados como curinga. Os valores podem ser divididos por vírgulas (por exemplo, &quot;a,b,c&quot;) e/ou espaços em branco.

- Padrão: `[]`
- Requer um valor

### `--no-header`

Não gerar saída do cabeçalho da tabela

- Padrão: `false`
- Não aceita um valor

### `--date-fmt`

O formato de data (como uma string de formato de data do PHP)

- Padrão: `c`
- Requer um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `metrics:cpu`

\&lt;fg white=&quot;&quot; bg=&quot;red&quot;> BETA \&lt;/> Mostra o uso da CPU de um ambiente

```bash
magento-cloud cpu [-r|--range RANGE] [-i|--interval INTERVAL] [--to TO] [-1|--latest] [-s|--service SERVICE] [--type TYPE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT]
```

### `--range`, `-r`

O intervalo de tempo. As métricas serão carregadas por essa duração até a hora de término (—para). Você pode especificar unidades: horas (h), minutos (m) ou segundos (s). Mínimo \&lt;comment>5m\&lt;/comment>, máximo \&lt;comment>8h\&lt;/comment> ou mais (dependendo do projeto), padrão \&lt;comment>10m\&lt;/comment>.

- Requer um valor

### `--interval`, `-i`

O intervalo. O padrão é uma divisão do intervalo. Você pode especificar unidades: horas (h), minutos (m) ou segundos (s). Mínimo \&lt;comment>1m\&lt;/comment>.

- Requer um valor

### `--to`

A hora final. O padrão é agora.

- Requer um valor

### `--latest`, `-1`

Mostrar apenas o último ponto de dados único

- Padrão: `false`
- Não aceita um valor

### `--service`, `-s`

Filtrar por nome de serviço ou aplicativo Os caracteres % ou * podem ser usados como curinga.

- Padrão: `[]`
- Requer um valor

### `--type`

Filtrar por tipo de serviço (se — service não for fornecido). A versão não é necessária. Os caracteres % ou * podem ser usados como curinga.

- Padrão: `[]`
- Requer um valor

### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--environment`, `-e`

A ID do ambiente. Use &quot;.&quot; para selecionar o ambiente padrão do projeto.

- Requer um valor

### `--format`

O formato de saída: table, csv, tsv ou plain

- Padrão: `table`
- Requer um valor

### `--columns`, `-c`

Colunas a serem exibidas. Colunas disponíveis: carimbo de data e hora*, serviço*, usado*, limite*, porcentagem*, tipo (* = colunas padrão). O caractere &quot;+&quot; pode ser usado como um espaço reservado para as colunas padrão. Os caracteres % ou * podem ser usados como curinga. Os valores podem ser divididos por vírgulas (por exemplo, &quot;a,b,c&quot;) e/ou espaços em branco.

- Padrão: `[]`
- Requer um valor

### `--no-header`

Não gerar saída do cabeçalho da tabela

- Padrão: `false`
- Não aceita um valor

### `--date-fmt`

O formato de data (como uma string de formato de data do PHP)

- Padrão: `c`
- Requer um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `metrics:disk-usage`

Mostrar o uso do disco de um ambiente

```bash
magento-cloud disk [-B|--bytes] [-r|--range RANGE] [-i|--interval INTERVAL] [--to TO] [-1|--latest] [-s|--service SERVICE] [--type TYPE] [--tmp] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT]
```

### `--bytes`, `-B`

Mostrar tamanhos em bytes

- Padrão: `false`
- Não aceita um valor

### `--range`, `-r`

O intervalo de tempo. As métricas serão carregadas por essa duração até a hora de término (—para). Você pode especificar unidades: horas (h), minutos (m) ou segundos (s). Mínimo \&lt;comment>5m\&lt;/comment>, máximo \&lt;comment>8h\&lt;/comment> ou mais (dependendo do projeto), padrão \&lt;comment>10m\&lt;/comment>.

- Requer um valor

### `--interval`, `-i`

O intervalo. O padrão é uma divisão do intervalo. Você pode especificar unidades: horas (h), minutos (m) ou segundos (s). Mínimo \&lt;comment>1m\&lt;/comment>.

- Requer um valor

### `--to`

A hora final. O padrão é agora.

- Requer um valor

### `--latest`, `-1`

Mostrar apenas o último ponto de dados único

- Padrão: `false`
- Não aceita um valor

### `--service`, `-s`

Filtrar por nome de serviço ou aplicativo Os caracteres % ou * podem ser usados como curinga.

- Padrão: `[]`
- Requer um valor

### `--type`

Filtrar por tipo de serviço (se — service não for fornecido). A versão não é necessária. Os caracteres % ou * podem ser usados como curinga.

- Padrão: `[]`
- Requer um valor

### `--tmp`

Relatar uso de disco temporário (mostra colunas: timestamp, serviço, tmp_used, tmp_limit, tmp_percent, tmp_ipercent)

- Padrão: `false`
- Não aceita um valor

### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--environment`, `-e`

A ID do ambiente. Use &quot;.&quot; para selecionar o ambiente padrão do projeto.

- Requer um valor

### `--format`

O formato de saída: table, csv, tsv ou plain

- Padrão: `table`
- Requer um valor

### `--columns`, `-c`

Colunas a serem exibidas. Colunas disponíveis: timestamp*, service*, used*, limit*, percent*, ipercent*, tmp_percent*, ilimit, iused, tmp_ilimit, tmp_ipercent, tmp_iused, tmp_limit, tmp_used, type (* = colunas padrão). O caractere &quot;+&quot; pode ser usado como um espaço reservado para as colunas padrão. Os caracteres % ou * podem ser usados como curinga. Os valores podem ser divididos por vírgulas (por exemplo, &quot;a,b,c&quot;) e/ou espaços em branco.

- Padrão: `[]`
- Requer um valor

### `--no-header`

Não gerar saída do cabeçalho da tabela

- Padrão: `false`
- Não aceita um valor

### `--date-fmt`

O formato de data (como uma string de formato de data do PHP)

- Padrão: `c`
- Requer um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `metrics:memory`

\&lt;fg white=&quot;&quot; bg=&quot;red&quot;> BETA \&lt;/> Mostra o uso de memória de um ambiente

```bash
magento-cloud mem [-B|--bytes] [-r|--range RANGE] [-i|--interval INTERVAL] [--to TO] [-1|--latest] [-s|--service SERVICE] [--type TYPE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT]
```

### `--bytes`, `-B`

Mostrar tamanhos em bytes

- Padrão: `false`
- Não aceita um valor

### `--range`, `-r`

O intervalo de tempo. As métricas serão carregadas por essa duração até a hora de término (—para). Você pode especificar unidades: horas (h), minutos (m) ou segundos (s). Mínimo \&lt;comment>5m\&lt;/comment>, máximo \&lt;comment>8h\&lt;/comment> ou mais (dependendo do projeto), padrão \&lt;comment>10m\&lt;/comment>.

- Requer um valor

### `--interval`, `-i`

O intervalo. O padrão é uma divisão do intervalo. Você pode especificar unidades: horas (h), minutos (m) ou segundos (s). Mínimo \&lt;comment>1m\&lt;/comment>.

- Requer um valor

### `--to`

A hora final. O padrão é agora.

- Requer um valor

### `--latest`, `-1`

Mostrar apenas o último ponto de dados único

- Padrão: `false`
- Não aceita um valor

### `--service`, `-s`

Filtrar por nome de serviço ou aplicativo Os caracteres % ou * podem ser usados como curinga.

- Padrão: `[]`
- Requer um valor

### `--type`

Filtrar por tipo de serviço (se — service não for fornecido). A versão não é necessária. Os caracteres % ou * podem ser usados como curinga.

- Padrão: `[]`
- Requer um valor

### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--environment`, `-e`

A ID do ambiente. Use &quot;.&quot; para selecionar o ambiente padrão do projeto.

- Requer um valor

### `--format`

O formato de saída: table, csv, tsv ou plain

- Padrão: `table`
- Requer um valor

### `--columns`, `-c`

Colunas a serem exibidas. Colunas disponíveis: carimbo de data e hora*, serviço*, usado*, limite*, porcentagem*, tipo (* = colunas padrão). O caractere &quot;+&quot; pode ser usado como um espaço reservado para as colunas padrão. Os caracteres % ou * podem ser usados como curinga. Os valores podem ser divididos por vírgulas (por exemplo, &quot;a,b,c&quot;) e/ou espaços em branco.

- Padrão: `[]`
- Requer um valor

### `--no-header`

Não gerar saída do cabeçalho da tabela

- Padrão: `false`
- Não aceita um valor

### `--date-fmt`

O formato de data (como uma string de formato de data do PHP)

- Padrão: `c`
- Requer um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `mount:download`

Baixar arquivos de uma montagem, usando o &#39;rsync&#39;

```bash
magento-cloud mount:download [-a|--all] [-m|--mount MOUNT] [--target TARGET] [--source-path] [--delete] [--exclude EXCLUDE] [--include INCLUDE] [--refresh] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [-I|--instance INSTANCE] [-i|--identity-file IDENTITY-FILE]
```

### `--all`, `-a`

Baixar de todas as montagens

- Padrão: `false`
- Não aceita um valor

### `--mount`, `-m`

A montagem (como um caminho relativo ao aplicativo)

- Requer um valor

### `--target`

O diretório no qual os arquivos serão baixados. Se — all for usado, o caminho de montagem será anexado

- Requer um valor

### `--source-path`

Use o caminho de origem da montagem (em vez do caminho de montagem) como um subdiretório do destino, quando — all for usado

- Padrão: `false`
- Não aceita um valor

### `--delete`

Se os arquivos irrelevantes devem ser excluídos no diretório de destino

- Padrão: `false`
- Não aceita um valor

### `--exclude`

Arquivos a serem excluídos do download (padrão)

- Padrão: `[]`
- Requer um valor

### `--include`

Arquivo(s) não a excluir (padrão)

- Padrão: `[]`
- Requer um valor

### `--refresh`

Se o cache deve ser atualizado

- Padrão: `false`
- Não aceita um valor

### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--environment`, `-e`

A ID do ambiente. Use &quot;.&quot; para selecionar o ambiente padrão do projeto.

- Requer um valor

### `--app`, `-A`

O nome do aplicativo remoto

- Requer um valor

### `--worker`

Um nome de trabalhador

- Requer um valor

### `--instance`, `-I`

Uma ID de instância

- Requer um valor

### `--identity-file`, `-i`

Uma identidade SSH (chave privada) para usar

- Requer um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `mount:list`

Obter uma lista de montagens

```bash
magento-cloud mounts [--paths] [--refresh] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [-I|--instance INSTANCE]
```

### `--paths`

Saída somente dos caminhos de montagem (um por linha)

- Padrão: `false`
- Não aceita um valor

### `--refresh`

Se o cache deve ser atualizado

- Padrão: `false`
- Não aceita um valor

### `--format`

O formato de saída: table, csv, tsv ou plain

- Padrão: `table`
- Requer um valor

### `--columns`, `-c`

Colunas a serem exibidas. Colunas disponíveis: definição, caminho. Os caracteres % ou * podem ser usados como curinga. Os valores podem ser divididos por vírgulas (por exemplo, &quot;a,b,c&quot;) e/ou espaços em branco.

- Padrão: `[]`
- Requer um valor

### `--no-header`

Não gerar saída do cabeçalho da tabela

- Padrão: `false`
- Não aceita um valor

### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--environment`, `-e`

A ID do ambiente. Use &quot;.&quot; para selecionar o ambiente padrão do projeto.

- Requer um valor

### `--app`, `-A`

O nome do aplicativo remoto

- Requer um valor

### `--worker`

Um nome de trabalhador

- Requer um valor

### `--instance`, `-I`

Uma ID de instância

- Requer um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `mount:size`

Verificar o uso de montagens no disco

```bash
magento-cloud mount:size [-B|--bytes] [--refresh] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-i|--identity-file IDENTITY-FILE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [-I|--instance INSTANCE]
```

### `--bytes`, `-B`

Mostrar tamanhos em bytes

- Padrão: `false`
- Não aceita um valor

### `--refresh`

Atualizar o cache

- Padrão: `false`
- Não aceita um valor

### `--format`

O formato de saída: table, csv, tsv ou plain

- Padrão: `table`
- Requer um valor

### `--columns`, `-c`

Colunas a serem exibidas. Colunas disponíveis: disponível, máx, montagens, percent_used, tamanhos, usados. Os caracteres % ou * podem ser usados como curinga. Os valores podem ser divididos por vírgulas (por exemplo, &quot;a,b,c&quot;) e/ou espaços em branco.

- Padrão: `[]`
- Requer um valor

### `--no-header`

Não gerar saída do cabeçalho da tabela

- Padrão: `false`
- Não aceita um valor

### `--identity-file`, `-i`

Uma identidade SSH (chave privada) para usar

- Requer um valor

### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--environment`, `-e`

A ID do ambiente. Use &quot;.&quot; para selecionar o ambiente padrão do projeto.

- Requer um valor

### `--app`, `-A`

O nome do aplicativo remoto

- Requer um valor

### `--worker`

Um nome de trabalhador

- Requer um valor

### `--instance`, `-I`

Uma ID de instância

- Requer um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `mount:upload`

Carregar arquivos para uma montagem, usando o &#39;rsync&#39;

```bash
magento-cloud mount:upload [--source SOURCE] [-m|--mount MOUNT] [--delete] [--exclude EXCLUDE] [--include INCLUDE] [--refresh] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [-I|--instance INSTANCE] [-i|--identity-file IDENTITY-FILE]
```

### `--source`

Um diretório contendo arquivos para fazer upload

- Requer um valor

### `--mount`, `-m`

A montagem (como um caminho relativo ao aplicativo)

- Requer um valor

### `--delete`

Se os arquivos irrelevantes devem ser excluídos na montagem

- Padrão: `false`
- Não aceita um valor

### `--exclude`

Arquivos a serem excluídos do upload (padrão)

- Padrão: `[]`
- Requer um valor

### `--include`

Arquivo(s) não a excluir (padrão)

- Padrão: `[]`
- Requer um valor

### `--refresh`

Se o cache deve ser atualizado

- Padrão: `false`
- Não aceita um valor

### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--environment`, `-e`

A ID do ambiente. Use &quot;.&quot; para selecionar o ambiente padrão do projeto.

- Requer um valor

### `--app`, `-A`

O nome do aplicativo remoto

- Requer um valor

### `--worker`

Um nome de trabalhador

- Requer um valor

### `--instance`, `-I`

Uma ID de instância

- Requer um valor

### `--identity-file`, `-i`

Uma identidade SSH (chave privada) para usar

- Requer um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `operation:list`

\&lt;fg white=&quot;&quot; bg=&quot;red&quot;> BETA \&lt;/> Lista as operações de tempo de execução em um ambiente

```bash
magento-cloud ops [--full] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [--format FORMAT] [-c|--columns COLUMNS] [--no-header]
```

### `--full`

Não limite o comprimento do comando a ser exibido. O limite padrão é de 24 linhas.

- Padrão: `false`
- Não aceita um valor

### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--environment`, `-e`

A ID do ambiente. Use &quot;.&quot; para selecionar o ambiente padrão do projeto.

- Requer um valor

### `--app`, `-A`

O nome do aplicativo remoto

- Requer um valor

### `--worker`

Um nome de trabalhador

- Requer um valor

### `--format`

O formato de saída: table, csv, tsv ou plain

- Padrão: `table`
- Requer um valor

### `--columns`, `-c`

Colunas a serem exibidas. Colunas disponíveis: service*, name*, start*, role, stop (* = colunas padrão). O caractere &quot;+&quot; pode ser usado como um espaço reservado para as colunas padrão. Os caracteres % ou * podem ser usados como curinga. Os valores podem ser divididos por vírgulas (por exemplo, &quot;a,b,c&quot;) e/ou espaços em branco.

- Padrão: `[]`
- Requer um valor

### `--no-header`

Não gerar saída do cabeçalho da tabela

- Padrão: `false`
- Não aceita um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `operation:run`

\&lt;fg white=&quot;&quot; bg=&quot;red&quot;> BETA \&lt;/> Executar uma operação no ambiente

```bash
magento-cloud operation:run [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [-W|--no-wait] [--wait] [--] [<operation>]
```


### `operation`

O nome da operação


### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--environment`, `-e`

A ID do ambiente. Use &quot;.&quot; para selecionar o ambiente padrão do projeto.

- Requer um valor

### `--app`, `-A`

O nome do aplicativo remoto

- Requer um valor

### `--worker`

Um nome de trabalhador

- Requer um valor

### `--no-wait`, `-W`

Não aguarde a conclusão da operação

- Padrão: `false`
- Não aceita um valor

### `--wait`

Aguardar a conclusão da operação (padrão)

- Padrão: `false`
- Não aceita um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `project:clear-build-cache`

Limpar o cache de criação de um projeto

```bash
magento-cloud project:clear-build-cache [-p|--project PROJECT]
```

### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `project:get`

Clonar um projeto localmente

```bash
magento-cloud get [-e|--environment ENVIRONMENT] [--depth DEPTH] [--build] [-p|--project PROJECT] [-i|--identity-file IDENTITY-FILE] [--] [<project>] [<directory>]
```


### `project`

A ID do projeto


### `directory`

O diretório para o qual clonar. O padrão é o título do projeto


### `--environment`, `-e`

A ID de ambiente a ser clonada. O padrão é o padrão do projeto ou o primeiro ambiente disponível

- Requer um valor

### `--depth`

Criar um clone superficial: limite o número de confirmações no histórico

- Requer um valor

### `--build`

Criar o projeto após a clonagem

- Padrão: `false`
- Não aceita um valor

### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--identity-file`, `-i`

Uma identidade SSH (chave privada) para usar

- Requer um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `project:info`

Ler ou definir propriedades de um projeto

```bash
magento-cloud project:info [--refresh] [--date-fmt DATE-FMT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT] [-W|--no-wait] [--wait] [--] [<property>] [<value>]
```


### `property`

O nome da propriedade


### `value`

Definir um novo valor para a propriedade


### `--refresh`

Se o cache deve ser atualizado

- Padrão: `false`
- Não aceita um valor

### `--date-fmt`

O formato de data (como uma string de formato de data do PHP)

- Padrão: `c`
- Requer um valor

### `--format`

O formato de saída: table, csv, tsv ou plain

- Padrão: `table`
- Requer um valor

### `--columns`, `-c`

Colunas a serem exibidas. Os caracteres % ou * podem ser usados como curinga. Os valores podem ser divididos por vírgulas (por exemplo, &quot;a,b,c&quot;) e/ou espaços em branco.

- Padrão: `[]`
- Requer um valor

### `--no-header`

Não gerar saída do cabeçalho da tabela

- Padrão: `false`
- Não aceita um valor

### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--no-wait`, `-W`

Não aguarde a conclusão da operação

- Padrão: `false`
- Não aceita um valor

### `--wait`

Aguardar a conclusão da operação (padrão)

- Padrão: `false`
- Não aceita um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `project:list`

Obter uma lista de todos os projetos ativos

```bash
magento-cloud projects [--pipe] [--region REGION] [--title TITLE] [--my] [--refresh REFRESH] [--sort SORT] [--reverse] [--page PAGE] [-c|--count COUNT] [--format FORMAT] [--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT]
```

### `--pipe`

Gerar uma lista simples de IDs de projeto. Desativa a paginação.

- Padrão: `false`
- Não aceita um valor

### `--region`

Filtrar por região (correspondência exata)

- Requer um valor

### `--title`

Filtrar por título (pesquisa que não diferencia maiúsculas de minúsculas)

- Requer um valor

### `--my`

Exibir somente seus projetos

- Padrão: `false`
- Não aceita um valor

### `--refresh`

Atualizar ou não a lista

- Padrão: `1`
- Requer um valor

### `--sort`

Uma propriedade para classificar por

- Padrão: `title`
- Requer um valor

### `--reverse`

Classificar em ordem inversa (descendente)

- Padrão: `false`
- Não aceita um valor

### `--page`

Número da página. Isto ativa a paginação, apesar da configuração ou — count. Ignorado se o — pipe for indicado.

- Requer um valor

### `--count`, `-c`

O número de projetos a serem exibidos por página. Use 0 para desativar a paginação. Ignorado se o — page for especificado.

- Requer um valor

### `--format`

O formato de saída: table, csv, tsv ou plain

- Padrão: `table`
- Requer um valor

### `--columns`

Colunas a serem exibidas. Colunas disponíveis: id*, título*, região*, created_at, organization_id, organization_label, organization_name, status (* = colunas padrão). O caractere &quot;+&quot; pode ser usado como um espaço reservado para as colunas padrão. Os caracteres % ou * podem ser usados como curinga. Os valores podem ser divididos por vírgulas (por exemplo, &quot;a,b,c&quot;) e/ou espaços em branco.

- Padrão: `[]`
- Requer um valor

### `--no-header`

Não gerar saída do cabeçalho da tabela

- Padrão: `false`
- Não aceita um valor

### `--date-fmt`

O formato de data (como uma string de formato de data do PHP)

- Padrão: `c`
- Requer um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `project:set-remote`

Definir o projeto remoto para o repositório Git atual

```bash
magento-cloud set-remote [<project>]
```


### `project`

A ID do projeto


### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `repo:cat`

Ler um arquivo no repositório do projeto

```bash
magento-cloud repo:cat [-c|--commit COMMIT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--] <path>
```


### `path`

O caminho para o arquivo

- Obrigatório

### `--commit`, `-c`

O SHA de confirmação. Isso também pode aceitar os sufixos &quot;HEAD&quot; e acento circunflexo (^) ou til (~) para confirmações principais.

- Requer um valor

### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--environment`, `-e`

A ID do ambiente. Use &quot;.&quot; para selecionar o ambiente padrão do projeto.

- Requer um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `repo:ls`

Listar arquivos no repositório do projeto

```bash
magento-cloud repo:ls [-d|--directories] [-f|--files] [--git-style] [-c|--commit COMMIT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--] [<path>]
```


### `path`

O caminho para um subdiretório


### `--directories`, `-d`

Mostrar somente diretórios

- Padrão: `false`
- Não aceita um valor

### `--files`, `-f`

Mostrar somente arquivos

- Padrão: `false`
- Não aceita um valor

### `--git-style`

Saída de estilo semelhante a &quot;git ls-tree&quot;

- Padrão: `false`
- Não aceita um valor

### `--commit`, `-c`

O SHA de confirmação. Isso também pode aceitar os sufixos &quot;HEAD&quot; e acento circunflexo (^) ou til (~) para confirmações principais.

- Requer um valor

### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--environment`, `-e`

A ID do ambiente. Use &quot;.&quot; para selecionar o ambiente padrão do projeto.

- Requer um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `repo:read`

Ler um diretório ou arquivo no repositório do projeto

```bash
magento-cloud read [-c|--commit COMMIT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--] [<path>]
```


### `path`

O caminho para o diretório ou arquivo


### `--commit`, `-c`

O SHA de confirmação. Isso também pode aceitar os sufixos &quot;HEAD&quot; e acento circunflexo (^) ou til (~) para confirmações principais.

- Requer um valor

### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--environment`, `-e`

A ID do ambiente. Use &quot;.&quot; para selecionar o ambiente padrão do projeto.

- Requer um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `route:get`

Exibir informações detalhadas sobre um roteiro

```bash
magento-cloud route:get [--id ID] [-1|--primary] [-P|--property PROPERTY] [--refresh] [--date-fmt DATE-FMT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [-i|--identity-file IDENTITY-FILE] [--] [<route>]
```


### `route`

O URL original da rota


### `--id`

Uma ID de rota para selecionar

- Requer um valor

### `--primary`, `-1`

Selecionar a rota principal

- Padrão: `false`
- Não aceita um valor

### `--property`, `-P`

A propriedade a ser exibida

- Requer um valor

### `--refresh`

Ignorar o cache de rotas

- Padrão: `false`
- Não aceita um valor

### `--date-fmt`

O formato de data (como uma string de formato de data do PHP)

- Padrão: `c`
- Requer um valor

### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--environment`, `-e`

A ID do ambiente. Use &quot;.&quot; para selecionar o ambiente padrão do projeto.

- Requer um valor

### `--app`, `-A`

[Opção obsoleta, não é mais usada]

- Requer um valor

### `--identity-file`, `-i`

[Opção obsoleta, não é mais usada]

- Requer um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `route:list`

Listar todas as rotas de um ambiente

```bash
magento-cloud routes [--refresh] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--] [<environment>]
```


### `environment`

A ID do ambiente


### `--refresh`

Ignorar o cache de rotas

- Padrão: `false`
- Não aceita um valor

### `--format`

O formato de saída: table, csv, tsv ou plain

- Padrão: `table`
- Requer um valor

### `--columns`, `-c`

Colunas a serem exibidas. Colunas disponíveis: route*, type*, to*, url (* = default columns). O caractere &quot;+&quot; pode ser usado como um espaço reservado para as colunas padrão. Os caracteres % ou * podem ser usados como curinga. Os valores podem ser divididos por vírgulas (por exemplo, &quot;a,b,c&quot;) e/ou espaços em branco.

- Padrão: `[]`
- Requer um valor

### `--no-header`

Não gerar saída do cabeçalho da tabela

- Padrão: `false`
- Não aceita um valor

### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--environment`, `-e`

A ID do ambiente. Use &quot;.&quot; para selecionar o ambiente padrão do projeto.

- Requer um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `self:install`

Instalar ou atualizar arquivos de configuração da CLI

```bash
magento-cloud self:install [--shell-type SHELL-TYPE]
```

### `--shell-type`

O tipo de shell para preenchimento automático (bash ou zsh)

- Requer um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `self:update`

Atualize a CLI para a versão mais recente

```bash
magento-cloud update [--no-major] [--unstable] [--manifest MANIFEST] [--current-version CURRENT-VERSION] [--timeout TIMEOUT]
```

### `--no-major`

Atualizar somente entre versões secundárias ou de patch

- Padrão: `false`
- Não aceita um valor

### `--unstable`

Atualização para uma nova versão instável, se disponível

- Padrão: `false`
- Não aceita um valor

### `--manifest`

Substituir o local do arquivo de manifesto

- Requer um valor

### `--current-version`

Substituir a versão atual

- Requer um valor

### `--timeout`

Um tempo limite para a verificação da versão

- Padrão: `30`
- Requer um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `service:list`

Listar serviços no projeto

```bash
magento-cloud services [--refresh] [--pipe] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header]
```

### `--refresh`

Se o cache deve ser atualizado

- Padrão: `false`
- Não aceita um valor

### `--pipe`

Gerar uma lista apenas de nomes de serviço

- Padrão: `false`
- Não aceita um valor

### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--environment`, `-e`

A ID do ambiente. Use &quot;.&quot; para selecionar o ambiente padrão do projeto.

- Requer um valor

### `--format`

O formato de saída: table, csv, tsv ou plain

- Padrão: `table`
- Requer um valor

### `--columns`, `-c`

Colunas a serem exibidas. Colunas disponíveis: disco, nome, tamanho, tipo. Os caracteres % ou * podem ser usados como curinga. Os valores podem ser divididos por vírgulas (por exemplo, &quot;a,b,c&quot;) e/ou espaços em branco.

- Padrão: `[]`
- Requer um valor

### `--no-header`

Não gerar saída do cabeçalho da tabela

- Padrão: `false`
- Não aceita um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `service:mongo:dump`

Criar um despejo de arquivo binário de dados do MongoDB

```bash
magento-cloud mongodump [-c|--collection COLLECTION] [-z|--gzip] [-o|--stdout] [-r|--relationship RELATIONSHIP] [-i|--identity-file IDENTITY-FILE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP]
```

### `--collection`, `-c`

A coleção para despejo

- Requer um valor

### `--gzip`, `-z`

Compactar o despejo usando gzip

- Padrão: `false`
- Não aceita um valor

### `--stdout`, `-o`

Saída para STDOUT em vez de um arquivo

- Padrão: `false`
- Não aceita um valor

### `--relationship`, `-r`

O relacionamento de serviço a ser usado

- Requer um valor

### `--identity-file`, `-i`

Uma identidade SSH (chave privada) para usar

- Requer um valor

### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--environment`, `-e`

A ID do ambiente. Use &quot;.&quot; para selecionar o ambiente padrão do projeto.

- Requer um valor

### `--app`, `-A`

O nome do aplicativo remoto

- Requer um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `service:mongo:export`

Exportar dados do MongoDB

```bash
magento-cloud mongoexport [-c|--collection COLLECTION] [--jsonArray] [--type TYPE] [-f|--fields FIELDS] [-r|--relationship RELATIONSHIP] [-i|--identity-file IDENTITY-FILE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP]
```

### `--collection`, `-c`

A coleção a ser exportada

- Requer um valor

### `--jsonArray`

Exportar dados como uma única matriz JSON

- Padrão: `false`
- Não aceita um valor

### `--type`

O tipo de exportação, por exemplo, &quot;csv&quot;

- Requer um valor

### `--fields`, `-f`

Os campos a serem exportados

- Padrão: `[]`
- Requer um valor

### `--relationship`, `-r`

O relacionamento de serviço a ser usado

- Requer um valor

### `--identity-file`, `-i`

Uma identidade SSH (chave privada) para usar

- Requer um valor

### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--environment`, `-e`

A ID do ambiente. Use &quot;.&quot; para selecionar o ambiente padrão do projeto.

- Requer um valor

### `--app`, `-A`

O nome do aplicativo remoto

- Requer um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `service:mongo:restore`

Restaurar um despejo de arquivo binário de dados no MongoDB

```bash
magento-cloud mongorestore [-c|--collection COLLECTION] [-r|--relationship RELATIONSHIP] [-i|--identity-file IDENTITY-FILE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP]
```

### `--collection`, `-c`

A coleção a restaurar

- Requer um valor

### `--relationship`, `-r`

O relacionamento de serviço a ser usado

- Requer um valor

### `--identity-file`, `-i`

Uma identidade SSH (chave privada) para usar

- Requer um valor

### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--environment`, `-e`

A ID do ambiente. Use &quot;.&quot; para selecionar o ambiente padrão do projeto.

- Requer um valor

### `--app`, `-A`

O nome do aplicativo remoto

- Requer um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `service:mongo:shell`

Usar o shell MongoDB

```bash
magento-cloud mongo [--eval EVAL] [-r|--relationship RELATIONSHIP] [-i|--identity-file IDENTITY-FILE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP]
```

### `--eval`

Passar um fragmento de JavaScript para o shell

- Requer um valor

### `--relationship`, `-r`

O relacionamento de serviço a ser usado

- Requer um valor

### `--identity-file`, `-i`

Uma identidade SSH (chave privada) para usar

- Requer um valor

### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--environment`, `-e`

A ID do ambiente. Use &quot;.&quot; para selecionar o ambiente padrão do projeto.

- Requer um valor

### `--app`, `-A`

O nome do aplicativo remoto

- Requer um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `service:redis-cli`

Acesse a CLI Redis

```bash
magento-cloud redis [-r|--relationship RELATIONSHIP] [-i|--identity-file IDENTITY-FILE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--] [<args>]
```


### `args`

Argumentos a serem adicionados ao comando Redis


### `--relationship`, `-r`

O relacionamento de serviço a ser usado

- Requer um valor

### `--identity-file`, `-i`

Uma identidade SSH (chave privada) para usar

- Requer um valor

### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--environment`, `-e`

A ID do ambiente. Use &quot;.&quot; para selecionar o ambiente padrão do projeto.

- Requer um valor

### `--app`, `-A`

O nome do aplicativo remoto

- Requer um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `snapshot:create`

Criar um instantâneo de um ambiente

```bash
magento-cloud backup [--live] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<environment>]
```


### `environment`

O ambiente


### `--live`

Live backup: não interrompa o ambiente. Se definido, o ambiente estará em execução e aberto a conexões durante o backup. Isso reduz o tempo de inatividade, correndo o risco de fazer backup dos dados em um estado inconsistente.

- Padrão: `false`
- Não aceita um valor

### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--environment`, `-e`

A ID do ambiente. Use &quot;.&quot; para selecionar o ambiente padrão do projeto.

- Requer um valor

### `--no-wait`, `-W`

Não aguarde a conclusão da operação

- Padrão: `false`
- Não aceita um valor

### `--wait`

Aguardar a conclusão da operação (padrão)

- Padrão: `false`
- Não aceita um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `snapshot:delete`

Excluir um instantâneo do ambiente

```bash
magento-cloud snapshot:delete [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<id>]
```


### `id`

A ID do instantâneo. Necessário no modo não interativo.


### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--environment`, `-e`

A ID do ambiente. Use &quot;.&quot; para selecionar o ambiente padrão do projeto.

- Requer um valor

### `--no-wait`, `-W`

Não aguarde a conclusão da operação

- Padrão: `false`
- Não aceita um valor

### `--wait`

Aguardar a conclusão da operação (padrão)

- Padrão: `false`
- Não aceita um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `snapshot:get`

Exibir um instantâneo do ambiente

```bash
magento-cloud snapshot:get [-P|--property PROPERTY] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--date-fmt DATE-FMT] [--] [<id>]
```


### `id`

A ID do instantâneo. O padrão é o mais recente.


### `--property`, `-P`

A propriedade a ser exibida.

- Requer um valor

### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--environment`, `-e`

A ID do ambiente. Use &quot;.&quot; para selecionar o ambiente padrão do projeto.

- Requer um valor

### `--date-fmt`

O formato de data (como uma string de formato de data do PHP)

- Padrão: `c`
- Requer um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `snapshot:list`

Listar instantâneos disponíveis de um ambiente

```bash
magento-cloud snapshots [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT]
```

### `--format`

O formato de saída: table, csv, tsv ou plain

- Padrão: `table`
- Requer um valor

### `--columns`, `-c`

Colunas a serem exibidas. Os caracteres % ou * podem ser usados como curinga. Os valores podem ser divididos por vírgulas (por exemplo, &quot;a,b,c&quot;) e/ou espaços em branco.

- Padrão: `[]`
- Requer um valor

### `--no-header`

Não gerar saída do cabeçalho da tabela

- Padrão: `false`
- Não aceita um valor

### `--date-fmt`

O formato de data (como uma string de formato de data do PHP)

- Padrão: `c`
- Requer um valor

### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--environment`, `-e`

A ID do ambiente. Use &quot;.&quot; para selecionar o ambiente padrão do projeto.

- Requer um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `snapshot:restore`

Restaurar um instantâneo do ambiente

```bash
magento-cloud snapshot:restore [--target TARGET] [--branch-from BRANCH-FROM] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<snapshot>]
```


### `snapshot`

O nome do snapshot. O padrão é o mais recente


### `--target`

O ambiente para o qual restaurar. Define como padrão o ambiente atual do snapshot

- Requer um valor

### `--branch-from`

Se o — target ainda não existir, isto especifica o pai do novo ambiente

- Requer um valor

### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--environment`, `-e`

A ID do ambiente. Use &quot;.&quot; para selecionar o ambiente padrão do projeto.

- Requer um valor

### `--no-wait`, `-W`

Não aguarde a conclusão da operação

- Padrão: `false`
- Não aceita um valor

### `--wait`

Aguardar a conclusão da operação (padrão)

- Padrão: `false`
- Não aceita um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `source-operation:list`

Listar operações de origem em um ambiente

```bash
magento-cloud source-ops [--full] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header]
```

### `--full`

Não limite o comprimento do comando a ser exibido. O limite padrão é de 24 linhas.

- Padrão: `false`
- Não aceita um valor

### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--environment`, `-e`

A ID do ambiente. Use &quot;.&quot; para selecionar o ambiente padrão do projeto.

- Requer um valor

### `--format`

O formato de saída: table, csv, tsv ou plain

- Padrão: `table`
- Requer um valor

### `--columns`, `-c`

Colunas a serem exibidas. Colunas disponíveis: aplicativo, comando, operação. Os caracteres % ou * podem ser usados como curinga. Os valores podem ser divididos por vírgulas (por exemplo, &quot;a,b,c&quot;) e/ou espaços em branco.

- Padrão: `[]`
- Requer um valor

### `--no-header`

Não gerar saída do cabeçalho da tabela

- Padrão: `false`
- Não aceita um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `source-operation:run`

Executar uma operação de origem

```bash
magento-cloud source-operation:run [--variable VARIABLE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<operation>]
```


### `operation`

O nome da operação


### `--variable`

Uma variável a ser definida durante a operação, no formato \&lt;info>type:name=value\&lt;/info>

- Padrão: `[]`
- Requer um valor

### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--environment`, `-e`

A ID do ambiente. Use &quot;.&quot; para selecionar o ambiente padrão do projeto.

- Requer um valor

### `--no-wait`, `-W`

Não aguarde a conclusão da operação

- Padrão: `false`
- Não aceita um valor

### `--wait`

Aguardar a conclusão da operação (padrão)

- Padrão: `false`
- Não aceita um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `ssh-cert:load`

Gerar um certificado SSH

```bash
magento-cloud ssh-cert:load [--refresh-only] [--new] [--new-key]
```

### `--refresh-only`

Somente atualize o certificado, se necessário (não grave a configuração SSH)

- Padrão: `false`
- Não aceita um valor

### `--new`

Forçar a atualização do certificado

- Padrão: `false`
- Não aceita um valor

### `--new-key`

[Obsoleto] Em vez disso, use — new

- Padrão: `false`
- Não aceita um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `ssh-key:add`

Adicionar uma nova chave SSH

```bash
magento-cloud ssh-key:add [--name NAME] [--] [<path>]
```


### `path`

O caminho para uma chave pública SSH existente


### `--name`

Um nome para identificar a chave

- Requer um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `ssh-key:delete`

Excluir uma chave SSH

```bash
magento-cloud ssh-key:delete [<id>]
```


### `id`

A ID da chave SSH a ser excluída


### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `ssh-key:list`

Obter uma lista de chaves SSH em sua conta

```bash
magento-cloud ssh-keys [--format FORMAT] [-c|--columns COLUMNS] [--no-header]
```

### `--format`

O formato de saída: table, csv, tsv ou plain

- Padrão: `table`
- Requer um valor

### `--columns`, `-c`

Colunas a serem exibidas. Colunas disponíveis: id*, title*, path*, impressão digital (* = colunas padrão). O caractere &quot;+&quot; pode ser usado como um espaço reservado para as colunas padrão. Os caracteres % ou * podem ser usados como curinga. Os valores podem ser divididos por vírgulas (por exemplo, &quot;a,b,c&quot;) e/ou espaços em branco.

- Padrão: `[]`
- Requer um valor

### `--no-header`

Não gerar saída do cabeçalho da tabela

- Padrão: `false`
- Não aceita um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `subscription:info`

Ler ou modificar propriedades de assinatura

```bash
magento-cloud subscription:info [-s|--id ID] [--date-fmt DATE-FMT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT] [--] [<property>] [<value>]
```


### `property`

O nome da propriedade


### `value`

Definir um novo valor para a propriedade


### `--id`, `-s`

A ID da assinatura

- Requer um valor

### `--date-fmt`

O formato de data (como uma string de formato de data do PHP)

- Padrão: `c`
- Requer um valor

### `--format`

O formato de saída: table, csv, tsv ou plain

- Padrão: `table`
- Requer um valor

### `--columns`, `-c`

Colunas a serem exibidas. Os caracteres % ou * podem ser usados como curinga. Os valores podem ser divididos por vírgulas (por exemplo, &quot;a,b,c&quot;) e/ou espaços em branco.

- Padrão: `[]`
- Requer um valor

### `--no-header`

Não gerar saída do cabeçalho da tabela

- Padrão: `false`
- Não aceita um valor

### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `tunnel:close`

Fechar túneis SSH

```bash
magento-cloud tunnel:close [-a|--all] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP]
```

### `--all`, `-a`

Fechar todos os túneis

- Padrão: `false`
- Não aceita um valor

### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--environment`, `-e`

A ID do ambiente. Use &quot;.&quot; para selecionar o ambiente padrão do projeto.

- Requer um valor

### `--app`, `-A`

O nome do aplicativo remoto

- Requer um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `tunnel:info`

Exibir informações de relacionamento para túneis SSH

```bash
magento-cloud tunnel:info [-P|--property PROPERTY] [-c|--encode] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP]
```

### `--property`, `-P`

A propriedade de relacionamento a ser exibida

- Requer um valor

### `--encode`, `-c`

Saída como JSON codificado em base64

- Padrão: `false`
- Não aceita um valor

### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--environment`, `-e`

A ID do ambiente. Use &quot;.&quot; para selecionar o ambiente padrão do projeto.

- Requer um valor

### `--app`, `-A`

O nome do aplicativo remoto

- Requer um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `tunnel:list`

Listar túneis SSH

```bash
magento-cloud tunnels [-a|--all] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--format FORMAT] [-c|--columns COLUMNS] [--no-header]
```

### `--all`, `-a`

Exibir todos os túneis

- Padrão: `false`
- Não aceita um valor

### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--environment`, `-e`

A ID do ambiente. Use &quot;.&quot; para selecionar o ambiente padrão do projeto.

- Requer um valor

### `--app`, `-A`

O nome do aplicativo remoto

- Requer um valor

### `--format`

O formato de saída: table, csv, tsv ou plain

- Padrão: `table`
- Requer um valor

### `--columns`, `-c`

Colunas a serem exibidas. Colunas disponíveis: porta*, projeto*, ambiente*, aplicativo*, relacionamento*, url (* = colunas padrão). O caractere &quot;+&quot; pode ser usado como um espaço reservado para as colunas padrão. Os caracteres % ou * podem ser usados como curinga. Os valores podem ser divididos por vírgulas (por exemplo, &quot;a,b,c&quot;) e/ou espaços em branco.

- Padrão: `[]`
- Requer um valor

### `--no-header`

Não gerar saída do cabeçalho da tabela

- Padrão: `false`
- Não aceita um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `tunnel:open`

Abrir túneis SSH para os relacionamentos de um aplicativo

```bash
magento-cloud tunnel:open [-g|--gateway-ports] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [-i|--identity-file IDENTITY-FILE]
```

### `--gateway-ports`, `-g`

Permitir que hosts remotos se conectem a portas encaminhadas locais

- Padrão: `false`
- Não aceita um valor

### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--environment`, `-e`

A ID do ambiente. Use &quot;.&quot; para selecionar o ambiente padrão do projeto.

- Requer um valor

### `--app`, `-A`

O nome do aplicativo remoto

- Requer um valor

### `--identity-file`, `-i`

Uma identidade SSH (chave privada) para usar

- Requer um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `tunnel:single`

Abrir um único túnel SSH para uma relação de aplicativo

```bash
magento-cloud tunnel:single [--port PORT] [-g|--gateway-ports] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [-r|--relationship RELATIONSHIP] [-i|--identity-file IDENTITY-FILE]
```

### `--port`

A porta local

- Requer um valor

### `--gateway-ports`, `-g`

Permitir que hosts remotos se conectem a portas encaminhadas locais

- Padrão: `false`
- Não aceita um valor

### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--environment`, `-e`

A ID do ambiente. Use &quot;.&quot; para selecionar o ambiente padrão do projeto.

- Requer um valor

### `--app`, `-A`

O nome do aplicativo remoto

- Requer um valor

### `--relationship`, `-r`

O relacionamento de serviço a ser usado

- Requer um valor

### `--identity-file`, `-i`

Uma identidade SSH (chave privada) para usar

- Requer um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `user:add`

Adicionar um usuário ao projeto

```bash
magento-cloud user:add [-r|--role ROLE] [--force-invite] [-p|--project PROJECT] [-W|--no-wait] [--wait] [--] [<email>]
```


### `email`

O endereço de email do usuário


### `--role`, `-r`

A função do projeto do usuário (&quot;administrador&quot; ou &quot;visualizador&quot;) ou a função do tipo de ambiente (por exemplo, &quot;preparo:colaborador&quot; ou &quot;produção:visualizador&quot;). Para remover um usuário de um tipo de ambiente, defina a função como &quot;nenhum&quot;. Os caracteres % ou * podem ser usados como curinga para o tipo de ambiente, por exemplo, &#39;%:viewer&#39; para conceder ao usuário a função &#39;viewer&#39; em todos os tipos. A função pode ser abreviada. Por exemplo, &quot;produção:v&quot;.

- Padrão: `[]`
- Requer um valor

### `--force-invite`

Enviar um convite, mesmo que um já tenha sido enviado

- Padrão: `false`
- Não aceita um valor

### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--no-wait`, `-W`

Não aguarde a conclusão da operação

- Padrão: `false`
- Não aceita um valor

### `--wait`

Aguardar a conclusão da operação (padrão)

- Padrão: `false`
- Não aceita um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `user:delete`

Excluir um usuário do projeto

```bash
magento-cloud user:delete [-p|--project PROJECT] [-W|--no-wait] [--wait] [--] <email>
```


### `email`

O endereço de email do usuário

- Obrigatório

### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--no-wait`, `-W`

Não aguarde a conclusão da operação

- Padrão: `false`
- Não aceita um valor

### `--wait`

Aguardar a conclusão da operação (padrão)

- Padrão: `false`
- Não aceita um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `user:get`

Exibir as funções de um usuário

```bash
magento-cloud user:get [-l|--level LEVEL] [--pipe] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [-r|--role ROLE] [--] [<email>]
```


### `email`

O endereço de email do usuário


### `--level`, `-l`

O nível de função (&quot;projeto&quot; ou &quot;ambiente&quot;)

- Requer um valor

### `--pipe`

Transmitir a função para stdout (após fazer quaisquer alterações)

- Padrão: `false`
- Não aceita um valor

### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--environment`, `-e`

A ID do ambiente. Use &quot;.&quot; para selecionar o ambiente padrão do projeto.

- Requer um valor

### `--no-wait`, `-W`

Não aguarde a conclusão da operação

- Padrão: `false`
- Não aceita um valor

### `--wait`

Aguardar a conclusão da operação (padrão)

- Padrão: `false`
- Não aceita um valor

### `--role`, `-r`

[Obsoleto: use user:update para alterar a(s) função(ões) de um usuário]

- Requer um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `user:list`

Listar usuários do projeto

```bash
magento-cloud users [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT]
```

### `--format`

O formato de saída: table, csv, tsv ou plain

- Padrão: `table`
- Requer um valor

### `--columns`, `-c`

Colunas a serem exibidas. Colunas disponíveis: email*, nome*, função*, id*, granted_at, updated_at (* = colunas padrão). O caractere &quot;+&quot; pode ser usado como um espaço reservado para as colunas padrão. Os caracteres % ou * podem ser usados como curinga. Os valores podem ser divididos por vírgulas (por exemplo, &quot;a,b,c&quot;) e/ou espaços em branco.

- Padrão: `[]`
- Requer um valor

### `--no-header`

Não gerar saída do cabeçalho da tabela

- Padrão: `false`
- Não aceita um valor

### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `user:update`

Atualizar funções de usuário em um projeto

```bash
magento-cloud user:update [-r|--role ROLE] [-p|--project PROJECT] [-W|--no-wait] [--wait] [--] [<email>]
```


### `email`

O endereço de email do usuário


### `--role`, `-r`

A função do projeto do usuário (&quot;administrador&quot; ou &quot;visualizador&quot;) ou a função do tipo de ambiente (por exemplo, &quot;preparo:colaborador&quot; ou &quot;produção:visualizador&quot;). Para remover um usuário de um tipo de ambiente, defina a função como &quot;nenhum&quot;. Os caracteres % ou * podem ser usados como curinga para o tipo de ambiente, por exemplo, &#39;%:viewer&#39; para conceder ao usuário a função &#39;viewer&#39; em todos os tipos. A função pode ser abreviada. Por exemplo, &quot;produção:v&quot;.

- Padrão: `[]`
- Requer um valor

### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--no-wait`, `-W`

Não aguarde a conclusão da operação

- Padrão: `false`
- Não aceita um valor

### `--wait`

Aguardar a conclusão da operação (padrão)

- Padrão: `false`
- Não aceita um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `variable:create`

Criar uma variável

```bash
magento-cloud variable:create [-u|--update] [-l|--level LEVEL] [--name NAME] [--value VALUE] [--json JSON] [--sensitive SENSITIVE] [--prefix PREFIX] [--enabled ENABLED] [--inheritable INHERITABLE] [--visible-build VISIBLE-BUILD] [--visible-runtime VISIBLE-RUNTIME] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<name>]
```


### `name`

O nome da variável


### `--update`, `-u`

Atualizar a variável se ela já existir

- Padrão: `false`
- Não aceita um valor

### `--level`, `-l`

O nível no qual a variável será definida (&quot;projeto&quot; ou &quot;ambiente&quot;)

- Requer um valor

### `--name`

O nome da variável

- Requer um valor

### `--value`

O valor da variável

- Requer um valor

### `--json`

Se o valor da variável é formatado em JSON

- Padrão: `false`
- Requer um valor

### `--sensitive`

Se o valor da variável é sensível

- Padrão: `false`
- Requer um valor

### `--prefix`

O prefixo do nome da variável que pode determinar seu tipo, por exemplo, &quot;env&quot;. Aplicável somente se o nome ainda não contiver um prefixo. (por exemplo, &quot;nenhum&quot; ou &quot;env:&quot;)

- Padrão: `none`
- Requer um valor

### `--enabled`

Se a variável deve ser ativada no ambiente

- Padrão: `true`
- Requer um valor

### `--inheritable`

Se a variável é herdável por ambientes secundários

- Padrão: `true`
- Requer um valor

### `--visible-build`

Se a variável deve estar visível no momento da criação

- Requer um valor

### `--visible-runtime`

Se a variável deve estar visível no tempo de execução

- Padrão: `true`
- Requer um valor

### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--environment`, `-e`

A ID do ambiente. Use &quot;.&quot; para selecionar o ambiente padrão do projeto.

- Requer um valor

### `--no-wait`, `-W`

Não aguarde a conclusão da operação

- Padrão: `false`
- Não aceita um valor

### `--wait`

Aguardar a conclusão da operação (padrão)

- Padrão: `false`
- Não aceita um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `variable:delete`

Excluir uma variável

```bash
magento-cloud variable:delete [-l|--level LEVEL] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] <name>
```


### `name`

O nome da variável

- Obrigatório

### `--level`, `-l`

O nível da variável (&#39;project&#39;, &#39;environment&#39;, &#39;p&#39; ou &#39;e&#39;)

- Requer um valor

### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--environment`, `-e`

A ID do ambiente. Use &quot;.&quot; para selecionar o ambiente padrão do projeto.

- Requer um valor

### `--no-wait`, `-W`

Não aguarde a conclusão da operação

- Padrão: `false`
- Não aceita um valor

### `--wait`

Aguardar a conclusão da operação (padrão)

- Padrão: `false`
- Não aceita um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `variable:get`

Exibir uma variável

```bash
magento-cloud vget [-P|--property PROPERTY] [-l|--level LEVEL] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--pipe] [--] [<name>]
```


### `name`

O nome da variável


### `--property`, `-P`

Exibir uma única propriedade de variável

- Requer um valor

### `--level`, `-l`

O nível da variável (&#39;project&#39;, &#39;environment&#39;, &#39;p&#39; ou &#39;e&#39;)

- Requer um valor

### `--format`

O formato de saída: table, csv, tsv ou plain

- Padrão: `table`
- Requer um valor

### `--columns`, `-c`

Colunas a serem exibidas. Os caracteres % ou * podem ser usados como curinga. Os valores podem ser divididos por vírgulas (por exemplo, &quot;a,b,c&quot;) e/ou espaços em branco.

- Padrão: `[]`
- Requer um valor

### `--no-header`

Não gerar saída do cabeçalho da tabela

- Padrão: `false`
- Não aceita um valor

### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--environment`, `-e`

A ID do ambiente. Use &quot;.&quot; para selecionar o ambiente padrão do projeto.

- Requer um valor

### `--pipe`

[Opção obsoleta] Gerar somente o valor da variável

- Padrão: `false`
- Não aceita um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `variable:list`

Variáveis da lista

```bash
magento-cloud variables [-l|--level LEVEL] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT] [-e|--environment ENVIRONMENT]
```

### `--level`, `-l`

O nível da variável (&#39;project&#39;, &#39;environment&#39;, &#39;p&#39; ou &#39;e&#39;)

- Requer um valor

### `--format`

O formato de saída: table, csv, tsv ou plain

- Padrão: `table`
- Requer um valor

### `--columns`, `-c`

Colunas a serem exibidas. Colunas disponíveis: is_enabled, level, name, value. Os caracteres % ou * podem ser usados como curinga. Os valores podem ser divididos por vírgulas (por exemplo, &quot;a,b,c&quot;) e/ou espaços em branco.

- Padrão: `[]`
- Requer um valor

### `--no-header`

Não gerar saída do cabeçalho da tabela

- Padrão: `false`
- Não aceita um valor

### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--environment`, `-e`

A ID do ambiente. Use &quot;.&quot; para selecionar o ambiente padrão do projeto.

- Requer um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `variable:update`

Atualizar uma variável

```bash
magento-cloud variable:update [--allow-no-change] [-l|--level LEVEL] [--value VALUE] [--json JSON] [--sensitive SENSITIVE] [--enabled ENABLED] [--inheritable INHERITABLE] [--visible-build VISIBLE-BUILD] [--visible-runtime VISIBLE-RUNTIME] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] <name>
```


### `name`

O nome da variável

- Obrigatório

### `--allow-no-change`

Retorno com êxito (código de saída zero) se nenhuma alteração for fornecida

- Padrão: `false`
- Não aceita um valor

### `--level`, `-l`

O nível da variável (&#39;project&#39;, &#39;environment&#39;, &#39;p&#39; ou &#39;e&#39;)

- Requer um valor

### `--value`

O valor da variável

- Requer um valor

### `--json`

Se o valor da variável é formatado em JSON

- Padrão: `false`
- Requer um valor

### `--sensitive`

Se o valor da variável é sensível

- Padrão: `false`
- Requer um valor

### `--enabled`

Se a variável deve ser ativada no ambiente

- Padrão: `true`
- Requer um valor

### `--inheritable`

Se a variável é herdável por ambientes secundários

- Padrão: `true`
- Requer um valor

### `--visible-build`

Se a variável deve estar visível no momento da criação

- Requer um valor

### `--visible-runtime`

Se a variável deve estar visível no tempo de execução

- Padrão: `true`
- Requer um valor

### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--environment`, `-e`

A ID do ambiente. Use &quot;.&quot; para selecionar o ambiente padrão do projeto.

- Requer um valor

### `--no-wait`, `-W`

Não aguarde a conclusão da operação

- Padrão: `false`
- Não aceita um valor

### `--wait`

Aguardar a conclusão da operação (padrão)

- Padrão: `false`
- Não aceita um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor


## `worker:list`

Obter uma lista de todos os trabalhadores implantados

```bash
magento-cloud workers [--refresh] [--pipe] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header]
```

### `--refresh`

Se o cache deve ser atualizado

- Padrão: `false`
- Não aceita um valor

### `--pipe`

Gerar uma lista somente de nomes de trabalhadores

- Padrão: `false`
- Não aceita um valor

### `--project`, `-p`

A ID ou URL do projeto

- Requer um valor

### `--environment`, `-e`

A ID do ambiente. Use &quot;.&quot; para selecionar o ambiente padrão do projeto.

- Requer um valor

### `--format`

O formato de saída: table, csv, tsv ou plain

- Padrão: `table`
- Requer um valor

### `--columns`, `-c`

Colunas a serem exibidas. Colunas disponíveis: comandos, nome, tipo. Os caracteres % ou * podem ser usados como curinga. Os valores podem ser divididos por vírgulas (por exemplo, &quot;a,b,c&quot;) e/ou espaços em branco.

- Padrão: `[]`
- Requer um valor

### `--no-header`

Não gerar saída do cabeçalho da tabela

- Padrão: `false`
- Não aceita um valor

### `--help`, `-h`

Exibir esta mensagem de ajuda

- Padrão: `false`
- Não aceita um valor

### `--verbose`, `-v|-vv|-vvv`

Aumentar a verbosidade das mensagens

- Padrão: `false`
- Não aceita um valor

### `--version`, `-V`

Exibir esta versão do aplicativo

- Padrão: `false`
- Não aceita um valor

### `--yes`, `-y`

Responda &quot;sim&quot; às perguntas de confirmação; aceite o valor padrão para outras perguntas; desative a interação

- Padrão: `false`
- Não aceita um valor

### `--no-interaction`

Não faça perguntas interativas; aceite valores padrão. Equivalente ao uso da variável de ambiente: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Padrão: `false`
- Não aceita um valor

