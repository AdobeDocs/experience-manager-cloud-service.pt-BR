---
title: Visualização de logs para um conjunto de migração na ferramenta Transferência de conteúdo
description: Visualização de logs para um conjunto de migração na ferramenta Transferência de conteúdo
exl-id: aed1ac83-a2fb-425e-aca4-39cd0bb42fd3
source-git-commit: a3e79441d46fa961fcd05ea54e84957754890d69
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 36%

---

# Visualização de logs para um conjunto de migração {#view-logs-content-transfer-tool}


>[!CONTEXTUALHELP]
>id="aemcloud_ctt_logs"
>title="Exibir logs"
>abstract="Após a conclusão da extração da ingestão, verifique os logs em busca de erros/avisos. Todos os erros devem ser resolvidos imediatamente, seja resolvendo os problemas relatados ou entrando em contato com o suporte da Adobe."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html#troubleshooting" text="Resolução de problemas"
>additional-url="https://helpx.adobe.com/br/enterprise/using/support-for-experience-cloud.html" text="Contato com o suporte da Adobe"

Após a conclusão de cada etapa (extração e assimilação), verifique os registros e procure por erros.  Todos os erros devem ser resolvidos imediatamente, seja resolvendo os problemas relatados ou entrando em contato com o suporte da Adobe.

## Etapas para visualizar logs {#viewing-logs}

### Logs de extração

Para visualizar os logs de extração, vá para a instância do Adobe Experience Manager de origem e selecione o conjunto de migração desejado.

Em seguida, siga as etapas abaixo:

1. Selecione um conjunto de migração e clique em **Exibir registro** na barra de ações. Isso exibirá a caixa de diálogo Logs. Clique em **Log de extração** para visualizar os logs em uma nova guia.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam25.png) \
   Ou clique no link **CONCLUÍDO** status para visualizar logs em uma nova guia.

1. Para rastrear os logs sem usar a interface do usuário, você pode aplicar SSH ao ambiente do AEM de origem e rastrear o conteúdo do `crx-quickstart/cloud-migration/extraction-XXXXX/output.log file`.

### Logs de assimilação

Para visualizar os logs de assimilação, acesse a lista Trabalhos de assimilação no Cloud Acceleration Manager, localize o trabalho de migração desejado e clique nos três pontos (**..**) do trabalho. É possível clicar em **Baixar log** para baixar logs.

![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam28.png)
