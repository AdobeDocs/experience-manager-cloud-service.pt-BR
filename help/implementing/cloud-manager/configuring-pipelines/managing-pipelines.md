---
title: Gerenciar pipelines
description: Saiba como gerenciar os pipelines existentes, incluindo edição, execução e exclusão.
index: true
exl-id: 4aff5a84-134a-43fa-8de8-8d564f4edd16
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 500e1b78fb9688601848fc17f312fc23be83bcb0
workflow-type: tm+mt
source-wordcount: '1109'
ht-degree: 69%

---


# Gerenciar pipelines {#managing-pipelines}

Saiba como gerenciar os pipelines existentes, incluindo edição, execução e exclusão.

## Cartão Pipelines {#pipeline-card}

O cartão **Pipelines** na página **Visão geral do programa** no Cloud Manager fornece uma visão geral de todos os seus pipelines e seu status atual.

![Cartão Pipelines no Cloud Manager](/help/implementing/cloud-manager/assets/configure-pipeline/pipelines-card.png)

Ao clicar no botão de reticências ao lado de cada pipeline, você pode realizar as ações a seguir.

* [Executar o pipeline](#running-pipelines)
* [Editar o pipeline](#editing-pipelines)
* [Excluir o pipeline](#deleting-pipelines)
* [Exibir detalhes](#view-details)

Na parte inferior da lista de pipelines, você tem opções gerais.

* **Adicionar** - Para [adicionar um novo pipeline de produção](configuring-production-pipelines.md) ou [de não produção](configuring-non-production-pipelines.md).
* **Mostrar tudo** - Leva o usuário à tela Pipelines para exibir todos os pipelines em uma tabela mais detalhada.
* **Acessar informações do repositório** - Exibe as informações necessárias para acessar o repositório Git do Cloud Manager.
* **Saiba mais** - Navega até os recursos de documentação do pipeline de CI/CD.

## Janela Pipelines {#pipelines}

A janela **Pipelines** mostra uma lista completa de todos os pipelines do programa selecionado. Permite visualizar informações mais abrangentes que as disponíveis no [cartão do pipeline](#pipeline-card).

1. Faça logon no Cloud Manager, em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/), e selecione a organização apropriada.

1. No console **[Meus Programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, selecione o programa.

1. Na página **Visão geral do programa**, selecione a guia **Pipelines** para alternar para a janela **Pipelines**.

1. Nessa janela você pode ver uma lista de todos os pipelines do programa, bem como iniciar e parar a execução do pipeline, assim como no **cartão do pipeline**.

Se um pipeline estiver em execução, clicar no ícone de informações na coluna **Status** revelará detalhes sobre a execução.

![Detalhes da execução do pipeline](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-status.png)

Clicar em **Exibir detalhes** mostrará os [detalhes da execução do pipeline](#view-details).

Você também pode clicar no botão de reticências do pipeline para realizar ações adicionais apropriadas ao estado do pipeline, como [editá-lo](#editing-pipelines) ou [cancelar a execução](#cancel).

![Ações de pipeline](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-actions.png)

## Janela Atividade {#activity}

A janela **Atividade** mostra uma lista completa de todas as execuções de pipelines para o programa selecionado, bem como outros eventos importantes do programa.

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriados.

1. Na página **Visão geral do programa**, selecione a guia **Atividade** para alternar para a janela **Atividade**.

1. Aqui você pode ver uma lista de todas as execuções de pipeline do programa, incluindo as execuções atuais e históricas.

Se um pipeline estiver em execução, clicar no ícone de informações na coluna **Status** revelará detalhes sobre a execução.

![Detalhes da execução do pipeline](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-activity.png)

Tocar ou clicar na linha que representa a execução do pipeline leva você aos [detalhes da execução do pipeline](#view-details).

Você também pode clicar no botão de reticências para realizar outras ações na execução do pipeline, como exibir seus detalhes ou baixar o log, o que leva você à [página de detalhes do pipeline](#view-details).

![Ações de execução do pipeline](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-execution-actions.png)

## Execução de pipelines {#running-pipelines}

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriados.

1. Navegue até o cartão **Pipelines** da página **Visão geral do programa**, clique no botão de reticências ao lado do pipeline a ser executado e selecione **Executar** no menu.

1. A execução do pipeline começa e é indicada pela coluna **Status**.

Você pode ver os detalhes da execução clicando no botão de reticências novamente e selecionando **[Exibir detalhes](#view-details)**.

Dependendo do tipo de pipeline, talvez seja possível cancelar a execução clicando no botão de reticências novamente e selecionando **Cancelar**.

## Editar um pipeline {#editing-pipelines}

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriados.

1. Navegue até o cartão **Pipelines** da página **Visão geral do programa**, clique no botão de reticências ao lado do pipeline que deseja editar e selecione **Editar** no menu.

1. A caixa de diálogo **Editar pipeline de produção** ou **Editar pipeline de não produção** é exibida, permitindo editar os mesmos detalhes inseridos ao criar o pipeline.

   * Consulte as páginas a seguir para obter detalhes sobre os campos e as opções de configuração disponíveis para pipelines.
      * [Configuração de pipelines de produção](configuring-production-pipelines.md)
      * [Configurar pipelines de não produção](configuring-non-production-pipelines.md)

1. Clique em **Atualizar** quando concluir a edição do pipeline.

>[!NOTE]
>
>Não é possível editar um pipeline em execução.

>[!NOTE]
>
>Os pipelines de nível da Web e de configuração não são compatíveis com repositórios privados. Consulte [Adicionar um repositório privado no Cloud Manager](/help/implementing/cloud-manager/managing-code/private-repositories.md) para obter detalhes e a lista completa de limitações.

## Exclusão de pipelines {#deleting-pipelines}

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriados.

1. Navegue até o cartão **Pipelines** da página **Visão geral do programa**, clique no botão de reticências ao lado do pipeline a ser executado e selecione **Excluir** no menu.

>[!NOTE]
>
>Não é possível excluir um pipeline em execução.

## Exibir detalhes do pipeline {#view-details}

Você pode visualizar os detalhes de um pipeline para ver o status e os logs da última execução.

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriados.

1. Navegue até o cartão **Pipelines** da página **Visão geral do programa**, clique no botão de reticências ao lado do pipeline a ser executado e selecione **Exibir detalhes** no menu.

1. Você será levado à página de detalhes do pipeline em execução.

![Detalhes do pipeline](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-running-details.png)

Aqui, você pode ver o status das várias etapas do pipeline e recuperar registros de compilação para fins de diagnóstico. Consulte o documento [Implantando seu código](/help/implementing/cloud-manager/deploy-code.md) para obter mais informações sobre a implantação de código e a execução de testes.

Ao exibir todas as etapas de uma execução de pipeline, as que ainda não foram iniciadas aparecem esmaecidas. As etapas concluídas exibem sua duração.

Quando uma etapa do pipeline é concluída, um resumo é apresentado.

![Resumo da etapa](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-step.png)

Selecione o link **Exibir detalhes** para revelar a seção **Duração**. Isso inclui a duração média do pipeline com base na tendência histórica desse programa.

![Duração](/help/implementing/cloud-manager/assets/configure-pipeline/duration.png)

Se o pipeline tiver uma etapa de **Varredura de código** que gerou problemas, toque ou clique no botão **Detalhes de download** para exibir uma lista de [testes de qualidade do código](/help/implementing/cloud-manager/code-quality-testing.md) não aprovados.

![Problemas de qualidade do código](assets/managing-pipelines-code-quality-issues.png)

Uma coluna **Localização do arquivo do projeto** está disponível no arquivo CSV para indicar a localização do código incorreto. Essa coluna é o caminho relativo do projeto, enquanto a coluna **Localização do arquivo** é gerada pelo Maven.

![Detalhes do problema de verificação do código do projeto](assets/managing-pipelines-code-quality-details.png)

>[!NOTE]
>
>Só é possível exibir detalhes de um pipeline que está em execução ou que foi executado pelo menos uma vez.

## Cancelar pipelines {#cancel}

Se um pipeline estiver na fase de validação ou criação de imagem, você poderá cancelar com segurança a execução do pipeline.

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriados.

1. Na página de visão geral do programa, clique no botão de reticências do pipeline que deseja cancelar no cartão **Pipelines**.

   ![Cancelando um pipeline](/help/implementing/cloud-manager/assets/cancel-pipeline.png)

1. Selecione **Cancelar**.

Como alternativa, você pode cancelar um pipeline na página de detalhes do pipeline.

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriados.

1. Navegue até a guia **Pipelines** da página **Visão geral do programa** e selecione o pipeline que deseja cancelar.

1. Você será levado à página de detalhes do pipeline em execução.

   ![Cancelar detalhes do pipeline](/help/implementing/cloud-manager/assets/cancel-pipeline-details.png)

1. Selecione **Cancelar**.
