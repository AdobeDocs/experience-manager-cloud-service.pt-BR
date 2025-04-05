---
title: Notas de versão do Universal Editor 2025.03.10
description: Estas são as notas de versão do Universal Editor 2025.03.10.
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: beab4f94dc6d78c2b1ad87a02b9fe46dd0438bcc
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 0%

---


# Notas de versão do Universal Editor 2025.03.10 {#release-notes}

Estas são as notas de versão da versão de 10 de março de 2025 do Editor universal.

>[!TIP]
>
>Para obter as notas de versão atuais do Adobe Experience Manager as a Cloud Service, consulte [esta página](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Novidades {#what-is-new}

* **Movendo Componentes:** [Movendo componentes entre contêineres](/help/sites-cloud/authoring/universal-editor/authoring.md#reordering-components) agora observa o filtro de componente do contêiner de destino.
   * Não há mais um requisito para ter a mesma [definição de filtro](/help/implementing/universal-editor/filtering.md) em vigor para os contêineres de destino e de destino para mover o componente entre os contêineres.
* **Páginas Bloqueadas:** O Universal Editor Service observa o [status de bloqueio de uma página](/help/sites-cloud/authoring/sites-console/managing-pages.md#locking-a-page) e grava somente em páginas que não estão bloqueadas ou estão bloqueadas pelo usuário.

## Novas extensões para o editor universal {#extensions}

Várias novas extensões foram lançadas no [Extension Manager](https://developer.adobe.com/uix/docs/extension-manager/) para o Universal Editor, aprimorando a experiência de criação.

* **Extensão do MSM**: agora é possível interromper e reinstanciar a herança de componentes/blocos usando essa extensão.
* **Extensão de Propriedades da Página**: acesse a janela de propriedades da página diretamente do Editor Universal usando esta extensão.
* **Extensão do Fluxo de Trabalho**: use fluxos de trabalho em páginas e Fragmentos de Conteúdo que são instrumentados na página que usa esta extensão.
* **Extensão de Bloqueio de Página**: use esta extensão para bloquear e desbloquear uma página diretamente do Editor Universal.

## Outras melhorias {#other-improvements}

* Foram feitas correções para corrigir a validação para a tela headless.

## Substituição {#deprecation}

* A biblioteca `universal-editor-cors` fornecida via npm ou `https://unviersal-editor-service.experiencecloud.live/corslib/*` não deve mais ser usada.
   * Em vez disso, uma marca de script apontando para `https://universal-editor-service.adobe.io/cors.js` deve ser usada.
   * Consulte a [Visão geral do editor universal para desenvolvedores do AEM](/help/implementing/universal-editor/developer-overview.md) para obter detalhes sobre como instrumentar corretamente sua página para uso com o editor universal.
   * Os usuários verão uma mensagem de desativação uma vez por dia se o método errado for usado.
