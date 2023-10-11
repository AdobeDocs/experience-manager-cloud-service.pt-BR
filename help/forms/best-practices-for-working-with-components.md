---
title: Práticas recomendadas e pontos principais a serem lembrados ao trabalhar com formulários adaptáveis para AEM.
description: Algumas práticas recomendadas e pontos principais a serem lembrados ao trabalhar com componentes de Formulário adaptável.
source-git-commit: d33c7278d16a8cce76c87b606ca09aa91f1c3563
workflow-type: tm+mt
source-wordcount: '641'
ht-degree: 1%

---


# Práticas recomendadas para trabalhar com componentes{#best-practices-for-working-with-components}

Algumas práticas recomendadas e pontos principais a serem lembrados ao trabalhar com componentes de Formulário adaptável são os seguintes:

* Cada componente tem propriedades associadas que controlam sua aparência e funcionalidade. Para configurar as propriedades de um componente, toque no componente e ![propriedades](assets/Smock_Wrench_18_N.svg) para abrir as propriedades do componente no navegador Propriedades.
* Um componente é identificado com seu nome de elemento. Ao tocar em ![propriedades](assets/Smock_Wrench_18_N.svg), é possível alterar o nome do componente alterando o **[!UICONTROL Nome do elemento]** no navegador de propriedades. O campo Nome do elemento aceita somente letras, números, hifens (-) e sublinhados (_). Outros caracteres especiais não são permitidos e o nome do elemento deve começar com uma letra.

* Você pode modificar a propriedade Título de um componente Formulário adaptável em linha no editor de formulários sem abrir o navegador Propriedades, desde que o título esteja visível no formulário. Para fazer isso:

   1. Toque para selecionar um componente que tenha uma **[!UICONTROL Título]** propriedade e cuja **[!UICONTROL Ocultar título]** propriedade está desativada.

   1. Toque ![Ícone Editar](assets/Smock_Edit_18_N.svg) para tornar o título editável.

   1. Modifique o título e toque na tecla Return ou em qualquer lugar fora do componente para salvar as alterações. Toque na tecla Esc para descartar as alterações.

* Alguns componentes do formulário adaptável, como Email e Telefone, incluem padrões de validação prontos para uso. No entanto, você pode especificar a validação personalizada atualizando o **[!UICONTROL Padrão de validação]** sob a opção Padrões nas propriedades do componente. Consulte descrições de componentes na tabela acima para obter mais informações sobre validações padrão.

* Os campos adaptáveis do Forms, como Caixa numérica e Email, podem ser configurados para incluir tipos de entrada HTML5 especializados. Quando esses campos estão em foco em dispositivos móveis e tablets, o teclado exibe inicialmente o alfabeto, os números e os caracteres específicos que são normalmente usados para inserir informações nos campos. Isso ajuda os usuários a inserir informações rapidamente, sem precisar alternar entre conjuntos de caracteres no teclado numérico. Para permitir entrada especializada para um componente, ative a opção **[!UICONTROL Usar número do tipo de HTML]** em suas propriedades de componente.

* Você pode ativar um componente Caixa de texto para aceitar rich text. Para habilitar rich text para uma caixa de texto, habilite a opção **[!UICONTROL Permitir Rich Text]** nas propriedades do componente.

* Você pode ativar os componentes Caixa de texto, Email e Telefone para preencher automaticamente valores para campos como nome, endereço, cartão de crédito, telefone e email a partir das informações armazenadas nas configurações de preenchimento automático do navegador. Para ativar esse recurso, selecione **[!UICONTROL Ativar preenchimento automático]** nas propriedades do componente e selecione um **[!UICONTROL Preencher atributo automaticamente]**. Quando um usuário preenche um Formulário adaptável, os valores são sugeridos pelo perfil de preenchimento automático no navegador ou com base nos valores preenchidos anteriormente pelo usuário. Observe que o preenchimento automático funciona se as configurações de preenchimento automático no navegador do usuário estiverem ativadas.

* Especificar valores para os itens Botão de opção e Caixa de seleção em `{value}={text}` formato nas propriedades do componente.
* O componente de anexo de Arquivo, por padrão, permite que um usuário anexe apenas um arquivo. No entanto, você pode configurar as propriedades do componente para suportar vários anexos. Além disso, se um usuário anexar vários arquivos com o mesmo nome de arquivo, os anexos poderão causar alguns problemas. Portanto, é recomendável associar um identificador exclusivo para cada anexo enviado no envio do formulário. Para fazer isso:

   1. No seu [!DNL AEM Forms] servidor, navegue até **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Ferramentas]** > **[!UICONTROL Operações]** > **[!UICONTROL Console da Web]**.
   1. Localizar e tocar **[!UICONTROL Serviço de configuração adaptável do Forms]**.
   1. Na caixa de diálogo Serviço de configuração do Forms adaptável, ative **[!UICONTROL Tornar Nomes de Arquivos Exclusivos]**. Por padrão, está desativado.

* Para permitir que os usuários anexem um PDF usando o navegador Safari, verifique se **application/pdf** é adicionado à propriedade Tipos de arquivo suportados do componente de anexo de arquivo. Forms adaptável criado com o anterior [!DNL AEM Forms] a versão pode conter **.pdf** em vez de **application/pdf** na propriedade Tipos de arquivos suportados.

>[!NOTE]
>
>Os componentes do Formulário adaptável não são compatíveis com idiomas da direita para a esquerda (RTL). Por exemplo, hebraico.