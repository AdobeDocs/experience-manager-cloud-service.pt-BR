---
title: Como criar painéis repetíveis nos Componentes principais do formulário adaptável?
description: Saiba como criar seções ou campos repetíveis em um Formulário adaptável.
role: Architect, Developer, Admin, User
exl-id: 02521bf3-83c1-40a0-8fe6-23af240727e9
source-git-commit: d0e5a63896ccbeb32b565680276b461fbbf19e9c
workflow-type: tm+mt
source-wordcount: '1390'
ht-degree: 6%

---

# Criar formulários com seções repetíveis (Componentes principais) {#repeat-panel}


| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/creating-forms-repeatable-sections.html?lang=en) |
| AEM as a Cloud Service | Este artigo |

Uma seção repetível se refere a uma parte de um formulário que pode ser duplicada ou repetida várias vezes para coletar informações de várias instâncias dos mesmos dados.

Por exemplo, considere um formulário usado para coletar informações sobre a experiência profissional de uma pessoa. Você pode ter uma seção repetível para capturar detalhes de cada tarefa anterior. A seção repetível normalmente contém campos como nome da empresa, título do cargo, datas de emprego e responsabilidades do cargo. O usuário pode adicionar várias instâncias da seção repetível para inserir informações sobre cada cargo que manteve.

![Repetibilidade](/help/forms/assets/repeatable-adaptive-form-example.gif)

No final deste artigo, você aprenderá a:

* Criar uma seção repetível em um Formulário adaptável
* Definir o número mínimo ou máximo de repetições para um componente de Formulário adaptável
* Usar o editor de regras para configurar ações de adição ou exclusão para seções repetíveis

Você pode usar o [Painel](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel-container.html?lang=pt-br), [Acordeão](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion.html?lang=pt-BR), [Guias Horizontais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/horizontal-tabs.html?lang=pt-br)ou [Assistente](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard.html?lang=pt-br) componentes para tornar as seções de um Formulário adaptável repetíveis. Você pode adicionar componentes filhos aos componentes painel, acordeão, guias horizontais ou assistente para criar seção repetível em um formulário.


Os exemplos neste documento são baseados no [Painel](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel-container.html?lang=pt-br) componente. Você pode executar as etapas idênticas para tornar o [Acordeão](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion.html?lang=pt-BR), [Guias horizontais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/horizontal-tabs.html?lang=pt-br), e [Assistente](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard.html?lang=pt-br) componentes repetíveis.

## Adicionar ou excluir seções que podem ser repetidas em um formulário {#add-or-delete-repeatable-section-in-panel-container}

Para repetir um painel no formulário ou remover painéis repetíveis, um autor de formulário usa um componente de botão para adicionar ou remover uma ocorrência do painel. Para adicionar ou excluir seções (painéis) repetíveis em um formulário:

