---
title: Gerenciar pipelines
description: Saiba como gerenciar os pipelines existentes, incluindo edição, execução e exclusão.
index: true
exl-id: 4aff5a84-134a-43fa-8de8-8d564f4edd16
source-git-commit: a3e79441d46fa961fcd05ea54e84957754890d69
workflow-type: tm+mt
source-wordcount: '952'
ht-degree: 46%

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

A variável **Pipelines** A janela mostra uma lista completa de todos os pipelines para o programa selecionado. Isso é útil, pois apresenta informações mais abrangentes do que as disponíveis no [Cartão Pipeline.](#pipeline-card)

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriado.

1. No **Visão geral do programa** toque ou clique no link **Pipelines** para alternar para a guia **Pipelines** janela.

1. Aqui você pode ver uma lista de todos os pipelines para o programa, bem como iniciar e parar a execução do pipeline, como faria na variável **Cartão Pipelines**.

Se um pipeline estiver em execução, passar o mouse sobre ele **Status** revelará detalhes sobre a execução.

![Detalhes de execução do pipeline](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-status.png)

Tocar ou clicar **Exibir detalhes** levará você ao [detalhes da execução do pipeline.](#view-details)

## Janela de atividade {#activity}

A variável **Atividades** A janela mostra uma lista completa de todas as execuções de pipelines para o programa selecionado.

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriado.

1. No **Visão geral do programa** toque ou clique no link **Atividade** para alternar para a guia **Atividade** janela.

1. Aqui você pode ver uma lista de todas as execuções de pipeline do programa, incluindo as execuções atuais e históricas.

Se um pipeline estiver em execução, passar o mouse sobre ele **Status** revelará detalhes sobre a execução.

![Detalhes de execução do pipeline](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-activity.png)

Tocar ou clicar **Exibir detalhes** levará você ao [detalhes da execução do pipeline.](#view-details)

## Execução de pipelines {#running-pipelines}

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriado.

1. Navegue até a **Pipelines** do **Visão geral do programa** e clique no botão de reticências ao lado do pipeline executado e selecione **Executar** no menu.

1. A execução do pipeline começa e é indicada pela coluna **Status**.

Você pode ver os detalhes da execução clicando no botão de reticências novamente e selecionando **[Exibir detalhes](#view-details)**.

Dependendo do tipo de pipeline, talvez seja possível cancelar a execução clicando no botão de reticências novamente e selecionando **Cancelar**.

## Edição de pipelines {#editing-pipelines}

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriado.

1. Navegue até a **Pipelines** do **Visão geral do programa** e clique no botão de reticências ao lado do pipeline que deseja editar e selecione **Editar** no menu.

1. A caixa de diálogo **Editar pipeline de produção** ou **Editar pipeline de não produção** é exibida, permitindo editar os mesmos detalhes inseridos ao criar o pipeline.

   * Consulte as páginas a seguir para obter detalhes sobre todos os campos e opções de configuração disponíveis para pipelines.
      * [Configuração de pipelines de produção](configuring-production-pipelines.md)
      * [Configurar pipelines de não produção](configuring-non-production-pipelines.md)

1. Clique em **Atualizar** quando terminar de editar o pipeline.

>[!NOTE]
>
>Não é possível editar um pipeline em execução.

## Exclusão de pipelines {#deleting-pipelines}

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriado.

1. Navegue até a **Pipelines** do **Visão geral do programa** e clique no botão de reticências ao lado do pipeline executado e selecione **Excluir** no menu.

>[!NOTE]
>
>Não é possível excluir um pipeline em execução.

## Exibir detalhes do pipeline {#view-details}

Você pode visualizar os detalhes de um pipeline para ver o status e os logs da última execução.

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriado.

1. Navegue até a **Pipelines** do **Visão geral do programa** e clique no botão de reticências ao lado do pipeline executado e selecione **Exibir detalhes** no menu.

1. Você será levado à página de detalhes do pipeline em execução.

![Detalhes do pipeline](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-running-details.png)

Aqui, você pode ver o status das várias etapas do pipeline e recuperar registros de compilação para fins de diagnóstico. Consulte o documento [Implantação de código](/help/implementing/cloud-manager/deploy-code.md) para obter mais informações sobre implantação de código e execução de testes.

Todas as etapas em uma execução de pipeline são exibidas com aquelas que ainda não foram iniciadas esmaecidas. As etapas concluídas exibem sua duração.

Quando uma etapa do pipeline é concluída, um resumo é apresentado.

![Resumo da etapa](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-step.png)

Toque ou clique no **Exibir detalhes** link para revelar a **Duração** seção. Isso inclui a duração média do pipeline com base na tendência histórica para esse programa.

![Duração](/help/implementing/cloud-manager/assets/configure-pipeline/duration.png)

>[!NOTE]
>
>Você somente pode exibir detalhes de um pipeline que está em execução ou que foi executado pelo menos uma vez.

## Cancelar pipelines {#cancel}

Se um pipeline estiver na fase de validação ou criação de imagem, você poderá cancelar com segurança a execução do pipeline.

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriado.

1. Na página de visão geral do programa, clique no botão de reticências do pipeline que deseja cancelar na guia **Pipelines** cartão.

   ![Cancelar um pipeline](/help/implementing/cloud-manager/assets/cancel-pipeline.png)

1. Toque ou clique **Cancelar**.

Como alternativa, você pode cancelar um pipeline na página de detalhes do pipeline.

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriado.

1. Navegue até a **Pipelines** na guia **Visão geral do programa** e toque ou clique no pipeline que deseja cancelar.

1. Você será levado à página de detalhes do pipeline em execução.

   ![Cancelar detalhes do pipeline](/help/implementing/cloud-manager/assets/cancel-pipeline-details.png)

1. Toque ou clique **Cancelar**.
