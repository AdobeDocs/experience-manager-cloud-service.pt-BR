---
title: Migração para o complemento do AEM Commerce integration framework (CIF)
description: Como migrar de uma versão antiga para o complemento AEM Commerce integration framework (CIF)
exl-id: 0db03a05-f527-4853-b52f-f113bce929cf
feature: Commerce Integration Framework
role: Admin
index: false
source-git-commit: 173b70aa6f9ad848d0f80923407bf07540987071
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 38%

---

# Guia de migração para o Experience Manager Cloud Service {#cif-migration}

Este guia ajuda a identificar as áreas que você precisa atualizar para a migração do Experience Manager Cloud Service.

## Complemento do CIF

Para o Experience Manager as a Cloud Service, o complemento CIF é a única solução de integração comercial compatível para o Adobe Commerce e soluções comerciais de terceiros. O complemento CIF é implantado automaticamente para clientes no Experience Manager as a Cloud Service; não é necessária implantação manual. Consulte [Introdução ao AEM Commerce as a Cloud Service](getting-started.md).

Para dar suporte a projetos que implantam o CIF Adobe, forneça os [Componentes principais do AEM CIF](https://github.com/adobe/aem-core-cif-components).

O complemento CIF está disponível para o AEM 6.5 e por meio do [Portal de distribuição de softwares](https://experience.adobe.com/#/downloads/content/software-distribution/br/aem.html). Ele é compatível e fornece os mesmos recursos do complemento CIF para o Experience Manager as a Cloud Service, não sendo necessário fazer ajustes.

A CIF clássica com suas dependências não está mais disponível. Códigos que dependam dessa versão do CIF usando APIs Java `com.adobe.cq.commerce.api` devem ser ajustados para o complemento CIF e seus princípios.

O conector do CIF disponível anteriormente não pode mais ser instalado. Códigos que dependem desse conector precisam ser ajustados para o complemento CIF e seus princípios.

## Estrutura de projeto

Saiba mais sobre a [Estrutura de Projetos AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html?lang=pt-BR) e as características do AEM as a Cloud Service. Adapte a configuração do seu projeto ao layout do AEM as a Cloud Service.
Em comparação às implantações do AEM 6.5, há duas diferenças principais:

* O pacote OSGI do cliente GraphQL **não** deve mais ser incluído nos projetos AEM, agora ele é implantado por meio do complemento CIF.
* As configurações de OSGI para o cliente GraphQL e o Graphql Data Service **não** devem mais ser incluídas nos projetos AEM.

>[!TIP]
>
>Confira o projeto [Loja de referência Venia](https://github.com/adobe/aem-cif-guides-venia) no GitHub. Esse projeto fornece perfis Maven para o AEM as a Cloud Service e implantações locais que consideram as diferentes condições da estrutura.

## Catálogo de produtos

A importação de dados do catálogo de produtos não é mais suportada. Usando as entidades complementares do CIF, as solicitações de produtos e catálogos são feitas sob demanda por meio de chamadas em tempo real para uma solução de comércio externo. Acesse o capítulo Integração para saber mais sobre a integração de uma solução comercial.

>[!TIP]
>
>Se nenhuma API em tempo real estiver disponível, um cache de produto externo com APIs deverá ser usado para a integração. Exemplo [código aberto do Magento](https://business.adobe.com/products/magento/open-source.html).

## Experiências do catálogo de produtos com renderização do AEM

Se você usar o blueprint do catálogo com o CIF clássico, será necessário atualizar o fluxo de trabalho do catálogo de produtos. O complemento CIF agora renderiza experiências de catálogo de produtos dinamicamente usando modelos de catálogo do AEM. Não é mais necessária a replicação de dados ou páginas de produtos.

## Interação de compra e dados não armazenáveis em cache

As solicitações do lado do cliente para dados e interações não armazenáveis em cache (por exemplo, adição ao carrinho, pesquisa) devem ir diretamente para o endpoint de comércio (solução de comércio ou camada de integração) por meio de CDN/Dispatcher. Remova todas as chamadas em que o AEM era apenas um proxy.
