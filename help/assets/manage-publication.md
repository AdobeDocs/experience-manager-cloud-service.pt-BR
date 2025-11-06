---
title: 'Gerenciar publicação   '
description: Publicar ou cancelar a publicação de ativos no Experience Manager Assets, Dynamic Media e Brand Portal
mini-toc-levels: 1
feature: Asset Management, Publishing, Collaboration, Asset Processing
role: User, Developer, Admin
exl-id: 691a0925-0061-4c62-85ac-8257b96dddf2
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1536'
ht-degree: 4%

---

# Gerenciar publicação no Experience Manager Assets {#manage-publication-in-aem}

Como administrador do [!DNL Adobe Experience Manager Assets], você pode publicar ativos e pastas contendo ativos da instância do autor no [!DNL Experience Manager Assets], [!DNL Dynamic Media] e [!DNL Brand Portal]. Além disso, você pode agendar a publicação de um ativo ou pasta em uma data ou hora posterior. Após a publicação, os usuários podem acessar e distribuir os ativos para outros usuários. Por padrão, você pode publicar ativos e pastas em [!DNL Experience Manager Assets]. No entanto, você pode configurar o [!DNL Experience Manager Assets] para habilitar a publicação no [[!DNL Dynamic Media]](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/config-dm.html?lang=pt-BR) e [[!DNL Brand Portal]](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/brand-portal/configure-aem-assets-with-brand-portal.html?lang=pt-BR).

Você pode publicar ou desfazer a publicação de ativos no nível do ativo ou da pasta, usando a opção **[!UICONTROL Publicação rápida]** ou **[!UICONTROL Gerenciar publicação]**, disponível na interface [!DNL Experience Manager Assets]. Se você fizer modificações subsequentes no ativo ou pasta original em [!DNL Experience Manager Assets], as alterações não serão refletidas na instância de publicação até que você publique novamente a partir de [!DNL Experience Manager Assets]. Isso garante que as alterações de trabalho em andamento não estejam disponíveis na instância de publicação. Somente as alterações aprovadas publicadas por um administrador estão disponíveis na instância de publicação.

