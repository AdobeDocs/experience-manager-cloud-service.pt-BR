---
title: Introdução ao AEM Commerce as a Cloud Service
description: O Experience Manager Commerce as a Cloud Service consiste na Commerce Integration Framework (CIF), que é o padrão recomendado da Adobe para integrar e estender os serviços de comércio da Magento e outras soluções comerciais de terceiros com a Experience Cloud.
thumbnail: introducing-aem-commerce.jpg
translation-type: tm+mt
source-git-commit: 72d98c21a3c02b98bd2474843b36f499e8d75a03
workflow-type: tm+mt
source-wordcount: '1357'
ht-degree: 100%

---


# Apresentação do AEM Commerce as a Cloud Service {#commerce-intro}

O Experience Manager Commerce as a Cloud Service consiste na Commerce Integration Framework (CIF), que é o padrão recomendado da Adobe para integrar e estender os serviços de comércio da Magento e outras soluções comerciais de terceiros com a Experience Cloud. Ele permite que os clientes da Adobe ofereçam uma experiência de compra omnicanal extraordinária e personalizada com base em tecnologia de ponta.

A Commerce Integration Framework é um módulo complementar para o Experience Manager as a Cloud Service e fornece um conjunto de ferramentas de criação, componentes e uma loja de referência para acelerar o desenvolvimento de integrações entre o Experience Manager as a Cloud Service e soluções comerciais.

## Vantagens da CIF {#cif-benefits}

Estas são as principais vantagens:

* A integração é uma camada de abstração para padronizar e encapsular integrações com vários sistemas.

* A CIF é compatível com experiências headless/omnicanais.

   * Aplicativos de página única e aplicativos de várias páginas.
   * Pontos de extremidade GraphQL.

* A CIF oferece processos sem servidor e com base em microsserviços e camada de lógica de negócios para personalização e extensão de serviços comerciais.

* A CIF fornece integrações prontas para uso com soluções da Adobe, como AEM e Magento.

## Elementos da CIF {#cif-elements}

![Elementos da CIF](/help/commerce-cloud/assets/cif-overview1.jpg)


### Complemento CIF para ferramentas de criação {#add-on-authoring-tools}

O complemento CIF fornece acesso a ferramentas de criação para o comércio, como console do produto, seletores de produto e de categoria ou pesquisa de produtos para autores com o objetivo de capacitá-los a criar experiências avançadas com conteúdo de marketing e comércio. O complemento também gerencia a conexão de back-end com a Magento (ou sistema de comércio alternativo) via GraphQL. Depois de provisionado, o complemento é implantado automaticamente em ambientes do AEM as a Cloud Service.

### Componentes principais da CIF do AEM {#aem-cif-core}

Os Componentes principais da CIF do AEM são componentes renderizados do lado do servidor e do lado do cliente com suporte da Magento para GraphQL. Eles são utilizados para criar lojas estáticas e otimizadas para SEO que podem ser armazenadas em cache com base em tecnologias do AEM.

São fornecidos componentes básicos, comuns em implementações de comércio, como detalhes do produto, lista de produtos, navegação, pesquisa, etc. Eles podem ser utilizados como estão ou podem ser estendidos.

