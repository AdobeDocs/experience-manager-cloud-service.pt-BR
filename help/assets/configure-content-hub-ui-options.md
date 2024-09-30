---
title: Configurar a interface do usuário do Centro de conteúdo
description: Configurar a interface do usuário do Centro de conteúdo
exl-id: e9e22862-9bcd-459a-bcf4-7f376a0b329a
source-git-commit: 0c31f83d3e115a676c7daa37f634e25d08f4d06c
workflow-type: tm+mt
source-wordcount: '1374'
ht-degree: 12%

---

# Configurar a interface do usuário do Centro de conteúdo {#configure-content-hub-user-interface}

>[!CONTEXTUALHELP]
>id="configure_content_hub"
>title="Configurar a interface do usuário do Centro de conteúdo"
>abstract="O Experience Manager Assets permite que os administradores configurem as opções disponíveis na interface do usuário do Centro de conteúdo. Com base nas opções de configuração selecionadas pelos administradores, os usuários do Centro de conteúdo podem exibir campos no Centro de conteúdo. As opções de configuração incluem metadados ao importar ativos, filtros, propriedades de ativos, metadados ao pesquisar ativos, marcas personalizadas e links personalizados."

<!-- ![Download assets](assets/download-asset.jpg) -->
![Configurar ativos no Content Hub](assets/configure-assets.png)

O Experience Manager Assets permite que os administradores configurem as opções disponíveis na interface do usuário do Centro de conteúdo. Com base nas opções de configuração selecionadas pelos administradores, os usuários do Centro de conteúdo podem exibir campos no Centro de conteúdo. As opções de configuração incluem:

* Filtros disponíveis para usuários ao pesquisar ativos.

* Detalhes ou propriedades de ativos disponíveis para cada ativo.

* Campos de metadados disponíveis para usuários ao adicionar ativos ao Content Hub.

* Campos de metadados de ativos disponíveis para pesquisa no Content Hub.

* Conteúdo de marca que você precisa exibir para sua organização.

* Quaisquer links personalizados que você precise incluir no Content Hub, além de ativos, coleções e insights.

## Pré-requisitos {#prerequisites-configuration-ui}

