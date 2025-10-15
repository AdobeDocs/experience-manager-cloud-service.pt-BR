---
title: Migração para o complemento do AEM Commerce integration framework (CIF)
description: Como migrar de uma versão antiga para o complemento AEM Commerce integration framework (CIF)
exl-id: 0db03a05-f527-4853-b52f-f113bce929cf
feature: Commerce Integration Framework
role: Admin
index: false
source-git-commit: 0664e5dc4a7619a52cd28c171a44ba02c592ea3d
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 17%

---


# Guia de migração para o Experience Manager Cloud Service {#cif-migration}

Este guia ajuda a identificar as áreas que você precisa atualizar para a migração do Experience Manager Cloud Service.

## Complemento do CIF {#cif-add-on}

Para o Experience Manager as a Cloud Service, o complemento CIF é a única solução de integração comercial compatível para o Adobe Commerce e soluções comerciais de terceiros. O complemento CIF é implantado automaticamente para clientes no Experience Manager as a Cloud Service; não é necessária implantação manual. Consulte [Introdução ao AEM Commerce as a Cloud Service.](/help/commerce-cloud/cif-storefront/getting-started.md)

Para dar suporte a projetos que implantam o CIF Adobe, forneça [Componentes principais do AEM CIF.](https://github.com/adobe/aem-core-cif-components)

O complemento CIF está disponível para o AEM 6.5 e por meio do [Portal de distribuição de software.](/help/implementing/developing/tools/package-manager.md) É compatível e fornece os mesmos recursos que o complemento CIF para Experience Manager as a Cloud Service - nenhum ajuste é necessário.

A CIF clássica com suas dependências não está mais disponível. Códigos que dependam dessa versão do CIF usando APIs Java `com.adobe.cq.commerce.api` devem ser ajustados para o complemento CIF e seus princípios.

O conector do CIF disponível anteriormente não pode mais ser instalado. Códigos que dependem desse conector precisam ser ajustados para o complemento CIF e seus princípios.

## Estrutura de projeto {#project-structure}

Saiba mais sobre a [Estrutura de Projetos AEM](/help/implementing/developing/introduction/aem-project-content-package-structure.md) e as características do AEM as a Cloud Service. Adapte a configuração do seu projeto ao layout do AEM as a Cloud Service.

Comparadas às implantações do AEM 6.5, há duas diferenças principais:

* O pacote OSGi do cliente GraphQL **não** deve mais ser incluído no projeto do AEM. Ele é implantado por meio do complemento CIF
* As configurações de OSGi para o cliente GraphQL e o Graphql Data Service **não devem mais ser incluídas nos projetos AEM.**

>[!TIP]
>
>Confira o projeto [Loja de referência Venia](https://github.com/adobe/aem-cif-guides-venia) no GitHub. Esse projeto fornece perfis Maven para o AEM as a Cloud Service e implantações locais que consideram as diferentes condições da estrutura.

## Catálogo de produtos {#product-catalog}

A importação de dados do catálogo de produtos não é mais suportada. Usando as entidades complementares do CIF, as solicitações de produtos e catálogos são feitas sob demanda por meio de chamadas em tempo real para uma solução de comércio externo. Acesse o capítulo Integração para saber mais sobre a integração de uma solução comercial.

>[!TIP]
>
>Se nenhuma API em tempo real estiver disponível, um cache de produto externo com APIs deverá ser usado para a integração. Exemplo [código aberto do Magento.](https://business.adobe.com/br/products/magento/open-source.html)

## Experiências do catálogo de produtos com renderização do AEM {#aem-rendering}

Se você usar o blueprint do catálogo com o CIF clássico, será necessário atualizar o fluxo de trabalho do catálogo de produtos. O complemento CIF agora renderiza experiências de catálogo de produtos dinamicamente usando modelos de catálogo do AEM. Não é mais necessária a replicação de dados ou páginas de produtos.

## Interação de compra e dados não armazenáveis em cache {#non-cacheable}

As solicitações do lado do cliente para dados e interações não armazenáveis em cache (por exemplo, adição ao carrinho, pesquisa) devem ir diretamente para o endpoint de comércio (solução de comércio ou camada de integração) por meio de CDN/Dispatcher. Remova todas as chamadas em que o AEM era apenas um proxy.
