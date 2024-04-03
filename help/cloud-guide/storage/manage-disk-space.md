---
title: Gerenciar espaço em disco
description: Saiba como gerenciar o espaço em disco usando a interface de linha de comando.
feature: Cloud, Storage
exl-id: 480cb33b-ac83-441d-946e-5b4de09ad84e
source-git-commit: 1253d8357fd2554050d1775fefbc420a2097db5f
workflow-type: tm+mt
source-wordcount: '693'
ht-degree: 0%

---

# Gerenciar espaço em disco

Você pode encontrar a capacidade total de armazenamento para seu projeto na nuvem no contrato de infraestrutura do Adobe Commerce on Cloud e em seu [página da conta](https://accounts.magento.cloud/user). Cada cartão de projeto na sua conta mostra o número de _ambientes_, o _armazenamento_ capacidade em GB, e o número de _usuários_. Como alternativa, você pode usar o seguinte comando na nuvem:

```bash
magento-cloud subscription:info | grep storage
```

Exemplo de resposta:

```terminal
| storage              | 51200
```

Quando um ambiente de produção ou de preparo Pro atinge ou excede 95% da capacidade de armazenamento, a ferramenta de monitoramento da infraestrutura em nuvem aciona um alerta de suporte notificando você sobre um aumento automático na capacidade de armazenamento.

Exemplo de notificação:

>[!BEGINSHADEBOX]

_&quot;Nosso monitoramento detectou que o armazenamento de arquivos em seu cluster (project-id-environment) está quase cheio. O uso do disco está atualmente em níveis críticos de uso com menos de 1 GiB restante. No momento, o volume de armazenamento compartilhado está sendo submetido a upsizing de 60 GiB para 70 GiB para que seus serviços continuem funcionando. Consulte o uso de arquivos de produção e de preparo para ver se você pode liberar espaço.&quot;_

>[!ENDSHADEBOX]

>[!TIP]
>
>É recomendável monitorar regularmente a capacidade de armazenamento e mantê-la bem abaixo de 90% para evitar esses aumentos automáticos. Depois de alocado, o aumento de armazenamento para preparo e produção Pro não pode ser revertido.

## Verificar ambiente de integração

Você pode verificar o uso do espaço em disco para o ambiente de integração usando o `magento-cloud` CLI.

**Para verificar o uso aproximado do espaço em disco**:

```bash
magento-cloud db:size
```

Exemplo de resposta:

```terminal
Checking database service mysql...

+----------------+-----------------+--------+
| Allocated disk | Estimated usage | % used |
+----------------+-----------------+--------+
| 2.0 GiB        | 193.3 MiB       | ~ 9%   |
+----------------+-----------------+--------+
```

Todas as montagens compartilham um disco. Você pode verificar o uso do espaço em disco para montagens usando o `magento-cloud` CLI.

**Para verificar o uso aproximado do espaço em disco para montagens**:

```bash
magento-cloud mount:size
```

Exemplo de resposta:

```terminal
Checking disk usage for all mounts on <project>-<environment>-mymagento@ssh.us.magento.cloud...

+------------+-----------+---------+-----------+-----------+--------+
| Mount(s)   | Size(s)   | Disk    | Used      | Available | % Used |
+------------+-----------+---------+-----------+-----------+--------+
| app/etc    | 184 KiB   | 1.9 GiB | 481.3 MiB | 1.4 GiB   | 24.7%  |
| pub/media  | 128 KiB   |         |           |           |        |
| pub/static | 158.2 MiB |         |           |           |        |
| var        | 316.7 MiB |         |           |           |        |
+------------+-----------+---------+-----------+-----------+--------+
```

## Verificar clusters dedicados

Para ambientes Pro de armazenamento temporário e produção, você pode verificar o uso do espaço em disco em cada ambiente usando o `disk free` que informa a quantidade de espaço em disco usada pelo sistema de arquivos. Você deve usar o SSH para fazer logon em um ambiente remoto.

```bash
df -h
```

A variável `-h` exibe o relatório em um formato legível (KB, MB ou GB).

Na resposta de amostra a seguir, a variável `/mnt/shared` mount mostra o espaço em disco para mídia e `/data/mysql/` mount mostra o espaço em disco para o banco de dados:

```terminal
Filesystem                                    Size  Used Avail Use% Mounted on
udev                                           16G     0   16G   0% /dev
tmpfs                                         3.2G  9.1M  3.2G   1% /run
/dev/xvda1                                     59G  8.9G   48G  16% /
tmpfs                                          16G   36K   16G   1% /dev/shm
tmpfs                                         5.0M     0  5.0M   0% /run/lock
tmpfs                                          16G     0   16G   0% /sys/fs/cgroup
/dev/xvdj                                     9.8G  2.3G  7.6G  23% /data/mysql
/dev/xvdi                                     9.8G  491M  9.3G   5% /data/exports
192.168.5.5:/shared                           9.8G  591M  9.3G   6% /mnt/shared
/dev/loop0                                     91M   91M     0 100% /app/project
192.168.5.5:/shared/project/var         9.8G  591M  9.3G   6% /app/project/var
192.168.5.5:/shared/project/app/etc     9.8G  591M  9.3G   6% /app/project/app/etc
192.168.5.5:/shared/project/pub/media   9.8G  591M  9.3G   6% /app/project/pub/media
192.168.5.5:/shared/project/pub/static  9.8G  591M  9.3G   6% /app/project/pub/static
```

É possível limitar a resposta especificando um diretório. Por exemplo:

```bash
df -h var/
```

Exemplo de resposta:

```terminal
Filesystem                                    Size  Used Avail Use% Mounted on
192.168.5.5:/shared/project/var         9.8G  591M  9.3G   6% /app/project/var
```

## Alocar espaço em disco

Dois [arquivos de configuração](../environment/overview.md) controlar a alocação de espaço em disco nos ambientes na nuvem: a variável `.magento.app.yaml` e o `.magento/services.yaml` arquivo. Cada arquivo contém o `disk` que define o valor do tamanho do disco em MB para a respectiva configuração. Você só pode alterar a alocação de espaço em disco nos ambientes Pro integration e Starter.

>[!IMPORTANT]
>
>Para ambientes de produção e preparo profissionais, você deve [Enviar um tíquete de suporte da Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) para alterar a alocação de espaço em disco. Um aumento de tamanho dos ambientes de produção Pro e de preparo só pode ocorrer em determinados intervalos. Portanto, dependendo do uso atual do espaço em disco, o suporte pode recomendar o aumento da alocação de espaço em disco em um mínimo de 10 GB. Depois de alocado, o aumento de armazenamento para preparo e produção Pro não pode ser revertido.

### Espaço em disco do aplicativo

A variável `.magento.app.yaml` arquivo controla o [espaço em disco persistente](../application/properties.md#disk) disponíveis para o aplicativo.

**Para aumentar o espaço em disco do aplicativo**:

1. No ambiente de desenvolvimento local, abra o `.magento.app.yaml` arquivo de configuração.

1. Defina um novo valor para a variável `disk` propriedade (em MB).

   ```yaml
   disk: <value-mb>
   ```

1. Salvar alterações no arquivo.

1. Adicionar, confirmar e enviar por push as alterações de código.

   ```bash
   git add .magento.app.yaml && git commit -m "Increase disk space for application" && git push origin <branch-name>
   ```

   As alterações entrarão em vigor depois que você enviar o arquivo YAML atualizado para o ambiente remoto.

### Espaço em disco do serviço

A variável `.magento/services.yaml` file controla o espaço em disco disponível para cada serviço, como MySQL e Redis.

**Para aumentar o espaço em disco de um serviço**:

1. No ambiente de desenvolvimento local, abra o `.magento/services.yaml` arquivo de configuração.

1. Adicionar ou localizar um serviço no arquivo. Consulte [mais informações sobre a configuração de serviços](../services/services-yaml.md).

1. Defina um novo valor para a propriedade do disco (em MB).

   ```yaml
   <name>:
       type: <service-name>:<service-version>
       disk: <value-mb>
   ```

1. Salvar alterações no arquivo.

1. Adicionar, confirmar e enviar por push as alterações de código.

   ```bash
   git add .magento/services.yaml && git commit -m "Increase disk space for service" && git push origin <branch-name>
   ```

   As alterações entrarão em vigor depois que você enviar o arquivo YAML atualizado para o ambiente remoto.

## Monitorar espaço em disco

Em ambientes de produção Pro, é possível monitorar o espaço em disco e outros indicadores de desempenho usando a política de alerta Gerenciado para Adobe Commerce para New Relic. Para obter detalhes, consulte [Monitorar o desempenho com alertas gerenciados](../monitor/investigate-performance.md#monitor-performance-with-managed-alerts). Para obter mais orientações, consulte [Práticas recomendadas para resolver problemas de desempenho do banco de dados](https://experienceleague.adobe.com/docs/commerce-operations/implementation-playbook/best-practices/maintenance/resolve-database-performance-issues.html).

## Não há mais espaço

O cache de build pode crescer com o tempo. Se você receber um aviso que indica `No space left on device`, tente limpar o cache de criação e reimplantar:

```bash
magento-cloud project:clear-build-cache
```
