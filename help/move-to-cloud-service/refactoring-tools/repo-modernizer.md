---
title: Repository Modernizer
description: Repository Modernizer
exl-id: b89156a8-3d7d-4d36-89a2-beeda35bbc01
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 1%

---

# Repository Modernizer {#repo-modernizer}

O Repository Modernizer é um utilitário desenvolvido para reestruturar pacotes de projetos existentes, separando conteúdo e código em pacotes discretos para serem compatíveis com a estrutura do projeto definida para o Adobe Experience Manager como um Cloud Service.

## Introdução {#introduction}

O Adobe Experience Manager as a Cloud Service traz muitos novos recursos e possibilidades para seus projetos de AEM. No entanto, são necessárias algumas alterações para que os projetos do Adobe Experience Manager Maven sejam compatíveis com AEM Cloud Service. Em um nível alto, o AEM exige uma separação de **content** e **code** em subpacotes discretos para respeitar a divisão entre conteúdo mutável e imutável. Consulte [AEM Estrutura do Projeto](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html) para obter mais detalhes sobre a nova estrutura do projeto AEM para o Cloud Service.

O Repository Modernizer cria uma estrutura de projeto do Cloud Service compatível AEM criando a seguinte estrutura de implantação:

* `ui.apps` o pacote é implantado em  `/apps` e contém todo o código

* `ui.content` implantações de pacotes em áreas graváveis em tempo de execução (por exemplo,  `/content`,  `/conf`,  `/home`, ou qualquer coisa que não seja  `/apps`) e contém todo o conteúdo e configuração.

* `all` é um pacote de contêiner que contém os subpacotes  `ui.apps` e  `ui.content`.

>[!NOTE]
>A estrutura do Projeto é baseada em *Archetype 24* para pacotes e seus `pom.xml/filter.xml files`. Consulte [Arquétipo 24](https://github.com/adobe/aem-project-archetype) para obter mais detalhes.

## Uso do Repository Modernizer {#using-repo-modernizer}

>[!VIDEO](https://video.tv.adobe.com/v/333057/?quality=12&learn=on)

* Via Adobe I/O CLI : Recomenda-se usar o Repository Modernizer via `aio-cli-plugin-aem-cloud-service-migration` (AEM como um plug-in de refatoração de código Cloud Service para a CLI do Adobe I/O).

   Consulte **[Recurso Git: aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)** para saber como instalar e usar o plug-in.

* Como um utilitário independente : O Repository Modernizer também pode ser executado como um utilitário independente.

   Consulte **[Recurso Git: Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer)** para saber como usar essa ferramenta.

   >[!NOTE]
   >
   >O Repository Modernizer é desenvolvido usando NodeJS. Recomenda-se ter o NodeJS 10.0+ instalado.
