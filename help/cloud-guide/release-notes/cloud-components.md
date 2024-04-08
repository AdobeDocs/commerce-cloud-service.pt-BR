---
title: Componentes da nuvem para o Commerce
description: Consulte uma lista das melhorias mais recentes no pacote de componentes da nuvem.
recommendations: noDisplay, catalog
exl-id: b4e2508a-3558-4fa8-bae0-3eb76c7b2775
source-git-commit: c02dfd2709cdc63ac1630edaa8c89cad5f737ea1
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 0%

---

# Componentes da nuvem para o Commerce

A variável [Componentes da nuvem](https://github.com/magento/magento-cloud-components) O pacote de fornece funcionalidade principal estendida do Adobe Commerce para sites implantados na infraestrutura da nuvem. Este pacote é uma dependência do pacote ECE-Tools. Estas notas de versão descrevem os últimos aprimoramentos feitos neste pacote, que é um componente do [Cloud Tools Suite for Commerce](cloud-tools-suite.md).

A variável `magento/magento-cloud-components` O pacote usa a seguinte sequência de versão: `<major>.<minor>.<patch>`

As notas de versão incluem:

- ![novo ícone](../../assets/new.svg) Novos recursos
- ![ícone corrigir](../../assets/fix.svg) Correções e aprimoramentos

<!--Add release notes below-->

## v1.0.14 {#latest}

Data de lançamento: 8 de abril de 2024

- ![novo ícone](../../assets/new.svg) **PHP** — Adição de suporte para PHP 8.3.

## v1.0.13

Data de lançamento: 10 de março de 2023

- ![novo ícone](../../assets/new.svg) **Suporte avançado para PHP 8.2**—Correção de problemas de compatibilidade com determinadas versões do PHP 8.2.x para suportar o Commerce 2.4.6.

## v1.0.12

Data de lançamento: 13 de setembro de 2022

- ![ícone corrigir](../../assets/fix.svg) **Erros no aquecimento**—Correção de um problema que tentava [warmup](../environment/variables-post-deploy.md#warm_up_pages) quando a visibilidade da página é definida como [**Não visível individualmente**](https://docs.magento.com/user-guide/system/data-attributes-product.html#simple-product-csv-file-structure) no Administrador, resultando em `ERROR: Warming up failed: <link to page>` erros no log de implantação.<!-- MCLOUD-9134 -->

## v1.0.11

Data de lançamento: 4 de agosto de 2022

- ![ícone corrigir](../../assets/fix.svg) **Suporte adicionado para compatibilidade com o Symfony 5.4**—Correções para compatibilidade com o Symfony 5.4.<!-- AC-3550 -->

## v1.0.10

Data de lançamento: 10 de março de 2022

- ![novo ícone](../../assets/new.svg) **Suporte ao PHP 8.1**—Adição de suporte para PHP 8.1 e remoção do suporte para PHP 7.1.

## v1.0.9

Data de lançamento: 25 de outubro de 2021

- ![ícone corrigir](../../assets/fix.svg) **Atualizar monólogo**—Atualização da versão mínima necessária para o `monolog` empacotar para `^2.3`.<!-- ACMP-1263 -->

## v1.0.8

Data de lançamento: 29 de julho de 2021

- ![ícone corrigir](../../assets/fix.svg) **Barras à direita removidas de URLs gerados automaticamente**—Remoção das barras à direita dos URLs de páginas de categoria gerados durante o aquecimento do cache.<!--MCLOUD-7192-->

## v1.0.7

Data de lançamento: 9 de setembro de 2020

- ![novo ícone](../../assets/new.svg) **Melhorias no registro**—Reduza o tamanho do `cache.log` para melhorar o desempenho.<!--MCLOUD-6859-->

- ![ícone corrigir](../../assets/fix.svg) Correção de um erro de tipo nos valores de configuração do cache que causava a `php bin/magento cache:evict` Falha no comando da CLI.

## v1.0.6

Data de lançamento: 5 de agosto de 2020

- ![novo ícone](../../assets/new.svg) **Melhorar o desempenho do Redis**—Adição de `./bin/magento cache:evict` comando para remover chaves Redis expiradas, o que reduz o uso de memória Redis para melhorar o desempenho.<!--MCLOUD-6023-->

- ![ícone corrigir](../../assets/fix.svg) Remoção do suporte para *Contexto de logons do New Relic* para corrigir um problema de desempenho.<!--MCLOUD-6422-->

## v1.0.5

Data de lançamento: 25 de junho de 2020

- ![ícone corrigir](../../assets/fix.svg) Correção de um problema introduzido na versão 1.0.4 dos componentes da magento/magento-cloud que causava a falha da operação de liberação de cache durante a fase de implantação, interrompendo o processo de implantação.

## v1.0.4

Data de lançamento: 25 de junho de 2020

- ![novo ícone](../../assets/new.svg) **Logs New Relic implementados no contexto**— os registros de aplicativos gerados pelo Adobe Commerce agora são exibidos em rastreamentos no New Relic para melhorar os recursos de solução de problemas.<!--MCLOUD-6029-->

- ![novo ícone](../../assets/new.svg) **Melhoria no registro**—Adição de registro para rastrear a invalidação do cache e os eventos de reindexação completa.<!--MCLOUD-6157-->

## v1.0.3

Data de lançamento: 27 de fevereiro de 2020

- ![ícone corrigir](../../assets/fix.svg) Correção de um problema de compatibilidade com o suporte `ece-tools` Versões 2002.0.x que usam versões mais antigas do PHP.

## v1.0.2

Data de lançamento: 6 de fevereiro de 2020

- ![novo ícone](../../assets/new.svg) Ampliou a funcionalidade do `WARM_UP_PAGES` variável de ambiente para suportar o pré-carregamento de cache de páginas de produto específicas. Consulte a [variáveis pós-implantação](../environment/variables-post-deploy.md#warm_up_pages) para obter uma descrição detalhada do recurso.<!--MAGECLOUD-4444-->

- ![ícone corrigir](../../assets/fix.svg) Correção de um problema em que um URL de armazenamento inválido causa falha no gancho pós-implantação ao usar o `WARM_UP_PAGES` funcionalidade para preencher o cache. Esse problema ocorria somente quando as substituições de URL eram desativadas.<!-- MAGECLOUD-4094 -->

## v1.0.1

Data de lançamento: 23 de julho de 2019

- ![ícone corrigir](../../assets/fix.svg) Correção de um problema que afetava [**PÁGINAS_AQUECIDAS**](../environment/variables-post-deploy.md#warm_up_pages) funcionalidade que usa um URL de armazenamento padrão. Agora, se a variável `config:show:default-url` não é possível buscar um URL de base, então o URL da variável MAGENTO_CLOUD_ROUTES é usado.<!-- MAGECLOUD-3866 -->

## v1.0.0

Data de lançamento: 12 de junho de 2019

Esta é a primeira versão do [`magento/magento-cloud-components`](https://github.com/magento/magento-cloud-components) que é uma nova dependência para `ece-tools` pacote versão 2002.0.20 e posterior.

- ![novo ícone](../../assets/new.svg) Adição da capacidade de usar padrões de regex para configurar o **PÁGINAS_AQUECIDAS** variável de ambiente para armazenar em cache páginas únicas, vários domínios e várias páginas. Consulte [Variáveis pós-implantação](../environment/variables-post-deploy.md#warm_up_pages).<!--MAGECLOUD-3258-->
