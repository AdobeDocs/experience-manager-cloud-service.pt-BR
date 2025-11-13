---
title: Restaure o código Source anterior implantado
description: Saiba como restaurar um ambiente para sua última compilação bem-sucedida &ndash; nenhuma execução de pipeline é necessária.
feature: Operations
role: Admin
exl-id: 8f804f55-a66d-47ad-a48d-61b861cef4f7
source-git-commit: 4008b2f81bbd81cef343c6d2b04ba536b66d7d89
workflow-type: tm+mt
source-wordcount: '578'
ht-degree: 3%

---

# Restaurar o código-fonte anterior implantado no AEM as a Cloud Service {#restore-previous-code-deployed}

<!-- BETA BADGE REMOVED FOR NOVEMBER 2025 CM RELEASE badge: label="Beta" type="Positive" url="/help/implementing/cloud-manager/release-notes/current.md#gitlab-bitbucket"

>[!NOTE]
>
>The feature described in this article is only available through the beta program. To sign up for the beta, see [One-click rollback for pipeline deployments](/help/implementing/cloud-manager/release-notes/current.md##one-click-rollback). -->

Use **Restaurar o código anterior implantado** para reverter um ambiente instantaneamente para sua última compilação bem-sucedida; não é necessária a execução do pipeline.

Você simplesmente abre o menu ![Mais ícone ou o ícone do menu de reticências](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) do ambiente selecionado e escolhe **Restaurar** > **Código anterior implantado** para reverter o código-fonte implantado mais recentemente em segundos.

Consulte também [Restaurar conteúdo no AEM as a Cloud Service](/help/operations/restore.md).

>[!TIP]
>
>Você pode exibir a versão do código-fonte ativo em uso na exibição de detalhes do ambiente, na guia **Geral**. Consulte [Exibir detalhes de um ambiente](/help/implementing/cloud-manager/manage-environments.md#viewing-environment).
>
>![Versão do código Source em uso](/help/operations/assets/environments-view-details-sourcecodeversion.png)

**Restaurar código anterior implantado** fica disponível somente quando as seguintes condições são atendidas:

* Somente uma restauração é permitida por execução bem-sucedida do pipeline; para restaurar novamente, conclua outra execução bem-sucedida do pipeline.
* Você tem **permissões de Criação** de Restauração de Ambiente. Para obter detalhes sobre o gerenciamento de permissões, consulte [Permissões personalizadas](/help/implementing/cloud-manager/custom-permissions.md).
* O sinalizador de recurso que protege esse recurso está habilitado (ativado).
* O programa é executado no AEM as a Cloud Service.
* O último pipeline para esse ambiente foi concluído com êxito e executado há **menos de 30 dias**.
* O status do ambiente é *Em execução* e nenhum pipeline está em andamento.

**Restaurar código anterior implantado** funciona no ambiente `Production`, além do ambiente `Development`, ambiente `Stage` e `Specialized Testing Environment`. Após confirmar, o Cloud Manager inicia a restauração e envia uma notificação por push no início e na conclusão bem-sucedida.

>[!IMPORTANT]
>
>Para ser usado pela primeira vez, a Adobe recomenda validar o procedimento em `Stage` *antes* usando-o em `Production` para reduzir riscos e garantir estabilidade.


Se alguma verificação falhar, o Cloud Manager abre a caixa de diálogo a seguir, que lista uma ou mais condições não atendidas e desabilita a **Confirmação**, impedindo a restauração.

![Caixa de diálogo de falha de restauração de código anterior implantada](/help/operations/assets/restore-previous-code-deployment-not-allowed.png).

Se você quiser apenas restaurar os dados que foram perdidos, danificados ou acidentalmente excluídos para sua condição original, você pode usar [Restaurar Conteúdo no AEM as a Cloud Service](/help/operations/restore.md). Esse processo de restauração afeta apenas o conteúdo, deixando o código-fonte e a versão do AEM inalterados.

**Para restaurar o código anterior implantado:**

1. Faça logon no Cloud Manager, em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/), e selecione a organização apropriada.

1. Clique no programa para o qual deseja iniciar uma restauração.

1. Liste todos os ambientes do programa seguindo um destes procedimentos:

   * No menu do lado esquerdo, em **Serviços**, clique em ![Ícone de dados](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Data_18_N.svg) **Ambientes**.

     ![Guia Ambientes](assets/environments-1.png)

   * No menu do lado esquerdo, em **Programa**, clique em **Visão Geral** e, no cartão **Ambientes**, clique em ![ícone de Fluxo de Trabalho](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Workflow_18_N.svg) **Mostrar Tudo**.

     ![Mostrar todas as opções](assets/environments-2.png)

     >[!NOTE]
     >
     >O cartão **Ambientes** lista apenas três ambientes. Clique em **Mostrar tudo** no cartão para ver *todos* os ambientes do programa.

1. Na tabela Ambientes, à direita de um ambiente cujo código-fonte você deseja restaurar, clique em ![Ícone de mais ou ícone de menu de reticências](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) e em **Restaurar** > **Código anterior implantado**.

   ![Restaurar opção implantada de código anterior a partir do menu de reticências](/help/operations/assets/restore-previous-code-deployed-menu.png)

1. Na caixa de diálogo **Restaurar código anterior implantado**, revise a versão implantada no momento e a versão que deseja restaurar e clique em **Confirmar**.

   ![Restaurar caixa de diálogo implantada de código anterior](/help/operations/assets/restore-previous-code-deployed-dialogbox.png)

1. O Cloud Manager reverte o ambiente para a compilação anterior, mantém o conteúdo e a configuração intactos e marca o ambiente **Restaurando** na página Ambientes até que a implantação seja concluída.

   ![Restaurando a ativação](/help/operations/assets/restore-previous-code-deployed-restoring.png)

1. Próximo ao canto superior direito da página, clique no ícone ![Sino ou Ícone Notificações ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Bell_18_N.svg) **Notificações** para descobrir quando a restauração começa e termina.

   ![Restaurar notificações de código anteriores ao iniciar a restauração e quando a restauração for concluída](/help/operations/assets/restore-previous-code-notifications.png)
   *Notificações para um trabalho de restauração de código anterior.*
