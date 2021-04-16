---
title: Migração para o complemento CIF (Commerce Integration Framework) da AEM
description: Como migrar para o complemento CIF (Commerce Integration Framework) do AEM de uma versão antiga
translation-type: tm+mt
source-git-commit: cda25048e171f6aacd5349706ad4192965e703db
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 20%

---

# Guia de migração para o Experience Manager Cloud Service {#cif-migration}

Este guia ajuda a identificar as áreas que você precisa atualizar para a migração do Experience Manager Cloud Service.

## Complemento CIF

Para o Experience Manager as a Cloud Service, o complemento CIF é a única solução de integração comercial compatível para o Adobe Commerce e soluções comerciais de terceiros. O complemento CIF é implantado automaticamente para clientes no Experience Manager as a Cloud Service, e nenhuma implantação manual é necessária. Consulte [Introdução ao AEM Commerce as a Cloud Service](getting-started.md).

Para dar suporte a projetos que implantam o CIF Adobe, forneça [AEM os Componentes principais da CIF](https://github.com/adobe/aem-core-cif-components).

O complemento CIF está disponível para o AEM 6.5, assim como por meio do [Portal de distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html). Ele é compatível e fornece os mesmos recursos do complemento CIF para o Experience Manager como um Cloud Service, não sendo necessário fazer ajustes.

A CIF clássica com suas dependências não está mais disponível. O código que depende dessa versão da CIF usando `com.adobe.cq.commerce.api` APIs do Java deve ser ajustado para o complemento CIF e seus princípios.

O conector da CIF disponível anteriormente não pode mais ser instalado. O código que depende desse conector deve ser ajustado para o complemento CIF e seus princípios.

## Estrutura do projeto

Aprenda a [AEM Estrutura do Projeto](https://docs.adobe.com/content/help/pt-BR/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.translate.html) e as características do AEM como Cloud Service. Adapte a configuração do seu projeto ao layout do AEM as a Cloud Service.
Comparado às implantações AEM 6.5, há duas diferenças principais aqui:

* O pacote OSGI do cliente GraphQL **não** deve mais ser incluído nos projetos AEM, agora ele é implantado por meio do complemento CIF.
* As configurações de OSGI para o cliente GraphQL e o Graphql Data Service **não** devem mais ser incluídas nos projetos AEM.

>[!TIP]
>
>Confira o projeto [Loja de referência Venia](https://github.com/adobe/aem-cif-guides-venia) no GitHub. Esse projeto fornece perfis Maven para o AEM as a Cloud Service e implantações locais que consideram as diferentes condições da estrutura.

## Catálogo de produtos

A importação de dados de catálogo de produtos não é mais suportada. O uso dos principais do complemento CIF solicitações de produtos e catálogos é feito por demanda por meio de chamadas em tempo real para uma solução comercial externa. Acesse Integração de capítulo para saber mais sobre a integração de uma solução comercial.

>[!TIP]
>
>Se nenhuma API em tempo real estiver disponível, um cache de produto externo com APIs deverá ser usado para a integração. Exemplo [Magento open-source](https://magento.com/products/magento-open-source).

## Experiências do catálogo de produtos com renderização de AEM

Se você usar o blueprint do catálogo com a CIF clássica, precisará atualizar o fluxo de trabalho do catálogo de produtos. O complemento CIF agora renderiza experiências de catálogo de produtos dinamicamente usando modelos de catálogo de AEM. Não é mais necessária a replicação de dados de produto ou páginas de produto.

## Interação entre dados não armazenáveis em cache e compras

As solicitações do lado do cliente para dados e interações que não podem ser armazenados em cache (por exemplo, adicionar ao carrinho, pesquisa) devem ir diretamente para o terminal de comércio (solução comercial ou camada de integração) via CDN/Dispatcher. Remova qualquer chamada em que AEM era apenas um proxy.