* [Publicar ativos usando a Publicação rápida](#quick-publish)
* [Publicar ativos usando Gerenciar publicação](#manage-publication)
* [Publicar ativos mais tarde](#publish-assets-later)
* [Publicar ativos no Dynamic Media](#publish-assets-to-dynamic-media)
* [Publicar ativos no Brand Portal](#publish-assets-to-brand-portal)
* [Solicitar Publicação](#request-publication)
* [Limitações e dicas](#limitations-and-tips)

## Publicar ativos usando a Publicação rápida {#quick-publish}

A Publicação rápida permite publicar imediatamente o conteúdo no destino selecionado. No console [!DNL Experience Manager Assets], navegue até a pasta principal e selecione todos os ativos ou pastas que deseja publicar. Clique na opção **[!UICONTROL Publicação rápida]** na barra de ferramentas e selecione o destino na lista suspensa onde deseja publicar os ativos.

![Publicação rápida](assets/quick-publish-to-aem.png)

## Publicar ativos usando Gerenciar publicação {#manage-publication}

Gerenciar publicação permite publicar ou desfazer a publicação de conteúdo de e para o destino selecionado, [adicionar conteúdo](#add-content) à lista de publicação em todo o repositório DAM, [incluir configurações de pasta](#include-folder-settings) para publicar o conteúdo das pastas selecionadas e aplicar filtros, e [agendar publicações](#publish-assets-later) para uma data ou hora posterior.

No console [!DNL Experience Manager Assets], navegue até a pasta principal e selecione todos os ativos ou pastas que deseja publicar. Clique na opção **[!UICONTROL Gerenciar publicação]** na barra de ferramentas. Se você não tiver o [!DNL Dynamic Media] e o [!DNL Brand Portal] configurados na instância do [!DNL Experience Manager Assets], será possível publicar ativos e pastas somente no [!DNL Experience Manager Assets].

![Gerenciar publicação](assets/manage-publication-aem.png)

As seguintes opções estão disponíveis na interface [!UICONTROL Gerenciar Publicação]:

* [!UICONTROL Ações]
   * `Publish`: publicar ativos e pastas no destino selecionado
   * `Unpublish`: cancelar a publicação de ativos e pastas do destino

* [!UICONTROL Destino]
   * `Publish`: Publicar ativos e pastas em [!DNL Experience Manager Assets] (`AEM`)
   * `Dynamic Media`: Publicar ativos em [!DNL Dynamic Media]
   * `Brand Portal`: Publicar ativos e pastas em [!DNL Brand Portal]

* [!UICONTROL Programação]
   * `Now`: publicar ativos imediatamente
   * `Later`: Publicar ativos com base na data ou hora `Activation`

Para continuar, clique em **[!UICONTROL Avançar]**. Com base na seleção, a guia **[!UICONTROL Escopo]** reflete opções diferentes. As opções **[!UICONTROL Adicionar Conteúdo]** e **[!UICONTROL Incluir Configurações de Pasta]** estão disponíveis apenas para publicação de ativos e pastas em [!DNL Experience Manager Assets] (`Destination: Publish`).

![Gerenciar escopo de publicação](assets/manage-publication-aem-scope.png)

### Adicionar conteúdo {#add-content}

A publicação no [!DNL Experience Manager Assets] permite adicionar mais conteúdo (ativos e pastas) à lista de publicação. Você pode adicionar mais ativos ou pastas à lista nos repositórios DAM. Clique no botão **[!UICONTROL Adicionar Conteúdo]** para adicionar mais conteúdo.

É possível adicionar vários ativos de uma pasta ou adicionar várias pastas de uma vez. Mas não é possível adicionar ativos de várias pastas de uma vez.

![Adicionar conteúdo](assets/manage-publication-add-content.png)

### Incluir configurações de pasta {#include-folder-settings}

Por padrão, a publicação de uma pasta no [!DNL Experience Manager Assets] publica todos os ativos, subpastas e suas referências.

Para filtrar o conteúdo da pasta que você deseja publicar, clique em **[!UICONTROL Incluir configurações da pasta]**:

* `Include folder contents`

   * Ativado: todos os ativos da pasta selecionada, as subpastas (incluindo todos os ativos das subpastas) e as referências são publicadas.
   * Desativado: somente a pasta selecionada (vazia) e as referências são publicadas. Os ativos da pasta selecionada não são publicados.

* `Include folder contents` e `Include only immediate folder contents`

  Se ambas as opções forem selecionadas, todos os ativos da pasta selecionada, as subpastas (vazias) e as referências serão publicadas. Os ativos das subpastas não são publicados.

<!--
* [!UICONTROL Include only immediate folder contents]: Only the subfolders content and references are published. 

Only the selected folder content and references are published.
-->

![Incluir configurações da pasta](assets/manage-publication-include-folder-settings.png)

Depois de aplicar os filtros, clique em **[!UICONTROL OK]** e em **[!UICONTROL Publicar]**. Ao clicar no botão Publicar, uma mensagem de confirmação `Resource(s) have been scheduled for publication` é exibida. E os ativos e (ou) pastas selecionados são publicados no destino definido com base no agendador (`Now` ou `Later`). Faça logon na instância de publicação para verificar se os ativos e (ou) as pastas foram publicados com êxito.

![Publicar no AEM](assets/manage-publication-publish-aem.png)

Na ilustração acima, você pode ver valores diferentes para o atributo **[!UICONTROL Destino de publicação]**. Lembre-se de que você optou por publicar em [!DNL Experience Manager Assets] (`Destination: Publish`). Então, por que ele mostra que apenas uma pasta e um ativo são publicados em `AEM`, e os outros dois ativos são publicados em `AEM` e `Dynamic Media`?

Aqui, você deve entender a função das propriedades da pasta. A propriedade **[!UICONTROL Modo de publicação do Dynamic Media]** de uma pasta desempenha uma função importante na publicação. Para exibir as propriedades de uma pasta, selecione uma pasta e clique em **[!UICONTROL Propriedades]** na barra de ferramentas. Para um ativo, consulte as propriedades da pasta principal.

A tabela a seguir explica como ocorre a publicação dependendo do **[!UICONTROL Destino]** e do **[!UICONTROL Modo de publicação do Dynamic Media]** definidos:

| [!UICONTROL Destino] | [!UICONTROL Modo de publicação do Dynamic Media] | [!UICONTROL Destino de publicação] | Conteúdo permitido |
| --- | --- | --- | --- |
| Publicação | Publicação seletiva | `AEM` | Assets e/ou pastas |
| Publicação | Imediato | `AEM` e `Dynamic Media` | Assets e/ou pastas |
| Publicação | Por ativação | `AEM` e `Dynamic Media` | Assets e/ou pastas |
| Dynamic Media | Publicação seletiva | `Dynamic Media` | Ativos |
| Dynamic Media | Imediato | `None` | Não é possível publicar os ativos |
| Dynamic Media | Por ativação | `None` | Não é possível publicar os ativos |

>[!NOTE]
>
>Somente os ativos são publicados em [!DNL Dynamic Media].
>
>Não há suporte para a publicação de uma pasta em [!DNL Dynamic Media].
>
>Se você selecionar uma pasta (`Selective Publish`) e escolher o destino [!DNL Dynamic Media], o atributo [!UICONTROL Destino de publicação] refletirá `None`.


Vamos agora alterar o **[!UICONTROL Destino]** no caso de uso acima para **[!UICONTROL Dynamic Media]** e verificar os resultados. Ao fazer isso, somente o ativo da pasta `Selective Publish` é publicado em [!DNL Dynamic Media]. Os ativos das pastas `Immediate` e `Upon Activation` não foram publicados e refletem `None`.

![Publicar no Dynamic Media](assets/manage-publication-dynamic-media.png)

>[!NOTE]
>
>Se [!DNL Dynamic Media] não estiver configurado na instância [!DNL Experience Manager Assets] e o **[!UICONTROL Destino]** for **[!UICONTROL Publicar]**, os ativos e as pastas serão sempre publicados em `AEM`.
>
>A publicação em [!DNL Brand Portal] é independente das propriedades da pasta. Todos os ativos, pastas e coleções podem ser publicados no Brand Portal. Consulte [publicar ativos no Brand Portal](#publish-assets-to-brand-portal).

>[!NOTE]
>
>Se você tiver personalizado o assistente do [!DNL Manage Publication], sua personalização continuará a funcionar com as funcionalidades existentes.
>
>No entanto, você pode remover a personalização existente para usar os novos recursos do [!DNL Manager Publication].

## Publicar ativos mais tarde {#publish-assets-later}

Para agendar o fluxo de trabalho de publicação de ativos para uma data ou hora posterior:

1. No console [!UICONTROL Experience Manager Assets], navegue até a pasta principal e selecione todos os ativos ou pastas que deseja agendar a publicação.
1. Clique na opção **[!UICONTROL Gerenciar publicação]** na barra de ferramentas.
1. Clique em **[!UICONTROL Publicar]** de **[!UICONTROL Ação]** e selecione o **[!UICONTROL Destino]** onde deseja publicar o conteúdo.
1. Selecione **[!UICONTROL Mais tarde]** em **[!UICONTROL Agendamento]**.
1. Selecione uma **[!UICONTROL Data de ativação]** e especifique a data e a hora. Clique em **[!UICONTROL Avançar]**.

   ![Gerenciar Fluxo de Trabalho de Publicação](assets/manage-publication-workflow.png)

1. Na guia **[!UICONTROL Escopo]**, **[!UICONTROL Adicionar Conteúdo]** (se necessário). Clique em **[!UICONTROL Avançar]**.
1. Na guia **[!UICONTROL Workflows]**, especifique um título de Fluxo de Trabalho. Clique em **[!UICONTROL Publicar mais tarde]**.

   ![Título do fluxo de trabalho](assets/manage-publication-workflow-title.png)

   Faça logon na instância de destino para verificar os ativos publicados (dependendo da data ou hora agendadas).

## Publicar ativos no Dynamic Media {#publish-assets-to-dynamic-media}

Somente os ativos são publicados em [!DNL Dynamic Media]. No entanto, o comportamento de publicação é diferente com base nas propriedades da pasta. Uma pasta pode ter o **[!UICONTROL modo de Publicação do Dynamic Media]** configurado para publicação seletiva, que pode ser qualquer um dos seguintes:

* `Selective Publish`
* `Immediate`
* `Upon Activation`

O processo de publicação para **[!UICONTROL Imediato]** e **[!UICONTROL Na Ativação]** é consistente, no entanto, diferente para **[!UICONTROL Publicação Seletiva]**. Consulte [configurar publicação seletiva no nível da pasta no Dynamic Media](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/selective-publishing.html?lang=pt-BR). Depois de configurar a publicação seletiva em uma pasta, siga um destes procedimentos:

* [Publicar ativos seletivamente no Dynamic Media ou no Experience Manager usando Gerenciar publicação](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/selective-publishing.html?lang=en#selective-publish-manage-publication)
* [Cancelar a publicação seletiva de ativos do Dynamic Media ou do Experience Manager usando Gerenciar publicação](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/selective-publishing.html?lang=en#selective-unpublish-manage-publication)
* [Publicar ativos no Dynamic Media ou Experience Manager usando a Publicação rápida](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/selective-publishing.html?lang=en#quick-publish-aem-dm)
* [Publicar ou cancelar a publicação seletiva de ativos por meio dos resultados da pesquisa](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/selective-publishing.html?lang=en#selective-publish-unpublish-search-results)

## Publicar ativos no Brand Portal {#publish-assets-to-brand-portal}

Você pode publicar ativos, pastas e coleções na instância [!DNL Experience Manager Assets Brand Portal].

* [Publicar ativos no Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/brand-portal/publish-to-brand-portal.html?lang=en#publish-assets-to-bp)
* [Publicar pastas no Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/brand-portal/publish-to-brand-portal.html?lang=en#publish-folders-to-brand-portal)
* [Publicar coleções no Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/brand-portal/publish-to-brand-portal.html?lang=en#publish-collections-to-brand-portal)

## Solicitar Publicação {#request-publication}

A opção `Request Publication` ajuda na autenticação do fluxo de trabalho do Assets antes de publicá-lo no ambiente do Assets [!DNL AEM]. [!DNL AEM] fornece diferentes níveis de permissões para vários usuários. Você pode ser um *colaborador* que está carregando ativos, mas não pode publicá-los até que os carregamentos sejam verificados. Além disso, como *Administrador*, você pode gerenciar fluxos de trabalho de leitura e gravação da Assets.

A opção Solicitar publicação está disponível para os seguintes usuários:

* **Colaborador:** se você for um usuário que pode contribuir para o Assets [!DNL AEM], terá acesso limitado ao fluxo de trabalho do Assets [!DNL AEM]. O botão `Manage publication` está oculto para você. Como colaborador, você só pode contribuir adicionando Assets, mas não pode publicá-los ou ter acesso de leitura ao fluxo de trabalho.

* **Usuário do fluxo de trabalho:** este usuário não pode publicar ativos, mas tem acesso de leitura ao fluxo de trabalho. Como usuário de workflow, você pode:
   * solicitar publicação
   * botão exibir `Manage publication`
   * agende o fluxo de trabalho e veja as opções `schedule now` e `schedule later`

* **Administrador:** Como um tipo de administrador de usuário, você pode gerenciar etapas gerais de fluxo de trabalho para a Assets. O botão `Manage publication` está visível para você. Se o destino `publish` estiver selecionado, você poderá agendar um Ativo mais tarde para a etapa do fluxo de trabalho.

>[!NOTE]
>
>Se [!DNL Dynamic Media] for selecionado como destino, a etapa do fluxo de trabalho será desabilitada para **usuários do fluxo de trabalho** e **administradores**.
>

## Limitações e dicas {#limitations-and-tips}

* `Manage publication` está disponível para os usuários que têm pelo menos permissões de Leitura para o fluxo de trabalho.
* Pastas vazias não são publicadas.
* Se você publicar um ativo que está sendo processado, somente o conteúdo original será publicado. As representações estão ausentes. Aguarde a conclusão do processamento e publique ou republique o ativo depois que o processamento for concluído.
* Ao desfazer a publicação de um ativo complexo, cancele a publicação somente do ativo. Evite desfazer a publicação das referências, pois elas podem ser referenciadas por outros ativos publicados.
