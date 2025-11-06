---
title: Visão geral dos fragmentos de experiência
description: Estender fragmentos de experiência para o Adobe Experience Manager as a Cloud Service
exl-id: bd4ea763-d17c-40a6-9a86-a24d7600229e
feature: Developing, Experience Fragments
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1657'
ht-degree: 0%

---

# Fragmentos de experiência{#experience-fragments}

## Noções básicas {#the-basics}

Um [Fragmento de experiência](/help/sites-cloud/authoring/fragments/content-fragments.md) é um grupo de um ou mais componentes, incluindo conteúdo e layout, que podem ser referenciados nas páginas.

Um Fragmento de experiência principal, ou uma variante, ou ambos, usa:

* `sling:resourceType` : `/libs/cq/experience-fragments/components/xfpage`

Como não há `/libs/cq/experience-fragments/components/xfpage/xfpage.html`, ele é revertido para

* `sling:resourceSuperType` : `wcm/foundation/components/page`

## A representação HTML simples {#the-plain-html-rendition}

Usando o seletor `.plain.` na URL, você poderá acessar a representação simples do HTML.

Essa representação está disponível no navegador. No entanto, seu objetivo principal é permitir que outros aplicativos (por exemplo, aplicativos Web de terceiros, implementações personalizadas de publicações de conteúdo para dispositivos móveis) acessem o conteúdo do Fragmento de experiência diretamente, usando apenas o URL.

A representação simples do HTML adiciona o protocolo, o host e o caminho de contexto aos caminhos que são:

* do tipo: `src`, `href` ou `action`

* ou terminar com: `-src` ou `-href`

Por exemplo:

`.../brooklyn-coat/master.plain.html`

>[!NOTE]
>
>Os links sempre fazem referência à instância de publicação. Eles são destinados ao consumo por terceiros, de modo que o link é sempre chamado da instância de publicação, não da instância do autor.
>
>Para obter mais informações, consulte [Externalizar URLs](/help/implementing/developing/tools/externalizer.md).

![Representação simples de HTML](assets/xf-14.png)