* [Tornar o contêiner do painel repetível](#make-panel-container-repeatable)
* [Adicionar seção repetível](#add-repeatable-section-using-instance-manager-via-scripts)
* [Excluir seções que podem ser repetidas](#delete-repeatable-section-using-instance-manager-via-scripts)

### Tornar o contêiner do painel repetível {#make-panel-container-repeatable}

![Guia Acessibilidade](/help/forms/assets/repeat-panel.png)

Para tornar um painel repetível, execute as seguintes etapas:
1. Selecione um contêiner do painel e toque em ![cmppr](/help/forms/assets/cmppr.png).
1. Clique em **repetir painel** e alterne para **tornar o painel repetível**.
1. Definir **mínimo de repetições** conforme necessário para seções mínimas repetíveis, é possível definir **mínimo de repetições** a zero para a não repetição de painéis ou para remover os painéis repetidos. Por padrão, o valor de repetição mínima é zero.
1. Definir **máximo de repetições** para repetir o número de vezes necessário no painel, por padrão, o valor é infinito.

   >[!NOTE]
   >
   > 
   > * A repetição mínima não pode ser um valor -ve.
   > * Para criar um painel não repetível, defina o valor dos campos máximo e mínimo como um.

### Adicionar seção repetível usando o gerenciador de instâncias (por meio de scripts) {#add-repeatable-section-using-instance-manager-via-scripts}

O pai do painel que deve ser repetido deve conter um botão adicionar para gerenciar a ocorrência repetida do painel. Execute as seguintes etapas para inserir botões no pai e ativar scripts nos botões:

1. Adicionar um **componente de botão** ao pai do painel. No vídeo de exemplo abaixo, um componente de botão com o nome do rótulo **Adicionar** e nome do campo **AddPanel**, é usada. Selecione o componente e toque em ![edit-rules](/help/forms/assets/edit-rules.png). As regras do componente de botão são abertas no editor de regras.
1. Na janela Editor de regras, clique em **Criar**.

   Selecionar **Editor visual** na linha Objetos de formulário e Funções.

   1. Na área regra, em QUANDO, selecione estado **foi clicado**.
   1. Em ENTÃO, selecione **Adicionar instância** e arraste e solte o painel usando ![ativar/desativar painel lateral](/help/forms/assets/toggle-side-panel.png) ou selecione-o usando **Solte o objeto ou selecione aqui.**

   Selecionar **Editor de código** na linha Objetos de formulário e Funções. Clique em **Editar regras** e na área de código:

   * Para criar um botão Adicionar painel, especifique `this.panel.instanceManager.addInstance()`

   Clique em **Concluído**.

>[!VIDEO](https://video.tv.adobe.com/v/3421052/adaptive-forms-repeatable-sections-repeat-sections/?quality=12&learn=on)


### Excluir seções repetíveis usando o gerenciador de instâncias (por meio de scripts) {#delete-repeatable-section-using-instance-manager-via-scripts}

O pai do painel deve conter um botão Excluir para excluir a instância dos painéis repetíveis. Execute as seguintes etapas para inserir botões ao pai e ativar scripts nos botões para excluir painéis repetíveis:

1. Adicionar um **componente de botão** ao pai do painel, no vídeo abaixo, um componente de botão com o nome do rótulo **excluir** e nome do campo **DeletePanel** é usada. Selecione o componente e toque em ![edit-rules](/help/forms/assets/edit-rules.png). As regras do componente de botão são abertas no editor de regras.
1. Na janela Editor de regras, clique em **Criar**.

   Selecionar **Editor visual** na linha Objetos de formulário e Funções.

   1. Na área de regras, em QUANDO **DeletePanel**, selecionar estado **foi clicado**.
   1. Em ENTÃO, selecione **Remover Instância** e arraste e solte o painel usando ![ativar/desativar painel lateral](/help/forms/assets/toggle-side-panel.png) ou selecione-o usando **Solte o objeto ou selecione aqui.**

   Selecionar **Editor de código** na linha Objetos de formulário e Funções. Clique em **Editar regras** e na área de código:

   * Para criar um botão de exclusão do painel, especifique `this.panel.instanceManager.removeInstance(this.panel.instanceIndex)`

   Clique em **Concluído**.
>[!VIDEO](https://video.tv.adobe.com/v/3421620/adaptive-forms-repeatable-sections)

>[!NOTE]
>
>Se um campo pertencer a um painel repetível, você não poderá acessá-lo diretamente usando seu nome nos scripts. Para acessar o campo, especifique a instância repetível à qual o campo pertence usando o `instances` API em `InstanceManager`. A sintaxe para usar o `instances` API em `InstanceManager` é:
>
>
>`<panelName>.instanceManager.instances[<instanceNumber>].<fieldname>`
>
>
>Por exemplo, você cria um formulário adaptável com um painel repetível com uma caixa de texto. Ao preencher previamente o formulário com três caixas de texto repetíveis, é necessário o xml abaixo:
>
>
>`<panel1><textbox1>AA1</panel1></textbox1>`
>
>
>`<panel1><textbox1>AA2</panel1></textbox1>`
>
>
>`<panel1><textbox1>AA3</panel1></textbox1>`
>
>
>Para ler os dados AA1, especifique:
>
>
>`Panel1.instanceManager.instances[0].textbox.value`
>
>
>Para ler os dados AA2, especifique:
>
>
>`Panel1.instanceManager.instances[1].textbox.value`
>
>
>

<!-- 
>For more information, see: Class: InstanceManager#instances in [AEM Forms Java API reference](https://adobe.com/go/learn_aemforms_documentation_63).      
-->

>[!NOTE]
>
> Quando todas as instâncias de um painel forem removidas de um formulário adaptável, para adicionar uma instância do painel removido, use a sintaxe _panelName para capturar o gerenciador de instâncias do painel e use a API addInstance do gerenciador de instâncias para adicionar a instância excluída. Por exemplo, _panelName.addInstance(). Ele adiciona uma instância do painel removido.

<!--
![panel-repeatability-video](/help/adaptive-forms/assets/panel-repeatability-video.mp4)
-->

<!--

## Using the accordion layout for the parent panel &nbsp; {#using-the-accordion-layout-for-the-parent-panel-nbsp}

A panel has various layouts options. The Layout for accordian design option has out of the box support for repeatable panels. Perform the following steps to repeatable panel with Layout for accordian design option:

1. On the parent of panel to be repeated, tap ![cmppr](assets/cmppr.png). You can see the properties in the sidebar. In the **Layout** drop-down, select **Accordion**.
1. On a panel, which is to be repeated, tap ![cmppr](assets/cmppr.png). You can see the panel properties in the sidebar. Enable the **Make Panel Repeatable** tab, and specify value for the **Maximum** and **Minimum** fields.

   Now, you can use the plus (+) and delete ( ![delete-panel](assets/delete-panel.png)) buttons to add and remove the panels.

-->

## Uso de subformulários repetidos do Modelo de formulário (XDP/XSD) {#using-repeating-subforms-from-form-template-xdp-xsd}

O subformulário repetível é semelhante aos painéis repetíveis no Adaptive Forms. No AEM Forms Designer, execute as seguintes etapas para criar um subformulário repetitivo:

1. Na paleta Hierarquia, selecione o subformulário pai do subformulário que deseja repetir.
1. Na paleta Objeto, clique na guia Subformulário e, na lista Conteúdo, selecione Fluxo.
1. Selecione o subformulário a ser repetido.
1. Na paleta Objeto, clique na guia Subformulário e, na lista Conteúdo, selecione Posicionado ou Fluxado.
1. Clique na guia Vinculação e selecione Repetir subformulário para cada item de dados.
1. Para especificar o número mínimo de repetições, selecione Contagem Mínima e digite um número na caixa associada. Se essa opção estiver definida como 0 e nenhum dado for fornecido para os objetos no subformulário no momento da mesclagem de dados, o subformulário não será colocado quando o formulário for renderizado.
1. Para especificar o número máximo de repetições do subformulário, selecione Máximo e digite um número na caixa associada. Se você não especificar um valor na caixa Máx., o número de repetições de subformulário será ilimitado.
1. Para especificar um número definido de repetições de subformulário, independentemente da quantidade de dados, selecione Contagem inicial e digite um número na caixa associada. Se você selecionar essa opção e não houver dados disponíveis ou houver menos entradas de dados do que o valor de Contagem inicial especificado, instâncias vazias do subformulário ainda serão colocadas no formulário.
1. Adicione dois botões no subformulário pai — um para adicionar a instância e outro para excluir a instância do subformulário repetível. Para obter etapas detalhadas, consulte [Criar uma ação](https://help.adobe.com/en_US/AEMForms/6.1/DesignerHelp/WS107c29ade9134a2c74572b5612a87ca2b56-8000.2.html#WS107c29ade9134a2c-1f74d86012a87d4fe55-8000.2).
1. Agora, vincule o Modelo de formulário ao Formulário adaptável. Para obter etapas detalhadas, consulte [Criar um formulário adaptável com base em um modelo](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/creating-adaptive-form.html?lang=en#create-an-adaptive-form-based-on-an-xfa-form-template).
1. Use os botões criados na etapa 9 para adicionar e remover subformulários.

O arquivo .zip anexado contém uma amostra de subformulário repetível.

[Obter arquivo](/help/forms/assets/samplerepeatablesubform.zip)

## Usando configurações de repetição de um Esquema XML (XSD) {#using-repeat-settings-of-an-xml-schema-xsd-br}

Você pode criar painéis repetíveis de um Esquema XML e da propriedade minOccours &amp; maxOccurs de qualquer elemento de tipo complexo. Para obter informações detalhadas sobre o Esquema XML, consulte [Criar formulários adaptáveis usando o esquema XML como modelo de formulário](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/adaptive-form-xml-schema-form-model.html).

No código a seguir, a variável `SampleType`O painel usa a propriedade minOccours &amp; maxOccurs.

```xml
<?xml version="1.0" encoding="utf-8" ?>
    <xs:schema targetNamespace="https://adobe.com/sample.xsd"
                    xmlns="https://adobe.com/sample.xsd"
                    xmlns:xs="https://www.w3.org/2001/XMLSchema"
                >

        <xs:element name="sample" type="SampleType"/>

        <xs:complexType name="SampleType">
            <xs:sequence>
                <xs:element name="leaderName" type="xs:string" default="Enter Name"/>
                <xs:element name="assignmentStartDate" type="xs:date"/>
                <xs:element name="gender" type="GenderEnum"/>
                <xs:element name="noOfProjectsAssigned" type="IntType"/>
                <xs:element name="assignmentDetails" type="AssignmentDetails"
                                            minOccurs="0" maxOccurs="10"/>
            </xs:sequence>
        </xs:complexType>

        <xs:complexType name="AssignmentDetails">
            <xs:attribute name="name" type="xs:string" use="required"/>
            <xs:attribute name="durationOfAssignment" type="xs:unsignedInt" use="required"/>
            <xs:attribute name="numberOfMentees" type="xs:unsignedInt" use="required"/>
             <xs:attribute name="descriptionOfAssignment" type="xs:string" use="required"/>
             <xs:attribute name="financeRelatedProject" type="xs:boolean"/>
       </xs:complexType>
  <xs:simpleType name="IntType">
            <xs:restriction base="xs:int">
            </xs:restriction>
        </xs:simpleType>
  <xs:simpleType name="GenderEnum">
            <xs:restriction base="xs:string">
                <xs:enumeration value="Female"/>
                <xs:enumeration value="Male"/>
            </xs:restriction>
        </xs:simpleType>
    </xs:schema>
```


## Consulte também {#see-also}

{{see-also}}


>[!MORELIKETHIS]
>
>* [Criar um formulário adaptável](creating-adaptive-form-core-components.md)
>* [Criar estilo ou temas para seus formulários](using-themes-in-core-components.md)
>* [Adicionar comportamento dinâmico a formulários usando o editor de regras](rule-editor.md)
>* [Definir layout de formulários para diferentes tamanhos de tela e tipos de dispositivo](/help/sites-cloud/authoring/features/responsive-layout.md)