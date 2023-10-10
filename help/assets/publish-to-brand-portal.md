---
title: Publicar ativos, pastas e coleções no Brand Portal
description: Publicar ativos, pastas e coleções no Brand Portal.
contentOwner: Vishabh Gupta
feature: Brand Portal,Asset Distribution,Configuration
role: User
exl-id: 1cc438bc-8cad-4421-af03-c1f6d750e0a8
source-git-commit: 7f806c457f7bef1c5309bbc6f69d3989af1b06d3
workflow-type: tm+mt
source-wordcount: '1301'
ht-degree: 90%

---

# Publicar ativos no Brand Portal {#publish-assets-to-brand-portal}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-65/assets/brandportal/brand-portal-publish-folder.html?lang=en) |
| AEM as a Cloud Service | Este artigo |

Como administrador do Adobe Experience Manager (AEM) Assets, você pode publicar ativos, pastas e coleções na instância do AEM Assets Brand Portal. Além disso, você pode agendar o fluxo de trabalho de publicação de um ativo ou pasta para uma data ou hora posterior. Depois de publicados, os usuários do Brand Portal podem acessar e distribuir os ativos, as pastas e as coleções para outros usuários.

No entanto, primeiro você deve configurar o AEM Assets com o Brand Portal. Para obter detalhes, consulte [Configurar o AEM Assets com o Brand Portal](configure-aem-assets-with-brand-portal.md).

Se fizer modificações subsequentes no ativo, pasta ou coleção original no AEM Assets, as alterações não serão refletidas no Brand Portal até que publique novamente no AEM Assets. Esse recurso garante que as alterações de trabalho em andamento não estejam disponíveis no Brand Portal. Somente as alterações aprovadas publicadas por um administrador são disponibilizadas no Brand Portal.

