---
title: Trabalhadores
description: Saiba como configurar a propriedade workers no [!DNL Commerce] arquivo de configuração do aplicativo.
feature: Cloud, Configuration
exl-id: d6816925-5912-45ca-8255-6c307e58542d
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 0%

---

# Propriedade dos trabalhadores

Você pode definir um worker para ser executado independentemente da instância da Web sem uma instância do Nginx em execução; no entanto, o worker usa o mesmo armazenamento de rede usado pelo [!DNL Commerce] aplicação. Você não precisa configurar um servidor Web na instância do worker (usando Node.js ou Go) porque o roteador não pode direcionar solicitações públicas ao worker. Isso torna a instância do trabalhador ideal para tarefas em segundo plano ou tarefas em execução continuamente que correm o risco de bloquear uma implantação.

## Configurar um trabalhador

Os funcionários estão disponíveis para uso somente com ambientes de preparo e produção profissionais. Os ambientes Pro integration e Starter podem optar por usar o [CRON_CONSUMERS_RUNNER](../environment/variables-deploy.md#cron_consumers_runner) variável.

Para configurar um colaborador no Estágio Profissional ou na Produção, [Enviar um tíquete de suporte da Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) e incluir as seguintes informações:

- ID do projeto
- ID do ambiente
- Nome do trabalhador
- Comandos Start

É possível configurar um processo por trabalhador. Uma configuração básica e comum do operador no `.magento.app.yaml` O arquivo pode ter a seguinte aparência:

```yaml
workers:
    queue:
        commands:
            start: |
                php ./bin/magento queue:consumers:start commerce.eventing.event.publish
```

Este exemplo define um único trabalhador chamado `queue`, com um pequeno nível (tamanho S) de alocação de recursos, e executa o `php ./bin/magento` comando na inicialização. O trabalhador `queue` em seguida, é executado em cada nó como um processo de trabalho. Se o comando for encerrado, ele será reiniciado automaticamente.

## Comandos e substituições

A variável `commands.start` a chave é necessária para iniciar comandos com o aplicativo de trabalho. Você pode usar qualquer comando shell válido, embora seja ideal usar o idioma do aplicativo. Se o comando especificado pelo `start` for encerrada, ela será reiniciada automaticamente.

>[!IMPORTANT]
>
>A variável `deploy` e `post_deploy` ganchos e `crons` os comandos são executados somente no contêiner da web, não em instâncias do trabalhador.

### Herança

Definições para o `size`, `relationships`, `access`, `disk` e `mount`, e `variables` as propriedades são herdadas por um trabalhador, a menos que sejam explicitamente substituídas.

As propriedades a seguir são as mais usadas para substituir [configurações de nível superior](properties.md):

- `size`— aloque menos recursos a um único processo em segundo plano
- `variables`—instruir o aplicativo para executar de forma diferente

### Tempo e enfileiramento

Embora cada trabalhador fique atrás de outro, a configuração a seguir produz uma separação consistente de dois segundos nos carimbos de data e hora no `var/time.txt` arquivo, independentemente do sleep de oito segundos no código PHP:

```yaml
workers:
    time1:
        commands:
            start: 'php -r "sleep(8); echo time() . PHP_EOL;" >> var/time.txt& sleep 2'
```
