---
title: Como preencher previamente os campos do formulário adaptável?
description: Com os dados existentes para preencher previamente os campos de um formulário adaptável, os usuários podem preencher previamente as informações básicas em um formulário fazendo logon com seus perfis sociais.
topic-tags: develop
feature: Adaptive Forms, Foundation Components
exl-id: e2a87233-a0d5-48f0-b883-915fe56f105f
role: User, Developer
source-git-commit: 8f39bffd07e3b4e88bfa200fec51572e952ac837
workflow-type: tm+mt
source-wordcount: '2044'
ht-degree: 1%

---

# Preencher previamente campos do formulário adaptável{#prefill-adaptive-form-fields}

>[!NOTE]
>
> A Adobe recomenda usar os [Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=pt-BR) de captura de dados moderna e extensível para [criar um novo Forms Adaptável](/help/forms/creating-adaptive-form-core-components.md) ou [adicionar o Forms Adaptável às páginas do AEM Sites](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md). Esses componentes representam um avanço significativo na criação do Forms adaptável, garantindo experiências de usuário impressionantes. Este artigo descreve a abordagem mais antiga para criar o Forms adaptável usando componentes de base.

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/prepopulate-adaptive-form-fields.html?lang=pt-BR) |
| AEM as a Cloud Service | Este artigo |

## Introdução {#introduction}

É possível preencher previamente os campos de um Formulário adaptável usando dados existentes. Quando um usuário abre um formulário, os valores desses campos são preenchidos previamente. Para preencher previamente os dados em um formulário adaptável, disponibilize os dados do usuário como um XML/JSON de preenchimento prévio no formato que segue a estrutura de dados de preenchimento prévio do Adaptive Forms.

## Aplicabilidade e casos de uso

### Seguros

## O AEM Forms pode preencher previamente os dados do aplicativo de seguro?

Sim. O AEM Forms oferece suporte ao preenchimento prévio de campos de formulário usando fontes de dados de back-end, permitindo que as seguradoras reutilizem dados existentes do cliente ou da política e reduzam a entrada manual.

## Estrutura dos dados de preenchimento prévio {#the-prefill-structure}

Um Formulário adaptável pode ter uma combinação de campos vinculados e não vinculados. Os campos associados são campos que são arrastados da guia Localizador de conteúdo e contêm o valor da propriedade `bindRef` não vazio na caixa de diálogo de edição de campo. Os campos não vinculados são arrastados diretamente do navegador de componentes do Sidekick e têm um valor `bindRef` vazio.

É possível preencher previamente os campos vinculados e não vinculados de um Formulário adaptável. Os dados de pré-preenchimento contêm as seções afBoundData e afUnBoundData para preencher previamente os campos vinculados e não vinculados de um Formulário adaptável. A seção `afBoundData` contém os dados de preenchimento prévio para campos e painéis associados. Esses dados devem ser compatíveis com o schema do modelo de formulário associado:

