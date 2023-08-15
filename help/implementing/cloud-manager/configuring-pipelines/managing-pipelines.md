---
title: Gerenciar pipelines
description: Saiba como gerenciar os pipelines existentes, incluindo edição, execução e exclusão.
index: true
exl-id: 4aff5a84-134a-43fa-8de8-8d564f4edd16
source-git-commit: 5ad33f0173afd68d8868b088ff5e20fc9f58ad5a
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 97%

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

## Execução de pipelines {#running-pipelines}

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriado.

1. Navegue até o cartão **Pipelines** na página **Visão geral do programa** e clique no botão de reticências ao lado do pipeline que deseja executar e selecione **Executar** no menu.

1. A execução do pipeline começa e é indicada pela coluna **Status**.

Você pode ver os detalhes da execução clicando no botão de reticências novamente e selecionando **[Exibir detalhes](#view-details)**.

Dependendo do tipo de pipeline, talvez seja possível cancelar a execução clicando no botão de reticências novamente e selecionando **Cancelar**.

## Edição de pipelines {#editing-pipelines}

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriado.

1. Navegue até o cartão **Pipelines** na página **Visão geral do programa** e clique no botão de reticências ao lado do pipeline que deseja editar e selecione **Editar** no menu.

1. A caixa de diálogo **Editar pipeline de produção** ou **Editar pipeline de não produção** é exibida, permitindo editar os mesmos detalhes inseridos ao criar o pipeline.

   * Consulte as páginas a seguir para obter detalhes sobre todos os campos e opções de configuração disponíveis para pipelines.
      * [Configuração de pipelines de produção](configuring-production-pipelines.md)
      * [Configurar pipelines de não produção](configuring-non-production-pipelines.md)

1. Clique em **Atualizar** depois de concluir a edição do pipeline.

>[!NOTE]
>
>Não é possível editar um pipeline em execução.

## Exclusão de pipelines {#deleting-pipelines}

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriado.

1. Navegue até o cartão **Pipelines** na página **Visão geral do programa** e clique no botão de reticências ao lado do pipeline executado e selecione **Excluir** no menu.

>[!NOTE]
>
>Não é possível excluir um pipeline em execução.

## Exibir Detalhes {#view-details}

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriado.

1. Navegue até o cartão **Pipelines** na página **Visão geral do programa** e clique no botão de reticências ao lado do pipeline executado e selecione **Exibir detalhes** no menu.

1. Você será levado à página de detalhes do pipeline em execução.

![Detalhes do pipeline](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-running-details.png)

Aqui, você pode ver o status das várias etapas do pipeline e recuperar registros de compilação para fins de diagnóstico. Consulte o documento [Implantação de código](/help/implementing/cloud-manager/deploy-code.md) para obter mais informações.

>[!NOTE]
>
>Você somente pode exibir detalhes de um pipeline que está em execução ou que foi executado pelo menos uma vez.
