---
title: Gerar documento de registro para o Adaptive Forms
description: Explica como você pode gerar um modelo para um Documento de registro (DoR) para Adaptive Forms.
exl-id: 15540644-c0c3-45ce-97d3-3bdaa16fb4b6
source-git-commit: 4279b4a880429f535cf341d35ac38c9b4dc55ae2
workflow-type: tm+mt
source-wordcount: '3109'
ht-degree: 2%

---

# Gerar documento de registro para Forms adaptável (Componentes principais)

## Visão geral {#overview}

Quando um formulário é preenchido ou enviado, é possível manter um registro do formulário, em formato impresso ou documento. Este registro é conhecido como Documento de Registro (DoR). É uma cópia fácil de imprimir do formulário enviado. Você também pode consultar o documento de registro para as informações que os clientes preencheram posteriormente ou usar o Documento de registro para arquivar formulários e conteúdo juntos no Formato PDF.

![Documento do registro](assets/document-of-record.png)

Para criar um Documento de registro, um modelo baseado em XFA ou Acroform é unido aos dados coletados por um formulário adaptável. Você pode gerar um Documento de registro automaticamente ou sob demanda. A opção sob demanda permite especificar um modelo personalizado baseado em XFA ou Acroform para fornecer uma aparência personalizada ao seu Documento de registro.

É possível:

