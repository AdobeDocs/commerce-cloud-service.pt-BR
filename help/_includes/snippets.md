---
source-git-commit: b08443d937dfc18120daa0d6a1277b9c7bca67aa
workflow-type: tm+mt
source-wordcount: '829'
ht-degree: 0%

---
# Trechos de nuvem

## aviso de Elasticsearch {#elasticsearch-support}

>[!WARNING]
>
>O Elasticsearch 7.11 e posterior não é compatível com o Adobe Commerce na infraestrutura em nuvem. As versões do Adobe Commerce 2.3.7-p3, 2.4.3-p2 e 2.4.4 e posteriores são compatíveis com o serviço OpenSearch. As instalações locais continuam a suportar o Elasticsearch.

## Integração aprimorada {#enhanced-integration-envs}

>[!NOTE]
>
>Os projetos provisionados antes de 5 de junho de 2020 tinham vários ambientes de integração menores. Se você precisar de um ambiente de Integração maior para teste e desenvolvimento, solicite uma atualização para os ambientes de Integração aprimorada. Consulte a [Solicitação de ambiente de integração](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/announcements/commerce-announcements/integration-environment-enhancement-request-pro-and-starter.html) artigo na _Centro de ajuda do Adobe Commerce_ para obter detalhes.

## Opções de mesclagem {#merge-options}

Por padrão, o processo de implantação substitui todas as configurações no `env.php` arquivo; no entanto, você pode optar por mesclar um ou mais valores para uma configuração de serviço sem substituir todos os valores.

Defina o `_merge` opção para uma das seguintes opções:

- `true`—**Mesclar** os valores de serviço configurados com os valores da variável de ambiente.
- `false`—**Substituir** os valores de serviço configurados com os valores da variável de ambiente.

## Repositório privado {#private-repository}

>[!NOTE]
>
>A Adobe recomenda o uso de um repositório privado para o seu projeto do Adobe Commerce na infraestrutura em nuvem para proteger qualquer informação proprietária ou trabalho de desenvolvimento, como extensões e configurações confidenciais.

## Aviso de autoatendimento do profissional {#pro-self-service-warning}

>[!WARNING]
>
>Alguns **Projetos Pro** exigir um tíquete de suporte para atualizar a configuração de rota no `routes.yaml` e a configuração do cron no `.magento.app.yaml` arquivo. O Adobe recomenda atualizar e testar arquivos de configuração YAML em um ambiente de Integração e, em seguida, implantar alterações no ambiente de Preparo. Se suas alterações não forem aplicadas aos sites de Preparo após a reimplantação e não houver mensagens de erro relacionadas no log, você **DEVE** [Enviar um tíquete de suporte da Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) que descreve as tentativas de alteração de configuração. Inclua quaisquer arquivos de configuração YAML atualizados no ticket.

## Suporte a serviços profissionais {#pro-update-service}

>[!TIP]
>Para projetos Pro, você deve [enviar um tíquete de suporte da Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) para instalar ou atualizar [serviços](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/service/services-yaml.html) in `Staging` e `Production` somente ambientes.
>
>Indique as alterações de serviço necessárias, inclua as atualizações `.magento.app.yaml` e `services.yaml` e indique a versão do PHP no ticket. Para alterações de autoatendimento na versão, extensões ou configurações do ambiente do PHP, consulte [Configurações do PHP](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/app/php-settings.html) in _Configuração do aplicativo_.
>
>Para alterações em um _live_ Ambiente de produção (**Somente Pro**), você deve fornecer um aviso mínimo de 48 horas para permitir que a equipe de infraestrutura da nuvem tenha tempo suficiente para realizar o marshaling dos recursos e realizar uma atualização segura.

## Backups Pro {#pro-backups}

>[!TIP]
>
>Em ambientes de preparo e produção profissionais, você deve [enviar um tíquete de suporte da Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) para recuperar um backup específico, observando a data, a hora e o fuso horário no ticket.
>
>O Adobe faz **não** restaure qualquer ambiente a partir de um backup automático. Consulte [Restaurar um instantâneo do banco de dados de preparo ou produção](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/restore-a-db-snapshot-from-staging-or-production.html) para obter ajuda sobre como escolher um método para restaurar um instantâneo de Preparo ou Produção.

## Aviso de reimplantação {#redeploy-warning}

