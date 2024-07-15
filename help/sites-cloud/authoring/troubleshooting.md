---
title: Solucionar problemas do AEM durante a criação
description: Alguns problemas que você pode encontrar ao usar o AEM
exl-id: b9c0584d-255e-486d-b829-09e07499ecd2
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 66%

---

# Solucionar problemas do AEM durante a criação   {#troubleshooting-aem-when-authoring}

A seção a seguir aborda alguns problemas que você poderá enfrentar ao usar o AEM, junto com sugestões sobre como resolvê-los.

## A versão antiga da página ainda está no site publicado {#old-page-version-still-on-published-site}

* **Problema**:
   * Você fez alterações em uma página e a publicou no site de publicação, mas a versão *antiga* da página está sendo mostrada no site de publicação.
* **Motivo**:
   * Isso pode ter várias causas, mais frequentemente o cache (o navegador local ou o Dispatcher), embora possa, às vezes, ser um problema com a fila de replicação.
* **Soluções**:
   * Há várias possibilidades aqui:
   * Confirme se a página foi replicada corretamente. Verifique o status da página e, se necessário, o estado da fila de replicação.
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
