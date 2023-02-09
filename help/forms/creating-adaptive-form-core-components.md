---
title: Como criar um formulário adaptável?
description: Saiba como criar um formulário adaptável usando [!DNL Experience Manager Forms]. O Adaptive Forms são formulários HTML5 responsivos que simplificam a coleta e o processamento de informações. Saiba mais sobre como criar um formulário adaptável com base em um Modelo de dados de formulário e esquema XML ou JSON.
feature: Adaptive Forms, Core Components
role: User, Developer
level: Beginner
source-git-commit: 6f6cf5657bf745a2e392a8bfd02572aa864cc69c
workflow-type: tm+mt
source-wordcount: '1375'
ht-degree: 0%

---


# Criar um formulário adaptável (Componentes principais) {#creating-an-adaptive-form-core-components}

O Adaptive Forms permite criar formulários envolventes, responsivos, dinâmicos e adaptáveis. O AEM Forms fornece um assistente para usuários empresariais para criar rapidamente o Adaptive Forms. O assistente tem uma navegação de guia rápida para selecionar facilmente o modelo pré-configurado, o estilo, os campos e as opções de envio para criar um formulário adaptável. O Adaptive Forms fornece dois tipos de componentes:

* Os Componentes principais adaptáveis do Forms são componentes padronizados de captura de dados. Esses componentes fornecem recursos de personalização, tempo de desenvolvimento reduzido e custos de manutenção mais baixos para suas experiências de inscrição digital. Um desenvolvedor pode personalizar facilmente esses componentes. O Adobe recomenda o aproveitamento desses componentes modernos e extensíveis para desenvolver o Adaptive Forms.

* Os componentes básicos adaptáveis do Forms são componentes de captura de dados clássicos (antigos).

Este artigo descreve uma abordagem mais recente para criar um formulário adaptável. Para criar o Adaptive Forms com base em uma abordagem antiga, consulte [Criar um formulário adaptável (componentes básicos)](creating-adaptive-form.md)

![Assistente para criar um formulário adaptável](/help/release-notes/assets/wizard.png)


## Pré-requisitos

Você precisa do seguinte para criar um formulário adaptável:

* **Um modelo de formulário adaptável**: Um modelo fornece uma estrutura básica e define a aparência (layouts e estilos) de um formulário adaptável. Ele tem componentes pré-formatados contendo determinadas propriedades e estrutura de conteúdo. Também fornece as opções para definir um tema e uma ação de envio. O tema define a ação de aparência e envio define a ação a ser executada no envio de um formulário adaptável. Por exemplo, enviar os dados coletados para uma fonte de dados. O serviço em nuvem fornece um modelo OOTB, chamado em branco:

   * O `blank` O modelo é incluído em cada programa as a Cloud Service do AEM Forms.
   * Você pode instalar o pacote de referência, por meio do gerenciador de pacotes, para adicionar o `blank` modelo para seu programa as a Cloud Service do AEM Forms.
   * Você também pode [criar um novo modelo adaptável do Forms (Componentes principais)](template-editor.md) do zero.

* **Um tema de formulário adaptável**: Um tema contém detalhes de estilo para os componentes e painéis. Os estilos incluem propriedades como cores de plano de fundo, cores de estado, transparência, alinhamento e tamanho. Quando você aplica um tema, o estilo especificado reflete nos componentes correspondentes.  O `Canvas` O modelo é incluído em cada programa as a Cloud Service do AEM Forms.

   <!-- * You can install the reference package, via package manager, to add the `Canvas` template to your AEM Forms as a Cloud Service program.
    * You can also [create a new Adaptive Forms theme (Core Components)](template-editor.md) and deploy it to your AEM Forms as a Cloud Service program. -->

* **Permissões**: Adicione seus usuários a [!DNL forms-users] grupo. Os membros da [!DNL forms-users] têm permissões para criar um formulário adaptável. Para obter uma lista detalhada dos grupos de usuários específicos de formulários, consulte [Grupos e permissões](forms-groups-privileges-tasks.md).


