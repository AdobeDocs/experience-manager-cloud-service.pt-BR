---
title: Aplicar cortes inteligentes de vídeo a vídeos aprovados
description: O Dynamic Media com recursos de OpenAPI permite gerar automaticamente saídas de corte inteligente de vídeo para ativos de vídeo aprovados no Adobe Experience Manager (AEM).
role: Admin, User
badgeSaas: label="AEM Assets" type="Positive" tooltip="Aplicável ao AEM Assets)."
exl-id: video-smartcrop-dmwoapi
source-git-commit: c2b849ef25afd0809891a822a99ddd3059bf1919
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 2%

---


# Aplicar cortes inteligentes de vídeo a vídeos aprovados {#apply-video-smart-crops-dmwoapi}

O [!DNL Dynamic Media with OpenAPI capabilities] permite gerar automaticamente saídas de corte inteligente de vídeo para ativos de vídeo no [!DNL Adobe Experience Manager (AEM)]. Os cortes inteligentes de vídeo analisam o conteúdo do vídeo e ajustam dinamicamente o enquadramento para manter o assunto principal em foco em diferentes proporções de aspecto e dispositivos.

Os cortes inteligentes de vídeo são gerados automaticamente quando o recurso é ativado e o ativo de vídeo é aprovado

## Antes de começar {#prerequisites-for-video-smart-crops}

Verifique se você tem:

* Acesso a [!DNL AEM Assets as a Cloud Service].
* Permissão para editar esquemas de metadados.
* Dynamic Media com recursos OpenAPI habilitados para o seu ambiente.
* Ativos de vídeo que podem ser marcados como **[!UICONTROL Aprovados]**.

## Ativar cortes inteligentes de vídeo para vídeos {#enable-video-smart-crops}

Para ativar os Recortes inteligentes de vídeo, configure o esquema de metadados usado para ativos de vídeo:

1. Navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Assets]** > **[!UICONTROL Esquemas de Metadados]**.
2. Abra o esquema de metadados aplicável (por exemplo, **padrão**).
3. Selecione o formulário **Vídeo** e clique em **[!UICONTROL Editar]**.
4. Adicione um novo **[!UICONTROL Campo suspenso]** e configure o seguinte:

   * **Rótulo do Campo**: Criar Recortes Inteligentes de Vídeo
   * **Mapear para a propriedade**: `./jcr:content/dam:applyVideoSmartCrop`

5. Adicione os seguintes valores manualmente:

   * Sim → verdadeiro
   * Não → falso

6. Salve o esquema.

A opção **Criar cortes inteligentes de vídeo** agora está disponível no formulário de metadados de ativos de vídeo.

<!--
broken link
![Create Video Smartcrops field](/help/assets/assets/video-smartcrop-metadata-field.png)
-->

## Aplicar cortes inteligentes de vídeo a vídeos aprovados {#apply-video-smart-crops}

Aplique os cortes inteligentes de vídeo aos ativos de vídeo ativando o campo de metadados e aprovando o ativo.

Execute as seguintes etapas:

1. Em [!DNL Assets View], selecione **[!UICONTROL Assets]** e navegue até a pasta.
2. Selecione o ativo de vídeo.
3. Clique em **[!UICONTROL Detalhes]**.
4. No painel de metadados, localize **[!UICONTROL Criar Recortes Inteligentes de Vídeo]**.
5. Defina o valor como **Sim** e clique em **[!UICONTROL Salvar]**.
6. Defina o status do ativo como **[!UICONTROL Aprovado]**.

Depois que o ativo é aprovado, as saídas de corte inteligente de vídeo são geradas automaticamente.

## Exibir saídas de vídeo cortadas de forma inteligente {#view-video-smart-crops}

Depois que os cortes inteligentes de vídeo são gerados:

* As saídas estão disponíveis durante a reprodução do vídeo.
* O visualizador do Dynamic Media seleciona automaticamente o recorte mais apropriado com base no dispositivo e na taxa de proporção.
* A reprodução do vídeo se ajusta dinamicamente para manter o assunto principal em foco.

## Usar vídeos recortados de vídeo inteligente {#use-video-smart-crops}

Você pode usar as saídas de corte inteligente de vídeo onde quer que o ativo de vídeo seja entregue, como:

* Páginas da Web
* Aplicativos
* Players de vídeo incorporados

O visualizador aplica automaticamente o recorte inteligente apropriado durante a reprodução.

>[!NOTE]
>
>* Os cortes inteligentes de vídeo são gerados apenas para ativos de vídeo **Aprovados**.
>* Verifique se o campo **Criar Smartcrop de vídeo** está definido como **Sim** antes de aprovar o ativo.
>* Os cortes inteligentes de vídeo não modificam o ativo original. O recorte é aplicado dinamicamente durante a reprodução.