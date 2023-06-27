---
title: Modernizador de repositório
description: Modernizador de repositório
exl-id: cd9d212e-e720-4209-8b5a-659883cc1d95
source-git-commit: d361ddc9a50a543cd1d5f260c09920c5a9d6d675
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 6%

---

# Modernizador de repositório {#repo-modernizer}

O Repository Modernizer é um utilitário desenvolvido para reestruturar pacotes de projetos existentes separando o conteúdo e o código em pacotes discretos para serem compatíveis com a estrutura do projeto definida para o Adobe Experience Manager as a Cloud Service.

## Introdução {#introduction}

O Adobe Experience Manager as a Cloud Service traz muitos novos recursos e possibilidades para seus projetos AEM. No entanto, há algumas alterações necessárias para que os projetos do Adobe Experience Manager Maven sejam compatíveis com o AEM Cloud Service. Em um alto nível, o AEM requer uma separação de **conteúdo** e **código** em subpacotes discretos para respeitar a divisão entre conteúdo mutável e imutável. Consulte [Estrutura de projeto do AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure.html?lang=pt-BR) para obter mais detalhes sobre a nova estrutura do projeto AEM para o Cloud Service.

O Repository Modernizer cria uma estrutura de projeto do AEM Cloud Service compatível criando a seguinte estrutura de implantação:

* `ui.apps` o pacote é implantado em `/apps` e contém todo o código

* `ui.content` o pacote é implantado em áreas graváveis em tempo de execução (por exemplo, `/content`, `/conf`, `/home`, ou qualquer coisa que não `/apps`) e contém todo o conteúdo e configuração.

* `all` package é um pacote de contêiner que contém os subpacotes `ui.apps` e `ui.content`.

>[!NOTE]
>A estrutura do Projeto é baseada em *Arquétipo 24* para pacotes e seus `pom.xml/filter.xml files`. Consulte [Arquétipo 24](https://github.com/adobe/aem-project-archetype) para obter mais detalhes.

## Uso do Modernizador de repositório {#using-repo-modernizer}

>[!VIDEO](https://video.tv.adobe.com/v/333057/?quality=12&learn=on)

* Por meio da CLI do Adobe Developer : é recomendável usar o Repository Modernizer via `aio-cli-plugin-aem-cloud-service-migration` (Plug-in de refatoração de código as a Cloud Service AEM para a CLI da Adobe Developer).

  Consulte **[Recurso do Git: aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)** para que você possa aprender a instalar e usar o plug-in.

* Como um utilitário independente : o Repository Modernizer também pode ser executado como um utilitário independente.

  Consulte **[Recurso do Git: Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer)** para que você possa aprender a usar essa ferramenta.

  >[!NOTE]
  >
  >O Repository Modernizer é desenvolvido usando o NodeJS. É recomendável ter o NodeJS 10.0+ instalado.
