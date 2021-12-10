---
title: Gerar documento de registro para Forms adaptável
description: Explica como você pode gerar um modelo para um Documento de registro (DoR) para Adaptive Forms.
exl-id: 15540644-c0c3-45ce-97d3-3bdaa16fb4b6
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '2926'
ht-degree: 3%

---

# Gerar documento de registro para Forms adaptável

## Visão geral {#overview}

Quando um formulário é preenchido ou enviado, é possível manter um registro do formulário, em formato impresso ou documento. Este registro é conhecido como Documento de Registro (DoR). É uma cópia fácil de imprimir do formulário enviado. Você também pode consultar o documento de registro para as informações que os clientes preencheram posteriormente ou usar o Documento de registro para arquivar formulários e conteúdo juntos no Formato PDF.

![Documento do registro](assets/document-of-record.png)

Para criar um Documento de registro, um modelo baseado em XFA ou Acroform é unido aos dados coletados por um formulário adaptável. Você pode gerar um Documento de registro automaticamente ou sob demanda.
A opção sob demanda permite especificar um modelo personalizado baseado em XFA ou Acroform para fornecer uma aparência personalizada ao seu Documento de registro.

É possível:

* [Gerar um documento de registro baseado em XFA](#generate-an-XFA-based-document-of-record)
* [Gerar um documento de registro baseado em formulário (Acrobat Form PDF)](#generate-an-Acroform-based-document-of-record)
* [Gerar automaticamente um Documento de Registro](#auto-generate-a-document-of-record)

## Antes de você iniciar {#components-to-automatically-generate-a-document-of-record}

Antes de começar a aprender e a preparar os ativos necessários para um Documento de registro:

**Modelo base:** Um modelo XFA (arquivo XDP) criado AEM Designer ou um formulário Acrobat (AcroForm). [Modelo base](#base-template-of-a-document-of-record) é usada para especificar informações de estilo e identidade visual para um Documento de registro. Faça upload do seu modelo XFA (arquivo XDP) para a sua instância do AEM Forms antes de

**Formulário adaptável:** Um formulário adaptável para o qual o documento de registro deve ser gerado.

## Gerar um documento de registro baseado em XFA {#generate-an-XFA-based-document-of-record}

Carregue seu modelo XFA (arquivo XDP) na instância do AEM Forms. Execute as seguintes etapas para configurar um Formulário adaptável para usar o modelo XFA (arquivo XDP) como modelo para o Documento de registro:

1. Em AEM instância do autor, clique em **[!UICONTROL Forms]** > **[!UICONTROL Forms e documentos].**
1. Selecione um formulário e clique em **[!UICONTROL Propriedades]**.
1. Na janela Propriedades, toque em **[!UICONTROL Modelo de formulário]**.
1. No  **[!UICONTROL Modelo de formulário]** na guia , no **[!UICONTROL Selecionar de]** , selecione **[!UICONTROL Esquema]** ou **[!UICONTROL Nenhum]**. Também é possível selecionar um modelo de formulário ao criar um formulário.
1. Na seção Document of Record Template Configuration da guia Form Model , selecione **Associar Modelo de Formulário como Documento de Modelo de Registro**. Ao selecionar essa opção, todos os modelos XFA (arquivos XDP) disponíveis em sua máquina são exibidos. Selecione o arquivo apropriado. Além disso, verifique se o mesmo esquema (esquema de dados) é usado para o Formulário adaptável e para o modelo XFA selecionado (arquivo XDP).
1. Clique em **[!UICONTROL Feito.]**

Seu formulário adaptável agora está configurado para usar um arquivo XDP como modelo para o Documento de registro. As próximas etapas são para [vincular componentes do formulário adaptável aos campos de modelo correspondentes](#bind-adaptive-form-components-with-template-fields).

## Gerar um documento de registro baseado em formulário {#generate-an-Acroform-based-document-of-record}

Faça upload do seu PDF Adobe Acrobat (Acroform) para a instância do AEM Forms. Execute as seguintes etapas para configurar um Formulário adaptável para usar o Adobe Acrobat PDF (Acroform) como modelo para o Documento de registro:

1. Em AEM instância do autor, clique em **[!UICONTROL Forms]** > **[!UICONTROL Forms e documentos].**
1. Selecione um formulário e clique em **[!UICONTROL Propriedades]**.
1. Na janela Propriedades, toque em **[!UICONTROL Modelo de formulário]**.
1. No  **[!UICONTROL Modelo de formulário]** na guia , no **[!UICONTROL Selecionar de]** , selecione **[!UICONTROL Esquema]** ou **[!UICONTROL Nenhum]**. Também é possível selecionar um modelo de formulário ao criar um formulário.
1. Na seção Document of Record Template Configuration da guia Form Model , selecione **Associar Modelo de Formulário como Documento de Modelo de Registro**. Ao selecionar essa opção, todo o Acrobat PDF (Acroform) disponível em sua máquina será exibido. Selecione o arquivo apropriado.
1. Clique em **[!UICONTROL Feito.]**

O Formulário adaptável agora está configurado para usar um Acroform como modelo para o Documento de registro. As próximas etapas são para [vincular componentes do formulário adaptável aos campos de modelo correspondentes](#bind-adaptive-form-components-with-template-fields).

## Gerar automaticamente um Documento de Registro {#auto-generate-a-document-of-record}

Quando um Formulário adaptável é configurado para gerar automaticamente um Documento de registro, sempre que um formulário é alterado, seu Documento de registro é atualizado imediatamente. Por exemplo, se um campo for removido de um formulário adaptável existente, o campo correspondente também será removido e não estará visível no Documento de registro. Há muitas outras vantagens de gerar automaticamente o Documento de Registro. :

* Os desenvolvedores de formulários não precisam manter os vínculos de dados manualmente. O Documento de registro gerado automaticamente cuida de atualizações relacionadas ao vínculo de dados.
* Os desenvolvedores de formulários não precisam ocultar manualmente os campos que estão marcados como excluídos do Documento de registro. O Documento de Registros gerado automaticamente é pré-configurado para excluir esses campos.
* A opção Documento de registro gerado automaticamente economiza o tempo necessário para criar um modelo de formulário para o Documento de registro.
* A opção Documento de registro gerado automaticamente permite que você use diferentes estilos e aparências usando diferentes modelos base. Ajuda a selecionar o melhor estilo e aparência do Documento de registro para sua organização. Se você não especificar estilos, os estilos do sistema serão definidos como padrão.
* O Documento de Registros Gerado Automaticamente garante que qualquer alteração no formulário seja refletida imediatamente no Documento de Registro.

Execute as seguintes etapas para configurar um Formulário adaptável para gerar automaticamente um Documento de registro:

1. Em AEM instância do autor, clique em **[!UICONTROL Forms]** > **[!UICONTROL Forms e documentos].**
1. Selecione um formulário e clique em **[!UICONTROL Propriedades]**.
1. Na janela Propriedades, toque em **[!UICONTROL Modelo de formulário]**.
1. No  **[!UICONTROL Modelo de formulário]** na guia , no **[!UICONTROL Selecionar de]** , selecione **[!UICONTROL Esquema]** ou **[!UICONTROL Nenhum]**. Também é possível selecionar um modelo de formulário ao criar um formulário.
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

Você pode usar Enviar email, AEM a ação Enviar fluxo de trabalho juntamente com [Etapa Documento de registro e outras ações de envio](configuring-submit-actions.md) para receber um documento de registro.

## Atualizações incrementais no modelo de Documento de registro {#document-of-record-template-incremental-updates}

Os formulários adaptáveis e o documento correspondente dos modelos de registro podem evoluir ao longo do tempo. Você pode optar por adicionar, remover ou modificar campos em um formulário adaptável ou em um modelo de documento de registro.

Quando você faz alterações em um modelo de Documento de registro e carrega o modelo de Documento de registro alterado no AEM Forms, o editor de Adaptive Forms detecta automaticamente os vínculos alterados e informa sobre os componentes de formulário adaptáveis que exigem novos vínculos. Ele permite fazer atualizações incrementais em um modelo de Documento de registro.

Por exemplo, uma Organização, *We.Retail*, tem um modelo de Documento de registro baseado em AcroForm, *we-retail-fatura.pdf*. O modelo tem a seguinte aparência:

![Modelo original](assets/we-retail-invoice.png)

Depois de usar o modelo por algum tempo, a organização decide renomear `invoice-number` campo para `bill-number` e capturar o endereço de email dos compradores. Um desenvolvedor atualiza o nome da variável `invoice-number` e adiciona um campo de email ao modelo. Ele também cria uma nova versão de modelo chamada  *we-retail-Invoice-v2.pdf*.

![Modelo atualizado](assets/we-retail-new-invoice.png)

O desenvolvedor faz upload e se aplica ao modelo atualizado para o formulário adaptável. O formulário adaptável detecta e exibe automaticamente a lista de campos onde o vínculo foi alterado.

![Erro de vínculo](assets/we-retail-binding-error.png)

O desenvolvedor do formulário vincula os campos Adaptive Forms ao modelo Documento de registro correspondente.
>[!VIDEO](assets/we-retail-binding.mp4)

Agora, quando o formulário adaptativo é enviado, um Documento de registro atualizado é criado.

![Atualização dos pacotes-](assets/we-retail-new-invoice-sent-to-customer.png)

## Considerações principais ao trabalhar com o Documento de registro {#key-considerations-when-working-with-document-of-record}

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

### Fields {#fields}

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
   <td>Rabiscar a assinatura</td>
   <td>Scribble de assinatura</td>
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
   <td>Caixa de senha</td>
   <td>Campo de senha</td>
   <td>falso</td>
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
   <td><p>Botão Submeter por email</p> <p>Botão Submeter por HTTP</p> </td>
   <td>falso</td>
   <td> </td>
  </tr>
  <tr>
   <td>Termos e condições</td>
   <td> </td>
   <td>verdadeiro</td>
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

O modelo base fornece informações de estilo e aparência ao Documento de registro. Ele permite personalizar a aparência padrão do Documento de registro gerado automaticamente. Por exemplo, você pode usar o modelo base para adicionar o logotipo de sua empresa no cabeçalho e as informações de direitos autorais no rodapé do Documento de registro.

A página principal do modelo base é usada como uma página principal para o modelo Documento de registro. A página principal pode ter informações como cabeçalho de página, rodapé de página e número de página que você pode aplicar ao Documento de registro. Você pode aplicar essas informações ao Documento de registro usando o modelo básico para a geração automática do Documento de registro. O uso do template base permite alterar as propriedades padrão dos campos.

Sempre siga [Convenções de modelo básico](#base-template-conventions) ao criar o modelo base.

## Convenções de modelo básico {#base-template-conventions}

Um modelo base é usado para definir o cabeçalho, o rodapé, o estilo e a aparência de um Documento de registro. O cabeçalho e o rodapé podem incluir informações como o logotipo da empresa e o texto de direitos autorais. A primeira página principal no modelo base é copiada e usada como uma página principal para o Documento de registro, que contém cabeçalho, rodapé, número de página ou qualquer outra informação que deve aparecer em todas as páginas no Documento de registro. Se você usar um modelo base que não esteja em conformidade com as convenções do modelo base, a primeira página principal do modelo base ainda será usada no modelo Documento de registro. É altamente recomendável criar seu modelo base de acordo com suas convenções e usá-lo para a geração automática de Documento de registro.

**Convenções de página principais**

* No modelo base, nomeie o subformulário raiz como `AF_METATEMPLATE` e a página principal como `AF_MASTERPAGE`.

* A página principal com o nome `AF_MASTERPAGE` localizada na `AF_METATEMPLATE` o subformulário raiz é preferido para extrair informações de cabeçalho, rodapé e estilo.

* If `AF_MASTERPAGE` estiver ausente, a primeira página principal presente no template base será usada.

**Convenções de estilo para campos**

* Para aplicar estilo aos campos no Documento de registro, o modelo base fornece campos localizados na variável `AF_FIELDSSUBFORM` subformulário do `AF_METATEMPLATE` subformulário raiz.

* As propriedades desses campos são aplicadas aos campos no Documento de registro. Esses campos devem seguir o `AF_<name of field in all caps>_XFO` convenção de nomenclatura. Por exemplo, o nome do campo para a caixa de seleção deve ser `AF_CHECKBOX_XFO`.

Para criar um modelo base, faça o seguinte no AEM Designer.

1. Clique em **[!UICONTROL Arquivo]** > **[!UICONTROL Novo]**.
1. Selecione o **[!UICONTROL Baseado em um modelo]** opção.

1. Selecione o **[!UICONTROL Forms - Documento de registro]** categoria .
1. Selecionar **[!UICONTROL Modelo Base DoR]**.
1. Clique em **[!UICONTROL Próximo]** e fornecer as informações necessárias.

1. (Opcional) Modifique o estilo e a aparência dos campos que você deseja aplicar aos campos no Documento de registro.
1. Salve o formulário.

Agora você pode usar o formulário salvo como modelo base para o Documento de registro. Não modifique ou remova nenhum script presente no modelo base.

**Modificação do modelo base**

* Se não aplicar nenhum estilo sobre campos no template base, é aconselhável remover esses campos do template base para que todas as atualizações no template base sejam selecionadas automaticamente.
* Ao modificar o modelo base, não remova, adicione ou modifique scripts.

Siga rigorosamente as convenções acima mencionadas e as instruções para criar um modelo base.

## Personalizar as informações da marca no Documento de registro {#customize-the-branding-information-in-document-of-record}

Ao gerar um Documento de Registro, você pode alterar as informações de marca do Documento de Registro na guia Documento de Registro. A guia Documento de registro inclui opções como logotipo, aparência, layout, cabeçalho e rodapé, aviso de isenção de responsabilidade e se você deseja ou não incluir as opções de caixa de seleção e botão de opção não selecionadas.

Para localizar as informações de marca inseridas na guia Document of Record , verifique se a localidade do navegador está definida corretamente. Para personalizar as informações de marca do Documento de registro, execute as seguintes etapas:

1. Selecione um painel (painel raiz) no Documento de registro e toque em ![configure](assets/configure.png).
1. Toque ![dortab](assets/dortab.png). A guia Document of Record é exibida.
1. Selecione o modelo padrão ou um modelo personalizado para renderizar o Documento de registro. Se você selecionar o modelo padrão, uma visualização em miniatura do Documento de registro será exibida abaixo do menu suspenso Modelo.

   ![modelo de marca](assets/brandingtemplate.png)

   Se você optar por selecionar um modelo personalizado, navegue por um XDP selecionado em seu [!DNL AEM Forms] servidor. Se você quiser usar um modelo que ainda não esteja em seu [!DNL AEM Forms] , primeiro faça upload do XDP em seu [!DNL AEM Forms] servidor.

1. Com base na seleção de um modelo padrão ou personalizado, algumas ou todas as propriedades a seguir serão exibidas na guia Documento de registro. Especifique estes adequadamente:

   * **Imagem do logotipo**: Você pode optar por usar a imagem do logotipo do Formulário adaptável, escolher um DAM ou fazer upload de um de seu computador.
   * **Título do formulário**
   * **Texto do cabeçalho**
   * **Rótulo do aviso**
   * **Aviso**
   * **Texto do aviso**
   * **Cor do destaque**: A cor na qual o texto do cabeçalho e as linhas separadoras são renderizados no PDF de documento ou registro
   * **Família de fontes**: Família de fontes do texto no Document of Record PDF
   * **Para os componentes Caixa de seleção e Botão de opção , mostrar somente os valores selecionados**
   * **Separador para vários valores selecionados**
   * **Incluir objetos de formulário que não estão vinculados ao modelo de dados**
   * **Excluir campos ocultos do Documento de registro**
   * **Ocultar descrição de painéis**

   >[!NOTE]
   >
   >Se estiver usando um modelo de Formulário adaptável criado com uma versão do Designer anterior à 6.3, para que as propriedades Cor do destaque e Família de fontes funcionem, verifique se o seguinte está presente no modelo de Formulário adaptável abaixo do subformulário raiz:

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

1. Para salvar as alterações da marca, toque em Concluído.

## Layouts de tabela e coluna para painéis no Documento de registro {#table-and-column-layouts-for-panels-in-document-of-record}

O formulário adaptável pode ser longo, com vários campos de formulário. Talvez você não queira salvar um Documento de registro como uma cópia exata do formulário adaptável. Agora é possível escolher um layout de tabela ou coluna para salvar um ou mais painéis de Formulário adaptável no Document of Record PDF.

Antes de gerar um Documento de registro, nas configurações de um painel, selecione Layout para o documento de registro desse painel como Tabela ou Coluna. Os campos no painel são organizados adequadamente no Documento de registro.

![Campos em um painel renderizado em um layout de tabela no Documento de registro](assets/dortablelayout.png)

Campos em um painel renderizado em um layout de tabela no Documento de registro

![Campos em um painel renderizado em um layout de coluna no Documento de registro](assets/dorcolumnlayout.png)

Campos em um painel renderizado em um layout de coluna no Documento de registro

## Configurações do documento de registro {#document-of-record-settings}

As configurações Documento de registro permitem que você escolha as opções que deseja incluir no Documento de registro. Por exemplo, um banco aceita nome, idade, número de segurança social e número de telefone em um formulário. O formulário gera um número de conta bancária e detalhes da ramificação. Você pode optar por exibir somente o nome, o número da segurança social, a conta bancária e os detalhes da ramificação no Documento de registro.

As configurações de Documento de registro de um componente estão disponíveis em suas propriedades. Para acessar as propriedades de um componente, selecione o componente e clique em ![cmppr](assets/cmppr.png) na sobreposição. As propriedades são listadas na barra lateral e você pode encontrar as seguintes configurações nela.

**Configurações de nível de campo**

* **Excluir do documento de registro**: A definição da propriedade true exclui o campo do Documento de registro. Esta é uma propriedade com função de script chamada `excludeFromDoR`. Seu comportamento depende de **Excluir campos do DoR se ocultos** propriedade de nível de formulário.

* **Exibir painel como tabela:** Definir a propriedade exibe o painel como tabela no Documento de registro se o painel tiver menos de 6 campos. Aplicável somente para painel.
* **Excluir título do Documento de registro:** A configuração da propriedade exclui o título do painel/tabela do Documento de registro. Aplicável somente para painel e tabela.
* **Excluir descrição do documento de registro:** A configuração da propriedade exclui a descrição do painel/tabela do Documento de registro. Aplicável somente para painel e tabela.

**Configurações de nível de formulário**

* **Incluir campos não vinculados em DoR:** A configuração da propriedade inclui campos não vinculados do Formulário adaptável baseado em esquema no documento de registro. Por padrão, é verdadeiro.
* **Excluir campos de DoR se ocultos:** A configuração da propriedade substitui o comportamento da propriedade de nível de campo &quot;Excluir do documento de registro&quot; quando não é verdadeira. Se os campos estiverem ocultos no momento do envio do formulário, eles serão excluídos do Documento de registro se a propriedade estiver definida como true, desde que a propriedade &quot;Excluir do documento de registro&quot; não esteja definida.
