---
title: Implantação sem tempo de inatividade
description: Saiba como reduzir o tempo de inatividade geral ao implantar o Adobe Commerce em projetos de infraestrutura em nuvem.
feature: Cloud, Deploy, SCD, Themes
exl-id: ff89d2e1-dfc8-4f6d-bd98-947559af13f0
source-git-commit: 225fba1acfd8b3ce4d7ce989c7851e7b0b218680
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 0%

---

# Implantação sem tempo de inatividade

O Adobe Commerce na infraestrutura em nuvem executa o aplicativo em [_manutenção_ modo](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/setup/application-modes.html#production-mode) durante a fase de implantação, que coloca o site offline até que a implantação seja concluída. O tempo em que o site de produção está no modo de manutenção depende do tamanho do site, do número de alterações aplicadas durante a implantação e da configuração para implantação de conteúdo estático. É possível configurar seu projeto para que ele seja implantado com um **zero** efeito do tempo de inatividade.

Durante o processo de implantação, todas as conexões ficam em fila por até 5 minutos, preservando quaisquer sessões ativas e ações pendentes, como adicionar ao carrinho ou fazer checkout. Após a implantação, a fila é liberada e as conexões continuam sem interrupção. Para usar este _bloqueio de conexão_ para o seu benefício e reduzir a implantação para _zero_ tempo de inatividade, você deve configurar seu projeto para usar a estratégia de implantação mais eficiente.

Use as seguintes etapas para reduzir a quantidade de tempo que seu armazenamento leva para implantar uma atualização na Produção:

1. [Atualize para o `ece-tools` pacote](../dev-tools/install-package.md) ou [atualizar o `ece-tools` version](../dev-tools/update-package.md)
Seu projeto de infraestrutura do Adobe Commerce na nuvem deve ter a versão mais recente `ece-tools` para que você tenha as ferramentas disponíveis para configurar uma implantação ideal. Se você tiver o mais recente `ece-tools`, continue para a próxima etapa.

   >[!NOTE]
   >
   >Embora seja uma prática recomendada usar os mais recentes `ece-tools` o método de implantação sem tempo de inatividade funciona com `ece-tools` [versão 2002.0.13](../release-notes/cloud-release-archive.md#v2002013) e depois.

1. [Configurar implantação de conteúdo estático](static-content.md)
Se a implantação de conteúdo estático falhar na fase de implantação, seu site ficará preso no modo de manutenção. Quando ocorre uma falha durante a fase de criação, o processo evita o tempo de inatividade porque nunca inicia a fase de implantação. [Geração de conteúdo estático durante a fase de criação com HTML minified](static-content.md#setting-the-scd-on-build)O, também conhecido como estado ideal, é a configuração ideal para implantações sem tempo de inatividade e _impede_ inatividade se ocorrer uma falha.

1. [Configurar o gancho pós-implantação](../application/hooks-property.md)
Você deve configurar o gancho pós-implantação para limpar e aquecer o cache. Por padrão, a limpeza do cache ocorre durante a fase de implantação, quando o site está inativo. Mover o cache limpo para a fase de pós-implantação significa que o cache permanece ativo até que a fase de implantação seja concluída e, em seguida, você pode limpar com segurança o cache.

   Personalize a lista de páginas usadas para pré-carregar o cache com o [Variável de ambiente WARM_UP_PAGES](../environment/variables-post-deploy.md#warmuppages).

1. [Reduzir arquivos de tema](../environment/variables-deploy.md#scdmatrix)
Você pode reduzir o número de arquivos de tema desnecessários configurando a variável de ambiente SCD\_MATRIX.

1. [Acelere a implantação de conteúdo estático](../environment/variables-deploy.md#scdthreads)
Você pode acelerar o processo de implantação atualizando a variável de ambiente SCD\_THREADS para aumentar o número de threads para implantação de conteúdo estático.

>[!NOTE]
>
>Você pode validar a configuração do seu projeto para uma implantação ideal [execução do assistente de estado ideal](smart-wizards.md#verifying-an-ideal-configuration).