## Criar um formulário adaptável (Componentes principais) {#create-an-adaptive-form-core-components}

1. Faça logon no [!DNL Experience Manager Forms] Instância do autor. Pode ser uma instância do Cloud ou uma instância de desenvolvimento local.

1. Insira suas credenciais na página de logon do Experience Manager. Depois de fazer logon, no canto superior esquerdo, toque em **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms &amp; Documents]**.

1. Toque **[!UICONTROL Criar]**  > **[!UICONTROL Forms adaptável]**. O Assistente é aberto. Na guia Source , selecione um template:

   ![Modelo dos componentes principais](/help/forms/assets/core-components-template.png)

   Quando você seleciona um modelo, um tema e uma ação de envio especificada no modelo são selecionados automaticamente e o **[!UICONTROL Criar]** estiver ativado. Você pode ir para o **[!UICONTROL Estilo]** ou **[!UICONTROL Submissão]** guias para selecionar um tema diferente ou enviar uma ação. Se o template selecionado não especificar um tema, o botão criar permanecerá desativado. Você pode ir para o **[!UICONTROL Estilos]** para selecionar manualmente um tema.

1. No **[!UICONTROL Estilo]** selecione um tema:

   * Quando o template selecionado especifica um tema, o tema é selecionado automaticamente no assistente. Também é possível escolher um tema diferente na guia Style .

   * Se o modelo selecionado não especificar um tema, você pode usar a guia Style para escolher um tema. O **[!UICONTROL Criar]** é ativado somente depois que um tema é selecionado.

1. (Opcional) Na guia Dados, selecione um modelo de dados:

   * **Modelo de dados do formulário**: A [Modelo de dados do formulário](data-integration.md) O permite integrar entidades e serviços de diferentes fontes de dados a um Formulário adaptável. Escolha Modelo de dados de formulário se o Formulário adaptável que você está criando envolver a busca e gravação de dados de e para várias fontes de dados.

   * **Esquema JSON**: [Esquema JSON](adaptive-form-json-schema-form-model.md) Nosso formulário adaptável baseado em componentes principais permite uma integração perfeita com o sistema de back-end da sua organização, fornecendo a capacidade de associar um esquema JSON, que representa a estrutura dos dados que estão sendo produzidos ou consumidos. Essa associação permite que os autores adicionem dinamicamente conteúdo ao Formulário adaptável usando os elementos do esquema. Os elementos do esquema são facilmente acessíveis na guia Objetos do modelo de dados do navegador Conteúdo durante o processo de criação, e todos os campos são adicionados automaticamente a qualquer Formulário adaptável recém-criado.

   Por padrão, todos os campos do esquema JSON associado são automaticamente selecionados e convertidos em componentes de Formulário adaptável correspondentes, simplificando o processo de criação. O assistente oferece a conveniência adicional de permitir que você escolha seletivamente quais campos devem ser incluídos no formulário adaptável usando caixas de seleção.

1. No **[!UICONTROL Submissão]** selecione uma ação enviar:

   * Quando você seleciona um modelo, a ação de envio especificada no modelo é selecionada automaticamente. Você pode selecionar uma ação de envio diferente da guia Enviar. O **[!UICONTROL Submissão]** exibe todas as ações de envio disponíveis.

   * Quando o modelo selecionado não especifica uma ação de envio, você pode usar a variável **[!UICONTROL Submissão]** para selecionar uma ação enviar

1. (Opcional) Na seção **[!UICONTROL Delivery]** , é possível especificar uma data de publicação ou de cancelamento de publicação para um formulário adaptável.

