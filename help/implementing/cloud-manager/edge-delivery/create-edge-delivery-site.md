---
title: Crie seu primeiro site do Edge Delivery com um clique
description: Saiba como criar um site do Edge Delivery rapidamente no Cloud Manager com apenas um clique.
feature: Cloud Manager, Developing
role: Admin, Developer
exl-id: 292bf0b4-990b-4980-b971-91b8aedde3de
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '945'
ht-degree: 0%

---

# Crie seu primeiro site do Edge Delivery com um clique{#about-one-click-edge-delivery-site}

A criação do seu primeiro site do Edge Delivery com um clique foi projetada para ajudar a automatizar a integração e a implantação de sites do Edge Delivery no Cloud Manager. Ele simplifica bastante o processo, fazendo você clicar em um único botão. Esse clique único provisiona a infraestrutura necessária, integra-se ao GitHub para controle de versão e configura o armazenamento de documentos e ativos no Google Drive.

Essa automação ajuda a reduzir o esforço manual necessário para configurar o site inicial. Ele garante fluxos de trabalho perfeitos, escalabilidade e melhora o desempenho de suas equipes quando se trata de gerenciar conteúdo na borda.

<!-- Check out this quick 2-minute video for a step-by-step walkthrough on creating your first Edge Delivery site—no hassle, just one click.

