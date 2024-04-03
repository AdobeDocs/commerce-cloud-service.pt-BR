---
title: Serviço de email SendGrid
description: Saiba mais sobre o serviço de email SendGrid para Adobe Commerce na infraestrutura em nuvem e como você pode testar sua configuração de DNS.
exl-id: 30d3c780-603d-4cde-ab65-44f73c04f34d
source-git-commit: 7c22dc3b0e736043a3e176d2b7ae6c9dcbbf1eb5
workflow-type: tm+mt
source-wordcount: '1019'
ht-degree: 0%

---

# Serviço de email SendGrid

O serviço de proxy SendGrid SMTP (Simple Mail Transfer Protocol) fornece autenticação de email de saída e serviços de monitoramento de reputação, incluindo suporte para:

* Todos os emails transacionais de saída
* Endereços IP dedicados
* Registro de domínio, assinaturas do DomainKeys Identified Mail (DKIM) para validação de domínio de email (somente para ambientes de preparo e produção profissionais)
* Registro de domínio personalizado (somente para Pro)
* Integração automatizada para ambientes de integração Starter e Pro. Os ambientes de produção e de preparo profissionais exigem provisionamento e configuração manuais durante o processo de provisionamento de hardware do IaaS (Infrastructure as a Service, infraestrutura como serviço)

O proxy SMTP SendGrid não se destina ao uso como um servidor de email de uso geral para receber emails de entrada ou para uso com campanhas de marketing por email.

