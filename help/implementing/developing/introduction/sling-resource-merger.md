---
title: Uso da Fusão de Recursos do Sling no Adobe Experience Manager as a Cloud Service
description: A Sling Resource Merger fornece serviços para acessar e mesclar recursos
exl-id: 5b6e5cb5-4c6c-4246-ba67-6b9f752867f5
source-git-commit: ac760e782f80ee82a9b0604ef64721405fc44ee4
workflow-type: tm+mt
source-wordcount: '1160'
ht-degree: 2%

---

# Uso do Sling Resource Merger no AEM as a Cloud Service {#using-the-sling-resource-merger-in-aem}

## Propósito {#purpose}

A Sling Resource Merger fornece serviços para acessar e mesclar recursos. Ela fornece mecanismos de diferenciação (diferenciação) para ambos:

* **[](/help/implementing/developing/introduction/overlays.md)** Sobreposição de recursos usando os caminhos  [de pesquisa](/help/implementing/developing/introduction/overlays.md#search-paths).

* **** Substituições das caixas de diálogo do componente para a interface habilitada para toque (`cq:dialog`), usando a hierarquia do tipo de recurso (por meio da propriedade  `sling:resourceSuperType`).

Com a Fusão de Recursos do Sling, os recursos de sobreposição/sobreposição e/ou as propriedades são mesclados com os recursos/propriedades originais:

* O conteúdo da definição personalizada tem uma prioridade mais alta do que a original (ou seja, ela *sobreposições* ou *substitui* por ela).

* Sempre que necessário, [propriedades](#properties) definidas na personalização, indique como o conteúdo unido do original deve ser usado.

>[!CAUTION]
>
>A fusão de recursos do Sling e os métodos relacionados só podem ser usados com a interface habilitada para toque (que é a única interface disponível para o AEM como Cloud Service).

### Metas para AEM {#goals-for-aem}

Os objetivos da utilização da fusão de recursos Sling em AEM são:

* verifique se as alterações de personalização não são feitas em `/libs`.
* reduza a estrutura que é replicada de `/libs`.

   Ao usar o Sling Resource Merger, não é recomendável copiar toda a estrutura de `/libs`, pois isso resultaria na retenção de muitas informações na personalização (geralmente `/apps`). A duplicação de informações aumenta desnecessariamente a chance de problemas quando o sistema é atualizado de alguma forma.

>[!CAUTION]
>
>Você ***não deve*** alterar nada no caminho `/libs`.
>
>Isso ocorre porque o conteúdo de `/libs` pode ser substituído sempre que as atualizações forem aplicadas à sua instância.
>
>* As sobreposições dependem de [caminhos de pesquisa](/help/implementing/developing/introduction/overlays.md#search-paths).
>
>* As substituições não dependem dos caminhos de pesquisa, elas usam a propriedade `sling:resourceSuperType` para fazer a conexão.

>
>No entanto, as substituições são frequentemente definidas em `/apps`, já que a prática recomendada no AEM como Cloud Service é definir personalizações em `/apps`; isso ocorre porque você não deve alterar nada em `/libs`.

### Propriedades {#properties}

A fusão de recursos fornece as seguintes propriedades:

* `sling:hideProperties` (  `String` ou  `String[]`)

   Especifica a propriedade, ou lista de propriedades, a ser ocultada.

   O curinga `*` oculta tudo.

* `sling:hideResource` ( `Boolean`)

   Indica se os recursos devem ser completamente ocultos, incluindo seus filhos.

* `sling:hideChildren` (  `String` ou  `String[]`)

   Contém o nó filho ou a lista de nós filhos a serem ocultados. As propriedades do nó serão mantidas.

   O curinga `*` oculta tudo.

* `sling:orderBefore` (  `String`)

   Contém o nome do nó irmão que o nó atual deve ser posicionado na frente.

Essas propriedades afetam como os recursos/propriedades correspondentes/originais (de `/libs`) são usados pela sobreposição/sobreposição (geralmente em `/apps`).

### Criar a estrutura {#creating-the-structure}

Para criar uma sobreposição ou sobreposição, é necessário recriar o nó original, com a estrutura equivalente, no destino (normalmente `/apps`). Por exemplo:

* Sobreposição

   * A definição da entrada de navegação para o console Sites , conforme mostrado no painel, é definida em:

      `/libs/cq/core/content/nav/sites/jcr:title`

   * Para sobrepor isso, crie o seguinte nó:

      `/apps/cq/core/content/nav/sites`

      Em seguida, atualize a propriedade `jcr:title` conforme necessário.

* Substituir

   * A definição da caixa de diálogo habilitada para toque para o console Textos é definida em:

      `/libs/foundation/components/text/cq:dialog`

   * Para substituir isso, crie o seguinte nó - por exemplo:

      `/apps/the-project/components/text/cq:dialog`

Para criar qualquer um desses, você só precisa recriar a estrutura do esqueleto. Para simplificar a recriação da estrutura, todos os nós intermediários podem ser do tipo `nt:unstructured` (não têm de refletir o tipo de nó original; por exemplo, em `/libs`).

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
>Ao usar o Sling Resource Merger (ou seja, ao lidar com a interface padrão habilitada para toque), não é recomendável copiar toda a estrutura de `/libs`, pois resultaria na retenção de muitas informações em `/apps`. Isso pode causar problemas quando o sistema for atualizado de qualquer maneira.

### Casos de uso {#use-cases}

Isso, junto com a funcionalidade padrão, permite:

* **Adicionar uma propriedade**

   A propriedade não existe na definição `/libs`, mas é necessária na sobreposição/sobreposição `/apps`.

   1. Crie o nó correspondente em `/apps`
   1. Crie a nova propriedade neste nó &quot;

* **Redefinir uma propriedade (não propriedades criadas automaticamente)**

   A propriedade é definida em `/libs`, mas um novo valor é necessário na sobreposição/sobreposição `/apps`.

   1. Crie o nó correspondente em `/apps`
   1. Crie a propriedade correspondente neste nó (em / `apps`)

      * A propriedade terá uma prioridade com base na configuração do Resolvedor de Recursos do Sling.
      * A alteração do tipo de propriedade é suportada.

         Se você usar um tipo de propriedade diferente daquele usado em `/libs`, o tipo de propriedade definido será usado.
   >[!NOTE]
   >
   >A alteração do tipo de propriedade é suportada.

* **Redefinir uma propriedade criada automaticamente**

   Por padrão, as propriedades criadas automaticamente (como `jcr:primaryType`) não estão sujeitas a uma sobreposição/sobreposição para garantir que o tipo de nó atualmente em `/libs` seja respeitado. Para impor uma sobreposição/sobreposição, é necessário recriar o nó em `/apps`, ocultar explicitamente a propriedade e redefini-la:

   1. Crie o nó correspondente em `/apps` com o `jcr:primaryType` desejado
   1. Crie a propriedade `sling:hideProperties` nesse nó, com o valor definido como o da propriedade criada automaticamente; por exemplo, `jcr:primaryType`

      Essa propriedade, definida em `/apps`, agora terá prioridade sobre aquela definida em `/libs`

* **Redefinir um nó e seus filhos**

   O nó e seus filhos são definidos em `/libs`, mas uma nova configuração é necessária na sobreposição/sobreposição `/apps`.

   1. Combine as ações de:

      1. Ocultar filhos de um nó (mantendo as propriedades do nó)
      1. Redefinir a propriedade/propriedades

* **Ocultar uma propriedade**

   A propriedade é definida em `/libs`, mas não é necessária na sobreposição/sobreposição `/apps`.

   1. Crie o nó correspondente em `/apps`
   1. Crie uma propriedade `sling:hideProperties` do tipo `String` ou `String[]`. Use esta opção para especificar as propriedades a serem ocultadas/ignoradas. Também é possível usar curingas. Por exemplo:

      * `*`
      * `["*"]`
      * `jcr:title`
      * `["jcr:title", "jcr:description"]`

* **Ocultar um nó e seus filhos**

   O nó e seus filhos são definidos em `/libs`, mas não são necessários na sobreposição/sobreposição `/apps`.

   1. Crie o nó correspondente em /apps
   1. Criar uma propriedade `sling:hideResource`

      * tipo: `Boolean`
      * valor: `true`

* **Ocultar filhos de um nó (ao manter as propriedades do nó)**

   O nó, suas propriedades e seus filhos são definidos em `/libs`. O nó e suas propriedades são necessários na sobreposição/sobreposição `/apps`, mas alguns ou todos os nós filho não são necessários na sobreposição/sobreposição `/apps`.

   1. Crie o nó correspondente em `/apps`
   1. Crie a propriedade `sling:hideChildren`:

      * tipo: `String[]`
      * valor: uma lista dos nós secundários (conforme definido em `/libs`) para ocultar/ignorar

      O curinga &amp;ast; pode ser usado para ocultar/ignorar todos os nós filhos.


* **Reordenar nós**

   O nó e seus irmãos são definidos em `/libs`. Uma nova posição é necessária para que o nó seja recriado na sobreposição/sobreposição `/apps`, onde a nova posição é definida em referência ao nó irmão apropriado em `/libs`.

   * Use a propriedade `sling:orderBefore`:

      1. Crie o nó correspondente em `/apps`
      1. Crie a propriedade `sling:orderBefore`:

         Isso especifica o nó (como em `/libs`) que o nó atual deve ser posicionado antes de:

         * tipo: `String`
         * valor: `<before-SiblingName>`

### Chamando a Fusão de Recursos do Sling do seu código {#invoking-the-sling-resource-merger-from-your-code}

A Sling Resource Merger inclui dois provedores de recursos personalizados - um para sobreposições e outro para substituições. Cada um desses pode ser chamado em seu código usando um ponto de montagem:

>[!NOTE]
>
>Ao acessar o recurso, é recomendável usar o ponto de montagem apropriado.
>
>Isso garante que o Sling Resource Merger seja chamado e o recurso totalmente mesclado seja retornado (reduzindo a estrutura que precisa ser replicada de `/libs`).

* Sobreposição:

   * finalidade: mesclar recursos com base em seu caminho de pesquisa
   * ponto de montagem: `/mnt/overlay`
   * usage: `mount point + relative path`
   * exemplo:

      * `getResource('/mnt/overlay' + '<relative-path-to-resource>');`

* Substituir:

   * finalidade: mesclar recursos com base em seu super tipo
   * ponto de montagem: `/mnt/overide`
   * uso: `mount point + absolute path`
   * exemplo:

      * `getResource('/mnt/override' + '<absolute-path-to-resource>');`

