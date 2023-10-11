---
title: Como projetar o esquema XML para um formulário adaptável?
description: Saiba como criar um esquema XML para um Formulário adaptável e criar um Formulário adaptável com base no esquema para produzir dados de reclamação de esquema.
feature: Adaptive Forms
role: User, Developer
level: Beginner, Intermediate
exl-id: 5b8ad9a8-77d4-4234-a4d7-c8964b975e96
source-git-commit: 7a65aa82792500616f971df52b8ddb6d893ab89d
workflow-type: tm+mt
source-wordcount: '952'
ht-degree: 6%

---

# Criar esquema XML para um formulário adaptável {#creating-adaptive-forms-using-xml-schema}

## Pré-requisitos {#prerequisites}

A criação de um formulário adaptável usando um esquema XML como modelo de formulário requer conhecimento básico de esquemas XML. Além disso, é recomendável ler o conteúdo a seguir antes deste artigo.

* [Criação de um formulário adaptável](creating-adaptive-form.md)
* [Esquema XML](https://www.w3.org/TR/xmlschema-2/)

## Usando um esquema XML como modelo de formulário {#using-an-xml-schema-as-form-model}

[!DNL Experience Manager Forms] O oferece suporte à criação de um Formulário adaptável usando um esquema XML existente como modelo de formulário. Esse esquema XML representa a estrutura em que os dados são produzidos ou consumidos pelo sistema de back-end em sua organização.

Os principais recursos do uso de um esquema XML são:

* A estrutura do XSD é exibida como uma árvore na guia Localizador de conteúdo no modo de criação de um Formulário adaptável. Você pode arrastar e adicionar elemento da hierarquia XSD ao Formulário adaptável.
* Você pode preencher previamente o formulário usando um XML compatível com o esquema associado.
* No envio, os dados inseridos pelo usuário são enviados como XML que se alinha ao schema associado.

Um esquema XML consiste em tipos de elementos simples e complexos. Os elementos têm atributos que adicionam regras ao elemento. Quando esses elementos e atributos são arrastados para um Formulário adaptável, eles são mapeados automaticamente para o componente de Formulário adaptável correspondente.

Esse mapeamento de elementos XML com componentes do Formulário adaptável é o seguinte:

<table>
 <tbody>
  <tr>
   <th><strong>Elemento ou atributo XML </strong></th>
   <th><strong>Componente de formulário adaptável</strong></th>
  </tr>
  <tr>
   <td><code>xs:string</code></td>
   <td>Caixa de texto</td>
  </tr>
  <tr>
   <td><code>xs:boolean</code></td>
   <td>Caixa de seleção</td>
  </tr>
  <tr>
   <td>
    <ul>
     <li><code>xs:unsignedInt</code></li>
     <li><code>xs:xs:int</code></li>
     <li><code class="code">xs:decimal
        </code></li>
     <li>Todos os tipos de valores numéricos</li>
    </ul> </td>
   <td>Caixa numérica</td>
  </tr>
  <tr>
   <td><code>xs:date</code></td>
   <td>Seletor de data</td>
  </tr>
  <tr>
   <td><code class="code">xs:enumeration
      </code></td>
   <td>Lista suspensa</td>
  </tr>
  <tr>
   <td>Qualquer elemento de tipo complexo</td>
   <td>Painel</td>
  </tr>
 </tbody>
</table>

## Exemplo de esquema XML {#sample-xml-schema}

Este é um exemplo de um esquema XML.

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
                <xs:element name="assignmentStartBirth" type="xs:date"/>
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

>[!NOTE]
>
>Certifique-se de que o esquema XML tenha apenas um elemento raiz. Não há suporte para um esquema XML com mais de um elemento raiz.

## Adição de propriedades especiais a campos usando o esquema XML {#adding-special-properties-to-fields-using-xml-schema}

Você pode adicionar os seguintes atributos aos elementos do Esquema XML para adicionar propriedades especiais aos campos do Formulário adaptável associado.

<table>
 <tbody>
  <tr>
   <th><strong>Propriedade do esquema</strong></th>
   <th><strong>Uso no formulário adaptável</strong></th>
   <th><strong>Compatível com o </strong></th>
  </tr>
  <tr>
   <td><code>use=required </code></td>
   <td>Marca um campo como obrigatório<br /> </td>
   <td>Atributo</td>
  </tr>
  <tr>
   <td><code>default="default value"</code></td>
   <td>Adiciona um valor padrão</td>
   <td>Elemento e atributo</td>
  </tr>
  <tr>
   <td><code>minOccurs="3"</code></td>
   <td><p>Especifica o mínimo de ocorrências</p> <p>(Para subformulários repetíveis (tipos complexos))</p> </td>
   <td>Elemento (tipo complexo)</td>
  </tr>
  <tr>
   <td><code class="code">maxOccurs="10"
      </code></td>
   <td><p>Especifica o máximo de ocorrências</p> <p>(Para subformulários repetíveis (tipos complexos))</p> </td>
   <td>Elemento (tipo complexo)</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Ao arrastar um elemento de esquema para um Formulário adaptável, uma legenda padrão é gerada por:
>
>* Colocar o primeiro caractere do nome do elemento em maiúsculas
>* Inserção de espaço em branco nos limites do Camel Case.
>
>Por exemplo, se você adicionar a variável `userFirstName` elemento de esquema, a legenda gerada no Formulário adaptável é `User First Name`.

## Limitar valores aceitáveis para um componente de Formulário adaptável {#limit-acceptable-values-for-an-adaptive-form-component}

Você pode adicionar as seguintes restrições aos elementos do esquema XML para limitar os valores aceitáveis para um componente de Formulário adaptável:

<table>
 <tbody>
  <tr>
   <td><p><strong> Propriedade do esquema</strong></p> </td>
   <td><p><strong>Tipo de dados</strong></p> </td>
   <td><p><strong>Descrição</strong></p> </td>
   <td><p><strong>Componente</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>totalDigits</code></p> </td>
   <td><p>String</p> </td>
   <td><p>Especifica o número máximo de dígitos permitidos em um componente. O número de dígitos especificado deve ser maior que zero.</p> </td>
   <td>
    <ul>
     <li>Caixa numérica</li>
     <li>Escalonador numérico</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>maximum</code></p> </td>
   <td><p>String</p> </td>
   <td><p>Especifica o limite superior para valores numéricos e datas. Por padrão, o valor máximo é incluído.</p> </td>
   <td>
    <ul>
     <li>Caixa numérica</li>
     <li>Escalonador numérico<br /> </li>
     <li>Seletor de data</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>minimum</code></p> </td>
   <td><p>String</p> </td>
   <td><p>Especifica o limite inferior para valores numéricos e datas. Por padrão, o valor mínimo é incluído.</p> </td>
   <td>
    <ul>
     <li>Caixa numérica</li>
     <li>Escalonador numérico</li>
     <li>Seletor de data</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>exclusiveMaximum</code></p> </td>
   <td><p>Booleano</p> </td>
   <td><p>Se true, o valor numérico ou a data especificada no componente do formulário deverá ser menor que o valor numérico ou a data especificada para a propriedade máxima.</p> <p>Se false, o valor numérico ou a data especificada no componente do formulário deve ser menor ou igual ao valor numérico ou à data especificada para a propriedade maximum.</p> </td>
   <td>
    <ul>
     <li>Caixa numérica</li>
     <li>Escalonador numérico</li>
     <li>Seletor de data</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>exclusiveMinimum</code></p> </td>
   <td><p>Booleano</p> </td>
   <td><p>Se true, o valor numérico ou a data especificada no componente do formulário deverá ser maior que o valor numérico ou a data especificada para a propriedade minimum.</p> <p>Se false, o valor numérico ou a data especificada no componente do formulário deve ser maior ou igual ao valor numérico ou à data especificada para a propriedade minimum.</p> </td>
   <td>
    <ul>
     <li>Caixa numérica</li>
     <li>Escalonador numérico</li>
     <li>Seletor de data</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>minLength</code></p> </td>
   <td><p>String</p> </td>
   <td><p>Especifica o número mínimo de caracteres permitidos em um componente. O comprimento mínimo deve ser igual ou maior que zero.</p> </td>
   <td>
    <ul>
     <li>Caixa de texto</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>maxLength</code></p> </td>
   <td><p>String</p> </td>
   <td><p>Especifica o número máximo de caracteres permitidos em um componente. O comprimento máximo deve ser maior que zero.</p> </td>
   <td>
    <ul>
     <li>Caixa de texto</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>length</code></p> </td>
   <td><p>String</p> </td>
   <td><p>Especifica o número exato de caracteres permitidos em um componente. O comprimento deve ser igual ou maior que zero.</p> </td>
   <td>
    <ul>
     <li>Caixa de texto</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>fractionDigits</code></p> </td>
   <td><p>String</p> </td>
   <td><p>Especifica o número máximo de casas decimais permitidas em um componente. O número de dígitos da fração deve ser igual ou maior que zero.</p> </td>
   <td>
    <ul>
     <li> Caixa numérica com tipo de dados flutuante ou decimal</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>pattern</code></p> </td>
   <td><p>String</p> </td>
   <td><p>Especifica a sequência dos caracteres. Um componente aceita os caracteres se eles estiverem em conformidade com o padrão especificado.</p> <p>A propriedade padrão mapeia para o padrão de validação do componente de Formulário adaptável correspondente.</p> </td>
   <td>
    <ul>
     <li>Todos os componentes adaptáveis do Forms mapeados para um esquema XSD </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## Perguntas frequentes {#frequently-asked-questions}

**Tenho uma estrutura complexa longa no Localizador de conteúdo. Como posso encontrar um elemento específico?**

Você tem duas opções:

* Rolar pela estrutura de árvore
* Use a caixa Pesquisar para localizar um elemento

**O que é um bindRef?**

A `bindRef` é a conexão entre um componente de Formulário adaptável e um elemento ou atributo de esquema. Ele dita que `XPath` em que o valor capturado deste componente ou campo está disponível no XML de saída. A `bindRef`também é usado ao preencher previamente um valor de campo do XML preenchido previamente (preenchido previamente).

**Por que não consigo arrastar elementos individuais de um subformulário (estrutura gerada de qualquer tipo complexo) para subformulários repetíveis (os valores minOccours ou maxOccurs são maiores que 1)?**

Em um subformulário repetível, você deve usar o subformulário Concluído. Se desejar apenas campos seletivos, use a estrutura inteira e exclua os indesejados.
