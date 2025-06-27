---
title: Notas de versão do Universal Editor 2025.06.19
description: Estas são as notas de versão do Universal Editor de 2025.06.19.
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: 5ffae9e548ca952975b3ea805808e227102ec99f
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 0%

---


# Notas de versão do Universal Editor 2025.06.19 {#release-notes}

Estas são as notas de versão do editor universal de 19 de junho de 2025.

>[!TIP]
>
>Para obter as notas de versão atuais do Adobe Experience Manager as a Cloud Service, consulte [esta página](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Novidades {#what-is-new}

* **Suporte para vários campos no Painel de Propriedades** -
  [O componente de contêiner](/help/implementing/universal-editor/field-types.md#container) agora pode ser usado para criar propriedades de vários campos.
* **Suporte para propriedades aninhadas** - O campo [`name`](/help/implementing/universal-editor/field-types.md#nesting) agora oferece suporte a caminhos para habilitar o aninhamento de propriedades.
* **Painel direito redimensionável** - O painel lateral agora pode ser redimensionado para ter uma melhor conta para conteúdo mais longo exibido no painel lateral.

## Recursos da adoção antecipada {#early-adopter}

Para testar alguns recursos futuros, faça parte do programa de adoção antecipada da Adobe.

### **Desfazer/Refazer** {#undo-redo}

Desfazer e refazer agora está disponível para autores de conteúdo do Universal Editor.

* Isso inclui edições feitas em contexto, edições feitas por meio do painel Propriedades, bem como adição (ou duplicação), movimentação e exclusão de blocos.
* Desfazer e refazer estão limitados à sessão atual do navegador.

Se você estiver interessado em testar esse novo recurso e compartilhar seu feedback, envie um email para o Gerente de sucesso do cliente da Adobe a partir do endereço de email associado à sua Adobe ID.

## Outras melhorias {#other-improvements}

* Foram corrigidos erros de colisão de chave de recurso ao mover blocos entre contêineres.
* Correção de um problema que causava a falha da duplicação do último bloco de um container.
* O menu suspenso Adicionar ação agora lista apenas componentes que têm um plug-in adequado definido no arquivo `component-definition.json`.
* A data de modificação usada pela caixa de diálogo de publicação foi corrigida, onde, em algumas circunstâncias, as páginas não eram reconhecidas como modificadas e não eram republicadas.
* Correção do comportamento de herança do MSM em que a edição de um contêiner cancelava a herança de nós filhos.
* `fetchUrl` foi corrigido, restaurando blocos de movimentação de um contêiner para outro.
