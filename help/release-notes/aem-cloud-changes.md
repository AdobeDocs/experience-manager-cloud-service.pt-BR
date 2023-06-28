---
title: Alterações importantes no Adobe Experience Manager (AEM) as a Cloud Service
description: Alterações importantes no Adobe Experience Manager (AEM) as a Cloud Service
exl-id: fe11d779-66cd-45aa-aa6b-c819b88d2405
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '846'
ht-degree: 95%

---

# Alterações importantes no Adobe Experience Manager (AEM) as a Cloud Service {#notable-changes-aem-cloud}

O AEM Cloud Service oferece muitos novos recursos e possibilidades para gerenciar os projetos do AEM. No entanto, existem várias diferenças entre o AEM Sites no local ou no Adobe Managed Services, em comparação ao AEM Cloud Service. Este documento destaca as diferenças importantes.

>[!CONTEXTUALHELP]
>id="aem_cloud_notable_changes"
>title="Alterações importantes no AEM as a Cloud Service"
>abstract="Nesta guia, é possível visualizar o conteúdo que o ajudará a entender as diferenças entre o AEM no local, ou no Adobe Managed Services, e o AEM as a Cloud Service."
>additional-url="https://video.tv.adobe.com/v/330543" text="Evolução do AEM as a Cloud Service"


>[!NOTE]
>Este documento destaca as alterações importantes no AEM como um todo. Para obter mais informações e conhecer as alterações específicas da solução, consulte:
>
>* [Introdução ao Adobe Experience Manager as a Cloud Service](/help/overview/introduction.md)
>* [Novidades e diferenças](/help/overview/what-is-new-and-different.md) entre o Adobe Experience Manager as a Cloud Service e as versões anteriores
>* A [Arquitetura](/help/overview/architecture.md) do Adobe Experience Manager as a Cloud Service
>* [Alterações importantes no AEM Sites as a Cloud Service](/help/sites-cloud/sites-cloud-changes.md)
>* [Alterações importantes no AEM Assets as a Cloud Service](/help/assets/assets-cloud-changes.md)

As principais diferenças encontram-se nas seguintes áreas:

* [/apps e /libs não mudam no tempo de execução](#apps-libs-immutable)

* [Pacotes e configurações de OSGi devem ser tratados como código](#osgi)

* [Não são permitidas alterações no repositório de publicação](#changes-to-publish-repo)

* [Não são permitidos modos de execução personalizados](#custom-runmodes)

* [Remoção dos agentes de replicação e alterações relacionadas](#replication-agents)

* [Remoção da interface clássica do usuário ](#classic-ui)

* [Entrega do lado da publicação](#publish-side-delivery)

* [Manuseio e entrega de ativos](#asset-handling)

## /apps e /libs não mudam no tempo de execução {#apps-libs-immutable}

O conteúdo e as subpastas em `/apps` e `/libs` são somente leitura. Não é possível fazer alterações nesses locais com recursos ou códigos personalizados. É retornado um erro de que esse conteúdo é somente leitura e que não foi possível concluir a operação de gravação. Isso tem impacto em várias áreas do AEM:

* Não são permitidas alterações em `/libs` de forma alguma.
   * Essa não é uma regra nova, no entanto, não foi aplicada nas versões anteriores do AEM no local.
* Sobreposições para áreas em `/libs` que podem ser sobrepostas ainda são permitidas dentro de `/apps`.
   * Essas sobreposições devem vir do Git por meio do pipeline de CI/CD.
* As informações de design do modelo estático armazenadas no `/apps` não podem ser editadas por meio da interface do usuário.
   * É recomendável usar Modelos editáveis.
   * Se os Modelos estáticos ainda forem obrigatórios, as informações de configuração devem vir do Git por meio do pipeline de CI/CD.
* As configurações de implantação de MSM Blueprint e MSM personalizado devem ser instaladas no Git por meio do pipeline de CI/CD.
* As mudanças na tradução de I18n precisam vir do Git por meio do pipeline de CI/CD.

## Pacotes e configurações de OSGi devem ser tratados como código {#osgi}

As alterações nos pacotes e configurações OSGi devem ser introduzidas por meio do pipeline de CI/CD.

* Os pacotes OSGi novos ou atualizados devem ser introduzidos por meio do Git, através do pipeline de CI/CD.
* As alterações nas configurações de OSGi só podem vir do Git por meio do pipeline de CI/CD.

O console da Web, usado nas versões anteriores do AEM para alterar pacotes e configurações de OSGi, não está disponível no AEM Cloud Service.

## Não são permitidas alterações no repositório de publicação {#changes-to-publish-repo}

Além das alterações na pasta `/home` no nível de publicação, alterações diretas no repositório de publicação não são permitidas no AEM Cloud Service. Em versões anteriores do AEM no local ou AEM no AMS, as alterações de código poderiam ser feitas diretamente no repositório de publicação. Algumas limitações podem ser atenuadas das seguintes formas:

* Para configuração de conteúdo e baseada em conteúdo: faça as alterações na instância de criação e as publique.
* Para código e configuração: faça as alterações no repositório de GIT e execute o pipeline de CI/CD para implementá-las.

## Não são permitidos modos de execução personalizados {#custom-runmodes}

Os seguintes modos de execução são fornecidos prontos para uso no AEM Cloud Service:

* `author`
* `publish`
* `prod`
* `author.prod`
* `publish.prod`
* `stage`
* `author.stage`
* `publish.stage`
* `dev`
* `author.dev`
* `publish.dev`

Modos de execução adicionais ou personalizados não são possíveis no AEM Cloud Service.

## Remoção dos agentes de replicação e alterações relacionadas {#replication-agents}

No AEM Cloud Service, o conteúdo é publicado usando a [Distribuição de conteúdo de sling](https://sling.apache.org/documentation/bundles/content-distribution.html). Os agentes de replicação usados nas versões anteriores do AEM não são mais usados ou fornecidos, o que pode afetar as seguintes áreas dos projetos atuais do AEM:

* Fluxos de trabalho personalizados que enviam conteúdo para agentes de replicação dos servidores de visualização, por exemplo.
* Personalização dos agentes de replicação para transformar conteúdo
* Uso de Replicação reversa para devolver o conteúdo da publicação para o autor

Além disso, observe que os botões Pausar e Desativar foram removidos do console de administração do agente de replicação.

## Remoção da interface clássica do usuário {#classic-ui}

A interface clássica do usuário não está mais disponível no AEM Cloud Service.

## Entrega do lado da publicação {#publish-side-delivery}

A aceleração HTTP, incluindo o CDN e o gerenciamento de tráfego para os serviços de criação e publicação, é fornecida por padrão no AEM Cloud Service.

Para a transição de projetos do AMS ou de uma instalação local, a Adobe recomenda utilizar a CDN integrada, pois os recursos do AEM Cloud Service são otimizados para a CDN fornecida.

## Manuseio e entrega de ativos {#asset-handling}

O upload, processamento e download de ativos estão otimizados no [!DNL Experience Manager Assets] as a [!DNL Cloud Service]. Agora, o [!DNL Assets] é mais eficiente, permite maior dimensionamento e possibilita uploads e downloads muito mais rápidos. Além disso, isso afeta o código personalizado existente e algumas operações. Para uma lista de alterações e para paridade com os recursos do [!DNL Experience Manager] 6.5, consulte as [alterações do  [!DNL Assets]](/help/assets/assets-cloud-changes.md).
