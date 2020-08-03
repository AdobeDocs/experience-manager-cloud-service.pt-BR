---
title: Alterações notáveis no AEM Commerce como Cloud Service
description: Mudanças notáveis no AEM Commerce como Cloud Service em comparação ao Adobe Experience Manager 6.5.
translation-type: tm+mt
source-git-commit: df6f679b70a7cc70e4f76612c0a72a31443cd1b8
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 6%

---


# Notable changes to AEM Commerce as a Cloud Service {#notable-changes}

O Adobe Experience Manager como Cloud Service oferece muitos novos recursos e possibilidades para gerenciar seus projetos de AEM. Este documento destaca as diferenças importantes entre os recursos de Comércio e a CIF (Commerce Integration Framework) para serviços no local, Adobe Managed Service e Experience Manager como Cloud Service. Para outras alterações, consulte as [alterações genéricas no Experience Manager como Cloud Service](/help/release-notes/aem-cloud-changes.md).

As principais diferenças em relação ao Experience Manager 6.5 são as seguintes:
* [Suporte para CIF Classic](#cif-classic)
* [Implantação de ferramentas de criação CIF](#cif-tools)
* [Transferência do serviço local e gerenciado pelo Adobe](#moving-cif-cs)

## Suporte para CIF Classic/Quickstart em Experience Manager como Cloud Service {#cif-classic}

O Classic Commerce Integration Framework, que incluía um Importador de produtos para importar e armazenar catálogos de produtos no Experience Manager, não está mais disponível no Experience Manager como Cloud Service. A utilização de CIF clássico não é suportada em Experience Manager como Cloud Service e os projetos que utilizam CIF clássico terão de substituir a implementação CIF clássica pela versão suportada, como descrito em [CIF em Experience Manager como Cloud Service](https://git.corp.adobe.com/AdobeDocs/experience-manager-cloud-service.en/blob/cif/help/commerce-cloud/architecture.md)

## Implantação de CIF {#deployment}

Veja abaixo os diferentes modelos de implantação da Commerce Integration Framework para as diferentes ofertas de AEM:

|  | AEM local | Managed Services AEM | Cloud Service AEM |
|-------------     |-----------|-----------|-----------|
| Como implantar as ferramentas de criação CIF para backend do Magento | [Consulte o Conector](https://github.com/adobe/commerce-cif-connector/blob/master/README.md) CIF suportado no AEM 6.5 | [Consulte o Conector](https://github.com/adobe/commerce-cif-connector/blob/master/README.md) CIF suportado no AEM 6.5 | AEM como um Cloud Service precisa ser provisionado com o suplemento CIF. Entre em contato com seu representante de vendas para obter mais detalhes |
| Como implantar o projeto [CIF Venia](https://github.com/adobe/aem-cif-guides-venia) | Instalação do pacote AEM | Implantação realizada pelo [Cloud Manager](https://docs.adobe.com/content/help/br/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html) | O projeto foi movido para o Repositório [Git do](https://docs.adobe.com/content/help/pt-BR/experience-manager-cloud-service/implementing/managing-code/integrating-with-git.translate.html) Cloud Manager e a implantação foi feita pelo Gerenciador [da Cloud](https://docs.adobe.com/content/help/pt-BR/experience-manager-cloud-service/implementing/deploying/overview.translate.html) |

>[!Nnota]
>
>A versão CIF Classic/Quickstart da Commerce Integration Framework pode ser usada em AEM oferta local para casos de uso muito limitados. No entanto, essa não é a solução recomendada.

## Mudar para AEM Comércio como Cloud Service do On-premise e Managed Services {#moving-cif-cs}

Os clientes que mudam de uma instalação AEM local ou Managed Services para AEM como Cloud Service precisam fazer alguns ajustes menores no projeto AEM.

O primeiro ajuste, conforme descrito acima, é necessário para o conector CIF. O conector CIF é substituído pelo suplemento CIF implantado pelo Adobe. Portanto, não instale o conector CIF no AEM como Cloud Service. Além disso, o uso com o SDK da AEM Cloud local não é suportado, o Adobe fornece o suplemento CIF também para desenvolvimento [](develop.md)local.

Segundo, entender a Estrutura [do Projeto](https://docs.adobe.com/content/help/pt-BR/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.translate.html) AEM e as características da AEM como Cloud Service. Adapte a configuração do projeto ao AEM como um layout de Cloud Service.
As principais diferenças são:

* O pacote OSGI do cliente GraphQL não **deve** mais ser incluído no projeto AEM, ele é implantado por meio do suplemento CIF
* As configurações de OSGI para o cliente GraphQL e o Graphql Data Service não **** devem mais ser incluídas no projeto AEM

>[!Tip]
>
>Confira o [AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia) no GitHub. Este projeto fornece perfis Maven para AEM como Cloud Service e implantações locais que têm em conta as diferentes condições de enquadramento.
