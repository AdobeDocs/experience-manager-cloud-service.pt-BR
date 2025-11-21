---
title: New Relic One
description: Saiba mais sobre o serviço de monitoramento de desempenho de aplicativo (APM) da New Relic One para o AEM as a Cloud Service e como você pode acessá-lo.
exl-id: 9fa0c5eb-415d-4e56-8136-203d59be927e
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: 2c863e0cfad3211e811665a5169def7705e8b907
workflow-type: tm+mt
source-wordcount: '1817'
ht-degree: 39%

---


# New Relic One {#user-access}

Saiba mais sobre o serviço de monitoramento de desempenho de aplicativo (APM) da New Relic One para o AEM as a Cloud Service e como você pode acessá-lo.

## Sobre o New Relic One {#introduction}

A Adobe atribui grande importância ao monitoramento, disponibilidade e desempenho do seu aplicativo. O AEM as a Cloud Service inclui acesso ao monitoramento do New Relic One, oferecendo às equipes visibilidade abrangente das métricas de desempenho do sistema e do ambiente como parte da oferta padrão de produtos.

Este documento descreve como gerenciar o acesso aos recursos de monitoramento de desempenho de aplicativo (APM) do New Relic One em ambientes AEM as a Cloud Service. O gerenciamento eficaz desses recursos suporta o desempenho ideal e maximiza os benefícios do AEM as a Cloud Service.

Quando um novo programa de produção é criado, a subconta do New Relic One associada ao seu programa do AEM as a Cloud Service é criada automaticamente. [Esta subconta deve ser ativada](#activate-sub-account) para começar a assimilar dados.

## Recursos {#transaction-monitoring}

O APM da New Relic One para AEM as a Cloud Service inclui muitos recursos.

* Acesso direto a uma conta dedicada do New Relic One

* O agente APM instrumentado da New Relic One que mostra chamadas de método exatas com números de linha, incluindo dependências externas e bancos de dados

* Otimização integral do desempenho ao combinar métricas principais do monitoramento ao nível de infraestrutura e do monitoramento de aplicativos (Adobe Experience Manager)

* A AEM as a Cloud Service expõe MBeans do Java Management Extensions (JMX) e verificações de integridade diretamente no New Relic Insights, permitindo uma inspeção detalhada do desempenho do aplicativo e das métricas de integridade.

## Ativar a subconta do New Relic One {#activate-sub-account}

Para um programa recém-criado, uma subconta do New Relic One é criada para você. No entanto, você deve ativá-lo para assimilar dados. Essa ativação não é automática. Siga estas etapas para ativar a subconta.

>[!NOTE]
>
>Um usuário com a função **Proprietário da empresa** deve estar conectado para gerenciar a subconta do New Relic One.

1. Faça logon no Cloud Manager, em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/), e selecione a organização apropriada.

