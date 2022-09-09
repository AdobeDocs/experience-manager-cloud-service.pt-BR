---
title: Desenvolvimento de SPAs para o AEM
description: Este artigo apresenta questões importantes a serem consideradas ao engajar um desenvolvedor de front-end para desenvolver uma SPA para AEM, além de fornecer uma visão geral da arquitetura de AEM em relação à SPA para manter em mente ao implantar uma SPA desenvolvida em AEM.
exl-id: f6c6f31a-69ad-48f6-b995-e6d0930074df
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '2076'
ht-degree: 1%

---

# Desenvolvimento de SPAs para o AEM {#developing-spas-for-aem}

Aplicativos de página única (SPAs) podem oferecer experiências interessantes para usuários de sites. Os desenvolvedores desejam criar sites usando estruturas SPA e os autores desejam editar o conteúdo com facilidade no AEM para um site criado usando essas estruturas.

Este artigo apresenta questões importantes a serem consideradas ao envolver um desenvolvedor de front-end para desenvolver uma SPA para AEM e fornece uma visão geral da arquitetura de AEM em relação à implantação de SPA no AEM.

## Princípios de desenvolvimento SPA para AEM {#spa-development-principles-for-aem}

O desenvolvimento de aplicativos de página única no AEM parte do princípio de que o desenvolvedor front-end cumpre as práticas recomendadas padrão ao criar um SPA. Se, como desenvolvedor front-end, você seguir essas práticas recomendadas gerais, bem como alguns princípios específicos de AEM, seu SPA funcionará com [AEM e seus recursos de criação de conteúdo](introduction.md#content-editing-experience-with-spa).

* **[Portabilidade](#portability)** - Assim como com qualquer componente, os componentes devem ser construídos para serem tão portáteis quanto possível. A SPA deve ser criada com componentes portáveis e reutilizáveis.
* **[AEM unidades Estrutura do Site](#aem-drives-site-structure)** - O desenvolvedor de front-end cria componentes e é proprietário de sua estrutura interna, mas depende do AEM para definir a estrutura de conteúdo do site.
* **[Renderização dinâmica](#dynamic-rendering)** - Todas as renderizações devem ser dinâmicas.
* **[Roteamento dinâmico](#dynamic-routing)** - O SPA é responsável pelo roteamento e AEM o escuta e busca com base nele. Qualquer roteamento também deve ser dinâmico.

Caso tenha esses princípios em mente ao desenvolver seu SPA, ele será o mais flexível e uma prova futura possível, além de ativar todas as funcionalidades de criação AEM compatíveis.

Se você não precisar oferecer suporte aos recursos de criação de AEM, talvez seja necessário considerar um [Modelo de design SPA](#spa-design-models).

### Portabilidade {#portability}

Assim como ao desenvolver qualquer componente, seus componentes devem ser projetados de forma a maximizar sua portabilidade. Quaisquer padrões que funcionem contra a portabilidade ou a reutilização dos componentes devem ser evitados para garantir a compatibilidade, flexibilidade e sustentabilidade a partir de agora.

O SPA resultante deve ser construído com componentes altamente portáteis e reutilizáveis.

### AEM unidades Estrutura do Site {#aem-drives-site-structure}

O desenvolvedor front-end deve se considerar responsável pela criação de uma biblioteca de componentes SPA usados para criar o aplicativo. O desenvolvedor front-end tem controle total da estrutura interna dos componentes. [No entanto, AEM sempre possui a estrutura do site.](editor-overview.md)

Isso significa que o desenvolvedor de front-end pode adicionar conteúdo de cliente antes ou depois do ponto de entrada dos componentes e também pode fazer chamadas de terceiros dentro do componente. No entanto, o desenvolvedor de front-end não tem controle total sobre como os componentes são aninhados, por exemplo.

### Renderização dinâmica {#dynamic-rendering}

O SPA deve depender apenas da renderização dinâmica do conteúdo. Essa é a expectativa padrão em que o AEM busca e renderiza todos os filhos da estrutura de conteúdo.

Qualquer renderização explícita que aponte para um conteúdo específico é considerada renderização estática e, embora seja suportada, não será compatível com AEM recursos de criação de conteúdo. Isto também contraria o princípio da [portabilidade](#portability).

### Roteamento dinâmico {#dynamic-routing}

Assim como com a renderização, todo o roteamento também deve ser dinâmico. Em AEM, [o SPA deve sempre ser o proprietário do roteamento](routing.md) e AEM escuta e busca conteúdo com base nela.

Qualquer roteamento estático funciona em relação à variável [princípio da portabilidade](#portability) e limita o autor ao não ser compatível com os recursos de criação de conteúdo do AEM. Por exemplo, com roteamento estático, se o autor de conteúdo quiser alterar uma rota ou alterar uma página, ele precisará solicitar que o desenvolvedor de front-end faça isso.

## Arquétipo de projeto do AEM {#aem-project-archetype}

Qualquer projeto AEM deve aproveitar [Arquétipo de projeto AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=pt_BR), que suporta projetos SPA usando o React ou Angular e aproveita o SDK SPA.

## Modelos de design de SPA {#spa-design-models}

Se a variável [princípios do desenvolvimento da SPA em AEM](#spa-development-principles-for-aem) forem seguidas, sua SPA funcionará com todos os recursos de criação de conteúdo AEM compatíveis.

No entanto, pode haver casos em que tal não seja totalmente necessário. A tabela a seguir apresenta uma visão geral dos vários modelos de design, suas vantagens e suas desvantagens.

<table>
 <tbody>
  <tr>
   <th><strong>Modelo de design<br /> </strong></th>
   <th><strong>Vantagens</strong></th>
   <th><strong>Desvantagens</strong></th>
  </tr>
  <tr>
   <td>AEM é usado como um CMS sem periféricos sem usar o <a href="/help/implementing/developing/hybrid/reference-materials.md">SPA estrutura do SDK do Editor.</a></td>
   <td>O desenvolvedor front-end tem controle total sobre o aplicativo.</td>
   <td><p>Os autores de conteúdo não podem aproveitar AEM experiência de criação de conteúdo.</p> <p>O código não é portátil nem reutilizável se contiver referências estáticas ou roteamento.</p> <p>Não permite o uso do editor de modelo, portanto, o desenvolvedor de front-end deve manter modelos editáveis por meio do JCR.</p> </td>
  </tr>
  <tr>
   <td>O desenvolvedor de front-end usa a estrutura do SDK do Editor de SPA, mas abre apenas algumas áreas para o autor de conteúdo.</td>
   <td>O desenvolvedor mantém o controle sobre o aplicativo, permitindo apenas a criação em áreas restritas do aplicativo.</td>
   <td><p>Os autores de conteúdo são restritos a um conjunto limitado de AEM experiência de criação de conteúdo.</p> <p>O código pode não ser portátil nem reutilizável se contiver referências estáticas ou roteamento.</p> <p>Não permite o uso do editor de modelo, portanto, o desenvolvedor de front-end deve manter modelos editáveis por meio do JCR.</p> </td>
  </tr>
  <tr>
   <td>O projeto aproveita totalmente o SDK do Editor de SPA e os componentes de primeiro plano são desenvolvidos como uma biblioteca e a estrutura de conteúdo do aplicativo é delegada à AEM.</td>
   <td><p>O aplicativo é reutilizável e portátil.</p> <p>O autor de conteúdo pode editar o aplicativo usando AEM experiência de criação de conteúdo.<br /> </p> <p>O SPA é compatível com o editor de modelo.</p> </td>
   <td><p>O desenvolvedor não está no controle da estrutura do aplicativo e da parte do conteúdo delegada ao AEM.</p> <p>O desenvolvedor ainda pode reservar áreas do aplicativo para o conteúdo que não deve ser criado usando o AEM.</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Embora todos os modelos sejam compatíveis com o AEM, apenas com a implementação do terceiro (e, portanto, seguindo o [SPA princípios de desenvolvimento em AEM](#spa-development-principles-for-aem)) os autores de conteúdo poderão interagir e editar o conteúdo da SPA no AEM como estão acostumados.

## Migrando SPA existentes para AEM {#migrating-existing-spas-to-aem}

Geralmente, se o SPA seguir a variável [Princípios de desenvolvimento SPA para AEM](#spa-development-principles-for-aem), seu SPA funcionará no AEM e poderá ser editado usando o Editor de SPA AEM.

Siga estas etapas para preparar seu SPA existente para trabalhar com o AEM.

1. **Torne seus componentes JS modulares.** - Torná-los capazes de ser processados em qualquer ordem, posição e tamanho.
1. **Use os contêineres fornecidos pelo SDK para colocar seus componentes na tela.** - AEM fornece um componente de sistema de página e parágrafo para você usar.
1. **Crie um componente de AEM para cada componente JS.** - Os componentes AEM definem a caixa de diálogo e a saída JSON.

## Instruções para desenvolvedores front-end {#instructions-for-front-end-developers}

A principal tarefa para envolver um desenvolvedor de front-end para criar um SPA para AEM é concordar com os componentes e seus modelos JSON.

Veja a seguir um esboço das etapas que um desenvolvedor de front-end precisa seguir ao desenvolver um SPA para AEM.

1. **Concordar em componentes e em seu modelo JSON**

   Os desenvolvedores front-end e os desenvolvedores de AEM back-end precisam concordar sobre quais componentes são necessários e um modelo para que haja uma correspondência individual entre SPA componentes e os componentes back-end.

   AEM componentes ainda são necessários, principalmente para fornecer caixas de diálogo de edição e exportar o modelo de componentes.

1. **Nos componentes React , acesse o modelo por meio de`this.props.cqModel`**

   Depois que os componentes forem aceitos e o modelo JSON estiver em vigor, o desenvolvedor front-end poderá desenvolver o SPA e simplesmente acessar o modelo JSON por meio de `this.props.cqModel`.

1. **Implementar `render()` método**

   O desenvolvedor de front-end implementa o `render()` , como consideram adequado, e podem usar os campos do `cqModel` propriedade. Isso gera os fragmentos DOM e HTML que serão inseridos na página. Esta é a maneira padrão de criar um aplicativo no React.

1. **Mapeie o componente para o tipo de recurso AEM por meio de`MapTo()`**

   O mapeamento armazena classes de componentes e é usado internamente pelo `Container` componente para recuperar e instanciar dinamicamente componentes com base no tipo de recurso especificado.

   Isso serve como a &quot;cola&quot; entre front-end e back-end para que o editor saiba a quais componentes os componentes de reação correspondem.

   O `Page` e `ResponsiveGrid` são bons exemplos de classes que estendem a base `Container`.

1. **Defina o `EditConfig` como parâmetro para`MapTo()`**

   Esse parâmetro é necessário para informar ao editor como o componente deve ser nomeado, desde que o ainda não seja renderizado ou não tenha conteúdo para renderização.

1. **Estender o `Container` classe para páginas e contêineres**

   Os sistemas de páginas e parágrafo devem estender essa classe para que a delegação para componentes internos funcione conforme esperado.

1. **Implemente uma solução de roteamento que use o HTML5 `History` API.**

   Quando a variável `ModelRouter` está ativado, chamando a função `pushState` e `replaceState` As funções do acionarão uma solicitação para `PageModelManager` para buscar um fragmento ausente do modelo.

   A versão atual do `ModelRouter` suporta apenas o uso de URLs que apontem para o caminho de recurso real dos pontos de entrada do Modelo do Sling. Não é compatível com o uso de URLs personalizados ou aliases.

   O `ModelRouter` pode ser desativado ou configurado para ignorar uma lista de expressões regulares.

## AEM-Agnóstico {#aem-agnostic}

Esses blocos de código ilustram como os componentes do React e do Angular não precisam de nada específico do Adobe ou AEM.

* Tudo o que está dentro do componente JavaScript é independente de AEM.
* No entanto, o que é específico para AEM é que o componente JS deve ser mapeado para um componente AEM com o auxiliar MapTo .

![AEM abordagem agnóstico](assets/aem-agnostic.png)

O `MapTo` O auxiliar é a &quot;cola&quot; que permite que os componentes de back-end e de front-end sejam combinados:

* Informa ao contêiner JS (ou sistema de parágrafo JS) qual componente JS é responsável pela renderização de cada um dos componentes presentes no JSON.
* Ele adiciona um atributo HTML data ao HTML que o componente JS renderiza, para que o Editor de SPA saiba qual caixa de diálogo exibir ao autor ao editar o componente.

Para obter mais informações sobre como usar `MapTo` e criando SPA para AEM em geral, consulte o guia de Introdução para sua estrutura escolhida.

* [Introdução ao SPA no AEM usando o React](getting-started-react.md)
* [Introdução ao SPA no AEM usando o Angular](getting-started-angular.md)

## Arquitetura AEM e SPA {#aem-architecture-and-spas}

A arquitetura geral de AEM incluindo ambientes de desenvolvimento, criação e publicação não é alterada ao usar SPA. No entanto, é útil entender como o desenvolvimento SPA se encaixa nessa arquitetura.

![Arquitetura AEM e SPA](assets/aem-architecture.png)

* **Ambiente de criação**

   É aqui que a origem do aplicativo SPA e a origem do componente são verificadas.

   * O gerador clientlib do NPM cria uma biblioteca do cliente do projeto do SPA.
   * Essa biblioteca será obtida pelo Maven e implantada pelo plug-in Maven Build, juntamente com o componente para o autor do AEM.

* **Autor do AEM**

   O conteúdo é criado no autor do AEM, incluindo a criação de SPA.

   Quando um SPA é editado usando o Editor de SPA no ambiente de criação:

   1. O SPA solicita o HTML externo.
   1. O CSS é carregado.
   1. O Javascript do aplicativo SPA é carregado.
   1. Quando o aplicativo de SPA é executado, o JSON é solicitado, permitindo que o aplicativo crie o DOM da página, incluindo o `cq-data` atributos.
   1. Essa `cq-data` os atributos do permitem que o editor carregue informações adicionais da página para que saiba quais configurações de edição estão disponíveis para os componentes.

* **AEM Publish**

   É aqui que o conteúdo criado e as bibliotecas compiladas, incluindo artefatos SPA aplicativo, clientlibs e componentes, são publicados para consumo público.

* **Dispatcher / CDN**

   O dispatcher serve como a camada de cache de AEM para os visitantes do site.
   * As solicitações são processadas de forma semelhante à forma como estão no Autor do AEM, no entanto, não há solicitação das informações da página, pois isso só é necessário para o editor.
   * Javascript, CSS, JSON e HTML são armazenados em cache, otimizando a página para entrega rápida.

>[!NOTE]
>
>No AEM, não há necessidade de executar mecanismos de criação do Javascript ou executar o próprio Javascript. AEM hospeda somente os artefatos compilados do aplicativo SPA.

## Próximas etapas {#next-steps}

* [Introdução ao SPA no AEM usando o React](getting-started-react.md) mostra como um SPA básico é criado para funcionar com o Editor de SPA no AEM usando o React.
* [Introdução ao SPA no AEM usando o Angular](getting-started-angular.md) mostra como um SPA básico é criado para funcionar com o Editor de SPA no AEM usando o Angular.
* [Visão geral do editor de SPA](editor-overview.md) aprofunda o modelo de comunicação entre AEM e SPA.
* [Projeto SPA WKND](wknd-tutorial.md) O é um tutorial passo a passo que implementa um projeto de SPA simples no AEM.
* [Modelo dinâmico para mapeamento de componentes para SPA](model-to-component-mapping.md) explica o modelo dinâmico para o mapeamento de componentes e como ele funciona no SPA em AEM.
* [SPA Blueprint](blueprint.md) O oferece um mergulho profundo em como o SDK do SPA para AEM funciona, caso você deseje implementar SPA em AEM para uma estrutura diferente de React ou Angular ou deseje simplesmente uma compreensão mais profunda.
