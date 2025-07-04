---
title: Importar formulários de metadados de [!DNL Admin View] para [!DNL Assets View]
description: Este artigo descreve como importar o formulário de metadados de [!DNL Admin View] para [!DNL Assets View]
contentOwner: AG
feature: Metadata
role: User, Admin
exl-id: 5fb4fe97-486a-4a91-af60-a7182efcc2f9
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 0%

---

# Importar formulários de metadados de [!DNL Admin View] para [!DNL Assets View] {#import-metadata-forms-from-admin-view-to-assets-view}

[!DNL Adobe Experience Manager Assets] permite importar formulários de metadados e suas associações de pastas de [!DNL Admin View] para [!DNL Assets View].

## Antes de começar{#prerequisites-for-importing-metadata-forms-to-assets-view}

Verifique se você tem direitos de administrador para importar os formulários de metadados e suas associações de pastas de [!DNL Admin View] para [!DNL Assets View].

## Importar formulários de metadados para [!DNL Assets View]{#import-metadata-forms-to-assets-view}

Como administrador, execute as seguintes etapas para importar os formulários de metadados disponíveis em [!DNL Admin View] para [!DNL Assets View]:

1. Navegue até a página inicial do [!DNL Assets View] e clique em **[!UICONTROL Forms de Metadados]** em **[!UICONTROL Configurações]** para abrir a página **[!UICONTROL Forms de Metadados]** exibindo a lista de formulários de metadados disponíveis no [!DNL Assets View].

   ![página de formulários de metadados](/help/assets/assets/metadata-forms-page.png)

1. Selecione **[!UICONTROL Importar]**, uma mensagem de processamento será exibida (por exemplo, *Processando 2 formulários de metadados... Aguarde.*) enquanto a importação está em andamento. Após a conclusão do processamento, a tabela **[!UICONTROL Importar formulários de metadados]** é exibida, o que inclui uma lista de formulários de metadados disponíveis em [!DNL Admin View]. A linha de tabela inclui, nome do formulário de metadados (em **[!UICONTROL Nome]**), pastas associadas a esse formulário (em **[!UICONTROL Associação de Pastas]**) e uma opção para visualizar ![visualizar](/help/assets/assets/Preview.svg) o formulário antes de importá-lo.

   ![Página Importar Forms de Metadados](/help/assets/assets/import-metadata-forms-page.png)

   >[!NOTE]
   > 
   > Na **[!UICONTROL Forms de Metadados de Importação]**, a tabela a **[!UICONTROL Duplicar]** ao lado de um nome de formulário mostra que o formulário já foi aplicado a uma pasta em [!DNL Assets View]. A importação desse formulário duplicado substitui o existente aplicado à pasta. Para evitar essa substituição, renomeie o formulário antes de importá-lo. Clique no nome do formulário para renomeá-lo.

1. Clique em ![selecionar pasta](/help/assets/assets/x.svg) ao lado de um nome de pasta (em [!UICONTROL Associação de Pastas]) para remover a associação de pastas com o formulário.
1. Clique em ![selecionar pasta](/help/assets/assets/add-to-folder.svg) para selecionar uma pasta à qual atribuir o formulário de metadados correspondente.
1. Clique no círculo vermelho para exibir detalhes sobre componentes de metadados ou mapeamentos não compatíveis no formulário que foram excluídos da importação.

   ![Página Importar Forms de Metadados](/help/assets/assets/unsupported-import-elements.png)

1. Selecione um ou mais formulários na tabela e clique em **[!UICONTROL Iniciar Importação]** para importar os formulários de metadados e suas pastas associadas para [!DNL Assets View]. Uma mensagem de processamento é exibida (por exemplo, *Importação de 3 formulários de metadados. Aguarde.*). Quando a importação for concluída, uma mensagem de êxito confirmará que os formulários foram importados com êxito e a página **[!UICONTROL Metadata Forms]** (de [!DNL Assets View]) exibirá formulários importados recentemente e existentes disponíveis em [!DNL Assets View]. Você pode fazer o seguinte nesta página:

   * Clique no cabeçalho da coluna para classificar a tabela por [!UICONTROL Nome], [!UICONTROL Modificado] ou [!UICONTROL Autor].
   * Selecione o formulário importado e clique em **[!UICONTROL Remover da(s) pasta(s)]**. Em seguida, verifique o nome da pasta no caminho da pasta para confirmar se a pasta está corretamente transferida.

     ![verificar página de formulários de metadados](/help/assets/assets/confirm-ported-folder.png)
   * Selecione o formulário importado e clique em **[!UICONTROL Editar]** para exibir todas as configurações compatíveis do formulário de metadados. Consulte [Configurar Forms de Metadados](https://experienceleague.adobe.com/pt-br/docs/experience-manager-assets-essentials/help/metadata#metadata-forms) para obter mais informações sobre os formulários de metadados, seus componentes e campos.

   ![verificar página de formulários de metadados](/help/assets/assets/verify-metadata-forms-page.png)

## Verificar os formulários de metadados importados{#Verify-the-imported-metadata-forms}

Após importar os formulários de metadados de [!DNL Admin View] para [!DNL Assets View], siga estas etapas para verificar a importação:

1. Navegue até qualquer uma das pastas associadas do formulário de metadados importado.
1. Navegue até uma [página de detalhes do ativo](/help/assets/navigate-assets-view.md#preview-assets) e verifique se os componentes de metadados, campos de componentes e valores de campo compatíveis estão sincronizados a partir de [!DNL Admin View]. Consulte o artigo [Metadados no Assets Essentials](https://experienceleague.adobe.com/pt-br/docs/experience-manager-assets-essentials/help/metadata) para obter mais informações sobre componentes de metadados, campos de componentes e valores de campos.

   >[!NOTE]
   >
   > Na [[!DNL Assets View] página de detalhes](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/assets/assets-view/metadata-assets-view#metadata-forms) ou na [[!DNL Admin View] página de propriedades](https://experienceleague.adobe.com/pt-br/docs/experience-manager-65/content/assets/administer/metadata-schemas), as alterações nos valores de propriedades de metadados são sincronizadas automaticamente entre as duas interfaces. No entanto, as alterações estruturais no formulário, como adicionar ou remover campos ou outras modificações, não são sincronizadas.
