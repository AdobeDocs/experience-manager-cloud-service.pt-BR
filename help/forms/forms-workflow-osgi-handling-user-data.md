---
title: Fluxos de trabalho centrados no Forms no OSGi | Manuseio de dados do usuário
description: Fluxos de trabalho centrados no Forms no OSGi | Manuseio de dados do usuário
uuid: 6eefbe84-6496-4bf8-b065-212aa50cd074
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9f400560-8152-4d07-a946-e514e9b9cedf
source-git-commit: 2d4ffd5518d671a55e45a1ab6f1fc41ac021fd80
workflow-type: tm+mt
source-wordcount: '994'
ht-degree: 0%

---


# Fluxos de trabalho centrados no Forms no OSGi | Manuseio de dados do usuário {#forms-centric-workflows-on-osgi-handling-user-data}

Os fluxos de trabalho de AEM centrados na Forms permitem que você automatize processos de negócios reais centrados na Forms. Os fluxos de trabalho consistem em uma série de etapas executadas em uma ordem especificada no modelo de fluxo de trabalho associado. Cada etapa executa uma ação específica, como atribuir uma tarefa a um usuário ou enviar uma mensagem de email. Os workflows podem interagir com ativos no repositório, contas de usuário e serviços. Portanto, os workflows podem coordenar atividades complicadas que envolvem qualquer aspecto do Experience Manager.

Um fluxo de trabalho centrado em formulários pode ser acionado ou iniciado por meio de qualquer um dos seguintes métodos:

* Envio de um aplicativo da Caixa de entrada AEM
* Enviando um aplicativo do aplicativo AEM [!DNL Forms]
* Envio de um formulário adaptável
* Uso de uma pasta monitorada
* Enviar uma comunicação interativa ou uma carta

Para obter mais informações sobre fluxos de trabalho e recursos de AEM centrados no Forms, consulte [Fluxo de trabalho centrado no Forms no OSGi](aem-forms-workflow.md).

## Dados do usuário e armazenamentos de dados {#user-data-and-data-stores}

Quando um workflow é acionado, uma carga é gerada automaticamente para a instância do workflow. Cada instância de fluxo de trabalho recebe uma ID de instância exclusiva e uma ID de carga associada. A carga contém os locais de repositório para dados de usuário e formulário associados a uma instância de fluxo de trabalho. Além disso, os rascunhos e os dados históricos de uma instância do workflow também são armazenados no repositório do AEM.

Os locais de repositório padrão onde a carga, os rascunhos e o histórico de uma instância de fluxo de trabalho residem são os seguintes:

>[!NOTE]
>
>É possível configurar locais diferentes para armazenar dados de carga, rascunho e histórico ao criar um fluxo de trabalho ou aplicativo. Para identificar os locais onde um fluxo de trabalho ou aplicativo armazenou dados, revise o fluxo de trabalho.

<table>
 <tbody>
  <tr>
   <td> </td>
   <td><b>AEM 6.4 [!DNL Forms]</b></td>
   <td><b>AEM 6.3 [!DNL Forms]</b></td>
  </tr>
  <tr>
   <td><strong>Instância do fluxo de trabalho <br /></strong></td>
   <td>/var/workflow/instances/[server_id]/&lt;date&gt;/[workflow-instance]/</td>
   <td>/etc/workflow/instances/[server_id]/[date]/[workflow-instance]/</td>
  </tr>
  <tr>
   <td><strong>Carga útil</strong></td>
   <td>/var/fd/dashboard/payload/[server_id]/[date]/<br /> [payload-id]/</td>
   <td>/etc/fd/dashboard/payload/[server_id]/[date]/<br /> [payload-id]/</td>
  </tr>
  <tr>
   <td><strong>Rascunhos</strong></td>
   <td>/var/fd/dashboard/instances/[server_id]/<br /> [date]/[workflow-instance]/draft/[workitem]/</td>
   <td>/etc/fd/dashboard/instances/[server_id]/<br /> [date]/[workflow-instance]/draft/[workitem]/</td>
  </tr>
  <tr>
   <td><strong>Histórico</strong></td>
   <td>/var/fd/dashboard/instances/[server_id]/<br /> [date]/[workflow_instance]/history/</td>
   <td>/etc/fd/dashboard/instances/[server_id]/<br /> [date]/[workflow_instance]/history/</td>
  </tr>
 </tbody>
</table>

## Acessar e excluir dados do usuário {#access-and-delete-user-data}

Você pode acessar e excluir dados do usuário de uma instância do fluxo de trabalho no repositório. Para isso, você deve saber a ID da instância do fluxo de trabalho associada ao usuário. É possível encontrar a ID de instância de uma instância de fluxo de trabalho usando o nome de usuário do usuário que iniciou a instância de fluxo de trabalho ou que é o destinatário atual da instância de fluxo de trabalho.

No entanto, não é possível identificar ou os resultados podem ser ambíguos ao identificar workflows associados a um iniciador nos seguintes cenários:

* **Fluxo de trabalho disparado por meio de uma pasta monitorada**: uma instância de fluxo de trabalho não poderá ser identificada com seu iniciador se o fluxo de trabalho for disparado por uma pasta monitorada. Nesse caso, as informações do usuário são codificadas nos dados armazenados.
* **Fluxo de trabalho iniciado a partir da instância de publicação do AEM**: todas as instâncias de fluxo de trabalho são criadas usando um usuário de serviço quando o Adaptive Forms ou as letras são enviadas a partir da instância de publicação do AEM. Nesses casos, o nome do usuário conectado não é capturado nos dados da instância do fluxo de trabalho.

### Acessar dados do usuário {#access}

Para identificar e acessar os dados do usuário armazenados para uma instância de workflow, execute as seguintes etapas:

