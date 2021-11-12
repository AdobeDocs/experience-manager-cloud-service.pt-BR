---
title: Acesso do Usuário ao Novo Relic
description: Siga esta página para saber mais sobre o New Relic Application Performance Monitoring for AEM as a Cloud Service
source-git-commit: 62bee2d28c92c1d36651eb8b88607255640e511b
workflow-type: tm+mt
source-wordcount: '1049'
ht-degree: 0%

---


# Acesso do Usuário ao Novo Relic {#user-access}

## Introdução {#introduction}

O Adobe dá alta ênfase ao monitoramento, disponibilidade e desempenho de seu aplicativo. Para ajudar a atingir essa meta, o AEM as a Cloud Service fornece acesso a um novo conjunto personalizado de monitoramento de Relic como parte da oferta padrão de produto para garantir que suas equipes tenham a visibilidade máxima para o sistema Cloud Service Adobe Experience Manager e para as métricas de desempenho do ambiente. Esta seção descreve os recursos de monitoramento do New Relic habilitados em seus ambientes AEM as a Cloud Service para ajudar a reforçar o desempenho e permitir que você aproveite ao máximo AEM as a Cloud Service.

## AEM monitoramento as a Cloud Service de transações via Nova Relação - Proposta de Valor {#transaction-monitoring}

Aqui está o resumo da proposta de valor do New Relic Application Performance Monitoring para AEM as a Cloud Service:

* Acesso direto a uma conta dedicada do Novo Relic One (acesso gerenciado pelo Adobe Support).

* Agente APM Instrumentado New Relic que mostra chamadas exatas de método com números de linha, incluindo dependências externas e bancos de dados.

* Otimização holística do desempenho ao combinar métricas principais do monitoramento de nível de infraestrutura e do monitoramento de aplicativos (Adobe Experience Manager).

* Exposição de AEM Mbeans JMX as a Cloud Service e verificações de integridade diretamente nas métricas do New Relic Insights, permitindo uma inspeção profunda do desempenho da pilha de aplicativos e das métricas de integridade.

## Acesso à sua conta as a Cloud Service do Novo Relic AEM {#accessing-new-relic}

Sua conta dedicada do New Relic será provisionada e gerenciada pelo Adobe através do envolvimento do Atendimento ao cliente. O Adobe permanecerá o proprietário e o administrador e fornecerá a conta em seu nome para fornecer acesso à sua subconta dedicada.

Para obter acesso à sua subconta New Relic associada ao seu Programa as a Cloud Service AEM:

