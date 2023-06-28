---
title: Integração com o Adobe Target
description: Integração com o Adobe Target
exl-id: 2b4cf35e-2b75-4303-8d09-f6644ad99274
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '716'
ht-degree: 72%

---

# Integração com o Adobe Target{#integrating-with-adobe-target}

Como parte da Adobe Experience Cloud, [Adobe Target](https://business.adobe.com/products/target/adobe-target.html) O permite aumentar a relevância do conteúdo por meio do direcionamento e da medição em todos os canais. O Adobe Target é usado pelos profissionais de marketing para projetar e executar testes online, criar segmentos de público instantaneamente (com base no comportamento) e automatizar o direcionamento de conteúdo e experiências online. O AEM as a Cloud Service adotou o fluxo de trabalho direcionado usado no Adobe Target Standard. Se você usa o Target, está familiarizado com o ambiente de edição de direcionamento no AEM as a Cloud Service.

Integre seus sites de AEM ao Adobe Target para que você possa personalizar o conteúdo em suas páginas:

* Implemente o direcionamento de conteúdo.
* Use os públicos do Target para criar experiências personalizadas.
* Envie dados de contexto para o Target quando os visitantes interagirem com suas páginas.
* Rastreie as taxas de conversão.

>[!NOTE]
>
>Os clientes que não têm uma conta do Target existente podem solicitar acesso ao Target Foundation Pack para Experience Cloud. O Foundation Pack fornece uso limitado por volume do Target.


Para integrar com o Target, execute as seguintes tarefas:

* [Execute as tarefas de pré-requisito](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/target-requirements.html?lang=pt-BR): registre-se no Adobe Target e configure determinados aspectos da instância de autor do AEM. Sua conta do Adobe Target deve ter no mínimo o nível de permissão **aprovador**. Além disso, você deve proteger as configurações de atividade no nó de publicação para que elas fiquem inacessíveis aos usuários.

* O Experience Platform Launch é a ferramenta padrão para instrumentar um site do AEM com recursos do Target (bibliotecas JS). Portanto, a integração do AEM as a Cloud Service com o Launch e o Adobe Target está intimamente relacionada (consulte os links abaixo).

   * [Integração com o Adobe Target usando o Adobe I/O](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/integration-target-ims.html)
   * [Integrar o Experience Platform Launch](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-data-collection-tags/overview.html)
   * [Integrar o AEM ao Adobe Launch por meio do Adobe I/O](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-data-collection-tags/overview.html?lang=en)
   * [Noções básicas sobre a integração do AEM com o Experience Platform Launch, Analytics e Target](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-data-collection-tags/overview.html)

>[!NOTE]
>
>A configuração do IMS (contas técnicas) do Experience Platform Launch é pré-configurada no AEM as a Cloud Service. Os usuários não precisam criar essa configuração.

1. [Configurar atividades](https://experienceleague.adobe.com/docs/experience-manager-65/authoring/personalization/activitylib.html?lang=pt-BR): associe suas atividades à configuração de nuvem do Target.

>[!CAUTION]
>
>No AEM as a Cloud Service, o agente de replicação que sincroniza as Ofertas e Atividades do AEM para o Adobe Target é desativado por padrão. Entre em contato com [Suporte para Adobe](https://experienceleague.adobe.com/?support-solution=General&amp;lang=pt-BR#support) se for necessário reativar o agente de replicação.

>[!NOTE]
>
>Se você estiver usando o Target com uma configuração de proxy personalizada, deverá definir ambas as configurações de proxy do HTTP Client, pois algumas funcionalidades do AEM estão usando as APIs 3.x e algumas outras as APIs 4.x:
>
>* A 3.x está configurada com [http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
>* A 4.x está configurada com [http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)
>

>[!CAUTION]
>
>Proteger o nó de configurações de atividade **cq:ActivitySettings** na instância de publicação para que fique inacessível aos usuários normais. O nó de configurações de atividade só deve estar acessível ao serviço que lida com a sincronização de atividades com o Adobe Target.
>
>Consulte [Pré-requisitos para integração com o Adobe Target](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/target-requirements.html?lang=pt-BR#securing-the-activity-settings-node) para obter informações detalhadas.

Quando a integração for concluída, você poderá [criar conteúdo direcionado](https://experienceleague.adobe.com/docs/experience-manager-65/authoring/personalization/content-targeting-touch.html?lang=pt-BR) que envia dados do visitante para o Adobe Target. Os componentes da página exigem um código específico para ativar o direcionamento de conteúdo. (Consulte [Desenvolvimento de conteúdo direcionado](https://experienceleague.adobe.com/docs/experience-manager-65/developing/personlization/target.html?lang=pt-BR).

>[!NOTE]
>
>Ao direcionar um componente no autor do AEM, o componente faz uma série de chamadas do lado do servidor para o Adobe Target registrar a campanha, configurar ofertas e recuperar segmentos do Adobe Target (se configurado). Nenhuma chamada do lado do servidor é feita do ambiente de publicação do AEM para o Adobe Target.

## Fontes de informações de segundo plano {#background-information-sources}

Integrar o AEM as a Cloud Service com o Adobe Target exige conhecimento do Adobe Target, de gerenciamento de Atividades do AEM e de gerenciamento de Públicos do AEM. Familiarize-se com as seguintes informações:

* Adobe Target (consulte a [documentação do Adobe Target](https://experienceleague.adobe.com/docs/target/using/target-home.html?lang=pt-BR)).
* Console de Atividades do AEM (consulte [Gerenciamento de atividades](https://experienceleague.adobe.com/docs/experience-manager-65/authoring/personalization/activitylib.html?lang=pt-BR)).
* Públicos do AEM (consulte [Gerenciamento de públicos](https://experienceleague.adobe.com/docs/experience-manager-65/authoring/personalization/managing-audiences.html?lang=pt-BR)).

>[!NOTE]
>
>Ao trabalhar com o Adobe Target, o número máximo de artefatos permitidos em uma campanha é o seguinte:
>
>* 50 locais
>* 2.000 experiências
>* 50 métricas
>* 50 segmentos de relatórios
