---
title: Processo de implantação
description: Saiba como a implantação funciona para o Adobe Commerce em projetos de infraestrutura em nuvem.
feature: Cloud, Build, Deploy, SCD
exl-id: 378fa290-5a71-4ac2-816a-a7c837e45b2f
source-git-commit: 3d9e3294872fedcc43744f54a71c71d8951ed853
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 0%

---

# Processo de implantação

O processo de implantação começa quando você faz uma mesclagem, uma notificação por push ou uma sincronização do seu ambiente, ou quando aciona um [reimplantação manual](../dev-tools/cloud-cli-overview.md#redeploy-the-environment). O processo de implantação leva tempo, mas há maneiras de otimizar a implantação que dependem se você está desenvolvendo e testando ou trabalhando com um site ativo. Principalmente, você pode controlar o [implantação de conteúdo estático](static-content.md).

Há três fases distintas do processo de implantação: criação, implantação e pós-implantação. Cada fase executa ações específicas com recursos limitados:

## ![Fase de criação](../../assets/status-build.png) Fase de criação

A variável _build_ A fase monta contêineres para os serviços definidos nos arquivos de configuração e instala dependências com base no `composer.lock` e executa os ganchos de criação definidos na variável `.magento.app.yaml` arquivo. Sem a capacidade de se conectar a qualquer serviço ou acessar o banco de dados, a fase de criação depende dos recursos limitados ao ambiente.

## ![Fase de implantação](../../assets/status-deploy.png) Fase de implantação

A variável _implantar_ coloca uma suspensão temporária em solicitações recebidas e faz a transição do site para [modo de manutenção](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/setup/application-modes.html). A fase de implantação usa os novos contêineres e, após montar o sistema de arquivos, abre conexões de rede, ativa os serviços definidos na variável `relationships` seção do `.magento.app.yaml` e executa os ganchos de implantação definidos na variável `.magento.app.yaml` arquivo. Tudo é _somente leitura_, exceto para diretórios definidos no `.magento.app.yaml` arquivo. Por padrão, a variável [`mounts` propriedade](../application/properties.md#mounts) inclui os seguintes diretórios:

- `app/etc`—contém o `env.php` e `config.php` arquivos de configuração
- `pub/media`—contém todos os dados de mídia, como produtos ou categorias
- `pub/static`—contém arquivos estáticos gerados
- `var`—contém arquivos temporários criados durante o tempo de execução

Todos os outros diretórios têm permissões somente leitura. O novo site se torna ativo no final da fase de implantação, à medida que sai do modo de manutenção e libera a suspensão temporária em solicitações recebidas.

Na fase de implantação, cópias do `app/etc/config.php` e `app/etc/env.php` os arquivos de configuração de implantação são salvos com a extensão BAK. Consulte [Configurações da loja](../store/store-settings.md#restore-configuration-files) para saber como restaurar esses arquivos.

## ![Fase de pós-implantação](../../assets/status-post-deploy.png) Fase de pós-implantação

A variável _pós-implantação_ A fase executa os ganchos de pós-implantação definidos na `.magento.app.yaml` arquivo. A execução de qualquer ação nesta fase pode afetar o desempenho do site; no entanto, você pode usar o [PÁGINAS_AQUECIDAS](../environment/variables-post-deploy.md#warmuppages) para preencher o cache.

## ![Verificar estado](../../assets/status-verify.png) Verificar configurações

Você pode testar a configuração ideal para o estado do seu projeto executando o [Assistentes inteligentes](smart-wizards.md).

>[!NOTE]
>
>Com `ece-tools` 2002.1.0 e versões posteriores, você pode usar o recurso de implantação baseada em cenário para personalizar os processos de criação, implantação e pós-implantação do seu projeto Adobe Commerce na infraestrutura em nuvem. Consulte [Implantação baseada em cenário](scenario-based.md).
