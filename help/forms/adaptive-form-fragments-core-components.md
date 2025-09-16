---
title: O que são fragmentos de formulário adaptável?
description: O Adaptive Forms fornece um mecanismo para criar um segmento de formulário, como um painel ou um grupo de campos, como usá-lo em qualquer Formulário adaptável. Também é possível salvar um painel existente como fragmento.
topic-tags: author
keywords: Adicionar fragmentos de formulário adaptável, Fragmentos de formulário adaptável, Criar um fragmento de formulário, Adicionar um fragmento a um formulário adaptável, Gerenciar fragmentos
feature: Adaptive Forms, Core Components
exl-id: 3a9ad1b7-2f6f-4ca9-a1c9-549c4238c59e
role: User, Developer
source-git-commit: ab84a96d0e206395063442457a61f274ad9bed23
workflow-type: tm+mt
source-wordcount: '1479'
ht-degree: 3%

---

# Criar e usar fragmentos adaptáveis do Forms em um formulário adaptável com base nos Componentes principais {#adaptive-form-fragments}


| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service (Componentes principais) | Este artigo |
| AEM as a Cloud Service (Componentes de base) | [Clique aqui](/help/forms/adaptive-form-fragments.md) |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/adaptive-form-fragments.html) |

Embora cada formulário seja projetado para um propósito específico, há alguns segmentos comuns na maioria dos formulários, como o de fornecer detalhes pessoais, como nome e endereço, detalhes familiares e detalhes de renda. Os desenvolvedores de formulários são necessários para criar esses segmentos comuns sempre que um novo formulário for criado.

O Forms adaptável fornece um mecanismo conveniente para criar segmentos de formulário, como um painel ou um grupo de campos, somente uma vez e reutilizá-los no Forms adaptável. Esses segmentos reutilizáveis e independentes são chamados de fragmentos de formulário adaptável.

Os fragmentos de formulário se integram perfeitamente em vários formulários, simplificando a criação de formulários consistentes e com aparência profissional. Os fragmentos de formulário garantem a reutilização, a padronização e a consistência da marca por meio da funcionalidade &quot;alterar uma vez e refletir em todos os lugares&quot;. Experimente maior capacidade de manutenção e eficiência, já que as atualizações feitas em um local são propagadas automaticamente em todos os formulários que utilizam esses fragmentos.

Você pode adicionar um fragmento várias vezes a um documento e usar as propriedades de vinculação de dados de seus componentes para vinculá-lo a diferentes fontes de dados ou esquemas. Por exemplo, você pode usar o mesmo fragmento de endereço para os endereços permanente, para contato e de faturamento, e conectá-lo a diferentes campos de uma fonte de dados ou esquema.

>[!NOTE]
>
> Você pode personalizar facilmente a experiência do fragmento para usuários com a [Caixa de diálogo de Configuração e Caixa de diálogo de Design do componente de Fragmento de Formulário](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/adaptive-form-fragment).

## Criar um fragmento de formulário adaptável {#create-a-fragment}

Você pode criar um fragmento de formulário adaptável do zero ou salvar um painel em um formulário adaptável existente como fragmento. Para criar um fragmento de formulário:

1. Faça logon na instância do AEM Forms em https://[*hostname*]:[*port*]/aem/forms.html.
1. Clique em **Criar > Fragmento de formulário adaptável**.

   ![Criar fragmento de formulário adaptável](/help/forms/assets/adaptive-form-fragment.png)

1. Especifique título, nome, descrição e tags para o fragmento. Certifique-se de especificar um nome exclusivo para o fragmento. Se outro fragmento existir com o mesmo nome, o fragmento não será criado.
1. Selecione um modelo de formulário. Você pode criar um fragmento de formulário para Componentes principais com base no Forms adaptável ou Componentes de base com base no Forms adaptável. Para criar fragmento de formulário para formulários baseados em Componentes principais, selecione um modelo baseado em Componentes principais.

   Ao criar fragmento de formulário para formulários baseados em Componentes principais, use a opção Selecionar tema do formulário para selecionar um tema baseado em Componentes principais.

