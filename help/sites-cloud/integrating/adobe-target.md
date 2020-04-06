---
title: Integração com o Adobe Target
description: 'Integração com o Adobe Target '
translation-type: tm+mt
source-git-commit: 518c3156b2ee1f6431ea11333c57548a42133aa9

---


# Integração com o Adobe Target{#integrating-with-adobe-target}

Como parte da Adobe Marketing Cloud, o [Adobe Público alvo](http://www.adobe.com/solutions/testing-targeting/testandtarget.html) permite aumentar a relevância do conteúdo por meio da definição de metas e da medição em todos os canais. O Público alvo da Adobe é usado pelos comerciantes para projetar e executar testes online, criar segmentos de audiência instantâneos (com base no comportamento) e automatizar a definição de metas de conteúdo e experiências online. O AEM como um serviço em nuvem adotou o fluxo de trabalho de definição de metas usado no Adobe Público alvo Standard. Se você usar o Público alvo, estará familiarizado com o ambiente de edição de definição de metas no AEM como um serviço em nuvem.

Integre seus sites do AEM ao Público alvo da Adobe para personalizar conteúdo em suas páginas:

* Implemente a definição de metas de conteúdo.
* Use audiências de Públicos alvos para criar experiências personalizadas.
* Envie dados de contexto ao Público alvo quando os visitantes interagirem com suas páginas.
* Rastrear taxas de conversão.

>[!NOTE]
>
>O Adobe Experience Manager como cliente do Cloud Service que não tem uma conta de Público alvo existente pode solicitar acesso ao Público alvo Foundation Pack para a Experience Cloud.  O Foundation Pack fornece utilização limitada em volume do Público alvo.


Para integrar ao Público alvo, execute as seguintes tarefas:

* [Execute tarefas](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/target-requirements.html)de pré-requisito: Registre-se no Público alvo da Adobe e configure certos aspectos da instância do autor do AEM. Sua conta de Público alvo da Adobe deve ter, no mínimo, permissões de nível de **aprovador** . Além disso, você deve proteger as configurações de atividade no nó de publicação para que ele fique inacessível aos usuários.

* O Launch da Adobe é a ferramenta de fato para instrumentar um site do AEM com recursos de Público alvo (bibliotecas JS). Portanto, a integração do AEM como um serviço em nuvem com o Launch e o Público alvo da Adobe é fornecida em conjunto (consulte os links abaixo).

   * [Integração com o Público alvo da Adobe usando E/S da Adobe](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/integration-ims-adobe-io.html)
   * [Integrar lançamento pela Adobe](https://docs.adobe.com/content/help/en/experience-manager-learn/sites/integrations/adobe-launch-integration-tutorial-understand.html)
   * [Integrar o AEM ao Adobe Launch via E/S da Adobe](https://helpx.adobe.com/experience-manager/using/aem_launch_adobeio_integration.html)
   * [Como entender a integração do AEM com o Launch da Adobe, do Analytics e do Público alvo](https://helpx.adobe.com/experience-manager/kt/integration/using/aem-launch-integration-tutorial-understand.html)

1. [Configurar Atividades](https://docs.adobe.com/content/help/en/experience-manager-65/authoring/personalization/activitylib.html): Associe suas Atividades à configuração da nuvem do Público alvo.

>[!NOTE]
>
>A configuração do IMS (contas técnicas) para o Launch da Adobe é pré-configurada no AEM como um serviço em nuvem. Os usuários não precisam criar essa configuração.

>[!NOTE]
>
>Se você estiver usando um Público alvo com uma configuração de proxy personalizada, precisará configurar ambas as configurações de proxy do Cliente HTTP, já que algumas funcionalidades do AEM estão usando as APIs 3.x e outras as APIs 4.x:
>
>* 3.x é configurado com [http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
>* 4.x é configurado com [http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)
>



>[!CAUTION]
>
>You must secure the activity settings node **cq:ActivitySettings** on the publish instance so that it is inaccessible to normal users. O nó de configurações de atividade só deve estar acessível ao serviço que lida com a sincronização de atividades com o Adobe Target.
>
>See [Prerequisites for Integrating with Adobe Target](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/target-requirements.html#securing-the-activity-settings-node) for detailed information.

Quando a integração estiver concluída, você poderá [criar conteúdo](https://docs.adobe.com/content/help/en/experience-manager-65/authoring/personalization/content-targeting-touch.html) direcionado que envie dados do visitante para o Adobe Público alvo. Observe que os componentes da página exigem um código específico para permitir a definição de metas de conteúdo. (Consulte [Desenvolvimento de conteúdo](https://docs.adobe.com/content/help/en/experience-manager-65/developing/personlization/target.html)direcionado.

>[!NOTE]
>
>Quando você público alvo um componente no autor de AEM, o componente faz uma série de chamadas do lado do servidor para o Adobe Público alvo para registrar a campanha, configurar o oferta e recuperar segmentos do Público alvo da Adobe (se configurado). Nenhuma chamada do lado do servidor é feita da publicação do AEM para o Adobe Público alvo.

## Fontes de informações de plano de fundo {#background-information-sources}

A integração do AEM como um serviço em nuvem com o Público alvo da Adobe exige conhecimento do Público alvo da Adobe, gerenciamento do AEM Atividade e gerenciamento do AEM Audiência. Familiarize-se com as seguintes informações:

* Público alvo da Adobe (consulte a documentação [do Público alvo](https://marketing.adobe.com/resources/help/en_US/target/)da Adobe).
* Console do AEM Atividade (consulte [Gerenciamento de Atividade](https://docs.adobe.com/content/help/en/experience-manager-65/authoring/personalization/activitylib.html).
* Audiências AEM (consulte [Gerenciamento de Audiências](https://docs.adobe.com/content/help/en/experience-manager-65/authoring/personalization/managing-audiences.html).

>[!NOTE]
>
>Ao trabalhar com o Adobe Público alvo, a seguir está o número máximo de artefatos permitidos em uma campanha:
>
>* 50 locais
>* 2.000 experiências
>* 50 métricas
>* 50 segmentos de relatórios
>