* Abra uma solicitação acessando a guia Suporte no Admin Console.
* Certifique-se de que seu tíquete inclua os detalhes da ID do programa, bem como a lista de usuários para os quais você solicita que as equipes do Adobe abram o acesso ao Novo Relic.
* Todos os usuários devem receber um nome completo e um endereço de email válido.

   >[!NOTE]
   >Consulte [Portal de suporte AEM para Experience Cloud](https://helpx.adobe.com/enterprise/using/support-for-experience-cloud.html) para obter mais detalhes.

Depois que o acesso é fornecido, o Novo Relic envia um email de confirmação para cada usuário, para que o usuário possa concluir o processo de configuração e fazer logon.

Se o usuário não conseguir localizar o email de confirmação da conta original:

1. Navegue até a página de logon do Novo Relic em [login.newrelic.com/login](https://login.newrelic.com/login).

1. Selecionar **Esqueceu sua senha**.

   ![](/help/implementing/cloud-manager/assets/new-relic/newrelic-1.png)

1. Digite o endereço de email da conta e selecione **Enviar meu link de redefinição**.

   ![](/help/implementing/cloud-manager/assets/new-relic/newrelic-2.png)

1. Quando o sistema do Novo Relic retornar uma mensagem de email, selecione o link nele para confirmar sua conta novamente.

   >[!NOTE]
   >Se você não receber um email do New Relic:
   >Verifique sua [filtros de spam](https://docs.newrelic.com/docs/accounts/accounts-billing/account-setup/create-your-new-relic-account/). Se aplicável, [adicionar novo link à sua lista de permissões de email](https://docs.newrelic.com/docs/accounts/accounts/account-maintenance/account-email-settings/#email-whitelist).
   >Por favor, dê feedback sobre o tíquete de suporte e nossas equipes ajudarão você ainda mais

1. Se você concluir o processo de inscrição e não conseguir fazer logon em sua conta devido a mensagens de erro de email ou senha, registre um tíquete de suporte via [Admin Console](https://adminconsole.adobe.com/).

### Verificar seu email {#verify-email}

Se for solicitado que você verifique seu email durante o logon, significa que seu email está associado a várias contas e terá a opção de verificar seu email durante o logon. Isso permitirá escolher qual conta acessar. Se você não verificar seu endereço de email, o New Relic tentará fazer logon com o registro de usuário criado mais recentemente associado ao seu endereço de email. Para evitar a verificação do email durante cada logon, clique na caixa de seleção Lembre-me na tela de logon.

Para obter mais ajuda, abra um tíquete de suporte via [Portal de suporte AEM](https://helpx.adobe.com/enterprise/using/support-for-experience-cloud.html).

## Exceções {#exceptions}

AEM as a Cloud Service enfoca a oferta somente na solução APM do Novo Relic e não oferece suporte para recursos de alerta, registro ou integração de API.

Para obter mais ajuda ou orientação adicional sobre as ofertas do New Relic para o seu AEM Programa as a Cloud Service, abra um tíquete de suporte via [Portal de suporte AEM](https://helpx.adobe.com/enterprise/using/support-for-experience-cloud.html) para obter assistência.

## Perguntas frequentes sobre a nova conta do Relic {#faqs}

### O que o Adobe monitora com o Novo Relic? {#adobe-monitor}

O Adobe monitora os serviços AEM as a Cloud Service Author, Publish and Preview (onde disponível) por meio do plug-in New Relic APM Java. O Adobe habilita a Telemetria APM Novo Relic personalizada e o monitoramento em ambientes as a Cloud Service de não-produção e produção AEM. Sua conta New Relic está anexada a uma conta Adobe principal mantida e tem vários aplicativos reportando nela.

Três por AEM ambiente as a Cloud Service:

* Um aplicativo para o serviço Autor por ambiente
* Um aplicativo para o Serviço de publicação por ambiente (incluindo a Publicação dourada)
* Um aplicativo para o serviço de Visualização por ambiente
   >[!IMPORTANT]
   >Cada aplicativo usa uma chave de licença, AEM ambientes as a Cloud Service relatarão somente para uma conta New Relic . As métricas e os eventos de monitoramento completo da APM do Novo Relic e da Infraestrutura são retidos por 7 dias.

### Quem pode acessar os dados do New Relic Cloud Service? {#access-new-relic-cloud}

O acesso total de leitura será concedido para até 10 membros de sua equipe. O acesso de leitura incluirá todas as métricas APM coletadas pelo agente New Relic .

### A configuração personalizada do SSO é suportada? {#custom-sso}

A configuração de SSO personalizada não é atualmente suportada para a conta New Relic provisionada pelo Adobe.

### E se você já tiver uma assinatura New Relic no local? {#new-relic-subscription}

A nova plataforma de observabilidade do New Relic chamada New Relic One permite que os grupos de suporte do Adobe e suas equipes observem, monitorem e visualizem métricas e eventos, tudo em um único lugar. O novo Relic One fornece aos usuários a capacidade de pesquisar em todas as contas, onde eles têm acesso e visualizar os dados de todos os serviços e hosts em uma única visualização. Embora as equipes de suporte do Adobe monitorem o aplicativo as a Cloud Service AEM usando o New Relic e outras ferramentas internas como parte de seu serviço, suas equipes podem continuar a utilizar o New Relic para serviços e infraestrutura hospedados no local. Eles poderão visualizar os dados do Adobe e de contas do New Relic gerenciadas pelo cliente.

>[!NOTE]
>O usuário deve ter as permissões certas e usar a mesma metodologia de logon para ambas as contas (Adobe e conta New Relic gerenciada pelo cliente).


