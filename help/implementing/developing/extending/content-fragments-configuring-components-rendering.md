---
title: Fragmentos de conteúdo configuram componentes para renderização
description: Fragmentos de conteúdo configuram componentes para renderização
exl-id: 6606dc3b-f1b8-4941-8fd0-f69cbd414afa
source-git-commit: ca849bd76e5ac40bc76cf497619a82b238d898fa
workflow-type: tm+mt
source-wordcount: '522'
ht-degree: 6%

---

# Fragmentos de conteúdo configuram componentes para renderização{#content-fragments-configuring-components-for-rendering}

Há vários [serviços avançados](#definition-of-advanced-services-that-need-configuration) relacionado à renderização de fragmentos de conteúdo. Para usar esses serviços, os tipos de recursos desses componentes devem se tornar conhecidos pela estrutura de fragmentos de conteúdo.

Isso é feito configurando a variável [Serviço OSGi - Configuração do componente de fragmento de conteúdo](#osgi-service-content-fragment-component-configuration).

Essas informações são necessárias quando:

* É necessário implementar seu próprio componente baseado em Fragmento de conteúdo,
* E precisam usar os serviços avançados.

É recomendável usar os Componentes principais.

>[!CAUTION]
>
>* **Se você não precisar da variável [serviços avançados](#definition-of-advanced-services-that-need-configuration)** descrito abaixo, você pode ignorar essa configuração.
>
>* **Ao estender ou usar os componentes prontos para uso**, não é recomendável alterar a configuração do OSGi.
>
>* **Você pode gravar um componente do zero que usa somente a API de Fragmentos de conteúdo, sem serviços avançados**. No entanto, nesse caso, será necessário desenvolver o componente para que ele manipule o processamento apropriado.
>
>Portanto, é recomendável usar os Componentes principais.

## Definição dos Serviços Avançados que precisam de Configuração {#definition-of-advanced-services-that-need-configuration}

Os serviços que exigem o registro de um componente são:

* Determinar as dependências corretamente durante a publicação (ou seja, verifique se os fragmentos e modelos podem ser publicados automaticamente com uma página se tiverem sido alterados desde a última publicação).
* Suporte para fragmentos de conteúdo na pesquisa de texto completo.
* Gestão/gestão *conteúdo intermediário.*
* Gestão/gestão *ativos de mídia mista.*
* Liberação do Dispatcher para fragmentos referenciados (se uma página contendo um fragmento for republicada).
* Uso de renderização baseada em parágrafo.

Se você precisar de um ou mais desses recursos, então (normalmente) é mais fácil usar os Serviços avançados prontos para uso, em vez de desenvolvê-los do zero.

## Serviço OSGi - Configuração do componente de fragmento de conteúdo {#osgi-service-content-fragment-component-configuration}

A configuração precisa ser vinculada ao serviço OSGi **Configuração do componente de fragmento de conteúdo**:

`com.adobe.cq.dam.cfm.impl.component.ComponentConfigImpl`

>[!NOTE]
>
>Consulte [Configuração do OSGi](/help/implementing/deploying/overview.md#osgi-configuration) para obter mais detalhes.

Por exemplo:

![Configuração do Componente de Fragmento de Conteúdo de Configuração do OSGi](assets/cf-component-configuration-osgi.png)

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
   <td>O nome da propriedade que contém a referência ao fragmento; por exemplo, <code>fragmentPath</code> ou <code>fileReference</code></td>
  </tr>
  <tr>
   <td><strong>Propriedade do(s) elemento(s)</strong></td>
   <td><code>dam.cfm.component.elementsProp</code></td>
   <td>O nome da propriedade que contém o(s) nome(s) dos elementos a serem renderizados; por exemplo,<code>elementName</code></td>
  </tr>
  <tr>
   <td><strong>Propriedade de variação</strong><br /> </td>
   <td><code>dam.cfm.component.variationProp</code></td>
   <td>O nome da propriedade que contém o nome da variação a ser renderizada; por exemplo,<code>variationName</code></td>
  </tr>
 </tbody>
</table>

Para algumas funcionalidades, seu componente terá que aderir às convenções predefinidas. A tabela a seguir detalha as propriedades que precisam ser definidas, pelo seu componente, para cada parágrafo (ou seja, `jcr:paragraph` para cada instância de componente), para que os serviços possam detectá-los e processá-los corretamente.

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
   <td><p>Uma propriedade de string que define como os parágrafos devem ser gerados se em <em>modo de renderização de elemento único</em>.</p> <p>Valores:</p>
    <ul>
     <li><code>all</code> : para renderizar todos os parágrafos</li>
     <li><code>range</code> : para renderizar o intervalo de parágrafos fornecido pelo <code>paragraphRange</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>paragraphRange</code></td>
   <td><p>Uma propriedade de string que define o intervalo de parágrafos a serem gerados se <em>modo de renderização de elemento único</em>.</p> <p>Formato:</p>
    <ul>
     <li><code>1</code> ou <code>1-3</code> ou <code>1-3;6;7-8</code> ou <code>*-3;5-*</code>
     <ul>
       <li><code>-</code> indicador de intervalo</li>
       <li><code>;</code> separador de lista</li>
       <li><code>*</code> curinga</li>
     </ul>
     </li>
     <li>só será avaliado se <code>paragraphScope</code> está definida como <code>range</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>paragraphHeadings</code></td>
   <td>Uma propriedade booleana que define se cabeçalhos (por exemplo, <code>h1</code>, <code>h2</code>, <code>h3</code>) são contadas como parágrafos (<code>true</code>) ou não (<code>false</code>)</td>
  </tr>
 </tbody>
</table>

## Exemplo {#example}

Como exemplo, consulte o seguinte (em uma instância AEM predefinida):

```
/apps/core/wcm/config/com.adobe.cq.dam.cfm.impl.component.ComponentConfigImpl-core-comp-v1.config
```

Isso contém:

```
dam.cfm.component.resourceType="core/wcm/components/contentfragment/v1/contentfragment"
dam.cfm.component.fileReferenceProp="fragmentPath"
dam.cfm.component.elementsProp="elementName"
dam.cfm.component.variationProp="variationName"
```
