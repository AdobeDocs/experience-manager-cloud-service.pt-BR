---
title: 'Solucionar problemas do AEM durante a criação  '
description: Alguns problemas que podem ocorrer quando você usa o AEM
exl-id: b9c0584d-255e-486d-b829-09e07499ecd2
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: ht
source-wordcount: '235'
ht-degree: 100%

---

# Solucionar problemas do AEM durante a criação   {#troubleshooting-aem-when-authoring}

A seção a seguir aborda alguns problemas que você poderá enfrentar ao usar o AEM, junto com sugestões sobre como resolvê-los.

## A versão antiga da página ainda está no site publicado {#old-page-version-still-on-published-site}

* **Problema**:
   * Você fez alterações em uma página e a publicou no site de publicação, mas a versão *antiga* da página está sendo mostrada no site de publicação.
* **Motivo**:
   * Isso pode ter várias causas, a mais frequente é o cache (o navegador local ou o Dispatcher), embora, às vezes, possa haver um problema com a fila de replicação.
* **Soluções**:
   * Há várias possibilidades aqui:
   * Confirmar se a página foi replicada corretamente. Verificar o status da página e, se necessário, o estado da fila de replicação.
   * Limpar o cache no seu navegador local e acessar a página novamente.
   * Adicionar `?` ao final do URL da página. Por exemplo:
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
