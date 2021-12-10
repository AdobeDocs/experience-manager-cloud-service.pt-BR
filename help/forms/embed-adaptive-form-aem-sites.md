---
title: 'Como incorporar um formulário adaptável em uma página de sites de AEM? '
description: Você pode incorporar o Adaptive Forms em páginas de sites AEM. Os usuários podem preencher e enviar formulários sem sair das páginas do site.
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '949'
ht-degree: 1%

---


# Incorporar um formulário adaptável AEM página de sites {#embed-an-adaptive-form-or-interactive-communication-in-aem-sites-page}

[!DNL AEM Forms] O permite que desenvolvedores de formulários incorporem, sem interrupções, o Adaptive Forms em uma página do AEM Sites ou em uma página da Web hospedada fora do AEM. O formulário adaptável incorporado é totalmente funcional e os usuários podem preencher e enviar o formulário sem sair da página. Ajuda o usuário a permanecer no contexto de outros elementos na página da Web e interagir simultaneamente com o formulário .

<!-- For information about embedding an Adaptive Form in an external web page, see [Embed Adaptive Form in external web page](/help/forms/using/embed-adaptive-form-external-web-page.md). -->

Na página AEM Sites, é possível adicionar um Formulário adaptável usando:

* **[[!DNL AEM Forms] Componente do contêiner](#af-component)**
   [!DNL AEM Forms] O fornece um componente que pode ser adicionado às páginas do site. O [!DNL AEM Forms] O componente Contêiner permite que você incorpore um Formulário adaptável.

* **[Navegador de ativos](/help/forms/using/embed-adaptive-form-aem-sites.md#asset-browser)**
Todos os formulários criados estão disponíveis em Ativos. Você pode arrastar e soltar o formulário como um ativo na página.

## Pré-requisitos {#prerequisites}

Para incorporar um formulário adaptável em uma página de sites de AEM que use um modelo editável, verifique se o componente Formulário AEM está configurado como um componente permitido no modelo associado. Para obter mais informações, consulte **Política e propriedades (contêiner de layout)** seção em [Criação de modelos de página](/help/sites-authoring/templates.md).

No caso de uma página Sites usando um modelo estático, é necessário configurá-la no sistema de parágrafo da página do site. Para obter mais informações, Consulte [Configuração dos componentes no modo de Design](/help/sites-authoring/default-components-designmode.md).

## Como incorporar um formulário adaptável  {#af-component}

Para incorporar um formulário adaptável usando [!DNL AEM Forms] Componente do contêiner:

1. Abra a página AEM sites, no modo de edição, na qual deseja incorporar um Formulário adaptável .
1. No painel Navegador de componentes , arraste e solte o [!DNL AEM Forms] Componente de contêiner na página.

   Como alternativa, você pode pesquisar um Formulário adaptável no navegador Ativos e arrastar e soltar na página Sites . Incorpora o formulário em um [!DNL AEM Forms] Contêiner.

   >[!NOTE]
   >
   >Vários [!DNL AEM Forms] Os componentes do contêiner em uma página não são compatíveis.

1. Toque em incorporado [!DNL AEM Forms] Componente de contêiner na página de sites e toque em ![settings_icon](assets/settings_icon.png) na barra de ações. O **[!UICONTROL Editar contêiner do AEM Forms]** será aberta.
1. Na opção Editar [!DNL AEM Forms] Container , especifique o seguinte.

   * **Tipo de ativo:** Selecione o tipo de ativo a ser incorporado. As opções são Formulário adaptável
   * **Caminho do ativo**: Navegue e selecione o Formulário adaptável a ser incorporado. Ele é preenchido automaticamente se você soltou no navegador Ativos.
   * (Somente formulário adaptável) **Pós-envio**: Selecione a ação a ser acionada no envio do formulário. Você pode optar por mostrar uma mensagem de agradecimento ou uma página de agradecimento.

      * **Mensagem de agradecimento**: Escreva uma mensagem usando o editor de rich text para mostrar no envio do formulário. Essa opção está disponível somente quando você opta por mostrar uma mensagem de agradecimento.
      * **Página de agradecimento**: Navegue e selecione a página a ser exibida no envio do formulário. Essa opção está disponível somente quando você opta por mostrar uma página de agradecimento.
      * **Atualizar página no envio**: Permita atualizar a página que contém o formulário adaptável incorporado para mostrar a página de agradecimento. Caso contrário, a página de agradecimento substituirá o Formulário adaptável no [!DNL AEM Forms] , sem atualizar a página. Essa opção está disponível somente quando você opta por mostrar uma página de agradecimento.
   * **Tema**: Selecione um tema que defina o estilo dos componentes do seu Formulário adaptável . O estilo inclui propriedades de aparência, como estilo de fonte, cor de plano de fundo, dimensões e alinhamento.
   * **Altura**: Especifique a altura do contêiner. Deixe em branco para redimensionar automaticamente o contêiner.
   * **Biblioteca de clientes CSS**: Especifique o caminho para uma biblioteca de cliente CSS.


1. Salve as configurações. O formulário adaptável agora está incorporado na página.

## Publicação do formulário adaptável incorporado {#publishing-embedded-adaptive-form}

Vamos considerar os seguintes cenários para a publicação de um ativo incorporado (Formulário adaptativo ) AEM página de sites:

* Se você estiver publicando a página AEM sites pela primeira vez e ela incluir um Formulário adaptável incorporado , publique a página sites e o ativo incorporado.
* Se você modificou apenas o Formulário adaptativo incorporado em uma página do site publicada, publique o ativo original e as alterações refletirão na página do site publicado. A página do site publicada inclui uma referência ao ativo e não requer a republicação da página.
* Se você modificou a página de sites e o Formulário adaptativo incorporado , republique a página de sites e o ativo incorporado.

## Modificação do formulário adaptável incorporado {#modifying-embedded-adaptive-form-and-interactive-communication}

AEM página de sites mantém uma referência ao Formulário adaptável no [!DNL AEM Forms] Contêiner. Portanto, todas as configurações e propriedades, como o tema, os estilos e a ação de envio, configuradas no Formulário adaptável original são retidas no Formulário adaptável incorporado.

Para modificar qualquer configuração ou propriedade do Formulário adaptável incorporado, execute um dos procedimentos a seguir.

* Abra o formulário original no Adaptive Forms em seus respectivos editores e modifique-o.
* Toque no Formulário adaptável na página do site no modo de edição e toque em **[!UICONTROL Editar em uma nova janela]**. O formulário original é aberto no modo de edição que pode ser modificado.

>[!NOTE]
>
>As alterações feitas no formulário adaptável original refletem automaticamente no formulário incorporado. No entanto, republique o Formulário adaptativo ou a página do site para refletir as alterações na página publicada.

## Considerações e práticas recomendadas {#considerations-and-best-practices}

Lembre-se dos pontos a seguir ao incorporar o Adaptive Forms nas páginas de sites AEM:

* O cabeçalho e o rodapé no formulário original não são incluídos no formulário incorporado.
* Os rascunhos e envios de usuários de formulários incorporados são suportados e visíveis nas guias Rascunhos e Forms enviados no portal de formulários.
* A ação de envio configurada no formulário original é retida no formulário incorporado.
* O direcionamento de experiência e os testes A/B configurados no formulário original não funcionam no formulário incorporado. No entanto, você pode usar o direcionamento de experiência na página de sites para apresentar diferentes formulários com base nos perfis do usuário.
* Se o Adobe Analytics estiver configurado para o formulário original, os dados analíticos do formulário incorporado serão capturados no Adobe Analytics. No entanto, não está disponível no relatório de análise de formulários.

