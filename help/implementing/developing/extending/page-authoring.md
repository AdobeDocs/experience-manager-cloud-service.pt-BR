---
title: Personalização da criação de página
description: Saiba mais sobre os mecanismos que o AEM as a Cloud Service oferece para personalizar a funcionalidade de criação de página.
exl-id: 98d3c7ab-46d2-4e8d-b0da-5c8a7b398135
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '969'
ht-degree: 2%

---

# Personalização da criação de página {#customizing-page-authoring}

O Adobe Experience Manager as a Cloud Service fornece mecanismos para permitir personalizar a funcionalidade de criação de página (e a [consoles](/help/implementing/developing/extending/consoles.md)) da sua instância de criação.

## Clientlibs {#clientlibs}

As clientlibs permitem estender a implementação padrão para habilitar uma nova funcionalidade, ao mesmo tempo em que reutiliza as funções, objetos e métodos padrão.

Ao personalizar, você pode criar sua própria clientlib em `/apps.` A nova clientlib deve:

* Depende da clientlib de criação `cq.authoring.editor.sites.page`.
* Faça parte do `cq.authoring.editor.sites.page.hook` categoria.

Consulte [Uso de bibliotecas do lado do cliente no AEM as a Cloud Service](/help/implementing/developing/introduction/clientlibs.md).

## Sobreposições {#overlays}

As sobreposições se baseiam nas definições de nó e permitem sobrepor a funcionalidade padrão no `/libs` com sua própria funcionalidade personalizada no `/apps`.

Ao criar uma sobreposição, não é necessária uma cópia 1:1 do original, pois a [fusão de recursos do sling](/help/implementing/developing/introduction/sling-resource-merger.md) permite a herança.

