---
title: 'Integração ao Adobe Analytics '
description: 'Integração ao Adobe Analytics '
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 12%

---


# Integração ao Adobe Analytics{#integrating-with-adobe-analytics}

A integração do Adobe Analytics e do AEM as a Cloud Service permite rastrear a atividade da página da Web:

* Uma configuração do Adobe Analytics permite que o AEM se autentique com o Adobe Analytics.
* Uma estrutura identifica os dados enviados para o conjunto de relatórios do Adobe Analytics.

Os dados incluem página e dados do usuário, por exemplo:

* dados que AEM componentes coletam
* cliques em links
* informações de uso do vídeo
* o número de visitas à página do Adobe Analytics

As páginas listadas abaixo podem ajudar a configurar a integração. Observe que o Launch by Adobe é a ferramenta de fato para instrumentar um site AEM com recursos do Analytics (bibliotecas JS). Portanto, integrar AEM as a Cloud Service com o Launch e o Adobe Analytics está de mãos dadas.

* [Conectar ao Adobe Analytics e Criar Frameworks](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/adobeanalytics-connect.html) - Observe que as &quot;estruturas do Analytics&quot; são herdadas no AEM e sua criação não funciona AEM as a Cloud Service, pois requer a interface do usuário clássica. Em vez disso, o Launch by Adobe deve ser usado para mapeamento de variável e para implantação de bibliotecas JS em páginas.
* [Integrar o Launch by Adobe](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/adobe-launch-integration-tutorial-understand.html)
* [Integrar AEM com o Adobe Launch via Adobe I/O](https://helpx.adobe.com/experience-manager/using/aem_launch_adobeio_integration.html)
* [Noções básicas sobre a integração do AEM com o Launch by Adobe, Analytics e Target](https://helpx.adobe.com/experience-manager/kt/integration/using/aem-launch-integration-tutorial-understand.html)
* [Configuração do rastreamento de link para o Adobe Analytics](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/adobeanalytics-link.html)
* [Mapeamento de dados do componente com propriedades do Adobe Analytics](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/adobeanalytics-mapping.html)
* [Configuração do rastreamento de vídeo para Adobe Analytics](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/adobeanalytics-video.html)
* [Classificações Adobe](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/adobeanalytics-classifications.html)

>[!CAUTION]
>
>Os clientes da Adobe Experience Manager as a Cloud Service que não têm uma conta existente do Analytics podem solicitar acesso ao Analytics Foundation Pack para Experience Cloud.  Este Foundation Pack fornece uso limitado por volume do Analytics.

>[!NOTE]
>
>A configuração IMS (contas técnicas) do Launch by Adobe é pré-configurada AEM as a Cloud Service. Os usuários não precisam criar essa configuração.

## Informações adicionais {#further-information}

Consulte:

* [Estender a integração do Adobe Analytics](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-analytics/extending-analytics.html) para obter informações sobre o desenvolvimento de componentes que coletam dados do usuário e personalizam a estrutura do Adobe Analytics. Observe que &quot;Estruturas do Analytics&quot; são herdadas no AEM e sua criação não funciona AEM as a Cloud Service, pois requer a interface do usuário clássica. Em vez disso, o Launch by Adobe deve ser usado para mapeamento de variável e para implantação de bibliotecas JS em páginas.
* o artigo da base de conhecimento, [Integração do Adobe Analytics - solução de problemas](https://helpx.adobe.com/experience-manager/kb/sitecatalystintegrationtroubleshooting.html), para obter informações sobre como solucionar problemas da integração com o Adobe Analytics.

>[!NOTE]
>
>Se estiver usando o Adobe Analytics com uma configuração de proxy personalizada, precisará [configurar dois pacotes OSGi](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/configuring-osgi.html) (por exemplo, com o console da Web) necessários para as configurações de proxy do **Apache HTTP Client**. Ambos são necessários, pois algumas funcionalidades do AEM usam as APIs 3.x, enquanto outros usam as APIs 4.x. Configurar:
>
>* **Day Commons HTTP Client 3.1** para configurar a API 3.x;
   >  por exemplo, [https://localhost:4502/system/console/configMgr/com.day.commons.httpclient](https://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
>
>* **Configuração de proxy de componentes HTTP do Apache** para configurar a API 4.x;
   >  por exemplo, [https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)
>