- Para o Adaptive Forms usando o [modelo de formulário XFA](#xfa-based-af), use o XML de preenchimento prévio compatível com o esquema de dados do modelo XFA.
- Para o Forms Adaptável usando o [esquema XML](#xml-schema-af), use o XML de preenchimento prévio compatível com a estrutura do esquema XML.
- Para o Forms adaptável usando o [esquema JSON](#json-schema-based-adaptive-forms), use o JSON de preenchimento prévio compatível com o esquema JSON.
- Para o Forms adaptável usando o esquema do FDM, use o JSON de preenchimento prévio compatível com o esquema do FDM.
- Para o Adaptive Forms com [nenhum modelo de formulário](#adaptive-form-with-no-form-model), não há dados associados. Cada campo é um campo não vinculado e é pré-preenchido usando o XML não vinculado.

### Exemplo de estrutura XML de preenchimento prévio {#sample-prefill-xml-structure}

```xml
<?xml version="1.0" encoding="UTF-8"?>
<afData>
  <afBoundData>
     <employeeData>
        .
     </employeeData>
  </afBoundData>

  <afUnboundData>
    <data>
      <textbox>Hello World</textbox>
         .
         .
      <numericbox>12</numericbox>
         .
         .
    </data>
  </afUnboundData>
</afData>
```

### Exemplo de estrutura JSON de preenchimento prévio {#sample-prefill-json-structure}

```javascript
{
   "afBoundData": {
      "employeeData": { }
   },
   "afUnboundData": {
      "data": {
         "textbox": "Hello World",
         "numericbox": "12"
      }
   }
}
```

Para campos vinculados com o mesmo vínculo ou campos não vinculados com o mesmo nome, os dados especificados na tag XML ou no objeto JSON são preenchidos em todos os campos. Por exemplo, dois campos em um formulário são mapeados para o nome `textbox` nos dados de preenchimento prévio. Durante o tempo de execução, se o primeiro campo da caixa de texto contiver &quot;A&quot;, então &quot;A&quot; será automaticamente preenchido na segunda caixa de texto. Esse vínculo é chamado de vínculo ativo de campos de formulário adaptável.

### Formulário adaptável usando o modelo de formulário XFA {#xfa-based-af}

A estrutura do XML de preenchimento prévio e do XML enviado para o Adaptive Forms baseado em XFA é a seguinte:

- **Estrutura XML de Preenchimento Prévio**: o XML de Preenchimento Prévio do Formulário Adaptável baseado em XFA deve ser compatível com o esquema de dados do modelo de formulário XFA. Para preencher previamente campos não associados, envolva a estrutura XML de preenchimento prévio na marca `/afData/afBoundData`.

- **Estrutura XML Enviada**: quando nenhum XML de preenchimento prévio é usado, o XML enviado contém dados para campos associados e não associados na marca wrapper `afData`. Se um XML de preenchimento prévio for usado, o XML enviado terá a mesma estrutura que o XML de preenchimento prévio. Se o XML de preenchimento prévio começar com a marca raiz `afData`, o XML de saída também terá o mesmo formato. Se o XML de preenchimento prévio não tiver `afData/afBoundData`wrapper e, em vez disso, iniciar diretamente da marca raiz do esquema como `employeeData`, o XML enviado também iniciará com a marca `employeeData`.

Prefill-Submit-Data-ContentPackage.zip

[Obter arquivo](assets/prefill-submit-data-contentpackage.zip)
Amostra contendo dados de preenchimento prévio e dados enviados

### FORMS adaptável baseado em esquema XML  {#xml-schema-af}

A estrutura do XML de preenchimento prévio e do XML enviado para o Adaptive Forms com base no esquema XML é a seguinte:

- **Estrutura XML de preenchimento prévio**: o XML de preenchimento prévio deve ser compatível com o Esquema XML associado. Para preencher previamente os campos não vinculados, coloque a estrutura XML de preenchimento previamente na tag /afData/afBoundData.
- **Estrutura XML enviada**: se nenhum XML de preenchimento prévio for usado, o XML enviado conterá dados para campos associados e não associados na marca wrapper `afData`. Se o XML de preenchimento prévio for usado, o XML enviado terá a mesma estrutura do XML de preenchimento prévio. Se o XML de preenchimento prévio começar com a marca raiz `afData`, o XML de saída terá o mesmo formato. Se o XML de preenchimento prévio não tiver o invólucro `afData/afBoundData` e, em vez disso, iniciar diretamente da marca raiz do esquema como `employeeData`, o XML enviado também iniciará com a marca `employeeData`.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<xs:schema targetNamespace="https://adobe.com/sample.xsd"
            xmlns="https://adobe.com/sample.xsd"
            xmlns:xs="https://www.w3.org/2001/XMLSchema">

    <xs:element name="sample" type="SampleType"/>

    <xs:complexType name="SampleType">
        <xs:sequence>
            <xs:element name="noOfProjectsAssigned" type="xs:string"/>
        </xs:sequence>
    </xs:complexType>
</xs:schema>
```

Para campos cujo modelo é um esquema XML, os dados são pré-preenchidos na marca `afBoundData`, como mostrado na amostra XML abaixo. Ele pode ser usado para preencher previamente um Formulário adaptável com um ou mais campos de texto não vinculados.

```xml
<?xml version="1.0" encoding="UTF-8"?><afData>
  <afUnboundData>
    <data>
      <textbox>Ignorance is bliss :) </textbox>
    </data>
  </afUnboundData>
  <afBoundData>
    <data>
      <noOfProjectsAssigned>twelve</noOfProjectsAssigned>
    </data>
  </afBoundData>
</afData>
```

>[!NOTE]
>
>É recomendável não usar campos não vinculados em painéis vinculados (painéis com o `bindRef` não vazio que foi criado ao arrastar componentes da guia Sidekick ou Fontes de dados). Isso pode causar perda de dados desses campos não vinculados. Além disso, é recomendável que os nomes dos campos sejam exclusivos em todo o formulário, especialmente para campos não vinculados.

#### Um exemplo sem afData e afBoundData wrapper {#an-example-without-afdata-and-afbounddata-wrapper}

```xml
<?xml version="1.0" encoding="UTF-8"?><config>
 <assignmentDetails descriptionOfAssignment="Some Science Project" durationOfAssignment="34" financeRelatedProject="1" name="Lisa" numberOfMentees="1"/>
 <assignmentDetails descriptionOfAssignment="Kidding, right?" durationOfAssignment="4" financeRelatedProject="1" name="House" numberOfMentees="3"/>
</config>
```

### Forms adaptável baseado em esquema JSON {#json-schema-based-adaptive-forms}

Para o Adaptive Forms com base no esquema JSON, a estrutura do JSON de preenchimento prévio e do JSON enviado é descrita abaixo. Para obter mais informações, consulte [Criando Forms adaptável usando o esquema JSON](adaptive-form-json-schema-form-model.md).

- **Preencher previamente a estrutura JSON**: o JSON de preenchimento prévio deve ser compatível com o Esquema JSON associado. Opcionalmente, ele pode ser encapsulado no objeto /afData/afBoundData se você também quiser preencher previamente os campos não vinculados.
- **Estrutura JSON enviada**: se nenhum JSON de preenchimento prévio for usado, o JSON enviado conterá dados para campos ligados e não ligados na marca afData wrapper. Se o JSON de preenchimento prévio for usado, o JSON enviado terá a mesma estrutura que o JSON de preenchimento prévio. Se o JSON de preenchimento prévio começar com o objeto raiz afData, o JSON de saída terá o mesmo formato. Se o JSON de preenchimento prévio não tiver o invólucro afData/afBoundData e, em vez disso, iniciar diretamente a partir do objeto raiz do esquema, como o usuário, o JSON enviado também começará com o objeto do usuário.

```json
{
  "id": "https://some.site.somewhere/entry-schema#",
  "$schema": "https://json-schema.org/draft-04/schema#",
  "type": "object",
  "properties": {
    "address": {
      "type": "object",
      "properties": {
        "name": {
          "type": "string"
        },
        "age": {
          "type": "integer"
        }
      }
    }
  }
}
```

Para campos que usam o modelo de esquema JSON, os dados são pré-preenchidos no objeto afBoundData, como mostrado na amostra JSON abaixo. Ele pode ser usado para preencher previamente um Formulário adaptável com um ou mais campos de texto não vinculados. Veja abaixo um exemplo de dados com o wrapper `afData/afBoundData`:

```json
{
  "afData": {
    "afUnboundData": {
      "data": { "textbox": "Ignorance is bliss :) " }
    },
    "afBoundData": {
      "data": { {
   "user": {
    "address": {
     "city": "Noida",
     "country": "India"
}}}}}}}
```

Veja abaixo um exemplo sem o `afData/afBoundData` wrapper:

```json
{
  "user": {
    "address": {
      "city": "Noida",
      "country": "India"
    }
  }
}
```

>[!NOTE]
>
> O uso de campos não vinculados em painéis vinculados (painéis com bindRef não vazios que foram criados ao arrastar componentes da guia Sidekick ou Fontes de dados) é **não** recomendado, pois pode causar perda de dados dos campos não vinculados. É recomendável ter nomes de campo exclusivos em todo o formulário, especialmente para campos não vinculados.
>

### Formulário adaptável sem modelo de formulário {#adaptive-form-with-no-form-model}

Para o Adaptive Forms sem modelo de formulário, os dados de todos os campos estão na marca `<data>` de `<afUnboundData> tag`.

Além disso, tome nota do seguinte:

As tags XML para os dados do usuário enviados para vários campos são geradas usando o nome dos campos. Portanto, os nomes dos campos devem ser exclusivos.

```xml
<?xml version="1.0" encoding="UTF-8"?><afData>
  <afUnboundData>
    <data>
      <radiobutton>2</radiobutton>
      <repeatable_panel_no_form_model>
        <numericbox>12</numericbox>
      </repeatable_panel_no_form_model>
      <repeatable_panel_no_form_model>
        <numericbox>21</numericbox>
      </repeatable_panel_no_form_model>
      <checkbox>2</checkbox>
      <textbox>Nopes</textbox>
    </data>
  </afUnboundData>
  <afBoundData/>
</afData>
```

## Configuração do serviço de preenchimento prévio {#configuring-prefill-service-using-configuration-manager}

Use a propriedade `alloweddataFileLocations` da **Configuração do Serviço de Preenchimento Prévio Padrão** para definir o local dos arquivos de dados ou um regex (expressão regular) para os locais dos arquivos de Dados.

O seguinte arquivo JSON exibe uma amostra:

```JSON
  {
  "alloweddataFileLocations": "`file:///C:/Users/public/Document/Prefill/.*`"
  }
```

Para definir valores de uma configuração, [Gere Configurações OSGi usando o AEM SDK](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=pt-BR#generating-osgi-configurations-using-the-aem-sdk-quickstart) e [implante a configuração](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=pt-BR#deployment-process) na sua instância do Cloud Service.

>[!NOTE]
>
> - Por padrão, o preenchimento prévio é permitido por meio de arquivos crx para todos os tipos de Forms adaptável (XSD, XDP, JSON, FDM e sem modelo de formulário baseado). O preenchimento prévio é permitido somente com arquivos JSON e XML.
> - O protocolo crx cuida da segurança de dados pré-preenchida e, portanto, é permitido por padrão. O preenchimento prévio por meio de outros protocolos usando regex genérico pode causar vulnerabilidade. Na configuração do, especifique uma configuração de URL segura para proteger seus dados.

## O caso curioso de painéis repetíveis {#the-curious-case-of-repeatable-panels}

Geralmente, os campos vinculados (esquema de formulário) e não vinculados são criados no mesmo Formulário adaptável, mas as exceções a seguir são algumas caso os campos vinculados sejam repetíveis:

- Os painéis repetíveis não vinculados não são compatíveis com o Adaptive Forms usando o modelo de formulário XFA, XSD, esquema JSON ou esquema FDM.
- Não use campos não vinculados em painéis repetíveis vinculados.

>[!NOTE]
>
> Como regra geral, não misture campos vinculados e não vinculados se eles forem cruzados em dados preenchidos pelo usuário em campos desvinculados. Se possível, você deve modificar o esquema ou o modelo de formulário XFA e adicionar uma entrada para campos não vinculados, para que também se torne vinculado e seus dados estejam disponíveis como outros campos nos dados enviados.

## Protocolos compatíveis com o preenchimento prévio de dados do usuário {#supported-protocols-for-prefilling-user-data}

O Forms adaptável pode ser preenchido previamente com dados do usuário no formato de dados de preenchimento prévio por meio dos seguintes protocolos quando configurado com regex válido:

### O protocolo crx:// {#the-crx-protocol}

```javascript
http
https://`servername`/content/forms/af/xml.html?wcmmode=disabled&dataRef=crx:///tmp/fd/af/myassets/sample.xml
```

O nó especificado deve ter uma propriedade chamada `jcr:data` e conter os dados.

### O protocolo file://  {#the-file-protocol-nbsp}

```javascript
https://`servername`/content/forms/af/someAF.html?wcmmode=disabled&dataRef=file:///C:/Users/form-user/Downloads/somesamplexml.xml
```

O arquivo referenciado deve estar no mesmo servidor.

### O protocolo https:// {#the-http-protocol}

```javascript
https://`servername`/content/forms/af/xml.html?wcmmode=disabled&dataRef=https://servername/somesamplexmlfile.xml
```

### O protocolo service:// {#the-service-protocol}

```javascript
https://`servername`/content/forms/af/abc.html?wcmmode=disabled&dataRef=service://[SERVICE_NAME]/[IDENTIFIER]
```

- SERVICE_NAME refere-se ao nome do serviço de preenchimento prévio OSGI. Consulte [Criar e executar um serviço de preenchimento prévio](prepopulate-adaptive-form-fields.md#create-and-run-a-prefill-service).
- IDENTIFIER refere-se a quaisquer metadados necessários pelo serviço de preenchimento prévio OSGI para buscar os dados de preenchimento prévio. Um identificador para o usuário conectado é um exemplo de metadados que podem ser usados.

>[!NOTE]
>
> Não há suporte para a transmissão de parâmetros de autenticação.

### Definição do atributo de dados em slingRequest {#setting-data-attribute-in-slingrequest}

Você também pode definir o atributo `data` em `slingRequest`, onde o atributo `data` é uma cadeia de caracteres que contém XML ou JSON, conforme mostrado no código de exemplo abaixo (O exemplo é para XML):

```javascript
<%
           String dataXML="<afData>" +
                            "<afUnboundData>" +
                                "<data>" +
                                    "<first_name>"+ "Tyler" + "</first_name>" +
                                    "<last_name>"+ "Durden " + "</last_name>" +
                                    "<gender>"+ "Male" + "</gender>" +
                                    "<location>"+ "Texas" + "</location>" +
                                    "</data>" +
                            "</afUnboundData>" +
                        "</afData>";
        slingRequest.setAttribute("data", dataXML);
%>
```

Você pode gravar uma sequência XML ou JSON simples contendo todos os seus dados e defini-la em slingRequest. Isso pode ser feito facilmente no JSP do renderizador para qualquer componente, que você deseja incluir na página, onde é possível definir o atributo de dados slingRequest.

Por exemplo, quando você deseja um design específico para a página com um tipo específico de cabeçalho. Para isso, você pode escrever seu próprio `header.jsp`, que pode ser incluído no componente de página e definir o atributo `data`.

Outro bom exemplo é um caso de uso em que você deseja preencher previamente os dados ao fazer logon por meio de contas sociais como Facebook, Twitter ou LinkedIn. Nesse caso, você pode incluir um JSP simples em `header.jsp`, que busca dados da conta de usuário e define o parâmetro de dados.

prefill-page component.zip

[Obter arquivo](assets/prefill-page-component.zip)
Amostra de prefill.jsp no componente Página

## [!DNL AEM Forms] serviço personalizado {#aem-forms-custom-prefill-service}

Você pode usar o serviço de preenchimento prévio personalizado para os cenários, em que lê constantemente os dados de uma fonte predefinida. O serviço de preenchimento prévio lê os dados de fontes de dados definidas e preenche os campos do Formulário adaptável com o conteúdo do arquivo de dados de preenchimento prévio. Também ajuda a associar permanentemente os dados pré-preenchidos a um Formulário adaptável.

### Criar e executar um serviço de preenchimento prévio {#create-and-run-a-prefill-service}

O serviço de pré-preenchimento é um serviço OSGi e é empacotado por meio do pacote OSGi. Você cria o pacote OSGi, carrega e instala-o em [!DNL AEM Forms] pacotes. Antes de começar a criar o pacote:

- [Baixar o [!DNL AEM Forms] SDK Cliente](https://helpx.adobe.com/br/aem-forms/kb/aem-forms-releases.html)
- Baixar o pacote padrão

- Coloque o arquivo de dados (dados de preenchimento prévio) no repositório crx. Você pode colocar o arquivo em qualquer local na pasta \contents do repositório crx.

[Obter arquivo](assets/prefill-sumbit-xmlsandcontentpackage.zip)

#### Criar um serviço de preenchimento {#create-a-prefill-service}

O pacote padrão (pacote do serviço de preenchimento de exemplo) contém uma implementação de exemplo do serviço de preenchimento prévio [!DNL AEM Forms]. Abra o pacote padrão em um editor de código. Por exemplo, abra o projeto padronizado no Eclipse para edição. Depois de abrir o pacote padrão em um editor de código, execute as etapas a seguir para criar o serviço.

1. Abra o arquivo src\main\java\com\adobe\test\Prefill.java para edição.
1. No código, defina o valor de:

   - `nodePath:` A variável de caminho de nó que aponta para o local do repositório crx contém o caminho do arquivo de dados (preenchimento prévio). Por exemplo, /content/prefilldata.xml
   - `label:` O parâmetro de rótulo especifica o nome de exibição do serviço. Por exemplo, Serviço de preenchimento prévio padrão

1. Salvar e fechar o arquivo `Prefill.java`.
1. Adicione o pacote `AEM Forms Client SDK` ao caminho de compilação do projeto padrão.
1. Compile o projeto e crie o .jar para o pacote.

#### Iniciar e usar o serviço de preenchimento prévio {#start-and-use-the-prefill-service}

Para iniciar o serviço de preenchimento prévio, carregue o arquivo JAR no Console da Web do [!DNL AEM Forms] e ative o serviço. Agora, o serviço começa a aparecer no editor Adaptive Forms. Para associar um serviço de preenchimento prévio a um Formulário adaptável:

1. Abra o Formulário adaptável no Editor de Forms e abra o painel Propriedades do Contêiner de formulário.
1. No console Propriedades, navegue até o contêiner [!DNL AEM Forms] > Básico > Serviço de preenchimento prévio.
1. Selecione o Serviço de preenchimento prévio padrão e clique em **[!UICONTROL Salvar]**. O serviço está associado ao formulário.

<!-- ## Prepopulate data at client {#prefill-at-client}

When you prefill an Adaptive Form, the [!DNL AEM Forms] server merges data with an Adaptive Form and delivers the filled form to you. By default, the data merge action takes place at the server.

You can configure the [!DNL AEM Forms] server to perform the data merge action at the client instead of the server. It significantly reduces the time required to prefill and render Adaptive Forms. By default, the feature is disabled. You can enable it from the Configuration Manager or command line.

* To enable or disable from configuration manager:
  1. Open AEM Configuration Manager.
  1. Locate and open the Adaptive Form and Interactive Communication Web Channel Configuration
  1. Enable the Configuration.af.clientside.datamerge.enabled.name option
* To enable or disable from the command line:
  * To enable, run the following cURL command:
    `curl -u admin:admin -X POST -d apply=true \ -d propertylist=af.clientside.datamerge.enabled \ -d af.clientside.datamerge.enabled=true \ http://${crx.host}:${crx.port}/system/console/configMgr/Adaptive%20Form%20and%20Interactive%20Communication%20Web%20Channel%20Configuration`

  * To disable, run the following cURL command:
    `curl -u admin:admin -X POST -d apply=true \ -d propertylist=af.clientside.datamerge.enabled \ -d af.clientside.datamerge.enabled=false \ http://${crx.host}:${crx.port}/system/console/configMgr/Adaptive%20Form%20and%20Interactive%20Communication%20Web%20Channel%20Configuration`

   To take full advantage of the prepopulate data at client option, update your prefill service to return [FileAttachmentMap](https://helpx.adobe.com/br/experience-manager/6-5/forms/javadocs/com/adobe/forms/common/service/PrefillData.html) and [CustomContext](https://helpx.adobe.com/br/experience-manager/6-5/forms/javadocs/com/adobe/forms/common/service/PrefillData.html) -->