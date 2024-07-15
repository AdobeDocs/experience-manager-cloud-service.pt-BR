---
title: Práticas recomendadas e pontos principais a serem lembrados ao trabalhar com formulários adaptáveis para AEM.
description: Algumas práticas recomendadas e pontos principais a serem lembrados ao trabalhar com componentes de Formulário adaptável.
source-git-commit: 2d4ffd5518d671a55e45a1ab6f1fc41ac021fd80
workflow-type: tm+mt
source-wordcount: '640'
ht-degree: 1%

---


# Práticas recomendadas para trabalhar com componentes{#best-practices-for-working-with-components}

Algumas práticas recomendadas e pontos principais a serem lembrados ao trabalhar com componentes de Formulário adaptável são os seguintes:

* Cada componente tem propriedades associadas que controlam sua aparência e funcionalidade. Para configurar as propriedades de um componente, selecione o componente e selecione ![propriedades](assets/Smock_Wrench_18_N.svg) para abrir as propriedades do componente no navegador Propriedades.
* Um componente é identificado com seu nome de elemento. Ao selecionar ![propriedades](assets/Smock_Wrench_18_N.svg), é possível alterar o nome do componente alterando o valor do campo **[!UICONTROL Nome do elemento]** no navegador de propriedades. O campo Nome do elemento aceita somente letras, números, hifens (-) e sublinhados (_). Outros caracteres especiais não são permitidos e o nome do elemento deve começar com uma letra.

* Você pode modificar a propriedade Título de um componente Formulário adaptável em linha no editor de formulários sem abrir o navegador Propriedades, desde que o título esteja visível no formulário. Para fazer isso:

   1. Selecione para selecionar um componente que tenha uma propriedade **[!UICONTROL Title]** e cuja propriedade **[!UICONTROL Hide title]** esteja desabilitada.

   1. Selecione ![Ícone Editar](assets/Smock_Edit_18_N.svg) para tornar o título editável.

   1. Modifique o título e selecione a tecla Return ou selecione qualquer lugar fora do componente para salvar as alterações. Selecione a tecla Esc para descartar as alterações.

* Alguns componentes do formulário adaptável, como Email e Telefone, incluem padrões de validação prontos para uso. No entanto, você pode especificar a validação personalizada atualizando o campo **[!UICONTROL Padrão de Validação]** na opção Padrões nas propriedades do componente. Consulte descrições de componentes na tabela acima para obter mais informações sobre validações padrão.

* Os campos adaptáveis do Forms, como Caixa numérica e Email, podem ser configurados para incluir tipos de entrada HTML5 especializados. Quando esses campos estão em foco em dispositivos móveis e tablets, o teclado exibe inicialmente o alfabeto, os números e os caracteres específicos que são normalmente usados para inserir informações nos campos. Isso ajuda os usuários a inserir informações rapidamente, sem precisar alternar entre conjuntos de caracteres no teclado numérico. Para permitir entrada especializada para um componente, habilite a caixa de seleção **[!UICONTROL Usar número do tipo de HTML]** nas propriedades do componente.

* Você pode ativar um componente Caixa de texto para aceitar rich text. Para habilitar rich text para uma caixa de texto, habilite a caixa de seleção **[!UICONTROL Permitir rich text]** nas propriedades do componente.

* Você pode ativar os componentes Caixa de texto, Email e Telefone para preencher automaticamente valores para campos como nome, endereço, cartão de crédito, telefone e email a partir das informações armazenadas nas configurações de preenchimento automático do navegador. Para habilitar este recurso, selecione **[!UICONTROL Habilitar Preenchimento Automático]** nas propriedades do componente e selecione um **[!UICONTROL Atributo de Preenchimento Automático]**. Quando um usuário preenche um Formulário adaptável, os valores são sugeridos pelo perfil de preenchimento automático no navegador ou com base nos valores preenchidos anteriormente pelo usuário. O preenchimento automático funciona se as configurações de preenchimento automático no navegador do usuário estiverem ativadas.

* Especifique valores para os itens Botão de Opção e Caixa de Seleção no formato `{value}={text}` nas propriedades do componente.
* O componente de anexo de Arquivo, por padrão, permite que um usuário anexe apenas um arquivo. No entanto, você pode configurar as propriedades do componente para suportar vários anexos. Além disso, se um usuário anexar vários arquivos com o mesmo nome de arquivo, os anexos poderão causar alguns problemas. Portanto, é recomendável associar um identificador exclusivo para cada anexo enviado no envio do formulário. Para fazer isso:

   1. No servidor [!DNL AEM Forms], navegue até **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Ferramentas]** > **[!UICONTROL Operações]** > **[!UICONTROL Console da Web]**.
   1. Localize e selecione **[!UICONTROL Serviço de Configuração Adaptável do Forms]**.
   1. Na caixa de diálogo Serviço de Configuração do Forms Adaptive, habilite **[!UICONTROL Tornar os Nomes de Arquivos Exclusivos]**. Por padrão, está desativado.

* Para permitir que os usuários anexem um PDF usando o navegador Safari, verifique se **application/pdf** foi adicionado à propriedade Tipos de arquivo suportados do componente de anexo de arquivo. O Forms adaptável criado com a versão [!DNL AEM Forms] anterior pode conter **.pdf** em vez de **application/pdf** na propriedade Tipos de Arquivos com Suporte.

>[!NOTE]
>
>Os componentes do Formulário adaptável não são compatíveis com idiomas da direita para a esquerda (RTL). Por exemplo, hebraico.