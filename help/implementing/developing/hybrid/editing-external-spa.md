---
title: Edição de um SPA externo em AEM
description: Este documento descreve as etapas recomendadas para carregar um SPA independente em uma instância AEM, adicionar seções editáveis de conteúdo e ativar a criação.
translation-type: tm+mt
source-git-commit: bb8ab907dbeb422db410328f9c559c6794c16a8f
workflow-type: tm+mt
source-wordcount: '2127'
ht-degree: 0%

---

# Editar um SPA externo em AEM {#editing-external-spa-within-aem}

Ao decidir [que nível de integração](/help/implementing/developing/headful-headless.md) você gostaria de ter entre seus SPA externos e AEM, geralmente é necessário ser capaz de editar e visualização os SPA dentro do AEM.

## Visão geral {#overview}

Este documento descreve as etapas recomendadas para carregar um SPA independente em uma instância AEM, adicionar seções editáveis de conteúdo e ativar a criação.

## Pré-requisitos {#prerequisites}

Os pré-requisitos são simples.

* Verifique se uma instância do AEM está sendo executada localmente.
* Crie um AEM base SPA projeto usando [o Arquétipo de Projeto AEM.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?#available-properties)
   * Isso será a base do projeto AEM que será atualizado para incluir a SPA externa.
   * Para as amostras neste documento, estamos usando o ponto de partida de [o projeto SPA WKND.](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/spa-editor/spa-editor-framework-feature-video-use.html#spa-editor)
* Tenha a SPA de reação externa e funcional que você deseja integrar à mão.

## Carregar SPA para AEM Projeto {#upload-spa-to-aem-project}

Primeiro, você precisa carregar o SPA externo no seu projeto AEM.

1. Substitua `src` na pasta de projeto `/ui.frontend` pela pasta `src` do aplicativo React.
1. Inclua quaisquer dependências adicionais no `package.json` do aplicativo no arquivo `/ui.frontend/package.json`.
   * Verifique se as dependências do SDK SPA são de [versões recomendadas.](/help/implementing/developing/hybrid/getting-started-react.md#dependencies)
1. Inclua quaisquer personalizações na pasta `/public`.
1. Inclua todos os scripts ou estilos incorporados adicionados ao arquivo `/public/index.html`.

## Configure o SPA remoto {#configure-remote-spa}

Agora que o SPA externo faz parte do seu projeto AEM, ele precisa ser configurado dentro do AEM.

### Incluir pacotes SDK do Adobe SPA {#include-spa-sdk-packages}

Para aproveitar AEM recursos SPA, há dependências nos três pacotes a seguir.

* [`@adobe/aem-react-editable-components`](https://github.com/adobe/aem-react-editable-components)
* [`@adobe/aem-spa-component-mapping`](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping)
* [`@adobe/aem-spa-page-model-manager`](https://www.npmjs.com/package/@adobe/aem-spa-model-manager)

`@adobe/aem-spa-page-model-manager` fornece a API para inicializar um Gerenciador de modelos e recuperar o modelo da instância AEM. Esse modelo pode ser usado para renderizar AEM componentes usando APIs de `@adobe/aem-react-editable-components` e `@adobe/aem-spa-component-mapping`.

#### Instalação {#installation}

Execute o seguinte comando npm para instalar os pacotes necessários.

```shell
npm install --save @adobe/aem-spa-component-mapping @adobe/aem-spa-page-model-manager @adobe/aem-react-editable-components
```

### Inicialização do ModelManager {#model-manager-initialization}

Antes da renderização do aplicativo, [`ModelManager`](/help/implementing/developing/hybrid/blueprint.md#pagemodelmanager) precisa ser inicializado para lidar com a criação do AEM `ModelStore`.

Isso precisa ser feito dentro do arquivo `src/index.js` do aplicativo ou onde a raiz do aplicativo for renderizada.

Para isso, podemos usar a API `initializationAsync` fornecida pelo `ModelManager`.

A seguinte captura de tela mostra como ativar a inicialização do `ModelManager` em um aplicativo React simples. A única restrição é que `initializationAsync` precisa ser chamado antes de `ReactDOM.render()`.

![Inicializar o ModelManager](assets/external-spa-initialize-modelmanager.png)

Neste exemplo, `ModelManager` é inicializado e um `ModelStore` vazio é criado.

`initializationAsync` pode aceitar opcionalmente um  `options` objeto como parâmetro:

* `path` - Na inicialização, o modelo no caminho definido é obtido e armazenado no  `ModelStore`. Isso pode ser usado para buscar `rootModel` na inicialização, se necessário.
* `modelClient` - Permite fornecer um cliente personalizado responsável pela busca do modelo.
* `model` - Um  `model` objeto passado como parâmetro normalmente preenchido ao  [usar SSR.](/help/implementing/developing/hybrid/ssr.md)

### AEM Componentes de Folha Autorizáveis {#authorable-leaf-components}

1. Crie/identifique um componente AEM para o qual um componente React autorável será criado. Neste exemplo, estamos usando o componente de texto do projeto WKND.

   ![Componente de texto WKND](assets/external-spa-text-component.png)

1. Crie um componente de texto Reagir simples no SPA. Neste exemplo, um novo arquivo `Text.js` foi criado com o seguinte conteúdo.

   ![Text.js](assets/external-spa-textjs.png)

1. Crie um objeto de configuração para especificar os atributos necessários para permitir a edição de AEM.

   ![Criar objeto de configuração](assets/external-spa-config-object.png)

   * `resourceType` é obrigatório mapear o componente React para o componente AEM e ativar a edição ao abrir no editor de AEM.

1. Use a função de invólucro `withMappable`.

   ![Usar comMapable](assets/external-spa-withmappable.png)

   Essa função de empacotador mapeia o componente React para o AEM `resourceType` especificado na configuração e habilita os recursos de edição quando abertos no editor de AEM. Para componentes independentes, ele também buscará o conteúdo do modelo para o nó específico.

   >[!NOTE]
   >
   >Neste exemplo, há versões diferentes do componente: AEM componentes de Reação embutidos e desempacotados. A versão encapsulada precisa ser usada ao usar explicitamente o componente. Quando o componente faz parte de uma página, você pode continuar usando o componente padrão, como feito atualmente no editor de SPA.

1. Renderize o conteúdo no componente.

   As propriedades do JCR do componente de texto são exibidas da seguinte forma em AEM.

   ![Propriedades do componente de texto](assets/external-spa-text-properties.png)

   Esses valores são passados como propriedades para o componente `AEMText` React recém-criado e podem ser usados para renderizar o conteúdo.

   ```javascript
   import React from 'react';
   import { withMappable } from '@adobe/aem-react-editable-components';
   
   export const TextEditConfig = {
       // Empty component placeholder label
       emptyLabel:'Text', 
       isEmpty:function(props) {
          return !props || !props.text || props.text.trim().length < 1;
       },
       // resourcetype of the AEM counterpart component
       resourceType:'wknd-spa-react/components/text'
   };
   
   const Text = ({ text }) => (<div>{text}</div>);
   
   export default Text;
   
   export const AEMText = withMappable(Text, TextEditConfig);
   ```

   É assim que o componente aparecerá quando as configurações AEM estiverem completas.

   ```javascript
   const Text = ({ cqPath, richText, text }) => {
      const richTextContent = () => (
         <div className="aem_text" id={cqPath.substr(cqPath.lastIndexOf('/') + 1)} data-rte-editelement dangerouslySetInnerHTML={{__html: text}}/>
      );
      return richText ? richTextContent() : (<div className="aem_text">{text}</div>);
   };
   ```

   >[!NOTE]
   >
   >Neste exemplo, fizemos outras personalizações no componente renderizado para corresponder ao componente de texto existente. No entanto, isso não está relacionado à criação em AEM.

#### Adicionar componentes autoráveis à página {#add-authorable-component-to-page}

Depois que os componentes autoráveis React forem criados, nós poderemos usá-los em todo o aplicativo.

Vamos pegar uma página de exemplo onde precisamos adicionar um texto do projeto SPA WKND. Neste exemplo, queremos exibir o texto &quot;Hello World!&quot; em `/content/wknd-spa-react/us/en/home.html`.

1. Determine o caminho do nó a ser exibido.

   * `pagePath`: A página que contém o nó, em nosso exemplo  `/content/wknd-spa-react/us/en/home`
   * `itemPath`: Caminho para o nó na página, em nosso exemplo  `root/responsivegrid/text`
      * Isso consiste nos nomes dos itens que contêm na página.

   ![Caminho do nó](assets/external-spa-path.png)

1. Adicione o componente na posição desejada na página.

   ![Adicionar componente à página](assets/external-spa-add-component.png)

   O componente `AEMText` pode ser adicionado na posição desejada dentro da página com valores `pagePath` e `itemPath` definidos como propriedades. `pagePath` é uma propriedade obrigatória.

#### Verifique a edição do conteúdo de texto em AEM {#verify-text-edit}

Agora podemos testar o componente em nossa instância AEM em execução.

1. Execute o seguinte comando Maven do diretório `aem-guides-wknd-spa` para criar e implantar o projeto no AEM.

```shell
mvn clean install -PautoInstallSinglePackage
```

1. Em sua instância AEM, navegue até `http://<host>:<port>/editor.html/content/wknd-spa-react/us/en/home.html`.

![Edição do SPA em AEM](assets/external-spa-edit-aem.png)

O componente `AEMText` agora é autorável em AEM.

### AEM páginas autoráveis {#aem-authorable-pages}

1. Identifique uma página a ser adicionada para criação no SPA. Este exemplo usa `/content/wknd-spa-react/us/en/home.html`.
1. Criar um novo arquivo (por exemplo, `Page.js`) para o Componente de página criável. Aqui, podemos reutilizar o Componente de página fornecido em `@adobe/cq-react-editable-components`.
1. Repita a etapa quatro na seção [AEM componentes de folha autoráveis.](#authorable-leaf-components) Use a função de invólucro  `withMappable` no componente.
1. Como foi feito anteriormente, aplique `MapTo` aos tipos de recurso AEM para todos os componentes filho dentro da página.

   ```javascript
   import { Page, MapTo, withMappable } from '@adobe/aem-react-editable-components';
   import Text, { TextEditConfig } from './Text';
   
   export default withMappable(Page);
   
   MapTo('wknd-spa-react/components/text')(Text, TextEditConfig);
   ```

   >[!NOTE]
   >
   >Neste exemplo, estamos usando o componente de texto Reagir sem quebra de linha em vez do `AEMText` encapsulado criado anteriormente. Isso ocorre porque quando o componente faz parte de uma página/container e não está sozinho, o container cuidará do mapeamento recursivo do componente e da ativação dos recursos de criação, e o invólucro adicional não é necessário para cada filho.

1. Para adicionar uma página criável no SPA, siga as mesmas etapas na seção [Adicionar componentes autoráveis à página.](#add-authorable-component-to-page) Aqui podemos ignorar a  `itemPath` propriedade.

#### Verificar o conteúdo da página em AEM {#verify-page-content}

Para verificar se a página pode ser editada, siga as mesmas etapas na seção [Verificar a edição do conteúdo de texto no AEM.](#verify-text-edit)

![Editar uma página no AEM](assets/external-spa-edit-page.png)

A página agora é editável em AEM com um container de layout e um Componente de texto filho.

### Componentes de folha virtual {#virtual-leaf-components}

Nos exemplos anteriores, adicionamos componentes ao SPA com conteúdo AEM existente. No entanto, há casos em que o conteúdo ainda não foi criado no AEM, mas precisa ser adicionado posteriormente pelo autor do conteúdo. Para acomodar isso, o desenvolvedor front-end pode adicionar componentes nos locais apropriados no SPA. Esses componentes exibirão espaços reservados quando abertos no editor no AEM. Depois que o conteúdo é adicionado nesses espaços reservados pelo autor do conteúdo, os nós são criados na estrutura do JCR e o conteúdo é mantido. O componente criado permitirá o mesmo conjunto de operações que os componentes folha independentes.

Neste exemplo, estamos reutilizando o componente `AEMText` criado anteriormente. Queremos que o novo texto seja adicionado abaixo do componente de texto existente no home page WKND. A adição de componentes é idêntica à dos componentes folhosos normais. Entretanto, `itemPath` pode ser atualizado para o caminho onde o novo componente precisa ser adicionado.

Como o novo componente precisa ser adicionado abaixo do texto existente em `root/responsivegrid/text`, o novo caminho seria `root/responsivegrid/{itemName}`.

```html
<AEMText
 pagePath='/content/wknd-spa-react/us/en/home'
 itemPath='root/responsivegrid/text_20' />
```

O componente `TestPage` é semelhante ao seguinte após a adição do componente virtual.

![Teste do componente virtual](assets/external-spa-virtual-component.png)

>[!NOTE]
>
>Verifique se o componente `AEMText` tem `resourceType` definido na configuração para ativar esse recurso.

Agora é possível implantar as alterações em AEM seguindo as etapas na seção [Verificar a edição do conteúdo de texto no AEM.](#verify-text-edit) Um espaço reservado será exibido para o  `text_20` nó não existente no momento.

![O nó text_20 no aem](assets/external-spa-text20-aem.png)

Quando o autor do conteúdo atualiza esse componente, um novo nó `text_20` é criado em `root/responsivegrid/text_20` em `/content/wknd-spa-react/us/en/home`.

![O nó text20](assets/external-spa-text20-node.png)

#### Requisitos e limitações {#limitations}

Há vários requisitos para adicionar componentes de folha virtuais, bem como algumas limitações.

* A propriedade `pagePath` é obrigatória para a criação de um componente virtual.
* O nó de página fornecido no caminho em `pagePath` deve existir no projeto AEM.
* O nome do nó a ser criado deve ser fornecido em `itemPath`.
* O componente pode ser criado em qualquer nível.
   * Se fornecermos um `itemPath='text_20'` no exemplo anterior, o novo nó será criado diretamente sob a página, ou seja, `/content/wknd-spa-react/us/en/home/jcr:content/text_20`
* O caminho para o nó onde um novo nó é criado deve ser válido quando fornecido via `itemPath`.
   * Neste exemplo, `root/responsivegrid` deve existir para que o novo nó `text_20` possa ser criado lá.
* Somente a criação do componente folha é suportada. O container virtual e a página serão suportados em versões futuras.

## Personalizações adicionais {#additional-customizations}

Se você seguiu os exemplos anteriores, seu SPA externo agora pode ser editado dentro do AEM. Entretanto, há aspectos adicionais de seu SPA externo que você pode personalizar ainda mais.

### ID do nó raiz {#root-node-id}

Por padrão, assumimos que o aplicativo React é renderizado dentro de `div` da ID do elemento `spa-root`. Se necessário, isso pode ser personalizado.

Por exemplo, suponha que temos um SPA no qual o aplicativo é renderizado dentro de `div` da ID do elemento `root`. Isso precisa ser refletido em três arquivos.

1. Em `index.js` do aplicativo React (ou onde `ReactDOM.render()` é chamado)

   ![ReactDOM.render() no arquivo index.js](assets/external-spa-root-index.png)

1. Em `index.html` do aplicativo React

   ![O index.html do aplicativo](assets/external-spa-index.png)

1. No corpo do componente de página do aplicativo AEM por meio de duas etapas:

   1. Crie um novo `body.html` para o componente de página.

   ![Criar um novo arquivo body.html](assets/external-spa-update-body.gif)

   1. Adicione o novo elemento raiz no novo arquivo `body.html`.

   ![Adicione o elemento raiz ao body.html](assets/external-spa-add-root.png)

### Edição de um SPA React com Roteamento {#editing-react-spa-with-routing}

Se o aplicativo React externo SPA tiver várias páginas, [ele poderá usar o roteamento para determinar a página/componente a ser renderizado.](/help/implementing/developing/hybrid/routing.md) O caso básico de uso é corresponder ao URL ativo no momento ao caminho fornecido para uma rota. Para habilitar a edição nesses aplicativos habilitados para roteamentos, o caminho a ser comparado precisa ser transformado para acomodar informações específicas para AEM.

No exemplo a seguir, temos um aplicativo React simples com duas páginas. A página a ser renderizada é determinada pela correspondência do caminho fornecido ao roteador com o URL ativo. Por exemplo, se estivermos em `mydomain.com/test`, `TestPage` será renderizado.

![Roteamento em um SPA externo](assets/external-spa-routing.png)

Para habilitar a edição no AEM para este SPA de exemplo, as etapas a seguir são obrigatórias.

1. Identifique o nível que atuaria como a raiz no AEM.

   * Para nossa amostra, estamos considerando wknd-spa-response/us/en como a raiz do SPA. Isso significa que tudo que antecede esse caminho é AEM somente páginas/conteúdo.

1. Crie uma nova página no nível necessário.

   * Neste exemplo, a página a ser editada é `mydomain.com/test`. `test` está no caminho raiz do aplicativo. Isso também precisa ser preservado ao criar a página no AEM. Portanto, podemos criar uma nova página no nível raiz definido na etapa anterior.
   * A nova página criada deve ter o mesmo nome da página a ser editada. Neste exemplo para `mydomain.com/test`, a nova página criada deve ser `/path/to/aem/root/test`.

1. Adicione ajuda dentro SPA roteamento.

   * A página recém-criada ainda não renderizará o conteúdo esperado em AEM. Isso ocorre porque o roteador espera um caminho de `/test`, enquanto o caminho ativo AEM é `/wknd-spa-react/us/en/test`. Para acomodar a parte específica do URL AEM, precisamos adicionar alguns auxiliares do lado SPA.

   ![Roteamento auxiliar](assets/external-spa-router-helper.png)

   * O auxiliar `toAEMPath` fornecido por `@adobe/cq-spa-page-model-manager` pode ser usado para isso. Ele transforma o caminho fornecido para o roteamento para incluir partes específicas do AEM quando o aplicativo está aberto em uma instância AEM. Ele aceita três parâmetros:
      * O caminho necessário para o roteamento
      * O URL de origem da instância de AEM onde o SPA é editado
      * A raiz do projeto no AEM, conforme determinado na primeira etapa
   * Esses valores podem ser definidos como variáveis de ambiente para maior flexibilidade.



1. Verifique a edição da página no AEM.

   * Implante o projeto para AEM e navegue até a página `test` recém-criada. O conteúdo da página agora é renderizado e AEM componentes são editáveis.

## Recursos adicionais {#additional-resources}

O seguinte material de referência pode ser útil para compreender SPA no contexto da AEM.

* [Cabeça e Sem Cabeça em AEM](/help/implementing/developing/headful-headless.md)
* [O Arquivo do Projeto AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)
* [O projeto SPA WKND](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/spa-editor/spa-editor-framework-feature-video-use.html)
* [Introdução ao SPA no AEM usando React](/help/implementing/developing/hybrid/getting-started-react.md)
* [Materiais de referência SPA (referências de API)](/help/implementing/developing/hybrid/reference-materials.md)
* [SPA Blueprint e PageModelManager](/help/implementing/developing/hybrid/blueprint.md#pagemodelmanager)
* [roteamento Modelo SPA](/help/implementing/developing/hybrid/routing.md)
* [Renderização do servidor e do SPA](/help/implementing/developing/hybrid/ssr.md)