O seletor de representação simples usa um transformador em vez de scripts adicionais. O [Sling Rewriter](https://sling.apache.org/documentation/bundles/output-rewriting-pipelines-org-apache-sling-rewriter.html) é usado como transformador. Esse transformador é configurado da seguinte maneira:

* `/libs/experience-fragments/config/rewriter/experiencefragments`

### Configuração da geração de representação do HTML {#configuring-html-rendition-generation}

A representação do HTML é gerada usando os Pipelines de reescrita do Sling. O pipeline está definido em `/libs/experience-fragments/config/rewriter/experiencefragments`. O transformador do HTML é compatível com as seguintes opções:

* `allowedCssClasses`
   * Uma expressão RegEx que corresponde às classes CSS que devem ser deixadas na representação final.
   * Essa opção é útil se o cliente quiser eliminar algumas classes CSS específicas
* `allowedTags`
   * Uma lista de tags do HTML que serão permitidas na representação final.
   * Por padrão, as seguintes tags são permitidas (nenhuma configuração é necessária): html, head, title, body, img, p, span, ul, li, a, b, i, em, strong, h1, h2, h3, h4, h5, h6, br, noscript, div, link e script

A Adobe recomenda configurar a reescrita usando uma sobreposição. Consulte [Sobreposições no AEM as a Cloud Service](/help/implementing/developing/introduction/overlays.md).

## Modelos para fragmentos de experiência {#templates-for-experience-fragments}

>[!CAUTION]
>
>***Somente*** modelos editáveis têm suporte para Fragmentos de experiência.
>
>Os Fragmentos de experiência só podem ser usados em páginas baseadas em modelos editáveis.

<!-- 
***Only*** [editable templates](/help/sites-developing/page-templates-editable.md) are supported for Experience Fragments.
-->

Ao desenvolver um novo modelo para Fragmentos de experiência, você pode seguir as práticas padrão para um modelo editável.

<!-- 
When developing a new template for Experience Fragments you can follow the standard practices for an [editable template](/help/sites-developing/page-templates-editable.md).
-->

Para criar um modelo de Fragmento de experiência detectado pelo assistente **Criar Fragmento de Experiência**, siga um destes conjuntos de regras:

1. Ambos:

   1. O tipo de recurso do template (o nó inicial) deve herdar de:
      `cq/experience-fragments/components/xfpage`

   1. E o nome do template deve começar com:
      `experience-fragments`
Esse padrão permite que os usuários criem fragmentos de experiência em /content/experience-fragments, pois a propriedade `cq:allowedTemplates` dessa pasta inclui todos os modelos com nomes que começam com `experience-fragment`. Os clientes podem atualizar essa propriedade para incluir seu próprio esquema de nomenclatura ou locais do modelo.

1. [Modelos permitidos](/help/sites-cloud/authoring/fragments/content-fragments.md#configure-allowed-templates-folder) podem ser configurados no console Fragmentos de experiência.

<!--
1. Add the template details manually in `cq:allowedTemplates` on the `/content/experience-fragment` node.
-->

<!-- 
>[!NOTE]
>
>[Allowed templates](/help/sites-authoring/experience-fragments.md#configuring-allowed-templates) can be configured in the Experience Fragments console.
-->

## Componentes para fragmentos de experiência {#components-for-experience-fragments}

O desenvolvimento de componentes para uso com/nos Fragmentos de experiência segue as práticas padrão.

A única configuração adicional é garantir que os componentes sejam permitidos no modelo. Essa permissão é obtida com a Política de conteúdo.

<!--
[Developing components](/help/sites-developing/components.md) for use with/in Experience Fragments follow standard practices.

The only additional configuration is to ensure that the components are [allowed on the template, this is achieved with the Content Policy](/help/sites-developing/page-templates-editable.md#content-policies).
-->

## O provedor de reescrita de link do fragmento de experiência - HTML {#the-experience-fragment-link-rewriter-provider-html}

No AEM, é possível criar fragmentos de experiência. Um fragmento de experiência:

* consiste em um grupo de componentes juntamente com um layout,
* O pode existir independentemente de uma página do AEM.

Um dos casos de uso para esses grupos é para incorporar conteúdo em pontos de contato de terceiros, como o Adobe Target.

### Reescrita de link padrão {#default-link-rewriting}

<!--Using the [Export to Target](/help/sites-administering/experience-fragments-target.md) feature, you can:
-->

Com o recurso Exportar para o Target, você pode:

* criar um fragmento de experiência,
* adicionar componentes a ele,
* e, em seguida, exporte-a como uma Oferta do Adobe Target, no Formato HTML ou JSON.

Esse recurso pode ser ativado em uma instância de autor do AEM. Ele requer uma configuração válida do Adobe Target e configurações para o Externalizador de links.

<!--
This feature can be [enabled on an author instance of AEM](/help/sites-administering/experience-fragments-target.md#Prerequisites). It requires a valid Adobe Target Configuration, and configurations for the Link Externalizer.
-->

O Externalizador de links é usado para determinar os URLs corretos necessários ao criar a versão do HTML da oferta do Target, que é então enviada para o Adobe Target. Esse processo é necessário, pois o Adobe Target exige que todos os links dentro da Oferta do Target HTML possam ser acessados publicamente. Isso significa que todos os recursos aos quais os links fazem referência e o próprio fragmento de experiência devem ser publicados antes de serem usados.

Por padrão, ao criar uma oferta do HTML do Target, uma solicitação é enviada para um seletor de Sling personalizado no AEM. Este seletor é chamado `.nocloudconfigs.html`. Como o nome indica, ele cria uma renderização de HTML simples de um Fragmento de experiência, mas não inclui configurações de nuvem (que seriam informações supérfluas).

Depois de gerar a página do HTML, o pipeline de reescrita do Sling é modificado para a saída:

1. Os elementos `html`, `head` e `body` são substituídos por elementos `div`. Os elementos `meta`, `noscript` e `title` são removidos (são elementos filho do elemento `head` original e não são considerados quando substituídos pelo elemento `div`).

   Esse processo é feito para garantir que a Oferta do HTML Target possa ser incluída nas Atividades do Target.

2. O AEM modifica todos os links internos presentes no HTML, para que eles apontem para um recurso publicado.

   Para determinar os links a serem modificados, o AEM segue esse padrão para atributos de elementos HTML:

   1. `src` atributos
   2. `href` atributos
   3. `*-src` atributos (como `data-src` e `custom-src`)
   4. `*-href` atributos (como `data-href`, `custom-href`, e `img-href`)

   >[!NOTE]
   >
   >Os links internos no HTML são links relativos, mas pode haver casos em que os componentes personalizados forneçam URLs completos na HTML. Por padrão, o AEM ignora esses URLs completos e não faz modificações.

   Os links nesses atributos são executados por meio do AEM Link Externalizer `publishLink()` para recriar a URL como se ela estivesse em uma instância publicada e, como tal, disponibilizada publicamente.

Ao usar uma implementação pronta para uso, o processo descrito acima deve ser suficiente para gerar a oferta do Target a partir do fragmento de experiência e, em seguida, exportá-la para o Adobe Target. No entanto, há alguns casos de uso que não são considerados nesse processo. Alguns desses casos que não são considerados para incluem o seguinte:

* Mapeamento do Sling disponível somente na instância de publicação
* Redirecionamentos do Dispatcher

Para esses casos de uso, a AEM fornece a interface do provedor de reescrita de links.

### Interface do provedor de reescrita de links {#link-rewriter-provider-interface}

Para casos mais complicados, não cobertos pelo [padrão](#default-link-rewriting), a AEM oferece a Interface do Provedor de Reescrita de Link. Esta interface é uma interface `ConsumerType` que você pode implementar em seus pacotes, como um serviço. Ele ignora as modificações que o AEM realiza em links internos de uma oferta do HTML, conforme renderizado a partir de um Fragmento de experiência. Essa interface permite personalizar o processo de reescrita de links internos do HTML para alinhar-se às suas necessidades comerciais.

Exemplos de casos de uso para implementar essa interface como um serviço incluem:

* Os Mapeamentos do Sling são ativados nas instâncias de publicação, mas não na instância do autor
* Uma Dispatcher ou tecnologia semelhante é usada para redirecionar URLs internamente
* Os `sling:alias mechanisms` estão em vigor para os recursos

>[!NOTE]
>
>Essa interface processa apenas os links internos do HTML da Oferta do Target gerada.

A Interface do Provedor de Reescrita de Link ( `ExperienceFragmentLinkRewriterProvider`) é a seguinte:

```java
public interface ExperienceFragmentLinkRewriterProvider {

    String rewriteLink(String link, String tag, String attribute);

    boolean shouldRewrite(ExperienceFragmentVariation experienceFragment);

    int getPriority();

}
```

### Como usar a interface do provedor de reescrita de links {#how-to-use-the-link-rewriter-provider-interface}

Para usar a interface, primeiro você deve criar um pacote contendo um novo componente de serviço que implemente a interface do Provedor de reescrita de link.

Esse serviço é usado para conectar à regravação da Exportação do fragmento de experiência para o Target, para que ele possa ter acesso aos vários links.

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

Para que o serviço funcione, agora há três métodos que devem ser implementados dentro do serviço:

* `[shouldRewrite](#shouldrewrite)`
* `[rewriteLink](#rewritelink)`

   * `rewriteLinkExample2`

* `[getPriority](#priorities-getpriority)`

#### shouldRewrite {#shouldrewrite}

Indique ao sistema se ele deve regravar os links quando é feita uma chamada para Export to Target em uma determinada variação do Fragmento de experiência. Você pode implementar o seguinte método:

`shouldRewrite(ExperienceFragmentVariation experienceFragment);`

Por exemplo:

```java
@Override
public boolean shouldRewrite(ExperienceFragmentVariation experienceFragment) {
    return experienceFragment.getPath().equals("/content/experience-fragment/master");
}
```

Esse método recebe como parâmetro a variação do Fragmento de experiência que o sistema de Exportação para o Target está regravando.

No exemplo acima, você deseja reescrever:

* links presentes em `src`

* Somente atributos de `href`

* para um Fragmento de experiência específico:
  `/content/experience-fragment/master`

Quaisquer outros Fragmentos de experiência que passam pelo sistema Exportar para o Target são ignorados e não são afetados pelas alterações implementadas neste Serviço.

#### rewriteLink {#rewritelink}

Para a variação do Fragmento de experiência afetada pelo processo de regravação, ela continua a permitir que o serviço lide com a regravação do link. Sempre que um link é encontrado no HTML interno, o seguinte método é chamado:

`rewriteLink(String link, String tag, String attribute)`

Como entrada, o método recebe os parâmetros:

* `link`
A representação `String` do link que está sendo processado. Essa representação geralmente é um URL relativo que aponta para o recurso na instância do autor.

* `tag`
O nome do elemento HTML que está sendo processado.

* `attribute`
O nome exato do atributo.

Por exemplo, se o sistema Exportar para Destino estiver processando esse elemento, você poderá definir `CSSInclude` como:

```java
<link rel="stylesheet" href="/etc.clientlibs/foundation/clientlibs/main.css" type="text/css">
```

A chamada para o método `rewriteLink()` é feita usando estes parâmetros:

```java
rewriteLink(link="/etc.clientlibs/foundation/clientlibs/main.css", tag="link", attribute="href" )
```

Ao criar o serviço, suas decisões são baseadas na entrada fornecida e, em seguida, reescrevem o link de acordo.

Por exemplo, você deseja remover a parte `/etc.clientlibs` da URL e adicionar o domínio externo apropriado. Para simplificar, considere que você tenha acesso a um Resource Resolver para o seu serviço, como em `rewriteLinkExample2`:

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
>Se o método acima retornar `null`, o sistema Export to Target deixará o link como está, um link relativo para um recurso.

#### Prioridades - getPriority {#priorities-getpriority}

Não é incomum precisar de vários serviços para atender a diferentes tipos de Fragmentos de experiência, ou até mesmo ter um Serviço genérico que lida com a externalização e o mapeamento de todos os Fragmentos de experiência. Nesses casos, podem surgir conflitos sobre qual serviço usar. Por isso, a AEM oferece a possibilidade de definir **Prioridades** para diferentes serviços. As prioridades são especificadas usando o método:

* `getPriority()`

Este método permite o uso de vários serviços em que o método `shouldRewrite()` retorna &quot;true&quot; para o mesmo Fragmento de experiência. O serviço que retorna o número mais alto de seu método `getPriority()` é o que manipula a variação do fragmento de experiência.

Como exemplo, você pode ter um `GenericLinkRewriterProvider` que manipula o mapeamento básico para todos os Fragmentos de experiência e quando o método `shouldRewrite()` retorna `true` para todas as Variações de Fragmento de experiência. Para vários Fragmentos de experiência específicos, talvez você queira manuseio especial; portanto, nesse caso, você pode fornecer um `SpecificLinkRewriterProvider` para o qual o método `shouldRewrite()` retorna &quot;true&quot; somente para algumas Variações de Fragmento de experiência. Para garantir que `SpecificLinkRewriterProvider` seja escolhido para lidar com essas Variações de Fragmento de Experiência, ele deve retornar em seu método `getPriority()` um número maior que `GenericLinkRewriterProvider.`