1. Clique para abrir a guia **Modelo de formulário** e, no menu suspenso **Selecionar de**, selecione um dos seguintes modelos para o fragmento:

   ![Exibe o tipo de modelo na guia Modelo de Formulário](assets/create-af-1-1.png)

   * **Nenhum**: especifica criar o fragmento do zero sem usar nenhum modelo de formulário.

     >[!NOTE]
     >
     > No Forms adaptável, é possível usar um único fragmento de formulário (com base nos Componentes principais) várias vezes. Ele oferece suporte a fragmentos de formulário baseados em nenhum e em esquema.

   * **Esquema**: especifica a criação do fragmento usando um esquema XML ou JSON carregado para o AEM Forms. Você pode fazer upload ou selecionar dentre os esquemas XML ou JSON disponíveis como o modelo de formulário do fragmento. Ao selecionar um esquema XML, você também pode criar um fragmento de Formulário adaptável selecionando um complexType presente no esquema selecionado na caixa suspensa **[!UICONTROL Tipo complexo de esquema XML]**. Ao selecionar um esquema JSON, você também pode criar um fragmento de Formulário adaptável selecionando uma definição de esquema presente no esquema selecionado na caixa suspensa **[!UICONTROL Definições de esquema JSON]**.
   * **Modelo de dados de formulário**: especifica a criação do fragmento usando um modelo de dados de formulário (FDM). Você pode criar um fragmento de Formulário adaptável com base em apenas um objeto de modelo de dados em um modelo de dados de formulário (FDM). Expanda a lista suspensa Definições do Modelo de dados de formulário (FDM). Ela lista todos os objetos do modelo de dados no modelo de dados de formulário (FDM) especificado. Selecione um objeto de modelo de dados na lista.

   ![Modelo de dados de formulário (FDM)](assets/create-af-3.png)

1. Clique em **Criar** e em **Abrir** para abrir o fragmento, com um modelo padrão, no modo de edição. No modo de edição, é possível adicionar qualquer componente de Formulário adaptável ao fragmento.

<!-- For information about Adaptive Form components, see [Introduction to authoring Adaptive Forms](../../forms/using/introduction-forms-authoring.md). --> Além disso, se você selecionou um esquema XML como o modelo de formulário do fragmento, uma nova guia que exibe a hierarquia de modelo de formulário é exibida no localizador de conteúdo. Ela permite arrastar e soltar elementos do modelo de formulário no fragmento. <!--The added form-model elements get converted into form components while retaining the original properties from the associated XDP or XSD. -->

Depois que o fragmento do Formulário adaptável com base em um esquema ou modelo de dados de formulário (FDM) é criado, o modelo de dados de formulário (FDM) ou os elementos do esquema aparecem na guia Fontes de dados do navegador de conteúdo no Criador de formulários adaptáveis. Você pode arrastar e soltar elementos do modelo de formulário no fragmento. Os elementos de modelo de formulário adicionados são convertidos em componentes de formulário, ao mesmo tempo em que retêm as propriedades originais do esquema associado.


## Adicionar um fragmento a um Formulário adaptável {#insert-a-fragment-in-an-adaptive-form}

Para adicionar um fragmento de formulário adaptável a um formulário adaptável:

1. Abra o Formulário adaptável no modo de edição.
1. Adicione o componente **Fragmento de formulário adaptável** ao formulário.
1. Abra a caixa de diálogo Configuração do componente **Fragmento de formulário adaptável**.
1. Selecione a **Referência do fragmento** na guia **Básico**. Todos os fragmentos do Forms adaptável disponíveis para o formulário, dependendo do modelo do formulário, são exibidos.

1. Selecione um fragmento de formulário adaptável no componente **Fragmento de formulário adaptável** no formulário adaptável.

   ![selecione a opção Fragmentos de formulário adaptável](/help/forms/assets/adaptive-form-fragment-basic.png)

<!-- 
   >[!NOTE]
   >
   >The Adaptive Form fragment is not enabled for authoring from within the Adaptive Form. Moreover, you cannot use an XSD-based fragment in a JSON-based Adaptive Form and the opposite way. 
-->

O fragmento de Formulário adaptável é adicionado por referência ao Formulário adaptável e permanece em sincronia com o fragmento de Formulário adaptável independente. Isso implica que quaisquer modificações feitas no fragmento do Formulário adaptável sejam espelhadas em todas as instâncias em que o fragmento é incorporado no Adaptive Forms.

<!--### Embed a fragment in Adaptive Form {#embed-a-fragment-in-adaptive-form}

You can choose to embed an Adaptive Form fragment in an Adaptive Form by clicking the ![Embed](assets/Smock_Import_18_N.svg) icon the panel toolbar of the added fragment

The embedded fragment is no longer linked with the standalone fragment. You can edit the components in the embedded fragment from within the Adaptive Form.-->

<!-- 
## Configure fragment appearance {#configure-fragment-appearance}

Any fragment you insert in Adaptive Forms appears as a placeholder image. The placeholder displays titles of up to a maximum of ten child panels in the fragment. You can configure AEM Forms to show the complete fragment instead of the placeholder image.

Perform the following steps to show complete fragments in forms:

1. Go to AEM web console configuration page at https:[*host*]:[*port*]/system/console/configMgr.

1. Search and click **[!UICONTROL Adaptive Form and Interactive Communication Web Channel Configuration]** to open it in edit mode.
1. Disable **[!UICONTROL Enable Placeholder in place of Fragment]** checkbox to show complete fragments rather than the placeholder image.

-->

### Uso de fragmentos dentro de fragmentos {#using-fragments-within-fragments}

É possível criar fragmentos de formulário adaptável aninhados, o que significa que você pode adicionar um fragmento em outro fragmento e ter uma estrutura de fragmento aninhada.

