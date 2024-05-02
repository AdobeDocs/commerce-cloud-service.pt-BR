---
title: Gerenciamento de backup
description: Saiba como criar e restaurar manualmente um backup para seu projeto do Adobe Commerce na infraestrutura em nuvem.
feature: Cloud, Paas, Snapshots, Storage
exl-id: 1cb00db7-2375-4761-9c07-1e20a74859e0
source-git-commit: 4c3f3f2775e8327476233520e52b589f7264786f
workflow-type: tm+mt
source-wordcount: '711'
ht-degree: 0%

---

# Gerenciamento de backup

Você pode executar um backup manual de ambientes iniciais ativos a qualquer momento usando o **[!UICONTROL Backup]** botão na caixa [!DNL Cloud Console] ou usando o `magento-cloud snapshot:create` comando.

Um backup ou _instantâneo_ é um backup completo dos dados do ambiente que inclui todos os dados persistentes dos serviços em execução (banco de dados MySQL) e quaisquer arquivos armazenados nos volumes montados (var, pub/media, app/etc). O instantâneo não _não_ incluir código, pois o código já está armazenado no repositório baseado em Git. Não é possível fazer download de uma cópia de um snapshot.

O recurso de backup/snapshot não **não** se aplicam aos ambientes Pro Staging e Production, que recebem backups regulares para fins de recuperação de desastres por padrão. Consulte [Pro Backup e recuperação de desastres](../architecture/pro-architecture.md#backup-and-disaster-recovery) para obter mais informações. Diferentemente dos backups automáticos em tempo real nos ambientes Pro Staging e Production, os backups são **não** automático. É necessário _seu_ responsabilidade de criar manualmente um backup ou configurar um trabalho cron para criar periodicamente um backup dos ambientes de integração Starter ou Pro.

## Criar um backup manual

Você pode criar um backup manual de qualquer ambiente Starter ativo e integração com o ambiente Pro pelo [!DNL Cloud Console] ou crie um instantâneo da CLI da nuvem. Você deve ter um [Função de administrador](../project/user-access.md) para o ambiente.

**Para criar um backup de qualquer ambiente inicial usando o[!DNL Cloud Console]**:

1. Faça logon no [[!DNL Cloud Console]](https://console.adobecommerce.com).
1. Selecione um ambiente na barra de navegação do projeto. O ambiente deve estar ativo.
1. No _Backups_ clique em **[!UICONTROL Backup]**. Essa opção não está disponível para um ambiente Pro.

   ![Backup](../../assets/button-backup.png){width="150"}

**Para criar um backup de um ambiente de integração usando o[!DNL Cloud Console]**:

1. Faça logon no [[!DNL Cloud Console]](https://console.adobecommerce.com).
1. Selecione um ambiente de integração/desenvolvimento na barra de navegação do projeto. O ambiente deve estar ativo.
1. Selecione o **[!UICONTROL Backup]** no menu superior direito. Essa opção está disponível para ambientes Starter e Pro.
1. Clique em **[!UICONTROL Yes]** botão.

**Para criar um snapshot usando o `magento-cloud` CLI**:

1. Na estação de trabalho local, altere para o diretório do projeto.
1. Faça check-out da ramificação de ambiente para obter um instantâneo.
1. Crie o instantâneo.

   ```bash
   magento-cloud snapshot:create --live
   ```

   Como alternativa, você pode usar o `magento-cloud backup` comando short. A variável `--live` deixa o ambiente em execução para evitar tempo de inatividade. Para obter uma lista completa de opções, insira `magento-cloud snapshot:create --help`.

   Exemplo de resposta:

   ```terminal
   Creating a snapshot of develop-branch
   Waiting for the activity ID (User created a backup of develop-branch):
   
   Creating backup of develop-branch
   Created backup my-snapshot
   [============================] 45 secs (complete)
   Activity ID succeeded
   Snapshot name: my-snapshot
   ```

1. Verifique os snapshots mais recentes.

   ```bash
   magento-cloud snapshot:list
   ```

   A lista retorna informações sobre o status do snapshot:

   ```terminal
   Snapshots on the project (project-id), environment develop-branch (type: development):
   +---------------------------+----------------------+------------+
   | Created                   | Snapshot ID          | Restorable |
   +---------------------------+----------------------+------------+
   | 2023-03-08T17:07:01+00:00 | my-snapshot          | true       |
   +---------------------------+----------------------+------------+
   ```

## Restaurar um backup manual

Você deve ter [Acesso de administrador](../project/user-access.md) para o ambiente. Você tem até **sete dias** para _restaurar_ um backup manual. A restauração de um backup não altera o código da ramificação Git atual. Restaurar um backup dessa maneira não se aplica a ambientes de preparo e produção profissionais; consulte [Pro Backup e recuperação de desastres](../architecture/pro-architecture.md#backup-and-disaster-recovery).

Os tempos de restauração variam dependendo do tamanho do banco de dados:

- um banco de dados grande (mais de 200 GB) pode levar 5 horas
- banco de dados médio (150 GB) pode levar 2 horas e meia
- banco de dados pequeno (60 GB) pode levar 1 hora

>[!TIP]
>
>Restauração sem backup:
>
>- Para reverter para o código anterior ou remover extensões adicionadas em um ambiente, consulte [Reverter código](#roll-back-code).
>- Para restaurar um ambiente instável que não _não_ tiver um backup, consulte [Restaurar um ambiente](../development/restore-environment.md).

**Para restaurar um backup usando o[!DNL Cloud Console]**:

1. Faça logon no [[!DNL Cloud Console]](https://console.adobecommerce.com).
1. Selecione um ambiente na barra de navegação do projeto.
1. No _Backups_ exibir, escolha um backup na _Armazenado_ lista. O recurso de backup não **não** se aplicam aos ambientes Pro.
1. No ![Mais](../../assets/icon-more.png){width="32"} (_mais_), clique em **Restaurar**.
1. Revise as informações de restauração de backup e clique em **Sim, restaurar**.

**Para restaurar um instantâneo usando a CLI da nuvem**:

1. Na estação de trabalho local, altere para o diretório do projeto.
1. Confira a ramificação do ambiente a ser restaurada.
1. Lista todos os snapshots disponíveis.

   ```bash
   magento-cloud snapshot:list
   ```

   A lista retorna informações sobre os snapshots disponíveis:

   ```terminal
   Snapshots on the project (project-id), environment develop-branch (type: development):
   +---------------------------+----------------------+------------+
   | Created                   | Snapshot ID          | Restorable |
   +---------------------------+----------------------+------------+
   | 2023-03-08T17:07:01+00:00 | my-snapshot          | true       |
   +---------------------------+----------------------+------------+
   ```

1. Restaure um instantâneo usando a ID de instantâneo da lista.

   ```bash
   magento-cloud snapshot:restore <snapshot-id>
   ```

## Restaurar um Instantâneo da Recuperação de Desastres

Para restaurar o instantâneo da recuperação de desastres em ambientes de preparo e produção profissionais, [Importar o dump do banco de dados diretamente do servidor](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/how-to/restore-a-db-snapshot-from-staging-or-production#meth3).

## Reverter código

Backups e snapshots fazem _não_ inclua uma cópia do código. Seu código já está armazenado no repositório baseado em Git, portanto, você pode usar comandos baseados em Git para reverter (ou reverter) o código. Por exemplo, use `git log --oneline` para percorrer as confirmações anteriores; em seguida, use [`git revert`](https://git-scm.com/docs/git-revert) para restaurar o código de uma confirmação específica.

Além disso, é possível optar por armazenar o código em um _inativo_ filial. Use comandos do Git para criar uma ramificação em vez de usar `magento-cloud` comandos. Consulte sobre [Comandos do Git](../dev-tools/cloud-cli-overview.md#git-commands) no tópico da CLI da nuvem.
