---
title: Edição de um SPA externo no AEM
description: Este documento descreve as etapas recomendadas para fazer upload de um SPA independente em uma instância do AEM, adicionar seções editáveis de conteúdo e ativar a criação.
exl-id: 7978208d-4a6e-4b3a-9f51-56d159ead385
feature: Developing
role: Admin, Developer
index: false
source-git-commit: 81f85045212ca6fd92f2b665aeceaa0d4b92318c
workflow-type: tm+mt
source-wordcount: '2370'
ht-degree: 1%

---


# Edição de um SPA externo no AEM {#editing-external-spa-within-aem}

Ao decidir [que nível de integração](/help/implementing/developing/headful-headless.md) você gostaria de ter entre seu SPA externo e o AEM, considere que você deve ser capaz de editar e visualizar o SPA no AEM, com frequência.

{{ue-over-spa}}

## Visão geral {#overview}

Este documento descreve as etapas recomendadas para fazer upload de um SPA independente em uma instância do AEM, adicionar seções editáveis de conteúdo e ativar a criação.

## Pré-requisitos {#prerequisites}

Os pré-requisitos são simples.

* Verifique se uma instância do AEM está sendo executada localmente.
* Crie um projeto básico de SPA do AEM usando o [Arquétipo de Projetos AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?#available-properties).
   * O Forms é a base do projeto do AEM, que é atualizado para incluir o SPA externo.
   * Para as amostras neste documento, o Adobe está usando o ponto de partida do [projeto WKND SPA](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/spa-editor/spa-editor-framework-feature-video-use.html#spa-editor).
* Tenha em mãos o SPA externo React funcional que deseja integrar.

## Fazer upload de SPA para projeto do AEM {#upload-spa-to-aem-project}

Primeiro, carregue o SPA externo no seu projeto do AEM.

1. Substitua `src` na pasta do projeto `/ui.frontend` pela pasta `src` do aplicativo React.
1. Inclua qualquer dependência adicional no `package.json` do aplicativo no arquivo `/ui.frontend/package.json`.
   * Verifique se as dependências do SPA SDK são de [versões recomendadas](/help/implementing/developing/hybrid/getting-started-react.md#dependencies).
1. Incluir qualquer personalização na pasta `/public`.
1. Inclua qualquer script ou estilo incorporado adicionado ao arquivo `/public/index.html`.

## Configurar o SPA remoto {#configure-remote-spa}

Agora que o SPA externo faz parte do projeto do AEM, ele deve ser configurado no AEM.

### Incluir pacotes Adobe SPA SDK {#include-spa-sdk-packages}

Para aproveitar os recursos de SPA do AEM, há dependências nos três pacotes a seguir.

* [`@adobe/aem-react-editable-components`](https://github.com/adobe/aem-react-editable-components)
* [`@adobe/aem-spa-component-mapping`](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping)
* [`@adobe/aem-spa-page-model-manager`](https://www.npmjs.com/login?next=/package/@adobe/aem-spa-model-manager)

O pacote `@adobe/aem-spa-page-model-manager` fornece a API para inicializar um Gerenciador de Modelos e recuperar o modelo da instância do AEM. Esse modelo pode ser usado para renderizar componentes AEM usando APIs de `@adobe/aem-react-editable-components` e `@adobe/aem-spa-component-mapping`.

#### Instalação {#installation}

Execute o seguinte comando `npm` para poder instalar os pacotes necessários.

```shell
npm install --save @adobe/aem-spa-component-mapping @adobe/aem-spa-page-model-manager @adobe/aem-react-editable-components
```

### Inicialização do ModelManager {#model-manager-initialization}

Antes que o aplicativo seja renderizado, o [`ModelManager`](/help/implementing/developing/hybrid/blueprint.md#pagemodelmanager) deve ser inicializado para lidar com a criação do AEM `ModelStore`.

Essa inicialização deve ser feita dentro do arquivo `src/index.js` do seu aplicativo ou onde quer que a raiz do aplicativo seja renderizada.

Para fazer essa inicialização, você pode usar a API `initializationAsync` fornecida pelo `ModelManager`.

A captura de tela a seguir mostra como habilitar a inicialização do `ModelManager` em um aplicativo simples do React. A única restrição é que `initializationAsync` deve ser chamado antes de `ReactDOM.render()`.

![Inicializar ModelManager](assets/external-spa-initialize-modelmanager.png)

Neste exemplo, o `ModelManager` é inicializado e um `ModelStore` vazio é criado.

O `initializationAsync` pode, opcionalmente, aceitar um objeto `options` como parâmetro:

* `path` - Na inicialização, o modelo no caminho definido é buscado e armazenado em `ModelStore`. Este caminho pode ser usado para buscar o `rootModel` na inicialização, se necessário.
* `modelClient` - Permite fornecer um cliente personalizado responsável por buscar o modelo.
* `model` - Um objeto `model` passado como parâmetro normalmente preenchido ao usar SSR.

### Componentes de folha possíveis do AEM {#authorable-leaf-components}

1. Criar/identificar um componente do AEM para o qual um componente do React autorável é criado. Neste exemplo, ele está usando o componente de texto do projeto WKND.

   ![Componente de texto WKND](assets/external-spa-text-component.png)

1. Crie um componente de texto simples do React no SPA. Neste exemplo, um novo arquivo `Text.js` foi criado com o conteúdo a seguir.

   ![Text.js](assets/external-spa-textjs.png)

1. Crie um objeto de configuração para especificar os atributos necessários para habilitar a edição no AEM.

   ![Criar objeto de configuração](assets/external-spa-config-object.png)

   * `resourceType` é obrigatório mapear o componente React ao componente AEM e habilitar a edição ao abri-lo no Editor do AEM.

1. Use a função wrapper `withMappable`.

   ![Usar com Mapeável](assets/external-spa-withmappable.png)

   Esta função de wrapper mapeia o componente React para o AEM `resourceType` especificado na configuração e habilita recursos de edição quando aberto no Editor do AEM. Para componentes independentes, ela também busca o conteúdo do modelo para o nó específico.

   >[!NOTE]
   >
   >Neste exemplo, há versões separadas do componente: componentes React encapsulados e desencapsulados do AEM. A versão encapsulada deve ser usada ao usar explicitamente o componente. Quando o componente é parte de uma página, você pode continuar usando o componente padrão, como atualmente feito no editor de SPA.

1. Renderizar conteúdo no componente.

   As propriedades JCR do componente de texto aparecem da seguinte maneira no AEM.

   ![Propriedades do componente de texto](assets/external-spa-text-properties.png)

   Esses valores são passados como propriedades para o componente React `AEMText` criado e podem ser usados para renderizar o conteúdo.

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

   Veja a seguir como o componente aparece quando as configurações do AEM são concluídas.

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
   >Neste exemplo, mais personalizações foram feitas no componente renderizado para corresponder ao componente de texto existente. Não está relacionado à criação no AEM.

#### Adicionar componentes autoráveis à página {#add-authorable-component-to-page}

Depois que os componentes autoráveis do React forem criados, você poderá usá-los em todo o aplicativo.

Vejamos um exemplo de página em que você deve adicionar um texto do projeto WKND SPA. Neste exemplo, você deseja exibir o texto &quot;Olá, mundo!&quot; em `/content/wknd-spa-react/us/en/home.html`.

1. Determine o caminho do nó a ser exibido.

   * `pagePath`: a página que contém o nó, neste exemplo `/content/wknd-spa-react/us/en/home`
   * `itemPath`: Caminho para o nó dentro da página, neste exemplo `root/responsivegrid/text`
      * Consiste nos nomes dos itens que contêm itens na página.

   ![Caminho do nó](assets/external-spa-path.png)

1. Adicionar componente na posição desejada na página.

   ![Adicionar componente à página](assets/external-spa-add-component.png)

   O componente `AEMText` pode ser adicionado na posição necessária na página com valores `pagePath` e `itemPath` definidos como propriedades. `pagePath` é uma propriedade obrigatória.

#### Verificar edição de conteúdo de texto no AEM {#verify-text-edit}

Agora teste o componente na instância do AEM em execução.

1. Execute o seguinte comando Maven no diretório `aem-guides-wknd-spa` para poder compilar e implantar o projeto no AEM.

```shell
mvn clean install -PautoInstallSinglePackage
```

1. Na sua instância do AEM, navegue até `http://<host>:<port>/editor.html/content/wknd-spa-react/us/en/home.html`.

![Editando o SPA no AEM](assets/external-spa-edit-aem.png)

O componente `AEMText` agora pode ser criado no AEM.

### Páginas possíveis do AEM {#aem-authorable-pages}

1. Identifique uma página a ser adicionada para criação no SPA. Este exemplo usa `/content/wknd-spa-react/us/en/home.html`.
1. Crie um arquivo (por exemplo, `Page.js`) para o componente de Página que pode ser criado. use o Componente de Página fornecido em `@adobe/cq-react-editable-components`.
1. Repita a etapa quatro na seção [componentes de folha autoráveis do AEM](#authorable-leaf-components). Use a função wrapper `withMappable` no componente.
1. Como foi feito anteriormente, aplique `MapTo` aos tipos de recursos do AEM para todos os componentes filhos na página.

   ```javascript
   import { Page, MapTo, withMappable } from '@adobe/aem-react-editable-components';
   import Text, { TextEditConfig } from './Text';
   
   export default withMappable(Page);
   
   MapTo('wknd-spa-react/components/text')(Text, TextEditConfig);
   ```

   >[!NOTE]
   >
   >Neste exemplo, o componente de texto React não encapsulado é usado em vez do `AEMText` encapsulado criado anteriormente. O motivo é que, quando o componente faz parte de uma página/contêiner e não é independente, o contêiner cuida do mapeamento recursivo do componente. E ativar os recursos de criação e o invólucro adicional não é necessário para cada criança.

1. Para adicionar uma página para criação no SPA, siga as mesmas etapas na seção [Adicionar componentes para criação à página](#add-authorable-component-to-page). Aqui, você pode ignorar a propriedade `itemPath`.

#### Verificar conteúdo da página no AEM {#verify-page-content}

Para verificar se a página pode ser editada, siga as mesmas etapas na seção [Verificar Edição de Conteúdo de Texto no AEM](#verify-text-edit).

![Editando uma página no AEM](assets/external-spa-edit-page.png)

A página agora pode ser editada no AEM com um contêiner de layout e um componente de Texto filho.

### Componentes da folha virtual {#virtual-leaf-components}

Nos exemplos anteriores, você adicionou componentes ao SPA com conteúdo existente do AEM. No entanto, há casos em que o conteúdo ainda não foi criado no AEM, mas deve ser adicionado posteriormente pelo autor de conteúdo. Para acomodar esse cenário, o desenvolvedor de front-end pode adicionar componentes nos locais apropriados no SPA. Esses componentes exibem espaços reservados quando abertos no editor no AEM. Depois que o conteúdo é adicionado nesses espaços reservados pelo autor de conteúdo, os nós são criados na estrutura JCR e o conteúdo é mantido. O componente criado permite o mesmo conjunto de operações que os componentes folha independentes.

Neste exemplo, você está reutilizando o componente `AEMText` criado anteriormente. Você deseja que um novo texto seja adicionado abaixo do componente de texto existente na página inicial da WKND. A adição de componentes é a mesma para componentes de folha normais. No entanto, o `itemPath` pode ser atualizado para o caminho em que o novo componente deve ser adicionado.

Como o novo componente deve ser adicionado abaixo do texto existente em `root/responsivegrid/text`, o novo caminho é `root/responsivegrid/{itemName}`.

```html
<AEMText
 pagePath='/content/wknd-spa-react/us/en/home'
 itemPath='root/responsivegrid/text_20' />
```

O componente `TestPage` tem a seguinte aparência depois de adicionar o componente virtual.

![Testando o componente virtual](assets/external-spa-virtual-component.png)

>[!NOTE]
>
>Verifique se o componente `AEMText` tem seu `resourceType` definido na configuração para que você possa habilitar esse recurso.

Agora você pode implantar as alterações no AEM seguindo as etapas da seção [Verificar Edição de Conteúdo de Texto no AEM](#verify-text-edit). Um espaço reservado é exibido para o nó `text_20` não existente no momento.

![O nó text_20 no aem](assets/external-spa-text20-aem.png)

Quando o autor de conteúdo atualiza esse componente, um novo nó `text_20` é criado em `root/responsivegrid/text_20` em `/content/wknd-spa-react/us/en/home`.

![O nó text20](assets/external-spa-text20-node.png)

#### Requisitos e limitações {#limitations}

Há vários requisitos para adicionar componentes de folha virtual e algumas limitações.

* A propriedade `pagePath` é obrigatória para criar um componente virtual.
* O nó da página fornecido no caminho em `pagePath` deve existir no projeto AEM.
* O nome do nó a ser criado deve ser fornecido em `itemPath`.
* O componente pode ser criado em qualquer nível.
   * Se você fornecer um `itemPath='text_20'` no exemplo anterior, o novo nó será criado diretamente na página, ou seja, `/content/wknd-spa-react/us/en/home/jcr:content/text_20`
* O caminho para o nó onde um novo nó é criado deve ser válido quando fornecido via `itemPath`.
   * Neste exemplo, `root/responsivegrid` deve existir para que o novo nó `text_20` possa ser criado lá.
* Somente a criação de componente folha é suportada. O container virtual e a página serão compatíveis em versões futuras.

### Contêineres virtuais {#virtual-containers}

A capacidade de adicionar contêineres, mesmo que o contêiner correspondente ainda não tenha sido criado no AEM, é compatível. O conceito e a abordagem são semelhantes a [componentes de folha virtual](#virtual-leaf-components).

O desenvolvedor de front-end pode adicionar os componentes do contêiner em locais apropriados no SPA e esses componentes exibem espaços reservados quando abertos no editor no AEM. O autor pode então adicionar componentes e seu conteúdo ao contêiner que cria os nós necessários na estrutura JCR.

Por exemplo, se um contêiner existe em `/root/responsivegrid` e o desenvolvedor deseja adicionar um contêiner filho:

![Local do contêiner](assets/container-location.png)

O `newContainer` ainda não existe no AEM.

Ao editar a página que contém esse componente no AEM, um espaço reservado vazio para um contêiner é exibido no qual o autor pode adicionar conteúdo.

![Espaço reservado para contêiner](assets/container-placeholder.png)

![Local do contêiner no JCR](assets/container-jcr-structure.png)

Depois que o autor adiciona um componente secundário ao contêiner, o novo nó do contêiner é criado com o nome correspondente na estrutura JCR.

![Contêiner com conteúdo](assets/container-with-content.png)

![Contêiner com conteúdo no JCR](assets/container-with-content-jcr.png)

Mais componentes e conteúdo podem ser adicionados ao contêiner agora, conforme exigido pelo autor, e as alterações são persistentes.

#### Requisitos e limitações {#container-limitations}

Há vários requisitos para adicionar contêineres virtuais e algumas limitações.

* A política para determinar quais componentes podem ser adicionados é herdada do container principal.
* O pai imediato do container a ser criado deve existir no AEM.
   * Se o contêiner `root/responsivegrid` existir no contêiner AEM, um novo contêiner poderá ser criado fornecendo o caminho `root/responsivegrid/newContainer`.
   * No entanto, `root/responsivegrid/newContainer/secondNewContainer` não é possível.
* Somente um novo nível de componente pode ser criado de cada vez.

## Personalizações adicionais {#additional-customizations}

Se você seguiu os exemplos anteriores, seu SPA externo agora é editável no AEM. No entanto, há aspectos adicionais do SPA externo que você pode personalizar ainda mais.

### ID do nó raiz {#root-node-id}

Por padrão, você pode supor que o aplicativo React é renderizado dentro de um `div` de ID de elemento `spa-root`. Se necessário, essa sintaxe pode ser personalizada.

Por exemplo, suponha que você tenha um SPA no qual o aplicativo é renderizado dentro de um `div` de ID de elemento `root`. Essa sintaxe deve ser refletida nos três arquivos.

1. No `index.js` do aplicativo React (ou onde `ReactDOM.render()` é chamado)

   ![ReactDOM.render() no arquivo index.js](assets/external-spa-root-index.png)

1. No `index.html` do aplicativo React

   ![O index.html do aplicativo](assets/external-spa-index.png)

1. No corpo do componente de página do aplicativo AEM por meio de duas etapas:

   1. Crie um `body.html` para o componente de página.

   ![Criar um arquivo body.html](assets/external-spa-update-body.gif)

   1. Adicione o elemento raiz no novo arquivo `body.html`.

   ![Adicionar o elemento raiz a body.html](assets/external-spa-add-root.png)

### Edição de um SPA do React com Roteamento {#editing-react-spa-with-routing}

Se o aplicativo SPA externo do React tiver várias páginas, [ele poderá usar o roteamento para determinar a página/componente a ser renderizado](/help/implementing/developing/hybrid/routing.md). O caso de uso básico é corresponder o URL ativo no momento com o caminho fornecido para uma rota. Para habilitar a edição nesses aplicativos habilitados para roteamento, o caminho a ser correspondido deve ser transformado para acomodar as informações específicas do AEM.

No exemplo a seguir, você tem um aplicativo simples do React com duas páginas. A página a ser renderizada é determinada pela correspondência do caminho fornecido ao roteador com o URL ativo. Por exemplo, se você estiver em `mydomain.com/test`, `TestPage` é renderizado.

![Roteamento em um SPA externo](assets/external-spa-routing.png)

Para habilitar a edição no AEM para este exemplo de SPA, as seguintes etapas são necessárias.

1. Identifique o nível que atuaria como a raiz no AEM.

   * Para sua amostra, considere wknd-spa-react/us/en como a raiz do SPA. Essa raiz significa que tudo antes desse caminho é somente páginas/conteúdo do AEM.

1. Crie uma página no nível necessário.

   * Neste exemplo, a página a ser editada é `mydomain.com/test`. `test` está no caminho raiz do aplicativo. Esse caminho raiz também deve ser preservado ao criar a página no AEM. Portanto, é possível criar uma página no nível raiz definido na etapa anterior.
   * A nova página criada deve ter o mesmo nome da página a ser editada. Neste exemplo, para `mydomain.com/test`, a nova página criada deve ser `/path/to/aem/root/test`.

1. Adicione auxiliares no roteamento SPA.

   * A página criada ainda não pode renderizar o conteúdo esperado no AEM. O motivo é porque o roteador espera um caminho de `/test`, enquanto o caminho ativo do AEM é `/wknd-spa-react/us/en/test`. Para acomodar a parte específica do AEM do URL, você deve adicionar alguns auxiliares no lado do SPA.

   ![Auxiliar de roteamento](assets/external-spa-router-helper.png)

   * O auxiliar `toAEMPath` fornecido por `@adobe/cq-spa-page-model-manager` pode ser usado. Ele transforma o caminho fornecido para roteamento para incluir partes específicas do AEM quando o aplicativo estiver aberto em uma instância do AEM. Ele aceita três parâmetros:
      * O caminho necessário para roteamento
      * O URL de origem da instância do AEM onde o SPA é editado
      * A raiz do projeto no AEM, conforme determinado na primeira etapa

   * Esses valores podem ser definidos como variáveis de ambiente para obter mais flexibilidade.

1. Verifique a edição da página no AEM.

   * Implante o projeto no AEM e navegue até a página `test` criada. O conteúdo da página agora é renderizado e os componentes do AEM são editáveis.

## Limitações da estrutura {#framework-limitations}

O componente RemotePage espera que a implementação forneça um manifesto de ativo como o [webpack-manifest-plugin no GitHub](https://github.com/shellscape/webpack-manifest-plugin). No entanto, o componente RemotePage só foi testado para funcionar com a estrutura React (e o Next.js por meio do componente remote-page-next) e, portanto, não oferece suporte ao carregamento remoto de aplicativos de outras estruturas, como o Angular.

## Recursos adicionais {#additional-resources}

O material de referência a seguir pode ser útil para entender os SPAs no contexto do AEM.

* [Headful e Headless no AEM](/help/implementing/developing/headful-headless.md)
* [O Arquétipo de Projetos AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)
* [O projeto WKND SPA](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/spa-editor/spa-editor-framework-feature-video-use.html?lang=pt-BR)
* [Introdução a SPAs no AEM usando o React](/help/implementing/developing/hybrid/getting-started-react.md)
* [Materiais de referência de SPA (referências de API)](/help/implementing/developing/hybrid/reference-materials.md)
* [Blueprint do SPA e PageModelManager](/help/implementing/developing/hybrid/blueprint.md#pagemodelmanager)
* [Roteamento de modelo SPA](/help/implementing/developing/hybrid/routing.md)
