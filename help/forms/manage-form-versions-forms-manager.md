---
title: Gerenciar versões de formulários no Forms Manager
description: Saiba como criar e gerenciar versões do Adaptive Forms, fragmentos de formulário, temas e outros ativos na interface do usuário do Forms Manager.
feature: Adaptive Forms, Core Components, Foundation Components
role: User, Developer, Admin
badgeSaas: label="AEM Forms" type="Positive" tooltip="Aplicável ao AEM Forms)."
exl-id: cd2c6e15-99a6-4b4e-bfd1-8291a2001ebe
source-git-commit: 89b0f2a8ca9d2f60365a5c3962b0b4e826f79b3e
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 3%

---

# Gerenciar versões do Formulário Assets na interface do usuário do Forms Manager

<span class="preview"> Esse recurso está disponível por meio do programa de acesso antecipado. Para solicitar acesso, envie um email de seu endereço oficial para [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com). </span>

O Forms Manager agora oferece suporte ao controle de versão para ativos de formulário. Você pode criar versões, visualizar o histórico de versões e restaurar versões anteriores dos seus ativos na interface do usuário do Forms Manager.

## Tipos de ativos compatíveis {#supported-asset-types}

Você pode criar e gerenciar versões dos seguintes tipos de ativos:

| Tipo de ativo | Descrição |
|---|---|
| Forms adaptável (componentes principais) | Forms adaptável criado usando os Componentes principais |
| Forms adaptável (componentes de base) | Forms adaptável criado usando componentes básicos |
| Fragmentos de formulários | Seções de formulário reutilizáveis compartilhadas em vários formulários |
| Temas | Definições de estilo visual aplicadas ao Adaptive Forms |
| Modelos XDP | Modelos de formulário baseados em XFA |
| Ativos binários | Outros arquivos armazenados no repositório DAM de formulários |

## Criar uma versão {#create-version-forms-manager}

Para criar uma versão de um ativo de formulário:

1. Navegue até **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms e Documentos]**.
1. Selecione o formulário ou ativo.
1. No painel esquerdo, selecione **[!UICONTROL Linha do tempo]**.
1. Clique em **[!UICONTROL Salvar como versão]** na barra de ferramentas da linha do tempo.
   ![Salvar como Versão](/help/forms/assets/create-version.png)
1. Insira um **[!UICONTROL Rótulo]** e um **[!UICONTROL Comentário]** opcional para descrever as alterações.
1. Clique em **[!UICONTROL Criar]**.
   ![Salvar como Versão2](/help/forms/assets/create-version1.png)

A versão é exibida no painel Linha do tempo com rótulo, comentário e carimbo de data e hora.

## Versão de um ativo durante o upload {#version-on-upload}

Ao carregar um ativo com o mesmo nome de um ativo existente, o Forms Manager exibe uma caixa de diálogo **Carregar arquivo** que lista os ativos a serem atualizados. A caixa de diálogo mostra o nome, a seção e o caminho do ativo.

Quando um ativo com o mesmo nome já existe, o upload substitui o ativo existente e cria uma nova versão automaticamente. Você pode visualizar a versão criada na linha do tempo.

![Caixa de diálogo Carregar Arquivo mostrando o carregamento com versão](/help/forms/assets/version-upload.png)

## Exibir histórico de versões {#view-version-history}

Para exibir o histórico de versões de um ativo:

1. Selecione o ativo no Forms Manager.
1. No painel esquerdo, selecione **[!UICONTROL Linha do tempo]**.
   ![Histórico de Versões](/help/forms/assets/version-history.png)

A linha do tempo exibe todas as entradas da versão junto com os eventos de atividade. Cada entrada mostra o rótulo, comentário, autor e carimbo de data e hora.

## Restaurar uma versão anterior {#restore-version}

Para restaurar um ativo para uma versão anterior:

1. Selecione o ativo no Forms Manager.
1. No painel esquerdo, selecione **[!UICONTROL Linha do tempo]**.
1. Selecione a versão que deseja restaurar.
1. Clique em **[!UICONTROL Reverter para esta versão]**.
   ![Reverter versão](/help/forms/assets/revert-version.png)

>[!NOTE]
>
>As imagens não podem ser revertidas para uma versão anterior. Todos os outros tipos de ativos, incluindo o Forms adaptável, fragmentos de formulário, temas e modelos XDP, oferecem suporte à restauração de versão.

## Consulte também {#see-also}

* [Controle de versão, revisão e comentário em um Formulário adaptável](/help/forms/add-comments-annotations-versioning-adaptive-form-core-components.md)
* [Importar e exportar formulários e ativos relacionados](/help/forms/import-export-forms-templates.md)
* [Publicar e desfazer a publicação de formulários](/help/forms/publishing-unpublishing-forms.md)
