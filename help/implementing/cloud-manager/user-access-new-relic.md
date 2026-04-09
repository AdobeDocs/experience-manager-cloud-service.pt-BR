---
title: New Relic One
description: Saiba mais sobre o serviço de monitoramento de desempenho de aplicativo (APM) da New Relic One para o AEM as a Cloud Service e como você pode acessá-lo.
exl-id: 9fa0c5eb-415d-4e56-8136-203d59be927e
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: 090a890e25ee45fb8a46255c097f243a24b00756
workflow-type: tm+mt
source-wordcount: '2303'
ht-degree: 21%

---


# New Relic One {#user-access}

Saiba mais sobre o serviço de monitoramento de desempenho de aplicativo (APM) da New Relic One para o AEM as a Cloud Service e como você pode acessá-lo.

## Sobre o New Relic One {#introduction}

A Adobe atribui grande importância ao monitoramento, disponibilidade e desempenho do seu aplicativo. O AEM as a Cloud Service inclui acesso ao monitoramento do New Relic One, oferecendo às equipes visibilidade abrangente das métricas de desempenho do sistema e do ambiente como parte da oferta padrão de produtos.

Este artigo descreve como gerenciar o acesso aos recursos de monitoramento de desempenho de aplicativo (APM) do New Relic One em ambientes AEM as a Cloud Service. O gerenciamento eficaz desses recursos suporta o desempenho ideal e maximiza os benefícios do AEM as a Cloud Service.