### Uso de um fragmento de formulário várias vezes em um Formulário adaptável {#using-form-fragment-mutiple-times-in-af}

Você pode usar um fragmento de formulário com base em nenhum e em esquema várias vezes em um Formulário adaptável para salvar dados de forma exclusiva para cada campo de fragmentos de formulário. Por exemplo, você pode usar um fragmento de formulário de endereço para coletar detalhes de endereço para endereços permanentes, de comunicação e vivos presentes em um formulário de aplicativo de empréstimo.

![usando vários fragmentos no formulário adaptável](/help/forms/assets/using-multiple-fragment-af.gif)

## Suporte ao mapeamento automático para fragmentos em um Formulário adaptável

Ao criar um fragmento de formulário adaptável com base em uma definição de esquema JSON, ele pode ser reutilizado automaticamente em formulários criados a partir do mesmo esquema.
Se você arrastar e soltar um objeto de esquema ou qualquer objeto aninhado que corresponda ao mapeamento de definição de esquema JSON de um fragmento de formulário adaptável, o objeto será substituído pelo fragmento de formulário adaptável correspondente. Em vez de adicionar um painel com campos individuais, o formulário insere o fragmento de formulário adaptável mapeado.

![Arrastar e soltar um fragmento](/help/forms/assets/fragment.png)

Você também pode arrastar e soltar um fragmento de formulário adaptável vinculado da biblioteca de fragmentos de formulário adaptável no localizador de conteúdo do AEM e fornecer a referência de vinculação correta na caixa de diálogo Editar componente do painel de fragmentos do formulário adaptável.

## Gerenciar fragmentos {#manage-fragments}

É possível executar várias operações em fragmentos de formulário adaptável usando a interface do usuário do AEM Forms.

1. Acesse `https://[hostname]/aem/forms.html`.

1. Clique em **Selecionar** na barra de ferramentas da interface do usuário do AEM Forms e selecione um Fragmento de formulário adaptável. A barra de ferramentas exibe as seguintes operações que você pode executar no fragmento de Formulário adaptável selecionado.

<table>
 <tbody>
  <tr>
   <td><p><strong>Operação</strong></p> </td>
   <td><p><strong>Descrição</strong></p> </td>
  </tr>
  <tr>
   <td><p>Editar</p> </td>
   <td><p>Abre o fragmento de formulário adaptável selecionado no modo de edição.<br /> <br /> </p> </td>
  </tr>
   <tr>
   <td><p>Visualização</p> </td>
   <td><p>Fornece opções para visualizar o fragmento como uma HTML ou uma visualização personalizada mesclando dados de um arquivo XML com o fragmento. Para obter mais informações, consulte <a>Visualizando um formulário</a>.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Download</p> </td>
   <td><p>Baixa o fragmento selecionado.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Iniciar revisão/Gerenciar revisão</p> </td>
   <td><p>Permite iniciar e gerenciar uma revisão do fragmento selecionado. Para obter mais informações, consulte <a>Criação e gerenciamento de análises</a>.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Adicionar Dicionário</p> </td>
   <td><p>Gera um dicionário para localizar o fragmento selecionado. Para obter mais informações, consulte <a>Localizando Forms Adaptável</a>.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Publicar/Desfazer publicação</p> </td>
   <td><p>Publica/cancela a publicação do fragmento selecionado.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Excluir</p> </td>
   <td><p>Exclui o fragmento selecionado.<br /> <br /> </p> </td>
  </tr>
 </tbody>
</table>

## Pontos principais a serem lembrados ao trabalhar com fragmentos {#key-points-to-remember-when-working-with-fragments}

* Certifique-se de que o nome do fragmento seja exclusivo. O fragmento não é criado se houver um fragmento existente com o mesmo nome.
* Qualquer expressão, script ou estilo em um fragmento de Formulário adaptável independente é retido quando inserido por referência ou incorporado em um Formulário adaptável.
* Não é possível editar um fragmento de Formulário adaptável, que é inserido por referência, de um Formulário adaptável. Para editar, modifique o fragmento independente do Formulário adaptável.
* Ao publicar um Formulário adaptável, você precisa publicar os fragmentos independentes do Formulário adaptável inseridos por referência no Formulário adaptável.
* Ao republicar um fragmento de Formulário adaptável atualizado, as alterações são refletidas nas instâncias publicadas do Formulário adaptável em que o fragmento é usado.
* O formulário adaptável que contém o componente Verificar não é compatível com usuários anônimos. Além disso, não é recomendado usar o componente Verificar em um fragmento de Formulário adaptável.

## Fragmentos de referência {#reference-fragments}

Os fragmentos de formulário adaptável de referência que você pode usar para criar seu formulário estão disponíveis.
<!-- For more information, see [Reference Fragments](../../forms/using/reference-adaptive-form-fragments.md). -->



## Consulte também {#see-also}

{{see-also}}
