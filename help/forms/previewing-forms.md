---
title: Como visualizar um formulário adaptável?
description: Os usuários podem visualizar o formulário antes de publicá-lo ou ativá-lo, para garantir que ele atenda às expectativas. As opções de visualização podem variar entre os tipos de formulário compatíveis.
topic-tags: author
role: Admin, Developer, User
feature: Adaptive Forms
source-git-commit: 6511c4273ca3d394d98a61e8acb4d3cb03c243d5
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 2%

---


# Pré-visualização de um formulário {#previewing-a-form}

## Visão geral {#overview}

Entrada [!DNL AEM Forms], é possível visualizar os formulários e documentos presentes no repositório. A Pré-visualização ajuda a saber exatamente como os formulários são exibidos e se comportam quando são lançados para os usuários finais.

Ao visualizar formulários, eles são renderizados na interface interativa e o usuário pode preencher os formulários com dados. Ao visualizar documentos, eles são renderizados no modo não interativo e o usuário só pode visualizar o documento. Para formulários, uma opção adicional de Visualização personalizada está disponível. Com essa opção, é possível visualizar o formulário usando dados de um arquivo XML. Os dados preenchem alguns dos campos, ou todos os campos, do formulário que está sendo visualizado.

A tabela a seguir lista as opções de visualização disponíveis para diferentes tipos de formulários compatíveis:

<table>
 <tbody>
  <tr>
   <td><strong>Tipo de ativo</strong><br /> </td>
   <td><strong>Opções de visualização disponíveis</strong><br /> </td>
  </tr>
  <!--<tr>
   <td>Document</td>
   <td>PDF preview</td>
  </tr>-->
  <tr>
   <td>Formulário PDF</td>
   <td>Visualização e visualização do PDF com dados<br /> </td>
  </tr>
  <tr>
   <td>Formulário adaptável</td>
   <td>Visualização de HTML e visualização de HTML com dados</td>
  </tr>
  <!--<tr>
   <td>Form Template</td>
   <td>PDF preview, PDF preview with Data, HTML preview, HTML preview with Data<br /> </td>
  </tr>-->
 </tbody>
</table>

## Pré-visualização de um formulário {#previewing-a-form-1}

1. Selecione um ativo que deseja visualizar e clique em Visualizar ![aem6forms_preview](assets/aem6forms_preview.png) na barra de ferramentas ações.

   >[!NOTE]
   >
   >Para selecionar um ativo, alterne para a Exibição de lista na Exibição de cartão padrão. Clique em ![aem6forms_viewlist](assets/aem6forms_viewlist.png) ou ![aem6forms_viewcard](assets/aem6forms_viewcard.png) para alternar visualizações.

1. Clicar em Visualizar lista as possíveis opções de visualização aplicáveis ao Tipo de ativo selecionado. Clique na opção desejada para renderizar o ativo selecionado em uma nova guia.

   As opções são:

   * Visualizar como HTML
   * Exibir com dados
     <!--* Preview as PDF (available for form templates)-->

## Exibir com dados {#preview-with-data}

Ao selecionar **Visualizar com dados**, é possível ver a aparência do formulário com os dados reais inseridos. A opção Preview with Data permite fazer upload de um XML que contém dados de usuário de amostra. Os dados do usuário de exemplo são usados para preencher o formulário de visualização no formato escolhido.

1. Selecione um ativo e clique em Visualizar ![aem6forms_preview](assets/aem6forms_preview.png)e selecione **Visualizar com dados**.
1. Na caixa de diálogo Visualizar formulário, forneça FormData como um arquivo XML. Clique em Visualizar para renderizar o formulário com os dados mesclados do XML.

