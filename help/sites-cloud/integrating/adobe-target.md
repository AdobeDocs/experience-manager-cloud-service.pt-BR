---
title: Integração com o Adobe Target
description: Integração com o Adobe Target
exl-id: 2b4cf35e-2b75-4303-8d09-f6644ad99274
source-git-commit: 65e1ede4cdc8035657e8b37fe206ebed4ab7bb24
workflow-type: ht
source-wordcount: '723'
ht-degree: 100%

---

# Integração com o Adobe Target{#integrating-with-adobe-target}

Como parte da Adobe Marketing Cloud, o [Adobe Target](http://www.adobe.com/solutions/testing-targeting/testandtarget.html) permite aumentar a relevância do conteúdo por meio do direcionamento e da medição em todos os canais. O Adobe Target é usado pelos profissionais de marketing para projetar e executar testes online, criar segmentos de público instantaneamente (com base no comportamento) e automatizar o direcionamento de conteúdo e experiências online. O AEM as a Cloud Service adotou o fluxo de trabalho direcionado usado no Adobe Target Standard. Se você usa o Target, estará familiarizado com o ambiente de edição de direcionamento do AEM as a Cloud Service.

Integre o AEM Sites com o Adobe Target para personalizar o conteúdo em suas páginas:

* Implemente o direcionamento de conteúdo.
* Use os públicos do Target para criar experiências personalizadas.
* Envie dados de contexto para o Target quando os visitantes interagirem com suas páginas.
* Rastreie as taxas de conversão.

>[!NOTE]
>
>Os clientes do Adobe Experience Manager as a Cloud Service que não têm uma conta do Target existente podem solicitar acesso ao Target Foundation Pack para a Experience Cloud.  O Foundation Pack fornece uso limitado por volume do Target.


Para integrar com o Target, execute as seguintes tarefas:

* [Execute as tarefas de pré-requisito](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/target-requirements.html?lang=pt-BR): registre-se no Adobe Target e configure determinados aspectos da instância de autor do AEM. Sua conta do Adobe Target deve ter no mínimo o nível de permissão **aprovador**. Além disso, você deve proteger as configurações de atividade no nó de publicação para que elas fiquem inacessíveis aos usuários.

* O Launch by Adobe é a ferramenta padrão para instrumentar um site do AEM com recursos do Target (bibliotecas JS). Portanto, a integração do AEM as a Cloud Service com o Launch e o Adobe Target está intimamente relacionada (consulte os links abaixo).

   * [Integração com o Adobe Target usando o Adobe I/O](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/integration-target-ims.html?lang=pt-BR)
   * [Integrar o Launch by Adobe](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-launch/overview.html?lang=pt-BR)
   * [Integrar o AEM com o Adobe Launch via Adobe I/O](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-launch/overview.html?lang=pt-BR)
   * [Noções básicas sobre a integração do AEM com o Launch by Adobe, Analytics e Target](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-launch/overview.html?lang=pt-BR)

>[!NOTE]
>
>A configuração do IMS (contas técnicas) do Launch by Adobe é pré-configurada no AEM as a Cloud Service. Os usuários não precisam criar essa configuração.

1. [Configurar atividades](https://experienceleague.adobe.com/docs/experience-manager-65/authoring/personalization/activitylib.html?lang=pt-BR): associe suas atividades à configuração de nuvem do Target.

>[!CAUTION]
>
>No AEM as a Cloud Service, o agente de replicação que sincroniza as Ofertas e Atividades do AEM para o Adobe Target é desativado por padrão. Entre em contato com a equipe de [Suporte da Adobe](https://helpx.adobe.com/br/contact/enterprise-support.ec.html#experience-manager) se precisar reativar o agente de replicação.

>[!NOTE]
>
>Se você estiver usando o Target com uma configuração de proxy personalizada, precisará configurar ambas as configurações de proxy do cliente HTTP, pois algumas funcionalidades do AEM usam as APIs 3.x e outras usam as APIs 4.x:
>
>* A 3.x está configurada com [http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
>* A 4.x está configurada com [http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)
>


>[!CAUTION]
>
>Você deve proteger o nó de configurações de atividade **cq:ActivitySettings** na instância de publicação para que ele fique inacessível aos usuários normais. O nó de configurações de atividade só deve estar acessível ao serviço que lida com a sincronização de atividades com o Adobe Target.
>
>Consulte [Pré-requisitos para integração com o Adobe Target](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/target-requirements.html?lang=pt-BR#securing-the-activity-settings-node) para obter informações detalhadas.

Quando a integração for concluída, você poderá [criar conteúdo direcionado](https://experienceleague.adobe.com/docs/experience-manager-65/authoring/personalization/content-targeting-touch.html?lang=pt-BR) que envia dados do visitante para o Adobe Target. Observe que os componentes da página exigem um código específico para ativar o direcionamento de conteúdo. (Consulte [Desenvolvimento de conteúdo direcionado](https://experienceleague.adobe.com/docs/experience-manager-65/developing/personlization/target.html?lang=pt-BR).

>[!NOTE]
>
>Ao direcionar um componente no autor do AEM, o componente faz uma série de chamadas do lado do servidor para o Adobe Target registrar a campanha, configurar ofertas e recuperar segmentos do Adobe Target (se configurado). Nenhuma chamada do lado do servidor é feita do ambiente de publicação do AEM para o Adobe Target.

## Fontes de informações de segundo plano {#background-information-sources}

Integrar o AEM as a Cloud Service com o Adobe Target exige conhecimento do Adobe Target, de gerenciamento de Atividades do AEM e de gerenciamento de Públicos do AEM. Familiarize-se com as seguintes informações:

* Adobe Target (consulte a [documentação do Adobe Target](https://experienceleague.adobe.com/docs/target/using/target-home.html?lang=pt-BR)).
* Console de Atividades do AEM (consulte [Gerenciamento de atividades](https://experienceleague.adobe.com/docs/experience-manager-65/authoring/personalization/activitylib.html?lang=pt-BR).
* Públicos do AEM (consulte [Gerenciamento de públicos](https://experienceleague.adobe.com/docs/experience-manager-65/authoring/personalization/managing-audiences.html?lang=pt-BR).

>[!NOTE]
>
>Ao trabalhar com o Adobe Target, o número máximo de artefatos permitidos em uma campanha é o seguinte:
>
>* 50 locais
>* 2.000 experiências
>* 50 métricas
>* 50 segmentos de relatórios

