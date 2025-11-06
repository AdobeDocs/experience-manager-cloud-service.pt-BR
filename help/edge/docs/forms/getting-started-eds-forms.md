---
title: Introdução ao Forms no AEM Edge Delivery Services
description: Saiba como criar e fornecer formulários de alto desempenho no Adobe Experience Manager Edge Delivery Services, com ênfase na abordagem de criação do Editor universal.
feature: Edge Delivery Services
exl-id: ecea1e05-d36b-4d63-af9d-c69dafd2f94f
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '580'
ht-degree: 1%

---


# Introdução ao Forms no AEM Edge Delivery Services

<!--
<span class="preview"> This is a pre-release feature available through our <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html#new-features">pre-release channel</a>. </span>
-->

O Adobe Experience Manager (AEM) Edge Delivery Services (EDS) permite oferecer experiências da Web ultrarrápidas e altamente escaláveis. Este guia explica **como criar e publicar formulários para essas experiências**, com uma hierarquia de recomendação clara:

1. **Editor Universal (UE) - a melhor opção para a maioria das equipes**
2. **Criação Baseada em Documentos (Docs/Folhas) - Ideal para formulários simples e rápidos**
3. **Criação de documentos (DA) - Use para inserir formulários em páginas criadas pelo DA**

Ao final, você poderá escolher o método de criação correto, entender as opções de envio e seguir as próximas etapas para criar formulários prontos para produção.



## Escolhendo um Método de Criação

| Equipe e requisitos | Método recomendado | Por que |
|--------------------|--------------------|-----|
| Profissionais de marketing/designers precisam de controle visual, lógica condicional ou integrações do AEM | **Universal Editor** | Arrastar e soltar, regras avançadas, envios para FSS ou AEM Publish |
| Autores de conteúdo já trabalhando no Word/Google Docs/Sheets; captura de dados simples em planilha/email | **Criação Baseada em Documento** | Ferramentas familiares, caminho mais rápido para formulários básicos |
| Páginas do site criadas em **Document Authoring (DA)** | **Incorpore** um formulário UE ou Baseado em Doc na página do DA | O DA não cria formulários por conta própria |


## Métodos de criação em detalhes

### Editor universal

O Universal Editor é uma ferramenta de criação visual, do tipo &quot;arrastar e soltar&quot;, para profissionais de marketing e designers que combina velocidade e eficiência de nível empresarial:

- Edição em tempo real do WYSIWYG e visualizações de dispositivos.
- Regras avançadas e interface de validação — nenhum código é necessário.
- Integração direta com ativos, workflows e modelos de dados de formulário (FDM) do AEM.
- Entrega contínua para desenvolvedores para componentes personalizados em JS/CSS básicos.
- Destinos de envio flexíveis: comece de forma simples com o **Serviço de Envio do Forms (FSS)** ou alterne para as **ações de envio de Publicação do AEM** conforme suas necessidades aumentarem.

> **Recomendação**: inicie todos os novos projetos de formulário com o Universal Editor, a menos que sua equipe seja 100% centrada em documentos e o formulário seja muito básico.


### Criação Baseada Em Documento (Documentos/Planilhas)

A Criação baseada em documento é mais adequada para criar formulários simples e de baixa complexidade usando ferramentas familiares, como o Microsoft Word, Google Docs ou Google Sheets. Esse método é ideal para equipes de conteúdo que exigem uma maneira rápida e direta de criar formulários.

- Defina campos de formulário em uma tabela (Documentos) ou como linhas (Planilhas).
- Oferece suporte à validação básica de campo e ao Google reCAPTCHA para proteção contra spam.
- Os envios de formulários são tratados exclusivamente pelo Serviço de envio do Forms.
- Publicação instantânea — todas as alterações feitas no documento de origem são refletidas imediatamente no site, sem exigir um pipeline de implantação.


### Incorporação do Forms na Criação de documentos (DA)

A Criação de documentos (DA) foi projetada para criar conteúdo de página estruturada e não oferece suporte à criação de formulários nativos. Para adicionar um formulário a uma página criada pelo DA, siga estas etapas:

1. Crie o formulário usando o **Editor Universal** (recomendado) ou Criação Baseada em Documento.
2. Publique o formulário para gerar uma URL exclusiva (por exemplo, `/forms/contact-us`).
3. Na página do DA, insira um bloco **Incorporar formulário** e especifique a URL do formulário publicado.

<!-- 
## Feature Comparison

| Capability | Universal Editor | Document-Based | Document Authoring |
|------------|-----------------|----------------|--------------------|
| Visual drag-and-drop | ✅ | – | – |
| Advanced rules editor | ✅ | Limited | – |
| Attachments | ✅ | EA | – |
| reCAPTCHA Enterprise | ✅ | ✅ | Depends on embed |
| Submit to spreadsheet/email | ✅ (FSS) | ✅ (FSS) | Via embed |
| Submit to AEM workflows/FDM | ✅ | – | Via UE embed |
| Custom components (JS/CSS) | ✅ | ✅ | Via embed |
| Localization via Sites | ✅ | Manual | Via embed |

-->

## Próximas etapas

1. **Iniciar com Editor Universal:** Consulte o [guia de introdução do Editor Universal](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md) para começar a criar formulários.
2. **Configurar o envio do formulário:** Selecione e configure seu método de envio preferencial. Consulte [Serviço de Envio do Forms](/help/edge/docs/forms/configure-submission-action-for-eds-forms.md) ou Ações de envio de Publicação do AEM para obter instruções de configuração.
3. **Aplicar práticas recomendadas:** revise as [práticas recomendadas de design do formulário](/help/edge/docs/forms/universal-editor/best-practices-eds-forms.md) para garantir acessibilidade e desempenho.
4. **Usar Criação Baseada em Documento:** Para criar formulários com o Microsoft Excel ou o Google Sheets, siga o [Tutorial de Criação Baseada em Documento](/help/edge/docs/forms/tutorial.md).
5. **Incorporar o Forms na Criação de Documentos:** Se você estiver criando páginas na Criação de Documentos, consulte o [tutorial do DA](https://www.aem.live/developer/da-tutorial) para obter instruções sobre como incorporar formulários publicados.

> **Agora você está pronto para criar seu primeiro formulário de alto desempenho com o AEM Edge Delivery Services.**