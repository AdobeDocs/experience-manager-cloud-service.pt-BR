---
title: Notas da versão para [!DNL Workfront for Experience Manager enhanced connector]
description: Notas da versão para [!DNL Workfront for Experience Manager enhanced connector]
exl-id: 12de589d-fe5d-4bd6-b96b-48ec8f1ebcb6
source-git-commit: 081f7ed8c39382408285887928163e2569c5cbfe
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 4%

---

# Notas da versão para [!DNL Workfront for Experience Manager enhanced connector] {#release-notes-enhanced-connector-workfront}

A seção a seguir descreve as Notas de versão gerais de [!DNL Workfront for Experience Manager enhanced connector].

## Data de lançamento {#release-date}

A data de lançamento da versão mais recente 1.9.0 do [!DNL Workfront for Experience Manager enhanced connector] é 16 de junho de 2022.

## Destaques da versão {#release-highlights}

A versão mais recente do [!DNL Workfront for Experience Manager enhanced connector] O inclui a seguinte correção de erro:

* Ao fazer upload por meio de uma pasta vinculada ou usar o `Send To` ação disponível no Workfront para fazer upload de ativos no Experience Manager as a Cloud Service, os ativos são corrompidos e não podem ser abertos no Adobe Photoshop.

>[!IMPORTANT]
>
>O Adobe recomenda [atualizar para a versão 1.9.0 mais recente](../assets/update-workfront-enhanced-connector.md) do [!DNL Workfront for Experience Manager enhanced connector].

## Problemas conhecidos {#known-issues}

* Ao configurar pastas vinculadas ao projeto com o AEM 6.4, o Experience Manager não salva os valores para **[!UICONTROL subpastas]** e **[!UICONTROL Criar pasta vinculada em projetos com portfólio]** campos. O valor da variável **[!UICONTROL subpastas]** atualizações de campo para **[!UICONTROL indefinido]** e o valor da variável **[!UICONTROL Criar pasta vinculada em projetos com portfólio]** atualizações de campo para **[!UICONTROL Portfolio padrão]** automaticamente após salvar a configuração.

* Quando estiver usando a experiência clássica do Workfront, a variável **[!UICONTROL Enviar para]** disponível na **[!UICONTROL Mais]** a lista suspensa não permite selecionar o destino desejado no Experience Manager. O **[!UICONTROL Enviar para]** A opção funciona corretamente usando o **[!UICONTROL Ações do documento]** lista suspensa. O **[!UICONTROL Enviar para]** A opção funciona corretamente para **[!UICONTROL Mais]** lista suspensa, bem como a **[!UICONTROL Ações do documento]** lista suspensa disponível na nova experiência do Workfront.

## Versões anteriores {#previous-releases}

### Versão de março de 2022 {#march-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] O agora inclui as seguintes atualizações:

* Agora é possível criar pastas vinculadas entre o Adobe Workfront e o AEM Assets as a Cloud Service, mesmo se houver várias configurações de pastas vinculadas ao projeto.

* Adição de suporte para paginação de assinatura de evento.

* Adição de suporte para AEM 6.4.x.

* Adição de suporte para ambientes proxy.

* Várias correções de erros com base no feedback de parceiros e clientes.

>[!MORELIKETHIS]
>
>* [Integrar [!DNL Workfront for Experience Manager enhanced connector] com o Experience Manager 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/integrations/workfront-integrations.html?lang=en)
>* [Integrar [!DNL Workfront for Experience Manager enhanced connector] com o Experience Manager 6.4](https://experienceleague.adobe.com/docs/experience-manager-64/assets/integrations/workfront-integrations.html?lang=en)

