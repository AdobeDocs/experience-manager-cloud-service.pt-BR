---
title: Gerenciar metadados
seo-title: Manage [!DNL AEM Forms] metadata
description: Os metadados facilitam a categorização e a organização de ativos e ajudam os usuários que procuram um ativo específico.
seo-description: Metadata allows for easier categorization and organization of assets and helps users who are looking for a specific asset.
exl-id: 8527246a-37f0-4d43-a49e-1c76c265514e
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '1658'
ht-degree: 2%

---

# Adicionar, remover ou editar metadados de um Formulário adaptável {#manage-form-metadata}

Os metadados facilitam a categorização e a organização de ativos e ajudam os usuários que procuram um ativo específico.

[!DNL AEM Forms]O, por padrão, fornece um conjunto definido de metadados para cada tipo de ativo. Além dos metadados padrão, é possível adicionar metadados personalizados a cada um dos tipos de ativos. [!DNL AEM Forms] O também fornece o meio certo de criar, gerenciar e trocar todos esses metadados de forma eficiente para seus formulários.

<!-- If you're a developer or a site owner, you can customize Forms Portal, the end-user interface for [!DNL AEM Forms] to reflect the metadata you're using in your organization. For more information abouts Forms Portal, see [Introduction to publishing forms on a portal](introduction-publishing-forms.md). -->

## Metadados no [!DNL AEM Forms] {#metadata-in-aem-forms}

Entrada [!DNL AEM Forms], a lista de propriedades de metadados associada a um ativo depende do seu tipo. Além disso, se você adicionar qualquer propriedade de metadados personalizada, ela será adicionada em todos os ativos do tipo em que os metadados personalizados foram adicionados.

### Tipos de ativos {#asset-types}

Os seguintes tipos de ativos são compatíveis com o [!DNL AEM Forms]:

* Modelos de formulário (formulários XFA)
* PDF forms
* Documento (PDF simples)
* Adaptive Forms
* Modelo de dados do Forms
* XFS

#### Ampla lista de metadados {#extensive-list-of-metadata}

Veja a seguir uma extensa lista de propriedades de metadados compatíveis com o [!DNL AEM Forms]:

