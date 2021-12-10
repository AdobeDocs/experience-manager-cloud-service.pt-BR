---
title: Práticas recomendadas para trabalhar com componentes
seo-title: Best practices for working with components
description: Algumas práticas recomendadas e pontos principais a serem lembrados ao trabalhar com componentes do formulário adaptável
seo-description: Some best practices and key points to remember when working with Adaptive Form components
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 0%

---


# Práticas recomendadas para trabalhar com componentes{#best-practices-for-working-with-components}

Algumas práticas recomendadas e pontos principais a serem lembrados ao trabalhar com componentes do Formulário adaptável são os seguintes:

* Cada componente tem propriedades associadas que controlam sua aparência e funcionalidade. Para configurar as propriedades de um componente, toque no componente e toque em ![propriedades](assets/Smock_Wrench_18_N.svg) para abrir as propriedades do componente no navegador Propriedades.
* Um componente é identificado com seu nome de elemento. Ao tocar ![propriedades](assets/Smock_Wrench_18_N.svg), é possível alterar o nome do componente alterando o **[!UICONTROL Nome do elemento]** no navegador de propriedades. O campo Nome do elemento aceita somente letras, números, hifens (-) e sublinhados (_). Outros caracteres especiais não são permitidos e o nome do elemento deve começar com uma letra.

* É possível modificar a propriedade Título de um componente Formulário adaptável em linha no editor de formulário sem abrir o navegador Propriedades , desde que o título esteja visível no formulário. Para fazer isso:

   1. Toque para selecionar um componente que tenha um **[!UICONTROL Título]** e **[!UICONTROL Ocultar título]** está desativada.

   1. Toque ![Ícone Editar](assets/Smock_Edit_18_N.svg) para tornar o título editável.

   1. Modifique o título e toque na tecla Return ou em qualquer lugar fora do componente para salvar as alterações. Toque na chave Esc para descartar as alterações.

* Alguns componentes de Formulário adaptável, como Email e Telefone, incluem padrões de validação prontos para uso. No entanto, é possível especificar a validação personalizada atualizando o **[!UICONTROL Padrão de validação]** na opção Padrões nas propriedades do componente. Consulte descrições de componentes na tabela acima para obter mais informações sobre validações padrão.

* Campos adaptáveis do Forms, como Caixa numérica e Email, podem ser configurados para incluir tipos de entrada HTML5 especializados. Quando esses campos estão em foco em dispositivos móveis e tablets, o teclado exibe um alfabeto, números e caracteres específicos na frente, normalmente usados para inserir informações nos campos. Ajuda os usuários a inserir informações rapidamente sem precisar alternar entre conjuntos de caracteres no teclado. Para permitir entrada especializada em um componente, habilite a função **[!UICONTROL Usar número do tipo HTML]** caixa de seleção nas propriedades do componente.

* Você pode ativar um componente Caixa de texto para aceitar Rich Text. Para ativar o rich text de uma caixa de texto, ative a **[!UICONTROL Permitir Rich Text]** nas propriedades do componente.

* Você pode ativar os componentes Caixa de texto, Email e Telefone para preencher automaticamente valores para campos como nome, endereço, cartão de crédito, telefone e email a partir das informações armazenadas nas configurações de preenchimento automático do navegador. Para ativar este recurso, selecione **[!UICONTROL Ativar Preenchimento Automático]** nas propriedades do componente e selecione um **[!UICONTROL Atributo de preenchimento automático]**. Quando um usuário preenche um formulário adaptável, os valores são sugeridos a partir do perfil de preenchimento automático no navegador ou com base nos valores preenchidos anteriormente pelo usuário. Observe que o preenchimento automático funciona se as configurações de preenchimento automático no navegador do usuário estiverem ativadas.

* Especifique valores para os itens de Botão de opção e Caixa de seleção em `{value}={text}` nas propriedades do componente.
* O componente File attachment, por padrão, permite que um usuário anexe apenas um arquivo. No entanto, é possível configurar as propriedades do componente para suportar vários anexos. Além disso, se um usuário anexar vários arquivos com o mesmo nome de arquivo, os anexos podem causar alguns problemas. Portanto, é recomendável associar um identificador exclusivo para cada anexo enviado no envio do formulário. Para fazer isso:

   1. Em seu [!DNL AEM Forms] , navegue até **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Ferramentas]** > **[!UICONTROL Operações]** > **[!UICONTROL Console da Web]**.
   1. Localizar e tocar **[!UICONTROL Serviço de configuração adaptável do Forms]**.
   1. Na caixa de diálogo Adaptive Forms Configuration Service , habilite **[!UICONTROL Tornar Nomes de Arquivos Exclusivos]**. Por padrão, está desativado.

* Para permitir que os usuários anexem um PDF usando o navegador Safari, verifique se **application/pdf** é adicionado à propriedade Tipos de arquivo suportados do componente Anexo de arquivo . Forms adaptável criado com [!DNL AEM Forms] a versão pode conter **.pdf** em vez de **application/pdf** na propriedade Tipos de arquivo suportados .

>[!NOTE]
>
>Os componentes do Formulário adaptável não suportam idiomas da direita para a esquerda (RTL). Por exemplo, hebraico.