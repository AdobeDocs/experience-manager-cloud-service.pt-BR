---
title: Notas de versão do Universal Editor 2025.07.09
description: Estas são as notas de versão do Universal Editor de 2025.07.09.
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: 199ee7e11f6706773bd426c3d27236d6ea791a6c
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 0%

---


# Notas de versão do Universal Editor 2025.07.09 {#release-notes}

Estas são as notas de versão da versão de 9 de julho de 2025 do Universal Editor.

>[!TIP]
>
>Para obter as notas de versão atuais do Adobe Experience Manager as a Cloud Service, consulte [esta página](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Novidades {#what-is-new}

* [Ao clicar no botão da barra de ferramentas **Adicionar** nos contêineres](/help/sites-cloud/authoring/universal-editor/authoring.md#adding-components), se apenas um tipo de componente for permitido, ele será inserido imediatamente, sem a necessidade de seleção no menu suspenso.
* [A opção de barra de ferramentas do cabeçalho de autenticação ](/help/sites-cloud/authoring/universal-editor/navigation.md#autentication-settings) foi colocada atrás de um botão de alternância de recurso, pois não é útil na maioria dos casos.
* [Como o aninhamento de contêineres não é permitido para vários campos no painel de propriedades](/help/implementing/universal-editor/field-types.md#fields), a rotina de renderização agora filtra os contêineres aninhados da lista de campos para evitar aninhamento inválido.

## Recursos da adoção antecipada {#early-adopter}

Se você estiver interessado em testar esses recursos futuros e compartilhar seu feedback, envie um email para o Gerente de sucesso do cliente da Adobe a partir do endereço de email associado à sua Adobe ID.

### Novo RTE {#new-rte}

O novo RTE do ProseMirror, com um seletor de páginas na caixa de diálogo de link, agora está disponível no painel direito.

### Desfazer/Refazer {#undo-redo}

Desfazer e refazer agora está disponível para autores de conteúdo do Universal Editor.

* Isso inclui edições feitas em contexto, edições feitas por meio do painel Propriedades, bem como adição (ou duplicação), movimentação e exclusão de blocos.
* Desfazer e refazer estão limitados à sessão atual do navegador.

## Outras melhorias {#other-improvements}

* Foi corrigido um problema em que não era possível remover uma única referência de ativo ao editar por meio do painel de propriedades.
* Correção de um problema em que o painel Propriedades era carregado indefinidamente porque as referências de ativos eram convertidas automaticamente em matrizes, causando um estado de carregamento infinito.
   * Os valores de referência dos ativos agora são armazenados como estão, sem conversão automática em arrays.
* Correção de um problema em que o painel Propriedades não exibia campos quando um modelo era definido, mas não continha conteúdo.
   * Isso causava um estado de carregamento infinito para o painel Propriedades, para respostas vazias de detalhes, como Fragmentos de conteúdo vazios.
* A configuração ESLint foi refatorada para compatibilidade com a versão 9, incluindo regras atualizadas e suporte a plug-in.

## Desaprovações {#deprecations}

* O componente `text-input` agora está oficialmente obsoleto.
   * Em `model-definition.json`, use o componente de texto para criar entradas de texto para o painel Propriedades.
