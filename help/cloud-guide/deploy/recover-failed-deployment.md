---
title: Recuperação de falha de componente
description: Saiba como fazer a recuperação se um componente não for implantado corretamente na infraestrutura em nuvem do Adobe Commerce.
feature: Cloud, Deploy
exl-id: 4855be0c-6883-4ab1-a364-316d10e97250
source-git-commit: b44d97f82ef09288807c648010202422c9ac04eb
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 0%

---

# Recuperação de falha de componente

Este tópico discute como recuperar se um componente não for implantado corretamente. Exemplos típicos incluem componentes que possuem dependências que não são atendidas pelo seu ambiente remoto, tais como versões incompatíveis do PHP.

Você pode se recuperar de uma implantação com falha de qualquer uma das seguintes maneiras:

- [Restaurar um backup](../storage/snapshots.md#restore-a-snapshot)
- Limpar projeto e código de alterações anteriores e reimplantar

## Limpeza, remoção e reimplantação

Para limpar da implantação anterior, identifique o componente que foi adicionado ou atualizado e remova-o. Primeiro, faça logon no ambiente remoto e limpe manualmente o conteúdo do `var` diretório. Remova o componente da `composer.json` e reimplantar o ambiente.

**Para limpar o `var` diretórios**:

1. Na estação de trabalho local, altere para o diretório do projeto.

1. Use o SSH para fazer logon no ambiente remoto.

   ```bash
   magento-cloud ssh
   ```

1. Limpe a `var` diretórios.

   ```shell
   rm -rf var/*
   ```

1. Faça logout.

**Para remover o componente**:

1. Na estação de trabalho local, altere para o diretório do projeto.

1. Limpe o cache.

   ```bash
   composer clear-cache
   ```

1. Remova o componente da `composer.json` arquivo.

   ```bash
   composer remove <component-name>:<version>
   ```

   Se a mensagem a seguir for exibida, você não precisará fazer mais nada:

   ```terminal
   Package "<name>:<version>" listed for update is not installed. Ignoring.
   ```

1. Aguarde enquanto as dependências são atualizadas.

1. Adicionar, confirmar e enviar alterações de código.

   ```bash
   git add -A
   ```

   ```bash
   git commit -m "<message>"
   ```

   ```bash
   git push origin <environment-ID>
   ```

{{redeploy-warning}}

Saiba mais sobre como restaurar um ambiente sem um backup no [Restaurar um ambiente](../development/restore-environment.md).

{{stuck-deployment-tip}}