Para obter mais informações, consulte [Conjunto de documentação JS](https://developer.adobe.com/experience-manager/reference-materials/6-5/jsdoc/ui-touch/editor-core/index.html).

Para obter mais informações sobre sobreposições, consulte [Sobreposições para o Adobe Experience Manager as a Cloud Service](/help/implementing/developing/introduction/overlays.md).

## Adicionar nova camada (modo) {#add-new-layer-mode}

Quando você está editando uma página, há vários [modos](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes) disponíveis. Esses modos são implementados usando [camadas](/help/implementing/developing/introduction/ui-structure.md#layer). Eles permitem acesso a diferentes tipos de funcionalidade para o mesmo conteúdo de página. Os modos AEM padrão incluem Editar, Layout, Desenvolvedor, Timewarp, Status da Live Copy e Direcionamento.

### Exemplo de camada: status da Live Copy {#layer-example-live-copy-status}

Uma instância AEM padrão fornece a camada MSM. Isso acessa dados relacionados ao [gerenciamento multisite](/help/sites-cloud/administering/msm/overview.md) e o realça na camada.

Para vê-lo em ação, você pode editar qualquer cópia de idioma no [Conteúdo de amostra do WKND](/help/implementing/developing/introduction/develop-wknd-tutorial.md) e selecione o **Status da Live Copy** modo.

Você pode encontrar a definição da camada MSM (para referência) em:

`/libs/wcm/msm/content/touch-ui/authoring/editor/js/msm.Layer.js`

### Amostra de código {#code-sample}

Este é um exemplo de pacote que mostra como criar uma camada (modo) para exibição do MSM.

Você pode encontrar o código desta página em [GitHub.](https://github.com/Adobe-Marketing-Cloud/aem-authoring-new-layer-mode)

## Adicionar nova categoria de seleção ao navegador de ativos {#add-new-selection-category-to-asset-browser}

O navegador de ativos mostra ativos de vários tipos/categorias (por exemplo, imagens e documentos). Os ativos também podem ser filtrados por essas categorias de ativos.

### Amostra de código {#code-sample-1}

`aem-authoring-extension-assetfinder-flickr` é um exemplo de pacote que mostra como adicionar um grupo ao localizador de ativos. Este exemplo se conecta a [Flickr](https://www.flickr.com)fluxo público do e os mostra no painel lateral.

Você pode encontrar o código desta página em [GitHub.](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-assetfinder-flickr)

## Filtrar recursos {#filtering-resources}

Ao criar páginas, o usuário geralmente deve selecionar entre os recursos em uma lista.

Para manter a lista em um tamanho razoável e também relevante para o caso de uso, um filtro pode ser implementado no formato de um predicado personalizado. Por exemplo, se a variável `pathbrowser` O componente Granite é usado para permitir que o usuário selecione o caminho para um recurso específico. Os caminhos apresentados podem ser filtrados da seguinte maneira:

* Implementar o predicado personalizado implementando o [`com.day.cq.commons.predicate.AbstractNodePredicate`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/commons/predicate/package-summary.html) interface.
* Especifique um nome para o predicado e consulte esse nome ao usar o `pathbrowser`.

Para obter mais detalhes sobre como criar um predicado personalizado, consulte [neste artigo.](/help/implementing/developing/introduction/query-builder-custom-predicate.md)

## Adicionar nova ação a uma barra de ferramentas do componente {#add-new-action-to-a-component-toolbar}

Cada componente geralmente tem uma barra de ferramentas que fornece acesso a uma variedade de ações que podem ser executadas nesse componente.

### Amostra de código {#code-sample-2}

`aem-authoring-extension-toolbar-screenshot` é um pacote de amostra que mostra como criar uma ação personalizada da barra de ferramentas para renderizar componentes.

Você pode encontrar o código desta página em [GitHub.](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-toolbar-screenshot)

## Adicionar novo editor no local {#add-new-in-place-editor}

### Editor padrão no local {#standard-in-place-editor}

Em uma instalação padrão do AEM:

1. `/libs/cq/gui/components/authoring/editors/clientlibs/core/js/editors/editorExample.js` mantém as definições dos vários editores disponíveis.

1. Há uma conexão entre o editor e cada tipo de recurso (como no componente ) que pode usá-lo:

   * `cq:inplaceEditing`

     por exemplo:

      * `/libs/foundation/components/text/cq:editConfig`
      * `/libs/foundation/components/image/cq:editConfig`

         * propriedade: `editorType`

           Define o tipo de editor em linha usado quando a edição no local é acionada para esse componente; por exemplo, `text`, `textimage`, `image`, `title`.

1. Detalhes adicionais de configuração do editor podem ser configurados usando um `config` nó contendo configurações e um `plugin` para conter os detalhes de configuração do plug-in necessários.


Veja a seguir um exemplo de definição de proporções de aspecto para o plug-in de recorte de imagem do componente de imagem.

```xml
   <cq:inplaceEditing
           jcr:primaryType="cq:InplaceEditingConfig"
           active="{Boolean}true"
           editorType="image">
           <config jcr:primaryType="nt:unstructured">
               <plugins jcr:primaryType="nt:unstructured">
                   <crop jcr:primaryType="nt:unstructured">
                       <aspectRatios jcr:primaryType="nt:unstructured">
                           <_x0031_6-10
                               jcr:primaryType="nt:unstructured"
                               name="16 : 10"
                               ratio="0.625"/>
                       </aspectRatios>
                   </crop>
               </plugins>
           </config>
   </cq:inplaceEditing>
```

>[!NOTE]
>
>Rácio de colheita de AEM, tal como estabelecido pelo `ratio` são definidos como **altura/largura**. Isso difere da definição convencional de largura/altura e é feita por motivos de compatibilidade legal. Os usuários de criação não estarão cientes de qualquer diferença desde que você defina o `name` é exibida claramente, pois é o que é exibido na interface do usuário.

#### Criação de um novo editor no local {#creating-a-new-in-place-editor}

Para implementar um novo editor no local (na clientlib):

1. Implementar:

   * `setUp`
   * `tearDown`

1. Registre o editor (inclui o construtor):

   * `editor.register`

1. Forneça a conexão entre o editor e cada tipo de recurso (como no componente) que pode usá-lo.

#### Amostra de código para criar um novo editor no local {#code-sample-for-creating-a-new-in-place-editor}

`aem-authoring-extension-inplace-editor` é um pacote de amostra que mostra como criar um editor no local no AEM.

Você pode encontrar o código desta página em [GitHub.](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-inplace-editor)

## Adicionar uma nova ação de página {#add-a-new-page-action}

Para adicionar uma nova ação de página à barra de ferramentas da página, por exemplo, uma **Voltar ao Sites** (console) ação.

### Amostra de código {#code-sample-3}

`aem-authoring-extension-header-backtosites` é um pacote de amostra que mostra como criar uma ação de barra de cabeçalho personalizada para voltar ao console Sites.

Você pode encontrar o código desta página em [GitHub.](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-header-backtosites)

## Personalizar a solicitação para o fluxo de trabalho de ativação {#customizing-the-request-for-activation-workflow}

O workflow predefinido, **Solicitação para ativação**:

* Será exibido automaticamente no menu apropriado quando um autor de conteúdo **não tem** os direitos de replicação apropriados, mas **tem** associação de usuários e autores do DAM.

* Caso contrário, nada será exibido, pois os direitos de replicação foram removidos.

Para personalizar o comportamento nessa ativação, é possível sobrepor o **Solicitação para ativação** workflow:

1. Entrada `/apps` sobrepor o **Sites** assistente `/libs/wcm/core/content/common/managepublicationwizard`

   * Isso mesmo substitui a instância comum de `/libs/cq/gui/content/common/managepublicationwizard`.

1. Atualize o modelo de workflow e as configurações/scripts relacionados, conforme necessário.
1. Remova a direita para a `replicate` ação de todos os usuários apropriados para todas as páginas relevantes. Para acionar esse fluxo de trabalho como uma ação padrão quando qualquer um dos usuários tentar publicar (ou replicar) uma página.
