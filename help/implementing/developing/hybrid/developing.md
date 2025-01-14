---
title: Desenvolvimento de SPAs para o AEM
description: Este artigo apresenta perguntas importantes a serem consideradas ao envolver um desenvolvedor de front-end para desenvolver um SPA para AEM. Ele também fornece uma visão geral da arquitetura do SPA no que se refere ao AEM para ter em mente ao implantar um SPA desenvolvido no AEM.
exl-id: f6c6f31a-69ad-48f6-b995-e6d0930074df
feature: Developing
role: Admin, Architect, Developer
source-git-commit: e06766160009eaa1bbc41bbf7cfad967a5195e71
workflow-type: tm+mt
source-wordcount: '2028'
ht-degree: 8%

---

# Desenvolvimento de SPAs para o AEM {#developing-spas-for-aem}

Aplicativos de página única (SPAs) podem oferecer experiências interessantes para usuários de sites. Os desenvolvedores desejam criar sites usando estruturas de SPA, e os autores desejam editar o conteúdo de um site criado usando essas estruturas diretamente no AEM.

Este artigo apresenta questões importantes a serem consideradas ao envolver um desenvolvedor de front-end para desenvolver um SPA para AEM e fornece uma visão geral da arquitetura do AEM no que diz respeito à implantação do no SPA AEM.

{{ue-over-spa}}

## Princípios de desenvolvimento do SPA para AEM {#spa-development-principles-for-aem}

