---
title: Alterações importantes do complemento Commerce integration framework (CIF)
description: Alterações notáveis do Commerce integration framework (CIF) em comparação com versões antigas do CIF.
exl-id: 5a526960-96a1-421e-9fb0-0825e7df8f32
feature: Commerce Integration Framework
role: Admin
source-git-commit: 0e328d013f3c5b9b965010e4e410b6fda2de042e
workflow-type: tm+mt
source-wordcount: '427'
ht-degree: 0%

---

# Alterações importantes no complemento Commerce integration framework (CIF){#notable-changes}

O Adobe Experience Manager as a Cloud Service oferece muitos novos recursos e possibilidades para gerenciar os projetos AEM. Para saber mais sobre esses recursos, siga o link para [alterações no Experience Manager as a Cloud Service](/help/release-notes/aem-cloud-changes.md).

Este documento destaca as importantes diferenças entre o complemento Commerce integration framework (CIF) e as versões antigas do CIF CIF CIF, conhecidas como Classic (Quickstart) e Open-source.

## Instalação e atualizações

AEM O complemento CIF é instalado por meio do Cloud Manager. A instalação requer um crédito de CIF, exceto para sandboxes em que o CIF pode ser instalado sem créditos. Os créditos são recebidos automaticamente por meio do provisionamento do complemento CIF em seu contrato AEM.

O complemento é atualizado automaticamente como parte da atualização normal do AEM as a Cloud Service.

**Versões anteriores do CIF**

* CIF Classic: Nenhuma instalação necessária, CIF foi parte do Quickstart. As atualizações do CIF faziam parte das atualizações regulares do AEM ou do service pack
* CIF Open-source para AEM no local: instalação via GitHub. As atualizações faziam parte do trabalho manual de atualização/manutenção.
* CIF Open-source para AEM Adobe Managed Services: Instalação por meio da Equipe de Conta do Adobe. As atualizações faziam parte do trabalho manual de atualização/manutenção.

## Configuração do endpoint

O endpoint é configurado e atualizado por meio da interface do usuário do Cloud Manager ou de sua CLI.

**Versões anteriores do CIF**

* CIF Classic: por meio da configuração OSGi no AEM
* CIF Open-source: por meio do navegador de configuração CIF

## Implantação do projeto CIF Venia

Projeto disponível no [Repositório Git do Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/managing-code/integrating-with-git.html?lang=pt-BR) e implantação feita via [Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/overview.html?lang=pt-BR)

**Versões anteriores do CIF**

* CIF Classic: por meio da instalação do pacote AEM
* Fonte aberta do CIF: Via [Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/introduction.html?lang=pt-BR)

## Dados do catálogo de produtos

Os dados do catálogo de produtos são solicitados sob demanda por meio de chamadas em tempo real para um endpoint externo que oferece suporte às APIs necessárias do GraphQL. Essas APIs oferecem suporte ao acesso a dados dinâmicos ou em estágios em qualquer data. Nenhuma replicação necessária.

**Versões anteriores do CIF**

* CIF Classic: dados de produtos ao vivo e preparados são importados e mantidos no JCR no AEM Author por meio de importação completa ou delta de produtos. Os dados de produtos ao vivo são replicados para o AEM Publish.

## Experiências do catálogo de produtos com renderização por AEM

O AEM renderiza experiências de catálogo de produtos dinamicamente usando modelos de catálogo de AEM que foram atribuídos a produtos e categorias. Nenhuma replicação necessária.

**Versões anteriores do CIF**

* CIF Classic: AEM Author cria uma página do AEM para cada categoria/produto usando a ferramenta de blueprint do catálogo. Essas páginas são replicadas para o AEM Publish.

>[!NOTE]
>
>Para obter a documentação adicional sobre como usar o CIF com AEM Managed Service ou AEM no local, consulte [Commerce integration framework](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/getting-started.html)