* [Gerar um documento de registro baseado em XFA](#generate-an-XFA-based-document-of-record)
* [Gerar um documento de registro baseado em formulário (Acrobat Form PDF)](#generate-an-Acroform-based-document-of-record)
* [Gerar automaticamente um Documento de Registro](#auto-generate-a-document-of-record)

## Antes de você iniciar {#components-to-automatically-generate-a-document-of-record}

Antes de começar a aprender e a preparar os ativos necessários para um Documento de registro:

**Modelo base:** Um modelo XFA (arquivo XDP) criado no Forms Designer ou em um formulário Acrobat (AcroForm). [Modelo base](#base-template-of-a-document-of-record) é usada para especificar informações de estilo e identidade visual para um Documento de registro. Faça upload de seu modelo XFA (arquivo XDP) para sua instância do AEM Forms antes.

**Formulário adaptável:** Um formulário adaptável para o qual o documento de registro deve ser gerado.

## Gerar um documento de registro baseado em XFA {#generate-an-XFA-based-document-of-record}

Carregue seu modelo XFA (arquivo XDP) na instância do AEM Forms. Execute as seguintes etapas para configurar um Formulário adaptável para usar o modelo XFA (arquivo XDP) como modelo para o Documento de registro:

1. Na instância do autor do Experience Manager, clique em **[!UICONTROL Forms]** > **[!UICONTROL Forms e documentos].**
1. Selecione um formulário ou Crie um formulário adaptável e clique em **[!UICONTROL Propriedades]**.
1. Na janela Propriedades, toque em **[!UICONTROL Modelo de formulário]**.
1. No  **[!UICONTROL Modelo de formulário]** na guia , no **[!UICONTROL Selecionar de]** , selecione **[!UICONTROL Modelo de dados do formulário]**, **[!UICONTROL Esquema]** ou **[!UICONTROL Nenhum]**. Também é possível selecionar um modelo de formulário ao criar um formulário.
1. Na seção Document of Record Template Configuration da guia Form Model , selecione **Associar Modelo de Formulário como Documento de Modelo de Registro**. Ao selecionar essa opção, todos os modelos XFA (arquivos XDP) disponíveis em sua máquina são exibidos. Selecione o arquivo apropriado. Além disso, verifique se o mesmo esquema (esquema de dados) é usado para o Formulário adaptável e para o modelo XFA selecionado (arquivo XDP).
1. Clique em **[!UICONTROL Feito.]**

Seu formulário adaptável agora está configurado para usar um arquivo XDP como modelo para o Documento de registro. As próximas etapas são para [vincular componentes do formulário adaptável aos campos de modelo correspondentes](#bind-adaptive-form-components-with-template-fields).

## Gerar um documento de registro baseado em formulário {#generate-an-Acroform-based-document-of-record}

Faça upload do seu PDF Adobe Acrobat (Acroform) para a instância do AEM Forms. Execute as seguintes etapas para configurar um Formulário adaptável para usar o Adobe Acrobat PDF (Acroform) como modelo para o Documento de registro:

1. Na instância do autor do Experience Manager, clique em **[!UICONTROL Forms]** > **[!UICONTROL Forms e documentos].**
1. Selecione um formulário ou **[!UICONTROL Criar um formulário adaptável]** e clique em **[!UICONTROL Propriedades]**.
1. Na janela Propriedades, toque em **[!UICONTROL Modelo de formulário]**.
1. No  **[!UICONTROL Modelo de formulário]** na guia , no **[!UICONTROL Selecionar de]** , selecione **[!UICONTROL Modelo de dados do formulário]**, **[!UICONTROL Esquema]** ou **[!UICONTROL Nenhum]**. Também é possível selecionar um modelo de formulário ao criar um formulário.
1. Na seção Document of Record Template Configuration da guia Form Model , selecione **Associar Modelo de Formulário como Documento de Modelo de Registro**. Ao selecionar essa opção, todos os PDF Acrobat disponíveis em sua máquina são exibidos. Selecione o formulário que deseja usar.
1. Clique em **[!UICONTROL Feito.]**

O Formulário adaptável agora está configurado para usar um Acroform como modelo para o Documento de registro. As próximas etapas são para [vincular componentes do formulário adaptável aos campos de modelo correspondentes](#bind-adaptive-form-components-with-template-fields).

## Gerar automaticamente um Documento de Registro {#auto-generate-a-document-of-record}

Quando um Formulário adaptável é configurado para gerar automaticamente um Documento de registro, sempre que um formulário é alterado, seu Documento de registro é atualizado imediatamente. Por exemplo, se um campo for removido de um formulário adaptável existente, o campo correspondente também será removido e não estará visível no Documento de registro. Há muitas outras vantagens de gerar automaticamente o Documento de registro:

* Os desenvolvedores de formulários não precisam manter os vínculos de dados manualmente. O Documento de registro gerado automaticamente cuida de atualizações relacionadas ao vínculo de dados.
* Os desenvolvedores de formulários não precisam ocultar manualmente os campos que estão marcados como excluídos do Documento de registro. O Documento de registro gerado automaticamente é pré-configurado para excluir esses campos.
* A opção Documento de registro gerado automaticamente economiza o tempo necessário para criar um modelo de formulário para o Documento de registro.
* A opção Documento de registro gerado automaticamente permite que você use diferentes estilos e aparências usando diferentes modelos base. Ajuda a selecionar o melhor estilo e aparência do Documento de registro para sua organização. Se você não especificar estilos, os estilos do sistema serão definidos como padrão.
* O Documento de registro gerado automaticamente garante que qualquer alteração no formulário seja refletida imediatamente no Documento de registro.

Execute as seguintes etapas para configurar um Formulário adaptável para gerar automaticamente um Documento de registro:

1. Na instância do autor do Experience Manager, clique em **[!UICONTROL Forms]** > **[!UICONTROL Forms e documentos].**
1. Selecione um formulário ou Crie um formulário adaptável e clique em **[!UICONTROL Propriedades]**.
1. Na janela Propriedades, toque em **[!UICONTROL Modelo de formulário]**.
1. No  **[!UICONTROL Modelo de formulário]** na guia , no **[!UICONTROL Selecionar de]** , selecione **[!UICONTROL Modelo de dados do formulário]**, **[!UICONTROL Esquema]** ou **[!UICONTROL Nenhum]**. Também é possível selecionar um modelo de formulário ao criar um formulário.
1. Na seção Document of Record Template Configuration da guia Form Model , selecione **Gerar Documento de Registro**.
1. Clique em **[!UICONTROL Feito.]**

## Vincular componentes do formulário adaptável com campos de modelo {#bind-adaptive-form-components-with-template-fields}

Vincule campos de formulário adaptável com campos de modelo para exibir dados de formulário capturados no campo Documento de registro correspondente. Para vincular componentes do Formulário adaptável ao documento correspondente dos campos do modelo de registro:

1. Abra o Formulário adaptável, configurado para usar um modelo de formulário personalizado para edição.

1. Selecione um componente de Formulário adaptável e clique em abrir Configurar ![Configurar](assets/Smock_Wrench_18_N.svg) ícone . Ele abre o navegador de propriedades.

1. No navegador de propriedades, navegue e selecione um campo.

   * (Para o modelo AcroForm) a variável **[!UICONTROL Documento do campo Referência da associação de registros]** propriedade.
   * (Para modelo XFA) a variável **[!UICONTROL Referência de associação do modelo de dados]** propriedade.

1. Clique em **[!UICONTROL Salvar]**.

<!-- 
In the following video Adaptive Form components are binded with corresponding Acroform template fields and the Document of Record is sent as an email attachment.
-->

Você pode usar ações de envio, como &quot;Enviar email&quot;, &quot;Chamar um fluxo de trabalho AEM&quot;, &quot;Chamar um fluxo do Power Automate&quot; e outras [Enviar ações](configuring-submit-actions.md) para receber um documento de registro.
![Ações de envio de imagem](/help/forms/assets/submit-actions-img.png)



## Atualizações incrementais no modelo de Documento de registro {#document-of-record-template-incremental-updates}

Os formulários adaptáveis e o documento correspondente dos modelos de registro podem evoluir ao longo do tempo. Você pode optar por adicionar, remover ou modificar campos em um formulário adaptável ou em um modelo de documento de registro.

Quando você faz alterações em um modelo de Documento de registro e carrega o modelo de Documento de registro alterado no AEM Forms, o editor de Adaptive Forms detecta automaticamente os vínculos alterados e informa sobre os componentes de formulário adaptáveis que exigem novos vínculos. Ele permite fazer atualizações incrementais em um modelo de Documento de registro.

Por exemplo, uma Organização, *We.Retail*, tem um modelo de Documento de registro baseado em AcroForm, *we-retail-fatura.pdf*. O modelo tem a seguinte aparência:

![Modelo original](assets/we-retail-invoice.png)

Depois de usar o modelo por algum tempo, a organização decide renomear `invoice-number` campo para `bill-number` e capturar o endereço de email dos compradores. Um desenvolvedor atualiza o nome da variável `invoice-number` e adiciona um campo de email ao modelo. Ele também cria uma nova versão do modelo chamada  *we-retail-Invoice-v2.pdf*.

![Modelo atualizado](assets/we-retail-new-invoice.png)

<!--

The developer uploads and applies to the updated template to the adaptive form. The adaptive form automatically detects and displays list of fields where binding has changed.

![Binding Error](assets/we-retail-binding-error.png)

The form developer binds Adaptive Forms fields with corresponding Document of Record template.

-->

>[!VIDEO](assets/we-retail-binding.mp4)

Agora, quando o Formulário adaptativo é enviado, um Documento de registro atualizado é gerado.

![Atualização dos pacotes-](assets/we-retail-new-invoice-sent-to-customer.png)

## Principais considerações ao trabalhar com o Documento de registro {#key-considerations-when-working-with-document-of-record}

Lembre-se das considerações e limitações a seguir ao trabalhar no Documento de registro do Adaptive Forms.

* Os modelos de Documento de registro não suportam rich text. Portanto, qualquer rich text no Formulário adaptativo estático ou nas informações preenchidas pelo usuário final aparece como texto simples no Documento de registro.
* Os fragmentos de documento em um formulário adaptável não aparecem no Documento de registro. No entanto, os Fragmentos de formulário adaptáveis são compatíveis.
* Não há suporte para vínculo de conteúdo no Documento de registro gerado para o Formulário adaptável baseado no esquema XML.
* A versão localizada do Documento de registro é criada sob demanda para uma localidade quando o usuário solicita a renderização do Documento de registro. A localização do documento de registro ocorre juntamente com a localização do formulário adaptável. <!-- For more information on localization of Document of Record and Adaptive Forms see Using AEM translation workflow to localize Adaptive Forms and Document of Record.-->

<!-- ## Configure an adaptive form to generate  Document of Record {#adaptive-form-types-and-their-documents-of-record}

While creating an adaptive form, in the Form Model tab of Adaptive Form properties, select one the following option: 

* **None**
  Select the option to create an Adaptive Form without a form model. When the option is selected, the Document of Record is automatically generated for your Adaptive Form.

* **[Associate form template as a Document of Record template](creating-adaptive-form.md#create-an-adaptive-form-based-on-an-xfa-form-template)**
  
  Select the option to use an XFA Form as a template for Document of Record. 

* **[Generate Document of Record](creating-adaptive-form.md#create-an-adaptive-form-based-on-xml-or-json-schema)**
  Select the option to use an XFA Form as a template. When the option is selected, the Document of Record is automatically generated for your Adaptive Form. When you use an XML schema as a template for an Adaptive Form, ensure that the adaptive form and associated XFA Form use the same XML schema as your Adaptive Form
  

When you select a form model, configure Document of Record using options available under Document of Record Template Configuration. See [Document of Record Template Configuration](#document-of-record-template-configuration). -->

## Mapeamento de elementos de formulário adaptável {#mapping-of-adaptive-form-elements}

A tabela a seguir descreve os componentes do Formulário adaptável e os componentes XFA correspondentes e se eles forem exibidos em um Documento de registro.

### Campos {#fields}

<table>
 <tbody>
  <tr>
   <th>Componente de formulário adaptável</th>
   <th>Componente XFA correspondente</th>
   <th>Incluído por padrão no Documento de modelo de registro?</th>
   <th>Notas</th>
  </tr>
  <tr>
   <td>Botão</td>
   <td>Botão</td>
   <td>falso</td>
   <td> </td>
  </tr>
  <tr>
   <td>Caixa de seleção</td>
   <td>Caixa de seleção</td>
   <td>verdadeiro</td>
   <td> </td>
  </tr>
  <tr>
   <td>Seletor de data</td>
   <td>Campo de data/hora</td>
   <td>verdadeiro</td>
   <td> </td>
  </tr>
  <tr>
   <td>Lista suspensa</td>
   <td>Lista suspensa</td>
   <td>verdadeiro</td>
   <td> </td>
  </tr>
  <tr>
   <td>Caixa numérica</td>
   <td>Campo numérico</td>
   <td>verdadeiro</td>
   <td> </td>
  </tr>
  <tr>
   <td>Botão de opção</td>
   <td>Botão de opção</td>
   <td>verdadeiro</td>
   <td> </td>
  </tr>
  <tr>
   <td>Caixa de texto</td>
   <td>Campo de texto</td>
   <td>verdadeiro</td>
   <td> </td>
  </tr>
  <tr>
   <td>Botão de redefinição</td>
   <td>Botão Redefinir</td>
   <td>falso</td>
   <td> </td>
  </tr>
  <tr>
   <td>Botão Enviar</td>
   <td><p>Botão Enviar por email</p> <p>Botão Enviar por HTTP</p> </td>
   <td>falso</td>
   <td> </td>
  </tr>
  <tr>
   <td>Anexo de arquivo</td>
   <td> </td>
   <td>falso</td>
   <td>Não disponível no modelo Documento de registro. Disponível apenas no Documento de registro através de anexos.</td>
  </tr>
 </tbody>
</table>

### Contêineres {#containers}

<table>
 <tbody>
  <tr>
   <th>Componente de formulário adaptável</th>
   <th>Componente XFA correspondente</th>
   <th>Notas</th>
  </tr>
  <tr>
   <td>Painel<br /> </td>
   <td>Subformulário<br /> </td>
   <td>O painel repetível mapeia para subformulário repetível.</td>
  </tr>
 </tbody>
</table>

### Componentes estáticos {#static-components}

| Componente de formulário adaptável | Componente XFA correspondente | Notas |
|---|---|---|
| Imagem | Imagem | Os componentes TextDraw e Image, vinculados ou não, sempre aparecem no Documento de registro para um Formulário adaptável baseado em XSD, a menos que sejam excluídos usando as configurações de Documento de registro. |
| Texto | Texto |

### Tabelas {#tables}

Os componentes da tabela Adaptive Forms, como cabeçalho, rodapé e mapa de linha para os componentes XFA correspondentes. Você pode mapear painéis repetitivos para tabelas no Documento de registro.

## Modelo base de um Documento de Registro {#base-template-of-a-document-of-record}

O modelo base fornece informações de estilo e aparência ao Documento de registro. Ele permite personalizar a aparência padrão do Documento de registro gerado automaticamente. Por exemplo, você pode usar um modelo básico para adicionar o logotipo de sua empresa no cabeçalho e as informações de direitos autorais no rodapé do Documento de registro.

A página principal de um modelo base é usada como uma página principal para o modelo Documento de registro. A página mestre pode ter informações como um cabeçalho de página, rodapé de página e número de página que você pode aplicar ao Documento de registro. Você pode aplicar essas informações ao Documento de Registro usando o modelo base para a geração automática do Documento de Registro. Usar um template base permite alterar as propriedades padrão dos campos.

Sempre siga [Convenções de modelo básico](#base-template-conventions) ao criar o modelo base.

## Convenções de modelo básico {#base-template-conventions}

Um modelo base é usado para definir o cabeçalho, o rodapé, o estilo e a aparência de um Documento de registro. O cabeçalho e o rodapé podem incluir informações como o logotipo da empresa e o texto de direitos autorais. A primeira página principal no modelo base é copiada e usada como uma página principal para o Documento de registro, que contém um cabeçalho, rodapé, número de página ou qualquer outra informação que deve aparecer em todas as páginas no Documento de registro. Se você usar um modelo base que não esteja em conformidade com as convenções do modelo base, a primeira página principal do modelo base ainda será usada no modelo Documento de registro. É altamente recomendável criar seu modelo base de acordo com suas convenções e usá-lo para a geração automática do Documento de registro.

**Convenções de página principais**

* No modelo base, nomeie o subformulário raiz como `AF_METATEMPLATE` e a página principal como `AF_MASTERPAGE`.

* A página principal com o nome `AF_MASTERPAGE` localizada na `AF_METATEMPLATE` o subformulário raiz é preferido para extrair informações de cabeçalho, rodapé e estilo.

* If `AF_MASTERPAGE` estiver ausente, a primeira página principal presente no template base será usada.

**Convenções de estilo para campos**

* Para aplicar estilo aos campos no Documento de registro, o modelo base fornece campos localizados na variável `AF_FIELDSSUBFORM` subformulário do `AF_METATEMPLATE` subformulário raiz.

* As propriedades desses campos são aplicadas aos campos no Documento de registro. Esses campos devem seguir o `AF_<name of field in all caps>_XFO` convenção de nomenclatura. Por exemplo, o nome do campo para a caixa de seleção deve ser `AF_CHECKBOX_XFO`.

Para criar um modelo base, faça o seguinte no Forms Designer.

1. Clique em **[!UICONTROL Arquivo]** > **[!UICONTROL Novo]**.
1. Selecione o **[!UICONTROL Baseado em um modelo]** opção.

1. Selecione o **[!UICONTROL Forms - Documento de registro]** categoria .
1. Selecionar **[!UICONTROL Modelo Base DoR]**.
1. Clique em **[!UICONTROL Próximo]** e fornecer as informações necessárias.

1. (Opcional) Modifique o estilo e a aparência dos campos que você deseja aplicar aos campos no Documento de registro.
1. Salve o formulário.
   ![Propriedades básicas](/help/forms/assets/form-designer-dor-img.png)

Agora você pode usar o formulário salvo como modelo base para um Documento de registro. Não modifique ou remova nenhum script presente no modelo base.

**Modificação do modelo base**

* Não aplique nenhum estilo sobre campos no template base, é aconselhável remover esses campos do template base para que todas as atualizações no template base sejam selecionadas automaticamente.
* Ao modificar o modelo base, não remova, adicione ou modifique scripts.

Siga rigorosamente as convenções acima mencionadas e as instruções para criar um modelo base.

## Personalizar as informações da marca no Documento de registro {#customize-the-branding-information-in-document-of-record}

Ao gerar um Documento de Registro, você pode alterar as informações de marca do Documento de Registro na guia Documento de Registro. A guia Documento de registro inclui opções como logotipo, aparência, layout, cabeçalho e rodapé, aviso de isenção de responsabilidade e se você deseja ou não incluir as opções de caixa de seleção e botão de opção não selecionadas.

Para localizar as informações de marca inseridas na guia Document of Record , verifique se a localidade do navegador está definida corretamente. Para personalizar as informações de marca do Documento de registro, execute as seguintes etapas:

1. Selecione um painel (painel raiz) no Documento de registro e toque em ![configure](assets/configure.png).
1. Toque ![dortab](assets/dortab.png). A guia Document of Record é exibida.
1. Selecione o modelo padrão ou um modelo personalizado para renderizar o Documento de registro. Se você selecionar o modelo padrão, uma visualização em miniatura do Documento de registro será exibida abaixo do menu suspenso Modelo.
1. Com base na seleção de um modelo padrão ou personalizado, algumas ou todas as propriedades a seguir serão exibidas na guia Documento de registro. Especifique as propriedades mencionadas abaixo para definir a aparência do Documento de registro:

   1. **Propriedades básicas**:
      * **Modelo**: Se quiser selecionar um modelo personalizado, navegue e selecione um XDP no [!DNL AEM Forms] servidor. Se quiser usar um modelo que não esteja disponível em seu [!DNL AEM Forms] primeiro faça upload do XDP em seu [!DNL AEM Forms] servidor.
      * **Cor do destaque**: A cor na qual o texto do cabeçalho e as linhas separadoras são renderizados no documento de PDF de registro.
      * **Família de fontes**: Família de fontes do texto no PDF Documento de registro.

      * **Incluir objetos de formulário que não estão vinculados ao modelo de dados**: A configuração da propriedade inclui campos não vinculados do Formulário adaptável baseado em esquema no Documento de registro.
      <!-- **Exclude hidden fields from the Document of Record**: Setting the property identifies the hidden fields for exclusion from Document of Record.-->

      * **Ocultar descrição de painéis**: A configuração da propriedade exclui a descrição do painel/tabela do Documento de registro. Aplicável para painel e tabela.
   1. **Propriedades do campo de formulário**:
      * **Para os componentes Caixa de seleção e Botão de opção , mostrar somente os valores selecionados**: A configuração da propriedade exibe apenas os valores selecionados da caixa de seleção e do botão de opção em [!UICONTROL Documento de registro].
      * **Separador para vários valores**: É possível escolher qualquer separador, como vírgula ou quebra de linha, para exibir vários valores.
      * **Alinhamento de opções**: Você pode selecionar o alinhamento desejado (horizontal, vertical, igual ao formulário adaptável) para definir o alinhamento dos campos, como caixa de seleção ou botão de opção a serem exibidos em [!UICONTROL Documento de registro]. Por padrão, o alinhamento vertical é definido para os campos em [!UICONTROL Documento de registro]. A configuração das propriedades na [!UICONTROL Propriedades do campo de formulário] do DoR substitui as propriedades definidas no [!UICONTROL Alinhamento de Item] para os campos em um formulário adaptável. Nesse caso, selecione [!UICONTROL Igual ao formulário aptivo] , o alinhamento como configurado em uma instância do autor do formulário adaptável é usado para [!UICONTROL Documento de registro] campos.
      * **Número de opções para alinhamento horizontal**: é possível definir o número de opções a serem exibidas no Documento de registro para o alinhamento horizontal.
   1. **Página principal  Propriedades**:
      * **Imagem do logotipo**: Você pode optar por usar a imagem do logotipo do Formulário adaptável, escolher um DAM ou fazer upload de um de seu computador.
      * **Título do formulário**: Título do DoR.
      * **Texto do cabeçalho**: Texto que aparece na seção de cabeçalho do Documento de registro.
      * **Rótulo de isenção de responsabilidade**: Rótulo de isenção de responsabilidade.
      * **Isenção de responsabilidade**: Texto que especifica o âmbito dos direitos e obrigações do Documento de Registro.
      * **Texto de isenção de responsabilidade**: Texto de isenção de responsabilidade.
      ![Página principal  Propriedades](/help/forms/assets/dorpropertiesimg.png)
   >[!NOTE]
   >
   >Se você estiver usando um modelo de Formulário adaptável criado com uma versão do Designer anterior à 6.3, para que as propriedades Cor do destaque e Família de fontes funcionem, verifique se o seguinte está presente no modelo de Formulário adaptável abaixo do subformulário raiz:

   ```xml
   <proto>
   <font typeface="Arial"/>
   <fill>
   <color value="4,166,203"/>
   </fill>
   <edge>
   <color value="4,166,203"/>
   </edge>
   </proto>
   ```

1. Para salvar as alterações da marca, toque em **[!UICONTROL Concluído]**.



## Layouts de tabela e coluna para painéis no Documento de registro {#table-and-column-layouts-for-panels-in-document-of-record}

O formulário adaptável pode ser longo, com vários campos de formulário. Talvez você não queira salvar um Documento de registro como uma cópia exata do formulário adaptável. Agora é possível escolher um layout de tabela ou coluna para salvar um ou mais painéis de Formulário adaptável no Document of Record PDF.

Antes de gerar um Documento de registro, nas configurações de um painel, selecione Layout para o documento de registro desse painel como Tabela ou Coluna. Os campos no painel são organizados adequadamente no Documento de registro.

![Campos em um painel renderizado em um layout de tabela no Documento de registro](assets/dortablelayout.png)

Campos em um painel renderizado em um layout de tabela no Documento de registro

![Campos em um painel renderizado em um layout de coluna no Documento de registro](assets/dorcolumnlayout.png)

Campos em um painel renderizado em um layout de coluna no Documento de registro

## Configurações do documento de registro {#document-of-record-settings}

As configurações Documento de registro permitem que você escolha as opções que deseja incluir no Documento de registro. Por exemplo, um banco aceita nome, idade, número de segurança social e número de telefone em um formulário. O formulário gera um número de conta bancária e detalhes da ramificação. Você pode optar por exibir somente o nome, o número da segurança social, a conta bancária e os detalhes da ramificação no Documento de registro.

A configuração do componente Documento de registro está disponível em suas propriedades. Para acessar as propriedades de um componente, selecione o componente e clique em ![cmppr](assets/cmppr.png) na sobreposição. As propriedades são listadas na barra lateral e você pode encontrar as seguintes configurações nela.

**Configurações de nível de campo**

* **Excluir do documento de registro**: A definição da propriedade true exclui o campo do Documento de registro. Esta é uma propriedade com função de script chamada `excludeFromDoR`. Seu comportamento depende de **Excluir campos do DoR se ocultos** propriedade de nível de formulário.

* **Exibir painel como tabela:** Definir a propriedade exibe o painel como tabela no Documento de registro se o painel tiver menos de 6 campos. Aplicável somente para painel.
* **Excluir título do Documento de registro:** A configuração da propriedade exclui o título do painel/tabela do Documento de registro. Aplicável somente para painel e tabela.
* **Excluir descrição do documento de registro:** A configuração da propriedade exclui a descrição do painel/tabela do Documento de registro. Aplicável somente para painel e tabela.

**Configurações de nível de formulário**

* **Incluir campos não vinculados em DoR:** A configuração da propriedade inclui campos não vinculados do Formulário adaptável baseado em esquema no documento de registro. Por padrão, é verdadeiro.
<!-- **Exclude fields from DoR if hidden:** Set the property to exclude the hidden fields from Document of Record at form submission. When you enable [Revalidate on server](/help/forms/configuring-submit-actions.md#server-side-revalidation-in-adaptive-form-server-side-revalidation-in-adaptive-form), the server recomputes the hidden fields before excluding those fields from the Document of Record.->>