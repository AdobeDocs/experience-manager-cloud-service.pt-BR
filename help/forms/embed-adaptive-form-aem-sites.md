---
title: Incorporar um formulário adaptável na página do AEM Sites
seo-title: Hwo to add an Adaptive Form to an AEM Sites page?
description: Você pode usar o componente Forms -Embed adaptável para adicionar ou incorporar o Forms adaptável a uma página do AEM Sites para preencher e enviar um formulário sem sair das páginas do AEM Sites.
feature: Adaptive Forms
exl-id: 359b05e8-d8c1-4a77-9e70-6f6b6e668560
source-git-commit: 2a487654c3af2d2ec3aa43481caed5e1d4fc77a2
workflow-type: tm+mt
source-wordcount: '1154'
ht-degree: 0%

---

# Incorporar um formulário adaptável à página de sites do AEM {#embed-an-adaptive-form-to-aem-sites-page}

## Visão geral {#overview}

O AEM Forms permite que os desenvolvedores de formulários incorporem facilmente o Adaptive Forms em uma página do AEM Sites AEM ou em uma página da Web hospedada fora do. O Formulário adaptável incorporado é totalmente funcional e os usuários podem preencher e enviar o formulário sem sair da página. Ele ajuda o usuário a permanecer no contexto de outros elementos na página da Web e interagir simultaneamente com o formulário.



<!-- For information about embedding an Adaptive Form in an external web page, see [Embed Adaptive Form in external web page](/help/forms/using/embed-adaptive-form-external-web-page.md). -->

Na página AEM Sites, é possível adicionar um Formulário adaptável usando:

* **Forms adaptável - Componente incorporado**
Forms adaptável - O componente de Incorporação permite que os autores do AEM Sites incluam um Formulário adaptável existente em uma página do AEM Sites, melhorando assim a reutilização de formulários adaptáveis. O Adaptive Forms existente pode ser usado de forma independente ou incorporado na página do site. Essa integração oferece uma maneira conveniente para os clientes reutilizarem o Adaptive Forms que já criaram.

* **Navegador de ativos**
Todos os formulários estão disponíveis em Ativos. Você pode arrastar e soltar o formulário como um ativo na página.

## Pré-requisitos {#prerequisites}

Para incorporar um Formulário adaptável em uma página do AEM Sites que use um modelo editável, verifique se o componente Formulário AEM está configurado como um componente permitido no modelo associado.

No caso **Forms adaptável - Componente incorporado** não está visível no **Painel do navegador de componentes** de sites AEM, execute as seguintes etapas, conforme ilustrado no vídeo.