<table>
 <tbody> 
  <tr> 
   <td><strong>Nome da propriedade</strong></td> 
   <td><strong>Tipo de ativo</strong></td> 
   <td><strong>Descrição</strong><br /> </td> 
  </tr> 
  <tr> 
   <td>Título</td> 
   <td>Todos, exceto o recurso</td> 
   <td>Nome de exibição do ativo.<br /> </td> 
  </tr> 
  <tr> 
   <td>Descrição</td> 
   <td>Todos, exceto o recurso</td> 
   <td>Descrição do ativo. O usuário pode especificar esse valor.<br /> </td> 
  </tr> 
  <tr> 
   <td>Tipo</td> 
   <td>Todos</td> 
   <td><p>Um valor somente leitura que especifica o tipo de ativo. Ele pode ter um dos seguintes valores:</p> 
    <ul> 
     <li>Modelo de formulário</li> 
     <li>formulário PDF, formulário PDF (Acroform) ou formulário PDF (Signed)</li> 
     <li>Documento, Documento (Assinado)</li> 
     <li>Formulário adaptável</li> 
     <li>Modelo de dados do formulário</li>
     <li>Recurso</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>Criado</td> 
   <td>Todos</td> 
   <td>Um valor somente leitura que especifica o tempo de criação do ativo.</td> 
  </tr> 
  <tr> 
   <td>Data da última modificação</td> 
   <td>Todos</td> 
   <td>Um valor somente leitura que especifica a hora em que o ativo foi modificado pela última vez.</td> 
  </tr> 
  <tr> 
   <td>Autor</td> 
   <td>Todos, exceto o recurso</td> 
   <td><p>Um valor somente leitura que é automaticamente calculado com base no tipo de formulário.</p> 
    <ul> 
     <li>PDF/Modelo de formulário/Documento - obtido do arquivo binário carregado.</li> 
     <li>Formulário adaptável - Usuário conectado no momento da criação do formulário.</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>Status</td> 
   <td>Todos, exceto o recurso</td> 
   <td><p> Um valor somente leitura que define um dos seguintes estados de um formulário:</p> 
    <ul> 
     <li>Nenhum valor: se um formulário nunca foi publicado.</li> 
     <li>Publicado: quando um formulário é publicado.</li> 
     <li>Modificado: quando um formulário foi modificado depois de ter sido publicado uma vez.</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>Data da última publicação</td> 
   <td>Todos, exceto o recurso</td> 
   <td>Um valor somente leitura que especifica a hora em que o formulário foi publicado pela última vez.</td> 
  </tr> 
  <tr> 
   <td>Publicar hora de ligar/desligar</td> 
   <td>Todos, exceto o recurso</td> 
   <td><p>Hora em que o formulário está agendado para ser publicado/despublicado automaticamente. O usuário define esse valor ao editar metadados.</p> 
    <ul> 
     <li>A data de ativação e desativação da publicação deve ser posterior à data atual. </li> 
     <li>Publicar Fora do Tempo deve estar além de publicar No Tempo. </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>Enviar URL</td> 
   <td><p>Modelo de formulário</p> <p>formulário PDF</p> </td> 
   <td><p>Para configurar uma URL especificada pelo usuário para enviar dados de formulário a um servlet.</p> <p>O URL de envio pode ser configurado usando qualquer um dos métodos a seguir, listados em ordem de precedência:</p> 
    <ul> 
     <li>Especifique um URL de envio diretamente em um Modelo de formulário usando o botão Enviar HTTP ao criar um formulário XFA no AEM Forms Designer.</li> 
     <li>Na interface do usuário do AEM Forms, selecione um formulário e especifique uma URL de envio ao editar as propriedades dos metadados.</li> 
     <!-- <li>In Forms Portal, edit the Search &amp; Lister component and specify a submit URL under the Form Link tab.</li> -->
    </ul> </td> 
  </tr> 
  <tr> 
   <td>Perfil de renderização do HTML</td> 
   <td>Modelo de formulário</td> 
   <td>O perfil de renderização de HTML usado ao renderizar um Modelo de Formulário no formato HTML.</td> 
  </tr> 
  <tr> 
   <td>Renderizar formato</td> 
   <td><p>Modelo de formulário</p> <p>Formulário adaptável</p> </td> 
   <td><p>Essa opção permite que o usuário especifique o formato de renderização do formulário quando os formulários forem publicados:</p> 
    <ul> 
     <li>HTML</li> 
     <li>PDF</li> 
     <li>Ambos</li> 
    </ul> <p>Essa opção é usada para restringir o formato de renderização dos formulários somente no portal de formulários onde eles estão visíveis para o usuário final.</p> </td> 
  </tr> 
  <tr> 
   <td>Tags</td> 
   <td>Todos, exceto o recurso</td> 
   <td>Rótulos associados ao formulário para facilitar a pesquisa rápida e fácil.</td> 
  </tr> 
  <tr> 
   <td>Referências</td> 
   <td><p>Formulário adaptável</p> <p>Modelo de formulário</p> <p>Recurso</p> </td> 
   <td><p>Lista de ativos (outros formulários ou recursos) aos quais este formulário está relacionado. Esses ativos podem estar nas duas categorias a seguir:</p> 
    <ul> 
     <li>Refere-se: ativos aos quais o formulário atual se refere.</li> 
     <li>Referenciado por: Ativos que se referem ao ativo atual.</li> 
    </ul> <p>Esses ativos são exibidos como links e seus metadados podem ser acessados diretamente clicando neles.<br /> </p> </td> 
  </tr> 
  <tr> 
   <td>Seleção do modelo de formulário (XDP/XSD)</td> 
   <td>Formulário adaptável</td> 
   <td><p>Especifica qual modelo de formulário é usado durante a criação do Formulário adaptável. Essa propriedade pode ter os seguintes valores:</p> 
    <ul> 
      <li>Modelo de dados do formulário </li>
      <li>Esquema: um XML do esquema JSON</li>
     <!-- <li>Form template: A form template is selected from the ones existing in the repository. This value can be updated.</li> 
     <li>XML schema: An XSD file is uploaded. This value can be updated.</li> -->
     <li>Nenhum</li> 
    </ul> 
    <div>
      Um modelo de formulário depois de selecionado pode ser atualizado, mas não removido. 
    </div> </td> 
  </tr> 
 </tbody> 
</table>

## Exibir metadados de formulário {#view-form-metadata}

Os ativos têm valores de propriedade existentes, que podem ser exibidos no modo somente leitura. Esses metadados são originados no momento do upload ou da criação do formulário.

1. Navegue até o local do ativo para o qual deseja exibir metadados.

