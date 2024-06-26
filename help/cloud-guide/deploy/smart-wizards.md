---
title: Assistentes inteligentes
description: Saiba como usar assistentes inteligentes para avaliar se o projeto do Adobe Commerce na infraestrutura em nuvem está seguindo as práticas recomendadas de implantação.
feature: Cloud, Build, Deploy, SCD
exl-id: eb79431c-8835-4ae4-b453-9c4932c5d5ac
source-git-commit: 225fba1acfd8b3ce4d7ce989c7851e7b0b218680
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 0%

---

# Assistentes inteligentes

Os assistentes inteligentes podem ajudar você a determinar se a configuração da nuvem segue as práticas recomendadas. Os assistentes disponíveis ajudam nas seguintes configurações:

- Estado ideal para tempo mínimo de inatividade de implantação
- Configuração de balanceamento de carga para banco de dados e Redis
- Implantação de conteúdo estático (SCD) para o estágio sob demanda, de criação ou de implantação

Cada um dos comandos do assistente inteligente fornece uma resposta de verificação e, se aplicável, uma recomendação para a configuração adequada.

| Comando | Descrição |
| ------- | ------------|
| `wizard:ideal-state` | Verifique se o SCD está no estado _build_ estágio, a variável `SKIP_HTML_MINIFICATION` é `true`e o gancho post_deploy configurado no ambiente de nuvem. Não utilizar no ambiente de desenvolvimento local. |
| `wizard:master-slave` | Verifique se `REDIS_USE_SLAVE_CONNECTION` e a variável `MYSQL_USE_SLAVE_CONNECTION` é `true`. |
| `wizard:scd-on-demand` | Verifique se `SCD_ON_DEMAND` a variável de ambiente global é `true`. |
| `wizard:scd-on-build` | Verifique se `SCD_ON_DEMAND` a variável de ambiente global é `false` e a variável `SKIP_SCD` a variável de ambiente é `false` para o _build_ estágio. Verifica se `config.php` o arquivo contém informações de lojas, grupos de lojas e sites. |
| `wizard:scd-on-deploy` | Verifique se `SCD_ON_DEMAND` a variável de ambiente global é `false` e a variável `SKIP_SCD` a variável de ambiente é `false` para o _implantar_ estágio. Verifica se `config.php` o arquivo faz _NOT_ contém a lista de lojas, grupos de lojas e sites com informações relacionadas. |

Como exemplo, você pode verificar se a sua configuração ativa corretamente o recurso SCD sob demanda:

```bash
./vendor/bin/ece-tools wizard:scd-on-demand
```

Uma configuração bem-sucedida retorna:

```terminal
SCD on-demand is enabled
```

Uma configuração com falha retorna:

```terminal
SCD on-demand is disabled
```

## Verificar uma configuração ideal

A variável _ideal_ A configuração do seu projeto na nuvem ajuda a minimizar o tempo de inatividade da implantação, aquecendo o cache e gerando conteúdo estático quando solicitado pelo usuário. Este assistente é executado automaticamente durante o processo de implantação. Se a nuvem não estiver configurada para esse _estado ideal_, você receberá uma mensagem semelhante à seguinte:

```terminal
- SCD on build is not configured
- Post-deploy hook is not configured
- Skip HTML minification is disabled

Ideal state is not configured
```

Com base na saída, você precisa fazer as seguintes correções na sua configuração:

1. Ative a variável Skip HTML minification.

   > .magento.env.yaml

   ```yaml
   stage:
     global:
       SKIP_HTML_MINIFICATION: true
   ```

1. Configure o gancho pós-implantação.

   > .magento.app.yaml

   ```yaml
       post_deploy: |
           php ./vendor/bin/ece-tools post-deploy
   ```

1. Envie alterações de código e execute o teste novamente. Quando sua configuração é _ideal_, você receberá a seguinte mensagem.

   ```terminal
   Ideal state is configured
   ```
