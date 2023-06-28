---
title: Alterações importantes do complemento Commerce Integration Framework (CIF)
description: Alterações importantes da Commerce Integration Framework (CIF) em comparação às versões antigas da CIF.
exl-id: 5a526960-96a1-421e-9fb0-0825e7df8f32
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 3%

---

# Alterações importantes no complemento Commerce Integration Framework (CIF){#notable-changes}

O Adobe Experience Manager as a Cloud Service oferece muitos novos recursos e possibilidades para gerenciar os projetos AEM. Para saber mais sobre esses recursos, siga o link para [alterações no Experience Manager as a Cloud Service](/help/release-notes/aem-cloud-changes.md).

Este documento destaca as diferenças importantes entre o complemento Commerce Integration Framework (CIF) e as versões antigas da CIF, conhecidas como CIF Classic (Quickstart) e CIF Open-source.

## Instalação e atualizações

O complemento CIF do AEM é instalado por meio do Cloud Manager. A instalação requer um crédito da CIF, exceto para sandboxes, em que a CIF pode ser instalada sem créditos. Os créditos são recebidos automaticamente por meio do provisionamento do complemento CIF em seu contrato com o AEM.

O complemento é atualizado automaticamente como parte da atualização as a Cloud Service regular do AEM.

**Versões anteriores da CIF**

* CIF clássica: não é necessária nenhuma instalação. A CIF fazia parte do Quickstart. As atualizações da CIF faziam parte das atualizações regulares do AEM ou do service pack
* CIF Open-source para AEM no local: instalação via GitHub. As atualizações faziam parte do trabalho manual de atualização/manutenção.
* CIF Open-source para AEM Adobe Managed Services: instalação por meio da equipe de conta do Adobe. As atualizações faziam parte do trabalho manual de atualização/manutenção.

## Configuração do endpoint

O endpoint é configurado e atualizado por meio da interface do usuário do Cloud Manager ou de sua CLI.

**Versões anteriores da CIF**

* CIF clássica: por meio da configuração OSGi no AEM
* Código aberto da CIF: por meio do navegador de configuração da CIF

## Implantação do projeto CIF Venia

Projeto disponível em [Repositório Git do Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/managing-code/integrating-with-git.html) e implantação feita via [Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/overview.html?lang=pt-BR)

**Versões anteriores da CIF**

* CIF Classic: por meio da instalação do pacote AEM
* Código aberto da CIF: Via [Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/introduction.html?lang=pt-BR)

## Dados do catálogo de produtos

Os dados do catálogo de produtos são solicitados sob demanda por meio de chamadas em tempo real para um endpoint externo que oferece suporte às APIs necessárias do GraphQL. Essas APIs oferecem suporte ao acesso a dados dinâmicos ou em estágios em qualquer data. Nenhuma replicação necessária.

**Versões anteriores da CIF**

* CIF Clássico: dados de produtos em tempo real e em etapas são importados e mantidos em JCR no AEM Author por meio de uma importação completa ou delta de produtos. Os dados de produtos em tempo real são replicados para a publicação do AEM.

## Experiências do catálogo de produtos com renderização por AEM

O AEM renderiza experiências de catálogo de produtos dinamicamente usando modelos de catálogo de AEM que foram atribuídos a produtos e categorias. Nenhuma replicação necessária.

**Versões anteriores da CIF**

* CIF Clássica: o AEM Author cria uma página de AEM para cada categoria/produto usando a ferramenta de blueprint do catálogo. Essas páginas são replicadas para o AEM Publish.

>[!NOTE]
>
>Para obter a documentação adicional sobre como usar a CIF com AEM Managed Service ou AEM no local, consulte [Estrutura de integração do Commerce](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/getting-started.html)