O desenvolvimento de aplicativos de página única no AEM parte do princípio de que o desenvolvedor de front-end segue as práticas recomendadas padronizadas ao criar um SPA. Se, como desenvolvedor de front-end, você seguir essas práticas recomendadas gerais e alguns princípios específicos do AEM, seu SPA estará funcional com o [AEM e seus recursos de criação de conteúdo](introduction.md#content-editing-experience-with-spa).

* **[Portabilidade](#portability)** - Assim como com qualquer componente, os componentes devem ser compilados para serem o mais portáteis possível. O SPA deve ser desenvolvido com componentes portáteis e reutilizáveis.
* **[AEM controla a estrutura do site](#aem-drives-site-structure)** - O desenvolvedor de front-end cria componentes e tem a propriedade de sua estrutura interna, mas depende do AEM para definir a estrutura de conteúdo do site.
* **[Renderização dinâmica](#dynamic-rendering)** - Todas as renderizações devem ser dinâmicas.
* **[Roteamento dinâmico](#dynamic-routing)** - O SPA é responsável pelo roteamento e o AEM o escuta e realiza buscas com base nele. Qualquer roteamento também deve ser dinâmico.

Se você considerar esses princípios ao desenvolver seu SPA, ele se tornará o mais flexível e inovador possível e, ao mesmo tempo, ativará todas as funcionalidades de criação compatíveis com AEM.

Se você não precisar de suporte para recursos de criação de AEM, considere um [modelo de design de SPA](#spa-design-models) diferente.

### Portabilidade {#portability}

Assim como no desenvolvimento de qualquer componente, seus componentes devem ser projetados de forma a maximizar sua portabilidade. Quaisquer padrões que funcionem contra a portabilidade ou reutilização dos componentes devem ser evitados para garantir a compatibilidade, a flexibilidade e a manutenção no futuro.

O SPA resultante deve ser construído com componentes altamente portáteis e reutilizáveis.

### AEM direciona a estrutura do site {#aem-drives-site-structure}

O desenvolvedor de front-end deve se considerar responsável pela criação de uma biblioteca de componentes SPA usados para criar o aplicativo. O desenvolvedor de front-end tem controle total da estrutura interna dos componentes. [No entanto, o AEM sempre é proprietário da estrutura do site](editor-overview.md).

Esse controle significa que o desenvolvedor de front-end pode adicionar conteúdo do cliente antes ou depois do ponto de entrada dos componentes e também pode fazer uma chamada de terceiros dentro do componente. No entanto, o desenvolvedor de front-end não tem controle total sobre como os componentes se aninham, por exemplo.

### Renderização dinâmica {#dynamic-rendering}

O SPA deve depender apenas da renderização dinâmica do conteúdo. Essa expectativa é o padrão onde o AEM busca e renderiza todos os filhos da estrutura de conteúdo.

Qualquer renderização explícita que aponte para um conteúdo específico é considerada renderização estática e, embora seja compatível, é compatível com os recursos de criação de conteúdo do AEM. Também vai contra o princípio de [portabilidade](#portability).

### Roteamento Dinâmico {#dynamic-routing}

Assim como na renderização, todo o roteamento também deve ser dinâmico. No AEM, [o SPA sempre deve ser o proprietário do roteamento](routing.md) e o AEM escuta e busca conteúdo com base nele.

Qualquer roteamento estático funciona contra o [princípio de portabilidade](#portability) e limita o autor por não ser compatível com os recursos de criação de conteúdo do AEM. Por exemplo, com o roteamento estático, se o autor de conteúdo quiser alterar uma rota ou uma página, ele deverá solicitar que o desenvolvedor de front-end faça isso.

## Arquétipo de projeto do AEM {#aem-project-archetype}

Qualquer projeto do AEM deve utilizar o [Arquétipo de projeto do AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=pt-BR), que aceita projetos SPA que usam o React ou o Angular e utiliza o SDK de SPA.

## Modelos de design SPA {#spa-design-models}

Se os [princípios de desenvolvimento do SPA no AEM](#spa-development-principles-for-aem) forem seguidos, seu SPA estará funcional com todos os recursos de criação de conteúdo do AEM compatíveis.

No entanto, pode haver casos em que essa funcionalidade não seja totalmente necessária. A tabela a seguir fornece uma visão geral dos vários modelos de design, suas vantagens e suas desvantagens.

<table>
 <tbody>
  <tr>
   <th><strong>Modelo de design<br /> </strong></th>
   <th><strong>Vantagens</strong></th>
   <th><strong>Desvantagens</strong></th>
  </tr>
  <tr>
   <td>O AEM é usado como um CMS headless sem usar a <a href="/help/implementing/developing/hybrid/reference-materials.md">estrutura do SDK Editor do SPA.</a></td>
   <td>O desenvolvedor front-end tem controle total sobre o aplicativo.</td>
   <td><p>Os autores de conteúdo não podem usar a experiência de criação de conteúdo do AEM.</p> <p>O código não é portátil nem reutilizável se contiver referências estáticas ou roteamento.</p> <p>Não permite o uso do editor de modelos, portanto, o desenvolvedor de front-end deve manter modelos editáveis por meio do JCR.</p> </td>
  </tr>
  <tr>
   <td>O desenvolvedor de front-end usa a estrutura SDK do Editor de SPA, mas abre apenas algumas áreas para o autor de conteúdo.</td>
   <td>O desenvolvedor mantém controle sobre o aplicativo, habilitando apenas a criação em áreas restritas do aplicativo.</td>
   <td><p>Os autores de conteúdo são restritos a um conjunto limitado de experiências de criação de conteúdo no AEM.</p> <p>O código corre o risco de não ser portátil ou reutilizável se contiver referências estáticas ou roteamento.</p> <p>Não permite o uso do editor de modelos, portanto, o desenvolvedor de front-end deve manter modelos editáveis por meio do JCR.</p> </td>
  </tr>
  <tr>
   <td>O projeto usa totalmente o Editor de SPA SDK e os componentes de front-end são desenvolvidos como uma biblioteca e a estrutura de conteúdo do aplicativo é delegada ao AEM.</td>
   <td><p>O aplicativo é reutilizável e portátil.</p> <p>O autor de conteúdo pode editar o aplicativo usando a experiência de criação de conteúdo do AEM.<br /> </p> <p>O SPA é compatível com o editor de modelos.</p> </td>
   <td><p>O desenvolvedor não controla a estrutura do aplicativo e a parte do conteúdo delegada ao AEM.</p> <p>O desenvolvedor ainda pode reservar áreas do aplicativo para o conteúdo que não deve ser criado usando AEM.</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Embora todos os modelos sejam compatíveis com o AEM, apenas implementando o terceiro (e seguindo os [princípios de desenvolvimento do SPA](#spa-development-principles-for-aem) recomendados) os autores de conteúdo são capazes de interagir com o SPA AEM e editá-lo.

## Migração do AEM existente para o SPA {#migrating-existing-spas-to-aem}

Geralmente, se o SPA seguir os [Princípios de desenvolvimento do SPA](#spa-development-principles-for-aem), seu AEM SPA AEM AEM SPA funcionará no e poderá ser editado usando o editor.

Siga estas etapas para preparar seu SPA existente para trabalhar com AEM.

1. **Torne seus componentes JS modulares.** - Torná-las capazes de serem renderizadas em qualquer ordem, posição e tamanho.
1. **Use os contêineres fornecidos pelo SDK para colocar seus componentes na tela.** - O AEM fornece um componente de sistema de página e parágrafo para você usar.
1. **Crie um componente AEM para cada componente JS.** - Os componentes AEM definem a caixa de diálogo e a saída JSON.

## Instruções para desenvolvedores de front-end {#instructions-for-front-end-developers}

A principal tarefa de envolver um desenvolvedor de front-end para criar um SPA para AEM é chegar a um acordo sobre os componentes e seus modelos JSON.

Veja a seguir um esboço das etapas que um desenvolvedor de front-end deve seguir ao desenvolver um SPA para AEM.

1. **Concordar sobre os componentes e seu modelo JSON**

   Desenvolvedores de front-end e desenvolvedores de AEM de back-end devem concordar sobre quais componentes são necessários e um modelo para que haja uma correspondência individualizada entre os componentes de SPA e os componentes de back-end.

   Os componentes do AEM ainda são necessários, principalmente para fornecer caixas de diálogo de edição e exportar o modelo de componentes.

1. **Em componentes do React, acesse o modelo via`this.props.cqModel`**

   Quando os componentes forem acordados e o modelo JSON estiver em vigor, o desenvolvedor de front-end poderá desenvolver o SPA e simplesmente acessar o modelo JSON via `this.props.cqModel`.

1. **Implementar o método `render()` do componente**

   O desenvolvedor de front-end implementa o método `render()` da maneira que ele achar adequada e pode usar os campos da propriedade `cqModel`. Esse método gera os fragmentos DOM e HTML inseridos na página. Esse método também é a maneira padrão de criar um aplicativo no React.

1. **Mapear o componente para o tipo de recurso AEM via`MapTo()`**

   O mapeamento armazena classes de componente e é usado internamente pelo componente `Container` fornecido para recuperar e instanciar dinamicamente componentes com base no tipo de recurso fornecido.

   Este mapa serve como &quot;cola&quot; entre o front-end e o back-end, para que o editor saiba a quais componentes os componentes de reação correspondem.

   `Page` e `ResponsiveGrid` são bons exemplos de classes que estendem a base `Container`.

1. **Definir `EditConfig` do componente como parâmetro para`MapTo()`**

   Esse parâmetro é necessário para informar ao editor como o componente deve ser nomeado, desde que ainda não tenha sido renderizado ou não tenha conteúdo para renderizar.

1. **Estender a classe `Container` fornecida para páginas e contêineres**

   Os sistemas de páginas e parágrafos devem estender essa classe para que a delegação para componentes internos funcione conforme esperado.

1. **Implementar uma solução de roteamento que use a API HTML5 `History`.**

   Quando o `ModelRouter` está habilitado, chamar as funções `pushState` e `replaceState` aciona uma solicitação ao `PageModelManager` para buscar um fragmento ausente do modelo.

   A versão atual do `ModelRouter` dá suporte apenas ao uso de URLs que apontam para o caminho de recurso real dos pontos de entrada do Modelo do Sling. Ele não é compatível com o uso de URLs ou aliases personalizados.

   O `ModelRouter` pode ser desabilitado ou configurado para ignorar uma lista de expressões regulares.

## AEM-Agnóstico {#aem-agnostic}

Esses blocos de código ilustram como os componentes do React e do Angular não precisam de nada específico do Adobe ou do AEM.

* Tudo que está dentro do componente JavaScript é AEM-agnóstico.
* O que é específico do AEM, no entanto, é que o componente JS deve ser mapeado para um componente AEM com o auxiliar MapTo.

![Abordagem de AEM](assets/aem-agnostic.png)

O auxiliar do `MapTo` é a &quot;cola&quot; que permite que os componentes de back-end e front-end sejam combinados:

* Informa ao contêiner JS (ou sistema de parágrafo JS) qual componente JS é responsável pela renderização de cada um dos componentes presentes no JSON.
* Ele adiciona um atributo de dados HTML ao HTML que o componente JS renderiza, para que o Editor de SPA saiba qual caixa de diálogo exibir para o autor ao editar o componente.

Para obter mais informações sobre como usar o `MapTo` e criar o AEM para SPA em geral, consulte o guia de Introdução da estrutura escolhida.

* [Introdução ao SPA no AEM usando o React](getting-started-react.md)
* [Introdução ao SPA no AEM usando o Angular](getting-started-angular.md)

## Arquitetura do AEM e SPA {#aem-architecture-and-spas}

A arquitetura geral do AEM, incluindo ambientes de desenvolvimento, criação e publicação, não é alterada ao usar o SPA. No entanto, é útil compreender como o desenvolvimento do SPA se encaixa nessa arquitetura.

![Arquitetura do AEM e SPA](assets/aem-architecture.png)

* **Ambiente de compilação**

  Nesse ambiente, a origem do aplicativo SPA e a origem do componente são verificadas.

   * O gerador de clientlib do NPM cria uma biblioteca do cliente a partir do projeto SPA.
   * Essa biblioteca é retirada pelo Maven e implantada pelo plug-in Maven Build, juntamente com o componente, no autor do AEM.

* **Autor do AEM**

  O conteúdo é criado sobre o autor de AEM, incluindo a criação de SPA.

  Quando um SPA é editado usando o Editor de SPA no ambiente de criação:

   1. O SPA solicita o HTML externo.
   1. O CSS é carregado.
   1. O JavaScript do aplicativo SPA é carregado.
   1. Quando o aplicativo SPA é executado, o JSON é solicitado, permitindo que o aplicativo crie o DOM da página, incluindo os atributos `cq-data`.
   1. Os atributos `cq-data` permitem que o editor carregue informações de página adicionais para que ele saiba quais configurações de edição estão disponíveis para os componentes.

* **AEM Publish**

  Onde o conteúdo criado e as bibliotecas compiladas, incluindo artefatos de aplicativo SPA, bibliotecas de clientes e componentes, são publicados para consumo público.

* **Dispatcher/CDN**

  O Dispatcher serve como a camada de armazenamento em cache do AEM para os visitantes do site.
   * As solicitações são processadas de forma semelhante à forma como estão no autor do AEM. No entanto, não há solicitação das informações da página porque elas só são necessárias para o editor.
   * JavaScript, CSS, JSON e HTML são armazenados em cache, otimizando a página para entrega rápida.

>[!NOTE]
>
>Dentro do AEM, não há necessidade de executar mecanismos de build do JavaScript ou executar o próprio JavaScript. O AEM hospeda somente os artefatos compilados do aplicativo SPA.

## Próximas etapas {#next-steps}

* [Introdução ao SPA no AEM usando o React](getting-started-react.md) mostra como um SPA básico é criado para funcionar com o editor do SPA AEM usando o React.
* [Introdução ao SPA no AEM usando o Angular](getting-started-angular.md) mostra como um SPA básico é criado para funcionar com o editor de no SPA AEM usando o Angular.
* A [Visão geral do editor de SPA](editor-overview.md) aborda em detalhes o modelo de comunicação do AEM e do SPA.
* O [Projeto WKND SPA](wknd-tutorial.md) é um tutorial passo a passo para a implementação de um projeto SPA simples no AEM.
* [Modelo dinâmico para mapeamento de componentes para SPA](model-to-component-mapping.md) explica o modelo dinâmico para mapeamento de componentes e como ele funciona dentro do SPA no AEM.
* O [Blueprint do SPA](blueprint.md) oferece um aprofundamento sobre como o SPA SDK para AEM SPA AEM funciona caso você queira implementar o no para uma estrutura diferente do React ou do Angular. Ou você simplesmente gostaria de uma compreensão mais profunda.
