---
title: 'Gerenciar publicação   '
description: Publicar ou desfazer a publicação de ativos no Experience Manager Assets, Dynamic Media e Brand Portal
contentOwner: Vishabh Gupta
mini-toc-levels: 1
feature: Asset Management, Publishing, Collaboration, Asset Processing
role: User, Architect, Admin
exl-id: 691a0925-0061-4c62-85ac-8257b96dddf2
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '1491'
ht-degree: 8%

---

# Gerenciar publicação no Experience Manager Assets {#manage-publication-in-aem}

Como um [!DNL Adobe Experience Manager Assets] administrador é possível publicar ativos e pastas que contêm ativos da instância de criação para o [!DNL Experience Manager Assets], [!DNL Dynamic Media]e [!DNL Brand Portal]. Além disso, você pode agendar o fluxo de trabalho de publicação de um ativo ou pasta para uma data ou hora posterior. Após a publicação, os usuários podem acessar e distribuir os ativos para outros usuários. Por padrão, é possível publicar ativos e pastas para [!DNL Experience Manager Assets]. No entanto, é possível configurar [!DNL Experience Manager Assets] para ativar a publicação [[!DNL Dynamic Media]](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/config-dm.html) e [[!DNL Brand Portal]](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/brand-portal/configure-aem-assets-with-brand-portal.html).

Você pode publicar ou cancelar a publicação de ativos no nível do ativo ou da pasta, usando **[!UICONTROL Publicação rápida]** ou **[!UICONTROL Gerenciar publicação]** disponível na [!DNL Experience Manager Assets] interface. Se fizer modificações subsequentes no ativo ou pasta original em [!DNL Experience Manager Assets], as alterações não são refletidas na instância de publicação até que você republique de [!DNL Experience Manager Assets]. Isso garante que as alterações de trabalho em andamento não estejam disponíveis na instância de publicação. Somente as alterações aprovadas publicadas por um administrador estão disponíveis na instância de publicação.

