---
title: Modernizador do repositório
description: Modernizador do repositório
translation-type: tm+mt
source-git-commit: 5da0d4cc8c6d8781dd7cce8bbbde207568a6d10b
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 4%

---


# Modernizador do repositório {#repo-modernizer}

O Repository Modernizer é um utilitário desenvolvido para reestruturar pacotes de projetos existentes, separando o conteúdo e o código em pacotes discretos para ser compatível com a estrutura de projeto definida para a Adobe Experience Manager como um Cloud Service.

## Introdução {#introduction}

O Adobe Experience Manager como Cloud Service traz muitos novos recursos e possibilidades para seus projetos AEM. Entretanto, há algumas mudanças necessárias para que os projetos do Adobe Experience Manager Maven sejam compatíveis com AEM Cloud Service. Em um nível alto, AEM requer uma separação de **content** e **code** em subpacotes discretos para respeitar a divisão entre conteúdo mutável e imutável. Consulte [AEM Estrutura do Projeto](https://docs.adobe.com/content/help/pt-BR/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.translate.html) para obter mais detalhes sobre a nova estrutura do projeto AEM para Cloud Service.

O Modernizador do Repositório cria uma estrutura de projeto AEM Cloud Service compatível criando a seguinte estrutura de implantação:

* `ui.apps` o pacote implanta  `/apps` e contém todo o código

* `ui.content` implantações de pacotes em áreas graváveis em tempo de execução (por exemplo,  `/content`,  `/conf`,  `/home`ou qualquer coisa que não seja  `/apps`) e contém todo o conteúdo e a configuração.

* `all` package é um container package que contém os sub-packages  `ui.apps` e  `ui.content`.

>[!NOTE]
>A estrutura do Projeto se baseia em *Archetype 24* para pacotes e seus `pom.xml/filter.xml files`. Consulte [Archetype 24](https://github.com/adobe/aem-project-archetype) para obter mais detalhes.

## Usando o Modernizador do Repositório {#using-repo-modernizer}

* Por meio do Adobe I/O CLI: É recomendável usar o Repository Modernizer via `aio-cli-plugin-aem-cloud-service-migration` (AEM como um plug-in de refatoração de código de Cloud Service para a CLI do Adobe I/O).

   Consulte **[Recurso Git: aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)** para saber como instalar e usar o plug-in.

* Como um utilitário independente: O Modernizador do Repositório também pode ser executado como um utilitário independente.

   Consulte **[Recurso Git: Modernizador de repositório](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer)** para saber como usar essa ferramenta.

   >[!NOTE]
   >
   >O Modernizador do Repositório é desenvolvido com o NodeJS. É recomendável ter o NodeJS 10.0+ instalado.
