---
title: Alterações importantes do complemento Commerce Integration Framework (CIF)
description: Alterações importantes da Commerce Integration Framework (CIF) em comparação às versões antigas da CIF.
exl-id: 5a526960-96a1-421e-9fb0-0825e7df8f32
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 6%

---

# Alterações importantes no complemento Commerce Integration Framework (CIF){#notable-changes}

O Adobe Experience Manager as a Cloud Service oferece muitos novos recursos e possibilidades para gerenciar projetos do AEM. Para saber mais sobre esses recursos, siga o link para [alterações no Experience Manager as a Cloud Service](/help/release-notes/aem-cloud-changes.md).

Este documento destaca as importantes diferenças entre o complemento Commerce Integration Framework (CIF) e as versões antigas da CIF, principalmente conhecidas como CIF clássica (início rápido) e CIF fonte aberta.

## Instalação e atualizações

O complemento CIF do AEM é instalado por meio do Cloud Manager. A instalação requer um crédito da CIF, exceto para sandboxes, onde a CIF pode ser instalada sem créditos. Os créditos são recebidos automaticamente por meio do provisionamento do complemento CIF em seu contrato de AEM.

O complemento é atualizado automaticamente como parte das atualizações regulares AEM as a Cloud Service.

**Versões anteriores da CIF**

* CIF Classic: Sem a necessidade de instalação, a CIF fazia parte do Início rápido. As atualizações da CIF faziam parte de atualizações regulares de AEM ou service pack
* CIF — código aberto para AEM no local: Instalação via GitHub. As atualizações faziam parte do trabalho manual de atualização/manutenção.
* Origem aberta da CIF para AEM Adobe Managed Services: Instalação por meio do Gerente de sucesso do cliente. As atualizações faziam parte do trabalho manual de atualização/manutenção.

## Configuração do ponto de extremidade

O endpoint é configurado e atualizado por meio da interface do usuário do Cloud Manager ou da CLI.

**Versões anteriores da CIF**

* CIF Classic: Por meio da configuração OSGi no AEM
* Código aberto da CIF: Por meio do navegador de configuração da CIF

## Implantação do projeto CIF Venia

Projeto disponível em [Repositório Git do Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/managing-code/integrating-with-git.html) e implantação feita via [Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=pt-BR)

**Versões anteriores da CIF**

* CIF Classic: Via instalação AEM pacote
* Código aberto da CIF: Via [Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html?lang=pt-BR)

## Dados do catálogo de produtos

Os dados do catálogo de produtos são solicitados sob demanda por meio de chamadas em tempo real para um endpoint externo que oferece suporte às APIs GraphQL necessárias. Essas APIs oferecem suporte para o acesso a dados ao vivo ou preparados em qualquer data específica. Não é necessária replicação.

**Versões anteriores da CIF**

* CIF Classic: Os dados de produtos em tempo real e preparados são importados e mantidos no JCR no AEM Author por meio de importação completa ou delta de produtos. Os dados do produto em tempo real são replicados para o AEM Publish.

## Experiências do catálogo de produtos com renderização de AEM

AEM renderiza experiências de catálogo de produtos dinamicamente usando modelos de catálogo AEM que foram atribuídos a produtos e categorias. Não é necessária replicação.

**Versões anteriores da CIF**

* CIF Classic: O AEM Author cria uma página de AEM para cada categoria/produto usando a ferramenta de blueprint do catálogo. Essas páginas são replicadas para o AEM Publish.

>[!NOTE]
>
>Para obter a documentação adicional sobre como usar a CIF com AEM Managed Service ou AEM no local, consulte [Estrutura de integração de comércio](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/getting-started.html)
