---
title: Notas de versão do Universal Editor 2025.10.30
description: Estas são as notas de versão do Universal Editor 2025.10.30.
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: e3e571bef450ddc09eb30ab7d73b144ea521a87b
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 0%

---


# Notas de versão do Universal Editor 2025.10.30 {#release-notes}

Estas são as notas de versão do Universal Editor de 30 de outubro de 2025.

>[!TIP]
>
>Se você deseja testar os recursos do Universal Editor **futuros** antes de eles serem lançados, consulte as [Notas de Versão de Visualização do Universal Editor.](/help/release-notes/universal-editor/preview.md)

>[!TIP]
>
>Para obter as notas de versão atuais do Adobe Experience Manager as a Cloud Service, consulte [esta página](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Novidades {#what-is-new}

* [O novo RTE](#new-rte) agora pode inserir imagens.
   * Este recurso está desabilitado OtB e precisa ser habilitado explicitamente por meio de uma [definição de filtro.](/help/implementing/universal-editor/configure-rte.md#toolbar)

## Recursos da adoção antecipada {#early-adopter}

Se você estiver interessado em testar esses recursos futuros e compartilhar seu feedback, envie um email para o Gerente de sucesso do cliente da Adobe a partir do endereço de email associado à sua Adobe ID.

### Novo RTE {#new-rte}

O novo RTE do ProseMirror, com um seletor de páginas na caixa de diálogo de link, agora está disponível no painel direito. [Este RTE apresenta opções de configuração flexíveis.](/help/implementing/universal-editor/configure-rte.md)

## Outras melhorias {#other-improvements}

* Atualizar evento agora é informado se a ação foi desfeita.
* A cadeia de caracteres `No results` agora depende da localidade do navegador nas marcas do Editor Universal.
* Correção da quebra de linha extra no botão Publicar do Editor Universal.
* Foi feita uma limpeza na API de patch.
* O botão Selecionar conteúdo agora está visível no Safari.
* Compilação RPM corrigida.
* Atualização do CORS para evitar a atualização do texto editado novamente após salvar.
