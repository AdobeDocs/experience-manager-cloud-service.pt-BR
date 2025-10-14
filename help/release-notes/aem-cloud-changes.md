---
title: Alterações importantes no Adobe Experience Manager (AEM) as a Cloud Service
description: Alterações importantes no Adobe Experience Manager (AEM) as a Cloud Service.
exl-id: fe11d779-66cd-45aa-aa6b-c819b88d2405
feature: Release Information
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '862'
ht-degree: 45%

---

# Alterações importantes no Adobe Experience Manager as a Cloud Service {#notable-changes-aem-cloud}

O Adobe Experience Manager (AEM) Cloud Service oferece muitos novos recursos e possibilidades para gerenciar os projetos do AEM. No entanto, existem algumas diferenças entre o AEM Sites no local ou no Adobe Managed Service, em comparação ao AEM Cloud Service. Este documento destaca as diferenças importantes.

>[!CONTEXTUALHELP]
>id="aem_cloud_notable_changes"
>title="Alterações importantes no AEM as a Cloud Service"
>abstract="Nesta guia, é possível acessar conteúdos que ajudarão você a entender as diferenças entre o uso local do AEM, e por meio do Adobe Managed Services, em comparação com o AEM as a Cloud Service."
>additional-url="https://video.tv.adobe.com/v/346178?captions=por_br" text="Evolução do AEM as a Cloud Service"


>[!NOTE]
>Este documento destaca as alterações importantes no AEM como um todo. Para obter mais informações e conhecer as alterações específicas de cada solução, consulte:
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

* [Modos de execução personalizados não são permitidos](#custom-runmodes)

* [Remoção dos agentes de replicação e alterações relacionadas](#replication-agents)

* [Remoção da interface clássica do usuário &#x200B;](#classic-ui)

* [Entrega do lado da publicação](#publish-side-delivery)

* [Manuseio e entrega de ativos](#asset-handling)

## /apps e /libs não mudam no tempo de execução {#apps-libs-immutable}

Qualquer conteúdo e subpastas em `/apps` e `/libs` são somente leitura. Falha ao fazer alterações nesses locais com recursos ou códigos personalizados. É retornado um erro com um aviso de que o conteúdo é do tipo somente leitura e informando que não foi possível concluir a operação de gravação. Isso tem impacto em várias áreas do AEM:

* Não são permitidas alterações em `/libs` de forma alguma.
   * Essa não é uma regra nova, no entanto, não foi aplicada nas versões anteriores do AEM no local.
* Sobreposições para áreas em `/libs` que podem ser sobrepostas ainda são permitidas dentro de `/apps`.
   * Essas sobreposições devem vir do Git por meio do pipeline de CI/CD.
* As informações de design do Modelo Estático armazenadas em `/apps` não podem ser editadas por meio da interface do usuário.
   * Em vez disso, é recomendado usar os modelos editáveis.
   * Se os Modelos estáticos ainda forem necessários, as informações de configuração devem vir do Git por meio do pipeline de CI/CD.
* As configurações de implantação de MSM Blueprint e MSM personalizado devem ser instaladas no Git por meio do pipeline de CI/CD.
* As alterações na tradução de I18n devem vir do Git por meio do pipeline de CI/CD.

## Pacotes e configurações de OSGi devem ser tratados como código {#osgi}

As alterações nos pacotes e configurações de OSGi devem ser introduzidas por meio do pipeline de CI/CD.

* Os pacotes OSGi novos ou atualizados devem ser introduzidos por meio do Git por meio do pipeline de CI/CD.
* As alterações nas configurações de OSGi só podem vir do Git por meio do pipeline de CI/CD.

O console da Web, usado nas versões anteriores do AEM para alterar pacotes e configurações de OSGi, não está disponível no AEM Cloud Service.

## Não são permitidas alterações no repositório de publicação {#changes-to-publish-repo}

Além das alterações na pasta `/home` no nível de publicação, alterações diretas no repositório de publicação não são permitidas no AEM Cloud Service. Em versões anteriores do AEM no local ou AEM no AMS, as alterações de código poderiam ser feitas diretamente no repositório de publicação. Algumas limitações podem ser atenuadas das seguintes formas:

* Para conteúdo e configuração baseada em conteúdo: faça suas alterações na instância do autor e as publique.
* Para código e configuração: faça suas alterações no repositório GIT e execute o pipeline de CI/CD para implementá-las.

## Modos de execução personalizados não são permitidos {#custom-runmodes}

Modos de execução adicionais ou personalizados não são possíveis no AEM Cloud Service. Para obter uma lista de modos de execução fornecidos prontos para o AEM Cloud Service, consulte [Implantação do AEM as a Cloud Service](/help/implementing/deploying/overview.md#runmodes).

## Remoção dos agentes de replicação e alterações relacionadas {#replication-agents}

No AEM Cloud Service, o conteúdo é publicado usando a [Distribuição de conteúdo de sling](https://sling.apache.org/documentation/bundles/content-distribution.html). Os agentes de replicação usados nas versões anteriores do AEM não são mais usados ou fornecidos, o que pode afetar as seguintes áreas dos projetos existentes do AEM:

* Fluxos de trabalho personalizados que enviam conteúdo para agentes de replicação dos servidores de visualização, por exemplo.
* Personalização dos agentes de replicação para transformar conteúdo.
* Usar a Replicação reversa para devolver o conteúdo da Publicação para o Autor.

Além disso, os botões Pausar e Desativar são removidos do console de administração do agente de replicação.

## Remoção da interface clássica do usuário {#classic-ui}

A interface clássica do usuário não está mais disponível no AEM Cloud Service.

## Entrega do lado da publicação {#publish-side-delivery}

A aceleração HTTP, incluindo o CDN e o gerenciamento de tráfego para os serviços de Autor e Publicação, é fornecida por padrão no AEM Cloud Service.

Para projetos em transição do AMS ou de uma instalação local, a Adobe recomenda usar a CDN integrada, pois os recursos do AEM Cloud Service são otimizados para a CDN fornecida.

## Manuseio e entrega de ativos {#asset-handling}

O upload, processamento e download de ativos estão otimizados no [!DNL Experience Manager Assets] as a [!DNL Cloud Service]. O AEM [!DNL Assets] agora é mais eficiente, permite maior dimensionamento e possibilita uploads e downloads mais rápidos. Além disso, isso afeta o código personalizado existente e algumas operações. Para uma lista de alterações e para paridade com os recursos do [!DNL Experience Manager] 6.5, consulte as [alterações do  [!DNL Assets]](/help/assets/assets-cloud-changes.md).