1. Na instância do autor AEM, vá para `https://'[server]:[port]'/crx/de` e navegue até **[!UICONTROL Ferramentas > Consulta]**.

   Selecione **[!UICONTROL SQL2]** no menu suspenso **[!UICONTROL Type]**.

1. Dependendo das informações disponíveis, execute uma das seguintes consultas:

   * Execute o seguinte se o iniciador do fluxo de trabalho for conhecido:

   `SELECT &ast; FROM [cq:Workflow] AS s WHERE ISDESCENDANTNODE([path-to-workflow-instances]) and s.[initiator]='*initiator-ID*'`

   * Execute o seguinte se o usuário cujos dados você está encontrando for o destinatário atual do workflow:

   `SELECT &ast; FROM [cq:WorkItem] AS s WHERE ISDESCENDANTNODE([path-to-workflow-instances]) and s.[assignee]='*assignee-id*'`

   A consulta retorna o local de todas as instâncias do fluxo de trabalho para o iniciador do fluxo de trabalho especificado ou o destinatário do fluxo de trabalho atual.

   Por exemplo, a consulta a seguir retorna o caminho de duas instâncias de fluxo de trabalho do nó `/var/workflow/instances` cujo iniciador de fluxo de trabalho é `srose`.

   ![instância-fluxo-de-trabalho](assets/workflow-instance.png)

1. Vá para um caminho de instância de fluxo de trabalho retornado pela query. A propriedade de status exibe o status atual da instância do fluxo de trabalho.

   ![status](assets/status.png)

1. No nó da instância de fluxo de trabalho, navegue até `data/payload/`. A propriedade `path` armazena o caminho para a carga da instância de fluxo de trabalho. Você pode navegar até o caminho para acessar os dados armazenados na carga.

   ![caminho da carga](assets/payload-path.png)

1. Navegue até os locais dos rascunhos e do histórico da instância do fluxo de trabalho.

   Por exemplo:

   `/var/fd/dashboard/instances/server0/2018-04-09/_var_workflow_instances_server0_2018-04-09_basicmodel_54/draft/`

   `/var/fd/dashboard/instances/server0/2018-04-09/_var_workflow_instances_server0_2018-04-09_basicmodel_54/history/`

1. Repita as etapas 3 - 5 para todas as instâncias de fluxo de trabalho retornadas pela consulta na etapa 2.

   >[!NOTE]
   >
   >O aplicativo AEM [!DNL Forms] também armazena dados no modo offline. É possível que os dados de uma instância de fluxo de trabalho sejam armazenados localmente em dispositivos individuais e sejam enviados ao servidor [!DNL Forms] quando o aplicativo for sincronizado com o servidor.

### Excluir dados do usuário {#delete-user-data}

Você deve ser um administrador do AEM para excluir dados do usuário das instâncias do fluxo de trabalho, executando as seguintes etapas:

1. Siga as instruções em [Acessar dados do usuário](forms-workflow-osgi-handling-user-data.md#access) e anote o seguinte:

   * Caminhos para instâncias de fluxo de trabalho associadas ao usuário
   * Status das instâncias de fluxo de trabalho
   * Caminhos para cargas das instâncias de fluxo de trabalho
   * Caminhos para rascunhos e histórico das instâncias de fluxo de trabalho

1. Execute esta etapa para instâncias de fluxo de trabalho no status **EM EXECUÇÃO**, **SUSPENSO** ou **OBSOLETO**:

   1. Vá para `https://'[server]:[port]'/aem/start.html` e faça logon com credenciais de administrador.
   1. Navegue até **[!UICONTROL Ferramentas > Fluxo de trabalho> Instâncias]**.
   1. Selecione instâncias de fluxo de trabalho relevantes para o usuário e selecione **[!UICONTROL Encerrar]** para encerrar instâncias em execução.

      Para obter mais informações sobre como trabalhar com instâncias de fluxo de trabalho, consulte [Administrando instâncias de fluxo de trabalho](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/authoring/workflows/overview.html#authoring).

1. Vá para o console [!DNL CRXDE Lite], navegue até o caminho de carga de uma instância de fluxo de trabalho e exclua o nó `payload`.
1. Navegue até o caminho de rascunhos de uma instância de fluxo de trabalho e exclua o nó `draft`.
1. Navegue até o caminho do histórico de uma instância de fluxo de trabalho e exclua o nó `history`.
1. Navegue até o caminho da instância de fluxo de trabalho de uma instância de fluxo de trabalho e exclua o nó `[workflow-instance-ID]` do fluxo de trabalho.

   >[!NOTE]
   >
   >A exclusão do nó da instância de fluxo de trabalho removerá a instância de fluxo de trabalho para todos os participantes do fluxo de trabalho.

1. Repita as etapas 2 a 6 para todas as instâncias de fluxo de trabalho identificadas para um usuário.
1. Identifique e exclua dados de rascunho e envio offline da caixa de saída do aplicativo AEM [!DNL Forms] dos participantes do fluxo de trabalho para evitar qualquer envio para o servidor.

Também é possível usar APIs para acessar e remover nós e propriedades. Consulte os documentos a seguir para obter mais informações.

* [Como acessar programaticamente o AEM JCR](https://experienceleague.adobe.com/docs/experience-manager-65/developing/platform/access-jcr.html?lang=en#platform)
* [Removendo Nós e Propriedades](https://docs.adobe.com/docs/en/spec/jcr/2.0/10_Writing.html#10.9%20Removing%20Nodes%20and%20Properties)
* [Referência da API](https://helpx.adobe.com/experience-manager/6-3/sites-developing/reference-materials/javadoc/overview-summary.html)

>[!MORELIKETHIS]
>
>* [Usar fluxo de trabalho do AEM Forms para automação de processos empresariais](/help/forms/aem-forms-workflow.md)