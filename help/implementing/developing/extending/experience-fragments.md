---
title: Fragmentos de experiência
description: Extend Adobe Experience Manager as a Cloud Service Experience Fragments.
translation-type: tm+mt
source-git-commit: 625e56efdab2f41026988fb90b72c31ff876db57
workflow-type: tm+mt
source-wordcount: '1660'
ht-degree: 2%

---


# Fragmentos de experiência{#experience-fragments}

## Noções básicas {#the-basics}

Um [Fragmento de experiência](/help/sites-cloud/authoring/fundamentals/experience-fragments.md) é um grupo de um ou mais componentes, incluindo o conteúdo e o layout que podem ser referenciados nas páginas.

An Experience Fragment Master and/or Variant uses:

* `sling:resourceType` : `/libs/cq/experience-fragments/components/xfpage`

Como não há `/libs/cq/experience-fragments/components/xfpage/xfpage.html` ele volta para

* `sling:resourceSuperType` : `wcm/foundation/components/page`

## A representação HTML simples {#the-plain-html-rendition}

Using the `.plain.` selector in the URL, you can access the plain HTML rendition.

Isso está disponível no navegador, mas seu objetivo principal é permitir que outros aplicativos (por exemplo, aplicativos da Web de terceiros, implementações móveis personalizadas) acessem o conteúdo do Fragmento de experiência diretamente, usando apenas o URL.

A execução HTML simples adiciona o protocolo, o host e o caminho de contexto aos caminhos que são:

* do tipo: `src`, `href`ou `action`

* or end with: `-src`, or `-href`

Por exemplo:

`.../brooklyn-coat/master.plain.html`

>[!NOTE]
>
>Os links sempre fazem referência à instância de publicação. Eles devem ser consumidos por terceiros, de modo que o link sempre será chamado da instância de publicação, não do autor.

![Execução HTML simples](assets/xf-14.png)

