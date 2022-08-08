---
title: Incorporar um formulário adaptável na página do AEM Sites
seo-title: Hwo to add an Adaptive Form to an AEM Sites page?
description: Você pode usar o componente Contêiner do AEM Forms para adicionar ou incorporar o Adaptive Forms a uma página do AEM Sites para preencher e enviar um formulário sem sair das páginas do AEM Sites.
feature: Adaptive Forms
source-git-commit: dac38b2a90b2a1969e5332b8a658e8f1e0e5eccb
workflow-type: tm+mt
source-wordcount: '1036'
ht-degree: 1%

---

# Incorporar um formulário adaptável a uma página de sites de AEM {#embed-an-adaptive-form-to-aem-sites-page}

## Visão geral {#overview}

O AEM Forms permite que desenvolvedores de formulários incorporem, sem interrupções, formulários adaptáveis em uma página do AEM Sites ou em uma página da Web hospedada fora do AEM. O formulário adaptável incorporado é totalmente funcional e os usuários podem preencher e enviar o formulário sem sair da página. Ajuda o usuário a permanecer no contexto de outros elementos na página da Web e interagir simultaneamente com o formulário.

<!-- For information about embedding an Adaptive Form in an external web page, see [Embed Adaptive Form in external web page](/help/forms/using/embed-adaptive-form-external-web-page.md). -->

Na página AEM Sites, é possível adicionar um Formulário adaptável usando:

