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

Como parte do Adobe Marketing Cloud, [Adobe Target](http://www.adobe.com/solutions/testing-targeting/testandtarget.html) permite aumentar a relevância do conteúdo por meio da definição de metas e da medição em todos os canais. A Adobe Target é usada pelos comerciantes para projetar e executar testes online, criar segmentos de audiência instantâneos (com base no comportamento) e automatizar a definição de metas de conteúdo e experiências online. AEM como Cloud Service adotou o fluxo de trabalho de definição de metas usado no Adobe Target Standard. Se você usar o Público alvo, você estará familiarizado com o ambiente de edição de definição de metas no AEM como um Cloud Service.

Integre seus sites de AEM com o Adobe Target para personalizar o conteúdo em suas páginas:

* Implemente a definição de metas de conteúdo.
* Use audiências de Públicos alvos para criar experiências personalizadas.
* Envie dados de contexto ao Público alvo quando os visitantes interagirem com suas páginas.
* Rastrear taxas de conversão.

>[!NOTE]
>
>A Adobe Experience Manager como cliente Cloud Service que não tem uma conta de Público alvo existente pode solicitar acesso ao Público alvo Foundation Pack para Experience Cloud.  O Foundation Pack fornece utilização limitada em volume do Público alvo.


Para integrar ao Público alvo, execute as seguintes tarefas:

* [Execute tarefas](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/target-requirements.html) de pré-requisito: Registre-se no Adobe Target e configure certos aspectos da instância do autor AEM. Sua conta Adobe Target deve ter no mínimo **aprover** permissões de nível. Além disso, você deve proteger as configurações de atividade no nó de publicação para que ele fique inacessível aos usuários.

* Launch by Adobe é a ferramenta de fato para instrumentar um site AEM com recursos de Público alvo (bibliotecas JS). Portanto, a integração do AEM como Cloud Service com o Launch e o Adobe Target é acompanhada (veja os links abaixo).

   * [Integração com a Adobe Target usando o Adobe I/O](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/integration-ims-adobe-io.html)
   * [Integrar Launch by Adobe](https://docs.adobe.com/content/help/en/experience-manager-learn/sites/integrations/adobe-launch-integration-tutorial-understand.html)
   * [Integrar AEM com o lançamento do Adobe via Adobe I/O](https://helpx.adobe.com/experience-manager/using/aem_launch_adobeio_integration.html)
   * [Como entender AEM integração com Launch by Adobe, Analytics e Públicos alvos](https://helpx.adobe.com/experience-manager/kt/integration/using/aem-launch-integration-tutorial-understand.html)

>[!NOTE]
>
>A configuração IMS (contas técnicas) para Launch by Adobe é pré-configurada em AEM como um Cloud Service. Os usuários não precisam criar essa configuração.

1. [Configurar Atividades](https://docs.adobe.com/content/help/en/experience-manager-65/authoring/personalization/activitylib.html): Associe suas Atividades à configuração da nuvem do Público alvo.

>[!CAUTION]
>
>Em AEM como Cloud Service, o agente de replicação que sincroniza Ofertas e Atividades de AEM para Adobe Target é desativado por padrão. Entre em contato com a equipe [Suporte ao Adobe](https://helpx.adobe.com/contact/enterprise-support.ec.html#experience-manager) se precisar reativar o agente de replicação.

>[!NOTE]
>
>Se você estiver usando um Público alvo com uma configuração de proxy personalizada, precisará configurar ambas as configurações de proxy do Cliente HTTP, já que algumas funcionalidades do AEM estão usando as APIs 3.x e outras as APIs 4.x:
>
>* O 3.x está configurado com [http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
>* O 4.x está configurado com [http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)

>



>[!CAUTION]
>
>É necessário proteger o nó de configurações de atividade **cq:ActivitySettings** na instância de publicação para que ele fique inacessível aos usuários normais. O nó de configurações de atividade só deve estar acessível ao serviço que lida com a sincronização de atividades com o Adobe Target.
>
>Consulte [Pré-requisitos para integração com o Adobe Target](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/target-requirements.html#securing-the-activity-settings-node) para obter informações detalhadas.

Quando a integração estiver concluída, você poderá [criar conteúdo direcionado](https://docs.adobe.com/content/help/en/experience-manager-65/authoring/personalization/content-targeting-touch.html) que envia dados do visitante para a Adobe Target. Observe que os componentes da página exigem um código específico para permitir a definição de metas de conteúdo. (Consulte [Desenvolvimento para conteúdo direcionado](https://docs.adobe.com/content/help/en/experience-manager-65/developing/personlization/target.html).

>[!NOTE]
>
>Quando você público alvo um componente AEM autor, o componente faz uma série de chamadas do lado do servidor para a Adobe Target para registrar a campanha, configurar o oferta e recuperar segmentos Adobe Target (se configurado). Nenhuma chamada do lado do servidor é feita AEM publicação para a Adobe Target.

## Fontes de informações de plano de fundo {#background-information-sources}

Integrar AEM como Cloud Service com a Adobe Target requer conhecimento da Adobe Target, gerenciamento AEM e gerenciamento AEM Audiência. Familiarize-se com as seguintes informações:

* Adobe Target (Consulte a [documentação do Adobe Target](https://docs.adobe.com/content/help/en/target/using/target-home.html)).
* AEM console do Atividade (Consulte [Gerenciando Atividade](https://docs.adobe.com/content/help/en/experience-manager-65/authoring/personalization/activitylib.html).
* AEM Audiência (Consulte [Gerenciando Audiência](https://docs.adobe.com/content/help/en/experience-manager-65/authoring/personalization/managing-audiences.html).

>[!NOTE]
>
>Ao trabalhar com a Adobe Target, o número máximo de artefatos permitidos em uma campanha é o seguinte:
>
>* 50 locais
>* 2.000 experiências
>* 50 métricas
>* 50 segmentos de relatórios

>


