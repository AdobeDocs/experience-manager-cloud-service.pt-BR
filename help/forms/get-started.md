---
title: Introdução aos formulários HTML5
description: Para começar, implante o pacote complementar do AEM Forms e importe os formulários HTML5 existentes para o AEM.
content-type: reference
topic-tags: hTML5_forms
discoiquuid: f276d150-8936-4bfb-8475-7ca36815b233
feature: HTML5 Forms,Mobile Forms
exl-id: a3245f05-6ea3-4f90-8981-bfa89d2e7335
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 1496d7517d586c99c5f1001fff13d88275e91d09
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---

# Introdução aos formulários HTML5 {#getting-started-with-html-forms}

<span class="preview"> O recurso HTML5 Forms é oferecido como parte do Programa de acesso antecipado. Para solicitar acesso, envie um email de sua ID de email oficial (comercial) para aem-forms-ea@adobe.com.
</span>

Os formulários HTML5 oferecem vários recursos prontos para dispositivos móveis. Ele ajuda você a expandir suas soluções e fluxos de trabalho atuais para tablets ou dispositivos smartphones com navegadores HTML5. Alguns recursos incluem:

* Renderização de modelos de formulário XFA baseada em **HTML5:** Além do PDF forms comum, você agora pode renderizar seus formulários existentes baseados em XFA no formato HTML5. Ele ajuda a expandir a plataforma do cliente para dispositivos móveis (Apple iPad, tablet Android, smartphones e assim por diante) que oferecem suporte ao HTML5 e não oferecem suporte ao Adobe Reader com XFA Forms. Para obter mais informações sobre o recurso de renderização baseado em HTML5, consulte [Introdução aos formulários HTML5](/help/forms/introductionhtml5.md).

* **Gerenciamento do Forms:** Além disso, o AEM inclui novos recursos para simplificar o processo de organização e gerenciamento de formulários. Você pode ativar, desativar, publicar e visualizar formulários.<!--For more information, see [Introduction to managing forms](/help/forms/using/introduction-managing-forms.md).-->

## Configuração do ambiente para formulários HTML5 {#installing-html-forms}

Para ativar os envios de formulários e a renderização adequada do HTML5 Forms, execute as seguintes etapas:

* **Adicionar filtros do Dispatcher:** Atualize seu arquivo `src/conf.dispatcher.d/filters/filters.any` para permitir as solicitações necessárias para o HTML5 Forms. Adicione as seguintes regras de filtro:

  ```
  /0103 { /type "allow" /method '(HEAD|POST)' /url "/content/xfaforms/profiles/default.submit.html" }  # allow POSTs to form selectors under content
  /0104 { /type "allow" /method '(GET|HEAD|POST)' /url "/*.xdp.html" }
  ```

* **Adicione um pacote para envio:** No projeto, adicione um pacote na pasta `src/main/content/jcr_root/content` para oferecer suporte à funcionalidade de envio de formulário.

* **Importar HTML5 Forms:** importe seus formulários do sistema de arquivos local para o AEM Forms.