1. No console **[Meus Programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, clique no programa para o qual você deseja gerenciar seus usuários do New Relic One.

1. Na parte inferior do cartão **Ambientes** na página de visão geral do programa, clique em ![Mais ícone](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) e selecione **Ativar New Relic**.

   ![Gerenciar usuários](assets/newrelic-activate-sub-account.png)

   * Você também pode acessar a opção **Gerenciar usuários**. Na parte superior da tela **Ambientes** do seu programa, clique em ![Ícone Aproveitar mais](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg).

1. [Execute um pipeline](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#running-pipelines) para o mesmo ambiente para concluir com êxito a ativação da subconta.

Quando a subconta é desativada, não há assimilação de dados.

## Gerenciar usuários do New Relic One {#manage-users}

Siga estas etapas para definir os usuários da sua subconta da New Relic One associada ao seu programa do AEM as a Cloud Service.

>[!NOTE]
>
>Um usuário na função de **Proprietário da empresa** ou **Gerente de implantação** deve estar conectado para gerenciar usuários do New Relic One.

1. Faça logon no Cloud Manager, em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/), e selecione a organização apropriada.

1. Clique no programa para o qual você deseja gerenciar os usuários do New Relic One.

1. Na parte inferior do cartão **Ambientes** na página de visão geral do programa, clique no ![ícone Mais](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) e selecione **Gerenciar usuários**.

   ![Gerenciar usuários](assets/newrelic-manage-users.png)

   * Você também pode acessar a opção **Gerenciar usuários**. Na parte superior da tela **Ambientes** do seu programa, clique em ![Ícone Aproveitar mais](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg).

1. Na caixa de diálogo **Gerenciar usuários do New Relic**, digite o nome e o sobrenome do usuário que deseja adicionar e clique no botão **Adicionar**. Repita essa etapa para todos os usuários que deseja adicionar.

   ![Adicionar usuários](assets/newrelic-add-users.png)

1. Para remover usuários da New Relic One, clique no botão Excluir na extremidade direita da linha que representa o usuário.

1. Clique em **Salvar** para criar os usuários.

Depois de definir os usuários, a New Relic envia um email de confirmação para cada usuário ao qual você concedeu acesso, de modo que o indivíduo possa concluir o processo de configuração e fazer logon.

>[!NOTE]
>
>Se você estiver gerenciando os usuários do New Relic One, também deverá adicionar a si mesmo como usuário para ter acesso a si mesmo. Para ter acesso à New Relic One, não basta ter a função **Proprietário da empresa** ou **Gerente de implantação**. Você também deve criar a si mesmo como usuário.

## Ativar sua conta de usuário do New Relic One {#activate-user-account}

Depois que uma conta de usuário da New Relic One é criada conforme descrito na seção de visualização [Gerenciar usuários da New Relic One](#manage-users), a New Relic envia a esses usuários um email de confirmação para o endereço fornecido. Para usar essas contas, os usuários devem primeiro ativar suas contas junto à New Relic, redefinindo suas senhas.

**Para ativar sua conta de usuário do New Relic One:**

1. Clique no link fornecido por email pelo New Relic.

1. Na página de entrada do New Relic, clique em **Esqueceu sua senha?**

   ![Logon na New Relic](/help/implementing/cloud-manager/assets/new-relic/newrelic-1.png)

1. Digite o endereço de email no qual você recebeu o email de confirmação e selecione **Enviar meu link de redefinição**.

   ![Inserir endereço de email](/help/implementing/cloud-manager/assets/new-relic/newrelic-2.png)

1. O New Relic envia um email contendo um link para confirmar a conta.

Se você não receber um email de confirmação da New Relic, consulte a [seção de solução de problemas](#troubshooting).

## Acessar o New Relic One {#accessing-new-relic}

Depois de [ativar sua conta do New Relic](#activate-account), você poderá acessar o New Relic One diretamente ou pela Cloud Manager.

**Para acessar o New Relic One por meio do Cloud Manager:**

1. Faça logon no Cloud Manager, em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/), e selecione a organização apropriada.

1. Clique no programa para o qual deseja acessar o New Relic One.

1. Na parte inferior do cartão **Ambientes** na página de visão geral do programa, clique no ![ícone Mais](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) e selecione **Abrir o New Relic**.

   ![Gerenciar usuários](assets/newrelic-access.png)

   * Você também pode acessar o New Relic. Na parte superior da tela **Ambientes** do seu programa, clique em ![Ícone Aproveitar mais](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg).

1. Na nova guia do navegador que é aberta, faça logon na New Relic One.

**Para acessar o New Relic One diretamente:**

1. Acesse a página de logon do New Relic em [`https://login.newrelic.com/login`](https://login.newrelic.com/login)

1. Faça logon na New Relic One.

### Verificar seu email {#verify-email}

Se for solicitado que você verifique seu email ao fazer logon no New Relic One, significa que seu email está associado a várias contas. Você pode escolher qual conta acessar.

Se você não verificar seu endereço de email, a New Relic tentará fazer seu logon com o registro de usuário criado mais recentemente que esteja associado ao seu endereço de email. Para evitar a verificação do email em cada logon, clique na caixa de seleção **Lembrar-se de mim** na tela de logon.

Para obter mais ajuda, abra um tíquete de suporte por meio do [Portal de suporte do AEM](https://helpx.adobe.com/br/enterprise/using/support-for-experience-cloud.html).

## Solução de problemas de acesso de usuários ao New Relic One {#troubleshooting}

Se você foi adicionado como um usuário do New Relic One, conforme descrito em [Gerenciar usuários do New Relic One](#manage-users), e não puder localizar o email de confirmação da conta original, poderá executar as seguintes etapas de solução de problemas.

**Para solucionar problemas de acesso de usuário ao New Relic One:**

1. Acesse a página de logon do New Relic em [`login.newrelic.com/login`](https://login.newrelic.com/login).

1. Clique em **[!UICONTROL Esqueceu sua senha?]**.

   ![Logon na New Relic](/help/implementing/cloud-manager/assets/new-relic/newrelic-1.png)

1. Digite o endereço de email usado para criar sua conta e selecione **Enviar meu link de redefinição**.

   ![Inserir endereço de email](/help/implementing/cloud-manager/assets/new-relic/newrelic-2.png)

1. O New Relic envia um email contendo um link para confirmar a conta.

Se você concluir o processo de inscrição e não conseguir fazer logon em sua conta devido a mensagens de erro relacionadas a email ou senha, registre um tíquete de suporte por meio da [Admin Console](https://adminconsole.adobe.com/).

Se você não receber um email do New Relic, faça o seguinte:

* Verifique seus [filtros de spam](https://docs.newrelic.com/docs/accounts/accounts-billing/account-setup/create-your-new-relic-account/).
* Se aplicável, [adicione o New Relic ao seu incluo na lista de permissões de email](https://docs.newrelic.com/docs/accounts/accounts/account-maintenance/account-email-settings/#email-whitelist).
* Se nenhuma das sugestões ajudar, forneça feedback sobre o tíquete de suporte.

## Notas de uso {#usage-notes}

* É possível adicionar no máximo 30 usuários. Se o número máximo de usuários for atingido, remova alguns para poder adicionar novos.
* Os usuários adicionados ao New Relic são do tipo **Básico**. Consulte a [documentação do New Relic para obter detalhes](https://docs.newrelic.com/docs/accounts/accounts-billing/new-relic-one-user-management/user-type/).
* O AEM as a Cloud Service somente oferece a solução de APM da New Relic One e não oferece suporte a alertas, registros ou integrações de API.

>[!NOTE]
>
>Se nenhuma atividade de **logon de usuário** for detectada na sua subconta do New Relic One por 30 dias ou mais, o agente APM será interrompido. Os dados não são enviados do AEM Cloud Service para o New Relic. *Os dados não serão enviados novamente até que sua subconta seja reativada.*
>
>Siga as mesmas etapas na seção [Ativar a subconta do New Relic One](#activate-sub-account) deste documento para reativar a subconta do New Relic One.

Para obter mais ajuda ou orientação sobre as ofertas da New Relic One para o seu Programa AEM as a Cloud Service, abra um tíquete de suporte no [Portal de Suporte da AEM](https://helpx.adobe.com/br/enterprise/using/support-for-experience-cloud.html).

## Perguntas frequentes {#faqs}

+++**O que o Adobe monitora com o New Relic One?**

A Adobe monitora os serviços de autoria, publicação e visualização do AEM as a Cloud Service (quando disponíveis) por meio do plug-in Java da New Relic One. A Adobe habilita a telemetria e o monitoramento personalizados da APM da New Relic One em ambientes de produção e não produção do AEM as a Cloud Service.

Sua conta do New Relic One é anexada a uma conta principal mantida pela Adobe e tem vários aplicativos subordinados a ela; três por ambiente AEM as a Cloud Service.

* Um aplicativo para o serviço do Autor por ambiente
* Um aplicativo para o serviço `Publish` por ambiente (incluindo o Golden Publish)
* Um aplicativo para o serviço de Visualização por ambiente

Observação:

* Cada aplicativo usa uma chave de licença.
* Os ambientes do AEM as a Cloud Service são subordinados a apenas uma conta da New Relic One.
* As métricas e os eventos completos de monitoramento do New Relic One são retidos por três meses.

+++

+++**O Adobe envia notificações de alerta do New Relic One?**

A Adobe fornece acesso ao New Relic One somente para fins de observação e não o usa para alertas de clientes ou alertas operacionais internos. As notificações para qualquer incidente são enviadas usando [perfis de notificação de usuário](/help/journey-onboarding/notification-profiles.md).
+++

+++**Quem pode acessar os dados do New Relic One Cloud Service?**

O acesso integral para leitura será concedido para até 30 membros da sua equipe. O acesso de leitura inclui todas as métricas de APM coletadas pelo agente do New Relic One.
+++

+++**Há suporte para a configuração personalizada de SSO?**

A configuração personalizada do SSO não é suportada para a conta da New Relic One provisionada pela Adobe.
+++

+++**E se eu já tiver uma assinatura local do New Relic?**

A New Relic One é a nova plataforma de observabilidade da New Relic e permite que o suporte da Adobe e suas equipes observem, monitorem e visualizem métricas e eventos, tudo em um só lugar.

A New Relic One fornece aos usuários a capacidade de pesquisar em todas as contas, nas quais têm acesso e visualizam dados de todos os serviços e hosts em uma única visualização.

O suporte da Adobe monitora o AEM as a Cloud Service com o New Relic One e outras ferramentas, enquanto suas equipes ainda podem usar o New Relic para serviços e infraestrutura locais. Eles poderão visualizar os dados de contas da New Relic One gerenciadas pela Adobe e de contas da New Relic gerenciadas pelo cliente.

>[!NOTE]
>
>Para visualizar ambos os conjuntos de dados na New Relic One, um usuário precisa ter as permissões certas e usar a mesma metodologia de logon para ambas as contas (contas da New Relic One gerenciadas pela Adobe e contas da New Relic gerenciadas pelo cliente).

+++

+++**O agente APM da minha conta do New Relic One foi interrompido. O que aconteceu?**

[Os agentes APM serão interrompidos](#limitations) se nenhuma atividade for detectada por 30 dias ou mais. Siga as mesmas etapas na seção [Ativar a subconta do New Relic One](#activate-sub-account) deste documento para reativar a subconta do New Relic One.
+++
