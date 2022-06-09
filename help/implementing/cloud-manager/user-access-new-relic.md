---
title: Novo Relic One
description: Saiba mais sobre o serviço APM (New Relic One application performance monitoring) para AEM as a Cloud Service e como você pode acessá-lo.
exl-id: 9fa0c5eb-415d-4e56-8136-203d59be927e
source-git-commit: 09049213eaf92830dc0e0d4c0885017c69a5d56e
workflow-type: tm+mt
source-wordcount: '1622'
ht-degree: 1%

---


# Novo Relic One {#user-access}

Saiba mais sobre o serviço APM (New Relic One application performance monitoring) para AEM as a Cloud Service e como você pode acessá-lo.

## Introdução {#introduction}

O Adobe dá grande ênfase ao monitoramento, disponibilidade e desempenho de seu aplicativo. AEM as a Cloud Service fornece acesso a um novo conjunto de monitoramento personalizado do New Relic One como parte da oferta padrão de produtos para garantir que suas equipes tenham a máxima visibilidade de suas métricas de desempenho do ambiente e do sistema as a Cloud Service AEM.

Este documento descreve como gerenciar o acesso aos recursos de APM (New Relic One application performance monitoring) habilitados em seus ambientes AEM as a Cloud Service para ajudar a oferecer suporte ao desempenho e permitir que você aproveite ao máximo AEM as a Cloud Service.

Quando um novo programa de produção é criado, a subconta New Relic One associada ao seu AEM programa as a Cloud Service é criada automaticamente.

## Recursos {#transaction-monitoring}

O novo Relic One APM para AEM as a Cloud Service tem muitos recursos.

* Acesso direto a uma conta dedicada do Novo Relic One (acesso gerenciado pelo Adobe Support)

* Novo Relic Instrumentado Um agente APM que mostra chamadas exatas de método com números de linha, incluindo dependências externas e bancos de dados

* Otimização holística do desempenho ao combinar métricas principais do monitoramento de nível de infraestrutura e do monitoramento de aplicativos (Adobe Experience Manager)

* Exposição de AEM Mbeans JMX as a Cloud Service e verificações de integridade diretamente nas métricas do New Relic Insights, permitindo uma inspeção profunda do desempenho da pilha de aplicativos e das métricas de integridade.

## Gerenciar novos usuários do Relic One {#manage-users}

Siga estas etapas para definir os usuários da sua subconta New Relic One associada ao seu Programa AEM as a Cloud Service.

>[!NOTE]
>
>Um usuário em **Proprietário da empresa** ou **Gerenciador de implantação** deve estar conectado para gerenciar novos usuários do Relic One.

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização apropriada.

1. Clique no programa para o qual você deseja gerenciar seus novos usuários do Relic One.

1. Alterne para **Ambientes** do **Visão geral do programa** clicando na página **Ambientes** na parte superior da tela.

1. No **Ambientes** clique no botão de reticências na parte superior da tela, ao lado do **Adicionar ambiente** botão.

1. No menu reticências, clique em **Gerenciar usuários**.

   ![Gerenciar usuários](assets/newrelic-manage-users.png)

1. No **Gerenciar novos usuários do Relic** digite o nome e o sobrenome do usuário que deseja adicionar e clique no botão **Adicionar** botão. Repita essa etapa para todos os usuários que deseja adicionar.

   ![Adicionar usuários](assets/newrelic-add-users.png)

1. Para remover um novo Relic de um usuário, clique no botão Excluir na extremidade direita da linha que representa o usuário.

1. Clique em **Salvar** para criar os usuários.

Depois que os usuários são definidos, o Novo Relic envia um email de confirmação para cada usuário ao qual você concedeu acesso, para que o usuário possa concluir o processo de configuração e fazer logon.

>[!NOTE]
>
>Se você estiver gerenciando os novos usuários do Relic One, também deverá se adicionar como usuário para ter acesso. Ser o **Proprietário da empresa** ou **Gerenciador de implantação** não é suficiente para ter acesso ao Novo Relic One. Você também deve criar a si mesmo como um usuário.

## Ative sua nova conta de usuário do Relic One {#activate-account}

