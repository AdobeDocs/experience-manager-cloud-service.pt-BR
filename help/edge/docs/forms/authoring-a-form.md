---
title: Como criar formulários no AEM?
description: Saiba mais sobre as várias plataformas de criação de formulários disponíveis no Adobe Experience Manager (AEM) e como escolher a correta com base em suas necessidades.
feature: Edge Delivery Services, Adaptive Forms, Core Components
role: User, Developer
exl-id: bd9cb623-c272-4cdf-ad39-f97043f781a6
source-git-commit: a2f85b844aaff1642340250c5d8a755c80b9373d
workflow-type: tm+mt
source-wordcount: '1176'
ht-degree: 1%

---

# Como criar Forms no Adobe Experience Manager (AEM)?

O Adobe Experience Manager (AEM) fornece uma plataforma flexível para a criação de formulários envolventes, responsivos, dinâmicos e adaptáveis. Ele oferece uma interface de usuário intuitiva e um conjunto avançado de componentes prontos para uso para criar e gerenciar o Adaptive Forms. O Forms pode ser criado com ou sem um modelo de formulário ou esquema, dependendo de seus requisitos.

## Considerações principais ao escolher uma plataforma de criação

O AEM fornece várias opções de criação de formulários para criar formulários interativos e envolventes. Ao selecionar um ambiente de criação de formulário, considere os seguintes fatores:

| ?? **Consideração** | ?? **O que perguntar** |
|----------------------|--------------------|
| **Experiência do usuário** | Quem criará os formulários — desenvolvedores, usuários empresariais ou autores de conteúdo? |
| **Complexidade do formulário** | O formulário precisa de regras avançadas, seções dinâmicas ou integrações? |
| **Necessidades de Reutilização** | Partes do formulário serão reutilizadas em diferentes formulários ou projetos? |
| **Flexibilidade de design** | Você precisa de controle total sobre layout, temas e estilo? |
| **Requisitos de integração** | O formulário precisa se conectar a modelos de dados, fluxos de trabalho ou sistemas externos? |
| **Facilidade de uso** | A plataforma é intuitiva para o nível de habilidade técnica da sua equipe? |
| **Desempenho e escalabilidade** | O formulário será usado em escala ou em ambientes de alto tráfego? |
| **Entrega omnicanal** | O formulário será usado em sites, aplicativos móveis, quiosques ou vários canais? |
| **Flexibilidade de publicação** | Onde os formulários serão publicados no AEM, no Edge Delivery ou em aplicativos personalizados? |

## Visão geral dos métodos de criação de formulários no AEM

O AEM oferece suporte a vários métodos de criação, cada um adequado para diferentes necessidades de usuários, níveis de habilidade técnica e destinos de publicação.

* [Componentes de base](/help/forms/create-adaptive-form-tutorial.md): use Componentes de base para criar formulários tradicionais e interativos. Mais adequado para formulários que se integram a sistemas herdados ou que dependem de fluxos de trabalho já estabelecidos. O Forms criado com os Componentes de base pode ser publicado somente no AEM e não é compatível com o Edge Delivery Services.

* [Componentes principais](/help/forms/creating-adaptive-form-core-components.md): use Componentes principais para criar formulários modernos, responsivos e escalonáveis. Eles oferecem suporte à reutilização, acessibilidade e melhor desempenho. O Forms criado com os Componentes principais pode ser publicado no AEM e no Edge Delivery Services, oferecendo flexibilidade entre plataformas.

* [Edge Delivery Services Forms](/help/edge/docs/forms/overview.md): o Edge Delivery Services Forms transforma a maneira como os formulários são criados, executados e processados. Ao utilizar o Edge Delivery Services, as organizações podem criar formulários digitais rápidos, seguros e altamente disponíveis, aprimorando a experiência do usuário e a eficiência operacional com um ambiente de desenvolvimento rápido. Você pode criar o Edge Delivery Services Forms de duas maneiras:
   * [Criação no WYSIWYG](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md): use o Universal Editor para criar formulários visuais, do tipo arrastar-e-soltar, ideais para autores de conteúdo com conhecimento técnico limitado. O Forms criado com Universal Editor é fornecido usando o Edge Delivery Services para renderização rápida e leve.
   * [Criação com base em documento](/help/edge/docs/forms/tutorial.md): use ferramentas como o Microsoft Excel ou o Google Sheets para definir a estrutura e o conteúdo do formulário. Esse método é útil para usuários empresariais que preferem entradas orientadas por planilha. Normalmente, esses formulários são publicados por meio do Edge Delivery Services e são adequados para casos de uso leves e de alto volume.
