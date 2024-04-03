---
title: Atualizar projeto para usar ECE-Tools
description: Saiba como atualizar seu projeto Adobe Commerce na infraestrutura em nuvem para usar o pacote ECE-Tools e aproveitar as correções e os recursos mais recentes.
feature: Cloud, Install
exl-id: 820cca84-2817-4881-829f-ebb78400d8c7
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 0%

---

# Atualizar projeto para usar o pacote ECE-Tools

Adobe descontinuou o `magento/magento-cloud-configuration` e `magento/ece-patches` pacotes a favor do `ece-tools` que simplifica muitos processos na nuvem. Se você usar um projeto mais antigo do Adobe Commerce na infraestrutura em nuvem que não _não_ contém o `ece-tools` pacote, você deverá executar um procedimento único, manual _atualização_ para o seu projeto.

>[!WARNING]
>
>Se o seu projeto contiver a variável `ece-tools` pacote, você pode ignorar a atualização a seguir. Para verificar, recupere a variável [!DNL Commerce] versão usando o `php vendor/bin/ece-tools -V` no diretório raiz do projeto local.

Este processo de atualização de projeto requer que você atualize o `magento/magento-cloud-metapackage` restrição de versão no `composer.json` no diretório raiz. Essa restrição permite atualizações para o Adobe Commerce em metapackages de infraestrutura em nuvem, incluindo a remoção de pacotes obsoletos, sem atualizar a versão atual do Adobe Commerce.

{{upgrade-tip}}

## Remover pacotes obsoletos

Antes de executar uma atualização para usar o `ece-tools` pacote, verifique a `composer.lock` arquivo para os seguintes pacotes obsoletos:

- `magento/magento-cloud-configuration`
- `magento/ece-patches`

## Atualizar o metapackage

Cada versão do Adobe Commerce exige uma restrição diferente com base no seguinte:

```terminal
>=current_version <next_version
```

- Para `current_version`, especifique a versão do Adobe Commerce a ser instalada.
- Para `next_version`, especifique a próxima versão de patch após o valor especificado em `current_version`.

Se você deseja instalar o Adobe Commerce `2.3.5-p2`, definir `current_version` para `2.3.5` e a variável `next_version` para `2.3.6`. A restrição `">=2.3.5 <2.3.6"` instala o pacote mais recente disponível para a versão 2.3.5.

Você sempre pode encontrar a restrição do metapackage mais recente no [`magento-cloud` modelo](https://github.com/magento/magento-cloud/blob/master/composer.json).

O exemplo a seguir coloca uma restrição para o metapackage do Adobe Commerce na infraestrutura em nuvem para qualquer versão maior ou igual à versão atual 2.4.5 e inferior à próxima versão 2.4.6:

```json
"require": {
    "magento/magento-cloud-metapackage": ">=2.4.5 <2.4.6"
},
```

## Atualizar o projeto

Para atualizar seu projeto para usar o `ece-tools` pacote, você deve atualizar o metapackage e o `.magento.app.yaml` conecta as propriedades e executa uma atualização do Composer.

**Para atualizar o projeto para usar as ferramentas ece**:

1. Atualize o `magento/magento-cloud-metapackage` restrição de versão no `composer.json` arquivo.

   ```bash
   composer require "magento/magento-cloud-metapackage":">=2.4.5 <2.4.6" --no-update
   ```

1. Atualize o metapackage.

   ```bash
   composer update magento/magento-cloud-metapackage
   ```

1. Modifique os comandos de gancho no `magento.app.yaml` arquivo.

   ```yaml
   hooks:
       # We run build hooks before your application has been packaged.
       build: |
           set -e
           php ./vendor/bin/ece-tools run scenario/build/generate.xml
           php ./vendor/bin/ece-tools run scenario/build/transfer.xml
       # We run deploy hook after your application has been deployed and started.
       deploy: |
           php ./vendor/bin/ece-tools run scenario/deploy.xml
       # We run post deploy hook to clean and warm the cache. Available with ECE-Tools 2002.0.10.
       post_deploy: |
           php ./vendor/bin/ece-tools run scenario/post-deploy.xml
   ```

1. Verifique e remova o [pacotes obsoletos](#remove-deprecated-packages). Os pacotes obsoletos podem impedir uma atualização bem-sucedida.

   ```bash
   composer remove magento/magento-cloud-configuration
   ```

   ```bash
   composer remove magento/ece-patches
   ```

1. Pode ser necessário atualizar a `ece-tools` pacote.

   ```bash
   composer update magento/ece-tools
   ```

1. Adicione e confirme as alterações de código. Neste exemplo, os seguintes arquivos foram atualizados:

   ```terminal
   .magento.app.yaml
   composer.json
   composer.lock
   ```

1. Enviar as alterações de código para o servidor remoto e mesclar esta ramificação com o `integration` filial.

   ```bash
   git push origin <branch-name>
   ```
