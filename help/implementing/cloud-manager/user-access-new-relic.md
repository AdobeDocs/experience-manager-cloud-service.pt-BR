---
title: Novo Relic Um
description: Saiba mais sobre o serviço APM (New Relic One application performance monitoring) para AEM as a Cloud Service e como você pode acessá-lo.
exl-id: 9fa0c5eb-415d-4e56-8136-203d59be927e
source-git-commit: 6cf164093cc543fe4847859b248e70efd86efbb1
workflow-type: tm+mt
source-wordcount: '1038'
ht-degree: 1%

---


# Novo Relic Um {#user-access}

Saiba mais sobre o serviço APM (New Relic One application performance monitoring) para AEM as a Cloud Service e como você pode acessá-lo.

## Introdução {#introduction}

O Adobe dá grande ênfase ao monitoramento, disponibilidade e desempenho de seu aplicativo. Para ajudar a atingir essa meta, o AEM as a Cloud Service fornece acesso a um novo conjunto de monitoramento de Relic One personalizado como parte da oferta padrão de produtos para garantir que suas equipes tenham a visibilidade máxima para suas métricas de desempenho do ambiente e do sistema as a Cloud Service AEM.

Este documento descreve os recursos de APM (New Relic One application performance monitoring) habilitados em seus ambientes AEM as a Cloud Service para ajudar a suportar o desempenho e permitir que você aproveite ao máximo AEM as a Cloud Service.

## Recursos {#transaction-monitoring}

O novo Relic One APM para AEM as a Cloud Service tem muitos recursos.

* Acesso direto a uma conta dedicada do Novo Relic One (acesso gerenciado pelo Adobe Support)

* Novo Relic Instrumentado Um agente APM que mostra chamadas exatas de método com números de linha, incluindo dependências externas e bancos de dados

* Otimização holística do desempenho ao combinar métricas principais do monitoramento de nível de infraestrutura e do monitoramento de aplicativos (Adobe Experience Manager)

* Exposição de AEM Mbeans JMX as a Cloud Service e verificações de integridade diretamente nas métricas do New Relic Insights, permitindo uma inspeção profunda do desempenho da pilha de aplicativos e das métricas de integridade.

## Acessar o novo Relic One {#accessing-new-relic}

Siga estas etapas para obter acesso à sua subconta New Relic One associada ao seu Programa as a Cloud Service AEM.

1. Abra uma solicitação acessando a guia Suporte no Admin Console.
1. Em sua solicitação, inclua os detalhes da ID do programa, bem como a lista de usuários que exigem acesso ao Novo Relic.
   * Devem ser fornecidos os nomes completos e os endereços de email válidos de todos os usuários.

