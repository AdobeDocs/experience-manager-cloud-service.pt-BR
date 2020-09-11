---
title: Alterações importantes no AEM Commerce as a Cloud Service
description: Alterações importantes no AEM Commerce as a Cloud Service em comparação ao Adobe Experience Manager 6.5.
translation-type: tm+mt
source-git-commit: 2934d0d8d3977bb7884bae9654ac26e9fa57b34f
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 94%

---


# Alterações importantes no AEM Commerce as a Cloud Service {#notable-changes}

O Adobe Experience Manager as a Cloud Service oferece muitos novos recursos e possibilidades para gerenciar projetos do AEM. Este documento destaca as importantes diferenças entre as funcionalidades de comércio da CIF (Commerce Integration Framework) para o Adobe Managed Service, o Experience Manager as a Cloud Service e para serviços no local. Para outras alterações, consulte as [alterações genéricas no Experience Manager as a Cloud Service](/help/release-notes/aem-cloud-changes.md).

Estas são as principais diferenças em relação ao Experience Manager 6.5:
* [Suporte à CIF clássica](#cif-classic)
* [Implantação de ferramentas de criação da CIF](#cif-tools)
* [Migração dos serviços no local e do Adobe Managed Service](#moving-cif-cs)

## Suporte à CIF clássica/início rápido no Experience Manager as a Cloud Service {#cif-classic}

A Commerce Integration Framework clássica, que incluía um importador de produtos para importar e armazenar catálogos de produtos no Experience Manager, já não está disponível no Experience Manager as a Cloud Service. A CIF clássica não é compatível com o Experience Manager as a Cloud Service e os projetos que usam a CIF clássica terão de implementar a versão compatível no seu lugar, como descrito em [CIF no Experience Manager as a Cloud Service](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/commerce/architecture/magento.html#overview)

## Implantação da CIF {#deployment}

Veja abaixo os diferentes modelos de implantação da Commerce Integration Framework para as diferentes soluções do AEM:

|  | AEM no local | AEM Managed Services | AEM Cloud Service |
|-------------     |-----------|-----------|-----------|
| Como implantar as ferramentas de criação da CIF para back-end da Magento | Consulte o [Conector da CIF](https://github.com/adobe/commerce-cif-connector/blob/master/README.md) compatível com o AEM 6.5 | Consulte o [Conector da CIF](https://github.com/adobe/commerce-cif-connector/blob/master/README.md) compatível com o AEM 6.5 | O AEM as a Cloud Service deve ser provisionado com o complemento CIF. Entre em contato com seu representante de vendas para obter mais informações |
| Como implantar o projeto [CIF Venia](https://github.com/adobe/aem-cif-guides-venia) | Instalação do pacote do AEM | Implantação feita pelo [Cloud Manager](https://docs.adobe.com/content/help/pt-BR/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html) | O projeto foi movido para o [Repositório Git do Cloud Manager](https://docs.adobe.com/content/help/pt-BR/experience-manager-cloud-service/implementing/managing-code/integrating-with-git.translate.html) e a implantação foi feita pelo [Cloud Manager](https://docs.adobe.com/content/help/pt-BR/experience-manager-cloud-service/implementing/deploying/overview.translate.html) |

>[!NOTE]
>
>Para obter documentação adicional sobre como usar o CIF com AEM Managed Service ou AEM On-premise, consulte a [Commerce Integration Framework](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/getting-started.html)

>[!NOTE]
>
>A Commerce Integration Framework clássica/início rápido pode ser usada na solução local do AEM em casos de uso muito limitados. No entanto, essa solução não é recomendada.

## Migrar para o AEM Commerce as a Cloud Service a partir de serviços no local e do Managed Services {#moving-cif-cs}

Os clientes que migram de uma instalação AEM no local ou do Managed Services para o AEM as a Cloud Service precisam fazer alguns ajustes no projeto do AEM.

O primeiro ajuste necessário, conforme descrito acima, é para o Conector da CIF. O Conector da CIF é substituído pelo complemento CIF implantado pela Adobe. Portanto, não instale o Conector da CIF no AEM as a Cloud Service. Além disso, ele não é compatível com o SDK local da AEM Cloud. A Adobe fornece o complemento CIF também para [desenvolvimento local](develop.md).

O segundo passo é entender a [estrutura do Projeto AEM](https://docs.adobe.com/content/help/pt-BR/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.translate.html) e as características do AEM as a Cloud Service. Adapte a configuração do seu projeto ao layout do AEM as a Cloud Service.
As principais diferenças são:

* O pacote OSGI do cliente GraphQL **não** deve mais ser incluído nos projetos AEM, agora ele é implantado por meio do complemento CIF.
* As configurações de OSGI para o cliente GraphQL e o Graphql Data Service **não** devem mais ser incluídas nos projetos AEM.

>[!TIP]
>
>Confira o projeto [Loja de referência Venia](https://github.com/adobe/aem-cif-guides-venia) no GitHub. Esse projeto fornece perfis Maven para o AEM as a Cloud Service e implantações locais que consideram as diferentes condições da estrutura.
