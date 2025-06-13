---
title: Reprocessamento de ativos digitais
description: Saiba mais sobre os vários métodos de reprocessamento de ativos digitais
contentOwner: KK
exl-id: 4759fa8c-10c7-4446-a135-3104b9beaee8
feature: Asset Processing
role: User, Leader, Developer
source-git-commit: fecbebde808c545a84889da5610a79c088f2f459
workflow-type: tm+mt
source-wordcount: '722'
ht-degree: 3%

---

# Reprocessamento de ativos digitais {#reprocessing-digital-assets}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Novo</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime e Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Novo</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nova</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>integração do AEM Assets com o Edge Delivery Services</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Novo</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>Extensibilidade da Interface do Usuário</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Novo</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>Habilitar o Dynamic Media Prime e o Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>Práticas recomendadas de pesquisa</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>Práticas recomendadas para metadados</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Centro de conteúdo</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>Dynamic Media com recursos da OpenAPI</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>Documentação do AEM Assets para desenvolvedores</b></a>
        </td>
    </tr>
</table>

É possível reprocessar ativos em uma pasta que já tenha um perfil de metadados existente que você alterou posteriormente. Se quiser que a predefinição recém-editada seja reaplicada aos ativos existentes na pasta, reprocesse a pasta. Você pode reprocessar quantos ativos forem necessários.

Reprocessamento de ativos em uma pasta se você encontrar um dos dois cenários a seguir:

* Você deseja executar uma predefinição de conjunto de lotes em uma pasta de ativos existente que já tenha ativos carregados nela.
* Posteriormente, você pode editar uma predefinição de conjunto de lotes existente que foi aplicada anteriormente a uma pasta de ativos.

## Reprocessar ativos {#reprocessing-steps}

Para reprocessar ativos em uma pasta:

1. Em [!DNL Experience Manager], na página do Assets, selecione os ativos recém-adicionados ou os ativos que deseja reprocessar.
Caso selecione uma pasta:

   * O fluxo de trabalho considera todos os arquivos na pasta selecionada de forma recursiva.
   * Se houver uma ou mais subpastas com ativos na pasta principal selecionada, o fluxo de trabalho reprocessará cada ativo na hierarquia de pastas.
   * Como prática recomendada, evite executar esse fluxo de trabalho em uma hierarquia de pastas com mais de 1000 ativos.

1. Selecione **[!UICONTROL Reprocessar Assets]**. Escolha entre as duas opções:

   ![Reprocessando Opções do Assets](assets/reprocessing-assets-options.png)

   * **[!UICONTROL Processo Completo]:** selecione essa opção quando desejar executar o processo geral, incluindo o perfil padrão, o perfil personalizado, o processamento dinâmico (se configurado) e os fluxos de trabalho de pós-processamento.
   * **[!UICONTROL Avançado]:** selecione esta opção para escolher o reprocessamento avançado.

     ![Opções Avançadas de Reprocessamento do Assets](assets/reprocessing-assets-options-advanced.png)

     Selecione entre as seguintes opções avançadas:

      * **[!UICONTROL Representações de Visualização Padrão]:** escolha esta opção quando quiser reprocessar as representações visualizadas por padrão.

      * **[!UICONTROL Metadados]:** escolha essa opção quando quiser extrair informações de metadados e marcas inteligentes para os ativos selecionados.

      * **[!UICONTROL Processando Perfis]:** Escolha esta opção quando quiser reprocessar um perfil selecionado. Você pode escolher a opção **[!UICONTROL Processo completo]** para incluir o processamento padrão e o perfil personalizado atribuído no nível da pasta.
        <!--When assets are uploaded to a folder, [!DNL Experience Manager] checks the containing folder's properties for a processing profile. If none is applied, a parent folder in the hierarchy is checked for a processing profile to apply.-->

      * **[!UICONTROL Fluxo de Trabalho de Pós-processamento]:** Escolha esta opção quando for necessário um processamento adicional de ativos que não possa ser obtido usando os perfis de processamento. Workflows de pós-processamento adicionais podem ser adicionados à configuração. O pós-processamento permite adicionar processamento totalmente personalizado além do processamento configurável usando microsserviços de ativos.

Consulte [usar microsserviços de ativos e perfis de processamento](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/asset-microservices-configure-and-use.html?lang=pt-BR) para saber mais sobre perfis de processamento e fluxo de trabalho de pós-processamento.

![Opções Avançadas de Reprocessamento do Assets2](assets/reprocessing-assets-options-advanced-2.png)

Depois de selecionar as opções apropriadas, clique em **[!UICONTROL Reprocessar]**. A mensagem de sucesso é exibida.

## Cenários para reprocessar ativos digitais {#scenarios-reprocessing}

[!DNL Experience Manager] permite o reprocessamento de ativos digitais para os seguintes componentes.

### Tags inteligentes {#reprocessing-smart-tags}

As organizações que lidam com ativos digitais usam cada vez mais vocabulário controlado por taxonomia em metadados de ativos. Basicamente, ele inclui uma lista de palavras-chave que funcionários, parceiros e clientes normalmente usam para consultar e pesquisar ativos digitais de uma classe específica. Marcar ativos com um vocabulário controlado por taxonomia garante que eles sejam facilmente identificados e recuperados.

Em comparação aos vocabulários de linguagem natural, marcar ativos digitais com base na taxonomia de negócios ajuda a alinhá-los aos negócios de uma empresa e garante que os ativos mais relevantes apareçam nas pesquisas.

Leia mais sobre [Reprocessar marcas de cores de imagens existentes no DAM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/color-tag-images.html?lang=pt-BR#color-tags-existing-images).

### Corte inteligente {#reprocessing-smart-crop}

Leia mais sobre o [Corte inteligente do Dynamic Media](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/image-profiles.html?lang=pt-BR), que permite aplicar cortes específicos (**[!UICONTROL Corte inteligente]** e corte de pixels) e configuração de nitidez aos ativos carregados.

### Metadados {#reprocessing-metadata}

[!DNL Adobe Experience Manager Assets] mantém metadados para cada ativo. Ele facilita a categorização e a organização de ativos e ajuda as pessoas que estão procurando um ativo específico. Com a capacidade de extrair metadados de arquivos carregados no Experience Manager Assets, o gerenciamento de metadados se integra ao fluxo de trabalho criativo. Com a capacidade de manter e gerenciar metadados com seus ativos, você pode organizar e processar ativos automaticamente com base nos metadados.

Leia mais sobre [Reprocessando perfis de metadados](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/metadata-profiles.html?lang=pt-BR).

### Reprocessamento de ativos do Dynamic Media em uma pasta {#reprocessing-dynamic-media}

Você pode reprocessar ativos em uma pasta que já tenha um Perfil de imagem do Dynamic Media ou um Perfil de vídeo do Dynamic Media que você alterou posteriormente. Para obter mais informações, visite [reprocessar ativos do Dynamic Media em uma pasta](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/about-image-video-profiles.html?lang=pt-BR).

>[!NOTE]
>
>Você precisa configurar o [!DNL Dynamic Media] no ambiente para habilitar a caixa de diálogo Dynamic Media.
>

### Fluxos de trabalhos

Leia mais sobre [perfis de processamento e fluxos de trabalho de pós-processamento](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/asset-microservices-configure-and-use.html?lang=pt-BR).
