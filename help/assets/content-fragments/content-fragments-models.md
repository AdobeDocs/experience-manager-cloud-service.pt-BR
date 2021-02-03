---
title: Modelos de fragmentos do conteúdo
description: Modelos de fragmento de conteúdo são usados para criar fragmentos de conteúdo com conteúdo estruturado.
translation-type: tm+mt
source-git-commit: 3538c03a6a455cd22423ca5a4fd69c1fe57b3e5e
workflow-type: tm+mt
source-wordcount: '2156'
ht-degree: 7%

---


# Modelos de fragmentos do conteúdo {#content-fragment-models}

Os Modelos de fragmento de conteúdo definem a estrutura do conteúdo para seus [fragmentos de conteúdo](/help/assets/content-fragments/content-fragments.md).

Para usar os Modelos de fragmento de conteúdo, faça o seguinte:

1. [Ativar a funcionalidade do Modelo de fragmento de conteúdo para sua instância](/help/assets/content-fragments/content-fragments-configuration-browser.md)
1. [Crie](#creating-a-content-fragment-model) e  [configure](#defining-your-content-fragment-model) seus Modelos de fragmento de conteúdo
1. [Ative seus ](#enabling-disabling-a-content-fragment-model) Modelos de fragmento de conteúdo para uso ao criar Fragmentos de conteúdo para uso ao criar Fragmentos de conteúdo
1. [Permita seus Modelos de fragmento de conteúdo nas ](#allowing-content-fragment-models-assets-folder) pastas de Ativos necessárias, configurando  **Políticas**.

## Criação de um modelo de fragmento de conteúdo {#creating-a-content-fragment-model}

1. Navegue até **Ferramentas**, **Ativos** e abra **Modelos de fragmento de conteúdo**.
1. Navegue até a pasta apropriada para sua [configuração](/help/assets/content-fragments/content-fragments-configuration-browser.md).
1. Use **Criar** para abrir o assistente.

   >[!CAUTION]
   >
   >Se o [uso de modelos de fragmento de conteúdo não tiver sido ativado](/help/assets/content-fragments/content-fragments-configuration-browser.md), a opção **Criar** não estará disponível.

1. Especifique o **título do modelo**. Você também pode adicionar **Tags**, uma **Descrição** e selecionar **Ativar modelo** para [ativar o modelo](#enabling-disabling-a-content-fragment-model), se necessário.

   ![título e descrição](assets/cfm-models-02.png)

1. Use **Create** para salvar o modelo vazio. Uma mensagem indicará o sucesso da ação. Você pode selecionar **Abrir** para editar imediatamente o modelo ou **Concluído** para retornar ao console.

## Definição do modelo de fragmento de conteúdo {#defining-your-content-fragment-model}

O modelo de fragmento de conteúdo define efetivamente a estrutura dos fragmentos de conteúdo resultantes usando uma seleção de **[Tipos de dados](#data-types)**. Usando o editor de modelo, você pode adicionar instâncias dos tipos de dados e configurá-las para criar os campos necessários:

>[!CAUTION]
>
>Editar um modelo de fragmento de conteúdo existente pode afetar fragmentos dependentes.

1. Navegue até **Ferramentas**, **Ativos** e abra **Modelos de fragmento de conteúdo**.

1. Navegue até a pasta que contém o modelo de fragmento do conteúdo.
1. Abra o modelo necessário para **Editar**; use a ação rápida ou selecione o modelo e a ação na barra de ferramentas.

   Depois de abrir o editor de modelo, é mostrado:

   * esquerda: campos já definidos
   * direito: **Tipos de dados** disponíveis para criar campos (e **Propriedades** para uso depois que os campos forem criados)

   >[!NOTE]
   >
   >Quando um campo é **Obrigatório**, o **Rótulo** indicado no painel à esquerda é marcado com um asterisco (*****).

   ![propriedades](assets/cfm-models-03.png)

1. **Para adicionar um campo**

   * Arraste um tipo de dados necessário para o local necessário para um campo:

      ![tipo de dados para campo](assets/cfm-models-04.png)

   * Depois que um campo for adicionado ao modelo, o painel direito mostrará as **Propriedades** que podem ser definidas para esse tipo de dados específico. Aqui você pode definir o que é necessário para esse campo.

      * Muitas propriedades são autoexplicativas, para obter detalhes adicionais, consulte [Propriedades](#properties).
      * Digitar um **Rótulo de campo** preencherá automaticamente o **Nome da propriedade** - se estiver vazio, e poderá ser atualizado manualmente posteriormente.

      Por exemplo:

      ![propriedades do campo](assets/cfm-models-05.png)


1. **Como remover um campo**

   Selecione o campo desejado e clique/toque no ícone lixeira. Você receberá uma solicitação para confirmar a ação.

   ![remover](assets/cfm-models-06.png)

1. Adicione todos os campos obrigatórios e defina as propriedades relacionadas, conforme necessário. Por exemplo:

   ![save](assets/cfm-models-07.png)

1. Selecione **Salvar** para persistir na definição.

## Tipos de dados {#data-types}

Uma seleção de tipos de dados está disponível para definir seu modelo:

* **Texto em linha única**
   * Adicione um ou mais campos de uma única linha de texto; o comprimento máximo pode ser definido
* **Texto multilinha**
   * Uma área de texto que pode ser Rich Text, Plain Text ou Markdown
* **Número**
   * Adicionar um ou mais campos numéricos
* **Booleano**
   * Adicionar uma caixa de seleção booleana
* **Data e hora**
   * Adicionar uma data e/ou hora
* **Enumeração**
   * Adicionar um conjunto de caixas de seleção, botões de opção ou campos suspensos
* **Tags**
   * Permite que os autores de fragmentos acessem e selecionem áreas de tags
* **Referência de conteúdo**
   * Referências a outros conteúdos, de qualquer tipo; pode ser usado para [criar conteúdo aninhado](#using-references-to-form-nested-content)
* **Referência do fragmento**
   * Refere outros fragmentos de conteúdo; pode ser usado para [criar conteúdo aninhado](#using-references-to-form-nested-content)
   * O tipo de dados pode ser configurado para permitir que os autores de fragmentos:
      * Edite o fragmento referenciado diretamente.
      * Criar um novo fragmento de conteúdo, com base no modelo apropriado
* **Objeto JSON**
   * Permite que o autor do fragmento de conteúdo insira a sintaxe JSON nos elementos correspondentes de um fragmento.
      * Para permitir que AEM armazene JSON direto que você tenha copiado/colado de outro serviço.
      * O JSON será transmitido e sairá como JSON no GraphQL.
      * Inclui o realce da sintaxe JSON, o preenchimento automático e o realce de erros no editor de fragmentos de conteúdo.

## Propriedades {#properties}

Muitas propriedades são autoexplicativas, para certas propriedades, mais detalhes são os seguintes:

* **Renderizar**
comoAs várias opções para realizar/renderizar o campo em um fragmento. Geralmente, isso permite definir se o autor verá uma única instância do campo ou poderá criar várias instâncias.

* **Rótulo**
do campoInserir um 
**O** Rótulo de campo gerará automaticamente um Nome **de** propriedade, que pode ser atualizado manualmente se necessário.

* **A validação**
ValidationBasic está disponível por mecanismos como a propriedade  **** Requirements. Alguns tipos de dados têm campos de validação de adição. Consulte [Validação](#validation) para obter mais detalhes.

* No tipo de dados **Texto de várias linhas**, é possível definir o **Tipo padrão** como:

   * **Texto formatado**
   * **Markdown**
   * **Texto sem formatação**

   Se não for especificado, o valor padrão **Rich Text** será usado para esse campo.

   Alterar o **Tipo padrão** em um modelo de fragmento de conteúdo só terá efeito em um fragmento de conteúdo existente relacionado depois que esse fragmento for aberto no editor e salvo.

* **O**
UniqueContent (para o campo específico) deve ser exclusivo em todos os fragmentos de conteúdo criados a partir do modelo atual.

   Isso é usado para garantir que os autores de conteúdo não possam repetir o conteúdo já adicionado em outro fragmento do mesmo modelo.

   Por exemplo, um campo **Texto de linha única** chamado `Country` no Modelo de fragmento de conteúdo não pode ter o valor `Japan` em dois Fragmentos de conteúdo dependentes. Um aviso será emitido quando a segunda instância for tentada.

   >[!NOTE]
   A exclusividade é garantida por raiz linguística.

   >[!NOTE]
   As variações podem ter o mesmo valor *exclusivo* que as variações do mesmo fragmento, mas não o mesmo valor que o usado em qualquer variação de outros fragmentos.

* ****
TraduzívelMarcar a caixa de seleção &quot;Traduzível&quot; em um campo no editor de modelo CF

   * Verifique se o nome da propriedade do campo foi adicionado na configuração de conversão, context `/content/dam/<tenant>`, se ainda não estiver presente.
   * Para GraphQL: defina uma propriedade `<translatable>` no campo Fragmento de conteúdo como `yes`, para permitir o filtro de query GraphQL para saída JSON com apenas conteúdo traduzível.

* Consulte **[Referência do fragmento (Fragmentos aninhados)](#fragment-reference-nested-fragments)** para obter mais detalhes sobre esse tipo de dados específico e suas propriedades.

## Validação {#validation}

Vários tipos de dados agora incluem a possibilidade de definir requisitos de validação para quando o conteúdo é inserido no fragmento resultante:

* **Texto em linha única**
   * Compare com um regex predefinido.
* **Número**
   * Verifique valores específicos.
* **Referência de conteúdo**
   * Teste tipos específicos de conteúdo.
   * Somente ativos com tamanho de arquivo especificado ou menor podem ser referenciados.
   * Somente as imagens em um intervalo predefinido de largura e/ou altura (em pixels) podem ser referenciadas.
* **Referência do fragmento**
   * Teste um modelo de fragmento de conteúdo específico.

<!--
  * Only predefined file types can be referenced.
  * No more than the predefined number of assets can be referenced. 
  * No more than the predefined number of fragments can be referenced.
-->

## Usando referências para formar Conteúdo aninhado {#using-references-to-form-nested-content}

Fragmentos de conteúdo podem formar conteúdo aninhado, usando um dos seguintes tipos de dados:

* **[Referência de conteúdo](#content-reference)**
   * Fornece uma referência simples a outro conteúdo; de qualquer tipo.
   * Pode ser configurado para uma ou várias referências (no fragmento resultante).

* **[Referência](#fragment-reference-nested-fragments)**  de fragmento (fragmentos aninhados)
   * Faz referência a outros fragmentos, dependendo dos modelos específicos especificados.
   * Permite incluir/recuperar dados estruturados.

      >[!NOTE]
      Este método é de especial interesse em conjunto com [Delivery de conteúdo sem cabeçalho usando Fragmentos de conteúdo com GraphQL](/help/assets/content-fragments/content-fragments-graphql.md).
   * Pode ser configurado para uma ou várias referências (no fragmento resultante).

>[!NOTE]
AEM tem uma proteção de recorrência para:
* Referências de conteúdo
Isso impede que o usuário adicione uma referência ao fragmento atual. Isso pode levar a uma caixa de diálogo vazia do seletor de Referência de fragmento.

* Referências de fragmento no GraphQL
Se você criar um query profundo que retorna vários Fragmentos de conteúdo referenciados entre si, ele retornará null na primeira ocorrência.


### Referência de conteúdo {#content-reference}

A Referência de conteúdo permite renderizar o conteúdo de outra fonte; por exemplo, imagem ou fragmento de conteúdo.

Além das propriedades padrão, você pode especificar:

* O **Caminho raiz** para qualquer conteúdo referenciado.
* Os tipos de conteúdo que podem ser referenciados.
* Limitações para tamanhos de arquivo.
* Restrições de imagem.
   <!-- Check screenshot - might need update -->
   ![Referência de conteúdo](assets/cfm-content-reference.png)

### Referência do fragmento (fragmentos aninhados) {#fragment-reference-nested-fragments}

A Referência do fragmento faz referência a um ou mais fragmentos de conteúdo. Esse recurso de especial interesse ao recuperar conteúdo para uso no aplicativo, pois permite recuperar dados estruturados com várias camadas.

Por exemplo:

* Um modelo que define detalhes para um funcionário; eles incluem:
   * Uma referência ao modelo que define o empregador (empresa)

```xml
type EmployeeModel {
    name: String
    firstName: String
    company: CompanyModel
}

type CompanyModel {
    name: String
    street: String
    city: String
}
```

>[!NOTE]
Isso é de especial interesse em conjunto com [Delivery de conteúdo sem cabeçalho usando Fragmentos de conteúdo com GraphQL](/help/assets/content-fragments/content-fragments-graphql.md).

Além das propriedades padrão, você pode definir:

* **Renderizar como**:

   * **vários campos**  - o autor do fragmento pode criar várias referências, individuais

   * **referência**  de fragmento - permite que o autor do fragmento selecione uma única referência para um fragmento

* **Modelo**
TipoVários modelos podem ser selecionados. Ao criar o Fragmento de conteúdo, qualquer fragmento referenciado deve ter sido criado usando esses modelos.

* **Caminho**
raizEspecifica um caminho raiz para qualquer fragmento referenciado.

* **Permitir criação de fragmentos**

   Isso permitirá que o autor do fragmento crie um novo fragmento com base no modelo apropriado.

   * **fragmentreferencecomposite**  - permite que o autor do fragmento crie um composto, selecionando vários fragmentos

   <!-- Check screenshot - might need update -->
   ![Referência do fragmento](assets/cfm-fragment-reference.png)

>[!NOTE]
Existe um mecanismo de proteção contra recorrências. Ela proíbe que o usuário selecione o Fragmento de conteúdo atual na Referência do fragmento. Isso pode levar a uma caixa de diálogo vazia do seletor de Referência de fragmento.
Também há uma proteção de recorrência para Referências de fragmento no GraphQL. Se você criar um query profundo em dois Fragmentos de conteúdo que fazem referência uns aos outros, ele retornará um valor nulo.

## Ativar ou desativar um modelo de fragmento de conteúdo {#enabling-disabling-a-content-fragment-model}

Para ter total controle sobre o uso dos Modelos de fragmento de conteúdo, eles têm um status que pode ser definido.

### Habilitar um modelo de fragmento de conteúdo {#enabling-a-content-fragment-model}

Depois que um modelo é criado, ele precisa ser habilitado para que:

* Está disponível para seleção ao criar um novo Fragmento de conteúdo.
* Pode ser referenciado em um Modelo de fragmento de conteúdo.
* Está disponível para GraphQL; então o schema é gerado.

Para habilitar um Modelo sinalizado como:

* **Rascunho** : mew (nunca ativado).
* **Desativado** : foi especificamente desativado.

Use a opção **Ativar** de:

* A barra de ferramentas superior, quando o Modelo necessário for selecionado.
* A Ação rápida correspondente (passe o mouse sobre o Modelo necessário).

![Ativar um rascunho ou modelo desativado](assets/cfm-status-enable.png)

### Desabilitando um Modelo de Fragmento de Conteúdo {#disabling-a-content-fragment-model}

Um modelo também pode ser desativado para que:

* O modelo não está mais disponível como base para a criação de *novos* Fragmentos de conteúdo.
* No entanto:
   * O schema GraphQL continua sendo gerado e ainda pode ser consultado (para evitar o impacto da API JSON).
   * Todos os Fragmentos de conteúdo baseados no modelo ainda podem ser consultados e retornados do ponto de extremidade GraphQL.
* O modelo não pode mais ser referenciado, mas as referências existentes são mantidas intocadas e ainda podem ser consultadas e retornadas do ponto final GraphQL.

Para desativar um Modelo sinalizado como **Ativado**, use a opção **Desativar** de:

* A barra de ferramentas superior, quando o Modelo necessário for selecionado.
* A Ação rápida correspondente (passe o mouse sobre o Modelo necessário).

![Desativar um modelo ativado](assets/cfm-status-disable.png)

## Permitir modelos de fragmento de conteúdo na pasta Ativos {#allowing-content-fragment-models-assets-folder}

Para implementar o gerenciamento de conteúdo, você pode configurar **Policies** na pasta Assets para controlar quais modelos de fragmento de conteúdo são permitidos para a criação de fragmentos nessa pasta.

>[!NOTE]
O mecanismo é semelhante a [permitir modelos de página](/help/sites-cloud/authoring/features/templates.md#allowing-a-template-author) para uma página, e seus filhos, em propriedades avançadas de uma página.

Para configurar **Policies** para **Modelos de fragmento de conteúdo permitidos**:

1. Navegue e abra **Propriedades** para a pasta Ativos necessária.

1. Abra a guia **Policies**, onde você pode configurar:

   * **Herdado de`<folder>`**

      As políticas são automaticamente herdadas ao criar novas pastas secundárias; a política pode ser reconfigurada (e a herança quebrada) se as subpastas precisarem permitir modelos diferentes da pasta pai.

   * **Modelos de fragmento de conteúdo permitidos por caminho**

      Vários modelos podem ser permitidos.

   * **Modelos de fragmento de conteúdo permitidos por tag**

      Vários modelos podem ser permitidos.
   ![Política do modelo de fragmento de conteúdo](assets/cfm-model-policy-assets-folder.png)

1. **** Salve as alterações.

Os Modelos de fragmento de conteúdo permitidos para uma pasta são resolvidos da seguinte forma:
* As **Políticas** para **Modelos de fragmento de conteúdo permitidos**.
* Se estiver vazio, tente determinar a política usando as regras de herança.
* Se a cadeia de herança não fornecer um resultado, verifique a configuração **Cloud Services** dessa pasta (também primeiro diretamente e depois por herança).
* Se nenhuma das opções acima apresentar resultados, não haverá modelos permitidos para essa pasta.

## Excluindo um modelo de fragmento de conteúdo {#deleting-a-content-fragment-model}

>[!CAUTION]
A exclusão de um modelo de fragmento de conteúdo pode afetar fragmentos dependentes.

Para excluir um modelo de fragmento de conteúdo:

1. Navegue até **Ferramentas**, **Ativos** e abra **Modelos de fragmento de conteúdo**.

1. Navegue até a pasta que contém o modelo de fragmento do conteúdo.
1. Selecione seu modelo, seguido por **Excluir** na barra de ferramentas.

   >[!NOTE]
   Se o modelo for referenciado, um aviso será dado. Agir adequadamente.

## Publicar um modelo de fragmento de conteúdo {#publishing-a-content-fragment-model}

Os modelos de fragmento de conteúdo precisam ser publicados quando/antes que qualquer fragmento de conteúdo dependente seja publicado.

Para publicar um modelo de fragmento de conteúdo:

1. Navegue até **Ferramentas**, **Ativos** e abra **Modelos de fragmento de conteúdo**.

1. Navegue até a pasta que contém o modelo de fragmento do conteúdo.
1. Selecione seu modelo, seguido por **Publicar** na barra de ferramentas.
O status publicado será indicado no console.

   >[!NOTE]
   Se você publicar um fragmento de conteúdo para o qual o modelo ainda não foi publicado, uma lista de seleção indicará isso e o modelo será publicado com o fragmento.

## Cancelamento de publicação de um modelo de fragmento de conteúdo {#unpublishing-a-content-fragment-model}

Os modelos de fragmento de conteúdo podem ser despublicados se não forem referenciados por nenhum fragmento.

Para cancelar a publicação de um modelo de fragmento de conteúdo:

1. Navegue até **Ferramentas**, **Ativos** e abra **Modelos de fragmento de conteúdo**.

1. Navegue até a pasta que contém o modelo de fragmento do conteúdo.
1. Selecione seu modelo, seguido por **Cancelar a publicação** na barra de ferramentas.
O status publicado será indicado no console.
