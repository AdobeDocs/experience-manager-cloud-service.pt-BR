---
title: Notas de versão do Universal Editor 2024.08.13
description: Estas são as notas de versão do Universal Editor de 2024.08.13.
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: c66621eb336b8e6eb5ceb1056c089c190fcd1c34
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 0%

---


# Notas de versão do Universal Editor 2024.08.13 {#release-notes}

Estas são as notas de versão da versão de 13 de agosto de 2024 do Universal Editor.

>[!TIP]
>
>Para obter as notas de versão atuais do Adobe Experience Manager as a Cloud Service, consulte [esta página.](/help/release-notes/release-notes-cloud/release-notes-current.md)

## Novidades {#what-is-new}

* **Tipos de Dados Personalizados**: Personalize o editor de acordo com suas necessidades de dados exclusivas com a capacidade de [criar campos personalizados dentro do painel de propriedades.](https://developer.adobe.com/uix/docs/services/aem-universal-editor/api/item-types-renderers/)
   * Independentemente de você estar desenvolvendo um seletor de produto personalizado para casos de uso de comércio ou preenchendo uma lista suspensa com valores de seus back-end, esse recurso oferece o controle necessário sobre os dados que os autores usam para compor conteúdo.
* **Arrastar e soltar entre contêineres**: aproveite a maior flexibilidade na composição de layout com a capacidade de [mover componentes entre diferentes contêineres por meio do recurso de arrastar e soltar](/help/sites-cloud/authoring/universal-editor/authoring.md#reordering-components) no [painel Árvore de Conteúdo.](/help/sites-cloud/authoring/universal-editor/navigation.md#content-tree-mode)
* **Integração otimizada do GitHub**: o armazenamento em cache das respostas do GitHub foi introduzido, acelerando significativamente a recuperação de tags e o `universal-editor-cors-library`, resultando em uma experiência do usuário mais rápida e suave.
* **Validação configurável do token IMS**: para aumentar a flexibilidade no gerenciamento de token, a [validação do token IMS agora é opcional.](/help/implementing/universal-editor/local-dev.md#setting-up-service)
   * Essa opção de configuração permite desabilitar a validação conforme necessário, simplificando as configurações do gateway de nuvem.
* **Integração do Splunk**: o log do Splunk foi integrado ao [Serviço do Editor Universal para desenvolvimento local](/help/implementing/universal-editor/local-dev.md#setting-up-service), aprimorando o monitoramento e o diagnóstico.
   * Essa integração garante um rastreamento eficiente de registros, operações ininterruptas e solução de problemas mais rápida.

## Correções de erros {#bug-fixes}

* **Feedback de Publicação Aprimorado**: se a publicação falhar devido a permissões insuficientes, o feedback para o usuário durante a publicação foi aprimorado para exibir um aviso claro em vez de simplesmente indicar uma falha.
* **Tratamento de URLs aprimorado**: foram corrigidos problemas de codificação/decodificação de URLs incorretos que causavam falhas de publicação.
* **Tratamento preciso de dados**: um problema no qual os números flutuantes eram armazenados incorretamente como números inteiros foi resolvido, garantindo um tratamento preciso de dados em todo o seu conteúdo.
* **Segurança e Estabilidade**: as vulnerabilidades de segurança nas imagens do Docker foram corrigidas e a cobertura de testes para componentes críticos, como o Seletor de Componentes e Navegação Estrutural, foi implementada, resultando em uma experiência do editor mais segura, estável e confiável.