1. Toque **[!UICONTROL Criar]**. Uma caixa de diálogo para especificar o título, o nome e o local para salvar o Formulário adaptativo é exibida:

   * **[!UICONTROL Título]** Especifica o nome de exibição do formulário. O título ajuda a identificar o formulário no [!DNL Experience Manager Forms] interface do usuário.
   * **[!UICONTROL Nome:]** Especifica o nome do formulário. Um nó com o nome especificado é criado no repositório. À medida que você começa a digitar um título, o valor do campo de nome é gerado automaticamente. Você pode alterar o valor sugerido. O campo de nome pode incluir somente caracteres alfanuméricos, hifens e sublinhados. Todas as entradas inválidas são substituídas por um hífen.
   * **[!UICONTROL Caminho:]** Especifica o local em que o formulário adaptativo deve ser salvo. Você pode salvar o formulário adaptável diretamente em `/content/dam/formsanddocuments` ou criar uma pasta como `/content/dam/formsanddocuments/adaptiveforms` para salvar um formulário adaptável. Certifique-se de criar a pasta antes de usá-la no caminho. O **[!UICONTROL Caminho]** não cria uma pasta automaticamente.

1. Toque **[!UICONTROL Criar]**. Um formulário adaptável é criado e aberto no editor do Adaptive Forms. O editor exibe o conteúdo disponível no template.  Com base no tipo de formulário adaptável, os elementos de formulário presentes no <!--XFA form template, XML schema or --> O esquema JSON ou o Modelo de dados de formulário são exibidos no **[!UICONTROL Objetos do modelo de dados]** da guia **[!UICONTROL Navegador de conteúdo]** na barra lateral. Também é possível arrastar e soltar esses elementos para criar o Formulário adaptável.

Agora, você pode arrastar e soltar os Componentes principais adaptáveis do Forms no contêiner do Adaptive Forms para projetar e criar o formulário.

## Componentes principais adaptáveis do Forms disponíveis

Os Componentes principais adaptáveis do Forms são componentes padronizados de captura de dados. Esses componentes fornecem recursos de personalização, tempo de desenvolvimento reduzido e custos de manutenção mais baixos para suas experiências de inscrição digital. Os seguintes Componentes principais estão disponíveis e prontos para uso:

* Opção Adaptável Forms: O recurso acordeão permite que o usuário revele e oculte seções de conteúdo relacionado em um formulário adaptável.

* Botão Adaptável Forms
* Grupo de caixa de seleção adaptável do Forms
* Seletor de data adaptável do Forms
* Lista suspensa adaptável do Forms
* Entrada de email adaptável do Forms
* Anexos de arquivo adaptáveis do Forms
* Guias horizontais adaptáveis do Forms
* Imagem adaptável do Forms
* Entrada do número adaptável do Forms
* Painel adaptável Forms
* Botão de opção adaptável do Forms
* Botão adaptável de redefinição do Forms
* Botão Adaptive Forms Submit
* Entrada de telefone adaptável do Forms
* Texto adaptável do Forms
* Caixa de texto adaptável do Forms
* Título adaptável do Forms
* Layout do assistente adaptável do Forms
* Cabeçalho
* Rodapé

## Editar as propriedades do Modelo de formulário de um formulário adaptável {#edit-form-model}

1. Selecione o formulário adaptável e toque em ![Informações da página](/help/forms/assets/Smock_Properties_18_N.svg) > **[!UICONTROL Abrir propriedades]**. A página Propriedades do formulário é aberta.

1. Vá para o **[!UICONTROL Modelo de formulário]** e escolha um modelo de formulário. Se o formulário adaptável não tiver um modelo de formulário, você terá a liberdade de escolher um esquema JSON ou um modelo de dados de formulário. Por outro lado, se o formulário adaptável já estiver baseado em um modelo de formulário, você terá a opção de alternar para outro modelo de formulário do mesmo tipo. Por exemplo, se o formulário estiver usando um esquema JSON, você poderá facilmente alternar para outro esquema JSON e, de forma semelhante, se o formulário estiver usando um Modelo de dados de formulário, poderá alternar para outro Modelo de dados de formulário.

1. Toque **[!UICONTROL Salvar]** para salvar as propriedades.
