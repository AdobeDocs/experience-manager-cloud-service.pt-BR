---
title: Integração com o Adobe Target
description: 'Integração com o Adobe Target '
translation-type: tm+mt
source-git-commit: 518c3156b2ee1f6431ea11333c57548a42133aa9

---


# Integração com o Adobe Target{#integrating-with-adobe-target}

Como parte da Adobe Marketing Cloud, o [Adobe Target](http://www.adobe.com/solutions/testing-targeting/testandtarget.html) permite aumentar a relevância do conteúdo por meio da definição de metas e medição em todos os canais. O Adobe Target é usado por profissionais de marketing para projetar e executar testes online, criar segmentos de público-alvo instantâneos (com base no comportamento) e automatizar a definição de metas de conteúdo e experiências online. O AEM como um serviço em nuvem adotou o fluxo de trabalho de definição de metas usado no Adobe Target Standard. Se você usar o Target, você estará familiarizado com o ambiente de edição de definição de metas no AEM como um serviço de nuvem.

Integre seus sites do AEM ao Adobe Target para personalizar o conteúdo em suas páginas:

* Implemente a definição de metas de conteúdo.
* Use públicos-alvo do Target para criar experiências personalizadas.
* Envie dados de contexto ao Target quando os visitantes interagirem com suas páginas.
* Rastrear as taxas de conversão.

>[!NOTE]
>
>O Adobe Experience Manager como cliente do Cloud Service que não tem uma conta Target existente pode solicitar acesso ao Target Foundation Pack para a Experience Cloud.  O Foundation Pack fornece uso limitado por volume do Target.


Para integrar-se ao Target, execute as seguintes tarefas:

* [Execute tarefas](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/target-requirements.html)de pré-requisito: Registre-se no Adobe Target e configure certos aspectos da instância do autor do AEM. Sua conta do Adobe Target deve ter, no mínimo, permissões de nível de **aprovador** . Além disso, você deve proteger as configurações de atividade no nó de publicação para que ele fique inacessível aos usuários.

* O Launch da Adobe é a ferramenta de fato para instrumentar um site do AEM com recursos do Target (bibliotecas JS). Portanto, a integração do AEM como um serviço em nuvem com o Launch e o Adobe Target é fornecida em conjunto (consulte os links abaixo).

   * [Integração com o Adobe Target usando o Adobe I/O](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/integration-ims-adobe-io.html)
   * [Integrar lançamento pela Adobe](https://docs.adobe.com/content/help/en/experience-manager-learn/sites/integrations/adobe-launch-integration-tutorial-understand.html)
   * [Integrar o AEM ao Adobe Launch via E/S da Adobe](https://helpx.adobe.com/experience-manager/using/aem_launch_adobeio_integration.html)
   * [Como entender a integração do AEM com o Launch da Adobe, Analytics e Target](https://helpx.adobe.com/experience-manager/kt/integration/using/aem-launch-integration-tutorial-understand.html)

1. [Configurar atividades](https://docs.adobe.com/content/help/en/experience-manager-65/authoring/personalization/activitylib.html): Associe suas Atividades à configuração da nuvem do Target.

>[!NOTE]
>
>A configuração do IMS (contas técnicas) para o Launch da Adobe é pré-configurada no AEM como um serviço em nuvem. Os usuários não precisam criar essa configuração.

>[!NOTE]
>
>Se você estiver usando o Target com uma configuração de proxy personalizada, precisará configurar ambas as configurações de proxy do Cliente HTTP, já que algumas funcionalidades do AEM estão usando as APIs 3.x e outras as APIs 4.x:
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
>Quando você direciona um componente no autor de AEM, o componente faz uma série de chamadas do servidor para o Adobe Target para registrar a campanha, configurar ofertas e recuperar segmentos do Adobe Target (se configurado). Nenhuma chamada do lado do servidor é feita da publicação do AEM para o Adobe Target.

## Fontes de informações de plano de fundo {#background-information-sources}

A integração do AEM como um serviço em nuvem com o Adobe Target requer conhecimento do Adobe Target, gerenciamento de atividades do AEM e gerenciamento de públicos-alvo do AEM. Familiarize-se com as seguintes informações:

* Adobe Target (consulte a documentação [do](https://marketing.adobe.com/resources/help/en_US/target/)Adobe Target).
* Console de atividades do AEM (consulte [Gerenciamento de atividades](https://docs.adobe.com/content/help/en/experience-manager-65/authoring/personalization/activitylib.html).
* Públicos-alvo do AEM (consulte [Gerenciamento de públicos-alvo](https://docs.adobe.com/content/help/en/experience-manager-65/authoring/personalization/managing-audiences.html).

>[!NOTE]
>
>Ao trabalhar com o Adobe Target, o número máximo de artefatos permitidos em uma campanha é o seguinte:
>
>* 50 locais
>* 2.000 experiências
>* 50 métricas
>* 50 segmentos de relatório
>