Consulte o documento [Portal de suporte AEM para Experience Cloud](https://helpx.adobe.com/br/enterprise/using/support-for-experience-cloud.html) para obter mais detalhes sobre como abrir tíquetes.

Depois que o acesso é fornecido, o Novo Relic envia um email de confirmação para cada usuário, para que o usuário possa concluir o processo de configuração e fazer logon.

Se o usuário não conseguir localizar o email de confirmação da conta original, siga essas etapas.

1. Navegue até a página de logon do Novo Relic em [`login.newrelic.com/login`](https://login.newrelic.com/login).

1. Selecionar **Esqueceu sua senha?**.

   ![Novo logon do Relic](/help/implementing/cloud-manager/assets/new-relic/newrelic-1.png)

1. Digite o endereço de email da conta e selecione **Enviar meu link de redefinição**.

   ![Inserir endereço de email](/help/implementing/cloud-manager/assets/new-relic/newrelic-2.png)

1. O New Relic enviará ao usuário um email contendo um link para confirmar a conta.

Se você concluir o processo de inscrição e não conseguir fazer logon em sua conta devido a mensagens de erro de email ou senha, registre um tíquete de suporte por meio do [Admin Console](https://adminconsole.adobe.com/).

>[!TIP]
>
>Se você não receber um email do New Relic:
>
>* Verifique sua [filtros de spam](https://docs.newrelic.com/docs/accounts/accounts-billing/account-setup/create-your-new-relic-account/).
>* Se aplicável, [adicionar novo link à sua lista de permissões de email](https://docs.newrelic.com/docs/accounts/accounts/account-maintenance/account-email-settings/#email-whitelist).
>* Se nenhuma das sugestões ajudar, forneça feedback sobre o tíquete de suporte e a equipe de suporte do Adobe ajudará você ainda mais.


### Verificar seu email {#verify-email}

Se for solicitado que você verifique seu email durante o logon, significa que seu email está associado a várias contas. Isso permite escolher qual conta acessar.

Se você não verificar seu endereço de email, o New Relic tentará fazer logon com o registro de usuário criado mais recentemente associado ao seu endereço de email. Para evitar a verificação do email durante cada logon, clique no botão **Lembre-se de mim** na tela de logon.

Para obter mais ajuda, abra um tíquete de suporte pelo [Portal de suporte AEM](https://helpx.adobe.com/enterprise/using/support-for-experience-cloud.html).

## Exceções {#exceptions}

AEM as a Cloud Service oferece apenas a solução Nova versão em um APM e não oferece suporte para alertas, registros ou integrações de API.

Para obter mais ajuda ou orientação adicional sobre as ofertas do Novo Relic One para o seu Programa as a Cloud Service AEM, abra um tíquete de suporte via [Portal de suporte AEM](https://helpx.adobe.com/enterprise/using/support-for-experience-cloud.html).

## Perguntas frequentes sobre a nova conta do Relic {#faqs}

### O que o Adobe monitora com o Novo Relic One? {#adobe-monitor}

O Adobe monitora os serviços de criação, publicação e visualização AEM as a Cloud Service (quando disponíveis) por meio do plug-in Java do New Relic One. O Adobe permite a telemetria e o monitoramento personalizados do New Relic One APM em ambientes de não produção e produção AEM as a Cloud Service.

Sua conta New Relic One é anexada a uma conta Adobe principal mantida e tem vários aplicativos reportando nela: três por AEM ambiente as a Cloud Service.

* Um aplicativo para o serviço de criação por ambiente
* Um aplicativo para o serviço de publicação por ambiente (incluindo o Golden Publish)
* Um aplicativo para o serviço de visualização por ambiente

Observação:

* Cada aplicativo usa uma chave de licença.
* AEM ambientes as a Cloud Service reportam-se a apenas uma conta do Novo Relic One.
* Métricas e eventos de monitoramento completo do Novo Relic One são retidos por 7 dias.

### Quem pode acessar os dados do serviço em nuvem New Relic One? {#access-new-relic-cloud}

O acesso total de leitura será concedido para até 10 membros de sua equipe. O acesso de leitura incluirá todas as métricas de APM coletadas pelo agente do Novo Relic One.

### A configuração personalizada de SSO é suportada? {#custom-sso}

A configuração personalizada do SSO não é suportada para a conta do Novo Relic One provisionada pelo Adobe.

### E se eu já tiver uma assinatura do New Relic no local? {#new-relic-subscription}

O Novo Relic One é a nova plataforma de observabilidade do New Relic e permite que o suporte ao Adobe e suas equipes observem, monitorem e visualizem métricas e eventos, tudo em um único lugar.

O novo Relic One fornece aos usuários a capacidade de pesquisar em todas as contas, onde eles têm acesso e visualizar os dados de todos os serviços e hosts em uma única visualização.

Embora o suporte ao Adobe monitore o aplicativo as a Cloud Service AEM usando o New Relic One e outras ferramentas internas como parte de seu serviço, suas equipes podem continuar a utilizar o New Relic para serviços e infraestrutura hospedados no local. Eles poderão visualizar os dados de contas do Adobe New Relic One e de contas New Relic gerenciadas pelo cliente.

>[!NOTE]
>
>Para visualizar ambos os conjuntos de dados no Novo Relic One, um usuário deve ter as permissões certas e usar a mesma metodologia de logon para ambas as contas (Adobe New Relic One e New Relic accounts gerenciadas pelo cliente).
