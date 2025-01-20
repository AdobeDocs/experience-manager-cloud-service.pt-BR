---
Title: Authoring a Form
Description: This article provides information on various form authoring platforms, including the Universal Editor, document-based authoring, and Adaptive Forms editors (Core Components and Foundation Components).
Keywords: Universal Editor for WYSIWYG authoring, document-based authoring, Adaptive Forms editors, Adaptive Forms editors for Core Components authoring, Adaptive Forms editors for Foundation Components authoring
feature: Edge Delivery Services
Role: User, Developer
hide: true
hidefromtoc: true
source-git-commit: bdc0e51a8b16df432f1f1aeabed11135fb8c8e0c
workflow-type: tm+mt
source-wordcount: '877'
ht-degree: 0%

---


# Criação de um formulário

O Adobe Experience Manager oferece e oferece suporte a vários editores para criar um Formulário. Você pode usar:
* Editor universal (para criação no WYSIWYG)
* Microsoft Excel ou Google Sheets (conhecido como criação baseada em documento)
* Editores adaptáveis do Forms (para Componentes principais ou criação baseada em componentes de base)

**[imagem a ser adicionada]**

## Editor universal (para criação no WYSIWYG)

O Universal Editor é um editor visual versátil que oferece um recurso &quot;o que você vê é o que você obtém&quot; (WYSIWYG), garantindo uma experiência intuitiva de criação de formulários. É recomendável usar o Editor universal ao criar novos formulários, pois ele fornece um design moderno e fácil de usar e uma interface conveniente de arrastar e soltar.

Para criar formulários usando o Editor universal, os modelos de Edge Delivery Services disponíveis no ambiente AEM são usados. Esses formulários herdam a aparência das configurações no repositório GitHub do Edge Delivery Services. [Uma conexão entre seu ambiente AEM e o repositório GitHub do Edge Delivery Services](/help/edge/docs/forms/publishing-forms.md) foi estabelecida para habilitar a publicação desses formulários no Edge Delivery Services.

Para obter etapas detalhadas sobre como criar usando o Editor Universal, consulte o artigo [Criação de Conteúdo com o Editor Universal](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/sites/authoring/universal-editor/authoring).

## Microsoft Excel ou Google Sheets (conhecido como criação baseada em documento)

Você pode criar formulários usando a criação baseada em documentos com arquivos do Microsoft Excel ou do Google Sheets, permitindo que você aproveite os ecossistemas e as APIs robustos do Google Sheets, do Microsoft Excel e do Microsoft SharePoint. Essa abordagem é particularmente útil para criar formulários simples sem serviços de envio avançados.

