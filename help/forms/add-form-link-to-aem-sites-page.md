---
title: Como adicionar links de formulários na página do AEM Sites usando o componente Link do portal do Forms?
description: Saiba como adicionar links de formulários à página do AEM Sites.
feature: Adaptive Forms, Core Components
role: User, Developer, Admin
source-git-commit: 58533d9a950fa4dc0e043ef8cb935d65fc68d233
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 1%

---


# Adicionar links de formulário à página Sites

No cenário do site bancário, o **Link** do Portal Forms aprimora a navegação, orientando os usuários para formulários específicos em várias seções do site. Ele fornece referências diretas a formulários, como aplicativos de empréstimo, formulários de abertura de conta ou pesquisas de feedback, posicionados estrategicamente em todo o site. O componente **Link** insere links que direcionam os usuários para Forms adaptável específico na página Sites. Por exemplo, no site do banco, os usuários anônimos podem acessar um formulário de pesquisa geral, enquanto os usuários conectados podem acessar diretamente formulários mais seguros, como solicitações de empréstimo ou formulários de autorização de transação.

![Ícone de link](/help/forms/assets/link-forms.png){width="250" align="center"}

## Pré-requisito

Antes de explorar os vários recursos de um componente do Forms Portal, verifique se os Componentes principais estão habilitados para o seu ambiente. Para obter instruções detalhadas sobre como habilitar os Componentes principais para o seu ambiente, [clique aqui](/help/forms/enable-adaptive-forms-core-components.md).

Depois de implantar os Componentes principais mais recentes em seu ambiente, os componentes do Forms Portal ficam acessíveis em seu ambiente de criação.

## Adicionar o componente Link à página Sites

Para adicionar o componente de portal **Link** à página Sites, execute as seguintes etapas:

1. Abra a página do AEM Sites no modo **Editar**.
1. Vá para as **[!UICONTROL Informações da Página]** > **[!UICONTROL Editar Modelo]**
   ![Editar política de modelo](/help/forms/assets/save-form-as-draft-edit-template.png){width="250" align="center"}

1. Clique na **[!UICONTROL Política]** e marque a caixa de seleção **[!UICONTROL Link]** em **[Nome do projeto do Arquétipo AEM] - Forms e Portal de Comunicações**.

   ![Seleção de Política](/help/forms/assets/add-link.png){width="250" align="center"}

1. Clique em **[!UICONTROL Concluído]**.
1. Agora, abra novamente a página do AEM Sites no modo de criação.
1. Localize a seção no editor de páginas que permite adicionar o componente Forms Portal.

1. Clique no ícone **Adicionar**. O ícone é um sinal de mais (+) que significa a opção de adicionar novos componentes.

   Clicar no ícone **Adicionar** exibe uma caixa de diálogo **Inserir novo componente** que exibe vários componentes para inserção.

   >[!NOTE]
   >
   > Como alternativa, você também pode arrastar e soltar o componente.

1. Navegue pelos componentes disponíveis na caixa de diálogo e selecione o componente desejado na lista. Por exemplo, selecione o componente **Link** da lista para adicionar o componente **Link** do Forms Portal.

   ![Componente de link](/help/forms/assets/add-link-in-sites.png){width="250" align="center"}

Agora, configure as propriedades do componente **Link**.

## Entender as propriedades do componente Link

Você pode personalizar facilmente as propriedades do componente **Link** usando a caixa de diálogo de configuração para obter uma experiência perfeita para o usuário. Para configurar, selecione o componente e, em seguida, selecione o ![ícone Configurar](assets/configure_icon.png). A caixa de diálogo **[!UICONTROL Link]** é aberta.

### Guia Exibir

![Guia Exibição](/help/forms/assets/link-asset-tab.png){width="250" align="center"}

Na guia **[!UICONTROL Exibir]**, forneça a legenda do link e a dica de ferramenta para facilitar a identificação dos formulários representados pelo link.

### Guia Informações do ativo

![Guia Informações do Assets](/help/forms/assets/link-asset-info.png){width="250" align="center"}

Na guia **[!UICONTROL Informações do ativo]**, especifique o caminho do repositório onde o ativo está armazenado.

### Guia Parâmetros de consulta

![Guia Parâmetros de Consulta](/help/forms/assets/link-query-tab.png){width="250" align="center"}

Na guia **[!UICONTROL Parâmetros de consulta]**, especifique os parâmetros adicionais no formato de par de valor-chave. Quando o link for clicado, esses parâmetros adicionais serão transmitidos junto com o formulário.

## Exibir links de formulário na página Sites usando o componente Link

Visualize a página Sites para exibir o link para um Formulário Adaptável, que é especificado na guia de propriedades **Informações do Assets** do componente **Link**. Clicar no link exibe o formulário na tela para usuários, que podem acessá-lo com base nas permissões.

![Guia Parâmetros de Consulta](/help/forms/assets/link-forms.png){width="250" align="center"}

## Artigos relacionados

{{forms-portal-see-also}}

## Consulte também {#see-also}

{{see-also}}
