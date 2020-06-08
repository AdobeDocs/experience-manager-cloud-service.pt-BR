---
title: Alterações importantes no Adobe Experience Manager (AEM) as a Cloud Service
description: Alterações importantes no Adobe Experience Manager (AEM) as a Cloud Service
translation-type: tm+mt
source-git-commit: e76de9b84931dced6383570e384ffdb6fb334daf
workflow-type: tm+mt
source-wordcount: '820'
ht-degree: 100%

---


# Alterações importantes no Adobe Experience Manager (AEM) as a Cloud Service {#notable-changes-aem-cloud}

O AEM Cloud Service oferece muitos novos recursos e possibilidades para gerenciar os projetos do AEM. No entanto, existem várias diferenças entre o AEM Sites no local ou no Adobe Managed Services, em comparação ao AEM Cloud Service. Este documento destaca as diferenças importantes.

>[!NOTE]
>Este documento destaca as alterações importantes no AEM como um todo. Para ver as alterações específicas da solução, consulte:
>
>* [Alterações importantes do AEM Sites no AEM Cloud Service](/help/sites-cloud/sites-cloud-changes.md)
>* [Alterações importantes do AEM Assets no AEM Cloud Service](/help/assets/assets-cloud-changes.md)


As principais diferenças encontram-se nas seguintes áreas:

* [/apps e /libs não mudam no tempo de execução](#apps-libs-immutable)
* [Pacotes e configurações de OSGi devem ser baseados em repositório](#osgi)
* [Não são permitidas alterações no repositório de publicação](#changes-to-publish-repo)
* [Não são permitidos modos de execução personalizados](#custom-runmodes)
* [Remoção dos agentes de replicação](#replication-agents)
* [Remoção da interface do usuário clássica](#classic-ui)
* [Entrega do lado da publicação](#publish-side-delivery)
* [Manuseio e entrega de ativos](#asset-handling)

## /apps e /libs não mudam no tempo de execução {#apps-libs-immutable}

O conteúdo e as subpastas em `/apps` e `/libs` são somente leitura. Qualquer recurso ou código personalizado que espere fazer alterações nesse local falhará. Será retornado um erro de que esse conteúdo é somente leitura e que não foi possível concluir a operação de gravação. Isso tem impacto em várias áreas do AEM:

* Não são permitidas alterações em `/libs` de forma alguma.
   * Essa não é uma regra nova, no entanto, não foi aplicada nas versões anteriores do AEM no local.
* Sobreposições para áreas no `/libs` que podem ser sobrepostas ainda são permitidas dentro do `/apps`.
   * Essas sobreposições devem vir do Git por meio do pipeline de CI/CD.
* As informações de design do modelo estático armazenadas no `/apps` não podem ser editadas por meio da interface do usuário.
   * É recomendável que você aproveite os Modelos editáveis.
   * Se os Modelos estáticos ainda forem obrigatórios, as informações de configuração devem vir do Git por meio do pipeline de CI/CD.
* As configurações de implantação de MSM Blueprint e MSM personalizado devem ser instaladas no Git por meio do pipeline de CI/CD.
* As mudanças na tradução de I18n precisam vir do Git por meio do pipeline de CI/CD.

## Pacotes e configurações de OSGi devem ser baseados em repositório {#osgi}

O console da Web, usado nas versões anteriores do AEM para alterar as configurações de OSGi, não está disponível no AEM Cloud Service. Portanto, as alterações no OSGi devem ser introduzidas por meio do pipeline de IC/CD.

* As alterações nas configurações de OSGi só podem ser realizadas por meio da persistência de Git como configurações de OSGi baseadas em JCR.
* Os pacotes de OSGi novos ou atualizados devem ser introduzidos por meio do Git como parte do processo de criação do pipeline de CI/CD.

## Não são permitidas alterações no repositório de publicação {#changes-to-publish-repo}

Alterações diretas no repositório de publicação não são permitidas no AEM Cloud Service. Nas versões anteriores do AEM no local ou AEM no AMS, as alterações de código podem ser feitas diretamente no repositório de publicação, por exemplo, criar usuários, atualizar perfis de usuário e criar nós. Isso não é mais possível e pode ser atenuado das seguintes maneiras:

* Para configuração de conteúdo e baseada em conteúdo: faça as alterações na instância de criação e as publique.
* Para código e configuração: faça as alterações no repositório de GIT e execute o pipeline de CI/CD para implementá-las.
* Para dados relacionados ao usuário, como envios de formulário ou dados de perfil: use o Serviço de perfil unificado da Experience Cloud Platform ou de outra loja com reconhecimento de sessão de terceiros.

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

## Remoção dos agentes de replicação {#replication-agents}

No AEM Cloud Service, o conteúdo é publicado usando a [Distribuição de conteúdo de sling](https://sling.apache.org/documentation/bundles/content-distribution.html). Os agentes de replicação usados nas versões anteriores do AEM não são mais usados ou fornecidos, o que pode afetar as seguintes áreas dos projetos atuais do AEM:

* Fluxos de trabalho personalizados que enviam conteúdo para agentes de replicação dos servidores de visualização, por exemplo.
* Personalização dos agentes de replicação para transformar conteúdo
* Uso de Replicação reversa para devolver o conteúdo da publicação para o autor

## Remoção da interface do usuário clássica {#classic-ui}

A interface do usuário clássica não está mais disponível no AEM Cloud Service.

## Entrega do lado da publicação {#publish-side-delivery}

A aceleração HTTP, incluindo o CDN e o gerenciamento de tráfego para os serviços de criação e publicação, é fornecida por padrão no AEM Cloud Service.

Para a transição de projetos do AMS ou de uma instalação local, a Adobe recomenda utilizar a CDN integrada, pois os recursos do AEM Cloud Service são otimizados para a CDN fornecida.

## Manuseio e entrega de ativos {#asset-handling}

O upload, tratamento e download de ativos foram otimizados no AEM Cloud Service para serem mais eficientes, permitindo melhor dimensionamento e uploads e downloads mais rápidos. No entanto, isso pode afetar alguns códigos personalizados existentes.

* O fluxo de trabalho padrão **DAM Asset Update** nas versões anteriores do AEM não está mais disponível.
* Os componentes do site que fornecem um binário **sem transformação** devem usar o download direto.
   * O servlet Sling GET foi alterado para fazer isso por padrão.
* Os componentes do site que fornecem um binário **com transformação** (por exemplo, redimensionamento via servlet) podem continuar a operar da mesma forma.
* Os ativos que entram pelo Gerenciador de pacotes exigem reprocessamento manual usando a ação **Reprocessar ativos** na interface Ativos.
