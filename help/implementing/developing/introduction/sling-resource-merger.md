---
title: Uso da Fusão de recursos do Sling no Adobe Experience Manager as a Cloud Service
description: O Sling Resource Merger fornece serviços para acessar e mesclar recursos
exl-id: 5b6e5cb5-4c6c-4246-ba67-6b9f752867f5
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '1158'
ht-degree: 1%

---

# Uso do Sling Resource Merger no AEM as a Cloud Service {#using-the-sling-resource-merger-in-aem}

## Propósito {#purpose}

O Sling Resource Merger fornece serviços para acessar e mesclar recursos. Ela fornece mecanismos de diferenciação para:

* **[Sobreposições](/help/implementing/developing/introduction/overlays.md)** de recursos usando os [caminhos de pesquisa](/help/implementing/developing/introduction/overlays.md#search-paths).

* **Substitui** das caixas de diálogo de componente para a interface habilitada para toque (`cq:dialog`), usando a hierarquia de tipo de recurso (por meio da propriedade `sling:resourceSuperType`).

Com o Sling Resource Merger, os recursos e/ou propriedades de sobreposição/substituição são mesclados com os recursos/propriedades originais:

* O conteúdo da definição personalizada tem uma prioridade mais alta que a do original (ou seja, *sobreposições* ou *substituições*).

* Quando necessário, as [propriedades](#properties) definidas na personalização indicam como o conteúdo mesclado do original será usado.

>[!CAUTION]
>
>O Sling Resource Merger e os métodos relacionados só podem ser usados com a interface habilitada para toque (que é a única interface disponível para o AEM as a Cloud Service).

### Metas para o AEM {#goals-for-aem}

As metas para usar a Fusão de recursos do Sling no AEM são:

* verifique se as alterações de personalização não foram feitas em `/libs`.
* reduza a estrutura replicada de `/libs`.

  Ao usar o Sling Resource Merger, não é recomendável copiar toda a estrutura de `/libs`, pois isso resultaria em muitas informações mantidas na personalização (geralmente `/apps`). Duplicar informações aumenta desnecessariamente a chance de problemas quando o sistema é atualizado de alguma forma.

>[!CAUTION]
>
>Você ***deve*** não alterar nada no caminho `/libs`.
>
>Isso ocorre porque o conteúdo de `/libs` pode ser substituído sempre que atualizações forem aplicadas à sua instância.
>
>* As sobreposições dependem dos [caminhos de pesquisa](/help/implementing/developing/introduction/overlays.md#search-paths).
>
>* As substituições não dependem dos caminhos de pesquisa, elas usam a propriedade `sling:resourceSuperType` para fazer a conexão.
>
>No entanto, as substituições geralmente são definidas em `/apps`, já que a prática recomendada no AEM as a Cloud Service é definir personalizações em `/apps`. Isso ocorre porque você não deve alterar nada em `/libs`.

### Propriedades {#properties}

A fusão de recursos oferece as seguintes propriedades:

* `sling:hideProperties` ( `String` ou `String[]`)

  Especifica a propriedade, ou lista de propriedades, a ser ocultada.

  O curinga `*` oculta tudo.

* `sling:hideResource` ( `Boolean`)

  Indica se os recursos devem ser completamente ocultos, incluindo seus filhos.

* `sling:hideChildren` ( `String` ou `String[]`)

  Contém o nó filho, ou lista de nós filhos, a ser ocultado. As propriedades do nó são mantidas.

  O curinga `*` oculta tudo.

* `sling:orderBefore` ( `String`)

  Contém o nome do nó irmão no qual o nó atual deve ser posicionado.

Essas propriedades afetam como os recursos/propriedades correspondentes/originais (de `/libs`) são usados pela sobreposição/substituição (geralmente em `/apps`).

### Criação da estrutura {#creating-the-structure}

Para criar uma sobreposição ou substituição, é necessário recriar o nó original, com a estrutura equivalente, no destino (geralmente `/apps`). Por exemplo:

* Sobreposição

   * A definição da entrada de navegação do console Sites, como mostrado no painel, é definida em:

     `/libs/cq/core/content/nav/sites/jcr:title`

   * Para sobrepor isso, crie o seguinte nó:

     `/apps/cq/core/content/nav/sites`

     Em seguida, atualize a propriedade `jcr:title`, conforme necessário.

* Substituir

   * A definição da caixa de diálogo habilitada para toque do console de Textos está definida em:

     `/libs/foundation/components/text/cq:dialog`

   * Para substituir isso, crie o seguinte nó - por exemplo:

     `/apps/the-project/components/text/cq:dialog`

Para criar qualquer uma dessas opções, basta recriar a estrutura do esqueleto. Para simplificar a recriação da estrutura, todos os nós intermediários podem ser do tipo `nt:unstructured` (eles não precisam refletir o tipo de nó original; por exemplo, em `/libs`).

Portanto, no exemplo de sobreposição acima, os seguintes nós são necessários:

```shell
/apps
  /cq
    /core
      /content
        /nav
          /sites
```

>[!NOTE]
>
>Ao usar o Sling Resource Merger (ou seja, ao lidar com a interface de usuário padrão habilitada para toque), não é recomendável copiar toda a estrutura de `/libs`, pois isso resultaria em muitas informações mantidas em `/apps`. Isso pode causar problemas quando o sistema é atualizado de alguma forma.

### Casos de uso {#use-cases}

Eles, juntamente com a funcionalidade padrão, permitem:

* **Adicionar uma propriedade**

  A propriedade não existe na definição `/libs`, mas é necessária na sobreposição/substituição `/apps`.

   1. Criar o nó correspondente em `/apps`
   1. Criar a nova propriedade neste nó &quot;

* **Redefinir uma propriedade (não propriedades criadas automaticamente)**

  A propriedade está definida em `/libs`, mas um novo valor é necessário na sobreposição/substituição `/apps`.

   1. Criar o nó correspondente em `/apps`
   1. Criar a propriedade correspondente neste nó (em / `apps`)

      * A propriedade terá uma prioridade com base na configuração do Sling Resource Resolver.
      * Não há suporte para a alteração do tipo de propriedade.

        Se você usar um tipo de propriedade diferente daquele usado em `/libs`, o tipo de propriedade definido será usado.

  >[!NOTE]
  >
  >Não há suporte para a alteração do tipo de propriedade.

* **Redefinir uma propriedade criada automaticamente**

  Por padrão, as propriedades criadas automaticamente (como `jcr:primaryType`) não estão sujeitas a uma sobreposição/substituição para garantir que o tipo de nó atualmente em `/libs` seja respeitado. Para impor uma sobreposição/substituição, é necessário recriar o nó em `/apps`, ocultar explicitamente a propriedade e redefini-la:

   1. Crie o nó correspondente em `/apps` com o `jcr:primaryType` desejado
   1. Crie a propriedade `sling:hideProperties` nesse nó, com o valor definido como aquele da propriedade criada automaticamente; por exemplo, `jcr:primaryType`

      Esta propriedade, definida em `/apps`, terá prioridade sobre aquela definida em `/libs`

* **Redefinir um nó e seus filhos**

  O nó e seus filhos estão definidos em `/libs`, mas uma nova configuração é necessária na sobreposição/substituição `/apps`.

   1. Combine as ações de:

      1. Ocultar filhos de um nó (mantendo as propriedades do nó)
      1. Redefinir a propriedade/as propriedades

* **Ocultar uma propriedade**

  A propriedade está definida em `/libs`, mas não é necessária na sobreposição/substituição de `/apps`.

   1. Criar o nó correspondente em `/apps`
   1. Crie uma propriedade `sling:hideProperties` do tipo `String` ou `String[]`. Use esta opção para especificar as propriedades que devem ser ocultas/ignoradas. Curingas também podem ser usados. Por exemplo:

      * `*`
      * `["*"]`
      * `jcr:title`
      * `["jcr:title", "jcr:description"]`

* **Ocultar um nó e seus filhos**

  O nó e seus filhos estão definidos em `/libs`, mas não são necessários na sobreposição/substituição `/apps`.

   1. Crie o nó correspondente em /apps
   1. Criar uma propriedade `sling:hideResource`

      * tipo: `Boolean`
      * valor: `true`

* **Ocultar filhos de um nó (ao manter as propriedades do nó)**

  O nó, suas propriedades e seus filhos estão definidos em `/libs`. O nó e suas propriedades são necessários na sobreposição/substituição `/apps`, mas alguns ou todos os nós filhos não são necessários na sobreposição/substituição `/apps`.

   1. Criar o nó correspondente em `/apps`
   1. Criar a propriedade `sling:hideChildren`:

      * tipo: `String[]`
      * value: uma lista dos nós filhos (conforme definido em `/libs`) a serem ocultados/ignorados

      O curinga &amp;ast; pode ser usado para ocultar/ignorar todos os nós filhos.

* **Reordenar nós**

  O nó e seus irmãos estão definidos em `/libs`. Uma nova posição é necessária para que o nó seja recriado na sobreposição/substituição `/apps`, onde a nova posição é definida em referência ao nó irmão apropriado em `/libs`.

   * Usar a propriedade `sling:orderBefore`:

      1. Criar o nó correspondente em `/apps`
      1. Criar a propriedade `sling:orderBefore`:

         Isso especifica o nó (como em `/libs`) que o nó atual deve ser posicionado antes:

         * tipo: `String`
         * valor: `<before-SiblingName>`

### Chamar o Sling Resource Merger a partir de seu código {#invoking-the-sling-resource-merger-from-your-code}

O Sling Resource Merger inclui dois provedores de recursos personalizados, um para sobreposições e outro para substituições. Cada um desses pode ser chamado dentro do código usando um ponto de montagem:

>[!NOTE]
>
>Ao acessar o recurso, é recomendável usar o ponto de montagem apropriado.
>
>Isso garante que o Sling Resource Merger seja chamado e que o recurso totalmente mesclado seja retornado (reduzindo a estrutura que deve ser replicada de `/libs`).

* Sobreposição:

   * finalidade: mesclar recursos com base no caminho de pesquisa
   * ponto de montagem: `/mnt/overlay`
   * uso: `mount point + relative path`
   * exemplo:

      * `getResource('/mnt/overlay' + '<relative-path-to-resource>');`

* Substituir:

   * finalidade: mesclar recursos com base em seu supertipo
   * ponto de montagem: `/mnt/overide`
   * uso: `mount point + absolute path`
   * exemplo:

      * `getResource('/mnt/override' + '<absolute-path-to-resource>');`

