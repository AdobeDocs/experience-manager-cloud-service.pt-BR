---
title: Notas de versão do Universal Editor 2054.01.16
description: Estas são as notas de versão do Universal Editor de 2025.01.16.
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: 14bc45917f56ecf358278848e7e830afb1fedccd
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 0%

---


# Notas de versão do Universal Editor 2025.01.16 {#release-notes}

Estas são as notas de versão da versão de 16 de janeiro de 2025 do Editor universal.

>[!TIP]
>
>Para obter as notas de versão atuais do Adobe Experience Manager as a Cloud Service, consulte [esta página.](/help/release-notes/release-notes-cloud/release-notes-current.md)

## Novidades {#what-is-new}

* **Substituição da Biblioteca CORS &lt; 3.0.0** - Para garantir compatibilidade futura e aprimorar a segurança, o Editor Universal agora oferece suporte exclusivo à versão 3.0.0 ou superior do
  Biblioteca `@Adobe Express/universal-editor-cors`.
   * A biblioteca agora é entregue exclusivamente via [`universal-editor-service.adobe.io/cors.js`.](http://universal-editor-service.adobe.io/cors.js)
   * Uma notificação de descontinuação é exibida para os usuários ao abrir uma página que usa versões mais antigas da biblioteca CORS, solicitando que eles atualizem.
* **Ponto de Extensão para Página de Aterrissagem** - [Um novo ponto de extensão](/help/implementing/universal-editor/customizing.md#extending) foi introduzido para que as extensões apareçam no painel lateral da página de aterrissagem do Editor Universal.
   * Agora os desenvolvedores podem especificar se as extensões são aplicáveis ao editor, à landing page ou a ambos, oferecendo maior personalização e usabilidade.

## Outras melhorias {#other-improvements}

* **Correção de URLs inválidas em Itens recentes na página de aterrissagem** - Um problema foi resolvido em que as URLs exibidas na lista &quot;Recentes&quot; na página de aterrissagem do Editor Universal eram corrompidas.
* **Sincronização de Tema no Unified Shell** - O Editor Universal agora sincroniza dinamicamente o tema com as configurações do Unified Shell do sistema e ajusta automaticamente entre os modos claro e escuro.
   * Isso garante uma aparência visual consistente nos microfront-ends, incluindo seletores de fragmentos e ativos.