* [Publicar ativos no Brand Portal](#publish-assets-to-bp)
* [Publicar pastas no Brand Portal](#publish-folders-to-brand-portal)
* [Publicar coleções no Brand Portal](#publish-collections-to-brand-portal)

>[!NOTE]
>
>A Adobe recomenda uma publicação escalonada, de preferência durante horários que não sejam de pico, para que o autor do AEM não ocupe recursos excessivos.
>Os ativos devem ser publicados em lotes. A recomendação para o tamanho do lote é de 15K.
> Para [!DNL Experience Manager Assets] as a [!DNL Cloud Service], a taxa de transferência observada nas condições do laboratório é de 1000 ativos por hora. A taxa é observada com um tamanho médio de ativos de 10 MB.

## Publicar ativos no Brand Portal {#publish-assets-to-bp}

Veja a seguir as etapas para publicar ativos do AEM Assets no Brand Portal:

1. No console Assets, abra a pasta principal, selecione todos os ativos que deseja publicar e clique na opção **[!UICONTROL Publicação rápida]** na barra de ferramentas.

   ![publish2bp-2](assets/publish2bp.png)

1. Veja a seguir as duas maneiras de publicar ativos:
   * [Publicar agora](#publish-to-bp-now) (Publicar ativos imediatamente)
   * [Publicar mais tarde](#publish-to-bp-later) (agendar a publicação de ativos)

### Publicar ativos agora {#publish-to-bp-now}

Para publicar os ativos selecionados no Brand Portal, siga um dos procedimentos a seguir:

* Na barra de ferramentas, selecione **[!UICONTROL Publicação rápida]**. Em seguida, no menu, clique em **[!UICONTROL Publicar no Brand Portal]**.

* Na barra de ferramentas, selecione **[!UICONTROL Gerenciar publicação]**.

   1. Em **[!UICONTROL Ação]**, selecione **[!UICONTROL Publicar no Brand Portal]**.

      Em **[!UICONTROL Agendamento]**, selecione **[!UICONTROL Agora]**.

      Clique em **[!UICONTROL Avançar]**.

   2. Confirme sua seleção no **[!UICONTROL Escopo]** e clique em **[!UICONTROL Publicar no Brand Portal]**.

Será exibida uma mensagem informando que os ativos foram enfileirados para publicação no Brand Portal. Faça logon na interface do Brand Portal para ver os ativos publicados.

### Publicar ativos mais tarde {#publish-to-bp-later}

Para agendar a publicação dos ativos no Brand Portal para uma data ou hora posterior:

1. Selecione os ativos que deseja agendar a publicação e clique em **[!UICONTROL Gerenciar publicação]** na barra de ferramentas na parte superior.

1. Na página **[!UICONTROL Gerenciar publicação]**, selecione **[!UICONTROL Publicar no Brand Portal]** a partir de **[!UICONTROL Ação]**.

   Selecione **[!UICONTROL Mais tarde]** em **[!UICONTROL Agendamento]**.

   ![publishlaterbp-1](assets/publishlaterbp-1.png)

1. Selecione uma **[!UICONTROL Data de ativação]** e especifique a hora. Clique em **[!UICONTROL Avançar]**.

1. Selecione uma **Data de ativação** e especifique a hora. Clique em **Avançar**.

1. Especifique um **[!UICONTROL Título de fluxo de trabalho]** em **[!UICONTROL Fluxos de trabalho]**. Clique em **[!UICONTROL Publicar mais tarde]**.

   ![publishworkflow](assets/publishworkflow.png)

Faça logon na interface do Brand Portal para ver os ativos publicados (dependendo da data ou hora agendadas).

![bp_landingpage](assets/bp_landingpage.png)

>[!NOTE]
>
> * A parte de usuários existente do grupo Usuários DAM tem acesso de leitura no caminho &quot;/conf/global/settings/cloudconfigs/mediaportal&quot;
>* Os novos usuários (ou usuários não administradores) exigem os seguintes direitos para publicar no brand portal.
> Caminhos:
> &quot;/conf/global/settings/cloudconfigs/mediaportal&quot; : jcr:read
>/libs : jcr:read
>/conf : jcr:read
>/content : jcr:read, crx:replicate
>/content/dam/ : jcr:read,modify, crx:replicate

## Publicar pastas no Brand Portal {#publish-folders-to-brand-portal}

Você pode publicar ou cancelar a publicação de pastas de ativos imediatamente ou agendar para uma data ou hora posterior.

### Publicar pastas no Brand Portal {#publish-folders-to-bp}

1. No console Assets, selecione as pastas que deseja publicar e clique na opção **[!UICONTROL Publicação rápida]** na barra de ferramentas.

   ![publish2bp](assets/publish2bp.png)

1. **Publicar pastas agora**

   Para publicar as pastas selecionadas no Brand Portal, siga um dos procedimentos a seguir:

   * Na barra de ferramentas, selecione **[!UICONTROL Publicação rápida]**.

     No menu, selecione **[!UICONTROL Publicar no Brand Portal]**.

   * Na barra de ferramentas, selecione **[!UICONTROL Gerenciar publicação]**.

      1. Em **[!UICONTROL Ação]**, selecione **[!UICONTROL Publicar no Brand Portal]**.

         Em **[!UICONTROL Agendamento]**, selecione **[!UICONTROL Agora]**.

         Clique em **Avançar.**

      1. Confirme sua seleção no **[!UICONTROL Escopo]** e clique em **[!UICONTROL Publicar no Brand Portal]**.

   Será exibida uma mensagem informando que a pasta foi colocada na fila para publicação no Brand Portal. Faça logon na interface do Brand Portal para ver a pasta publicada.

1. **Publicar pastas mais tarde**

   Para agendar a publicação das pastas de ativos para uma data ou hora posterior:

   1. Selecione as pastas que deseja agendar a publicação e selecione **[!UICONTROL Gerenciar publicação]** na barra de ferramentas na parte superior.
   1. Em **[!UICONTROL Ação]**, selecione **[!UICONTROL Publicar no Brand Portal]**.

      Em **[!UICONTROL Agendamento]**, selecione **[!UICONTROL Mais tarde]**.

   1. Selecione uma **[!UICONTROL Data de ativação]** e especifique a hora. Clique em **[!UICONTROL Avançar]**.

      ![publishlaterbp](assets/publishlaterbp.png)

   1. Confirme sua seleção no **[!UICONTROL Escopo]**. Clique em **[!UICONTROL Avançar]**.

   1. Especifique um título de Fluxo de trabalho em **[!UICONTROL Fluxos de trabalho]**. Clique em **[!UICONTROL Publicar mais tarde]**.

      ![manageschedulepub](assets/manageschedulepub.png)

### Cancelar publicação de pastas do Brand Portal {#unpublish-folders-from-brand-portal}

Você pode remover qualquer pasta de ativos publicada no Brand Portal ao cancelar a publicação da instância do AEM Assets. Após cancelar a publicação da pasta original, a cópia não estará mais disponível para os usuários do Brand Portal.

Você pode cancelar a publicação de pastas de ativos do Brand Portal imediatamente ou agendar para uma data e hora posteriores.

Para cancelar a publicação de pastas de ativos do Brand Portal:

1. No console Assets, selecione as pastas de ativos que deseja publicar e clique na opção **[!UICONTROL Gerenciar publicação]** na barra de ferramentas.

   ![publish2bp-1](assets/publish2bp.png)

1. **Cancelar a publicação de pastas de ativos agora**

   Para cancelar a publicação da pasta de ativos selecionada imediatamente no Brand Portal:

   1. Na barra de ferramentas, selecione **[!UICONTROL Gerenciar publicação]**.

   1. Em **[!UICONTROL Ação]**, selecione **[!UICONTROL Cancelar publicação do Brand Portal]**.

      Em **[!UICONTROL Agendamento]**, selecione **[!UICONTROL Agora]**.

      Clique em **[!UICONTROL Avançar]**.

   1. Confirme sua seleção no **[!UICONTROL Escopo]** e clique em **[!UICONTROL Cancelar publicação no Brand Portal]**.

      ![confirm-unpublish](assets/confirm-unpublish.png)

1. **Cancelar a publicação de pastas de ativos mais tarde**

   Para agendar o cancelamento de publicação de uma pasta de ativos para uma data e hora posteriores:

   1. Na barra de ferramentas, selecione **[!UICONTROL Gerenciar publicação]**.

   1. Em **[!UICONTROL Ação]**, selecione **[!UICONTROL Cancelar publicação do Brand Portal]**.

      Em **[!UICONTROL Agendamento]**, selecione **[!UICONTROL Mais tarde]**.

   1. Selecione uma **[!UICONTROL Data de ativação]** e especifique a hora. Clique em **[!UICONTROL Avançar]**.

   1. Confirme a seleção no **[!UICONTROL Escopo]** e clique em **[!UICONTROL Avançar]**.

   1. Especifique um **[!UICONTROL Título de fluxo de trabalho]** em **[!UICONTROL Fluxos de trabalho]**. Clique em **[!UICONTROL Cancelar publicação mais tarde]**.

      ![unpublishworkflows](assets/unpublishworkflows.png)

## Publicar coleções no Brand Portal {#publish-collections-to-brand-portal}

Você pode publicar ou cancelar a publicação de coleções da instância da nuvem do AEM Assets.

>[!NOTE]
>
>Os fragmentos de conteúdo não podem ser publicados no Brand Portal. Portanto, se selecionar fragmentos de conteúdo no AEM Assets, a ação **[!UICONTROL Publicar no Brand Portal]** não estará disponível.
>
>Se as coleções que contêm fragmentos de conteúdo forem publicadas do AEM Assets no Brand Portal, todo o conteúdo da pasta, exceto fragmentos de conteúdo, será replicado para a interface do Brand Portal.

### Publicar coleções {#publish-collections}

Veja a seguir as etapas para publicar coleções do AEM Assets no Brand Portal:

1. Na interface do usuário do AEM Assets, clique no logotipo do AEM.

1. Na página **Navegação**, acesse **[!UICONTROL Ativos]** > **[!UICONTROL Coleções]**.

1. No console **Coleções**, selecione as coleções que deseja publicar no Brand Portal.

   ![select_collection](assets/select_collection.png)

1. Na barra de ferramentas, clique em **[!UICONTROL Publicar no Brand Portal]**.

1. Na caixa de diálogo de confirmação, clique em **[!UICONTROL Publicar]**.

1. Feche a mensagem de confirmação.

   Faça logon no Brand Portal como administrador.  A coleção publicada está disponível no console Coleções.

   ![coleção publicada](assets/published_collection.png)

### Cancelar publicação de coleções {#unpublish-collections}

Você pode remover qualquer coleção publicada no Brand Portal ao cancelar a publicação a partir da instância do AEM Assets. Após cancelar a publicação da coleção original, a cópia não estará mais disponível para os usuários do Brand Portal.

Veja a seguir as etapas para cancelar a publicação de uma coleção:

1. No console **Coleções** da instância do AEM Assets, selecione a coleção que deseja cancelar a publicação.

   ![select_collection](assets/select_collection-1.png)

1. Na barra de ferramentas, clique no ícone **[!UICONTROL Remover do Brand Portal]**.
1. Na caixa de diálogo, clique em **[!UICONTROL Cancelar publicação]**.
1. Feche a mensagem de confirmação. A coleção é removida da interface do Brand Portal.

Além do que foi descrito acima, você também pode publicar esquemas de metadados, predefinições de imagens, aspectos de pesquisa e tags do AEM Assets para o Brand Portal.

* [Publicar predefinições, esquemas e aspectos no Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/publish-schema-search-facets-presets.html)
* [Publicar marcações no Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/brand-portal-publish-tags.html)


Consulte a [documentação do Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html) para obter mais informações.


<!--
   Comment Type: draft

   <li> </li>
   -->

<!--
   Comment Type: draft

   <li>Step text</li>
   -->

**Consulte também**

* [Traduzir ativos](translate-assets.md)
* [API HTTP de ativos](mac-api-assets.md)
* [Formatos de arquivo compatíveis com os ativos](file-format-support.md)
* [Pesquisar ativos](search-assets.md)
* [Ativos conectados](use-assets-across-connected-assets-instances.md)
* [Relatórios de ativos](asset-reports.md)
* [Esquemas de metadados](metadata-schemas.md)
* [Baixar ativos](download-assets-from-aem.md)
* [Gerenciar metadados](manage-metadata.md)
* [Pesquisar aspectos](search-facets.md)
* [Gerenciar coleções](manage-collections.md)
* [Importação de metadados em massa](metadata-import-export.md)