Para começar a criar um formulário usando o Microsoft Excel ou o Google Sheets, [configure um projeto AEM usando a placa-padrão do AEM Forms](/help/edge/docs/forms/tutorial.md#create-a-new-aem-project-pre-configured-with-adaptive-forms-block) e clone o repositório GitHub correspondente no computador local. O AEM Forms Edge Delivery fornece um recurso chamado Bloco de Forms adaptável, que simplifica o processo de criação de formulários para capturar e armazenar dados. Para saber como criar e publicar formulários usando o Bloco de Forms adaptável no Edge Delivery Services, consulte [Criar um formulário](/help/edge/docs/forms/create-forms.md).

## Editores adaptáveis do Forms (para Componentes principais ou criação baseada em componentes de base)

Você pode criar formulários envolventes, responsivos e dinâmicos. O editor de Formulário adaptável fornece um assistente amigável que permite criar rapidamente o Forms adaptável. O assistente de formulário apresenta uma navegação de guia fácil, permitindo selecionar modelos pré-configurados para componentes básicos ou principais, temas, modelos de dados e opções de envio para criar um formulário com eficiência.

[A criação de formulários com Componentes principais](/help/forms/creating-adaptive-form-core-components.md) permite que você aproveite componentes de captura de dados padronizados que podem ser personalizados, reduzindo o tempo de desenvolvimento e os custos de manutenção para experiências de inscrição digital. Esses formulários podem ser publicados usando o Bloco Forms adaptável no Edge Delivery Services ou por meio da instância AEM Publish.

[A criação de formulários com Foundation Components](/help/forms/create-an-adaptive-form.md) usa componentes de captura de dados clássicos. Esses formulários só podem ser publicados usando a instância AEM Publish.

Você também pode publicar formulários criados com os Editores Forms adaptáveis nos Edge Delivery Services estabelecendo uma [conexão entre seu ambiente AEM e o repositório GitHub dos Edge Delivery Services](/help/edge/docs/forms/publishing-forms.md).

## Como escolher entre vários tipos de criação de formulário?

A tabela a seguir descreve os recursos e casos de uso para cada editor de criação, ajudando você a escolher o editor correto com base em seus requisitos e necessidades de envio de formulário.

| **Editor de Criação de Formulário** | **Abordagem principal** | **Recursos** | **Método de Publicação** | **Casos de uso** |
|--------|-----------|-------|-------|------------------------------------------------|
| **Criação baseada em documento** | Aproveita ferramentas familiares, como o Google Docs e o Microsoft Office, para a criação de formulários. | Os Forms são projetados usando planilhas, com dados enviados diretamente para as planilhas do Google Sheets ou do Microsoft Excel. </br> </br> Esses formulários são mais rápidos de criar e implantar. Você não precisa de conhecimento prévio sobre AEM para desenvolver componentes e estilos personalizados para esses formulários. | Esses formulários são publicados em Edge Delivery Services e têm uma pontuação muito alta no Google Lighthouse. </br> </br> A pontuação mais alta resulta em uma renderização mais rápida e melhor SEO. | Esses formulários são ideais para a prototipagem rápida ou formulários básicos em que não são necessários serviços de envio avançados. </br> </br> Eles são adequados para pesquisas, registros ou formulários de feedback que exigem armazenamento de dados em planilhas. Esses formulários são publicados nos serviços da Edge Delivery |
| **Editor Universal** </br> </br> Se você estiver criando um novo formulário, use o Editor Universal para criar formulários. | Oferece uma interface do WYSIWYG para criação intuitiva de formulários. | Os Forms são projetados usando uma interface intuitiva de arrastar e soltar. </br> </br> Esses formulários usam a aparência e comportamento emprestados do repositório GitHub do Edge Delivery Services configurado para o formulário correspondente. | Esses formulários são publicados em Edge Delivery Services e têm uma pontuação muito alta no Google Lighthouse. </br> </br> A pontuação mais alta resulta em uma renderização mais rápida e melhor SEO. | Esses formulários são ideais para criar formulários para sites e páginas do Edge Delivery Service. Esses formulários apresentam cenários que envolvem formulários complexos, fluxos de trabalho complexos, ações personalizadas ou integrações com sistemas externos |
| **Editores adaptáveis do Forms** | Fornece uma abordagem orientada por assistente para iniciar rapidamente a criação de formulários usando modelos, estilo e campos predefinidos. | Use esses editores para criar formulários baseados em Componentes principais ou formulários baseados em Componentes de base. | Esses formulários podem ser publicados no Edge Delivery Services ou por meio de instâncias AEM Publish. | Use esses editores para criar formulários baseados em Componentes principais ou formulários baseados em Componentes de base. Ideal para cenários que envolvem formulários complexos, fluxos de trabalho complexos, ações personalizadas ou integrações com sistemas externos. |


>[!NOTE]
>
>
> Caso encontre recursos ausentes no Editor universal que estavam disponíveis anteriormente no editor do Adaptive Forms, você pode solicitá-los enviando um email para mailto:aem-forms-ea@adobe.com usando seu endereço de email oficial.

## Artigo relacionado

* [Criação baseada em documento usando o Microsoft Excel ou o Google Sheets](/help/edge/docs/forms/create-forms.md)
* [Editor universal para criação no WYSIWYG](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/edge-delivery/wysiwyg-authoring/authoring)
* [Criar um formulário adaptável (componentes de base)](/help/forms/creating-adaptive-form.md)
* [Criar um formulário adaptável (componentes principais)](/help/forms/create-an-adaptive-form.md)

## Consulte também

{{see-more-forms-eds}}