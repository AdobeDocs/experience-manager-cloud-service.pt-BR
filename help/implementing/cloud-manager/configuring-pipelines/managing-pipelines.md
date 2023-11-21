---
title: Gerenciar pipelines
description: Saiba como gerenciar os pipelines existentes, incluindo edição, execução e exclusão.
index: true
exl-id: 4aff5a84-134a-43fa-8de8-8d564f4edd16
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '938'
ht-degree: 68%

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

A janela **Pipelines** mostra uma lista completa de todos os pipelines do programa selecionado. Isso permite visualizar informações mais abrangentes do que as disponíveis no [cartão do pipeline.](#pipeline-card)

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriado.

1. No **Visão geral do programa** selecione a **Pipelines** para alternar para a guia **Pipelines** janela.

1. Aqui você pode ver uma lista de todos os pipelines do programa, bem como iniciar e parar a execução do pipeline, assim como no **cartão do pipeline**.

Se um pipeline estiver em execução, passar o mouse sobre a coluna **Status** revelará detalhes da execução.

![Detalhes da execução do pipeline](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-status.png)

Tocar ou clicar em **Exibir detalhes** mostrará os [detalhes da execução do pipeline.](#view-details)

## Janela Atividade {#activity}

A janela **Atividades** mostra uma lista completa de todas as execuções de pipeline do programa selecionado.

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriado.

1. No **Visão geral do programa** selecione a **Atividade** para alternar para a guia **Atividade** janela.

1. Aqui você pode ver uma lista de todas as execuções de pipeline do programa, incluindo as execuções atuais e históricas.

Se um pipeline estiver em execução, passar o mouse sobre a coluna **Status** revelará detalhes da execução.

![Detalhes da execução do pipeline](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-activity.png)

Tocar ou clicar em **Exibir detalhes** mostrará os [detalhes da execução do pipeline.](#view-details)

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

   * Consulte as páginas a seguir para obter detalhes sobre os campos e as opções de configuração disponíveis para pipelines.
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

Ao exibir todas as etapas de uma execução de pipeline, as que ainda não foram iniciadas aparecem esmaecidas. As etapas concluídas exibem sua duração.

Quando uma etapa do pipeline é concluída, um resumo é apresentado.

![Resumo da etapa](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-step.png)

Selecione o **Exibir detalhes** link para revelar a **Duração** seção. Isso inclui a duração média do pipeline com base na tendência histórica desse programa.

![Duração](/help/implementing/cloud-manager/assets/configure-pipeline/duration.png)

>[!NOTE]
>
>Só é possível exibir detalhes de um pipeline que está em execução ou que foi executado pelo menos uma vez.

## Cancelar pipelines {#cancel}

Se um pipeline estiver na fase de validação ou criação de imagem, você poderá cancelar com segurança a execução do pipeline.

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriado.

1. Na página de visão geral do programa, clique no botão de reticências do pipeline que deseja cancelar na guia **Pipelines** cartão.

   ![Cancelar um pipeline](/help/implementing/cloud-manager/assets/cancel-pipeline.png)

1. Selecionar **Cancelar**.

Como alternativa, você pode cancelar um pipeline na página de detalhes do pipeline.

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriado.

1. Navegue até a **Pipelines** na guia **Visão geral do programa** e selecione o pipeline que deseja cancelar.

1. Você será levado à página de detalhes do pipeline em execução.

   ![Cancelar detalhes do pipeline](/help/implementing/cloud-manager/assets/cancel-pipeline-details.png)

1. Selecionar **Cancelar**.
