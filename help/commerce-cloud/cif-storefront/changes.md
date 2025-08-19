---
title: Alterações importantes do complemento Commerce integration framework (CIF)
description: Alterações importantes do Commerce integration framework (CIF) em comparação às versões antigas do CIF.
exl-id: 5a526960-96a1-421e-9fb0-0825e7df8f32
feature: Commerce Integration Framework
role: Admin
source-git-commit: 856442039fcd25ec675a6258d182f7a35f590c3c
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 0%

---


# Alterações importantes no complemento do Commerce integration framework (CIF) {#notable-changes}

O Adobe Experience Manager as a Cloud Service oferece muitos novos recursos e possibilidades para gerenciar os projetos do AEM. Para saber mais sobre esses recursos, siga o link para [alterações no Experience Manager as a Cloud Service.](/help/release-notes/aem-cloud-changes.md)

Este documento destaca as diferenças importantes entre o complemento Commerce integration framework (CIF) e as versões antigas do CIF, conhecidas como CIF Classic (Quickstart) e CIF Open-Source.

## Instalação e atualizações

O complemento AEM CIF é instalado por meio do Cloud Manager. A instalação requer um crédito do CIF, exceto para sandboxes, em que o CIF pode ser instalado sem créditos. Os créditos são recebidos automaticamente por meio do provisionamento do complemento CIF em seu contrato do AEM.

O complemento é atualizado automaticamente como parte da atualização normal do AEM as a Cloud Service.

### Versões anteriores do CIF {#previous-versions-installation}

* CIF Classic: nenhuma instalação necessária, o CIF fazia parte do Quickstart. As atualizações do CIF faziam parte das atualizações regulares do AEM ou de service packs
* CIF Open-source para AEM no local: instalação via GitHub. As atualizações faziam parte do trabalho manual de atualização/manutenção.
* CIF Open-source para AEM Adobe Managed Services: instalação por meio da Equipe de conta da Adobe. As atualizações faziam parte do trabalho manual de atualização/manutenção.

## Configuração do endpoint {#endpoint-configuration}

O endpoint é configurado e atualizado por meio da interface do usuário do Cloud Manager ou de sua CLI.

### Versões anteriores do CIF {#previous-versions-endpoint}

* CIF Classic: por meio da configuração do OSGi no AEM
* Código aberto do CIF: por meio do navegador de configuração do CIF

## Implantação do projeto CIF Venia {#venia-project}

Projeto disponível no [Repositório Git do Cloud Manager](/help/implementing/cloud-manager/managing-code/integrating-with-git.md) e implantação feita via [Cloud Manager.](/help/implementing/deploying/overview.md)

### Versões anteriores do CIF {#previous-versions-venia}

* CIF Classic: por meio da instalação do pacote do AEM
* Código aberto do CIF: Via [Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/introduction.html?lang=pt-BR)

## Dados do catálogo de produtos {#product-catalog-data}

Os dados do catálogo de produtos são solicitados sob demanda por meio de chamadas em tempo real para um endpoint externo que oferece suporte às APIs necessárias do GraphQL. Essas APIs oferecem suporte ao acesso a dados dinâmicos ou em estágios em qualquer data. Nenhuma replicação necessária.

### Versões anteriores do CIF {#previous-versions-catalog}

* CIF Classic: dados de produtos ao vivo e em preparo são importados e mantidos em JCR no AEM Author por meio de importação completa ou delta de produtos. Os dados do produto em tempo real são replicados para a publicação do AEM.

## Experiências do catálogo de produtos com renderização do AEM {#catalog-experiences}

O AEM renderiza experiências de catálogo de produtos dinamicamente usando modelos de catálogo do AEM que foram atribuídos a produtos e categorias. Nenhuma replicação necessária.

### Versões anteriores do CIF {#previous-cif-versions}

* CIF Classic: o AEM Author cria uma página do AEM para cada categoria/produto usando a ferramenta de blueprint do catálogo. Essas páginas são replicadas para o AEM Publish.

>[!NOTE]
>
>Para obter a documentação adicional sobre como usar o CIF com o AEM Managed Service ou o AEM no local, consulte [Commerce integration framework.](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/getting-started.html)
