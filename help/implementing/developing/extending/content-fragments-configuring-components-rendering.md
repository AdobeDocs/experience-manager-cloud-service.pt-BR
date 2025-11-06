---
title: Fragmentos de conteúdo configuram componentes para renderização
description: Fragmentos de conteúdo configuram componentes para renderização
exl-id: 6606dc3b-f1b8-4941-8fd0-f69cbd414afa
feature: Developing, Content Fragments
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 5%

---

# Fragmentos de conteúdo configuram componentes para renderização{#content-fragments-configuring-components-for-rendering}

Há vários [serviços avançados](#definition-of-advanced-services-that-need-configuration) relacionados à renderização de fragmentos de conteúdo. Para usar esses serviços, os tipos de recursos desses componentes devem se tornar conhecidos pela estrutura de fragmentos de conteúdo.

Isso é feito configurando o [Serviço OSGi - Configuração do componente de fragmento de conteúdo](#osgi-service-content-fragment-component-configuration).

Essas informações são necessárias quando:

* Você precisa implementar seu próprio componente baseado em Fragmento de conteúdo,
* E precisam usar os serviços avançados.

A Adobe recomenda usar os Componentes principais.

>[!CAUTION]
>
>* **Se você não precisar dos [serviços avançados](#definition-of-advanced-services-that-need-configuration)** descritos abaixo, ignore essa configuração.
>
>* **Ao estender ou usar o(s) componente(s) predefinido(s)**, não é recomendável alterar a configuração do OSGi.
>
>* **Você pode gravar um componente do zero que use somente a API de fragmentos de conteúdo, sem serviços avançados**. No entanto, nesse caso, será necessário desenvolver o componente para que ele manipule o processamento apropriado.
>
>Portanto, é recomendável usar os Componentes principais.

## Definição de serviços avançados que precisam de configuração {#definition-of-advanced-services-that-need-configuration}

Os serviços que exigem o registro de um componente são:

* Determinar as dependências corretamente durante a publicação (ou seja, verifique se os fragmentos e modelos podem ser publicados automaticamente com uma página se foram alterados desde a última publicação).
* Suporte para fragmentos de conteúdo na pesquisa de texto completo.
* O gerenciamento/manuseio de *conteúdo intermediário.*
* O gerenciamento/manuseio de *ativos de mídia mista.*
* Limpeza do Dispatcher para fragmentos referenciados (se uma página contendo um fragmento for republicada).
* Uso da renderização baseada em parágrafo.

Se você precisar de um ou mais desses recursos, (normalmente) é mais fácil usar os Serviços avançados prontos para uso, em vez de desenvolvê-los do zero.

## Serviço OSGi - Configuração do componente de fragmento de conteúdo {#osgi-service-content-fragment-component-configuration}

A configuração deve ser associada à **Configuração do componente de fragmento de conteúdo** do serviço OSGi:

`com.adobe.cq.dam.cfm.impl.component.ComponentConfigImpl`

>[!NOTE]
>
>Consulte [Configuração OSGi](/help/implementing/deploying/overview.md#osgi-configuration) para obter mais detalhes.

Por exemplo:

![Configuração do componente de fragmento de conteúdo da configuração OSGi](assets/cf-component-configuration-osgi.png)

A configuração do OSGi é:

<table>
 <thead>
  <tr>
   <td>Rótulo</td>
   <td>Configuração OSGi<br /> </td>
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
   <td>O nome da propriedade que contém a referência ao fragmento; por exemplo, <code>fragmentPath</code> ou <code>fileReference</code></td>
  </tr>
  <tr>
   <td><strong>Propriedade dos elementos</strong></td>
   <td><code>dam.cfm.component.elementsProp</code></td>
   <td>O nome da propriedade que contém o(s) nome(s) do(s) elemento(s) a serem renderizados; por exemplo,<code>elementName</code></td>
  </tr>
  <tr>
   <td><strong>Propriedade de variação</strong><br /> </td>
   <td><code>dam.cfm.component.variationProp</code></td>
   <td>O nome da propriedade que contém o nome da variação a ser renderizada; por exemplo,<code>variationName</code></td>
  </tr>
 </tbody>
</table>

Para algumas funcionalidades, seu componente terá que aderir a convenções predefinidas. A tabela a seguir detalha as propriedades que precisam ser definidas pelo componente para cada parágrafo (ou seja, `jcr:paragraph` para cada instância de componente) para que os serviços possam detectá-las e processá-las corretamente.

<table>
 <thead>
  <tr>
   <td>Nome de propriedade</td>
   <td>Descrição</td>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><code>paragraphScope</code></td>
   <td><p>Uma propriedade de cadeia de caracteres que define como os parágrafos devem ser gerados se estiverem no <em>modo de renderização de elemento único</em>.</p> <p>Valores:</p>
    <ul>
     <li><code>all</code> : para renderizar todos os parágrafos</li>
     <li><code>range</code> : para renderizar o intervalo de parágrafos fornecido por <code>paragraphRange</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>paragraphRange</code></td>
   <td><p>Uma propriedade de cadeia de caracteres que define o intervalo de parágrafos a ser gerado se estiver em <em>modo de renderização de elemento único</em>.</p> <p>Formato:</p>
    <ul>
     <li><code>1</code> ou <code>1-3</code> ou <code>1-3;6;7-8</code> ou <code>*-3;5-*</code>
     <ul>
       <li><code>-</code> indicador de intervalo</li>
       <li><code>;</code> separador de lista</li>
       <li><code>*</code> curinga</li>
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

Como exemplo, consulte o seguinte (em uma instância do AEM pronta para uso):

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
