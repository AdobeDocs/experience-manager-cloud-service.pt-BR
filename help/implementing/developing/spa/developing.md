---
title: Desenvolver SPA para AEM
description: Este artigo apresenta questões importantes a serem consideradas ao envolver um desenvolvedor de front-end para desenvolver uma SPA para AEM, além de fornecer uma visão geral da arquitetura do AEM em relação à SPA para ter em mente ao implantar um SPA desenvolvido no AEM.
translation-type: tm+mt
source-git-commit: 0799a817095558edd49b53ddc915c9474181fef7
workflow-type: tm+mt
source-wordcount: '2078'
ht-degree: 0%

---


# Desenvolver SPA para AEM {#developing-spas-for-aem}

Aplicativos de página única (SPA) podem oferta experiências interessantes para usuários de sites. Os desenvolvedores querem ser capazes de criar sites usando estruturas SPA e os autores querem editar o conteúdo no AEM para um site criado usando essas estruturas.

Este artigo apresenta questões importantes a serem consideradas ao envolver um desenvolvedor de front-end para desenvolver uma SPA para AEM e fornece uma visão geral da arquitetura do AEM em relação à implantação do SPA no AEM.

## Princípios de desenvolvimento SPA para AEM {#spa-development-principles-for-aem}

O desenvolvimento de aplicativos de página única em AEM pressupõe que o desenvolvedor front-end observe as práticas recomendadas padrão ao criar um SPA. Se você seguir essas práticas recomendadas gerais e alguns princípios específicos para AEM como desenvolvedor front-end, seu SPA funcionará com [AEM e seus recursos](introduction.md#content-editing-experience-with-spa)de criação de conteúdo.

* **[Portabilidade](#portability)** - Como com qualquer componente, os componentes devem ser construídos para serem o mais portáteis possível. O SPA deve ser construído com componentes portáveis e reutilizáveis.
* **[Estrutura](#aem-drives-site-structure)** do site do AEM - o desenvolvedor do front-end cria componentes e é proprietário de sua estrutura interna, mas depende do AEM para definir a estrutura de conteúdo do site.
* **[Renderização](#dynamic-rendering)** dinâmica: todas as renderizações devem ser dinâmicas.
* **[Roteamento](#dynamic-routing)** dinâmico - O SPA é responsável pelo roteamento e AEM o escuta e busca com base nele. Qualquer roteamento também deve ser dinâmico.

Se você tiver esses princípios em mente ao desenvolver seu SPA, ele será o mais flexível e a prova futura possível, além de permitir a funcionalidade de criação AEM suportada.

Se não precisar suportar os recursos de criação AEM, talvez seja necessário considerar um modelo [de design](#spa-design-models)SPA diferente.

### Portabilidade {#portability}

Como ao desenvolver qualquer componente, seus componentes devem ser projetados de modo a maximizar sua portabilidade. Quaisquer padrões que funcionem contra a portabilidade ou a reusabilidade dos componentes devem ser evitados para garantir a compatibilidade, flexibilidade e manutenção futura.

O SPA resultante deve ser construído com componentes altamente portáteis e reutilizáveis.

### Estrutura do site das unidades AEM {#aem-drives-site-structure}

O desenvolvedor front-end deve se considerar responsável pela criação de uma biblioteca de componentes SPA usados para criar o aplicativo. O desenvolvedor front-end tem controle total da estrutura interna dos componentes. [No entanto, AEM sempre possui a estrutura do site.](editor-overview.md)

Isso significa que o desenvolvedor front-end pode adicionar conteúdo ao cliente antes ou depois do ponto de entrada dos componentes e também pode fazer chamadas de terceiros dentro do componente. No entanto, o desenvolvedor de front-end não está no controle total de como os componentes são aninhados, por exemplo.

### Renderização dinâmica {#dynamic-rendering}

O SPA deve depender apenas da renderização dinâmica do conteúdo. Essa é a expectativa padrão na qual AEM busca e renderiza todos os filhos da estrutura de conteúdo.

Qualquer renderização explícita que aponte para um conteúdo específico é considerada uma renderização estática e, embora seja suportada, não será compatível com AEM recursos de criação de conteúdo. Isto também vai contra o princípio da [portabilidade](#portability).

### Roteamento dinâmico {#dynamic-routing}

Assim como na renderização, todos os roteamentos também devem ser dinâmicos. No AEM, [o SPA deve ser o proprietário do roteamento](routing.md) e AEM o ouve e busca conteúdo com base nele.

Qualquer roteamento estático funciona de acordo com o [princípio da portabilidade](#portability) e limita o autor ao não ser compatível com os recursos de criação de conteúdo da AEM. Por exemplo, com roteamento estático, se o autor do conteúdo quiser alterar uma rota ou uma página, ele ou ela precisará solicitar que o desenvolvedor de front-end faça isso.

## Arquétipo de projeto do AEM{#aem-project-archetype}

Qualquer projeto AEM deve aproveitar o [AEM Project Archetype](https://docs.adobe.com/content/help/pt-BR/experience-manager-core-components/using/developing/archetype/overview.html), que suporta projetos SPA usando React ou Angular e aproveita o SPA SDK.

## Modelos de design SPA {#spa-design-models}

Se os [princípios de desenvolvimento de SPA em AEM](#spa-development-principles-for-aem) forem seguidos, seu SPA funcionará com todos os recursos de criação AEM conteúdo suportados.

No entanto, podem existir casos em que tal não seja inteiramente necessário. A tabela a seguir apresenta uma visão geral dos vários modelos de design, suas vantagens e suas desvantagens.

<table>
 <tbody>
  <tr>
   <th><strong>Modelo de design<br /> </strong></th>
   <th><strong>Vantagens</strong></th>
   <th><strong>Desvantagens</strong></th>
  </tr>
  <tr>
   <td>AEM é usado como um CMS sem cabeçalho sem usar a estrutura do SDK do Editor de <a href="/help/implementing/developing/spa/reference-materials.md">SPA.</a></td>
   <td>O desenvolvedor front-end tem controle total sobre o aplicativo.</td>
   <td><p>Os autores de conteúdo não podem aproveitar AEM experiência de criação de conteúdo.</p> <p>O código não é portátil nem reutilizável se contiver referências estáticas ou roteamento.</p> <p>Não permite o uso do editor de modelo, portanto, o desenvolvedor front-end deve manter modelos editáveis por meio do JCR.</p> </td>
  </tr>
  <tr>
   <td>O desenvolvedor front-end usa a estrutura do SDK do Editor de SPA, mas abre apenas algumas áreas para o autor do conteúdo.</td>
   <td>O desenvolvedor mantém controle sobre o aplicativo, permitindo apenas a criação em áreas restritas do aplicativo.</td>
   <td><p>Os autores de conteúdo são restritos a um conjunto limitado de experiências de criação de conteúdo AEM.</p> <p>O código pode não ser portátil nem reutilizável se contiver referências estáticas ou roteamento.</p> <p>Não permite o uso do editor de modelo, portanto, o desenvolvedor front-end deve manter modelos editáveis por meio do JCR.</p> </td>
  </tr>
  <tr>
   <td>O projeto aproveita totalmente o SDK do Editor de SPA e os componentes de front-end são desenvolvidos como uma biblioteca e a estrutura de conteúdo do aplicativo é delegada à AEM.</td>
   <td><p>O aplicativo é reutilizável e portátil.</p> <p>O autor do conteúdo pode editar o aplicativo usando AEM experiência de criação de conteúdo.<br /> </p> <p>O SPA é compatível com o editor de modelo.</p> </td>
   <td><p>O desenvolvedor não controla a estrutura do aplicativo e a parte do conteúdo delegada ao AEM.</p> <p>O desenvolvedor ainda pode reservar áreas do aplicativo para o conteúdo que não deve ser criado usando AEM.</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Embora todos os modelos sejam suportados em AEM, somente ao implementar o terceiro (e, portanto, seguir os princípios de desenvolvimento de [SPA recomendados em AEM](#spa-development-principles-for-aem)) os autores de conteúdo poderão interagir e editar o conteúdo do SPA em AEM, conforme estiverem acostumados.

## Migração de SPA existentes para AEM {#migrating-existing-spas-to-aem}

Geralmente, se sua SPA seguir os princípios de desenvolvimento de [SPA para AEM](#spa-development-principles-for-aem), sua SPA funcionará em AEM e poderá ser editada usando o editor de SPA de AEM.

Siga estas etapas para preparar seu SPA existente para trabalhar com AEM.

1. **Torne seus componentes JS modulares.** - Torná-los capazes de serem apresentados em qualquer ordem, posição e tamanho.
1. **Use os container fornecidos pelo SDK para colocar seus componentes na tela.** - AEM fornece um componente de sistema de página e parágrafo para você usar.
1. **Crie um componente AEM para cada componente JS.** - Os componentes AEM definem a caixa de diálogo e a saída JSON.

## Instruções para desenvolvedores front-end {#instructions-for-front-end-developers}

A principal tarefa de envolver um desenvolvedor front-end para criar um SPA para AEM é concordar com os componentes e seus modelos JSON.

A seguir está um resumo das etapas que um desenvolvedor front-end precisa seguir ao desenvolver um SPA para AEM.

1. **Concordar em componentes e em seus modelos JSON**

   Desenvolvedores front-end e desenvolvedores de AEM back-end precisam concordar sobre quais componentes são necessários e um modelo para que haja uma correspondência individual entre SPA componentes e os componentes back-end.

   AEM componentes ainda são necessários principalmente para fornecer caixas de diálogo de edição e exportar o modelo do componente.

1. **Em Reagir componentes, acesse o modelo via`this.props.cqModel`**

   Depois que os componentes forem aceitos e o modelo JSON estiver implementado, o desenvolvedor de front-end poderá desenvolver o SPA e simplesmente acessar o modelo JSON via `this.props.cqModel`.

1. **Implementar o `render()` método do componente**

   O desenvolvedor de front-end implementa o `render()` método como ele considera adequado e pode usar os campos da `cqModel` propriedade. Isso gera os fragmentos DOM e HTML que serão inseridos na página. Essa é a maneira padrão de criar um aplicativo no React.

1. **Mapeie o componente para o tipo de recurso AEM via`MapTo()`**

   O mapeamento armazena classes de componentes e é usado internamente pelo componente fornecido `Container` para recuperar e instanciar dinamicamente componentes com base no tipo de recurso fornecido.

   Isso serve como a &quot;colagem&quot; entre front-end e back-end para que o editor saiba a quais componentes os componentes reagem correspondem.

   Os `Page` e `ResponsiveGrid` são bons exemplos de classes que estendem a base `Container`.

1. **Defina o parâmetro do componente `EditConfig` como`MapTo()`**

   Esse parâmetro é necessário para informar ao editor como o componente deve ser nomeado desde que ainda não seja renderizado ou não tenha conteúdo para renderizar.

1. **Estender a `Container` classe fornecida para páginas e container**

   Os sistemas de páginas e parágrafos devem estender essa classe para que a delegação aos componentes internos funcione como esperado.

1. **Implemente uma solução de roteamento que use a API HTML5 `History` .**

   Quando o `ModelRouter` estiver ativado, chamar as funções `pushState` e `replaceState` disparará uma solicitação para o `PageModelManager` para buscar um fragmento ausente do modelo.

   A versão atual do suporte `ModelRouter` apenas ao uso de URLs que apontam para o caminho de recurso real dos pontos de entrada do Modelo Sling. Ele não suporta o uso de URLs personalizados ou aliases.

   O `ModelRouter` pode ser desabilitado ou configurado para ignorar uma lista de expressões regulares.

## AEM-Agnóstico {#aem-agnostic}

Esses blocos de código ilustram como seus componentes React e Angular não precisam de nada específico para o Adobe ou AEM.

* Tudo o que está dentro do componente JavaScript é AEM-agnóstico.
* O que, no entanto, é específico para AEM é que o componente JS deve ser mapeado para um componente AEM com o auxiliar MapTo.

![AEM abordagem agnóstica](assets/aem-agnostic.png)

O `MapTo` auxiliar é a &quot;cola&quot; que permite que os componentes de back-end e de front-end sejam combinados:

* Ele informa ao container JS (ou sistema de parágrafo JS) qual componente JS é responsável pela renderização de cada um dos componentes presentes no JSON.
* Ele adiciona um atributo de dados HTML ao HTML que o componente JS renderiza, para que o Editor de SPA saiba qual caixa de diálogo será exibida ao autor ao editar o componente.

Para obter mais informações sobre como usar `MapTo` e criar SPA para AEM em geral, consulte o guia Introdução para sua estrutura escolhida.

* [Introdução ao SPA no AEM usando React](getting-started-react.md)
* [Introdução ao SPA no AEM usando o Angular](getting-started-angular.md)

## Arquitetura AEM e SPA {#aem-architecture-and-spas}

A arquitetura geral de AEM incluindo ambientes de desenvolvimento, criação e publicação não é alterada ao usar SPA. No entanto, é útil entender como o desenvolvimento SPA se encaixa nessa arquitetura.

![Arquitetura AEM e SPA](assets/aem-architecture.png)

* **Criar Ambiente**

   É aqui que a origem do aplicativo SPA e a fonte do componente são desconectadas.

   * O gerador clientlib do NPM cria uma biblioteca de clientes a partir do projeto SPA.
   * Essa biblioteca será tirada pelo Maven e implantada pelo plug-in Maven Build juntamente com o componente para o autor do AEM.

* **AEM Author**

   O conteúdo é criado no autor AEM, incluindo a criação de SPA.

   Quando um SPA é editado usando o Editor SPA no ambiente de criação:

   1. O SPA solicita o HTML externo.
   1. O CSS é carregado.
   1. O Javascript do aplicativo SPA é carregado.
   1. Quando o aplicativo SPA é executado, o JSON é solicitado, permitindo que o aplicativo crie o DOM da página incluindo os `cq-data` atributos.
   1. Esses `cq-data` atributos permitem que o editor carregue informações adicionais da página para que ele saiba quais configurações de edição estão disponíveis para os componentes.

* **AEM Publish**

   É aqui que o conteúdo criado e as bibliotecas compiladas, incluindo artefatos SPA aplicativos, clientlibs e componentes, são publicados para consumo público.

* **Dispatcher / CDN**

   O dispatcher serve como a camada de cache de AEM para visitantes no site.
   * As solicitações são processadas de forma semelhante à forma como estão no autor de AEM, no entanto, não há solicitação de informações da página, pois isso só é necessário para o editor.
   * Javascript, CSS, JSON e HTML são armazenados em cache, otimizando a página para delivery rápido.

>[!NOTE]
>
>Dentro AEM não há necessidade de executar os mecanismos de criação do Javascript ou executar o próprio Javascript. AEM hospeda somente os artefatos compilados do aplicativo SPA.

## Próximas etapas {#next-steps}

* [A Introdução ao SPA no AEM usando o React](getting-started-react.md) mostra como um SPA básico foi criado para funcionar com o Editor SPA no AEM usando o React.
* [A Introdução ao SPA no AEM usando o Angular](getting-started-angular.md) mostra como um SPA básico foi criado para funcionar com o Editor SPA no AEM usando o Angular.
* [SPA Visão geral](editor-overview.md) do editor aprofunda o modelo de comunicação entre AEM e o SPA.
* [SPA Projeto](wknd-tutorial.md) WKND é um tutorial passo a passo que implementa um projeto SPA simples em AEM.
* [O Modelo dinâmico para mapeamento de componentes para SPA](model-to-component-mapping.md) explica o modelo dinâmico para mapeamento de componentes e como ele funciona dentro do SPA em AEM.
* [SPA Blueprint](blueprint.md) oferta um aprofundamento sobre como o SDK SPA para AEM funciona caso você deseje implementar SPA em AEM para uma estrutura diferente de React ou Angular ou simplesmente deseje um entendimento mais profundo.
