---
title: Chaves de autenticação
description: Saiba como aplicar chaves de autenticação a um projeto de desenvolvimento no Adobe Commerce na infraestrutura em nuvem.
feature: Cloud, Security
topic: Security
exl-id: b05cd4c2-0804-49c8-980a-4c7b6932082b
source-git-commit: 13e76d3e9829155995acbb72d947be3041579298
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 0%

---

# Chaves de autenticação

Você deve ter uma chave de autenticação para acessar o repositório do Adobe Commerce e habilitar os comandos instalar e atualizar para o projeto do Adobe Commerce na infraestrutura em nuvem. Há dois métodos para especificar credenciais de autorização do Composer.

- **arquivo de autenticação**—Um arquivo que contém seu Adobe Commerce [credenciais de autorização](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/prerequisites/authentication-keys.html) no diretório raiz da infraestrutura do Adobe Commerce na nuvem.
- **variável de ambiente**— Uma variável de ambiente para configurar chaves de autenticação em seu projeto do Adobe Commerce na infraestrutura em nuvem para evitar exposição acidental.

>[!BEGINSHADEBOX]

**Nota de segurança**

O Adobe recomenda o uso de [variável de ambiente](#composer-auth-environment-variable) com seu projeto na nuvem para evitar a exposição acidental de suas credenciais de autorização.

O método do arquivo de autenticação é ideal ao usar o Cloud Docker for Commerce como uma ferramenta de desenvolvimento local, mas tenha cuidado para não carregar o `auth.json` para um repositório público baseado em Git. Você pode adicionar o `auth.json` arquivo para o [`.gitignore` arquivo](../project/file-structure.md#ignoring-files).

>[!ENDSHADEBOX]

## Arquivo de autenticação

**Para criar uma `auth.json` arquivo**:

1. Se você não tiver um `auth.json` no diretório raiz do projeto, crie um.

   - Usando um editor de texto, crie um `auth.json` arquivo no diretório raiz do projeto.
   - Copie o conteúdo de [amostra `auth.json`](https://github.com/magento/magento2/blob/2.3/auth.json.sample) no novo `auth.json` arquivo.

1. Substituir `<public-key>` e `<private-key>` com suas credenciais de autenticação da Adobe Commerce.

   ```json
   {
       "http-basic": {
           "repo.magento.com": {
               "username": "<public-key>",
               "password": "<private-key>"
           }
       }
   }
   ```

1. Salve as alterações e saia do editor de texto.

## Variável de ambiente de autenticação do Composer

O método a seguir é a melhor maneira de evitar a exposição acidental de credenciais confidenciais em um repositório público baseado em Git.

**Para adicionar chaves de autenticação usando uma variável de ambiente**:

1. No _[!DNL Cloud Console]_, clique no ícone de configuração no lado direito da navegação do projeto.

   ![Configurar projeto](../../assets/icon-configure.png){width="36"}

1. No _Configurações do projeto_ clique em **[!UICONTROL Variables]**.

1. Clique em **[!UICONTROL Create variable]**.

1. No **[!UICONTROL Variable name]** insira `env:COMPOSER_AUTH`.

1. No _Valor_ , adicione o seguinte e substitua `<public-key>` e `<private-key>` com suas credenciais de autenticação da Adobe Commerce:

   ```json
   {
       "http-basic": {
           "repo.magento.com": {
               "username": "<public-key>",
               "password": "<private-key>"
           }
       }
   }
   ```

1. Selecionar **[!UICONTROL Available during buildtime]** e desmarque **[!UICONTROL Available during runtime]**.

1. Clique em **[!UICONTROL Create variable]**.

1. Remova o `auth.json` de cada ambiente.
