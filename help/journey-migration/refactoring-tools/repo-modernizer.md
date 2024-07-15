---
title: Modernizador de repositório
description: Saiba como reestruturar pacotes de projetos existentes e torná-los compatíveis com a estrutura do projeto definida para o Adobe Experience Manager as a Cloud Service.
exl-id: cd9d212e-e720-4209-8b5a-659883cc1d95
feature: Migration
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 2%

---

# Modernizador de repositório {#repo-modernizer}

O Repository Modernizer é um utilitário desenvolvido para reestruturar pacotes de projetos existentes separando o conteúdo e o código em pacotes discretos para serem compatíveis com a estrutura do projeto definida para o Adobe Experience Manager as a Cloud Service.

## Introdução {#introduction}

O Adobe Experience Manager as a Cloud Service traz muitos novos recursos e possibilidades para seus projetos AEM. No entanto, há algumas alterações necessárias para que os projetos do Adobe Experience Manager Maven sejam compatíveis com o AEM Cloud Service. Em um alto nível, o AEM requer uma separação de **conteúdo** e **código** em subpacotes discretos para respeitar a divisão entre conteúdo mutável e imutável. Consulte [Estrutura de projeto AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure.html?lang=pt-BR) para obter mais detalhes sobre a nova estrutura de projeto AEM para Cloud Service.

O Repository Modernizer cria uma estrutura de projeto do AEM Cloud Service compatível criando a seguinte estrutura de implantação:

* O pacote `ui.apps` é implantado em `/apps` e contém todo o código

* O pacote `ui.content` é implantado em áreas graváveis em tempo de execução (por exemplo, `/content`, `/conf`, `/home` ou qualquer coisa que não seja `/apps`) e contém todo o conteúdo e configuração.

* O pacote `all` é um pacote de contêiner que contém os subpacotes `ui.apps` e `ui.content`.

>[!NOTE]
>A estrutura do Projeto é baseada no *Arquétipo 24* para pacotes e seus `pom.xml/filter.xml files`. Consulte [Arquétipo 24](https://github.com/adobe/aem-project-archetype) para obter mais detalhes.

## Uso do Modernizador de repositório {#using-repo-modernizer}

>[!VIDEO](https://video.tv.adobe.com/v/333057/?quality=12&learn=on)

* Por meio da CLI de Adobe I/O : a Adobe recomenda o uso do Repository Modernizer via `aio-cli-plugin-aem-cloud-service-migration` (plug-in de refatoração de código AEM as a Cloud Service para a CLI de Adobe I/O).

  Consulte **[Recurso do Git: aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)** para que você possa aprender a instalar e usar o plug-in.

* Como um utilitário independente : o Repository Modernizer também pode ser executado como um utilitário independente.

  Consulte **[Git Resource: Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer)** para que você possa aprender a usar esta ferramenta.

  >[!NOTE]
  >
  >O Repository Modernizer é desenvolvido usando o NodeJS. É recomendável ter o NodeJS 10.0+ instalado.
