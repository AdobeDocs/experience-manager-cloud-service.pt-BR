---
title: Visualização de páginas usando dados do ContextHub
description: A barra de ferramentas do ContextHub exibe os dados dos armazenamentos do ContextHub, permite alterar esses dados e é útil para visualizar o conteúdo
exl-id: 9c0536c5-900e-4814-9e31-f9fee5adc17c
source-git-commit: 6bb7b2d056d501d83cf227adb239f7f40f87d0ce
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 25%

---

# Visualização de páginas usando dados do ContextHub  {#previewing-pages-using-contexthub-data}

A barra de ferramentas do ContextHub exibe os dados dos armazenamentos do ContextHub e permite alterar esses dados. A barra de ferramentas do ContextHub é útil para visualizar o conteúdo determinado pelos dados em um armazenamento do ContextHub.

A barra de ferramentas consiste em uma série de modos de interface que contêm um ou mais módulos de interface.

* Os modos da interface são ícones exibidos no lado esquerdo da barra de ferramentas. Ao selecionar um ícone, a barra de ferramentas revela os módulos de interface do usuário que ele contém.
* Os módulos de interface exibem dados de um ou mais armazenamentos do ContextHub. Alguns módulos de interface também permitem manipular dados de armazenamento.

O ContextHub instala vários modos de interface e módulos de interface do usuário. Seu administrador pode ter [ContextHub configurado](/help/implementing/developing/personalization/configuring-contexthub.md) para exibir diferentes.

## Revelação da barra de ferramentas do ContextHub {#revealing-the-contexthub-toolbar}

A barra de ferramentas do ContextHub está disponível no modo Visualização. A barra de ferramentas está disponível somente nas instâncias do autor e somente se o administrador a tiver ativado.

![A barra de ferramentas do ContextHub](/help/sites-cloud/authoring/assets/contexthub-toolbar.png)

1. Com a página aberta para edição, selecione Visualizar na barra de ferramentas.

   ![O botão Visualizar](/help/sites-cloud/authoring/assets/contexthub-preview-button.png)

1. Para exibir a barra de ferramentas, selecione o ícone do ContextHub.

   ![O botão ContextHub](/help/sites-cloud/authoring/assets/contexthub-button.png)

## Recursos do módulo de UI {#ui-module-features}

Cada módulo de interface do usuário fornece um conjunto diferente de recursos, mas os seguintes tipos de recursos são comuns. Como os módulos de interface do usuário são extensíveis, o desenvolvedor pode implementar outros recursos conforme necessário.

### Conteúdo da barra de ferramentas {#toolbar-content}

Os módulos de interface podem exibir dados de um ou mais armazenamentos do ContextHub na barra de ferramentas. Os módulos de interface usam um ícone e um título para se identificarem.

![Personas do ContextHub](/help/sites-cloud/authoring/assets/contexthub-persona-button.png)

### Conteúdo pop-up {#popup-content}

Alguns módulos de interface exibem uma sobreposição de pop-up quando clicados ou tocados. Normalmente, o pop-up contém mais informações do que o que aparece na barra de ferramentas.

![Informações de perfil do ContextHub](/help/sites-cloud/authoring/assets/contexthub-profile.png)

### Forms pop-up {#popup-forms}

A sobreposição pop-up de um módulo pode incluir elementos de formulário que permitem alterar os dados no armazenamento do ContextHub. Se o conteúdo da página for determinado pelos dados de armazenamento, é possível usar o formulário e observar as alterações no conteúdo da página.

### Modo de tela inteira {#fullscreen-mode}

As sobreposições de pop-up podem incluir um ícone selecionado para expandir o conteúdo pop-up de forma a abranger toda a janela ou tela do navegador.

![Botão de tela cheia](/help/sites-cloud/authoring/assets/contexthub-fullscreen.png)
