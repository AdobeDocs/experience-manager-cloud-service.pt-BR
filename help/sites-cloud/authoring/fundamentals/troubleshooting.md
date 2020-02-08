---
title: Solucionar problemas do AEM durante a criação
description: Alguns problemas que podem ocorrer quando você usa o AEM
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8

---


# Solucionar problemas do AEM durante a criação {#troubleshooting-aem-when-authoring}

A seção a seguir aborda alguns problemas que você poderá enfrentar ao usar o AEM, junto com sugestões sobre como resolvê-los.

## A versão antiga da página ainda está no site publicado {#old-page-version-still-on-published-site}

* **Problema**:
   * You have made changes to a page and published the page to the publish site, but the *old* version of the page is still being shown on the publish site.
* **Motivo**:
   * Isso pode ter várias causas, a mais frequente é o cache (o navegador local ou o Dispatcher), embora, às vezes, possa haver um problema com a fila de replicação.
* **Soluções**:
   * Há várias possibilidades aqui:
   * Confirmar se a página foi replicada corretamente. Verificar o status da página e, se necessário, o estado da fila de replicação.
   * Limpar o cache no seu navegador local e acessar a página novamente.
   * Add `?` to the end of the page URL. For example:
      * `http://<host>:<port>/sites.html/content?`
      * Isso solicitará a página diretamente do AEM e ignorará o Dispatcher. Se você receber a página atualizada, isso será uma indicação de que é necessário limpar o cache do Dispatcher.
   * Entre em contato com o administrador do sistema se houver problemas com as filas de replicação.

## Ações de componentes não visíveis na barra de ferramentas {#component-actions-not-visible-on-toolbar}

* **Problema**:
   * A ampla variedade de ações aplicáveis do componente não é visível ao editar uma página de conteúdo no ambiente do autor. 
* **Motivo**:
   * Em casos raros, uma ação anterior pode afetar a barra de ferramentas.
* **Solução**:
   * Atualize a página.