* [Criação headless](https://experienceleague.adobe.com/en/docs/experience-manager-headless-adaptive-forms/using/tutorial/build-engaging-forms-using-core-components-and-headless-adaptive-forms-aem-forms-cloud-service): use APIs para renderizar formulários como JSON para qualquer front-end, por exemplo, React, Angular, aplicativos móveis ou quiosques, sem depender do AEM. Atualmente, somente os Componentes principais são compatíveis com entrega headless. Os formulários headless são ideais para casos de uso omnicanal e são consumidos independentemente da renderização de página do AEM, tornando-os flexíveis para implantações front-end personalizadas.

### Análise comparativa de métodos de criação de formulários do AEM

&#x200B;A tabela a seguir oferece uma comparação concisa de vários métodos de criação de formulário do AEM, destacando as abordagens, os recursos, as opções de publicação e os casos de uso ideais para auxiliar na seleção do método mais adequado às suas necessidades.

| **Consideração** | **Componentes de base** | **Componentes principais** | **Editor Universal (WYSIWYG)** | **Criação baseada em documento** | **Criação headless** |
|--------------------------|---------------------------------------------------------------------|------------------------------------------------------------------------|-------------------------------------------------------------------------|---------------------------------------------------------------------------|-------------------------------------------------------------------------|
| **Ideal Para** | Manutenção de formulários e workflows herdados no AEM | Formulários dimensionáveis e modernos com fluxos de trabalho e integrações complexos | Criar formulários para sites de serviços do Edge Delivery com requisitos complexos | Criação rápida de protótipos ou formulários básicos sem serviços avançados de envio | Experiências omnicanal em plataformas (Web, dispositivos móveis, quiosques etc.) |
| **Experiência do usuário** | Desenvolvedores, autores de conteúdo | Desenvolvedores, autores avançados | Usuários empresariais, autores de conteúdo | Usuários empresariais | Desenvolvedores |
| **Complexidade do formulário** | Formulários básicos | Formulários complexos com seções dinâmicas | Formulários complexos com ações personalizadas | Formulários simples | Formulários altamente complexos orientados por API |
| **Flexibilidade de design** | Limitado | Alta (personalização de CSS/JS) | Moderado (com base em modelos) | Limitado | Alta (controle de estrutura de front-end) |
| **Recurso de Integração** | Fluxos de trabalho básicos do AEM | Avançado (modelos de dados, workflows) | Integrado a sistemas externos | Básico (Google Sheets, Excel) | Controle total via APIs |
| **Método de Publicação** | Somente AEM | AEM e EDGE DELIVERY SERVICES | Edge Delivery Services | Edge Delivery Services | Qualquer front-end via APIs |
| **Desempenho e SEO** | Padrão | Aprimorado em relação aos componentes de base | Pontuações altas do Google Lighthouse para renderização mais rápida e melhor SEO | Pontuações altas do Google Lighthouse para renderização mais rápida e melhor SEO | Depende da implementação |
| **Entrega omnicanal** | Limitado | Moderado | Moderado | Limitado | Alta |

<!--
| **Form authoring methods** | **Key Approach** | **Features** | **Publishing Method** | **Use Cases** |
|-----------------------------|------------------|--------------|-----------------------|---------------|
| **Foundation Components** | Classic AEM authoring interface designed for standard web pages. | Includes basic components like text, images, tables, and charts. Limited reuse capabilities and primarily web-based. | Published on AEM only. | Best for maintaining legacy forms and workflows within AEM. |
| **Core Components** | Provides a modern, flexible approach with high customization capabilities. | Component-based authoring within AEM, offering high customization with CSS and JS. Built around accessibility guidelines and integrated with AEM Sites. | Published on AEM and Edge Delivery Services. | Suitable for scalable, modern forms with complex workflows and integrations. |
| **Universal Editor (WYSIWYG)** | Offers a WYSIWYG interface for intuitive form creation. | Forms are designed using an intuitive drag-and-drop interface. These forms inherit look and feel from the configured Edge Delivery Services GitHub repository for the corresponding form. | Published on Edge Delivery Services, achieving high Google Lighthouse scores for faster rendering and better SEO. | Ideal for creating forms for Edge Delivery Service sites and pages, especially scenarios involving complex forms, workflows, custom actions, or integrations with external systems. |
| **Document-based Authoring** | Uses familiar tools like Google Docs and Microsoft Office for form creation. | Forms are designed using spreadsheets, with data directly submitted to Google Sheets or Microsoft Excel. These forms are faster to create and deploy. No prior knowledge of AEM is required to develop custom components and styles for these forms. | Published on Edge Delivery Services, achieving high Google Lighthouse scores for faster rendering and better SEO. | Ideal for quick prototyping or basic forms where advanced submission services are not needed. Well-suited for surveys, registration, or feedback forms requiring data storage in spreadsheets. |
| **Headless Authoring** | Enables API-driven content creation for omnichannel delivery. | Full control via frontend frameworks, allowing content delivery across various platforms through APIs. | Can be integrated with any frontend via APIs. | Ideal for omnichannel experiences across platforms, suitable for web, mobile, kiosks, and more. |-->

### Comparação de recursos dos métodos de criação de formulários do AEM

A tabela a seguir fornece uma comparação detalhada dos principais recursos entre os diferentes métodos de criação de formulário do AEM, auxiliando na seleção da abordagem mais adequada para suas necessidades.&#x200B;

| **Recurso** | **Componentes de base** | **Componentes principais** | **Editor Universal (WYSIWYG)** | **Criação baseada em documento** | **Criação headless** |
|-----------------------------------------|---------------------------|---------------------|-------------------------------|-----------------------------|------------------------|
| **Composição Unificada com Sites** | ❌  | ✅  | ✅  | ❌  | ❌  |
| **Incorporando Suporte a Formulários** | ✅  | ✅  | ✅  | ✅  | ✅  |
| **Regras (Comportamento Dinâmico)** | Editor de regras avançado com funções personalizadas | Editor de regras avançado com funções personalizadas | Editor de regras avançado com funções personalizadas | Limitado: Mostrar/ocultar, valor de computação, funções personalizadas | Limitado: requer implementação personalizada |
| **Suporte ao Anexo** | ✅  | ✅  | ✅  | ℹ️ (Acesso antecipado) | ❌  |
| **Suporte ao CAPTCHA** | reCAPTCHA v2/Enterprise, hCaptcha (EA), Torniquete (EA) | reCAPTCHA v2/Enterprise, hCaptcha (EA) | reCAPTCHA Enterprise | reCAPTCHA Enterprise | Requer integração personalizada |
| **Recursos de Envio** | Endpoint REST, Email, Modelo de dados de formulário (FDM), Chamar fluxo de trabalho do AEM, SharePoint, OneDrive, Armazenamento Azure Blob, Power Automate, Workfront Fusion (EA) | Endpoint REST, Email, Modelo de dados de formulário (FDM), Chamar fluxo de trabalho do AEM, SharePoint, OneDrive, Armazenamento Azure Blob, Power Automate, Workfront Fusion (EA) | Endpoint REST, Email, Modelo de dados de formulário (FDM), Chamar fluxo de trabalho do AEM, SharePoint, OneDrive, Armazenamento Azure Blob, Power Automate, Workfront Fusion (EA) | Somente planilha | Endpoints de API personalizados |
| **Esquema de dados** | FDM, Personalizado | FDM, Personalizado | FDM, Personalizado | Personalizado | Personalizado |
| **Preenchimento prévio** | ✅  | ✅  | ?? (por meio do Assistente) | ✅  | Implementação personalizada |
| **Fragmentos** | ✅  | ✅  | ✅  | ✅  | ❌  |
| **Editor de regras visuais** | ✅  | ✅  | ✅  | ❌  | ❌  |
| **Localização** | ✅  | ✅  | ?? (pelo Sites) | ℹ️ (Excel - Manual, Função do Google Sheets) | Implementação personalizada |
| **Esquema de Dados (Árvore de Dados)** | ✅  | ✅  | ?? (por meio da extensão da interface do usuário) | ❌  | Implementação personalizada |
| **Suporte a modelos** | ✅  | ✅  | Somente conteúdo inicial, sem política | ❌  | Implementação personalizada |
| **Portal** | ✅  | ✅  | ❌  | ❌  | ❌  |
| **Criação de DoR** | ✅  | ✅  | ?? (via Derlina) | ❌  | ❌  |
| **Geração do DoR** | ✅  | ✅  | ?? (FORMS-2475 Novo) | ❌  | ❌  |
| **Tema** | ✅  | ✅  | ℹ️ (a nível do projeto) | ℹ️ (a nível do projeto) | Implementação personalizada |
| **Componente personalizado** | ✅  | ✅  | ✅  | ✅  | ✅  |
| **OOTB e funções personalizadas** | ✅  | ✅  | ✅  | ✅  | ✅  |
| **Referência do fragmento** | ✅  | ❌  | ❌  | ❌  | ❌  |
| **Assinar Integração** | ✅  | ❌  | ❌  | ❌  | ❌  |
| **Suporte de RTL** | ❌  | ✅  | ??  | ??  | Implementação personalizada |
| **Experimentação** | ❌  | ❌  | ✅  | ✅  | Implementação personalizada |
| **Gerenciamento de tarefas via Workfront** | ❌  | ❌  | ✅  | ❌  | ❌  |
| **Extensão do Personalization** | ❌  | ❌  | ??  | ❌  | Implementação personalizada |
| **Personalização do editor** | ❌  | ❌  | ✔ (via Extensão da Interface do Usuário) | ❌  | Implementação personalizada |
| **Enviar ação** | ✅  | ✅  | ✅  | Somente planilha | Implementação personalizada |


## Artigo relacionado

* [Criação baseada em documento usando o Microsoft Excel ou o Google Sheets](/help/edge/docs/forms/create-forms.md)
* [Editor universal para criação no WYSIWYG](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/edge-delivery/wysiwyg-authoring/authoring)
* [Criar um formulário adaptável (componentes de base)](/help/forms/creating-adaptive-form.md)
* [Criar um formulário adaptável (componentes principais)](/help/forms/create-an-adaptive-form.md)
