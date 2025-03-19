---
title: Notas de versão do Cloud Manager 2025.3.0 no Adobe Experience Manager as a Cloud Service
description: Saiba mais sobre o lançamento do Cloud Manager 2025.3.0 no AEM as a Cloud Service.
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: 663234640f16e6aa653251399751abf5daa17f82
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 13%

---

# Notas de versão do Cloud Manager 2025.3.0 no Adobe Experience Manager as a Cloud Service {#release-notes}

<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/Cloud+Manager+2025.03.0+Release -->

Saiba mais sobre o lançamento do Cloud Manager 2025.3.0 no AEM (Adobe Experience Manager) as a Cloud Service.


Consulte também as [notas de versão atuais do Adobe Experience Manager as a Cloud Service](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Datas de lançamento {#release-date}

A data de lançamento do Cloud Manager 2025.3.0 no AEM as a Cloud Service é quinta-feira, 13 de março de 2025.

A próxima versão está planejada para sexta-feira, 10 de abril de 2025.

## Novidades {#what-is-new}

* **Executar vários pipelines**

  A capacidade de executar vários pipelines simultaneamente foi introduzida na página Pipelines. Os usuários devem selecionar pelo menos um pipeline, mas não mais de dez. Próximo ao canto superior direito na página Pipelines, clique em **Executar selecionados (x)**. Uma caixa de diálogo modal é exibida, listando todos os pipelines que não podem ser iniciados. Clique em **Executar** para iniciar todos os pipelines válidos.

  ![Caixa de diálogo Executar pipelines selecionados](/help/implementing/cloud-manager/release-notes/assets/run-selected-pipelines.png)

  Consulte também [Executar vários pipelines](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#run-multiple-pipelines)

* **Suporte estendido para versões Node.js**

  O ambiente de compilação front-end agora oferece suporte às seguintes `Node.js` versões:

   * 23
   * 22
   * 20

  Consulte também [Desenvolver sites com o pipeline de front-end](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md#node-versions). <!-- CMGR-65307 -->

<!--
## Early adoption program {#early-adoption}

Be a part of Cloud Manager's early adoption program and have a chance to test upcoming features. -->


## Correções de erros

* Correção de **(UI) para atualizações de &#39;Configuração Avançada de Rede&#39; no Cloud Manager**

  Um problema raro que impedia atualizações na **Configuração Avançada de Rede** quando uma notificação de &quot;Atualização disponível&quot; estava presente foi resolvido. Anteriormente, o Cloud Manager bloqueava modificações de configuração, incluindo configurações avançadas de rede, para evitar conflitos durante uma atualização. Os clientes agora podem acionar manualmente a atualização pendente para aplicar as alterações necessárias sem restrições. <!-- CMGR-65913 and CMGR-65788 -->

* Correção de **(UI) para atualizações de lista de permissões de IP presas no estado &quot;Atualizando&quot;**

  Um problema raro em que as atualizações de lista de permissões de IP no Cloud Manager permaneciam presas no estado &quot;Atualizando&quot; devido à configuração de domínio ativo duplicada para um ambiente foi resolvido. Anteriormente, os clientes enfrentavam atrasos de processamento indefinidos ao atualizar listas de permissões IP, impedindo os ajustes necessários de acesso à rede. Essa correção garante que as atualizações da lista de permissões IP agora possam ser concluídas com êxito sem travar. <!-- CMGR-65786 -->




<!-- ## Known issues {#known-issues} -->
