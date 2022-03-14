---
title: Integração com o Adobe Target
description: Integração com o Adobe Target
exl-id: 2b4cf35e-2b75-4303-8d09-f6644ad99274
source-git-commit: 65e1ede4cdc8035657e8b37fe206ebed4ab7bb24
workflow-type: tm+mt
source-wordcount: '723'
ht-degree: 4%

---

# Integração com o Adobe Target{#integrating-with-adobe-target}

Como parte da Adobe Marketing Cloud, [Adobe Target](http://www.adobe.com/solutions/testing-targeting/testandtarget.html) permite aumentar a relevância do conteúdo por meio do direcionamento e da medição em todos os canais. O Adobe Target é usado pelos profissionais de marketing para projetar e executar testes online, criar segmentos de público-alvo instantaneamente (com base no comportamento) e automatizar o direcionamento de conteúdo e experiências online. AEM as a Cloud Service adotou o workflow para construção do target usado no Adobe Target Standard. Se você usar o Target, estará familiarizado com o ambiente de edição de direcionamento AEM as a Cloud Service.

Integre seus sites de AEM com o Adobe Target para personalizar o conteúdo em suas páginas:

* Implemente o direcionamento de conteúdo.
* Use os públicos-alvo do Target para criar experiências personalizadas.
* Envie dados de contexto para o Target quando os visitantes interagirem com suas páginas.
* Rastreie as taxas de conversão.

>[!NOTE]
>
>Os clientes do Adobe Experience Manager as a Cloud Service que não têm uma conta Target existente podem solicitar acesso ao Target Foundation Pack para Experience Cloud.  O Foundation Pack fornece uso limitado por volume do Target.


Para integrar com o Target, execute as seguintes tarefas:

* [Executar tarefas de pré-requisito](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/target-requirements.html): Registre-se no Adobe Target e configure determinados aspectos da instância do autor do AEM. Sua conta do Adobe Target deve ter **aprovador** permissões de nível mínimo. Além disso, você deve proteger as configurações de atividade no nó de publicação para que ele fique inacessível aos usuários.

* O Launch by Adobe é a ferramenta de fato para instrumentar um site AEM com recursos do Target (bibliotecas JS). Portanto, a integração AEM as a Cloud Service com o Launch e o Adobe Target está intimamente disponível (consulte os links abaixo).

   * [Integração com o Adobe Target usando o Adobe I/O](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/integration-ims-adobe-io.html)
   * [Integrar o Launch by Adobe](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/adobe-launch-integration-tutorial-understand.html)
   * [Integrar AEM com o Adobe Launch via Adobe I/O](https://helpx.adobe.com/experience-manager/using/aem_launch_adobeio_integration.html)
   * [Noções básicas sobre a integração do AEM com o Launch by Adobe, Analytics e Target](https://helpx.adobe.com/experience-manager/kt/integration/using/aem-launch-integration-tutorial-understand.html)

>[!NOTE]
>
>A configuração IMS (contas técnicas) do Launch by Adobe é pré-configurada AEM as a Cloud Service. Os usuários não precisam criar essa configuração.

1. [Configurar atividades](https://experienceleague.adobe.com/docs/experience-manager-65/authoring/personalization/activitylib.html): Associe suas atividades à configuração de nuvem do Target.

>[!CAUTION]
>
>Em AEM as a Cloud Service, o agente de replicação que sincroniza Ofertas e Atividades do AEM para o Adobe Target é desativado por padrão. Entre em contato com o [Suporte a Adobe](https://helpx.adobe.com/contact/enterprise-support.ec.html#experience-manager) equipe se você precisar reativar o agente de replicação.

>[!NOTE]
>
>Se você estiver usando o Target com uma configuração de proxy personalizada, precisará configurar ambas as configurações de proxy do cliente HTTP, pois algumas funcionalidades do AEM estão usando as APIs 3.x e outras as APIs 4.x:
>
>* 3.x está configurado com [http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
>* 4.x está configurado com [http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)
>


>[!CAUTION]
>
>Você deve proteger o nó de configurações da atividade **cq:ActivitySettings** na instância de publicação, para que ela fique inacessível aos usuários normais. O nó de configurações de atividade só deve estar acessível ao serviço que lida com a sincronização de atividades com o Adobe Target.
>
>Consulte [Pré-requisitos para integração com o Adobe Target](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/target-requirements.html#securing-the-activity-settings-node) para obter informações detalhadas.

Quando a integração for concluída, você poderá [criar conteúdo direcionado](https://experienceleague.adobe.com/docs/experience-manager-65/authoring/personalization/content-targeting-touch.html) que envia dados do visitante para a Adobe Target. Observe que os componentes da página exigem um código específico para ativar o direcionamento de conteúdo. (Consulte [Desenvolvimento de conteúdo direcionado](https://experienceleague.adobe.com/docs/experience-manager-65/developing/personlization/target.html).

>[!NOTE]
>
>Quando você direciona um componente em AEM autor, o componente faz uma série de chamadas do lado do servidor para o Adobe Target para registrar a campanha, configurar ofertas e recuperar segmentos do Adobe Target (se configurado). Nenhuma chamada do lado do servidor é feita AEM publicação no Adobe Target.

## Fontes de informações de fundo {#background-information-sources}

Integrar AEM as a Cloud Service com o Adobe Target requer conhecimento do Adobe Target, gerenciamento de atividades AEM e gerenciamento de AEM públicos-alvo. Familiarize-se com as seguintes informações:

* Adobe Target (consulte a [Documentação do Adobe Target](https://experienceleague.adobe.com/docs/target/using/target-home.html)).
* Console Atividades AEM (consulte [Gerenciamento de atividades](https://experienceleague.adobe.com/docs/experience-manager-65/authoring/personalization/activitylib.html).
* Públicos-alvo AEM (consulte [Gerenciamento de públicos-alvo](https://experienceleague.adobe.com/docs/experience-manager-65/authoring/personalization/managing-audiences.html).

>[!NOTE]
>
>Ao trabalhar com o Adobe Target, o número máximo de artefatos permitidos em uma campanha é o seguinte:
>
>* 50 locais
>* 2.000 experiências
>* 50 métricas
>* 50 segmentos de relatórios

