---
title: Gerenciar pipelines
description: Saiba como gerenciar os pipelines existentes, incluindo edição, execução e exclusão.
index: true
exl-id: 4aff5a84-134a-43fa-8de8-8d564f4edd16
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1493'
ht-degree: 27%

---


# Gerenciar pipelines {#managing-pipelines}

Saiba como gerenciar os pipelines existentes, incluindo edição, execução e exclusão.

## Cartão do pipeline {#pipeline-card}

O cartão **Pipelines** na página **Visão geral do programa** no Cloud Manager fornece uma visão geral de todos os seus pipelines e seu status atual.

![Cartão Pipelines no Cloud Manager](/help/implementing/cloud-manager/assets/configure-pipeline/pipelines-card.png)

Ao clicar em ![Reticências - ícone Mais](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) ao lado de cada pipeline, você pode realizar as seguintes ações:

* [Executar um pipeline](#running-pipelines)
* [Cancelar um pipeline](#cancel)
* [Editar um pipeline](#editing-pipelines)
* [Excluir um pipeline](#deleting-pipelines)
* [Exibir detalhes da última execução de um pipeline](#view-details)

Na parte inferior da lista de pipelines, você tem as seguintes opções gerais:

* **Adicionar** - A [adicionar um novo pipeline de produção](configuring-production-pipelines.md) ou [adicionar um novo pipeline de não produção](configuring-non-production-pipelines.md)
* **Mostrar tudo** - Leva o usuário à tela Pipelines para exibir todos os pipelines em uma tabela mais detalhada.
* **Acessar informações do repositório** - Exibe as informações necessárias para acessar o repositório Git do Cloud Manager.
* **Saiba mais** - Navega até os recursos de documentação do pipeline de CI/CD.

## Página Pipelines {#pipelines}

A página **Pipelines** mostra uma lista completa de todos os pipelines do programa selecionado. Essas informações são úteis porque apresentam informações mais abrangentes do que as disponíveis no [Cartão do pipeline](#pipeline-card).

1. Faça logon no Cloud Manager, em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/), e selecione a organização apropriada.

1. No console **[Meus Programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, selecione o programa.

1. Na página **Visão geral do programa**, clique na guia ![Pipeline - ícone do fluxo de trabalho](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Workflow_18_N.svg) **Pipelines**.

1. Na página **Pipelines**, você pode ver uma lista de todos os pipelines do programa e iniciar e parar a execução do pipeline como faria no **Cartão Pipelines**.

Se um pipeline estiver em execução, clique em ![Informações - ícone de mídia](https://spectrum.adobe.com/static/icons/ui_18/InfoMedium.svg) na coluna **Status** para exibir um pop-up com detalhes sobre a execução. Na janela pop-up, clique em **Exibir detalhes** para ver os [detalhes da execução do pipeline](#view-details).

![Detalhes da execução do pipeline](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-status.png)


Você também pode clicar em ![Reticências - Mais ícone](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) ao lado do pipeline para realizar ações adicionais apropriadas ao estado do pipeline, como [editá-lo](#editing-pipelines) ou [cancelar a execução](#cancel).

![Ações de pipeline](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-actions.png)

### Marcar favoritos do pipeline{#pipeline-favorites}

Você pode marcar pipelines específicos como favoritos para que eles apareçam no topo da lista na página **Pipelines**. Essa capacidade facilita a localização e a execução de pipelines acessados com frequência.

**Para marcar os favoritos do pipeline:**

1. Faça logon no Cloud Manager, em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/), e selecione a organização apropriada.
1. No console **[Meus Programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, selecione o programa.
1. Na página **Visão geral do programa**, clique na guia ![Pipeline - ícone do fluxo de trabalho](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Workflow_18_N.svg) **Pipelines**.
1. Na página Pipelines, à esquerda de um nome e tipo de pipeline, clique em ![Ícone de estrutura de tópicos de estrelas para o pipeline desmarcado](https://spectrum.adobe.com/static/icons/workflow_18/Smock_StarOutline_18_N.svg) para adicioná-lo à lista de favoritos.
Como alternativa, clique em ![Ícone de estrela para um pipeline favorito](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Star_18_N.svg) para remover o pipeline da sua lista de favoritos.


## Página Atividade {#activity}

A página **Atividade** mostra uma lista completa de todas as execuções de pipelines para o programa selecionado e outros eventos importantes do programa.

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriados.

1. Na página **Visão geral do programa**, no menu lateral, clique em ![Ícone de Campainha](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Bell_18_N.svg) **Atividade**.

1. Na página **Atividade**, você pode ver uma lista de todas as execuções de pipeline do programa, incluindo as execuções atuais e históricas.

Se um pipeline estiver em execução, você poderá clicar em ![Informações - ícone de mídia](https://spectrum.adobe.com/static/icons/ui_18/InfoMedium.svg) na coluna **Status** para exibir um pop-up com informações sobre a execução.

![Detalhes da execução do pipeline](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-activity.png)

Clique na linha que representa a execução do pipeline para exibir os [detalhes da execução do pipeline](#view-details).

Você também pode clicar em ![Reticências - Mais ícone](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) para realizar ações adicionais na execução do pipeline, como exibir seus detalhes ou baixar o log, o que o levará à [página de detalhes do pipeline](#view-details).

![Ações de execução do pipeline](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-execution-actions.png)

## Executar um pipeline {#running-pipelines}

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriados.

1. Navegue até o cartão **Pipelines** na página **Visão geral do programa**.

1. Clique em ![Reticências - ícone Mais](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) ao lado do pipeline que você está executando.

1. No menu suspenso, clique em ![Executar - Ícone Reproduzir](https://spectrum.adobe.com/static/icons/workflow_18/Smock_PlayCircle_18_N.svg) **Executar**.

   A execução do pipeline é iniciada e a coluna **Status** exibe seu progresso.

Você pode ver os detalhes da execução clicando em ![Reticências - Mais ícone](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) novamente e clicando em **[Exibir detalhes](#view-details)**.

Dependendo do tipo de pipeline, talvez seja possível cancelar a execução clicando em ![Reticências - Mais ícone](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) novamente e clicando em **Cancelar**.

## Executar vários pipelines {#run-multiple-pipelines}

Com o Cloud Manager, você pode executar vários pipelines simultaneamente, melhorando a eficiência da implantação para clientes do AEM as a Cloud Service. O recurso **Executar selecionados** permite selecionar vários pipelines e acioná-los para execução simultânea. Ele reduz o esforço manual de execução de pipelines individualmente e otimiza os fluxos de trabalho de criação e implantação.

**Para executar vários pipelines:**

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriados.
1. No menu do lado esquerdo, clique em ![Ícone do fluxo de trabalho &#x200B;](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Workflow_18_N.svg) **Pipelines**.
1. Na tabela na página **Pipeline**, marque as caixas de seleção ao lado dos pipelines que deseja executar.
Se necessário, clique em ![Ícone de filtro, funnel](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Filter_18_N.svg) **Filtros** para classificar pipelines por nome, ambiente ou tipo de código implantado, ou uma combinação dos três.
1. Ao lado do canto superior direito da página, clique em **Executar selecionados (x)**.
1. Na caixa de diálogo **Executar pipelines selecionados (x)**, clique em **Executar (x)**.

   O botão **Executar** reflete o número de pipelines que podem continuar. Por exemplo, você pode ter selecionado quatro pipelines, mas um já está em execução. Ou um ambiente vinculado a um pipeline selecionado não existe mais. Nesses casos, o sistema se ajusta de acordo. O botão é atualizado para &quot;Executar (3)&quot; para indicar que três pipelines podem continuar.

1. Os pipelines começam a ser executados e seu status é atualizado na lista **Pipelines**.

## Editar um pipeline {#editing-pipelines}

Você pode editar um pipeline se ele não estiver em execução.

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriados.

1. Navegue até o cartão **Pipelines** na página **Visão geral do programa**.

1. Clique em ![Reticências - ícone Mais](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) ao lado do pipeline que você deseja editar.

1. No menu suspenso, clique em **Editar**.

1. Na caixa de diálogo **Editar Pipeline de Produção** ou **Editar Pipeline de Não Produção**, edite os mesmos detalhes inseridos ao criar o pipeline.

   Consulte as páginas a seguir para obter detalhes sobre os campos e as opções de configuração disponíveis para pipelines.
   * [Configurar um pipeline de produção](configuring-production-pipelines.md)
   * [Configurar um pipeline de não produção](configuring-non-production-pipelines.md)

1. Quando terminar, clique em **Atualizar**.

>[!NOTE]
>
>Os pipelines de nível da Web e de configuração não são compatíveis com repositórios privados. Consulte [Adicionar um repositório GitHub privado no Cloud Manager](/help/implementing/cloud-manager/managing-code/private-repositories.md) para obter detalhes e a lista completa de limitações.

## Excluir um pipeline {#deleting-pipelines}

Você pode excluir um pipeline se ele não estiver em execução.

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriados.

1. Navegue até o cartão **Pipelines** na página **Visão geral do programa**.

1. Clique em ![Reticências - ícone Mais](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) ao lado do pipeline que você está executando.

1. No menu suspenso, clique em **Excluir**.


## Exibir detalhes da última execução de um pipeline {#view-details}

Você pode verificar os detalhes de um pipeline para visualizar o status e os logs de sua execução mais recente. No entanto, você só poderá acessar os detalhes se o pipeline estiver em execução ou tiver sido executado pelo menos uma vez.

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriados.

1. Navegue até o cartão **Pipelines** na página **Visão geral do programa**.

1. No menu suspenso, clique em ![Reticências - ícone Mais](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) ao lado do pipeline que você está executando.

1. No menu suspenso, clique em **Exibir última execução**.

   Você será levado à página de detalhes do pipeline em execução.

   ![Detalhes do pipeline](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-running-details.png)

   Aqui, você pode ver o status das várias etapas do pipeline e recuperar logs de build para fins de diagnóstico. Consulte [Implantar Código](/help/implementing/cloud-manager/deploy-code.md) para obter mais informações sobre implantação de código e execução de testes.

   Ao exibir todas as etapas de uma execução de pipeline, as que ainda não foram iniciadas aparecem esmaecidas. As etapas concluídas exibem sua duração.

   Após a conclusão de uma etapa do pipeline, um resumo é apresentado.

   ![Resumo da etapa](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-step.png)

1. Clique em **Exibir detalhes** para expandir a seção **Duração**, na qual você pode ver a duração média do pipeline com base nas tendências históricas do programa.

   ![Duração](/help/implementing/cloud-manager/assets/configure-pipeline/duration.png)

1. Se seu pipeline incluiu uma etapa de **Verificação de código** que sinalizou problemas, clique em **Detalhes do Download** para acessar uma lista de [testes de qualidade do código](/help/implementing/cloud-manager/code-quality-testing.md) que falharam ao serem aprovados.

   ![Problemas de qualidade do código](assets/managing-pipelines-code-quality-issues.png)

   O arquivo CSV inclui uma coluna **Localização do Arquivo do Projeto**, mostrando o caminho para o código problemático relativo ao projeto. Por outro lado, a coluna **Localização do arquivo** reflete o caminho gerado pelo Maven.

   ![Detalhes do problema de verificação do código do projeto](assets/managing-pipelines-code-quality-details.png)

## Cancelar um pipeline {#cancel}

Você pode cancelar com segurança a execução do pipeline se ele estiver na fase de validação ou criação de imagem.

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriados.

1. Na página de visão geral do programa, clique em ![Reticências - Mais ícone](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) do pipeline que você deseja cancelar no cartão **Pipelines**.

   ![Cancelando um pipeline](/help/implementing/cloud-manager/assets/cancel-pipeline.png)

1. Clique em **Cancelar**.

Como alternativa, você pode cancelar um pipeline na página de detalhes do pipeline.

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriados.

1. Navegue até a guia ![Pipelines - Ícone do fluxo de trabalho](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Workflow_18_N.svg) guia **Pipelines** da página **Visão geral do programa** e selecione o pipeline que deseja cancelar.

   Você será levado à página de detalhes do pipeline em execução.

   ![Cancelar detalhes do pipeline](/help/implementing/cloud-manager/assets/cancel-pipeline-details.png)

1. Clique em **Cancelar**.