Depois que uma conta de usuário Novo Relic Um é criada conforme descrito na seção de visualização [Gerenciar novos usuários do Relic One](#manage-users), o New Relic envia a esses usuários um email de confirmação para o endereço fornecido. Para usar essas contas, os usuários devem primeiro ativar suas contas com o Novo Relic, redefinindo suas senhas.

Siga estas etapas para ativar sua conta como um novo usuário do Relic.

1. Clique no link fornecido no email de New Relic. Isso abre seu navegador para a página de logon Novo Relic .

1. Na página de logon Novo Relic , selecione **Esqueceu sua senha?**.

   ![Novo logon do Relic](/help/implementing/cloud-manager/assets/new-relic/newrelic-1.png)

1. Digite o endereço de email para onde você recebeu o email de confirmação e selecione **Enviar meu link de redefinição**.

   ![Inserir endereço de email](/help/implementing/cloud-manager/assets/new-relic/newrelic-2.png)

1. O New Relic lhe enviará um email contendo um link para confirmar a conta.

Se você não receber um email de confirmação do New Relic, consulte o [seção solução de problemas .](#troubshooting)

## Acessar o novo Relic One {#accessing-new-relic}

Depois de [Ativação da sua conta New Relic,](#activate-account) você pode acessar o Novo Relic One pelo Cloud Manager ou diretamente.

Para acessar o Novo Relic One via Cloud Manager:

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização apropriada.

1. Clique no programa para o qual você deseja acessar o Novo Relic One.

1. Alterne para **Ambientes** do **Visão geral do programa** clicando na página **Ambientes** na parte superior da tela.

1. No **Ambientes** clique no botão de reticências na parte superior da tela, ao lado do **Adicionar ambiente** botão.

1. No menu reticências, clique em **Abrir Novo Relic**.

1. Na nova guia do navegador que é aberta, faça logon no Novo Relic One.

Para acessar o Novo Relic One diretamente:

1. Navegue até a página de logon do Novo Relic em [`https://login.newrelic.com/login`](https://login.newrelic.com/login)

1. Faça logon no Novo Relic One.

### Verificar seu email {#verify-email}

Se for solicitado que você verifique seu email durante o logon no Novo Relic One, significa que seu email está associado a várias contas. Isso permite escolher qual conta acessar.

Se você não verificar seu endereço de email, o New Relic tentará fazer logon com o registro de usuário criado mais recentemente associado ao seu endereço de email. Para evitar a verificação do email durante cada logon, clique no botão **Lembre-se de mim** na tela de logon.

Para obter mais ajuda, abra um tíquete de suporte pelo [Portal de suporte AEM](https://helpx.adobe.com/br/enterprise/using/support-for-experience-cloud.html).

## Solução de problemas de novo acesso em linha única {#troubleshooting}

Se você foi adicionado como um novo usuário do Relic One, conforme descrito na seção [Gerenciar novos usuários do Relic One](#manage-users) e não é possível localizar o email de confirmação da conta original siga essas etapas.

1. Navegue até a página de logon do Novo Relic em [`login.newrelic.com/login`](https://login.newrelic.com/login).

1. Selecionar **Esqueceu sua senha?**.

   ![Novo logon do Relic](/help/implementing/cloud-manager/assets/new-relic/newrelic-1.png)

1. Digite o endereço de email usado para criar sua conta e selecione **Enviar meu link de redefinição**.

   ![Inserir endereço de email](/help/implementing/cloud-manager/assets/new-relic/newrelic-2.png)

1. O New Relic lhe enviará um email contendo um link para confirmar a conta.

Se você concluir o processo de inscrição e não conseguir fazer logon em sua conta devido a mensagens de erro de email ou senha, registre um tíquete de suporte por meio do [Admin Console.](https://adminconsole.adobe.com/)

Se você não receber um email do New Relic:

* Verifique sua [filtros de spam](https://docs.newrelic.com/docs/accounts/accounts-billing/account-setup/create-your-new-relic-account/).
* Se aplicável, [adicionar novo link à sua lista de permissões de email](https://docs.newrelic.com/docs/accounts/accounts/account-maintenance/account-email-settings/#email-whitelist).
* Se nenhuma das sugestões ajudar, forneça feedback sobre o tíquete de suporte e a equipe de suporte do Adobe ajudará você ainda mais.

## Limitações           {#limitations}

As seguintes limitações se aplicam à adição de usuários ao Novo Relic One:

* É possível adicionar no máximo 25 usuários. Se o número máximo de usuários tiver sido atingido, remova os usuários para poder adicionar novos usuários.
* Os usuários adicionados ao Novo Relic serão do tipo **Restrito** consulte [a documentação do New Relic para obter detalhes.](https://docs.newrelic.com/docs/accounts/original-accounts-billing/original-users-roles/users-roles-original-user-model/#:~:text=In%20general%2C%20Admins%20take%20responsibility,Restricted%20Users%20can%20use%20them.&amp;text=One%20or%20more%20individuals%20who,change)%20any%20New%20Relic%20features.)
* AEM as a Cloud Service oferece apenas a solução Nova versão em um APM e não oferece suporte para alertas, registros ou integrações de API.

Para obter mais ajuda ou orientação adicional sobre as ofertas do Novo Relic One para o seu Programa as a Cloud Service AEM, abra um tíquete de suporte via [Portal de suporte AEM](https://helpx.adobe.com/enterprise/using/support-for-experience-cloud.html).

## Perguntas Frequentes Sobre O Novo Relic One {#faqs}

### O que o Adobe monitora com o Novo Relic One? {#adobe-monitor}

O Adobe monitora os serviços de criação, publicação e visualização AEM as a Cloud Service (quando disponíveis) por meio do plug-in Java do New Relic One. O Adobe permite a telemetria e o monitoramento personalizados do New Relic One APM em ambientes de não produção e produção AEM as a Cloud Service.

Sua conta New Relic One é anexada a uma conta Adobe principal mantida e tem vários aplicativos reportando nela: três por AEM ambiente as a Cloud Service.

* Um aplicativo para o serviço de criação por ambiente
* Um aplicativo para o serviço de publicação por ambiente (incluindo o Golden Publish)
* Um aplicativo para o serviço de visualização por ambiente

Observação:

* Cada aplicativo usa uma chave de licença.
* AEM ambientes as a Cloud Service reportam-se a apenas uma conta do Novo Relic One.
* Métricas e eventos de monitoramento completo do Novo Relic One são retidos por sete dias.

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