1. Abra a página de propriedades usando uma das seguintes maneiras:

   * Clique em **[!UICONTROL Propriedades]** ![Propriedades](assets/Smock_Info_18_N.svg) ícone de Ações rápidas.

     >[!NOTE]
     >
     >As Ações rápidas são itens de ação exibidos ao passar o mouse sobre uma miniatura.

   * Selecione o formulário e clique no botão **[!UICONTROL Propriedades]** ![Propriedades](assets/Smock_Info_18_N.svg) ícone que aparece na barra de ferramentas.
   * Navegue até a página de detalhes do formulário clicando na miniatura do formulário quando não estiver no modo de seleção. Agora, clique no link ![Propriedades](assets/Smock_Info_18_N.svg) ícone de olho no canto superior direito e, em seguida, clique em Propriedades na lista abaixo.

1. A página de propriedades que é aberta exibe um esquema que contém apenas as propriedades de metadados que têm algum valor.

   <!-- The properties page has a toolbar containing two action icons:

    * Edit: ![Edit](assets/Smock_Edit_18_N.svg) Edit the metadata property values
    * View: ![aem6forms_eye_viewon](assets/aem6forms_eye_viewon.png) Navigate to the form details page, which opens the form in the preview mode. -->

   A parte de conteúdo é dividida em duas partes:

   * O painel esquerdo contém a miniatura do formulário
   * O painel direito contém propriedades de metadados no modo somente leitura, distribuídas em várias guias.

## Adicionar/atualizar valores de metadados de formulário {#add-update-form-metadata-values}

É possível editar o valor das propriedades de metadados existentes ou adicionar novos valores a um campo de propriedade de metadados existente (por exemplo, quando um campo de metadados está em branco).

<!-- ### Update metadata property values {#update-metadata-property-values}

1. Follow the steps mentioned in the previous section to open the properties page where existing metadata of the selected form can be viewed.  

1. From the toolbar, click the Edit icon ![Edit](assets/Smock_Edit_18_N.svg) to change the mode of the page from read-only to read/write.  

1. The properties page that opens holds a schema that contains a mix of editable input fields and static text.  

1. The properties displayed in static text are the ones that you cannot edit.  

1. You can navigate to other tabs to find input fields for metadata properties placed under them.

   This page has a toolbar containing two action icons different from those in view mode:

    * Cancel: ![aem6forms_close](assets/aem6forms_close.svg_w24.png) Cancel any changes made to metadata property values so far
    * Done: ![aem6forms_check](assets/aem6forms_check.png) Save all the changes made to metadata property values so far

   Both these actions direct the user back to read-only mode of the properties page containing the updated values.-->

### Atualizar a miniatura do formulário {#update-the-form-thumbnail}

O painel esquerdo na página de propriedades exibe a miniatura do formulário. Por padrão, a miniatura exibida é a gerada no momento da criação do formulário (Formulário adaptável) ou no momento do upload do formulário.

Para todos os tipos de formulário, você tem a opção de carregar uma imagem clicando em **[!UICONTROL Fazer upload de imagem]** e procure um arquivo de imagem no diretório local. A imagem selecionada é usada como uma miniatura em vez da padrão.

Para o Adaptive Forms, é fornecida uma funcionalidade adicional, que permite que o usuário gere uma miniatura como um instantâneo da visualização atual do Formulário adaptável. Desde [!DNL AEM Forms] O também oferece suporte à criação do Adaptive Forms, a visualização do Formulário adaptável pode mudar sempre que você alterar o Formulário adaptável. Essa funcionalidade de gerar uma miniatura ajuda a obter uma nova miniatura do Formulário adaptável com base no status de visualização atual. Clique em **[!UICONTROL Gerar visualização]** para executar esta ação.

>[!NOTE]
>
>* Use uma imagem quadrada para a miniatura. Quando você usa uma imagem não quadrada e visualiza a miniatura na exibição em lista, a miniatura aparece cortada.
>* Depois que uma nova imagem é carregada ou gerada, a miniatura é substituída por essa imagem e não pode ser redefinida para a imagem anterior.
>

## Adicionar metadados personalizados {#add-custom-metadata}

Além dos metadados fornecidos imediatamente, [!DNL AEM Forms] O oferece suporte aos novos metadados personalizados.