>[!TIP]
>
>Você pode encontrar detalhes do SendGrid para sua conta na [Interface de integração](https://cloud.magento.com) e selecione o **Detalhes do projeto** > **Informações de hospedagem** guia.

## Ativar ou desativar email

Por padrão, o email de saída é ativado nos ambientes de produção profissional e de preparo. A variável [!UICONTROL Outgoing emails] pode aparecer nas configurações do ambiente independentemente do status até que você defina a `enable_smtp` propriedade. Você pode permitir que emails de saída de outros ambientes enviem emails de autenticação de dois fatores para usuários de projetos na nuvem. Consulte [Configurar emails para teste](outgoing-emails.md).

## Painel SendGrid

Todos os projetos na nuvem são gerenciados em uma conta central, portanto, somente o Suporte tem acesso ao painel SendGrid. O SendGrid não fornece recursos de restrição de subconta.

Para revisar os logs de atividades para obter o status do delivery ou uma lista de endereços de email devolvidos, rejeitados ou bloqueados, [enviar um tíquete de suporte da Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket). A equipe de suporte **não é possível** recuperar logs de atividades com mais de 30 dias.

Se possível, inclua as seguintes informações na solicitação:

* o endereço ou endereços de email afetados
* o período em questão (somente nos últimos 30 dias)
* o assunto do email

## Correio identificado de DomainKeys (DKIM)

O DKIM é uma tecnologia de autenticação de email que permite aos Provedores de Serviços de Internet (ISPs) identificar endereços de remetente legítimos e falsos, uma técnica comumente usada em phishing e fraudes por email. O DKIM depende de um proprietário de domínio que gerencia os registros DNS. Ao usar o DKIM, o servidor do remetente usa uma chave privada para assinar as mensagens. Além disso, o proprietário do domínio adiciona um registro DKIM, que é um registro `TXT` para os registros DNS do domínio do remetente. Este `TXT` O registro contém uma chave pública que os servidores de email dos destinatários usam para verificar a assinatura de uma mensagem. O procedimento de criptografia de chave pública DKIM permite que os destinatários verifiquem a autenticidade de um remetente. Consulte [Explicação dos registros DKIM](https://docs.sendgrid.com/ui/account-and-settings/dkim-records).

>[!WARNING]
>
>As assinaturas DKIM do SendGrid e o suporte à autenticação de domínio estão disponíveis apenas para projetos Pro e não para o Starter. Como resultado, os emails transacionais de saída provavelmente serão sinalizados por filtros de spam. Usar DKIM melhora a taxa de entrega como um remetente de email autenticado. Para melhorar a taxa de delivery de mensagens, você pode atualizar do Starter para o Pro ou usar seu próprio servidor SMTP ou provedor de serviços de delivery de email. Consulte [Configurar conexões de email](https://experienceleague.adobe.com/docs/commerce-admin/systems/communications/email-communications.html) no _Guia de sistemas do administrador_.

### Autenticação de remetente e domínio

Para que o SendGrid envie emails transacionais em seu nome de ambientes de Produção Pro ou de Preparo, você deve definir as configurações de DNS para incluir as três entradas de DNS do subdomínio SendGrid. A cada conta do SendGrid é atribuído um `TXT` registro usado para autenticar emails de saída.

**Para habilitar a autenticação de domínio**:

1. Enviar um [tíquete de suporte](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) que solicita a ativação do DKIM para um domínio específico (**Somente ambientes de preparo e produção profissionais**).
1. Atualize sua configuração de DNS com o `TXT` e `CNAME` registros fornecidos a você no tíquete de suporte.

**Exemplo `TXT` registro com ID de conta**:

```text
v=spf1 include:u17504801.wl.sendgrid.net -all
```

**Exemplo `CNAME` registros**:

| Domínio | Aponta para | Tipo de registro |
| ---------- | ---------- | ------------- |
| em.emaildomain.com | uxxxxxx.wl.sendgrid.net | CNAME |
| s1_domainkey.emaildomain.com | s1.domainkey.uxxxxxx.wl.sendgrid.net | CNAME |
| s2_domainkey.emaildomain.com | s2.domainkey.uxxxxxx.wl.sendgrid.net | CNAME |

### Assinaturas DKIM e segurança automatizada

Você pode escolher entre segurança automática e manual ao configurar um domínio autenticado. Se você escolher a segurança automatizada, o SendGrid gerenciará os registros DKIM e SPF automaticamente. Quando você adiciona um novo endereço IP de envio dedicado à sua conta, o SendGrid atualiza as configurações de DNS e a assinatura DKIM imediatamente. Se você desativar a segurança automática, será responsável por atualizar sua assinatura DKIM sempre que alterar seu domínio de envio.

**Exemplo de segurança automatizada ativada**:

```text
subdomain.mydomain.com. | CNAME | uxxxxxx.wl.sendgrid.net
s1._domainkey.mydomain.com. | CNAME | s1.domainkey.uxxxxxx.wl.sendgrid.net
s2._domainkey.mydomain.com. | CNAME | s2.domainkey.uxxxxxx.wl.sendgrid.net
```

**Exemplo de segurança automatizada desativada**:

```text
me12345.mydomain.com | MX | mx.sendgrid.net
me12345.mydomain.com | TXT | v=spf1 include:sendgrid.net ~all
m1._mydomain.com | TXT | k=rsa; t=s; p=<public-key>
```

Após a configuração da autenticação de domínio, o SendGrid manipula automaticamente os registros SPF (Estrutura de Política de Segurança) e DKIM para você. Depois que o SendGrid fornece a `CNAME` Registros a serem adicionados aos registros DNS, é possível adicionar endereços IP dedicados e fazer outras atualizações de conta sem precisar gerenciar os registros SPF manualmente. Consulte [Segurança automatizada e sua assinatura DKIM](https://docs.sendgrid.com/ui/account-and-settings/dkim-records#automated-security-and-your-dkim-signature).

Para testar a configuração do DNS:

```terminal
dig CNAME em.domain_name
dig CNAME s1._domainkey.domain_name
dig CNAME s2._domainkey.domain_name
```

## Limite de email transacional

O limite de email transacional se refere ao número de mensagens de email transacionais que você pode enviar de ambientes Pro em um período específico, como 12.000 emails por mês de ambientes não relacionados à produção. O limite foi projetado para proteger contra o envio de spam e possíveis danos à reputação do email.

Não há limites rígidos para o número de emails que podem ser enviados no ambiente de Produção, desde que a pontuação da Reputação do remetente seja superior a 95%. A reputação é afetada pelo número de emails devolvidos ou rejeitados e se os registros de spam baseados em DNS sinalizaram seu domínio como uma possível fonte de spam. Consulte [Emails não enviados quando os créditos SendGrid são excedidos no Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/emails-not-being-sent-sendgrid-credits-exceeded.html) no _Knowledge base de suporte do Commerce_.

**Para verificar se o máximo de créditos é excedido**:

1. Na estação de trabalho local, altere para o diretório do projeto.

1. Use o SSH para fazer logon no ambiente remoto.

   ```bash
   magento-cloud ssh
   ```

1. Verifique a `/var/log/mail.log` para `authentication failed : Maxium credits exceeded` entradas.

   Se você vir algum `authentication failed` entradas de log e a variável **Reputação de envio de email** for um mínimo de 95, você pode [Enviar um tíquete de suporte da Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) para solicitar um aumento da colocação de crédito.

### Reputação de envio de email

Uma reputação de envio de email é uma pontuação atribuída por um provedor de serviços de Internet (ISP) a uma empresa que envia mensagens de email. Quanto maior a pontuação, mais provável um ISP entregará mensagens na caixa de entrada de um recipient. Se a pontuação cair abaixo de um determinado nível, o ISP poderá rotear mensagens para a pasta de spam dos recipients ou até mesmo rejeitar mensagens completamente. A pontuação de reputação é determinada por vários fatores, como uma média de 30 dias de classificação de seus endereços IP em relação a outros endereços IP e taxa de reclamação de spam. Consulte [5 maneiras de verificar sua reputação de envio](https://sendgrid.com/blog/5-ways-check-sending-reputation/).
