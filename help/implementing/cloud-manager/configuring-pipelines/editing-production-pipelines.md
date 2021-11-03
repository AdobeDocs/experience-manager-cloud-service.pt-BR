---
title: Edição de um pipeline de produção
description: Edição de um pipeline de produção
index: false
source-git-commit: b9d28088ad18a389108ebfb81aa750c63e637922
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 0%

---


# Edição de um pipeline de produção {#edit-prod-pipeline}

É possível editar as configurações de pipeline da variável **Visão geral do programa** página.

Siga as etapas abaixo para editar o pipeline configurado:

1. Navegar para **Pipelines** do cartão **Visão geral do programa** página.

1. Clique em **...** do **Pipelines** e clique em **Editar**, conforme mostrado na figura abaixo.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-edit1.png)

1. O **Editar pipeline de produção** será exibida.

   1. O **Configuração** permite atualizar a guia **Nome do pipeline**, **Acionador da implantação** e **Comportamento de falha de métricas importantes**.

      >[!NOTE]
      >Consulte [Adicionar e gerenciar repositórios](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) para saber como adicionar e gerenciar repositórios no Cloud Manager.

      ![](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-edit2.png)


   1. O **Origem** fornece uma opção para marcar ou desmarcar **Pausar antes de implantar em produção** e **Programado** opções de **Opções de implantação de produção**.

      ![](/help/implementing/cloud-manager/assets/configure-pipeline/prod-pipeline-editnotier.png)

   1. O **Auditoria de experiência** permite atualizar ou adicionar novas páginas.

      ![](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-edit4.png)

1. Clique em **Atualizar** depois de concluir a edição do pipeline.

## Ações adicionais do pipeline de produção {#additional-prod-actions}

### Execução de um pipeline de produção {#run-prod}

Você pode executar o pipeline de produção no cartão Pipelines :

1. Navegar para **Pipelines** do cartão **Visão geral do programa** página.

1. Clique em **...** do **Pipelines** e clique em **Executar**, conforme mostrado na figura abaixo.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/prod-run.png)

### Exclusão de um pipeline de produção {#delete-prod}

Você pode excluir o pipeline de produção do cartão Pipelines:

1. Navegar para **Pipelines** do cartão **Visão geral do programa** página.

1. Clique em **...** do **Pipelines** e clique em **Excluir**, conforme mostrado na figura abaixo.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/prod-delete.png)

   >[!NOTE]
   >Um usuário na função Gerenciador de implantação agora pode excluir o pipeline de Produção de maneira automatizada por meio do **Excluir** na placa Pipeline.