Uma ferramenta (Editor de esquema de metadados) é fornecida para definir o esquema para o layout de metadados; ou seja, o layout do que aparece no **[!UICONTROL Propriedades]** página de um formulário. O Editor de esquema de metadados permite adicionar ou modificar um esquema personalizado para seus ativos.

[!DNL AEM Forms] expõe os esquemas de metadados dos tipos de formulários compatíveis nesta ferramenta. Dessa forma, você pode acessar esses esquemas e usar a funcionalidade fornecida no editor de esquema de metadados para adicionar propriedades personalizadas.

### Navegar pelo editor de esquema de metadados {#navigate-the-metadata-schema-editor}

1. Navegue até **[!UICONTROL Ferramentas > Ativos > Esquemas de metadados]**.

1. Clique em **[!UICONTROL formulários]** dos formulários de esquema listados.

1. Na lista aberta, clique no tipo de ativo ao qual deseja adicionar metadados personalizados.

   >[!NOTE]
   >
   >Esses esquemas contêm propriedades de metadados que são fornecidas prontas para uso e não devem ser alteradas/editadas (marque a caixa de seleção e clique em editar na barra de ferramentas) para evitar problemas funcionais.

1. Qualquer tipo de ativo clicado abre uma lista contendo o `extendedmetadata` opção. Editar este esquema.

1. Marque a caixa de seleção ao lado de `extendedmetadata` e, em seguida, clique no botão Editar ![Editar](assets/Smock_Edit_18_N.svg) ícone que aparece na barra de ferramentas.

1. [!DNL AEM Forms] abre o editor de esquema de metadados/construtor de formulários do tipo de ativo selecionado (neste caso, Formulário adaptável).

   Editor de metadados

   1. O painel esquerdo contém seções com abas, onde os campos são posicionados, e o painel direito exibe todos os componentes de interface do usuário disponíveis e as propriedades do campo selecionado no painel esquerdo.

   1. A seção bloqueada não é editável e contém campos para todas as propriedades de metadados fornecidas imediatamente.

   1. Você pode adicionar guias adicionais clicando no símbolo +.

   1. Você pode adicionar um campo personalizado do tipo desejado arrastando o componente de campo da **[!UICONTROL Formulário de criação]** na página do esquema.
   1. As especificações desse campo podem ser fornecidas no **[!UICONTROL Configurações]** depois de clicar no campo.

### Adicionar propriedade de metadados personalizada no editor de esquema {#add-custom-metadata-property-in-schema-editor}

1. Navegue até a guia (existente ou nova) onde deseja adicionar a propriedade personalizada.

1. Arraste um componente do tipo desejado da **[!UICONTROL Formulário de criação]** seção para o painel esquerdo e coloque-o em um local conveniente.

   >[!NOTE]
   >
   >Não é possível mover as seções bloqueadas, mas você pode colocar o componente em qualquer um dos espaços vazios.

1. Clique em um componente que você acabou de arrastar. Na guia Configurações que é aberta no painel direito, preencha as informações dos seguintes campos:

   1. Especifique um Rótulo de campo para usar como um nome de exibição acima do campo colocado no esquema (Por exemplo: Departamento)
   1. No campo Mapear para propriedade, é possível ver um valor pré-preenchido **&#39;./jcr:content/metadata/default&#39;**. Altere o &#39;**padrão**&#39; para um nome de propriedade desejado, que é usado para armazenar a propriedade no repositório crx (Por exemplo: &#39;./jcr:content/metadata/department&#39;)

      >[!NOTE]
      >
      >Não altere o prefixo &#39;./jcr:content/metadata/&#39;, pois define o caminho onde a propriedade é armazenada.
      >
      >Além disso, o nome da propriedade deve ser exclusivo para evitar a gravação de valores para duas ou mais propriedades no mesmo local no repositório. Portanto, é recomendável alterar o valor &quot;padrão&quot;.

   1. Preencha outras configurações com base no requisito. Por exemplo: selecione a opção Obrigatório se desejar tornar o campo obrigatório.
   1. Para excluir um campo adicionado, selecione-o e clique no link excluir ![Excluir](assets/Smock_Delete_18_N.svg) ícone.

1. Se necessário, siga as etapas 1 a 3 para adicionar outra propriedade.
1. Clique em **[!UICONTROL Salvar]** depois de fazer todas as alterações.

   Você adicionou uma propriedade de metadados personalizada com êxito.

Todo o Forms adaptável em [!DNL AEM Forms] agora contêm essa propriedade de metadados adicional. Você pode editá-lo na página de propriedades.