* **[Componente Contêiner do AEM Forms](/help/forms/using/embed-adaptive-form-aem-sites.md#af-component)**
O AEM Forms fornece um componente que pode ser adicionado às páginas do site. O componente Contêiner do AEM Forms permite que você incorpore um Formulário adaptável.

* **[Navegador de ativos](/help/forms/using/embed-adaptive-form-aem-sites.md#asset-browser)**
Todos os formulários estão disponíveis em Ativos. Você pode arrastar e soltar o formulário como um ativo na página.

## Pré-requisitos {#prerequisites}

Para incorporar um formulário adaptável em uma página do AEM Sites que use um modelo editável, verifique se o componente Formulário AEM está configurado como um componente permitido no modelo associado. Para obter mais informações, consulte **Política e propriedades (contêiner de layout)** seção em [Criação de modelos de página](/help/sites-authoring/templates.md).

No caso de uma página Sites usando um modelo estático, é necessário configurá-la no sistema de parágrafo da página do site. Para obter mais informações, Consulte [Configuração dos componentes no modo de Design](/help/sites-authoring/default-components-designmode.md).

## Como incorporar um formulário adaptável {#af-component}

Para incorporar um formulário adaptável usando o componente Contêiner do AEM Forms:

1. Abra a página AEM sites, no modo de edição, na qual deseja incorporar um formulário adaptável.
1. No painel Navegador de componentes , arraste e solte o componente Contêiner do AEM Forms na página. Como alternativa, você pode pesquisar um Formulário adaptável no navegador Ativos e arrastar e soltar na página Sites . Ele incorpora o formulário em um Contêiner do AEM Forms. É possível criar e adicionar um novo formulário adaptável ou Incorporar um formulário adaptável existente.

   >[!NOTE]
   >
   >Vários componentes do contêiner do AEM Forms em uma página não são compatíveis.

1. Para criar e incorporar um novo formulário, na barra de ferramentas do componente, toque no **Criar formulário** ícone . Uma janela para criar o novo formulário é aberta.

1. Toque no componente AEM Forms Container incorporado na página Sites e toque em ![settings_icon](assets/settings_icon.png) na barra de ações. O **[!UICONTROL Editar contêiner do AEM Forms]** será aberta.
1. Na caixa de diálogo Editar contêiner do AEM Forms , especifique o seguinte.

   <!-- * **Asset Type:** Select the type of asset to embed. The options are Adaptive Form -->
   * **Caminho do ativo**: Navegue e selecione o Formulário adaptável a ser incorporado. Ele é preenchido automaticamente se você soltou no navegador Ativos.
   * **Pós-envio** : Selecione a ação a ser acionada no envio do formulário. Você pode optar por mostrar uma mensagem de agradecimento ou uma página de agradecimento.

      * **Mensagem de agradecimento**: Escreva uma mensagem usando o editor de rich text para mostrar no envio do formulário. Essa opção está disponível somente quando você opta por mostrar uma mensagem de agradecimento.
      * **Página de agradecimento**: Navegue e selecione a página a ser exibida no envio do formulário. Essa opção está disponível somente quando você opta por mostrar uma página de agradecimento.
         * **Redirecionar para página de agradecimento**: Habilite a opção para substituir a página que contém o formulário adaptável incorporado pela página de agradecimento. Caso contrário, a página de agradecimento substituirá o Formulário adaptável no contêiner do AEM Forms, sem atualizar os sites subjacentes na página. Essa opção está disponível somente quando você opta por mostrar uma página de agradecimento.
   * **Usar idioma da página**: Use o local da página do AEM Sites em vez do local do Formulário adaptativo.
   * **Definir foco no formulário**: Selecione para definir o foco no primeiro campo do formulário adaptável.

   * **Tema**: Selecione um tema que defina o estilo dos componentes do seu formulário adaptável. O estilo inclui propriedades de aparência, como estilo de fonte, cor de plano de fundo, dimensões e alinhamento.
   * **Altura**: Especifique a altura do contêiner. Deixe em branco para redimensionar automaticamente o contêiner.
   * **Biblioteca de clientes CSS**: Especifique o caminho para uma biblioteca de cliente CSS.

1. Salve as configurações. O formulário adaptável agora está incorporado na página.

## Publicação do formulário adaptável incorporado {#publishing-embedded-adaptive-form}

Vamos considerar os seguintes cenários para a publicação de um formulário adaptável incorporado AEM página de sites:

* Se você estiver publicando a página AEM sites pela primeira vez e ela incluir um Formulário adaptável incorporado, publique a página sites e o ativo incorporado.
* Se você modificou apenas o Formulário adaptativo incorporado em uma página do site publicada, publique o ativo original e as alterações refletirão na página do site publicado. A página do site publicada inclui uma referência ao ativo e não requer a republicação da página.
* Se você modificou a página de sites e o Formulário adaptativo incorporado , republique a página de sites e o ativo incorporado.

## Modificação do formulário adaptável incorporado  {#modifying-embedded-adaptive-form}

AEM página de sites mantém uma referência ao Formulário adaptável no Contêiner do AEM Forms. Portanto, todas as configurações e propriedades, como o tema, os estilos e a ação de envio, configuradas no Formulário adaptável original são retidas no Formulário adaptável incorporado.

Para modificar qualquer configuração ou propriedade do Formulário adaptável incorporado, execute um dos procedimentos a seguir.

* Abra o formulário original em formulários adaptáveis nos respectivos editores e modifique-o.
* Toque no Formulário adaptável na página do site no modo de edição e toque em **[!UICONTROL Editar em uma nova janela]**. O formulário original é aberto no modo de edição que pode ser modificado.

>[!NOTE]
>
>As alterações feitas no formulário adaptável original refletem automaticamente no formulário incorporado. No entanto, republique o Formulário adaptativo ou a página do site para refletir as alterações na página publicada.

## Considerações e práticas recomendadas {#considerations-and-best-practices}

Lembre-se dos seguintes pontos ao incorporar formulários adaptáveis em páginas de sites AEM:

* O cabeçalho e o rodapé no formulário original não são incluídos no formulário incorporado.
* Os rascunhos e envios de usuários de formulários incorporados são suportados e visíveis nas guias Rascunhos e Forms enviados no portal de formulários.
* A ação de envio configurada no formulário original é retida no formulário incorporado.
* O direcionamento de experiência e os testes A/B configurados no formulário original não funcionam no formulário incorporado. No entanto, você pode usar o direcionamento de experiência na página de sites para apresentar diferentes formulários com base nos perfis do usuário.
* Se o Adobe Analytics estiver configurado para o formulário original, os dados analíticos do formulário incorporado serão capturados no Adobe Analytics. No entanto, não está disponível no relatório de análise de formulários.