>[!VIDEO](https://video.tv.adobe.com/v/3458975?quality=12&learn=on) -->



<!--
## Practical use cases {#use-cases}

| Use case | Description |
| --- | --- |
| Website and application deployment | <ul><li>Automate the hosting and delivery of static or dynamic sites.</li><li>Ensure fast performance through edge caching. </li></ul> |
| API gateway and content delivery | <ul><li>Optimize API responses by caching data at the edge.</li><li>Reduce backend load and improved response times. </li></ul> |
| Real-time content updates | <ul><li>Instant deployment of new content across edge locations.</li><li>Support integration with automated content pipelines. </li></ul> |
| Edge computing workloads | <ul><li>Support serverless computing to process workloads closer to users.</li><li>Reduce latency and enhance performance. </li></ul> |
| Security and governance | <ul><li>Security is provided with integrated DDoS (Distributed Denial of Service) protection and WAF (Web Application Firewall) integration.</li><li>Ensure that content is delivered securely through TLS (Transport Security Layer) encryption. </li></ul> |
-->





## Crie um site do Edge Delivery no Cloud Manager com um clique {#one-click-edge-delivery-site}

Para criar um site do Adobe Edge Delivery com um clique, sua organização deve ter uma licença da Edge Delivery Services disponível. Esta licença faz parte do Adobe Experience Manager (AEM) e é necessária para criar o Edge Delivery Services no Cloud Manager.

Em termos de permissões, você deve ser membro da função Proprietário da empresa ou ter recebido as permissões apropriadas para adicionar ou editar programas no Cloud Manager. Esse nível de acesso permite gerenciar a integração do Edge Delivery Services em seus programas.

Consulte também [Introdução ao Edge Delivery Services no Cloud Manager](/help/implementing/cloud-manager/edge-delivery/introduction-to-edge-delivery-services.md).

<!-- PROPER AEM BOT CONFIGURATIONS MUST BE IN PLACE FIRST FOR AUTOMATIC CONTENT UPDATES? TRUE or FALSE? -->

**Para criar um site do Edge Delivery no Cloud Manager com um clique:**

1. Faça logon no Cloud Manager em [`https://my.cloudmanager.adobe.com`](https://my.cloudmanager.adobe.com/) e selecione o programa apropriado.
1. No canto superior esquerdo da página, clique em ![Mostrar ícone de menu](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) para exibir o menu do lado esquerdo.
1. No menu do lado esquerdo, no cabeçalho **Programa**, clique em **Visão geral**.
1. Na página **Visão Geral do Programa**, clique na guia **Edge Delivery**.
1. Na página do Edge Delivery, na caixa de diálogo **Lista de tarefas do Edge Delivery**, na caixa de grupo **Adicionar site do Edge Delivery**, clique em **Criar site agora**.
1. Na caixa de diálogo **Criar site do Edge Delivery**, no campo de texto **Nome do Projeto**, digite o nome do site e clique em **Criar site agora**.

   Uma janela aparece perto do centro superior da tela informando que o provisionamento do site do Edge Delivery foi iniciado.

Quando o provisionamento e a validação do site são concluídos pelo Cloud Manager, o **Nome do site** (o nome do projeto inserido anteriormente) aparece na caixa de listagem **Sites do Edge Delivery** na página do Edge Delivery. Além disso, uma marca de seleção verde é exibida à esquerda do URL do repositório.


### Explore um site do Edge Delivery criado com um clique {#explore-one-click-ed-site}

1. Faça logon no Cloud Manager em [`https://my.cloudmanager.adobe.com`](https://my.cloudmanager.adobe.com/) e selecione o programa apropriado.
1. No canto superior esquerdo da página, clique em ![Mostrar ícone de menu](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) para exibir o menu do lado esquerdo.
1. No menu do lado esquerdo, no cabeçalho **Programa**, clique em **Visão geral**.
1. Na página **Visão Geral do Programa**, clique na guia **Edge Delivery**.
1. Na página do Edge Delivery, siga um destes procedimentos:

   | O que explorar | Etapas |
   | --- | --- |
   | Repositório GitHub de um site | <ul><li>Na caixa de listagem **Sites do Edge Delivery**, no cabeçalho de coluna **Repositório**, clique na URL do site que você acabou de criar.<br>Talvez seja necessário entrar no GitHub com seu nome de usuário ou endereço de email e sua senha.</li> |
   | Publicar um site | <ul><li> Na caixa de listagem **Sites do Edge Delivery**, na extremidade direita do nome do site, clique em ![ícone Mais](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) para abrir o menu suspenso.</li><li>Clique em ![Ícone Publicar Verificação](https://spectrum.adobe.com/static/icons/workflow_18/Smock_PublishCheck_18_N.svg) **Publicar site** no menu suspenso.<br>Uma mensagem em caixa de informações é exibida informando que a publicação do site foi iniciada com êxito.</li></ul> |
   | Visualizar um site publicado | <ul><li>Na caixa de listagem **Sites do Edge Delivery**, no cabeçalho de coluna **Nome do site**, clique na URL do site que você acabou de criar e publicar.<br>Na barra de Endereços de URL do seu navegador, observe que a URL do site termina com `.page`, indicando que você está visualizando uma visualização do site.</li><li>Para ver o site ativo, altere manualmente `.page` para `.live` na barra de Endereços de URL.</li></ul> |
   | Conceda aos usuários acesso ao repositório de conteúdo no Google Drive | <ul><li> Na caixa de listagem **Sites do Edge Delivery**, na extremidade direita do nome do site, clique em ![ícone Mais](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) para abrir o menu suspenso.</li><li>Clique em ![Ícone Adicionar usuários](https://spectrum.adobe.com/static/icons/workflow_18/Smock_UsersAdd_18_N.svg) **Obter acesso ao repositório de conteúdo** no menu suspenso.</li><li>Na caixa de diálogo **Adicionar colaboradores ao site**, digite o endereço de email de um colaborador e clique em ![Ícone de marca de seleção](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Checkmark_18_N.svg).</li><li>Continue adicionando emails do colaborador, conforme necessário.</li><li>Quando terminar, clique em **Adicionar colaboradores**.</li><li>Para compartilhar o link com seus colaboradores de conteúdo, na caixa de diálogo **Collaboration adicionado com êxito**, clique em **OK**.</li><li>Na caixa de diálogo Collaboration adicionada com êxito, clique em ![Ícone Copiar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg) para copiar o link e compartilhá-lo com seus colaboradores.<br>Antes de compartilhar o link, confirme se os colaboradores estão conectados com o endereço de email associado à sua conta IMS. Se a conta de email IMS não estiver disponível, ele deverá usar o endereço de email adicionado como colaborador. Isso garante que os colaboradores possam acessar o link e ver o conteúdo a ser editado ou atualizado no Google Drive.</li><li>Quando terminar a edição, clique em **Publicar site** no Cloud Manager, conforme descrito acima.<br>Ou visualize as alterações feitas, conforme descrito acima.</li></ul> |
   | Conceda aos usuários acesso ao repositório básico no GitHub | <ul><li> Na caixa de listagem **Sites do Edge Delivery**, na extremidade direita do nome do site, clique em ![ícone Mais](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) para abrir o menu suspenso.</li><li>Clique em ![Ícone do código](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Code_18_N.svg) **Obter acesso ao repositório base** no menu suspenso.</li><li>Na caixa de diálogo **Acessar o repositório base do seu site**, digite o nome de usuário do GitHub de um colaborador e clique em ![Ícone de marca de seleção](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Checkmark_18_N.svg).</li><li>Continue adicionando nomes de usuário do GitHub, conforme necessário.</li><li>Quando terminar, clique em **Adicionar colaboradores**.</li>Os usuários devem conceder acesso a seu próprio nome de usuário do GitHub para visualizar o repositório. |