Os [Componentes principais da CIF do AEM](https://github.com/adobe/aem-core-cif-components) funcionam como os [Componentes principais do AEM Sites](https://github.com/adobe/aem-core-wcm-components), mas são dedicados a casos de uso específicos do comércio.

Estas são as principais vantagens desses componentes:

* São fáceis de usar nos projetos.
* Podem ser utilizados como estão ou com poucas modificações.
* Fornecem práticas recomendadas para a conexão com a Magento por meio de APIs GraphQL ou APIs REST

Componentes como o Teaser do produto e o Carrossel de produtos são fornecidos para permitir que os autores do AEM criem páginas de experiência no AEM, combinando conteúdo de marketing e comércio. Esses componentes podem ser facilmente arrastados e soltos em uma página de conteúdo criada no AEM e vinculada a produtos ou categorias específicos utilizando as ferramentas de criação da CIF, como o seletor de produto ou de categoria no Cloud Service.

Todos os componentes são de código aberto no [GitHub](https://github.com/adobe/aem-core-cif-components), o que revela total transparência nas mudanças feitas e permite que você obtenha a versão mais recente com facilidade. Você também pode fornecer solicitações de pull para melhorias e correções de erros que podem ser incorporadas.

### Loja AEM Venia {#aem-venia-storefront}

A [Loja AEM Venia](https://github.com/adobe/aem-cif-guides-venia) é uma vitrine de referência moderna e pronta para produção com uma jornada básica de comércio B2C. Ela pode ser utilizada para iniciar projetos comerciais e acelerar projetos usando o AEM, a CIF e a Magento. Inclui práticas recomendadas para a integração do AEM e da Magento e mostra como utilizar os [Componentes principais da CIF do AEM](https://github.com/adobe/aem-core-cif-components) e os [Componentes principais do AEM Sites](https://github.com/adobe/aem-core-wcm-components), além de ser compatível com os pontos de extremidade GraphQL do Adobe Commerce. Ela também fornece um site de referência para pré-vendas que demonstra a integração entre o AEM e a Magento.

A loja AEM Venia é um aplicativo de página mista em que o AEM oferece a loja e a Magento alimenta o back-end comercial com uma estrutura headless. A renderização do lado do servidor e do lado do cliente são utilizadas na loja. A renderização do lado do servidor é utilizada para fornecer conteúdo estático e a renderização do lado do cliente é utilizada para fornecer conteúdo dinâmico.

As páginas de produtos e de catálogos são relativamente estáticas e são renderizadas no lado do servidor utilizando os Componentes principais da CIF do AEM, como Detalhes do produto e Lista do produto em modelos genéricos criados no AEM. Esses componentes obtêm dados da Magento por meio de APIs GraphQL.
Essas páginas são criadas dinamicamente, renderizadas no servidor, armazenadas em cache no AEM Dispatcher e, em seguida, entregues no navegador.
Para atributos mais dinâmicos, como inventário ou preço, são usados componentes do lado do cliente. Componentes do lado cliente ou componentes da Web buscam dados diretamente da Magento por meio de APIs GraphQL e o conteúdo é renderizado no navegador.

#### Check-out {#checkout}

Essa loja de referência utiliza o componente Carrinho do lado do cliente, que renderiza o carrinho de compras e o formulário de check-out para demonstrar um padrão de integração de experiência completa. Você pode fornecer experiências comerciais com a Magento funcionando com arquitetura headless, sendo o AEM responsável pela loja. É recomendado usar os métodos de pagamento abstratos disponibilizados. Dessa forma, o cliente do navegador estabelece comunicação direta com o provedor do gateway de pagamento para que nem a nuvem da Adobe nem a da Magento armazenem ou passem dados confidenciais nos termos do PCI.

#### Gerenciamento de contas {#account-management}

O gerenciamento de contas é feito pela Magento e a loja de referência utiliza componentes do React do lado do cliente para permitir que o AEM renderize a experiência para as seguintes funcionalidades: Criar conta, Fazer logon e Esqueci a senha.

O projeto da loja AEM Venia é de código aberto. Para obter mais detalhes, consulte [Loja AEM Venia](https://github.com/adobe/aem-cif-guides-venia).

### Arquétipo de projeto do AEM{#aem-project-archtype}

O [Arquétipo de projeto do AEM](https://docs.adobe.com/content/help/pt-BR/experience-manager-core-components/using/developing/archetype/overview.html) pode ser usado para criar um projeto pequeno do Adobe Experience Manager com base em práticas recomendadas como ponto de partida para seus próprios projetos do AEM. Opcionalmente, os [Componentes principais da CIF do AEM ](https://github.com/adobe/aem-core-cif-components) podem ser incluídos em um novo projeto.

### Camada de extensão da CIF {#cif-extension}

A camada de extensão da CIF é uma camada intermediária para hospedar uma lógica de negócios complexa. Ela executa a plataforma Adobe I/O Runtime, que é a plataforma sem servidor da Adobe. Injetando lógica de negócios e de processos em um nível de microsserviço, ela permite estender chamadas de serviço completas. A lógica de negócios seria, por exemplo, utilizar localização e canal para definir uma estratégia de inventário. A lógica do processo seria, por exemplo, recuperar informações personalizadas.

### Camada de integração da CIF {#cif-integration-layer}

A camada de integração da CIF é utilizada para padronizar integrações com outras soluções comerciais. Ela executa a plataforma Adobe I/O Runtime, a plataforma sem servidor da Adobe, e permite integrações em nível de microsserviço com o mapeamento entre APIs de terceiros e as APIs do Adobe Commerce. Para ajudar você a começar a criar integrações de terceiros com o AEM, criamos uma [implementação de referência](https://github.com/adobe/commerce-cif-graphql-integration-reference) para demonstrar como um back-end comercial, que não seja a Magento, pode ser integrado por meio de APIs do Adobe Commerce (APIs GraphQL da Magento).

## Padrões de integração do AEM Commerce {#aem-commerce-integration}

Veja abaixo alguns dos padrões de integração do AEM Commerce implementados com frequência.

![Padrões de integração da CIF do AEM](/help/commerce-cloud/assets/aem-cif-integration-patterns-updated.JPG)


### Padrão de integração 1 {#integration-pattern-one}

Este é o nosso padrão de integração recomendado, em que o AEM oferece a loja e integra serviços comerciais por meio de APIs GraphQL do Adobe Commerce. Com esse padrão, o AEM oferece flexibilidade total para adaptar designs de sites de mídia avançada entre dispositivos. Esse padrão de integração é uma solução pronta para uso da CIF.


### Padrão de integração 2 {#integration-pattern-two}

Este padrão descreve uma maneira de fornecer conteúdo e soluções de comércio com arquitetura totalmente headless. A entrega é feita totalmente no lado do cliente. Nesse padrão, o conteúdo é fornecido pela API e os dados de HTML. Já os dados do Commerce são fornecidos por GraphQL. No momento, esse padrão não conta com suporte pronto para uso da CIF.


### Padrão de integração 3 {#integration-pattern-three}

Neste padrão, a Magento oferece a loja e incorpora o conteúdo criado no AEM. O conteúdo do AEM pode ser entregue via Fragmentos de experiência ou Fragmentos de conteúdo. Esse padrão de integração exige trabalho específico do projeto e não pode ser implementado com solução pronta para uso da CIF.


### Padrão de integração 4 {#integration-pattern-four}

Este é um padrão de integração comum em que a camada da loja ou de apresentação é dividida entre o AEM e uma solução comercial. Normalmente, a solução comercial fornece as páginas que não são de marketing, como check-out e conta, e o AEM fornece as páginas de marketing e a experiência de catálogo da loja. Nesse padrão, é necessário garantir que os carrinhos e as sessões do usuário sejam manipulados corretamente entre os dois sistemas para evitar uma experiência de usuário desarticulada. Por exemplo, a Magento armazena a sessão do carrinho e do usuário em um cookie, que pode ser compartilhado entre o AEM e a Magento. Esse padrão exige trabalho específico do projeto e não pode ser implementado com solução pronta para uso da CIF.