O seletor de representação simples usa um transformador em vez de scripts adicionais; o [Sling Rewriter](https://sling.apache.org/documentation/bundles/output-rewriting-pipelines-org-apache-sling-rewriter.html) é usado como o transformador. This is configured at

* `/libs/experience-fragments/config/rewriter/experiencefragments`

## Variações sociais {#social-variations}

Social variants can be posted on social media (text and image). In AEM these social variants can contain components; for example, text components, image components.

The image and text for the social post can be taken from any image resource type or text resource type at any level of depth (in either the building block or layout container).

Social variations also allow building blocks and take them into consideration when making social actions (on the publish environment).

To post the correct text and image to the social media network, some conventions need to be respected if you are developing your own customized components.

For this, the following properties must be used:

* For extracting the image

   * `fileReference`
   * `fileName`

* For extracting the text

   * `text`

Components that do not use this convention, will not be taken into consideration.

## Modelos para fragmentos de experiência {#templates-for-experience-fragments}

>[!CAUTION]
>
>***Only*** editable templates are supported for Experience Fragments.

<!-- >***Only*** [editable templates](/help/sites-developing/page-templates-editable.md) are supported for Experience Fragments.
-->

Ao desenvolver um novo modelo para Fragmentos de experiência, você pode seguir as práticas padrão de um modelo editável.

<!-- When developing a new template for Experience Fragments you can follow follow the standard practices for an [editable template](/help/sites-developing/page-templates-editable.md).
-->

Para criar um modelo de fragmento de experiência detectado pelo assistente **Criar fragmento** de experiência, siga um destes conjuntos de regras:

1. Ambos:

   1. O tipo de recurso do modelo (o nó inicial) deve herdar de:
      `cq/experience-fragments/components/xfpage`

   1. E o nome do modelo deve começar com:
      `experience-fragments`
Isso permite que os usuários criem fragmentos de experiência em /content/experience-fragments, já que a `cq:allowedTemplates` propriedade dessa pasta inclui todos os modelos que têm nomes começando com `experience-fragment`. Os clientes podem atualizar essa propriedade para incluir seus próprios esquemas de nomeação ou locais de modelo.

1. [Os modelos](/help/sites-cloud/authoring/fundamentals/experience-fragments.md#configure-allowed-templates-folder) permitidos podem ser configurados no console Fragmentos de experiência.

<!--
1. Add the template details manually in `cq:allowedTemplates` on the `/content/experience-fragment` node.
-->

<!-- >[!NOTE]
>
>[Allowed templates](/help/sites-authoring/experience-fragments.md#configuring-allowed-templates) can be configured in the Experience Fragments console.
-->

## Componentes para fragmentos de experiência {#components-for-experience-fragments}

O desenvolvimento de componentes para uso com/em Fragmentos de experiência segue as práticas padrão.

A única configuração adicional é garantir que os componentes sejam permitidos no modelo, isso é feito com a Política de conteúdo.

<!--
[Developing components](/help/sites-developing/components.md) for use with/in Experience Fragments follow standard practices.

The only additional configuration is to ensure that the components are [allowed on the template, this is achieved with the Content Policy](/help/sites-developing/page-templates-editable.md#content-policies).
-->

## O provedor de regravação do link do fragmento de experiência - HTML {#the-experience-fragment-link-rewriter-provider-html}

No AEM, você tem a possibilidade de criar Fragmentos de experiência. Um fragmento de experiência:

* consista num grupo de componentes e num esquema,
* can exist independently of an AEM page.

Um dos casos de uso desses grupos é para a incorporação de conteúdo em pontos de contato de terceiros, como o Público alvo da Adobe.

### Default Link Rewriting {#default-link-rewriting}

<!--Using the [Export to Target](/help/sites-administering/experience-fragments-target.md) feature, you can:
-->

Usando o recurso Exportar para Público alvo, é possível:

* criar um fragmento de experiência,
* add components to it,
* e, em seguida, exporte-o como uma Oferta de Público alvo da Adobe, em Formato HTML ou Formato JSON.

This feature can be enabled on an author instance of AEM. It requires a valid Adobe Target Configuration, and configurations for the Link Externalizer.

<!--
This feature can be [enabled on an author instance of AEM](/help/sites-administering/experience-fragments-target.md#Prerequisites). It requires a valid Adobe Target Configuration, and configurations for the Link Externalizer.
-->

The Link Externalizer is used to determine the correct URLs needed when creating the HTML version of the Target Offer, which is subsequently sent to Adobe Target. This is necessary as Adobe Target requires that all links inside the Target HTML Offer can be publicly accessed; this means that any resources the links reference, and the Experience Fragment itself, must be published before they can be used.

By default, when you construct a Target HTML Offer, a request is sent to a custom Sling selector in AEM. This selector is called `.nocloudconfigs.html`. As its name implies, it creates a plain HTML rendering of an Experience Fragment, but does not include cloud configurations (which would be superfluous information).

After you generate the HTML page, the Sling Rewriter pipeline makes modifications to the output:

1. The `html`, `head`, and `body` elements are replaced with `div` elements. The `meta`, `noscript` and `title` elements are removed (they are child elements of the original `head` element, and are not considered when this is replaced by the `div` element).

   This is done to ensure that the HTML Target Offer can be included in Target Activities.

2. AEM modifies any internal links present in the HTML, so that they point to a published resource.

   Para determinar os links a serem modificados, o AEM segue este padrão para atributos de elementos HTML:

   1. `src` atributos
   2. `href` atributos
   3. `*-src` atributos (como data-src, custom-src etc)
   4. `*-href` atributos (como `data-href`, `custom-href`, `img-href`etc)
   >[!NOTE]
   >
   >Na maioria dos casos, os links internos no HTML são links relativos, mas pode haver casos em que os componentes personalizados fornecem URLs completos no HTML. Por padrão, o AEM ignora esses URLs completos e não faz modificações.

   Os links nesses atributos são executados pelo Externalizador de links do AEM `publishLink()` para recriar o URL como se ele estivesse em uma instância publicada e, como tal, disponível ao público.

Ao usar uma implementação predefinida, o processo descrito acima deve ser suficiente para gerar a Oferta do Público alvo a partir do Fragmento de experiência e exportá-la para o Público alvo da Adobe. No entanto, existem alguns casos de utilização que não são tidos em conta neste processo; eles incluem:

* Mapeamento Sling disponível somente na instância de publicação
* Redirecionamentos do Dispatcher

Para esses casos de uso, o AEM fornece a Interface do provedor de regravação de links.

### Interface do provedor de regravador de links {#link-rewriter-provider-interface}

For more complicated cases, not covered by the [default](#default-link-rewriting), AEM offers the Link Rewriter Provider Interface. Esta é uma `ConsumerType` interface que você pode implementar em seus pacotes, como um serviço. It bypasses the modifications AEM performs on internal links of an HTML offer as rendered from an Experience Fragment. This interface allows you to customize the process of rewriting internal HTML links to align with your business needs.

Examples of use cases for implementing this interface as a service include:

* Sling Mappings are enabled on the publish instances, but not on the author instance
* A dispatcher or similar technology is used to redirect URLs internally
* There are `sling:alias mechanisms` in place for resources

>[!NOTE]
>
>This interface only processes the internal HTML links from the generated Target Offer.

The Link Rewriter Provider Interface ( `ExperienceFragmentLinkRewriterProvider`) is as follows:

```java
public interface ExperienceFragmentLinkRewriterProvider {

    String rewriteLink(String link, String tag, String attribute);

    boolean shouldRewrite(ExperienceFragmentVariation experienceFragment);

    int getPriority();

}
```

### How to use the Link Rewriter Provider Interface {#how-to-use-the-link-rewriter-provider-interface}

To use the interface you first need to create a bundle containing a new service component that implements the Link Rewriter Provider interface.

This service will be used to plug into the Experience Fragment Export to Target rewriting in order to have access to the various links.

Por exemplo, `ComponentService`:

```java
import com.adobe.cq.xf.ExperienceFragmentLinkRewriterProvider;
import com.adobe.cq.xf.ExperienceFragmentVariation;
import org.osgi.service.component.annotations.Service;
import org.osgi.service.component.annotations.Component;

@Component
@Service
public class GeneralLinkRewriter implements ExperienceFragmentLinkRewriterProvider {

    @Override
    public String rewriteLink(String link, String tag, String attribute) {
        return null;
    }

    @Override
    public boolean shouldRewrite(ExperienceFragmentVariation experienceFragment) {
        return false;
    }

    @Override
    public int getPriority() {
        return 0;
    }

}
```

For the service to work, there are now three methods that need to be implemented inside the service:

* ` [shouldRewrite](#shouldrewrite)`
* ` [rewriteLink](#rewritelink)`

   * `rewriteLinkExample2`

* ` [getPriority](#priorities-getpriority)`

#### shouldRewrite {#shouldrewrite}

You need to indicate to the system whether it needs to rewrite the links when a call is made for Export to Target on a certain Experience Fragment variation. You do this by implementing the method:

`shouldRewrite(ExperienceFragmentVariation experienceFragment);`

Por exemplo:

```java
@Override
public boolean shouldRewrite(ExperienceFragmentVariation experienceFragment) {
    return experienceFragment.getPath().equals("/content/experience-fragment/master");
}
```

This method receives, as a parameter, the Experience Fragment Variation that the Export to Target system is currently rewriting.

In the example above, we would like to rewrite:

* links presentes em `src`

* `href` attributes only

* for a specific Experience Fragment:
   `/content/experience-fragment/master`

Any other Experience Fragments that pass through the Export to Target system are ignored and not affected by changes implemented in this Service.

#### rewriteLink {#rewritelink}

For the Experience Fragment variation impacted by the rewriting process, it will then proceed to let the service handle the link rewriting. Everytime a link is encountered in the internal HTML, the following method is invoked:

`rewriteLink(String link, String tag, String attribute)`

As input, the method receives the parameters:

* `link`
The `String` representation of the link that is currently being processed. This is usually a relative URL pointing to the resource on the author instance.

* `tag`
The name of the HTML element that is currently being processed.

* `attribute`
The exact attribute name.

Se, por exemplo, o sistema Exportar para Público alvo estiver processando esse elemento no momento, você pode definir `CSSInclude` como:

```java
<link rel="stylesheet" href="/etc.clientlibs/foundation/clientlibs/main.css" type="text/css">
```

A chamada para o `rewriteLink()` método é feita usando estes parâmetros:

```java
rewriteLink(link="/etc.clientlibs/foundation/clientlibs/main.css", tag="link", attribute="href" )
```

Ao criar o serviço, você pode tomar decisões com base na entrada fornecida e, em seguida, reescrever o link de acordo.

Para nosso exemplo, gostaríamos de remover a parte `/etc.clientlibs` do URL e adicionar o domínio externo apropriado. Para simplificar, consideraremos que temos acesso a um Resolvedor de recursos para seu serviço, como em `rewriteLinkExample2`:

>[!NOTE]
>
>Para obter mais informações sobre como obter um resolvedor de recursos por meio de um usuário de serviço, consulte Usuários de serviço no AEM.

<!--
>For more information on how to get a resource resolver through a service user see [Service Users in AEM](/help/sites-administering/security-service-users.md).
-->

```java
private ResourceResolver resolver;

private Externalizer externalizer;

@Override
public String rewriteLink(String link, String tag, String attribute) {

    // get the externalizer service
    externalizer = resolver.adaptTo(Externalizer.class);
    if(externalizer == null) {
        // if there was an error, then we do not modify the link
        return null;
    }

    // remove leading /etc.clientlibs from resource link before externalizing
    link = link.replaceAll("/etc.clientlibs", "");

    // considering that we configured our publish domain, we directly apply the publishLink() method
    link = externalizer.publishLink(resolver, link);

    return link;
}
```

>[!NOTE]
>
>If the above method returns `null`, then the Export to Target system will leave the link as it is, a relative link to a resource.

#### Priorities - getPriority {#priorities-getpriority}

It is not uncommon to need several services to cater for different kinds of Experience Fragments, or even to have a Generic Service that handles externalizing and mapping for all Experience Fragments. In these cases, conflicts about which service to use might arise, so AEM provides the possibility to define **Priorities** for different services. The priorities are specified by using the method:

* `getPriority()`

Esse método permite o uso de vários serviços nos quais o `shouldRewrite()` método retorna true para o mesmo Fragmento de experiência. O serviço que retorna o maior número de seu `getPriority()`método é o serviço que lida com a Variação do fragmento de experiência.

As an example, you can have a `GenericLinkRewriterProvider` that handles the basic mapping for all Experience Fragments and when the `shouldRewrite()` method returns `true` for all Experience Fragment Variations. For several specific Experience Fragments, you may want special handling, so in this case, you can provide a `SpecificLinkRewriterProvider` for which the `shouldRewrite()` method returns true only for some Experience Fragment Variations. Para garantir que `SpecificLinkRewriterProvider` seja escolhido para lidar com essas Variações de fragmento de experiência, ele deve retornar em seu `getPriority()` método um número maior que `GenericLinkRewriterProvider.`