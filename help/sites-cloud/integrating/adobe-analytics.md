---
title: 'Integração ao Adobe Analytics '
description: 'Integração ao Adobe Analytics '
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: ht
source-wordcount: '545'
ht-degree: 100%

---


# Integração ao Adobe Analytics{#integrating-with-adobe-analytics}

A integração do Adobe Analytics com o AEM as a Cloud Service permite acompanhar a atividade da página da Web:

* Uma configuração do Adobe Analytics permite que o AEM faça autenticação com o Adobe Analytics.
* Uma estrutura identifica os dados enviados para o conjunto de relatórios do Adobe Analytics.

Os dados incluem página e dados do usuário, como por exemplo:

* dados que os componentes do AEM coletam
* cliques em links
* informações de uso de vídeo
* o número de visitas à página do Adobe Analytics

As páginas listadas abaixo podem ajudar a configurar a integração. Observe que o Launch by Adobe é a ferramenta de fato para instrumentar um site do AEM com recursos do Analytics (bibliotecas JS). Portanto, a integração do AEM as a Cloud Service com o Launch está de mãos dadas com a integração do Adobe Analytics.

* [Conectar-se ao Adobe Analytics e criar estruturas](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/adobeanalytics-connect.html?lang=pt_BR) - observe que as &quot;estruturas do Analytics&quot; são legadas no AEM e sua criação não funciona no AEM as a Cloud Service, pois requer a interface de usuário clássica. Em vez disso, o Launch by Adobe deve ser usado para mapeamento de variáveis e para implantação de bibliotecas JS em páginas.
* [Integrar o Launch by Adobe](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-launch/overview.html?lang=pt-BR)
* [Integrar o AEM com o Adobe Launch via Adobe I/O](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-launch/overview.html?lang=pt-BR)
* [Noções básicas sobre a integração do AEM com o Launch by Adobe, o Analytics e o Target](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-launch/overview.html?lang=pt-BR)
* [Configuração do rastreamento de links para o Adobe Analytics](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/adobeanalytics-link.html?lang=pt_BR)
* [Mapeamento de dados do componente com propriedades do Adobe Analytics](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/adobeanalytics-mapping.html?lang=pt_BR)
* [Configuração do rastreamento de vídeo para o Adobe Analytics](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/adobeanalytics-video.html?lang=pt_BR)
* [Classificações do Adobe](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/adobeanalytics-classifications.html?lang=pt_BR)

>[!CAUTION]
>
>Os clientes da Adobe Experience Manager as a Cloud Service que não têm uma conta existente do Analytics podem solicitar acesso ao Analytics Foundation Pack para Experience Cloud.  Este Foundation Pack fornece uso do Analytics limitado por volume.

>[!NOTE]
>
>A configuração do IMS (contas técnicas) do Launch by Adobe é pré-configurada no AEM as a Cloud Service. Os usuários não precisam criar essa configuração.

## Informações adicionais {#further-information}

Consulte:

* [Estender a integração do Adobe Analytics](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-analytics/extending-analytics.html?lang=pt_BR) para obter informações sobre o desenvolvimento de componentes que coletam dados do usuário e personalização da estrutura do Adobe Analytics. Observe que as &quot;estruturas do Analytics&quot; são legadas no AEM e sua criação não funciona no AEM as a Cloud Service, pois requer a interface de usuário clássica. Em vez disso, o Launch by Adobe deve ser usado para mapeamento de variáveis e para implantação de bibliotecas JS em páginas.
* O artigo da base de conhecimento, [Integração do Adobe Analytics - solução de problemas](https://helpx.adobe.com/br/experience-manager/kb/sitecatalystintegrationtroubleshooting.html), para obter informações sobre como solucionar problemas de integração com o Adobe Analytics.

>[!NOTE]
>
>Se estiver usando o Adobe Analytics com uma configuração de proxy personalizada, precisará [configurar dois pacotes OSGi](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/configuring-osgi.html?lang=pt_BR) (por exemplo, com o console da Web) necessários para as configurações de proxy do **Apache HTTP Client**. Ambos são necessários, pois algumas funcionalidades do AEM usam as APIs 3.x, enquanto outros usam as APIs 4.x. Configurar o:
>
>* **Day Commons HTTP Client 3.1** para configurar a API 3.x;
   >  por exemplo, [https://localhost:4502/system/console/configMgr/com.day.commons.httpclient](https://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
>
>* **Configuração de proxy de componentes HTTP do Apache** para configurar a API 4.x;
   >  por exemplo, [https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)
>

