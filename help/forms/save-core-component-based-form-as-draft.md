---
title: Como salvar o formulário adaptável baseado em Componentes principais como um rascunho e usar o componente Rascunhos e envios para listar rascunhos e envios?
description: Saiba como salvar os Componentes principais com base no Formulário adaptável como um rascunho. Também entende como usar o componente Rascunhos e envios para listar rascunhos e envios para usuários conectados?
feature: Adaptive Forms, Core Components
exl-id: c0653bef-afeb-40c1-b131-7d87ca5542bc
role: User, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1387'
ht-degree: 1%

---


# Salvar formulários como rascunhos e listá-los na página Sites

<!--This article provides information about the Auto-save feature, which is currently available as a pre-release feature. The pre-release feature is accessible only through our [pre-release channel](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/release-notes/prerelease#new-features).-->

Considere um usuário que começa a preencher um formulário, mas precisa pausar e retornar posteriormente. O AEM oferece uma opção `save-as-draft`, permitindo que o usuário salve o formulário como rascunho para conclusão futura. Para facilitar isso, o AEM fornece o componente de **Rascunhos e envios** do Forms Portal pronto para uso, que exibe rascunhos e envios em páginas do AEM Sites. O componente lista formulários que foram salvos como rascunhos para conclusão posterior, bem como aqueles que foram enviados. Somente os usuários conectados podem editar os rascunhos ou exibir os formulários enviados. No entanto, se um usuário anônimo navegar pela lista de formulários usando o componente **Pesquisa e Listagem** e salvar um formulário como rascunho, ele não será listado pelo componente **Rascunhos e Envios**. Para visualizar rascunhos e envios, os usuários devem estar conectados no momento do envio do formulário.

![Ícone Rascunhos](assets/drafts-component.png)

## Pré-requisitos

* Instale os componentes principais adaptáveis do Forms mais recentes até o momento para ativar o ambiente do AEM Cloud Service.

  Depois de implantar os Componentes principais mais recentes em seu ambiente, os componentes do Forms Portal ficam acessíveis em seu ambiente de criação.

* [Configurar o Armazenamento do Azure e o Conector de Armazenamento Unificado para Rascunhos e Envios do componente do Portal da Forms](#configure-azure-storage-and-unified-storage-connector-for-drafts--submissions-forms-portal-component)

### Configurar o Azure Storage e o Conector de armazenamento unificado para rascunhos e envios do componente do Portal da Forms

O componente **Rascunhos e Envios** precisa de uma configuração de armazenamento para salvar e listar rascunhos na página do AEM Sites. O Conector de armazenamento unificado oferece uma estrutura para vincular o AEM ao armazenamento externo. Para salvar o formulário como rascunho, verifique se você tem uma conta de armazenamento do Azure e uma chave de acesso para autorizar o acesso à conta de armazenamento [!DNL Azure]. Depois de ter a conta de armazenamento do Azure e a chave de acesso, execute as seguintes etapas para criar uma configuração de Armazenamento do Azure:

1. Navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Serviços de Nuvem]** > **[!UICONTROL Armazenamento do Azure]**.

   ![Seleção de Cartão de Armazenamento do Azure](/help/forms/assets/save-form-as-draft-azure-card.png)

1. Selecione uma pasta de configuração para criar a configuração e selecione **[!UICONTROL Criar]**.

   ![Selecionar pasta de configuração de armazenamento do Azure](/help/forms/assets/save-form-as-draft-select-config-folder.png)

1. Especifique um título para a configuração no campo **[!UICONTROL Título]**.
1. Especifique o nome da conta de armazenamento [!DNL Azure] nos campos **[!UICONTROL Conta de Armazenamento do Azure]** e **[!UICONTROL Chave de Acesso do Azure]**.

   ![Configuração de Armazenamento do Azure](/help/forms/assets/save-form-as-draft-azure-storage.png)

   Digite `Connection String` na caixa de texto `Azure Storage Account` e `Azure Key` na caixa de texto `Azure Access key`.

1. Clique em **Salvar**.

   >[!NOTE]
   >
   > Você pode recuperar a **[!UICONTROL Conta de Armazenamento do Azure]** e a **[!UICONTROL Chave de Acesso do Azure]** no [Portal do Microsoft Azure](https://learn.microsoft.com/en-us/azure/storage/common/storage-account-keys-manage?tabs=azure-portal).

   Depois de criar com êxito a Configuração de Armazenamento do Azure, configure o Conector de Armazenamento Unificado para o Forms Portal, usando as seguintes etapas:

1. Navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Forms]** > **[!UICONTROL Conector de Armazenamento Unificado]**.

   ![Armazenamento de conector unificado](/help/forms/assets/save-form-as-draft-unified-connector.png)

1. Na seção **[!UICONTROL Portal do Forms]**, selecione **[!UICONTROL Azure]** na lista suspensa **[!UICONTROL Armazenamento]**.
1. Especifique o caminho de configuração para a configuração de armazenamento do Azure no campo **[!UICONTROL Caminho de Configuração de Armazenamento]**.

   ![Configuração de armazenamento do conector unificado](/help/forms/assets/save-form-as-draft-unified-connector-storage.png)

1. Selecione **[!UICONTROL Salvar]**.

>[!NOTE]
>
> Se você precisar configurar uma opção de armazenamento, diferente do Azure, escreva para aem-forms-ea@adobe.com de seu endereço de email oficial com seus requisitos detalhados.

Depois de configurar com êxito o Armazenamento do Azure e o Conector de Armazenamento Unificado para armazenar os rascunhos e formulários enviados, adicione o componente **Rascunhos e envios** na página AEM Sites.

## Como adicionar o componente Rascunhos e envios a uma página do AEM Sites?

Você pode usar componentes prontos para uso do Forms Portal para listar rascunhos e envios na página Sites. Execute as seguintes etapas para adicionar o componente de portal **Rascunhos e Envios**:

1. Abra a página do AEM Sites no modo **Editar**.
1. Vá para as **[!UICONTROL Informações da Página]** > **[!UICONTROL Editar Modelo]**
   ![Editar política de modelo](/help/forms/assets/save-form-as-draft-edit-template.png)

1. Clique na **[!UICONTROL Política]** e marque a caixa de seleção **[!UICONTROL Rascunhos e Envios]** sob o **[Nome do Projeto do Arquétipo do AEM] - Forms e Portal de Comunicações**.

   ![Seleção de Política](/help/forms/assets/save-form-as-draft-enable-policy.png)

1. Clique em **[!UICONTROL Concluído]**.
1. Agora, abra novamente a página do AEM Sites no modo de criação.
1. Localize a seção no editor de páginas que permite adicionar o componente Forms Portal.
1. Clique no ícone **Adicionar**. O ícone é um sinal de mais (+) que significa a opção de adicionar novos componentes.

   Clicar no ícone **Adicionar** exibe uma caixa de diálogo **Inserir novo componente** que exibe vários componentes para inserção.

   >[!NOTE]
   >
   > Como alternativa, você também pode arrastar e soltar o componente.

1. Navegue pelos componentes disponíveis na caixa de diálogo e selecione o componente desejado na lista. Por exemplo, selecione o componente **Rascunhos e envios** na lista para adicionar o componente **Rascunhos e envios** do Forms Portal.

   ![Adicionar rascunho e componente de envio](/help/forms/assets/save-form-as-draft-add-dns.png)

Agora, configure as propriedades do componente **Rascunhos e Envios** de acordo com os requisitos.

## Configurar propriedades do componente de Rascunhos e Envios

Você pode configurar as propriedades de **Rascunhos e Envios**:

1. Selecione o componente de **Rascunhos e Envios**.
1. Clique no ![ícone Configurar](assets/configure_icon.png) e a caixa de diálogo será exibida.
1. Na caixa de diálogo **[!UICONTROL Rascunhos e Envios]**, especifique o seguinte:

   * **Título** Para identificar um componente em uma página do Sites e, por padrão, o título aparece na parte superior do componente.
   * **Selecionar tipo**: para indicar a listagem de formulários como rascunho ou formulários enviados. Se você escolher **Rascunho do Forms**, os formulários salvos como rascunhos serão exibidos. Como alternativa, selecionar **Forms Enviada** mostra os formulários enviados pelos usuários conectados.
   * **Layout**: para exibir formulários de rascunho de lista ou formulários enviados no formato de cartão ou lista.

   ![Propriedades dos componentes de Rascunho e Envio](/help/forms/assets/save-form-as-draft-dns-properties.png)

## Configurar formulários para serem salvos como rascunhos

Você pode configurar o Adaptive Forms das duas seguintes maneiras de salvá-los como rascunhos para uso posterior:

* [Ação do usuário](#user-action)
* [Salvar automático](#auto-save)

### Ação do usuário

>[!NOTE]
>
> Verifique se a versão dos [Componentes principais está definida como 3.0.24 ou posterior](https://github.com/adobe/aem-core-forms-components) para salvar formulários como rascunhos usando a regra **Salvar formulário**.

Para salvar um formulário como Rascunho, crie uma regra **Salvar Formulário** em um componente de formulário, como um botão. Quando o botão é clicado, a regra é acionada e o formulário é salvo como rascunho. Execute as seguintes etapas para criar uma regra **Salvar formulário** em um componente de botão:

1. Abra um Formulário adaptável em um modo de edição.
1. Selecione o ícone **[!UICONTROL Editar Regras]** para abrir o Editor de Regras para o componente **Botão**.
1. Selecione **[!UICONTROL Criar]** para configurar e criar a regra para o botão.
1. Na seção **[!UICONTROL Quando]**, selecione **está clicado** e na seção **[!UICONTROL Depois]**, selecione a opção **Salvar Formulário**.
1. Selecione **[!UICONTROL Concluído]** para salvar a regra.

   ![Criar regra para o botão](/help/forms/assets/save-form-as-drfat-create-rule.png)

Ao visualizar um formulário adaptável, preencha-o e clique no botão **Salvar formulário**, ele será salvo como rascunho.

### Rascunhos

>[!NOTE]
>
> Verifique se a versão dos [Componentes principais está definida como 3.0.52 ou posterior](https://github.com/adobe/aem-core-forms-components) para salvar formulários como rascunhos usando o recurso de salvamento automático.

Você também pode configurar um Formulário adaptável para salvar automaticamente com base em um evento baseado em tempo, garantindo que o formulário seja salvo após a duração especificada. Quando você [habilita componentes do Forms Portal para o seu ambiente](/help/forms/list-forms-on-sites-page.md#enable-forms-portal-components-for-your-existing-environment), a guia **Salvamento Automático** é exibida nas propriedades do contêiner Forms. Você pode configurar o recurso de salvamento automático para um Formulário adaptável:

1. Na instância do autor, abra um Formulário adaptável em um modo de edição.
1. Abra o navegador Conteúdo e selecione o componente **[!UICONTROL Contêiner do Guia]** do seu Formulário adaptável.
1. Clique no ícone de propriedades do Contêiner do Guia ![Propriedades do Guia](/help/forms/assets/configure-icon.svg) e abra a guia **[!UICONTROL Rascunhos]**.

   ![Salvamento automático](/help/forms/assets/auto-save.png)

1. Marque a caixa de seleção **[!UICONTROL Salvar rascunhos automaticamente]** para habilitar o salvamento automático do formulário como rascunhos.
1. Configure **[!UICONTROL Salvar Preferência]** como **Salvar rascunhos em intervalos regulares** para salvar automaticamente o formulário <!--based on the occurrence of an event or--> após um intervalo de tempo específico.
1. Especifique o intervalo em **[!UICONTROL Frequência do intervalo de salvamento (Segundos)]** para definir a duração que aciona o salvamento automático do formulário no intervalo definido.
1. Clique em **[!UICONTROL Concluído]**.

## Exibir rascunhos/formulários enviados na página Sites usando o componente Rascunhos e envios

Para exibir rascunhos salvos ou formulários enviados, use o componente do Portal do Forms **Rascunhos e Envios**.
Quando **[!UICONTROL Selecionar Tipo]** é selecionado como **Rascunho do Forms** na [caixa de diálogo de configuração do componente Rascunhos e Envios](#configure-properties-of-the-drafts--submissions-component), os formulários salvos como rascunhos são exibidos na página Sites. Você pode abrir os rascunhos clicando nas reticências (...) para preencher o formulário.

![Ícone Rascunhos](assets/drafts-component.png)

Quando **[!UICONTROL Selecionar Tipo]** é selecionado como **Forms Enviado** na [caixa de diálogo de configuração do componente Rascunhos e Envios](#configure-properties-of-the-drafts--submissions-component), os formulários enviados são exibidos. Você pode exibir os formulários enviados, mas não pode editá-los.

![Ícone de envios](assets/submission-listing.png)

Você também pode descartar os formulários clicando nas reticências (...) que aparecem no canto inferior direito do formulário.

>[!NOTE]
>
> No Portal do Forms, o componente Rascunhos e envios é compatível somente com envios de formulários baseados em Fundação.

## Próximas etapas

No próximo artigo, vamos aprender [como adicionar referências a formulários na página Sites usando o componente Link do Portal Forms](/help/forms/add-form-link-to-aem-sites-page.md).

## Artigos relacionados

{{forms-portal-see-also}}

## Consulte também {#see-also}

{{see-also}}