>[!VIDEO](https://video.tv.adobe.com/v/3410544)

Caso a página Sites esteja usando um modelo estático, é necessário configurá-lo no sistema de parágrafo da página do site.

## Incorporação de um formulário adaptável {#af-component}

Para incorporar um formulário adaptável usando a **[!UICONTROL Forms adaptável - Incorporado]** componente:

1. Abra a página Sites do AEM, no modo de edição, na qual você deseja incorporar um Formulário adaptável.
1. No painel Navegador de componentes, arraste e solte a [!UICONTROL Forms adaptável - Incorporado] componente na página. Como alternativa, você pode pesquisar um Formulário adaptável no navegador de Ativos e arrastá-lo para a página Sites. Você pode adicionar um novo Formulário adaptável ou incorporar um Formulário adaptável existente.

   >[!NOTE]
   >
   >Vários componentes Forms adaptáveis - incorporados em uma página não são compatíveis.

1. Para criar e incorporar um novo formulário, na barra de ferramentas do componente, toque no **Criar formulário** ícone. Uma janela para criar o formulário é aberta.

1. Toque no componente Forms adaptável incorporado - Incorporar na página Sites e toque em ![settings_icon](assets/settings_icon.png) na barra de ações. A variável **[!UICONTROL Editar Forms adaptável - Incorporado]** será aberta.
1. Na caixa de diálogo Editar Forms adaptável - Incorporar, especifique o seguinte.

   **Tipo de ativo:** Selecione o tipo de ativo a ser incorporado.
   * **Caminho do ativo**: Procure e selecione o Formulário adaptável a ser incorporado. Ela será preenchida automaticamente se você soltá-la no navegador de ativos.
   * **Envio de publicação** : selecione a ação a ser acionada no envio do formulário. Você pode optar por mostrar uma mensagem de agradecimento ou uma página de agradecimento.
      * Mostrar

      * **Obrigado Pela Mensagem**: escreva uma mensagem usando o editor de rich text para mostrar no envio do formulário. Essa opção está disponível somente quando você opta por mostrar uma mensagem de agradecimento.
      * **Página de agradecimento**: navegue e selecione a página que será exibida no envio do formulário. Essa opção está disponível somente quando você escolhe mostrar uma página de agradecimento.
         * **Redirecionar para a página de agradecimento**: habilite a opção para substituir a página que contém o Formulário adaptável incorporado pela página de agradecimento. Caso contrário, a página de agradecimento substituirá o Formulário adaptável na [!UICONTROL Forms adaptável - Incorporado] sem atualizar os sites subjacentes na página. Essa opção está disponível somente quando você escolhe mostrar uma página de agradecimento.
   * **Usar idioma da página**: Use o local da página do AEM Sites em vez do local do Formulário adaptável.
   * **Definir Foco no formulário**: selecione para definir o foco no primeiro campo do Formulário adaptável.
   * **Tema**: selecione um tema que defina o estilo dos componentes do seu Formulário adaptável. O estilo inclui propriedades de aparência, como estilo da fonte, cor do plano de fundo, dimensões e alinhamento.
   * **O formulário cobre toda a largura do quadro**: Se marcado, o iframe não será usado para renderizar o formulário.
   * **Altura**: especifique a altura do container. Deixe em branco para redimensionar automaticamente o contêiner.
   * **Biblioteca cliente CSS**: especifique o caminho para uma biblioteca de cliente CSS.

1. Salve as configurações. O Formulário adaptável agora está incorporado na página.

O site AEM também permite criar um Formulário adaptável em tempo real usando o componente Adaptive Forms - Embed. Siga as etapas para criar um Formulário adaptável usando o **Forms adaptável - Componente incorporado** na página do AEM:
1. Abra a página Sites do AEM, no modo de edição, na qual você deseja incorporar um Formulário adaptável.
1. No painel Navegador de componentes, arraste e solte o componente Forms adaptável - Incorporar na página.
1. Clique em **Plus** e você será redirecionado para o assistente de criação de formulários.

   ![Forms adaptável - Componente de incorporação](/help/forms/assets/aemformcontainer.png)

1. Agora é possível incorporar um Formulário adaptável nas páginas do site de AEM usando o [!UICONTROL Componente de container do AEM Forms].

## Publicação de formulário adaptável incorporado {#publishing-embedded-adaptive-form}

Considere os seguintes cenários para a publicação de um Formulário adaptável incorporado na página de sites AEM:

* Se você estiver publicando a página de sites do AEM pela primeira vez e ela incluir um Formulário adaptável incorporado, publique a página de sites e o ativo incorporado.
* Se você modificou somente o Formulário adaptável incorporado em uma página do site publicada, publique o ativo original e as alterações refletirão na página do site publicada. A página do site publicada inclui uma referência ao ativo e não requer a republicação da página.
* Se você modificou a página de sites e o Formulário adaptável incorporado, republique a página de sites e o ativo incorporado.

## Modificação do Formulário adaptável incorporado  {#modifying-embedded-adaptive-form}

A página de sites do AEM mantém uma referência ao Formulário adaptável no Forms adaptável - Incorporado. Portanto, todas as configurações e propriedades, como o tema, estilos e ação de envio, configuradas no Formulário adaptável original são mantidas no Formulário adaptável incorporado .

Para modificar qualquer configuração ou propriedade do Formulário adaptável incorporado, execute um dos procedimentos a seguir.

* Abra o formulário original em formulários adaptáveis nos respectivos editores e modifique-o.
* Toque no Formulário adaptável na página do site no modo de edição e toque em **[!UICONTROL Editar em uma nova janela]**. O formulário original é aberto no modo de edição que você pode modificar.

>[!NOTE]
>
>As alterações feitas no Formulário adaptável original são refletidas automaticamente no formulário inserido. No entanto, publique novamente o Formulário adaptável ou a página do site para refletir as alterações na página publicada.

## Considerações e práticas recomendadas {#considerations-and-best-practices}

Lembre-se dos seguintes pontos ao incorporar formulários adaptáveis em páginas de sites AEM:

* O cabeçalho e o rodapé no formulário original não estão incluídos no formulário incorporado.
* Os rascunhos e envios de formulários incorporados pelo usuário são suportados e ficam visíveis nas guias Rascunhos e Forms enviados no Portal do Forms.
* A ação de envio configurada no formulário original é retida no formulário incorporado.
* Se o Adobe Analytics estiver configurado para o formulário original, os dados de análise do formulário incorporado serão capturados no Adobe Analytics. No entanto, não está disponível no relatório de análise de formulários.
