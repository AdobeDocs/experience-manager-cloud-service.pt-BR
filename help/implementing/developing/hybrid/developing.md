---
title: Desenvolvimento de SPAs para o AEM
description: Este artigo apresenta perguntas importantes a serem consideradas ao envolver um desenvolvedor de front-end para desenvolver um SPA para AEM. Ele também fornece uma visão geral da arquitetura do SPA no que se refere ao AEM para ter em mente ao implantar um SPA desenvolvido no AEM.
exl-id: f6c6f31a-69ad-48f6-b995-e6d0930074df
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '2028'
ht-degree: 8%

---

# Desenvolvimento de SPAs para o AEM {#developing-spas-for-aem}

Aplicativos de página única (SPAs) podem oferecer experiências interessantes para usuários de sites. Os desenvolvedores desejam criar sites usando estruturas de SPA, e os autores desejam editar o conteúdo de um site criado usando essas estruturas diretamente no AEM.

Este artigo apresenta questões importantes a serem consideradas ao envolver um desenvolvedor de front-end para desenvolver um SPA para AEM e fornece uma visão geral da arquitetura do AEM no que diz respeito à implantação do no SPA AEM.

## Princípios de desenvolvimento do SPA para AEM {#spa-development-principles-for-aem}

O desenvolvimento de aplicativos de página única no AEM parte do princípio de que o desenvolvedor de front-end segue as práticas recomendadas padronizadas ao criar um SPA. Se, como desenvolvedor de front-end, você seguir essas práticas recomendadas gerais e alguns princípios específicos do AEM, seu SPA funcionará com [AEM e seus recursos de criação de conteúdo](introduction.md#content-editing-experience-with-spa).

* **[Portabilidade](#portability)** - Como acontece com qualquer componente, os componentes devem ser construídos para serem o mais portáteis possível. O SPA deve ser desenvolvido com componentes portáteis e reutilizáveis.
* **[AEM controla a estrutura do site](#aem-drives-site-structure)** - O desenvolvedor de front-end cria componentes e tem a propriedade de sua estrutura interna, mas depende do AEM para definir a estrutura de conteúdo do site.
* **[Renderização dinâmica](#dynamic-rendering)** - Todas as renderizações devem ser dinâmicas.
* **[Roteamento dinâmico](#dynamic-routing)** - O SPA é responsável pelo roteamento e o AEM o escuta e realiza buscas com base nele. Qualquer roteamento também deve ser dinâmico.

Se você considerar esses princípios ao desenvolver seu SPA, ele se tornará o mais flexível e inovador possível e, ao mesmo tempo, ativará todas as funcionalidades de criação compatíveis com AEM.

Se você não precisar de suporte para recursos de criação de AEM, considere [Modelo de design SPA](#spa-design-models).

### Portabilidade {#portability}

Assim como no desenvolvimento de qualquer componente, seus componentes devem ser projetados de forma a maximizar sua portabilidade. Quaisquer padrões que funcionem contra a portabilidade ou reutilização dos componentes devem ser evitados para garantir a compatibilidade, a flexibilidade e a manutenção no futuro.

O SPA resultante deve ser construído com componentes altamente portáteis e reutilizáveis.

### AEM direciona a estrutura do site {#aem-drives-site-structure}

O desenvolvedor de front-end deve se considerar responsável pela criação de uma biblioteca de componentes SPA usados para criar o aplicativo. O desenvolvedor de front-end tem controle total da estrutura interna dos componentes. [No entanto, o AEM sempre é o dono da estrutura do site](editor-overview.md).

Esse controle significa que o desenvolvedor de front-end pode adicionar conteúdo do cliente antes ou depois do ponto de entrada dos componentes e também pode fazer uma chamada de terceiros dentro do componente. No entanto, o desenvolvedor de front-end não tem controle total sobre como os componentes se aninham, por exemplo.

### Renderização dinâmica {#dynamic-rendering}

O SPA deve depender apenas da renderização dinâmica do conteúdo. Essa expectativa é o padrão onde o AEM busca e renderiza todos os filhos da estrutura de conteúdo.

Qualquer renderização explícita que aponte para um conteúdo específico é considerada renderização estática e, embora seja compatível, é compatível com os recursos de criação de conteúdo AEM. É igualmente contrário ao princípio da igualdade [portabilidade](#portability).

### Roteamento Dinâmico {#dynamic-routing}

Assim como na renderização, todo o roteamento também deve ser dinâmico. No AEM, [o SPA sempre deve ser o proprietário do roteamento](routing.md) e o AEM escuta e busca conteúdo com base nela.

Qualquer roteamento estático funciona contra o [princípio da portabilidade](#portability) e limita o autor por não ser compatível com os recursos de criação de conteúdo do AEM. Por exemplo, com o roteamento estático, se o autor de conteúdo quiser alterar uma rota ou uma página, ele deverá solicitar que o desenvolvedor de front-end faça isso.

## Arquétipo de projeto do AEM {#aem-project-archetype}

Qualquer projeto do AEM deve utilizar o [Arquétipo de projeto do AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=pt-BR), que aceita projetos SPA que usam o React ou o Angular e utiliza o SDK de SPA.

## Modelos de design SPA {#spa-design-models}

Se a variável [princípios do desenvolvimento do AEM no SPA](#spa-development-principles-for-aem) forem seguidos, o SPA funcionará com todos os recursos de criação de conteúdo AEM compatíveis.

No entanto, pode haver casos em que essa funcionalidade não seja totalmente necessária. A tabela a seguir fornece uma visão geral dos vários modelos de design, suas vantagens e suas desvantagens.

<table>
 <tbody>
  <tr>
   <th><strong>Modelo de design<br /> </strong></th>
   <th><strong>Vantagens</strong></th>
   <th><strong>Desvantagens</strong></th>
  </tr>
  <tr>
   <td>O AEM é usado como um CMS headless sem usar o <a href="/help/implementing/developing/hybrid/reference-materials.md">Estrutura do SDK do editor de SPA.</a></td>
   <td>O desenvolvedor front-end tem controle total sobre o aplicativo.</td>
   <td><p>Os autores de conteúdo não podem usar a experiência de criação de conteúdo AEM.</p> <p>O código não é portátil nem reutilizável se contiver referências estáticas ou roteamento.</p> <p>Não permite o uso do editor de modelos, portanto, o desenvolvedor de front-end deve manter modelos editáveis por meio do JCR.</p> </td>
  </tr>
  <tr>
   <td>O desenvolvedor de front-end usa a estrutura do SDK do Editor de SPA, mas abre apenas algumas áreas para o autor de conteúdo.</td>
   <td>O desenvolvedor mantém controle sobre o aplicativo, habilitando apenas a criação em áreas restritas do aplicativo.</td>
   <td><p>Os autores de conteúdo estão restritos a um conjunto limitado de experiências de criação de conteúdo no AEM.</p> <p>O código corre o risco de não ser portátil ou reutilizável se contiver referências estáticas ou roteamento.</p> <p>Não permite o uso do editor de modelos, portanto, o desenvolvedor de front-end deve manter modelos editáveis por meio do JCR.</p> </td>
  </tr>
  <tr>
   <td>O projeto usa totalmente o SDK do Editor de SPA, e os componentes de front-end são desenvolvidos como uma biblioteca e a estrutura de conteúdo do aplicativo é delegada ao AEM.</td>
   <td><p>O aplicativo é reutilizável e portátil.</p> <p>O autor de conteúdo pode editar o aplicativo usando a experiência de criação de conteúdo AEM.<br /> </p> <p>O SPA é compatível com o editor de modelos.</p> </td>
   <td><p>O desenvolvedor não controla a estrutura do aplicativo e a parte do conteúdo delegada ao AEM.</p> <p>O desenvolvedor ainda pode reservar áreas do aplicativo para o conteúdo que não deve ser criado usando AEM.</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Embora todos os modelos sejam suportados no AEM, somente implementando o terceiro (e seguindo o recomendado) [Princípios de desenvolvimento do SPA](#spa-development-principles-for-aem)SPA ) são os autores de conteúdo capazes de interagir com o AEM e editar seu conteúdo.

## Migração do AEM existente para o SPA {#migrating-existing-spas-to-aem}

Geralmente, se o seu SPA seguir o [Princípios de desenvolvimento do SPA para AEM](#spa-development-principles-for-aem), em seguida, o SPA funciona no AEM e pode ser editado usando o Editor de AEM do SPA.

Siga estas etapas para preparar seu SPA existente para trabalhar com AEM.

1. **Torne seus componentes JS modulares.** - Torne-os capazes de ser renderizados em qualquer ordem, posição e tamanho.
1. **Use os contêineres fornecidos pelo SDK para colocar seus componentes na tela.** - O AEM fornece um componente do sistema de páginas e parágrafos para você usar.
1. **Crie um componente AEM para cada componente JS.** - Os componentes AEM definem a caixa de diálogo e a saída JSON.

## Instruções para desenvolvedores de front-end {#instructions-for-front-end-developers}

A principal tarefa de envolver um desenvolvedor de front-end para criar um SPA para AEM é chegar a um acordo sobre os componentes e seus modelos JSON.

Veja a seguir um esboço das etapas que um desenvolvedor de front-end deve seguir ao desenvolver um SPA para AEM.

1. **Concordar sobre os componentes e seu modelo JSON**

   Desenvolvedores de front-end e desenvolvedores de AEM de back-end devem concordar sobre quais componentes são necessários e um modelo para que haja uma correspondência individualizada entre os componentes de SPA e os componentes de back-end.

   Os componentes do AEM ainda são necessários, principalmente para fornecer caixas de diálogo de edição e exportar o modelo de componentes.

1. **Nos componentes do React, acesse o modelo via`this.props.cqModel`**

   Quando os componentes forem acordados e o modelo JSON estiver em vigor, o desenvolvedor de front-end poderá desenvolver o SPA e simplesmente acessar o modelo JSON por meio de `this.props.cqModel`.

1. **Implementar do componente `render()` método**

   O desenvolvedor de front-end implementa o `render()` como bem entenderem e podem usar os campos de `cqModel` propriedade. Esse método gera os fragmentos DOM e HTML inseridos na página. Esse método também é a maneira padrão de criar um aplicativo no React.

1. **Mapear o componente para o tipo de recurso AEM via`MapTo()`**

   O mapeamento armazena classes de componente e é usado internamente pelo `Container` componente para recuperar e instanciar dinamicamente os componentes com base no tipo de recurso especificado.

   Este mapa serve como &quot;cola&quot; entre o front-end e o back-end, para que o editor saiba a quais componentes os componentes de reação correspondem.

   A variável `Page` e `ResponsiveGrid` são bons exemplos de classes que estendem a base `Container`.

1. **Definir o `EditConfig` como parâmetro para`MapTo()`**

   Esse parâmetro é necessário para informar ao editor como o componente deve ser nomeado, desde que ainda não tenha sido renderizado ou não tenha conteúdo para renderizar.

1. **Estender o fornecido `Container` classe para páginas e contêineres**

   Os sistemas de páginas e parágrafos devem estender essa classe para que a delegação para componentes internos funcione conforme esperado.

1. **Implementar uma solução de roteamento que use o HTML `History` API.**

   Quando a variável `ModelRouter` está ativado, chamando o `pushState` e `replaceState` acionar uma solicitação para o `PageModelManager` para buscar um fragmento ausente do modelo.

   A versão atual do `ModelRouter` O suporta apenas o uso de URLs que apontam para o caminho de recurso real dos pontos de entrada do Modelo Sling. Ele não é compatível com o uso de URLs ou aliases personalizados.

   A variável `ModelRouter` O pode ser desativado ou configurado para ignorar uma lista de expressões regulares.

## AEM-Agnóstico {#aem-agnostic}

Esses blocos de código ilustram como os componentes do React e do Angular não precisam de nada específico do Adobe ou do AEM.

* Tudo o que está dentro do componente JavaScript é independente de AEM.
* O que é específico do AEM, no entanto, é que o componente JS deve ser mapeado para um componente AEM com o auxiliar MapTo.

![Abordagem independente de AEM](assets/aem-agnostic.png)

A variável `MapTo` helper é a &quot;cola&quot; que permite que os componentes de back-end e front-end sejam combinados:

* Informa ao contêiner JS (ou sistema de parágrafo JS) qual componente JS é responsável pela renderização de cada um dos componentes presentes no JSON.
* Ele adiciona um atributo de dados HTML ao HTML que o componente JS renderiza, para que o Editor de SPA saiba qual caixa de diálogo exibir para o autor ao editar o componente.

Para obter mais informações sobre o uso de `MapTo` e a criação do AEM para SPA em geral, consulte o guia de Introdução para a estrutura escolhida.

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
   1. Quando o aplicativo SPA é executado, o JSON é solicitado, permitindo que o aplicativo crie o DOM da página, incluindo o `cq-data` atributos.
   1. A variável `cq-data` Os atributos permitem que o editor carregue informações de página adicionais para que saiba quais configurações de edição estão disponíveis para os componentes.

* **Publicação no AEM**

  Onde o conteúdo criado e as bibliotecas compiladas, incluindo artefatos de aplicativo SPA, bibliotecas de clientes e componentes, são publicados para consumo público.

* **Dispatcher/CDN**

  O Dispatcher serve como a camada de armazenamento em cache do AEM para os visitantes do site.
   * As solicitações são processadas de forma semelhante à forma como estão no autor do AEM. No entanto, não há solicitação das informações da página porque elas só são necessárias para o editor.
   * JavaScript, CSS, JSON e HTML são armazenados em cache, otimizando a página para entrega rápida.

>[!NOTE]
>
>Dentro do AEM, não há necessidade de executar mecanismos de criação JavaScript ou executar o próprio JavaScript. O AEM hospeda somente os artefatos compilados do aplicativo SPA.

## Próximas etapas {#next-steps}

* [Introdução ao SPA no AEM usando o React](getting-started-react.md) mostra como um SPA básico é construído para funcionar com o editor SPA no AEM usando o React.
* [Introdução ao SPA no AEM usando o Angular](getting-started-angular.md) mostra como um SPA básico é construído para funcionar com o editor SPA no AEM usando o Angular.
* A [Visão geral do editor de SPA](editor-overview.md) aborda em detalhes o modelo de comunicação do AEM e do SPA.
* [Projeto SPA WKND](wknd-tutorial.md) O é um tutorial passo a passo para a implementação de um projeto simples de SPA no AEM.
* [Modelo dinâmico para mapeamento de componentes para SPA](model-to-component-mapping.md) SPA explica o modelo dinâmico para o mapeamento de componentes e como ele funciona dentro do AEM.
* [Blueprint SPA](blueprint.md) O oferece um aprofundamento em como o SDK do SPA para AEM funciona caso você queira implementar o SPA no AEM para uma estrutura diferente do React ou do Angular. Ou você simplesmente gostaria de uma compreensão mais profunda.
