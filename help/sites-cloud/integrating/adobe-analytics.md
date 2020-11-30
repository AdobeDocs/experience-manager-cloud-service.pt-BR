---
title: 'Integração ao Adobe Analytics '
description: 'Integração ao Adobe Analytics '
translation-type: tm+mt
source-git-commit: ec747361935b94a729cdd5b6712aee6d3ce1b8a2
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 14%

---


# Integração ao Adobe Analytics{#integrating-with-adobe-analytics}

Integrar o Adobe Analytics e o AEM como um Cloud Service permite rastrear a atividade de sua página da Web:

* Uma configuração do Adobe Analytics permite que o AEM se autentique com o Adobe Analytics.
* Uma estrutura identifica os dados enviados para o conjunto de relatórios da Adobe Analytics.

Os dados incluem dados de página e do usuário, por exemplo:

* dados que AEM componentes coletam
* cliques em links
* informações de uso do vídeo
* o número de visitas de página do Adobe Analytics

As páginas listadas abaixo podem ajudá-lo a configurar a integração. Observe que a Launch by Adobe é a ferramenta de fato para instrumentar um site AEM com recursos do Analytics (bibliotecas JS). Portanto, a integração do AEM como Cloud Service com o Launch e o Adobe Analytics está de mãos dadas.

* [Conexão com a Adobe Analytics e Criação de Estruturas](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/adobeanalytics-connect.html) - Observe que &quot;Estruturas do Analytics&quot; são herdadas em AEM e sua criação não funciona em AEM como Cloud Service porque requer a interface clássica. Em vez disso, o Launch by Adobe deve ser usado tanto para mapeamento de variável quanto para implantação de bibliotecas JS em páginas.
* [Integrar Launch by Adobe](https://docs.adobe.com/content/help/en/experience-manager-learn/sites/integrations/adobe-launch-integration-tutorial-understand.html)
* [Integrar AEM com o lançamento do Adobe via Adobe I/O](https://helpx.adobe.com/experience-manager/using/aem_launch_adobeio_integration.html)
* [Como entender AEM integração com Launch by Adobe, Analytics e Públicos alvos](https://helpx.adobe.com/experience-manager/kt/integration/using/aem-launch-integration-tutorial-understand.html)
* [Configuração do rastreamento de links para Adobe Analytics](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/adobeanalytics-link.html)
* [Mapeamento de dados de componente com propriedades do Adobe Analytics](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/adobeanalytics-mapping.html)
* [Configuração do rastreamento de vídeo para Adobe Analytics](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/adobeanalytics-video.html)
* [Classificações de Adobe](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/adobeanalytics-classifications.html)

>[!CAUTION]
>
>A Adobe Experience Manager como cliente Cloud Service que não tem uma conta do Analytics existente pode solicitar acesso ao Analytics Foundation Pack para Experience Cloud.  Este Foundation Pack fornece uso limitado por volume do Analytics.

>[!NOTE]
>
>A configuração IMS (contas técnicas) para Launch by Adobe é pré-configurada em AEM como um Cloud Service. Os usuários não precisam criar essa configuração.

## Informações adicionais {#further-information}

Consulte:

* [Estendendo a integração](https://docs.adobe.com/content/help/en/experience-manager-65/developing/extending-aem/extending-analytics/extending-analytics.html) Adobe Analytics para obter informações sobre o desenvolvimento de componentes que coletam dados de usuários e personalizam a estrutura do Adobe Analytics. Observe que &quot;Estruturas do Analytics&quot; são herdadas em AEM, e sua criação não funciona em AEM como Cloud Service porque requer a interface clássica. Em vez disso, o Launch by Adobe deve ser usado tanto para mapeamento de variável quanto para implantação de bibliotecas JS em páginas.
* O artigo da base de conhecimento, Integração com o [Adobe Analytics - solução de problemas](https://helpx.adobe.com/experience-manager/kb/sitecatalystintegrationtroubleshooting.html), para obter informações sobre como solucionar problemas da integração com o Adobe Analytics.

>[!NOTE]
>
>Se estiver usando o Adobe Analytics com uma configuração de proxy personalizada, precisará [configurar dois pacotes OSGi](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/configuring/configuring-osgi.html) (por exemplo, com o console da Web) necessários para as configurações de proxy do **Apache HTTP Client**. Ambos são necessários, pois algumas funcionalidades do AEM usam as APIs 3.x, enquanto outros usam as APIs 4.x. Configurar:
>
>* **Day Commons HTTP Client 3.1** para configurar a API 3.x;
   >  por exemplo, [https://localhost:4502/system/console/configMgr/com.day.commons.httpclient](https://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
   >
   >
* **Configuração** de proxy de componentes HTTP do Apache para configurar a API 4.x;
   >  por exemplo, [https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)

>


