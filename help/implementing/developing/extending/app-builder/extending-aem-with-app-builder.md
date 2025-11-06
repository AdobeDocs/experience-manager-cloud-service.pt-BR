---
title: Estendendo o as a Cloud Service [!DNL Adobe Experience Manager] usando o Adobe Developer App Builder.
description: Estendendo o as a Cloud Service [!DNL Adobe Experience Manager] usando o Adobe Developer App Builder.
exl-id: 50d82745-5deb-4bfa-961b-714842403601
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '488'
ht-degree: 0%

---

# Extensão do as a Cloud Service [!DNL Adobe Experience Manager] usando o Adobe Developer App Builder {#extend-using-app-builder}

## O que é o App Builder para AEM as a Cloud Service {#project-appbuilder}

O novo Adobe Developer App Builder fornece uma estrutura de extensibilidade para que um desenvolvedor estenda facilmente as funcionalidades no AEM as a Cloud Service.

O App Builder fornece uma estrutura unificada de extensibilidade de terceiros para integrar e criar experiências personalizadas que estendem o Adobe Experience Manager. Com essa estrutura completa de extensibilidade, criada na infraestrutura da Adobe, os desenvolvedores podem criar microsserviços personalizados, estender e integrar o Adobe Experience Manager às soluções da Adobe e ao restante da pilha de TI.

O App Builder fornece uma maneira de os clientes estenderem facilmente o Adobe Experience Manager em vários casos de uso:

* Extensibilidade de middleware - Conecte sistemas externos com aplicativos Adobe criando conectores personalizados ou use um conjunto de integrações pré-construídas.
* Extensibilidade dos principais serviços - Amplie os principais recursos do aplicativo estendendo o comportamento padrão com recursos personalizados e lógica de negócios.
* Extensibilidade de experiência do usuário - Amplie a experiência principal para atender aos requisitos comerciais ou criar propriedades digitais específicas do cliente, vitrines e aplicativos de back-office.

>[!NOTE]
>
> Para clientes do AEM 6.5 que desejam usar o App Builder, consulte [Extensão do Adobe Experience Manager 6.5 usando o Adobe Developer App Builder](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/app-builder.html?lang=pt-BR).

## Arquitetura {#architecture}

Em vez de uma solução pronta para uso, a Adobe Developer App Builder fornece uma plataforma de desenvolvimento comum, consistente e padronizada para estender as soluções da Adobe Cloud, como o AEM, incluindo:

* Adobe Developer Console - Para microsserviços personalizados e desenvolvimento de extensão, permite que os desenvolvedores criem e gerenciem projetos enquanto acessam todas as ferramentas e APIs necessárias para que possam criar plug-ins e integrações.
* Ferramentas do desenvolvedor - Ferramentas de código aberto, SDKs e bibliotecas para permitir que os desenvolvedores criem facilmente extensões e integrações personalizadas. Use o React Spectrum (kit de ferramentas da interface do usuário da Adobe) para que você tenha uma interface de usuário comum para todos os aplicativos da Adobe.
* Serviços - I/O Runtime para infraestrutura de hospedagem na plataforma sem servidor da Adobe e Eventos de I/O para integrações baseadas em eventos. A Adobe também oferece suporte pronto para armazenar dados e arquivos.
* Adobe Experience Cloud - Os desenvolvedores podem enviar extensões e integrações para publicação em sua organização da Experience Cloud. Em seguida, os administradores do sistema podem revisar, gerenciar e aprovar essas extensões. Depois de publicadas, suas ferramentas e extensões personalizadas do App Builder podem ser encontradas junto com outros aplicativos da Adobe Experience Cloud.

O diagrama a seguir ilustra como um aplicativo padrão criado no App Builder usa essas funcionalidades:

![Arquitetura](/help/implementing/developing/extending/assets/appbuilder-architecture.jpg)

Para obter mais detalhes sobre a arquitetura do App Builder, consulte [Visão geral da arquitetura.](https://developer.adobe.com/app-builder/docs/guides/app_builder_guides/architecture_overview/architecture-overview)

## Introdução ao App Builder {#additional-resources}

A Adobe criou a documentação de Introdução para que você possa começar a usar o App Builder:

* [Introdução ao App Builder](https://developer.adobe.com/app-builder/docs/getting_started/)

## Continue aprendendo com a documentação {#appbuilder-documentation}

O App Builder fornece vídeos e documentação para desenvolvedores, incluindo guias e documentação de referência para ajudar você a começar a desenvolver seus próprios aplicativos personalizados:

* [Documentação do App Builder](https://developer.adobe.com/app-builder/docs/overview/)
* [Vídeos do App Builder](https://www.youtube.com/playlist?list=PLcVEYUqU7VRfDij-Jbjyw8S8EzW073F_o)

## Experimente um dos aplicativos de amostra {#appbuilder-codesamples}

Pronto para começar a desenvolver? O Adobe tem vários aplicativos de exemplo para ajudá-lo a começar rapidamente:

* [App Builder Code Labs no site da Adobe Developer](https://developer.adobe.com/app-builder/docs/resources/)