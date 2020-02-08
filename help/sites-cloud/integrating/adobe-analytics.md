---
title: Integração com o Adobe Analytics
description: 'Integração com o Adobe Analytics '
translation-type: tm+mt
source-git-commit: 6754693da488b0bc44a71aa9f0402fc1308b703a

---


# Integração com o Adobe Analytics{#integrating-with-adobe-analytics}

A integração do Adobe Analytics e do AEM como um serviço em nuvem permite rastrear a atividade da página da Web:

* Uma configuração do Adobe Analytics permite que o AEM se autentique com o Adobe Analytics.
* Uma estrutura identifica os dados enviados para o conjunto de relatórios do Adobe Analytics.

Os dados incluem dados de página e do usuário, por exemplo:

* dados que os componentes do AEM coletam
* cliques em links
* informações de uso do vídeo
* o número de visitas de página do Adobe Analytics

As páginas listadas abaixo podem ajudá-lo a configurar a integração. Observe que o Launch da Adobe é a ferramenta de fato para instrumentar um site do AEM com recursos do Analytics (bibliotecas JS). Portanto, a integração do AEM como um serviço em nuvem com o Launch e o Adobe Analytics é fornecida em conjunto.

* [Conexão com o Adobe Analytics e Criação de Estruturas](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/adobeanalytics-connect.html) - Observe que &quot;Estruturas do Analytics&quot; são herdadas no AEM, e sua criação não funciona no AEM como um Serviço de Nuvem porque requer a interface clássica. O lançamento pela Adobe deve ser usado, tanto para mapeamento de variáveis quanto para implantação de bibliotecas JS em páginas.
* [Integrar lançamento pela Adobe](https://docs.adobe.com/content/help/en/experience-manager-learn/sites/integrations/adobe-launch-integration-tutorial-understand.html)
* [Integrar o AEM ao Adobe Launch via E/S da Adobe](https://helpx.adobe.com/experience-manager/using/aem_launch_adobeio_integration.html)
* [Como entender a integração do AEM com o Launch da Adobe, Analytics e Target](https://helpx.adobe.com/experience-manager/kt/integration/using/aem-launch-integration-tutorial-understand.html)
* [Configuração do rastreamento de links para o Adobe Analytics](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/adobeanalytics-link.html)
* [Mapeamento de dados de componentes com as propriedades do Adobe Analytics](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/adobeanalytics-mapping.html)
* [Configuração do rastreamento de vídeo para o Adobe Analytics](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/adobeanalytics-video.html)
* [Classificações da Adobe](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/adobeanalytics-classifications.html)

>[!CAUTION]
>
>O Adobe Experience Manager como cliente do Cloud Service que não tem uma conta existente do Analytics pode solicitar acesso ao Analytics Foundation Pack para a Experience Cloud.  Este Foundation Pack fornece uso limitado por volume do Analytics.

>[!NOTE]
>
>A configuração do IMS (contas técnicas) para o Launch da Adobe é pré-configurada no AEM como um serviço em nuvem. Os usuários não precisam criar essa configuração.

## Informações adicionais {#further-information}

Consulte:

* [Extensão da integração](https://docs.adobe.com/content/help/en/experience-manager-65/developing/extending-aem/extending-analytics/extending-analytics.html) do Adobe Analytics para obter informações sobre o desenvolvimento de componentes que coletam dados de usuários e personalizam a estrutura do Adobe Analytics. Observe que &quot;Estruturas do Analytics&quot; são herdadas no AEM, e sua criação não funciona no AEM como um Serviço de nuvem porque requer a interface clássica. O lançamento pela Adobe deve ser usado, tanto para mapeamento de variáveis quanto para implantação de bibliotecas JS em páginas.
* O artigo da base de conhecimento, Integração do [Adobe Analytics - solução de problemas](https://helpx.adobe.com/experience-manager/kb/sitecatalystintegrationtroubleshooting.html), para obter informações sobre como solucionar problemas de integração do Adobe Analytics.

>[!NOTE]
>
>Se você estiver usando o Adobe Analytics com uma configuração de proxy personalizada, precisará [configurar dois pacotes](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/configuring/configuring-osgi.html) OSGi (por exemplo, com o console da Web) necessários para as configurações de proxy do **Apache HTTP Client** . Ambos são necessários, pois algumas funcionalidades do AEM usam as APIs 3.x, enquanto outros usam as APIs 4.x. Configurar:
>
>* **Day Commons HTTP Client 3.1** para configurar a API 3.x;
   >  por exemplo, [https://localhost:4502/system/console/configMgr/com.day.commons.httpclient](https://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
   >
   >
* **Configuração** de proxy de componentes HTTP Apache para configurar a API 4.x;
   >  por exemplo, [https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)
>


