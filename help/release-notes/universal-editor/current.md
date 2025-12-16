---
title: Notas de versão do Universal Editor 2025.12.12
description: Estas são as notas de versão do Universal Editor 2025.12.11.
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: b7b89587a81d0cadc81d4b2a486c022557c4a9fb
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 0%

---


# Notas de versão do Universal Editor 2025.12.12 {#release-notes}

Estas são as notas de versão da versão de 12 de dezembro de 2025 do Universal Editor.

>[!TIP]
>
>Se você deseja testar os recursos do Universal Editor **futuros** antes de eles serem lançados, consulte as [Notas de Versão de Visualização do Universal Editor.](/help/release-notes/universal-editor/preview.md)

>[!TIP]
>
>Para obter as notas de versão atuais do Adobe Experience Manager as a Cloud Service, consulte [esta página](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Novidades {#what-is-new}

* O suporte foi adicionado às tabelas existentes no [editor de rich text.](/help/sites-cloud/authoring/universal-editor/authoring.md#formatting-options)
* A chave da guia foi habilitada para aninhar listas no [editor de rich text.](/help/sites-cloud/authoring/universal-editor/authoring.md#formatting-options)
* O recurso de logon de desenvolvedor agora pode ser desabilitado por meio da [meta tag `aem-dev-login`.](/help/implementing/universal-editor/customizing.md#meta-tags)
* Um clique com o botão direito na seção de sobreposição agora exibe um menu de [opções contextuais.](/help/sites-cloud/authoring/universal-editor/authoring.md#context-options)
* O [recuo com escopo](/help/implementing/universal-editor/configure-rte.md#indentation) agora tem suporte no [editor de rich text.](/help/sites-cloud/authoring/universal-editor/authoring.md#formatting-options)

## Recursos da adoção antecipada {#early-adopter}

Se você estiver interessado em testar os recursos futuros listados abaixo e compartilhar seu feedback, envie um email para o seu Gerente de sucesso do cliente da Adobe a partir do endereço de email associado à sua Adobe ID.

* A cópia superficial foi implementada para Fragmentos de conteúdo.

## Outras melhorias {#other-improvements}

* O painel de propriedades agora é sincronizado quando vários campos são alterados em contexto.
* O seletor de Fragmento de conteúdo agora é aberto conforme esperado nas instâncias do AEM 6.5.
* A tecla Escape agora fecha as caixas de diálogo no editor de rich text.
* A ação **Remover componente** agora só está disponível quando um componente é selecionado.
* O editor de Fragmento de conteúdo correto (antigo ou novo) agora é aberto com base na instância usada (se o nome do host for o padrão do AEM as a Cloud Service, use o novo editor e, em seguida, use o editor herdado).
* A validação do filtro é adicionada à ação duplicar.
* Títulos longos agora são truncados no painel de propriedades.
* Os arrays gerenciadores de vários sites com mais de 10 valores agora são manipulados corretamente.
* Os erros de conflito ao criar vários componentes com o mesmo nome agora são manipulados corretamente.
* Foi adicionado gerenciamento de matriz de vários sites com valores >10.
