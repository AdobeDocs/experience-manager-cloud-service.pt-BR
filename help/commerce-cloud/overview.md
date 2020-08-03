---
title: Introdução ao comércio AEM como Cloud Service
description: O que há de novo AEM Comércio como Cloud Service.
translation-type: tm+mt
source-git-commit: c5694cf8651cf8ba5331c730fa1b1180310dd35a
workflow-type: tm+mt
source-wordcount: '1331'
ht-degree: 1%

---


# Apresentando AEM comércio como Cloud Service {#commerce-intro}

O Experience Manager Commerce como Cloud Service consiste em Commerce Integration Framework (CIF), que é o padrão recomendado para integrar e estender os serviços de comércio do Magento e outras soluções de comércio de terceiros ao Experience Cloud. Isso permite que os clientes do Adobe ofereçam uma experiência extraordinária e personalizada de compras em canais globais, com base na tecnologia mais avançada.

A Commerce Integration Framework é um módulo complementar para o Experience Manager como Cloud Service e fornece um conjunto de ferramentas de criação, componentes e uma vitrine de referência para acelerar o desenvolvimento de integrações entre o Experience Manager como Cloud Service e soluções de comércio.

## Benefícios CIF {#cif-benefits}

Os principais benefícios são:

* A integração é uma camada de abstração para padronizar e encapsular integrações com vários sistemas.

* O CIF oferece suporte a experiências sem cabeça/em canais móveis:

   * Aplicativos de página única e aplicativos de várias páginas
   * Pontos finais GraphQL

* O CIF fornece processos sem servidor e baseados em microserviços e camada lógica comercial para personalização e extensão de serviços comerciais.

* CIF fornece integrações prontas para uso com soluções de Adobe, como AEM e Magento

## CIF Elementos {#cif-elements}

![CIF Elementos](/help/commerce-cloud/assets/cif-overview1.jpg)


### add-on CIF para ferramentas de criação {#add-on-authoring-tools}

O add-on CIF fornece acesso às ferramentas de criação de comércio, como Console do produto, Seletores de produto e Categoria ou pesquisa de produtos para autores, para capacitá-los a criar experiências avançadas com conteúdo de marketing e comércio. O add-on também gerencia a conexão de backend com Magento (ou sistema de comércio alternativo) via GraphQL. Depois que o complemento é provisionado, ele é implantado automaticamente em AEM como ambientes Cloud Service.

### Componentes principais CIF AEM {#aem-cif-core}

Os componentes principais CIF AEM são componentes renderizados do lado do servidor e do cliente com suporte a Magento GraphQL. Eles são usados para criar um armazenamento de comércio estático, acessível e compatível com SEO baseado em tecnologias AEM.

Os componentes básicos são fornecidos, comuns em implementações comerciais, como Detalhes do produto, Lista do produto, Navegação, Pesquisa etc. Eles podem ser usados como estão ou podem ser estendidos.

