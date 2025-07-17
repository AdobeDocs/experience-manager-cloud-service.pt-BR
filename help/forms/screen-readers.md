---
title: Leitores de tela para formulários HTML5
description: Lista os leitores de tela compatíveis com os formulários HTML5.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 53c57180-7004-4534-9146-603f7770a6fe
feature: HTML5 Forms,Mobile Forms
exl-id: 07d20c2f-7d13-48ac-8d58-b367eb194558
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 22aeedaaf4171ad295199a989e659b6bf5ce9834
workflow-type: tm+mt
source-wordcount: '331'
ht-degree: 0%

---

# Leitores de tela para formulários HTML5 {#screen-readers-for-html-forms}

<span class="preview"> O recurso HTML5 Forms é oferecido como parte do Programa de acesso antecipado. Para solicitar acesso, envie um email de sua ID de email oficial (comercial) para aem-forms-ea@adobe.com.
</span>

Os componentes de formulários do HTML5 renderizam o modelo de formulário XFA para um formato HTML5. Todos os navegadores padrão compatíveis com HTML5 podem renderizar esses formulários. Para oferecer suporte a uma experiência de captura de dados semelhante nos formulários do PDF e do HTML5, o layout do PDF forms é retido nos formulários do HTML5.

Os formulários do HTML5 usam construções padrão do HTML, permitindo que ferramentas de acessibilidade regulares para o HTML sejam usadas com esses formulários. Se um formulário for criado de acordo com as práticas recomendadas para formulários acessíveis, ele funcionará com qualquer leitor de tela compatível. Além disso, esses formulários são ativados para navegação pelo teclado.

## Padrões de acessibilidade {#accessibility-standards}

Os formulários HTML5 estão em conformidade com a seção 508 para acessibilidade com exceções conhecidas. Consulte [VPAT para formulários HTML5](https://www.adobe.com/content/dam/cc1/en/accessibility/compliance/pdfs/adobe-livecycle-es4-section-508-vpat-portfolio.pdf) para obter detalhes.

## Leitores de tela certificados para formulários HTML5 {#certified-screen-readers-for-html-forms}

* JAWS 14.0 no Microsoft® Windows
* VoiceOver no macOS X e iPad

### MANDÍBULAS {#jaws}

Todos os pressionamentos de tecla e atalhos padrão funcionam para formulários HTML5. Para obter mais informações sobre o uso do JAWS, visite [https://www.freedomscientific.com/jaws-hq.asp](https://www.freedomscientific.com/jaws-hq.asp).

### VoiceOver {#voiceover}

Os formulários HTML5 são compatíveis com todos os pressionamentos de tecla e gestos padrão do Voice over. Para obter mais informações sobre como configurar e usar o VoiceOver, consulte [https://www.apple.com/accessibility/vision/](https://www.apple.com/accessibility/vision/).

## Problemas conhecidos {#known-issues}

* **(Somente Gerenciador Interno 9)** Nos formulários HTML5, as páginas são carregadas sob demanda (dinamicamente). O carregamento de página sob demanda causa problemas com o funcionamento dos leitores de tela. Quando o foco do leitor de tela está no último campo da página e o usuário pressiona Tab, o leitor de tela retorna o foco para o primeiro campo da primeira página do formulário.
* **(Somente no Gerenciador Interno 9)** O controle Seletor de Datas em formulários HTML5 não é totalmente acessível com teclado. No controle Seletor de datas, se você pressionar as teclas Para cima/Para baixo várias vezes, o controle Seletor de datas será fechado e o foco será movido para o próximo/último campo.

* O VoiceOver não consegue detectar as teclas de seta no widget de data no iPad safari.
