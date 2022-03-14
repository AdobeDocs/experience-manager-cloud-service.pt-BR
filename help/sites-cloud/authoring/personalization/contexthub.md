---
title: Visualização de páginas usando dados do ContextHub
description: A barra de ferramentas do ContextHub exibe os dados dos armazenamentos do ContextHub, permite alterar esses dados e é útil para visualizar o conteúdo
exl-id: 9c0536c5-900e-4814-9e31-f9fee5adc17c
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 89%

---

# Visualização de páginas usando dados do ContextHub  {#previewing-pages-using-contexthub-data}

A barra de ferramentas do ContextHub exibe os dados dos armazenamentos do ContextHub e permite alterar esses dados. A barra de ferramentas ContextHub é útil para visualizar o conteúdo que é determinado pelos dados em um armazenamento ContextHub.

A barra de ferramentas consiste em uma série de modos de interface que contêm um ou mais módulos de interface.

* Os modos de interface do usuário são ícones que aparecem no lado esquerdo da barra de ferramentas. Quando você clica ou toca em um ícone, a barra de ferramentas revela os módulos de interface do usuário que ele contém.
* Módulos de interface do usuário exibem dados de um ou mais armazenamentos do ContextHub. Alguns módulos de interface do usuário também permitem manipular os dados do armazenamento.

O ContextHub instala vários modos e módulos de interface do usuário. Seu administrador pode ter [configurado o ContextHub](/help/implementing/developing/personalization/configuring-contexthub.md) para exibir opções diferentes.

## Revelar a barra de ferramentas do ContextHub {#revealing-the-contexthub-toolbar}

A barra de ferramentas do ContextHub está disponível no modo de Visualização. A barra de ferramentas está disponível somente nas instâncias do autor e somente se o administrador a tiver ativado.

![A barra de ferramentas do ContextHub](/help/sites-cloud/authoring/assets/contexthub-toolbar.png)

1. Com a página aberta para edição, clique ou toque em Visualizar na barra de ferramentas.

   ![O botão Visualizar](/help/sites-cloud/authoring/assets/contexthub-preview-button.png)

1. Para exibir a barra de ferramentas, clique ou toque no ícone ContextHub.

   ![O botão ContextHub](/help/sites-cloud/authoring/assets/contexthub-button.png)

## Recursos do módulo da interface {#ui-module-features}

Cada módulo de interface fornece um conjunto diferente de recursos, mas os tipos de recursos a seguir são os mais comuns. Como os módulos de interface podem ser estendidos, o desenvolvedor pode implementar outros recursos, conforme necessário.

### Conteúdo da barra de ferramentas {#toolbar-content}

Os módulos de interface podem exibir dados de um ou mais armazenamentos do ContextHub na barra de ferramentas. Os módulos de interface usam um ícone e um título para se identificarem.

![Personas do ContextHub](/help/sites-cloud/authoring/assets/contexthub-persona-button.png)

### Conteúdo pop-up {#popup-content}

Alguns módulos de interface exibem uma sobreposição de pop-up quando clicados ou tocados. Normalmente, o pop-up contém mais informações do que o que aparece na barra de ferramentas.

![Informações de perfil do ContextHub](/help/sites-cloud/authoring/assets/contexthub-profile.png)

### Formulários pop-up {#popup-forms}

A sobreposição de pop-up de um módulo pode incluir elementos de formulário que permitem alterar os dados no armazenamento do ContextHub. Se o conteúdo da página for determinado pelos dados do armazenamento, será possível usar o formulário e observar as alterações no conteúdo da página.

### Modo de tela cheia {#fullscreen-mode}

As sobreposições de pop-up podem incluir um ícone que você clica ou toca para expandir o conteúdo do pop-up a toda a janela do navegador ou a tela.

![Botão de tela cheia](/help/sites-cloud/authoring/assets/contexthub-fullscreen.png)
