---
title: Fragmentos de conteúdo configuram componentes para renderização
description: Fragmentos de conteúdo configuram componentes para renderização
translation-type: tm+mt
source-git-commit: a5d6a072dfd8df887309f56ad4a61b6b38b32fa7
workflow-type: tm+mt
source-wordcount: '518'
ht-degree: 6%

---


# Fragmentos de conteúdo configuram componentes para renderização{#content-fragments-configuring-components-for-rendering}

Há vários serviços [](#definition-of-advanced-services-that-need-configuration) avançados relacionados à renderização de fragmentos de conteúdo. Para usar esses serviços, os tipos de recursos desses componentes devem se tornar conhecidos pela estrutura de fragmentos de conteúdo.

Isso é feito configurando o serviço [OSGi - Configuração](#osgi-service-content-fragment-component-configuration)do componente de fragmento de conteúdo.

Essas informações são necessárias quando:

* É necessário implementar seu próprio componente baseado em Fragmento de conteúdo,
* E precisa usar os serviços avançados.

É recomendável usar os Componentes principais.

>[!CAUTION]
>
>* **Se não precisar dos serviços[](#definition-of-advanced-services-that-need-configuration)**avançados descritos abaixo, ignore essa configuração.
   >
   >
* **Ao estender ou usar os componentes prontos para uso**, não é recomendável alterar a configuração do OSGi.
   >
   >
* **Você pode gravar um componente do zero que usa somente a API Fragmentos de conteúdo, sem serviços** avançados. No entanto, nesse caso, você terá que desenvolver seu componente para que ele lide com o processamento apropriado.
>
>
Portanto, é recomendável usar os Componentes principais.

## Definição de serviços avançados que precisam de configuração {#definition-of-advanced-services-that-need-configuration}

Os serviços que exigem o registro de um componente são:

* Determinar as dependências corretamente durante a publicação (isto é, garantir que os fragmentos e modelos possam ser publicados automaticamente com uma página se tiverem sido alterados desde a última publicação).
* Suporte para fragmentos de conteúdo na pesquisa de texto completo.
* Gerenciamento/tratamento de conteúdo *intermediário.*
* A gestão/tratamento de ativos de *meios de comunicação mistos.*
* O Dispatcher libera fragmentos referenciados (se uma página que contém um fragmento for republicada).
* Uso de renderização baseada em parágrafo.

Se você precisar de um ou mais desses recursos, então (normalmente) é mais fácil usar os Serviços avançados prontos para uso, em vez de desenvolvê-los do zero.

## Serviço OSGi - Configuração do componente de fragmento de conteúdo {#osgi-service-content-fragment-component-configuration}

A configuração precisa estar vinculada à Configuração **do componente de fragmento de** conteúdo do serviço OSGi:

`com.adobe.cq.dam.cfm.impl.component.ComponentConfigImpl`

>[!NOTE]
>
>Consulte Configuração [do](/help/implementing/deploying/overview.md#osgi-configuration) OSGi para obter mais detalhes.

Por exemplo:

![Configuração do componente de fragmento de conteúdo da configuração do OSGi](assets/cf-component-configuration-osgi.png)

A configuração do OSGi é:

<table>
 <thead>
  <tr>
   <td>Etiqueta</td>
   <td>Configuração do OSGi<br /> </td>
   <td>Descrição</td>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><strong>Tipo de recurso</strong></td>
   <td><code>dam.cfm.component.resourceType</code></td>
   <td>O tipo de recurso a ser registrado; por exemplo, <br /> <p><span class="cmp-examples-demo__property-value"><code>core/wcm/components/contentfragment/v1/contentfragment</code></code></p> </td>
  </tr>
  <tr>
   <td><strong>Propriedade de referência</strong></td>
   <td><code>dam.cfm.component.fileReferenceProp</code></td>
   <td>O nome da propriedade que contém a referência ao fragmento; por exemplo <code>fragmentPath</code> ou <code>fileReference</code></td>
  </tr>
  <tr>
   <td><strong>Propriedade do(s) elemento(s)</strong></td>
   <td><code>dam.cfm.component.elementsProp</code></td>
   <td>O nome da propriedade que contém os nomes dos elementos a serem renderizados; por exemplo,<code>elementName</code></td>
  </tr>
  <tr>
   <td><strong>Propriedade de variação</strong><br /> </td>
   <td><code>dam.cfm.component.variationProp</code></td>
   <td>O nome da propriedade que contém o nome da variação a ser renderizada; por exemplo,<code>variationName</code></td>
  </tr>
 </tbody>
</table>

Para algumas funcionalidades, seu componente terá que aderir às convenções predefinidas. A tabela a seguir detalha as propriedades que precisam ser definidas, pelo seu componente, para cada parágrafo (isto é, `jcr:paragraph` para cada instância do componente) para que os serviços possam detectá-las e processá-las corretamente.

<table>
 <thead>
  <tr>
   <td>Nome da Propriedade</td>
   <td>Descrição</td>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><code>paragraphScope</code></td>
   <td><p>Uma propriedade de string que define como os parágrafos devem ser exibidos se estiverem no modo <em>de renderização de</em>um único elemento.</p> <p>Valores:</p>
    <ul>
     <li><code>all</code> : para renderizar todos os parágrafos</li>
     <li><code>range</code> : para renderizar o intervalo de parágrafos fornecido por <code>paragraphRange</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>paragraphRange</code></td>
   <td><p>Uma propriedade de string que define o intervalo de parágrafos a serem enviados se estiver no modo <em>de renderização de um elemento</em>único.</p> <p>Formato:</p>
    <ul>
     <li><code>1</code> ou <code>1-3</code> ou <code>1-3;6;7-8</code> ou <code>*-3;5-*</code>
     <ul>
       <li><code>-</code> indicador de intervalo</li>
       <li><code>;</code> Separador de lista</li>
       <li><code>*</code> caractere curinga</li>
     </ul>
     </li>
     <li>avaliado somente se <code>paragraphScope</code> estiver definido como <code>range</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>paragraphHeadings</code></td>
   <td>Uma propriedade booleana que define se os cabeçalhos (por exemplo, <code>h1</code>, <code>h2</code>, <code>h3</code>) são contados como parágrafos (<code>true</code>) ou não (<code>false</code>)</td>
  </tr>
 </tbody>
</table>

## Exemplo {#example}

Como exemplo, consulte o seguinte (em uma instância do AEM predefinida):

```
/apps/core/wcm/config/com.adobe.cq.dam.cfm.impl.component.ComponentConfigImpl-core-comp-v1.config
```

Ele contém:

```
dam.cfm.component.resourceType="core/wcm/components/contentfragment/v1/contentfragment"
dam.cfm.component.fileReferenceProp="fragmentPath"
dam.cfm.component.elementsProp="elementName"
dam.cfm.component.variationProp="variationName"
```