Os Componentes [principais CIF](https://github.com/adobe/aem-core-cif-components) AEM funcionam como os Componentes [principais dos](https://github.com/adobe/aem-core-wcm-components) AEM Sites, mas são dedicados a casos de uso específicos do comércio.

Esses componentes são os principais benefícios:

* Eles são fáceis de usar em seus projetos.
* Eles podem ser usados no estado em que se encontram ou com modificações muito mínimas.
* Elas fornecem as práticas recomendadas para a conexão com o Magento por meio de APIs GraphQL ou REST APIs

Componentes como o Teaser de produto e o Carrossel de produto são fornecidos para permitir que os AEM Author criem páginas de experiência em AEM, combinando o conteúdo de marketing e comércio. Esses componentes podem ser facilmente arrastados e soltos em uma página de conteúdo criada no AEM e vinculada a produtos ou categorias específicos usando as ferramentas de criação CIF, como o Seletor de produto ou de Categoria no Cloud Service.

Todos os componentes são de fonte aberta no [GitHub](https://github.com/adobe/aem-core-cif-components). Isso mostra total transparência nas mudanças feitas em frente e permite que você obtenha a versão mais recente muito facilmente. Você também pode fornecer solicitações pull para melhorias e correções de bugs que podem ser incorporadas.

### AEM Venia Storefront {#aem-venia-storefront}

A Venia Storefront [](https://github.com/adobe/aem-cif-guides-venia) AEM é uma loja de referência moderna, pronta para produção, que exibe uma jornada básica de comércio B2C. Ele pode ser usado para iniciar projetos de comércio e acelerar projetos usando AEM, CIF e Magento. Ele demonstra as práticas recomendadas para a integração de AEM e Magento e mostra como usar os componentes [principais CIF e os componentes](https://github.com/adobe/aem-core-cif-components) principais [AEM Sites e suporta os endpoints](https://github.com/adobe/aem-core-wcm-components) GraphQL do Adobe Commerce. Ele também fornece um site de referência para pré-vendas para demonstrar a integração entre AEM e Magento.

A Venia Storefront AEM é uma aplicação de página mista na qual AEM possui o vidro e o Magento alimenta o backend do comércio de uma forma ininterrupta. A renderização do lado do servidor e a renderização do lado do cliente são usadas na vitrine. A renderização no servidor é usada para fornecer conteúdo estático e a renderização no cliente é usada para fornecer conteúdo dinâmico.

As páginas de produtos e catálogos são relativamente estáticas e são renderizadas no lado do servidor usando AEM componentes principais CIF, como Detalhes do produto e Lista do produto, em modelos genéricos criados em AEM. Esses componentes obtêm dados do Magento por meio de APIs GraphQL.
Essas páginas são criadas dinamicamente, renderizadas no servidor, armazenadas em cache no AEM dispatcher e, em seguida, entregues no navegador.
Para atributos mais dinâmicos, como inventário ou preço, por outro lado, componentes do lado do cliente são usados. Componentes do cliente ou componentes da Web buscam dados diretamente do Magento por meio de APIs GraphQL e o conteúdo é renderizado no navegador.

#### Check-out {#checkout}

Este vitrine de referência usa o componente Carrinho do lado do cliente que renderiza o carrinho de compras e o formulário de checkout para demonstrar um padrão de integração de experiência completa, onde você pode fornecer experiências comerciais com o Magento funcionando de forma completamente sem cabeça e AEM possuindo o vidro. Recomenda - se a utilização dos métodos de pagamento abstratos fornecidos. Isso coloca o cliente do navegador em comunicação direta com o provedor do gateway de pagamento para que nem as nuvens de Adobe nem Magento sejam seguras ou passem os dados confidenciais da PCI.

#### Gerenciamento de contas {#account-management}

O gerenciamento de contas é realizado pela Magento e o armazenamento de referência utiliza componentes baseados no React do lado do cliente para permitir que AEM renderize a experiência para as seguintes funcionalidades: Crie atos, faça logon e esquece a senha.

O projeto Venia Storefront AEM é open source e para obter mais detalhes, consulte [AEM Venia Storefront](https://github.com/adobe/aem-cif-guides-venia).

### AEM Project Archetype {#aem-project-archtype}

The [AEM Project Archetype](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/archetype/overview.html) can be used to create a minimal, best-practices-based Adobe Experience Manager project as a starting point for your own AEM projects. Opcionalmente, [AEM os Componentes](https://github.com/adobe/aem-core-cif-components) principais CIF podem ser incluídos em um projeto recém-gerado.

### Camada de extensão CIF {#cif-extension}

A camada de extensão CIF é uma camada intermediária para hospedar uma lógica comercial complexa. Ele executa a plataforma Adobe I/O Runtime que é a plataforma sem servidor Adobe. Ele permite estender chamadas de serviço completas, injetando lógica de negócios e de processo em um nível de microserviço. A lógica comercial seria, por exemplo, usar localização e canal para determinar uma estratégia de inventário. A lógica do processo seria, por exemplo, recuperar informações personalizadas.

### Camada de integração CIF {#cif-integration-layer}

A camada de integração CIF é usada para padronizar integrações com outras soluções de comércio. Ele executa a plataforma Adobe I/O Runtime que é a plataforma sem servidor Adobe e permite integrações em um microserviço mapeando APIs de terceiros em relação às APIs de Comércio Adobe. Para ajudá-lo a começar a criar integrações de terceiros com AEM, criamos uma implementação [de](https://github.com/adobe/commerce-cif-graphql-integration-reference) referência para demonstrar como um backend de comércio não-Magento pode ser integrado por meio de APIs de Comércio de Adobe (APIs de GraphQL de Magento).

## Padrões de integração de comércio AEM {#aem-commerce-integration}

Alguns dos padrões de integração do AEM Commerce implementados com frequência são mostrados abaixo.

![AEM padrões de integração CIF](/help/commerce-cloud/assets/aem-cif-integration-patterns-updated.JPG)


### Padrão de integração 1 {#integration-pattern-one}

Este é nosso padrão de integração recomendado onde AEM possui o vidro inteiro e integra serviços de comércio por meio de APIs GraphQL do Adobe Commerce. Esse padrão libera AEM flexibilidade total para adaptar designs de sites de mídia avançada em dispositivos. Esse padrão de integração é suportado pelo CIF como uma solução pronta para uso.


### Padrão de integração 2 {#integration-pattern-two}

Este padrão descreve uma maneira totalmente impensável de fornecer conteúdo e comércio. O delivery é totalmente do lado do cliente. Neste padrão, o conteúdo é fornecido por API e os dados de HTML e Comércio são fornecidos por GraphQL. No momento, esse padrão não é suportado pelo CIF out-of-the-box.


### Padrão de integração 3 {#integration-pattern-three}

Neste padrão, Magento possui o vidro e incorpora AEM conteúdo de autoria. O conteúdo de criação AEM pode ser entregue por Fragmentos de experiência ou Fragmentos de conteúdo. Este padrão de integração exigirá trabalho específico do projeto e não pode ser implementado prontamente com o CIF.


### Padrão de integração 4 {#integration-pattern-four}

Este é um padrão de integração comum em que a camada de vidro ou apresentação é dividida entre AEM e uma solução de Comércio. Normalmente, a solução Commerce fornece as páginas que não são de marketing, como check-out e minha conta, e AEM fornece as páginas de marketing e a experiência do catálogo de frente de loja. Neste padrão, é necessário garantir que os carrinhos e as sessões do usuário sejam tratados corretamente entre os dois sistemas para evitar uma experiência desarticulada do usuário. Por exemplo, o Magento armazena a sessão do carrinho e do usuário em um cookie, que pode ser compartilhado entre AEM e Magento. Este padrão exigirá trabalho específico do projeto e não pode ser implementado out-of-the-box com CIF.
