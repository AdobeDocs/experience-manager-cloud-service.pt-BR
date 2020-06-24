---
title: Integração com o Adobe Target
description: 'Integração com o Adobe Target '
translation-type: tm+mt
source-git-commit: bffc335fdafe6bf12a66bcd2f7aacf029fce567e
workflow-type: tm+mt
source-wordcount: '743'
ht-degree: 4%

---


# Integração com o Adobe Target{#integrating-with-adobe-target}

Como parte do Adobe Marketing Cloud, o [Adobe Target](http://www.adobe.com/solutions/testing-targeting/testandtarget.html) permite aumentar a relevância do conteúdo por meio da definição de metas e medição em todos os canais. O Adobe Target é usado pelos comerciantes para projetar e executar testes online, criar segmentos de audiência instantâneos (com base no comportamento) e automatizar a definição de metas de conteúdo e experiências online. O AEM como Cloud Service adotou o fluxo de trabalho de definição de metas usado no Adobe Target Standard. Se você usar o Target, estará familiarizado com o ambiente de edição de definição de metas no AEM como Cloud Service.

Integre seus sites do AEM com a Adobe Target para personalizar conteúdo em suas páginas:

* Implemente a definição de metas de conteúdo.
* Use audiências de Públicos alvos para criar experiências personalizadas.
* Envie dados de contexto ao Público alvo quando os visitantes interagirem com suas páginas.
* Rastrear taxas de conversão.

>[!NOTE]
>
>Adobe Experience Manager como clientes Cloud Service que não têm uma conta de Público alvo existente, podem solicitar acesso ao Target Foundation Pack para Experience Cloud.  O Foundation Pack fornece utilização limitada em volume do Público alvo.


Para integrar ao Público alvo, execute as seguintes tarefas:

* [Execute tarefas](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/target-requirements.html)de pré-requisito: Registre-se no Adobe Target e configure certos aspectos da instância do autor de AEM. A sua conta de Adobe Target deve ter, no mínimo, permissões de nível de **aprovador** . Além disso, você deve proteger as configurações de atividade no nó de publicação para que ele fique inacessível aos usuários.

* O Launch da Adobe é a ferramenta de fato para instrumentar um site do AEM com recursos de Público alvo (bibliotecas JS). Portanto, a integração do AEM como um Cloud Service com o Launch e o Adobe Target é acompanhada (consulte os links abaixo).

   * [Integração com o Adobe Target usando E/S da Adobe](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/integration-ims-adobe-io.html)
   * [Integrar lançamento pela Adobe](https://docs.adobe.com/content/help/en/experience-manager-learn/sites/integrations/adobe-launch-integration-tutorial-understand.html)
   * [Integrar o AEM ao Adobe Launch via E/S da Adobe](https://helpx.adobe.com/experience-manager/using/aem_launch_adobeio_integration.html)
   * [Como entender a integração do AEM com o Launch da Adobe, Analytics e Público alvo](https://helpx.adobe.com/experience-manager/kt/integration/using/aem-launch-integration-tutorial-understand.html)

>[!NOTE]
>
>A configuração do IMS (contas técnicas) para o Launch da Adobe é pré-configurada no AEM como um Cloud Service. Os usuários não precisam criar essa configuração.

1. [Configurar Atividades](https://docs.adobe.com/content/help/en/experience-manager-65/authoring/personalization/activitylib.html): Associe suas Atividades à configuração da nuvem do Público alvo.

>[!CAUTION]
>
>No AEM como um Cloud Service, o agente de replicação que sincroniza Ofertas e Atividades do AEM com o Adobe Target está desativado por padrão. Entre em contato com a equipe de suporte [da](https://helpx.adobe.com/contact/enterprise-support.ec.html#experience-manager) Adobe se precisar reativar o agente de replicação.

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

Quando a integração estiver concluída, você poderá [criar conteúdo](https://docs.adobe.com/content/help/en/experience-manager-65/authoring/personalization/content-targeting-touch.html) direcionado que envie dados do visitante para o Adobe Target. Observe que os componentes da página exigem um código específico para permitir a definição de metas de conteúdo. (Consulte [Desenvolvimento de conteúdo](https://docs.adobe.com/content/help/en/experience-manager-65/developing/personlization/target.html)direcionado.

>[!NOTE]
>
>Quando você público alvo um componente no autor de AEM, o componente faz uma série de chamadas do lado do servidor para o Adobe Target para registrar a campanha, configurar o oferta e recuperar segmentos de Adobe Target (se configurado). Nenhuma chamada do lado do servidor é feita da publicação do AEM para o Adobe Target.

## Fontes de informações de plano de fundo {#background-information-sources}

A integração do AEM como um Cloud Service com o Adobe Target exige conhecimento sobre Adobe Target, gerenciamento do AEM Atividade e gerenciamento do AEM Audiência. Familiarize-se com as seguintes informações:

* Adobe Target (Consulte a documentação [do](https://docs.adobe.com/content/help/en/target/using/target-home.html)Adobe Target).
* Console do AEM Atividade (consulte [Gerenciamento de Atividade](https://docs.adobe.com/content/help/en/experience-manager-65/authoring/personalization/activitylib.html).
* Audiências AEM (consulte [Gerenciamento de Audiências](https://docs.adobe.com/content/help/en/experience-manager-65/authoring/personalization/managing-audiences.html).

>[!NOTE]
>
>Ao trabalhar com Adobe Target, o número máximo de artefatos permitidos em uma campanha é o seguinte:
>
>* 50 locais
>* 2.000 experiências
>* 50 métricas
>* 50 segmentos de relatórios

>