Quando um novo programa de produção é criado, a subconta do New Relic One associada ao seu programa do AEM as a Cloud Service é criada automaticamente. [Esta subconta deve ser ativada](#activate-sub-account) para começar a assimilar dados.

## Recursos {#transaction-monitoring}

O APM da New Relic One para AEM as a Cloud Service inclui muitos recursos.

* Acesso direto a uma conta dedicada do New Relic One.

* Agente APM do New Relic One que mostra chamadas de método exato com números de linha, incluindo dependências externas e bancos de dados.

* Otimização holística do desempenho ao combinar métricas principais do monitoramento em nível de infraestrutura e do monitoramento de aplicativos (Adobe Experience Manager).

* Rastreadores de alterações automáticos para execuções de pipeline do Cloud Manager, atualizações do AEM e operações de Restauração de código. Esses rastreadores permitem que as equipes correlacionem implantações com alterações de desempenho de aplicativos diretamente no New Relic One.

## Ativar a subconta do New Relic One {#activate-sub-account}

Para um programa recém-criado, uma subconta do New Relic One é criada para você. No entanto, você deve ativá-lo para assimilar dados. Essa ativação não é automática. Siga estas etapas para ativar a subconta.

>[!NOTE]
>
>Um usuário com a função **Proprietário da empresa** deve estar conectado para gerenciar a subconta do New Relic One.

**Para ativar sua subconta do New Relic One:**

1. Entre no Cloud Manager em [experience.adobe.com](https://experience.adobe.com).
   1. Na seção **Acesso rápido**, clique em **Experience Manager**.
   1. No painel lateral esquerdo, clique em **Cloud Manager**.
1. Selecione a organização desejada.
1. No console **Meus Programas**, clique em um programa para o qual você deseja gerenciar seus usuários do New Relic One.
1. No menu do lado esquerdo, em **Serviços**, clique em ![Ícone de dados ou em ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Data_18_N.svg) **Ambientes**.
1. Na página Ambientes, próximo ao canto superior direito, clique no ![ícone Mais](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) e em **Ativar New Relic**.

   ![Ativar New Relic](/help/implementing/cloud-manager/assets/new-relic/new-relic-activate.png)

1. [Execute um pipeline](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#running-pipelines) para o mesmo ambiente para concluir com êxito a ativação da subconta.

Quando a subconta é desativada, não há assimilação de dados.

## Gerenciar usuários do New Relic One {#manage-users}

Você pode definir os usuários da sua subconta do New Relic One associada ao seu programa do AEM as a Cloud Service.

>[!NOTE]
>
>Um usuário na função de **Proprietário da empresa** ou **Gerente de implantação** deve estar conectado para gerenciar usuários do New Relic One.

**Para gerenciar usuários do New Relic One:**

1. Entre no Cloud Manager em [experience.adobe.com](https://experience.adobe.com).
   1. Na seção **Acesso rápido**, clique em **Experience Manager**.
   1. No painel lateral esquerdo, clique em **Cloud Manager**.
1. Selecione a organização desejada.
1. No console **Meus Programas**, clique em um programa para o qual você deseja gerenciar seus usuários do New Relic One.
1. No menu do lado esquerdo, em **Serviços**, clique em ![Ícone de dados ou em ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Data_18_N.svg) **Ambientes**.
1. Na página Ambientes, próximo ao canto superior direito, clique no ![ícone Mais](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) e em **Gerenciar Usuários**.

   ![Gerenciar usuários do New Relic](/help/implementing/cloud-manager/assets/new-relic/new-relic-manage-users.png)

1. Na caixa de diálogo **Gerenciar usuários do New Relic**, faça o seguinte:

   * Insira o nome e o sobrenome do usuário que deseja adicionar
   * Digite o endereço de email associado
   * Clique no ![ícone Adicionar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Add_18_N.svg) **Adicionar**. Repita essa etapa para cada usuário que deseja adicionar.
   * Clique em ![Excluir ícone](https://spectrum.adobe.com/static/icons/workflow_18/Smock_DeleteOutline_18_N.svg) para remover um usuário.

   ![Adicionar usuários](assets/newrelic-add-users.png)

1. Clique em **Salvar**.

Depois que os usuários são definidos, o New Relic envia um email de confirmação para cada um. A partir daí, eles podem concluir o processo de ativação e fazer logon.

>[!NOTE]
>
>Se você estiver gerenciando os usuários do New Relic One, também deverá adicionar a si mesmo como usuário. Para ter acesso à New Relic One, não basta ter a função **Proprietário da empresa** ou **Gerente de implantação**.

## Ativar sua conta de usuário do New Relic One {#activate-user-account}

Depois que uma conta de usuário do New Relic One é criada, conforme descrito em [Gerenciar usuários do New Relic One](#manage-users), a New Relic envia a esses usuários um email de confirmação para o endereço fornecido. Para usar essas contas, os usuários devem primeiro ativar suas contas junto à New Relic, redefinindo suas senhas.

**Para ativar sua conta de usuário do New Relic One:**

1. Clique no link fornecido por email pelo New Relic.

1. Na página de entrada do New Relic, clique em **Esqueceu sua senha?**

   ![Logon na New Relic](/help/implementing/cloud-manager/assets/new-relic/newrelic-1.png)

1. Digite o endereço de email no qual você recebeu o email de confirmação e selecione **Enviar meu link de redefinição**.

   ![Inserir endereço de email](/help/implementing/cloud-manager/assets/new-relic/newrelic-2.png)

1. O New Relic envia um email contendo um link para confirmar a conta.

Se você não receber um email de confirmação da New Relic, consulte a [seção de solução de problemas](#troubshooting).

## Abrir New Relic One {#accessing-new-relic}

Depois de [ativar sua conta do New Relic](#activate-account), você poderá abrir o New Relic One diretamente ou através do Cloud Manager.

**Para abrir o New Relic One por meio do Cloud Manager:**

1. Entre no Cloud Manager em [experience.adobe.com](https://experience.adobe.com).
   1. Na seção **Acesso rápido**, clique em **Experience Manager**.
   1. No painel lateral esquerdo, clique em **Cloud Manager**.
1. Selecione a organização desejada.
1. No console **Meus Programas**, clique em um programa para o qual você deseja abrir o New Relic One.
1. No menu do lado esquerdo, em **Serviços**, clique em ![Ícone de dados ou em ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Data_18_N.svg) **Ambientes**.
1. Na página Ambientes, próximo ao canto superior direito, clique no ![ícone Mais](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) e em **Abrir o New Relic**.

   ![Abrir New Relic](/help/implementing/cloud-manager/assets/new-relic/new-relic-open-new-relic.png)

1. Na nova guia do navegador que é aberta, faça logon na New Relic One.

**Para abrir o New Relic One diretamente:**

1. Vá para a [página de logon do New Relic](https://login.newrelic.com/login).

1. Faça logon na New Relic One.

### Verificar seu email {#verify-email}

Se for solicitado que você verifique seu email ao fazer logon no New Relic One, significa que seu email está associado a várias contas. Você pode escolher qual conta acessar.

Se você não verificar seu endereço de email, a New Relic tentará fazer seu logon com o registro de usuário criado mais recentemente que esteja associado ao seu endereço de email. Para evitar a verificação do email em cada logon, clique na caixa de seleção **Lembrar-se de mim** na tela de logon.

Para obter mais ajuda, abra um tíquete de suporte por meio do [Portal de suporte do AEM](https://helpx.adobe.com/br/enterprise/using/support-for-experience-cloud.html).

## Usar o controle de alterações {#change-tracker}

O Cloud Manager envia automaticamente rastreadores de alterações para o New Relic One sempre que execuções de pipeline, atualizações de AEM e Restauração de código compatíveis forem concluídas. Esses rastreadores aparecem como eventos de alteração na visualização **Controle de alterações** da New Relic, permitindo que sua equipe correlacione implantações com mudanças no desempenho do aplicativo, nas taxas de erro e na taxa de transferência.

<!-- See also [Introduction to change tracking](https://docs.newrelic.com/docs/change-tracking/overview/) and [Record and view deployments](https://docs.newrelic.com/docs/apm/apm-ui-pages/events/record-deployments/). -->

### Pipelines e fluxos de trabalho compatíveis {#supported-pipelines}

Os seguintes pipelines de Cloud Manager e os dois últimos tipos de fluxo de trabalho geram rastreadores de alteração no New Relic One:

| Tipo de pipeline/fluxo de trabalho | Descrição |
|---|---|
| **Pilha completa (implantação de CI_CD)** | Execuções de pipeline de pilha completa. O rastreamento inclui o nome do pipeline e a ID de execução. |
| **Configuração da camada da Web** | Execuções de pipeline de configuração no nível da Web. O rastreamento inclui o nome do pipeline e a ID de execução. |
| **Front-end** | Execuções de pipeline de front-end. O rastreamento inclui o nome do pipeline e a ID de execução. |
| **Configuração** | Execuções de pipeline de configuração. O rastreamento inclui o nome do pipeline e a ID de execução. |
| **atualização do AEM** | Atualizações de versão do AEM. Por exemplo, da versão {} para a versão {}. Os rastreadores são criados quando o evento de alteração no ambiente é concluído. |
| **Restaurar código** | O código restaura operações de um repositório e ramificação específicos. |

>[!NOTE]
>
>Atualmente, os rastreadores de alterações são permitidos apenas em ambientes do Skyline. Os pipelines que estão fora do escopo, como pipelines de scale-up e service pack, não geram rastreadores.

### Exibir rastreadores de alterações no New Relic One {#view-change-trackers}

Depois que uma execução de pipeline compatível for concluída, você poderá exibir o rastreador de alterações correspondente no New Relic One.

**Para exibir os rastreadores de alterações no New Relic One:**

1. [Acesse o New Relic One](#accessing-new-relic) por meio do Cloud Manager ou diretamente.
1. Navegue até **APM e serviços** e selecione o aplicativo para o ambiente relevante.
1. Na página de resumo do aplicativo, procure por indicadores do rastreador de alterações no gráfico. Passe o mouse sobre um rastreador para ver os detalhes da implantação.

   ![Alterar indicadores do rastreador no gráfico de tempo de transações da Web](/help/implementing/cloud-manager/assets/new-relic/new-relic-web-transactions-time.png)

1. Clique em qualquer evento de alteração no gráfico para abrir uma exibição detalhada.

   ![Painel de atributos de implantação com a URL do deepLink realçada](/help/implementing/cloud-manager/assets/new-relic/new-relic-deeplink.png) <i>Exibição detalhada de um evento de alteração.</i>

   O painel **Detalhes da alteração** à direita mostra, entre outras coisas, a Entidade, o Carimbo de Data e Hora, a Época, a Categoria, a ID de Implantação e o tipo de API.

   Para cada rastreador de alterações enviado pelo Cloud Manager para o New Relic One, o painel **Atributos de implantação**, na parte inferior direita, mostra os seguintes atributos:

   | Atributo | Descrição |
   |---|---|
   | **versão** | Uma string de descrição que inclui o nome do pipeline e a ID de execução. |
   | **changelog** | Reservado para uso futuro. |
   | **confirmar** | Reservado para uso futuro. |
   | **deepLink** | Clique no URL para vincular novamente à página de execução do pipeline no Cloud Manager. |

1. Para exibir uma lista completa de rastreadores de alterações, na barra lateral esquerda, em **Eventos**, clique em **Controle de alterações**.

   A tabela **Eventos de alteração** mostra cada implantação com seu carimbo de data/hora e descrição da versão.

   ![Opção de controle de alterações com a tabela Alterar eventos sendo exibida](/help/implementing/cloud-manager/assets/new-relic/new-relic-change-tracking.png)

>[!TIP]
>
>Use rastreadores de alterações junto com indicadores de desempenho do New Relic One, como **Tempo de resposta** e **Taxa de transferência**. Esses indicadores ajudam a identificar se uma implantação específica apresentou regressões ou melhorias de desempenho. Você pode comparar métricas de antes e depois de uma implantação diretamente na página Detalhes do evento de alteração.

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