>[!WARNING]
>
>O processo de implantação começa quando você executa uma mesclagem, envio por push ou sincronização do seu ambiente, ou quando você aciona uma reimplantação manual, durante a qual o [!DNL Commerce] o aplicativo está no modo de manutenção. Para um ambiente de produção, a Adobe recomenda concluir esse trabalho fora do horário de pico para evitar interrupções do serviço.

## Espaço reservado da rota {#route-placeholder}

>[!NOTE]
>
>Os exemplos de configuração de rota a seguir usam modelos de rota com espaços reservados. A variável `{default}` o espaço reservado representa o domínio padrão configurado para o site. Se o seu projeto tiver vários domínios, use o `{all}` espaço reservado para configurar o roteamento para o domínio padrão e todos os aliases. Consulte [Configurar rotas](/help/cloud-guide/routes/routes-yaml.md).

## Tempo de SCD {#scd-timing-warning}

>[!WARNING]
>
>Se tiver problemas com arquivos de conteúdo estático no aplicativo após a implantação, como arquivos de tema personalizados ausentes, aumente o tempo de execução máximo esperado para 900 segundos ou mais.

## Implantação baseada em cenário {#scenarios}

>[!NOTE]
>
>Com [!DNL ECE-Tools] 2002.1.0 e versões posteriores, você pode usar o recurso de implantação baseada em cenário para personalizar os processos de criação, implantação e pós-implantação do seu projeto Adobe Commerce na infraestrutura em nuvem. Consulte [Implantação baseada em cenário](/help/cloud-guide/deploy/scenario-based.md).

## Instrução de serviço {#service-instruction}

Use as instruções a seguir para configurar o serviço em ambientes Pro Integration e Starter, incluindo o `master` filial.

>[!NOTE]
>
>[Enviar um tíquete de suporte da Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) para alterar a configuração do serviço em ambientes de produção e preparo profissionais.

## Alteração de serviço {#service-change-tip}

>[!TIP]
>
>Após a configuração inicial do serviço, é possível alterar a versão do software de um serviço instalado atualizando o `services.yaml` e `.magento.app.yaml` arquivos de configuração. Consulte [Alterar versão do serviço](/help/cloud-guide/services/services-yaml.md#change-service-version) para obter orientação sobre como atualizar ou rebaixar um serviço.

## Dica de implantação travada {#stuck-deployment-tip}

>[!TIP]
>
>Para obter ajuda com implantações paralisadas, use o [Solução de problemas de implantação do Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/deployment/magento-deployment-troubleshooter.html) no _Centro de ajuda do Commerce_.

## Atualização para ECE-Tools {#ece-tools-package}

>[!NOTE]
>
>Se você usar uma versão do Adobe Commerce na infraestrutura em nuvem que não contenha a variável `ece-tools` pacote, você deverá executar um [atualização única](/help/cloud-guide/dev-tools/install-package.md) ao projeto de nuvem para remover pacotes obsoletos. Se você usa atualmente a variável `ece-tools` e você precisa atualizá-lo, consulte [Atualize o pacote ECE-Tools](/help/cloud-guide/dev-tools/update-package.md).

## Dica de atualização {#upgrade-tip}

>[!TIP]
>
>Antes de iniciar uma atualização ou um processo de patch, crie uma ramificação ativa do ambiente de integração e faça check-out da nova ramificação para a estação de trabalho local. Dedicar uma ramificação à atualização ou ao processo de patch ajuda a evitar interferência com o trabalho em andamento.

<!-- Fastly-related snippets begin -->

## Logon de administrador {#admin-login-step}

1. [Fazer logon](/help/get-started/onboarding.md#access-your-admin-panel) para o Administrador.

## Automatizar a implantação de trecho de VCL personalizado {#automate-vcl-snippet-deployment}

>[!NOTE]
>
>Em vez de carregar manualmente os trechos de VCL personalizados, você pode adicionar trechos à `$MAGENTO_CLOUD_APP_DIR/var/vcl_snippets_custom` no seu ambiente. Os trechos neste diretório são carregados automaticamente ao clicar em _fazer upload de VCL para Fastly_ no Administrador de comércio. Consulte [Implantação automatizada de trechos de VCL personalizados](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/CUSTOM-VCL-SNIPPETS.md#automated-custom-vcl-snippets-deployment) no módulo CDN Fastly para a documentação do Magento 2.

<!-- Fastly-related snippets end -->
