---
title: Visualização de logs para um conjunto de migração na ferramenta Transferência de conteúdo
description: Visualização de logs para um conjunto de migração na ferramenta Transferência de conteúdo
exl-id: aed1ac83-a2fb-425e-aca4-39cd0bb42fd3
source-git-commit: 9a098eefbb730ae2930169cf7402ab4799043291
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 12%

---

# Visualização de logs para um conjunto de migração {#view-logs-content-transfer-tool}


>[!CONTEXTUALHELP]
>id="aemcloud_ctt_logs"
>title="Visualização de logs"
>abstract="Após a conclusão da extração da assimilação, verifique os logs em busca de erros/avisos. Todos os erros devem ser resolvidos imediatamente, lidando com os problemas relatados ou entrando em contato com o suporte ao Adobe."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#troubleshooting" text="Resolução de problemas"
>additional-url="https://helpx.adobe.com/ca/enterprise/admin-guide.html/ca/enterprise/using/support-for-experience-cloud.ug.html" text="Entrar em contato com o suporte ao Adobe"

Após a conclusão de cada etapa (extração e assimilação), verifique os logs e procure erros.  Todos os erros devem ser resolvidos imediatamente, lidando com os problemas relatados ou entrando em contato com o suporte ao Adobe.

## Etapas para visualizar logs {#viewing-logs}

Para exibir os Logs de extração, vá para a instância do Adobe Experience Manager de origem e selecione o conjunto de migração desejado.

Em seguida, siga as etapas abaixo:

1. Selecione um conjunto de migração e clique em **Exibir registro** na barra de ações. Isso exibirá a caixa de diálogo Logs . Clique em **Log de extração** para exibir os logs em uma nova guia.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam25.png) \
   Ou clique no botão **CONCLUÍDO** status para exibir logs em uma nova guia.

1. Para rastrear os logs sem usar a interface do usuário, você pode aplicar SSH ao ambiente do AEM de origem e rastrear o conteúdo do `crx-quickstart/cloud-migration/extraction-XXXXX/output.log file`.

1. Para exibir os logs de Assimilação, vá para a lista Tarefas de Assimilação no Cloud Acceleration Manager e clique nos três pontos (**...**). Você pode clicar em **Baixar log** para baixar logs.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam28.png)
