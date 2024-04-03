---
title: Dados de exemplo
description: Saiba como instalar dados de amostra com o Adobe Commerce na infraestrutura em nuvem.
exl-id: 517e549f-15ba-47b3-9236-a1c4d24c917d
source-git-commit: 8a0523f1714b6ea41887e99b5c31294cf5e5255e
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 0%

---

# Dados de exemplo

Se você precisar de alguns dados de exemplo ao desenvolver sua loja, poderá instalar dados de amostra. Esses dados simulam uma loja ativa do Adobe Commerce com clientes, produtos e outros dados. Esses dados de amostra funcionam melhor com uma nova instalação do Adobe Commerce no modelo de infraestrutura em nuvem.

Como prática recomendada, instale dados de amostra em ambientes de desenvolvimento e integração. Se você usar dados de amostra no armazenamento temporário ou na produção, será necessário [remover](#reset-or-uninstall-sample-data) as informações e os produtos antes da ativação.

## Instalar dados de amostra

Para instalar dados de amostra:

1. Na estação de trabalho local, altere para o diretório do projeto.

1. Na raiz, insira o seguinte comando para adicionar dados de amostra:

   ```bash
   ./bin/magento sampledata:deploy
   ```

1. Aguarde até que os componentes sejam atualizados.

1. Confirme e envie as alterações:

   ```bash
   git add -A && git commit -m "Install sample data"
   ```

   ```bash
   git push origin <branch-name>
   ```

1. Aguarde a implantação do projeto.

1. Verifique se a instalação foi bem-sucedida acessando a página inicial da loja no ambiente de integração. É possível localizar o link do URL para a loja por meio da [!DNL Cloud Console].

1. Tirar um instantâneo do seu ambiente:

   ```bash
   magento-cloud snapshot:create -e <environment-ID>
   ```

Você pode começar a testar seu desenvolvimento com dados em tempo real!

## Redefinir ou desinstalar dados de exemplo

Você pode redefinir ou remover dados de amostra seguindo o mesmo procedimento usado para instalar os dados de amostra:

- Excluir dados de exemplo: `./bin/magento sampledata:remove`
- Redefinir dados de exemplo: `./bin/magento sampledata:reset`