* [Publicar ativos usando a Publicação rápida](#quick-publish)
* [Publicar ativos usando Gerenciar publicação](#manage-publication)
* [Publicar ativos mais tarde](#publish-assets-later)
* [Publicar ativos no Dynamic Media](#publish-assets-to-dynamic-media)
* [Publicar ativos no Brand Portal](#publish-assets-to-brand-portal)
* [Limitações e dicas](#limitations-and-tips)

## Publicar ativos usando a Publicação rápida {#quick-publish}

A publicação rápida permite publicar imediatamente o conteúdo no destino selecionado. No [!DNL Experience Manager Assets] , navegue até a pasta principal e selecione todos os ativos ou pastas que deseja publicar. Clique em **[!UICONTROL Publicação rápida]** na barra de ferramentas e selecione o destino na lista suspensa onde deseja publicar os ativos.

![Publicação rápida](assets/quick-publish-to-aem.png)

## Publicar ativos usando Gerenciar publicação {#manage-publication}

Gerenciar publicação permite publicar ou desfazer a publicação de conteúdo de e para o destino selecionado, [adicionar conteúdo](#add-content) para a lista de publicação em todo o repositório DAM, [incluir configurações de pasta](#include-folder-settings) para publicar o conteúdo das pastas selecionadas e aplicar filtros, e [agendar publicação](#publish-assets-later) para uma data ou hora posterior.

No [!DNL Experience Manager Assets] , navegue até a pasta principal e selecione todos os ativos ou pastas que deseja publicar. Clique em **[!UICONTROL Gerenciar publicação]** na barra de ferramentas. Se você não tiver [!DNL Dynamic Media] e [!DNL Brand Portal] configurado no [!DNL Experience Manager Assets] , é possível publicar ativos e pastas somente para [!DNL Experience Manager Assets].

![Gerenciar publicação](assets/manage-publication-aem.png)

As seguintes opções estão disponíveis na variável [!UICONTROL Gerenciar publicação] interface:

* [!UICONTROL Ações]
   * `Publish`: Publicar ativos e pastas no destino selecionado
   * `Unpublish`: Cancelar a publicação de ativos e pastas do destino

* [!UICONTROL Destino]
   * `Publish`: Publicar ativos e pastas em [!DNL Experience Manager Assets] (`AEM`)
   * `Dynamic Media`: Publicar ativos no [!DNL Dynamic Media]
   * `Brand Portal`: Publicar ativos e pastas em [!DNL Brand Portal]

* [!UICONTROL Programação]
   * `Now`: Publicar ativos imediatamente
   * `Later`: Publicar ativos com base no `Activation` data ou hora

Para continuar, clique em **[!UICONTROL Próximo]**. Com base na seleção, a variável **[!UICONTROL Escopo]** A guia reflete opções diferentes. As opções para **[!UICONTROL Adicionar conteúdo]** e **[!UICONTROL Incluir configurações de pasta]** estão disponíveis somente para publicar ativos e pastas em [!DNL Experience Manager Assets] (`Destination: Publish`).

![Gerenciar escopo de publicação](assets/manage-publication-aem-scope.png)

### Adicionar conteúdo {#add-content}

>[!NOTE]
>
>Esse recurso está disponível no canal de pré-lançamento. Consulte [Documentação do Canal de pré-lançamento](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html#enable-prerelease) para obter informações sobre como habilitar o recurso para seu ambiente.

Publicar em [!DNL Experience Manager Assets] permite adicionar mais conteúdo (ativos e pastas) à lista de publicação. Você pode adicionar mais ativos ou pastas à lista nos repositórios dam. Clique em **[!UICONTROL Adicionar conteúdo]** para adicionar mais conteúdo.

Você pode adicionar vários ativos de uma pasta ou adicionar várias pastas de cada vez. Mas não é possível adicionar ativos de várias pastas de cada vez.

![Adicionar conteúdo](assets/manage-publication-add-content.png)

### Incluir configurações de pasta {#include-folder-settings}

>[!NOTE]
>
>Esse recurso está disponível no canal de pré-lançamento. Consulte [Documentação do Canal de pré-lançamento](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html#enable-prerelease) para obter informações sobre como habilitar o recurso para seu ambiente.

Por padrão, publicar uma pasta em [!DNL Experience Manager Assets] O publica todos os ativos, subpastas e suas referências.

Para filtrar o conteúdo da pasta que deseja publicar, clique em **[!UICONTROL Incluir configurações de pasta]**:

* `Include folder contents`

   * Ativado: Todos os ativos da pasta selecionada, as subpastas (incluindo todos os ativos das subpastas) e as referências são publicadas.
   * Desativado: Somente a pasta selecionada (vazia) e as referências são publicadas. Os ativos da pasta selecionada não são publicados.

* `Include folder contents` e `Include only immediate folder contents`

   Se ambas as opções forem selecionadas, todos os ativos da pasta selecionada, as subpastas (vazias) e as referências serão publicadas. Os ativos das subpastas não são publicados.

<!--
* [!UICONTROL Include only immediate folder contents]: Only the subfolders content and references are published. 

Only the selected folder content and references are published.
-->

![Incluir configurações de pasta](assets/manage-publication-include-folder-settings.png)

Depois de aplicar os filtros, clique em **[!UICONTROL OK]** e, em seguida, clique em **[!UICONTROL Publicar]**. Ao clicar no botão publicar, uma mensagem de confirmação `Resource(s) have been scheduled for publication` é exibido. E os ativos e (ou) pastas selecionados são publicados no destino definido com base no programador (`Now` ou `Later`). Faça logon na sua instância de publicação para verificar se os ativos e (ou) as pastas foram publicados com êxito.

![Publicar no AEM](assets/manage-publication-publish-aem.png)

Na ilustração acima, você pode ver valores diferentes para a variável **[!UICONTROL Publicar Target]** atributo. Lembremos que você optou por publicar no [!DNL Experience Manager Assets] (`Destination: Publish`). Em seguida, por que ele está mostrando que apenas uma pasta e um ativo são publicados no `AEM`e os outros dois ativos são publicados para `AEM` e `Dynamic Media`?

Aqui, você deve entender a função das propriedades da pasta. Uma pasta **[!UICONTROL Modo de publicação do Dynamic Media]** A propriedade do tem um papel importante na publicação. Para exibir as propriedades de uma pasta, selecione uma pasta e clique em **[!UICONTROL Propriedades]** na barra de ferramentas. Para um ativo, consulte as propriedades da pasta pai.

A tabela a seguir explica como a publicação ocorre dependendo do **[!UICONTROL Destino]** e **[!UICONTROL Modo de publicação do Dynamic Media]**:

| [!UICONTROL Destino] | [!UICONTROL Modo de publicação do Dynamic Media] | [!UICONTROL Direcionamento da publicação] | Conteúdo permitido |
| --- | --- | --- | --- |
| Publicação | Publicação seletiva | `AEM` | Ativos e (ou) pastas |
| Publicação | Imediato | `AEM` e `Dynamic Media` | Ativos e (ou) pastas |
| Publicação | Por ativação | `AEM` e `Dynamic Media` | Ativos e (ou) pastas |
| Dynamic Media | Publicação seletiva | `Dynamic Media` | Ativos |
| Dynamic Media | Imediato | `None` | Não é possível publicar os ativos |
| Dynamic Media | Por ativação | `None` | Não é possível publicar os ativos |

>[!NOTE]
>
>Apenas os ativos são publicados em [!DNL Dynamic Media].
>
>Publicar uma pasta em [!DNL Dynamic Media] não é suportado.
>
>Se você selecionar uma pasta (`Selective Publish`) e escolha a variável [!DNL Dynamic Media] destino, o [!UICONTROL Publicar Target] O atributo reflete `None`.


Vamos agora alterar a **[!UICONTROL Destino]** no caso de uso acima referido para **[!UICONTROL Dynamic Media]** e verificar os resultados. Ao fazer isso, somente o ativo de `Selective Publish` a pasta é publicada em [!DNL Dynamic Media]. Os ativos do `Immediate` e `Upon Activation` as pastas não são publicadas e refletem `None`.

![Publicar no Dynamic Media](assets/manage-publication-dynamic-media.png)

>[!NOTE]
>
>If [!DNL Dynamic Media] não está configurado no [!DNL Experience Manager Assets] e a **[!UICONTROL Destino]** é **[!UICONTROL Publicar]**, os ativos e as pastas são sempre publicados em `AEM`.
>
>Publicar em [!DNL Brand Portal] O é independente das propriedades da pasta. Todos os ativos, pastas e coleções podem ser publicados na Brand Portal. Consulte [publicar ativos no Brand Portal](#publish-assets-to-brand-portal).

>[!NOTE]
>
>Se você personalizou a variável [!DNL Manage Publication] assistente, sua personalização continua a funcionar com as funcionalidades existentes.
>
>No entanto, é possível remover a personalização existente para usar o novo [!DNL Manager Publication] recursos.


## Publicar ativos mais tarde {#publish-assets-later}

Para agendar o fluxo de trabalho de publicação de ativos para uma data ou hora posterior:

1. No [!UICONTROL Experience Manager Assets] , navegue até a pasta principal e selecione todos os ativos ou pastas que deseja agendar para publicação.
1. Clique em **[!UICONTROL Gerenciar publicação]** na barra de ferramentas.
1. Clique em **[!UICONTROL Publicar]** from **[!UICONTROL Ação]** e selecione o **[!UICONTROL Destino]** onde deseja publicar o conteúdo.
1. Selecione **[!UICONTROL Mais tarde]** em **[!UICONTROL Agendamento]**.
1. Selecione um **[!UICONTROL Data de ativação]** e especifique a data e a hora. Clique em **[!UICONTROL Avançar]**.

   ![Gerenciar fluxo de trabalho de publicação](assets/manage-publication-workflow.png)

1. No **[!UICONTROL Escopo]** guia , **[!UICONTROL Adicionar conteúdo]** (se necessário). Clique em **[!UICONTROL Avançar]**.
1. No **[!UICONTROL Fluxos de trabalho]** , especifique um título de Fluxo de trabalho. Clique em **[!UICONTROL Publicar mais tarde]**.

   ![Título do fluxo de trabalho](assets/manage-publication-workflow-title.png)

   Faça logon na instância de destino para verificar os ativos publicados (dependendo da data ou hora programadas).

## Publicar ativos no Dynamic Media {#publish-assets-to-dynamic-media}

Apenas os ativos são publicados em [!DNL Dynamic Media]. No entanto, o comportamento de publicação é diferente com base nas propriedades da pasta. Uma pasta pode ter **[!UICONTROL Modo de publicação do Dynamic Media]** configurado para publicação seletiva, que pode ser qualquer um dos seguintes:

* `Selective Publish`
* `Immediate`
* `Upon Activation`

O processo de publicação para **[!UICONTROL Imediato]** e **[!UICONTROL Após ativação]** é consistente, no entanto, é diferente para **[!UICONTROL Publicação seletiva]**. Consulte [configurar a publicação seletiva no nível da pasta no Dynamic Media](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/selective-publishing.html). Depois de configurar a publicação seletiva em uma pasta, você pode executar qualquer um dos seguintes procedimentos:

* [Publicar ativos seletivamente no Dynamic Media ou no Experience Manager usando Gerenciar publicação](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/selective-publishing.html?lang=en#selective-publish-manage-publication)
* [Cancelar a publicação seletiva de ativos do Dynamic Media ou do Experience Manager usando Gerenciar publicação](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/selective-publishing.html?lang=en#selective-unpublish-manage-publication)
* [Publicar ativos no Dynamic Media ou Experience Manager usando a Publicação rápida](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/selective-publishing.html?lang=en#quick-publish-aem-dm)
* [Publicar ou cancelar a publicação seletiva de ativos por meio de resultados de pesquisa](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/selective-publishing.html?lang=en#selective-publish-unpublish-search-results)

## Publicar ativos no Brand Portal {#publish-assets-to-brand-portal}

Você pode publicar ativos, pastas e coleções no [!DNL Experience Manager Assets Brand Portal] instância.

* [Publicar ativos no Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/brand-portal/publish-to-brand-portal.html?lang=en#publish-assets-to-bp)
* [Publicar pastas no Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/brand-portal/publish-to-brand-portal.html?lang=en#publish-folders-to-brand-portal)
* [Publicar coleções no Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/brand-portal/publish-to-brand-portal.html?lang=en#publish-collections-to-brand-portal)

## Limitações e dicas {#limitations-and-tips}

* A opção para [!UICONTROL Gerenciar publicação] O está disponível somente para contas de usuário com permissões de replicação.
* Pastas vazias não são publicadas.
* Se você publicar um ativo que está sendo processado, somente o conteúdo original será publicado. As representações estão ausentes. Aguarde até que o processamento seja concluído e publique ou republique o ativo quando o processamento for concluído.
* Ao cancelar a publicação de um ativo complexo, cancele a publicação somente do ativo. Evite desfazer a publicação das referências, pois elas podem ser referenciadas por outros ativos publicados.
