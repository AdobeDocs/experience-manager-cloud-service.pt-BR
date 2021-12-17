---
title: Repository Modernizer
description: Repository Modernizer
source-git-commit: a6d225943c5d23ebd960fda0b0912a81f1f80014
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 4%

---

# Repository Modernizer {#repo-modernizer}

O Repository Modernizer é um utilitário desenvolvido para reestruturar pacotes de projetos existentes, separando conteúdo e código em pacotes discretos para serem compatíveis com a estrutura do projeto definida para o Adobe Experience Manager as a Cloud Service.

## Introdução {#introduction}

O Adobe Experience Manager as a Cloud Service traz muitos novos recursos e possibilidades para seus projetos de AEM. No entanto, há algumas alterações necessárias para que os projetos do Adobe Experience Manager Maven sejam compatíveis com o AEM Cloud Service. Em um alto nível, AEM exige uma separação de **conteúdo** e **código** em subpacotes discretos para respeitar a divisão entre conteúdo mutável e imutável. Consulte [Estrutura do projeto AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html?lang=pt-BR) para obter mais detalhes sobre a nova estrutura do projeto AEM para o Cloud Service.

O Repository Modernizer cria uma estrutura de projeto compatível do AEM Cloud Service criando a seguinte estrutura de implantação:

* `ui.apps` implantações de pacote em `/apps` e contém todo o código

* `ui.content` implantações de pacotes em áreas graváveis em tempo de execução (por exemplo, `/content`, `/conf`, `/home`ou nada que não `/apps`) e contém todo o conteúdo e configuração.

* `all` pacote é um pacote de contêiner que contém os subpacotes `ui.apps` e `ui.content`.

>[!NOTE]
>A estrutura do projeto se baseia em *Arquétipo 24* para os pacotes e respectivos `pom.xml/filter.xml files`. Consulte [Arquétipo 24](https://github.com/adobe/aem-project-archetype) para obter mais detalhes.

## Uso do Repository Modernizer {#using-repo-modernizer}

>[!VIDEO](https://video.tv.adobe.com/v/333057/?quality=12&learn=on)

* Via Adobe I/O CLI : Recomenda-se usar o Repository Modernizer via `aio-cli-plugin-aem-cloud-service-migration` (AEM plug-in de refatoração de código as a Cloud Service para o Adobe I/O CLI).

   Consulte **[Recurso Git: aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)** para saber como instalar e usar o plug-in.

* Como um utilitário independente : O Repository Modernizer também pode ser executado como um utilitário independente.

   Consulte **[Recurso Git: Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer)** para saber como usar essa ferramenta.

   >[!NOTE]
   >
   >O Repository Modernizer é desenvolvido usando NodeJS. Recomenda-se ter o NodeJS 10.0+ instalado.
