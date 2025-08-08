---
title: Notas de versão do Universal Editor 2025.07.31
description: Estas são as notas de versão do Universal Editor 2025.07.31.
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: 91799e32f363aca268a89a7eebcb5001c5295cc5
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 0%

---


# Notas de versão do Universal Editor 2025.07.31 {#release-notes}

Estas são as notas de versão do Universal Editor de 31 de julho de 2025.

>[!TIP]
>
>Para obter as notas de versão atuais do Adobe Experience Manager as a Cloud Service, consulte [esta página](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Novidades {#what-is-new}

* [A opção de barra de ferramentas do cabeçalho de autenticação](/help/sites-cloud/authoring/universal-editor/navigation.md#autentication-settings) permanece atrás de um recurso de alternância, conforme introduzido na [versão 2025.07.09.](/help/release-notes/universal-editor/2025/2025-07-09.md)
   * No entanto, agora ela está ativada por padrão.
* Novos recursos para [participantes antecipados do RTE](#new-rte)
   * O suporte ao modo escuro foi adicionado.
   * O suporte para alinhamento de texto foi adicionado.
      * Desativado por padrão e disponível somente para projetos headless
   * Suporte a recuo foi adicionado.
      * Desativado por padrão e disponível somente para projetos headless
   * As quebras (`<br>`) agora são inseridas no shift+enter.

## Recursos da adoção antecipada {#early-adopter}

Se você estiver interessado em testar esses recursos futuros e compartilhar seu feedback, envie um email para o Gerente de sucesso do cliente da Adobe a partir do endereço de email associado à sua Adobe ID.

### Novo RTE {#new-rte}

O novo RTE do ProseMirror, com um seletor de páginas na caixa de diálogo de link, agora está disponível no painel direito.

### Desfazer/Refazer {#undo-redo}

Desfazer e refazer agora está disponível para autores de conteúdo do Universal Editor.

* Isso inclui edições feitas em contexto, edições feitas por meio do painel Propriedades, bem como adição (ou duplicação), movimentação e exclusão de blocos.
* Desfazer e refazer estão limitados à sessão atual do navegador.

## Outras melhorias {#other-improvements}

* Correções para o RTE do adotante inicial
   * Pressionar Enter agora cria um novo item de lista (`<li>`) quando estiver em uma lista.
* Os vídeos agora são atualizados corretamente ao usar o DAM remoto.
* Suporte de serviço adicionado para 6.5 LTS.

## Desaprovações {#deprecations}

* Os componentes `text-input` e `text-area` foram oficialmente descontinuados na [versão 2025.07.09.](/help/release-notes/universal-editor/2025/2025-07-09.md)
   * Em `model-definition.json`, use o componente de texto para criar entradas de texto para o painel Propriedades.