[Os administradores do Content Hub](/help/assets/deploy-content-hub.md#step-3-onboard-content-hub-administrator) podem definir as opções de configuração para outros usuários em sua organização.

## Acessar opções de configuração no Content Hub {#access-configuration-options-content-hub}

Para acessar as opções de configuração no Content Hub:

1. Clique no ícone do usuário no painel direito.

1. Na seção **[!UICONTROL Configurações do Produto]**, selecione **[!UICONTROL Configurações]**.

   ![Acessar opções de configuração no Content Hub](assets/access-content-hub-configuration-ui.png)

## Gerenciar opções de configuração no Content Hub {#manage-configuration-options}

Como administrador, gerencie as seguintes opções de configuração para seus usuários:

* [Importar](#configure-import-options-content-hub)

* [Filtros](#configure-filters-content-hub)

* [Detalhes do ativo](#configure-asset-details-content-hub)

* [Pesquisar](#configure-metadata-search-content-hub)

* [Identidade visual](#configure-branding-content-hub)

* [Ativos expirados](#expired-assets-content-hub)

* [Links personalizados](#configure-custom-links-content-hub)

### Importar {#configure-import-options-content-hub}

Você pode configurar os campos de metadados exibidos para os usuários ao fazer upload ou importar ativos para o portal do Content Hub, como Nome da campanha, Palavras-chave, Canais, Período, Região etc. Para desabilitá-la, siga estas etapas:

1. Na interface de usuário [Configurações](#access-configuration-options-content-hub), clique em **[!UICONTROL Importar]**.

1. Clique em **[!UICONTROL Adicionar metadados]**.

1. Especifique um rótulo para a propriedade, mapeie-o para uma propriedade usando o campo **[!UICONTROL Metadados]** e selecione o tipo de entrada para os novos metadados do ativo.

1. Clique no botão **[!UICONTROL Campo obrigatório]** para tornar o novo campo de metadados obrigatório para especificação para usuários ao carregar novos ativos.

1. Clique em **[!UICONTROL Confirmar]**. Os novos metadados são exibidos na lista das propriedades de ativos existentes.

1. Clique em **[!UICONTROL Salvar]** para aplicar as alterações.

Da mesma forma, você pode clicar no ![ícone Editar](assets/do-not-localize/edit_icon.svg), disponível ao lado de cada propriedade disponível, para editar os rótulos, tornar esses campos obrigatórios ou não obrigatórios para os usuários ao carregar ativos usando a opção **[!UICONTROL Campo obrigatório]** ou clicar no ícone Excluir para excluir qualquer propriedade de metadados.

Clique na opção **[!UICONTROL Aprovação automática]** se precisar que todos os ativos adicionados ao repositório do Experience Manager Assets sejam aprovados automaticamente para que estejam disponíveis no Content Hub imediatamente. Os autores ou administradores do DAM precisam aprovar manualmente os ativos para disponibilizá-los no Content Hub. Por padrão, o botão está definido como Desligado.

Clique em **[!UICONTROL Salvar]** depois de fazer todas as modificações para aplicar as alterações.

![Detalhes do carregamento da interface de configuração no Content Hub](assets/configuration-ui-upload-details.png)

Metadados ativados na interface do usuário de configuração são exibidos na página de upload de ativos:

![Carregar metadados no Content Hub](assets/configuration-ui-add-assets.png)

### Filtros {#configure-filters-content-hub}

O Content Hub permite que os administradores configurem filtros que são exibidos ao pesquisar ativos. Execute as seguintes etapas para adicionar um novo filtro:

1. Na interface de usuário [Configurações](#access-configuration-options-content-hub), clique em **[!UICONTROL Filtros]**.

1. Clique em **[!UICONTROL Adicionar filtros]**.

1. Especifique um rótulo para o filtro, mapeie-o para uma propriedade usando o campo **[!UICONTROL Metadados]** e selecione o tipo de entrada para o novo filtro.
1. Clique em **[!UICONTROL Confirmar]**. O novo filtro é exibido na lista dos filtros existentes.

1. Clique em **[!UICONTROL Salvar]** para aplicar as alterações para que o novo filtro seja exibido na página Pesquisar ao filtrar ativos.

   >[!NOTE]
   >
   >O novo filtro é exibido na página Pesquisar somente se houver pelo menos um ativo no repositório que corresponda aos critérios do filtro.

Da mesma forma, você pode clicar no ![ícone Editar](assets/do-not-localize/edit_icon.svg), disponível ao lado de cada filtro disponível, para editar os rótulos ou clicar no ícone excluir para excluir qualquer filtro existente. Clique em **[!UICONTROL Salvar]** depois de fazer todas as modificações para aplicar as alterações.

![Filtros de configuração de interface do usuário no Content Hub](assets/configuration-ui-filters.png)

Os filtros ativados na Interface do Usuário de Configuração são exibidos na página Pesquisar:

![Pesquisar no Content Hub](assets/filters-for-search.png)


### Detalhes do ativo {#configure-asset-details-content-hub}

Você também pode configurar as propriedades de ativos exibidas para cada ativo, como nome do arquivo, título, formato, tamanho e assim por diante. Para desabilitá-la, siga estas etapas:

1. Na interface do usuário [Configurações](#access-configuration-options-content-hub), clique em **[!UICONTROL Detalhes do ativo]**.

1. Clique em **[!UICONTROL Adicionar metadados]**.

1. Especifique um rótulo para a propriedade, mapeie-o para uma propriedade usando o campo **[!UICONTROL Metadados]** e selecione o tipo de entrada para os novos metadados do ativo.
1. Clique em **[!UICONTROL Confirmar]**. Os novos metadados são exibidos na lista das propriedades de ativos existentes.

1. Clique em **[!UICONTROL Salvar]** para aplicar as alterações para que a nova propriedade seja exibida na página de detalhes do ativo.

Da mesma forma, você pode clicar no ![ícone Editar](assets/do-not-localize/edit_icon.svg), disponível ao lado de cada propriedade disponível, para editar os rótulos ou clicar no ícone excluir para excluir qualquer detalhe de ativo existente. Clique em **[!UICONTROL Salvar]** depois de fazer todas as modificações para aplicar as alterações.

![Detalhes do ativo da interface do usuário de configuração no Content Hub](assets/configuration-ui-asset-details.png)

As propriedades ativadas na Interface do Usuário da Configuração são exibidas na página Detalhes do ativo:

![Propriedades do ativo no Content Hub](assets/config-ui-asset-properties.png)

### Pesquisar {#configure-metadata-search-content-hub}

Os administradores podem definir os campos de metadados que são pesquisados quando um usuário especifica um critério de pesquisa no Content Hub. Execute as seguintes etapas:

1. Na interface de usuário [Configurações](#access-configuration-options-content-hub), clique em **[!UICONTROL Adicionar metadados]**.

1. Especifique o campo de metadados e clique em **[!UICONTROL Confirmar]**.

1. Clique em **[!UICONTROL Salvar]** para aplicar as alterações para que a nova propriedade de metadados seja exibida na lista de campos de metadados.

Da mesma forma, você pode clicar no ![ícone Editar](assets/do-not-localize/edit_icon.svg), disponível ao lado de cada propriedade de metadados disponível, para editar a propriedade ou clicar no ícone excluir para excluir qualquer propriedade existente. Clique em **[!UICONTROL Salvar]** depois de fazer todas as modificações para aplicar as alterações.

![Pesquisa de Interface do Usuário de Configuração no Content Hub](assets/configuration-ui-metadata-search.png)


### Identidade visual {#configure-branding-content-hub}

Os administradores também podem personalizar o título e o texto do corpo no banner do portal do Content Hub, de acordo com seus requisitos de marca. Para desabilitá-la, siga estas etapas:

1. Na interface de usuário [Configurações](#access-configuration-options-content-hub), clique em **[!UICONTROL Identidade Visual]**.

1. Especifique o texto no **[!UICONTROL Texto do título no banner]** e **[!UICONTROL Texto do corpo nos campos do banner]**.

1. Clique em **[!UICONTROL Salvar]** para aplicar as alterações.

![Marca da interface do usuário de configuração no Content Hub](assets/configuration-ui-branding.png)

As atualizações de marca ativadas na interface do usuário de configuração são exibidas no banner do portal do Content Hub:

![Marca da interface do usuário de configuração no Content Hub](assets/configuration-ui-branding-updates.png)

### Ativos expirados {#expired-assets-content-hub}

Os administradores podem controlar se precisam que os ativos expirados estejam visíveis no Content Hub. Se os ativos expirados se tornarem visíveis, eles também poderão definir se os usuários podem baixá-los.

Por padrão, os ativos expirados não são exibidos no Content Hub.

Para desabilitá-la, siga estas etapas:

1. Na interface do usuário [Configurações](#access-configuration-options-content-hub), clique em **[!UICONTROL Assets Expirado]**.

1. Na seção **[!UICONTROL Visível]**, habilite o botão **[!UICONTROL Permitir que usuários exibam ativos expirados]** para tornar todos os ativos expirados visíveis no Content Hub.

1. Depois de habilitar a visibilidade dos ativos, você pode habilitar ou desabilitar a capacidade de baixar ativos expirados usando a opção **[!UICONTROL Permitir que os usuários baixem ativos expirados]**.

1. Clique em **[!UICONTROL Salvar]** para aplicar as alterações.

   ![Ativos expirados no Content Hub](assets/expired-assets-content-hub.png)

Depois de ativar a visibilidade dos ativos, você pode visualizá-los no Content Hub, conforme mostrado na imagem a seguir:

![Ativos expirados no Content Hub](assets/view-download-expired-assets.png)

Se o administrador tiver ativado o download, os usuários do Content Hub também poderão baixá-los, conforme realçado na imagem.

Se a visibilidade dos ativos expirados estiver habilitada, o Content Hub também destacará os ativos que expiram nos próximos 15 dias usando a mensagem `Expiring in n days` no cartão de ativos.


### Links personalizados {#configure-custom-links-content-hub}

Você também pode adicionar guias personalizadas além das guias padrão **[!UICONTROL Todas as Assets]**, **[!UICONTROL Coleções]** e **[!UICONTROL Insights]** no portal do Content Hub logo abaixo do banner. Para desabilitá-la, siga estas etapas:

1. Na interface de usuário [Configurações](#access-configuration-options-content-hub), clique em **[!UICONTROL Links Personalizados]**.

1. Clique em **[!UICONTROL Adicionar link]**.

1. Especifique o texto nos campos **[!UICONTROL Rótulo]** e **[!UICONTROL URL]**. O rótulo definido é exibido como uma guia e, quando você clica no rótulo, navega até a URL definida no campo **[!UICONTROL URL]**.

1. Clique em **[!UICONTROL Confirmar]**.

1. Clique em **[!UICONTROL Salvar]** para aplicar as alterações.

Da mesma forma, você pode clicar no ![ícone Editar](assets/do-not-localize/edit_icon.svg), disponível ao lado de cada URL, para editar os links ou clicar no ícone excluir para excluir qualquer URL existente. Clique em **[!UICONTROL Salvar]** depois de fazer todas as modificações para aplicar as alterações.

![Links Personalizados da Interface do Usuário de Configuração no Content Hub](assets/configuration-ui-custom-links.png)

O link personalizado é exibido como uma nova guia ao lado da guia Insights na página inicial do Content Hub.

![Guias de Links Personalizados da Interface do Usuário de Configuração no Content Hub](assets/configuration-ui-custom-link-tab.png)
