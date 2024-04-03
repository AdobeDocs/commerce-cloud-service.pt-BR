---
title: Restaurar um ambiente
description: Saiba como desinstalar o aplicativo do Adobe Commerce de um projeto de infraestrutura em nuvem e restaurar um ambiente para um estado estável.
role: Developer
topic: Development
exl-id: b76bd6c3-986e-4adc-abd0-5b27db0d8a3b
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 0%

---

# Restaurar um ambiente

Se encontrar problemas no ambiente de integração e não tiver um [backup válido](../storage/snapshots.md), tente restaurar o ambiente usando um dos seguintes métodos:

- Redefinir ou reverter o código na ramificação Git
- Desinstale o [!DNL Commerce] aplicativo
- Forçar uma reimplantação
- Redefinir manualmente o banco de dados

{{stuck-deployment-tip}}

## Redefinir a ramificação Git

Redefinir a ramificação Git reverte o código para um estado estável no passado.

**Para redefinir a ramificação**:

1. Na estação de trabalho local, altere para o diretório do projeto.

1. Revise o histórico de Git commit. Uso `--oneline` para mostrar confirmações abreviadas em uma linha:

   ```bash
   git log --oneline
   ```

   Exemplo de resposta:

   ```terminal
   6bf9f45 (HEAD -> master, magento/master, magento/develop, magento/HEAD, develop) Create composer.lock
   34d7434 2.4.6 upgrade
   b69803c Update composer.lock
   c1bca24 Add sample data
   ec604c3 Update magento/ece-tools
   ...
   ```

1. Escolha um hash de confirmação que represente o último estado estável conhecido do código.

   Para redefinir a ramificação para seu estado inicializado original, localize a primeira confirmação que criou a ramificação. Você pode usar `--reverse` para exibir o histórico em ordem cronológica inversa.

1. Use a opção de reinicialização forçada para redefinir sua ramificação. Tenha cuidado ao usar esse comando, pois ele descarta todas as alterações desde a confirmação escolhida.

   ```bash
   git reset --hard <commit>
   ```

1. Envie suas alterações para acionar uma reimplantação, que reinstala o Adobe Commerce.

   ```bash
   git push --force <origin> <branch>
   ```

## Desinstalar o Commerce

Desinstalando o [!DNL Commerce] O aplicativo retorna o ambiente ao estado original restaurando o banco de dados, removendo a configuração de implantação e limpando o `var/` subdiretórios. Esta orientação também redefine a ramificação Git para um estado estável anterior. Se você não tiver um backup recente, mas puder acessar o ambiente remoto usando SSH, siga estas etapas para restaurar seu ambiente:

- Desabilitar gerenciamento de configuração
- Desinstalar o Adobe Commerce
- Redefinir a ramificação Git

A desinstalação do software Adobe Commerce remove e restaura o banco de dados, remove a configuração de implantação e limpa a `var/` subdiretórios. É importante desativar o [Gerenciamento de configuração](../store/store-settings.md) para que ele não aplique automaticamente as definições de configuração anteriores durante a próxima implantação. Verifique se o seu `app/etc/` o diretório não contém o `config.php` arquivo.

**Para desinstalar o software Adobe Commerce**:

1. Na estação de trabalho local, altere para o diretório do projeto.

1. Use o SSH para fazer logon no ambiente remoto.

   ```bash
   magento-cloud ssh
   ```

1. Remova o arquivo de configuração.
   - Para o Adobe Commerce 2.2 e posterior:

     ```bash
     rm app/etc/config.php
     ```

   - Para o Adobe Commerce 2.1:

     ```bash
     rm app/etc/config.local.php
     ```

1. Desinstale o aplicativo do Adobe Commerce.

   ```bash
   php bin/magento setup:uninstall -n
   ```

1. Confirme se o Adobe Commerce foi desinstalado com êxito.

   A seguinte mensagem é exibida para confirmar uma desinstalação bem-sucedida:

   ```terminal
   [SUCCESS]: Magento uninstallation complete.
   ```

1. Limpe a `var/` subdiretórios.

   ```bash
   rm -rf var/*
   ```

1. Faça logout.

>[!TIP]
>
>Como opção, é uma boa prática limpar os caches de criação.
>
>```bash
>magento-cloud project:clear-build-cache
>```

## Forçar uma reimplantação

Se você tentou desinstalar o Adobe Commerce e a implantação continua a falhar, tente forçar uma reimplantação manualmente.

```bash
git commit --allow-empty -m "<message>" && git push <origin> <branch>
```

## Redefinir o banco de dados

Se você tentou desinstalar o Adobe Commerce e o comando falhou ou não pôde ser concluído, é possível redefinir manualmente o banco de dados.

**Para redefinir o banco de dados**:

1. Na estação de trabalho local, altere para o diretório do projeto.

1. Use o SSH para fazer logon no ambiente remoto.

   ```bash
   magento-cloud ssh
   ```

1. Conectar ao banco de dados.

   ```bash
   mysql -h database.internal
   ```

1. Solte o `main` banco de dados.

   ```shell
   drop database main;
   ```

1. Criar um vazio `main` banco de dados.

   ```shell
   create database main;
   ```

1. Exclua os arquivos de configuração a seguir.

   - `config.php`
   - `config.php.bak`
   - `env.php`
   - `env.php.bak`

1. Faça logout e acione uma reimplantação.

   ```bash
   magento-cloud environment:redeploy
   ```

{{redeploy-warning}}
