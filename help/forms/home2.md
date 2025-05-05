---
title: Introdução ao  [!DNL AEM Forms]  as a Cloud Service
description: Utilize o AEM Forms para produzir formulários prontos para os negócios, criar fluxos de trabalho de processo empresarial e usar serviços de documento para criar e proteger documentos.
landing-page-description: Saiba como usar formulários no AEM as a Cloud Service.
role: Admin, Developer, User
feature: Adaptive Forms, Release Information
hide: true
hidefromtoc: true
source-git-commit: 4b4bc6f754c6336136d409cf49617c7fafd4f4c3
workflow-type: tm+mt
source-wordcount: '1145'
ht-degree: 10%

---


# AEM Forms as a Cloud Service {#introduction}

<!-- Version Navigation -->
<div class="version-selector">
  <p><strong>Procurando documentação para uma versão diferente?</strong></p>
  <ul>
    <li><a href="https://experienceleague.adobe.com/docs/experience-manager-65/forms/home.html?lang=pt-BR">Documentação do AEM 6.5 Forms</a></li>
    <li><strong>AEM Forms as a Cloud Service</strong> (Atual)</li>
  </ul>
</div>

## O que é o AEM Forms as a Cloud Service?

O AEM Forms as a Cloud Service é a solução nativa em nuvem da Adobe para criar, gerenciar e fornecer formulários e comunicações digitais. Ele permite que as organizações transformem transações complexas em experiências simples e digitais em toda a jornada do cliente. Você pode usar o serviço para:

* Digitalize e simplifique a experiência de inscrição e integração
* Fornecer comunicações personalizadas
* Automatizar fluxos de trabalho de back-office
* Integrar formulários e experiências de comunicação com fontes de dados
* Rastrear e otimizar o desempenho de formulários

O serviço é sempre atual, está sempre disponível e sempre aprendendo. As organizações podem usar o [!DNL AEM Forms] as a Cloud Service e obter todos esses recursos na nuvem sem a necessidade de nenhuma infraestrutura local. O serviço também livra as organizações de ciclos complexos de atualização, pois está sempre atualizado com os recursos mais recentes.

O Adobe [!DNL Experience Manager Forms as a Cloud Service] é uma solução centrada no cliente que oferece suporte a cada etapa da jornada do cliente:

<div class="card-container" style="display: flex; flex-wrap: wrap; gap: 20px; margin-bottom: 30px;">
  <div class="card" style="flex: 1 1 calc(50% - 20px); min-width: 300px; border: 1px solid #e1e1e1; border-radius: 8px; overflow: hidden; box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1); transition: transform 0.3s ease, box-shadow 0.3s ease;">
    <div class="card-header" style="background-color: #f5f5f5; padding: 15px 20px; border-bottom: 1px solid #e1e1e1;">
      <h3>Formulários adaptáveis</h3>
    </div>
    <div class="card-body" style="padding: 20px; background-color: #ffffff;">
      <p>Crie formulários responsivos e dinâmicos que se adaptem à entrada do usuário e ao tipo de dispositivo:</p>
      <ul>
        <li><a href="https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/creating-adaptive-form-core-components">Criar Forms Adaptável</a> - Crie formulários que se ajustam automaticamente a diferentes tamanhos de tela e entradas de usuário</li>
        <li><a href="https://experienceleague.adobe.com/pt-br/docs/experience-manager-core-components/using/adaptive-forms/introduction#available-components-a-breakdown-by-component-type">Biblioteca de Componentes Avançados</a> - Use uma variedade de campos de entrada e componentes de interface do usuário</li>
        <li><a href="https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/using-themes-in-core-components">Estilo do Forms Adaptável</a> - Aplique identidade visual e identidade visual consistentes a seus formulários</li>
        <li><a href="https://experienceleague.adobe.com/pt-br/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components">Usar temas e modelos pré-criados</a> - Acelere o desenvolvimento com componentes prontos para uso</li>
        <li><a href="https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/rule-editor-core-components/rule-editor-core-components">Validação de formulários</a> - Implementar regras de validação no lado do cliente e no lado do servidor</li>
        <li><a href="https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/configure-submit-actions-core-components">Ações de Envio</a> - Configure o que acontece quando os usuários enviam formulários</li>
        <li><a href="https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/generate-document-of-record-core-components">Documento de Registro</a> - Criar registros permanentes de dados de formulário enviados</li>
        <li><a href="https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/create-or-add-an-adaptive-form-to-aem-sites-page">Adicionar o Forms às páginas do AEM Sites</a> - Integre formulários com perfeição ao seu site</li>
        <li><a href="https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/forms/integrate/services/embed-adaptive-form-core-components-external-web-page">Adicionar o Forms a páginas de sites de terceiros</a> - Integrar formulários facilmente ao seu site</li>
      </ul>
    </div>
  </div>

<div class="card" style="flex: 1 1 calc(50% - 20px); min-width: 300px; border: 1px solid #e1e1e1; border-radius: 8px; overflow: hidden; box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1); transition: transform 0.3s ease, box-shadow 0.3s ease;">
    <div class="card-header" style="background-color: #f5f5f5; padding: 15px 20px; border-bottom: 1px solid #e1e1e1;">
      <h3>APIs de comunicação</h3>
    </div>
    <div class="card-body" style="padding: 20px; background-color: #ffffff;">
      <p>Gerar, manipular e proteger documentos de forma programática:</p>
      <ul>
        <li><a href="https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction#document-generation">Gerar comunicações personalizadas</a> - Crie documentos personalizados com base em modelos e dados</li>
        <li><a href="https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction#document-manipulation">Montar e manipular PDFs</a> - Combinar, dividir e modificar documentos do PDF</li>
        <li><a href="https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction#convert-to-and-validate-pdfa-compliant-documents">Criar Documentos PDF/A</a> - Gerar documentos com qualidade de arquivo</li>
        <li><a href="https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction#signature-apis">Aplicar assinaturas</a> - Proteger documentos com assinaturas</li>
        <li><a href="https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction#encryption-apis">Criptografar e descriptografar PDFs</a> - Proteger conteúdo confidencial de documentos</li>
        <li><a href="https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction#create-PS-PCL-ZPL-documents">Converter XDP em PostScript</a> - Transformar documentos XDP no formato PostScript</li>
        <li><a href="https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction#create-PS-PCL-ZPL-documents">Converter XDP em PCL</a> - Transformar documentos XDP em Linguagem de Comando de Impressora</li>
        <li><a href="https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction#create-PS-PCL-ZPL-documents">Converter XDP em ZPL</a> - Transformar documentos XDP em Idioma de Impressão Zebra</li>
        <li><a href="https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction#convert-to-and-validate-pdfa-compliant-documents">Converter PDF em Padrões PDF/A</a> - Criar documentos PDF compatíveis com arquivamento</li>
        <li><a href="https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction#convert-pdf-documents-to-pdf-x-standards">Adicionar Assinaturas Digitais</a> - Assinar documentos digitalmente para autenticação</li>
      </ul>
    </div>
  </div>

<div class="card" style="flex: 1 1 calc(50% - 20px); min-width: 300px; border: 1px solid #e1e1e1; border-radius: 8px; overflow: hidden; box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1); transition: transform 0.3s ease, box-shadow 0.3s ease;">
    <div class="card-header" style="background-color: #f5f5f5; padding: 15px 20px; border-bottom: 1px solid #e1e1e1;">
      <h3>Edge Delivery Services para Forms</h3>
    </div>
    <div class="card-body" style="padding: 20px; background-color: #ffffff;">
      <p>Criar e fornecer formulários usando o Edge Delivery Services:</p>
      <ul>
        <li><a href="https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/overview">Visão geral do Edge Delivery Forms</a> - Saiba mais sobre formulários com o Edge Delivery Services</li>
        <li><a href="https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/universal-editor/getting-started-universal-editor">Editor Universal para Forms</a> - Criar formulários usando o Editor Universal do WYSIWYG</li>
        <li><a href="https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/getting-started-edge-delivery-services-forms/tutorial">Criação baseada em documentos</a> - Criar formulários usando o Microsoft Word ou Google Docs</li>
        <li><a href="https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/universal-editor/style-theme-forms">Estilo Edge Delivery Forms</a> - Aplicar estilo personalizado aos seus formulários</li>
      </ul>
    </div>
  </div>

<div class="card" style="flex: 1 1 calc(50% - 20px); min-width: 300px; border: 1px solid #e1e1e1; border-radius: 8px; overflow: hidden; box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1); transition: transform 0.3s ease, box-shadow 0.3s ease;">
    <div class="card-header" style="background-color: #f5f5f5; padding: 15px 20px; border-bottom: 1px solid #e1e1e1;">
      <h3>Forms headless</h3>
    </div>
    <div class="card-body" style="padding: 20px; background-color: #ffffff;">
      <p>Ofereça experiências de formulário em qualquer canal ou estrutura de front-end:</p>
      <ul>
        <li><a href="https://experienceleague.adobe.com/pt-br/docs/experience-manager-headless-adaptive-forms/using/overview">Introdução ao Headless Forms</a> - saiba mais sobre a abordagem headless em formulários</li>
        <li>Criar formulários usando o React ou outras estruturas de front-end</li>
        <li>Integrar formulários a aplicativos móveis, sites e aplicativos de chat</li>
        <li>Aproveite os componentes existentes da interface do usuário com a funcionalidade de formulários</li>
        <li>Manter a lógica de formulário de back-end enquanto tem flexibilidade de front-end</li>
      </ul>
    </div>
  </div>

<div class="card" style="flex: 1 1 calc(50% - 20px); min-width: 300px; border: 1px solid #e1e1e1; border-radius: 8px; overflow: hidden; box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1); transition: transform 0.3s ease, box-shadow 0.3s ease;">
    <div class="card-header" style="background-color: #f5f5f5; padding: 15px 20px; border-bottom: 1px solid #e1e1e1;">
      <h3>Automação de Fluxo de Trabalho</h3>
    </div>
    <div class="card-body" style="padding: 20px; background-color: #ffffff;">
      <p>Automatizar processos de negócios envolvendo formulários e documentos:</p>
      <ul>
        <li><a href="https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/forms/create-form-centric-workflows/aem-forms-workflow-step-reference#assign-task-step">Criar processos comerciais</a> - Encaminhar formulários para aprovação ou feedback, fluxos de trabalho pós-envio ou fluxos de trabalho de back-end para gerenciar processos de inscrição</li>
        <li><a href="https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/forms/create-form-centric-workflows/aem-forms-workflow-step-reference#sign-document-step">Usar o Adobe Sign em um fluxo de trabalho do AEM</a> - Enviar um documento para assinatura </li>
        <li><a href="https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/forms/create-form-centric-workflows/aem-forms-workflow-step-reference#generate-document-of-record-step">Gerar um Documento de Registro </a> - Gerar sob demanda ou no envio de formulário</li>
      </ul>
    </div>
  </div>

<div class="card" style="flex: 1 1 calc(50% - 20px); min-width: 300px; border: 1px solid #e1e1e1; border-radius: 8px; overflow: hidden; box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1); transition: transform 0.3s ease, box-shadow 0.3s ease;">
    <div class="card-header" style="background-color: #f5f5f5; padding: 15px 20px; border-bottom: 1px solid #e1e1e1;">
      <h3>Assinaturas eletrônicas</h3>
    </div>
    <div class="card-body" style="padding: 20px; background-color: #ffffff;">
      <p>Adicione assinaturas eletrônicas juridicamente vinculativas aos seus formulários e documentos:</p>
      <ul>
        <li><a href="https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/forms/integrate/services/adobe-sign-integration-adaptive-forms">Integração do Adobe Sign</a> - Habilitar assinaturas eletrônicas no Adaptive Forms</li>
        <li><a href="https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/forms/create-form-centric-workflows/aem-forms-workflow-step-reference#sign-document-step">Adicionar Assinaturas Eletrônicas a Fluxos de Trabalho</a> - Incluir etapas de assinatura em processos comerciais</li>
        <li><a href="https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/forms/create-form-centric-workflows/aem-forms-workflow-step-reference#generate-document-of-record-step">Documento de registro com assinaturas</a> - Gerar registros assinados de envios de formulários</li>
      </ul>
    </div>
  </div>

<div class="card" style="flex: 1 1 calc(50% - 20px); min-width: 300px; border: 1px solid #e1e1e1; border-radius: 8px; overflow: hidden; box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1); transition: transform 0.3s ease, box-shadow 0.3s ease;">
    <div class="card-header" style="background-color: #f5f5f5; padding: 15px 20px; border-bottom: 1px solid #e1e1e1;">
      <h3>Analytics e Insights</h3>
    </div>
    <div class="card-body" style="padding: 20px; background-color: #ffffff;">
      <p>Obtenha insights sobre o uso e o desempenho do formulário:</p>
      <ul>
        <li><a href="https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/forms/integrate/services/enable-adobe-analytics-adaptive-form-using-experience-cloud-setup-automation">Habilitar Adobe Analytics</a> - Rastrear o uso e o desempenho do formulário</li>
        <li><a href="https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/forms/integrate/services/integrate-aem-forms-with-adobe-analytics">Integração manual do Analytics</a> - Configurar análises para acompanhamento detalhado</li>
        <li><a href="https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/forms/integrate/services/view-understand-aem-forms-analytics-reports">Exibir relatórios do Analytics</a> - Analisar o desempenho do formulário e o comportamento do usuário</li>
      </ul>
    </div>
  </div>

<div class="card" style="flex: 1 1 calc(50% - 20px); min-width: 300px; border: 1px solid #e1e1e1; border-radius: 8px; overflow: hidden; box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1); transition: transform 0.3s ease, box-shadow 0.3s ease;">
    <div class="card-header" style="background-color: #f5f5f5; padding: 15px 20px; border-bottom: 1px solid #e1e1e1;">
      <h3>Integração de dados</h3>
    </div>
    <div class="card-body" style="padding: 20px; background-color: #ffffff;">
      <p>Conecte formulários às suas fontes de dados e sistemas existentes:</p>
      <h4>Ecossistema do Adobe</h4>
      <ul>
        <li><a href="https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/use-adobe-sign/working-with-adobe-sign">Adobe Sign</a> - Enviar para assinaturas eletrônicas via Adobe Sign</li>
        <li><a href="https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/forms/integrate/services/integrate-adaptive-form-with-market-engage/integrate-form-to-marketo-engage">Marketo Engage</a> - Integrar formulários com o Adobe Marketo Engage</li>
        <li><a href="https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions#invoke-an-aem-workflow">Fluxo de trabalho do AEM</a> - Acione fluxos de trabalho do AEM com envios de formulários</li>
        <li><a href="https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions#workfront-fusion">Workfront</a> - Enviar um Formulário adaptável ao Adobe Workfront Fusion</li>
      </ul>
      <h4>Integrações do Microsoft</h4>
      <ul>
        <li><a href="https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/configure-msdynamics">Microsoft Dynamics 365</a> - Integrar ao CRM da Microsoft</li>
        <li><a href="https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/configure-azure-storage">Armazenamento Azure Blob</a> - Armazene dados de formulário no armazenamento na nuvem da Microsoft</li>
        <li><a href="https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/connect-to-sharepoint/connect-forms-to-sharepoint-document-library">Biblioteca de documentos do SharePoint</a> - Conecte-se às bibliotecas de documentos do Microsoft SharePoint</li>
        <li><a href="https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions#connect-af-sharepoint-list">Lista do SharePoint</a> - Conectar à lista do Microsoft SharePoint</li>
        <li><a href="https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions#submit-to-onedrive">OneDrive</a> - Conectar ao Microsoft OneDrive</li>
        <li><a href="https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/forms/integrate/services/forms-microsoft-power-automate-integration">Microsoft Power Automate</a> - Acionar fluxos do Microsoft Power Automate</li>
      </ul>
      <h4>Outras fontes de dados e serviços</h4>
      <ul>
        <li><a href="https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/aem-forms-salesforce-integration">Salesforce</a> - Integrar ao Salesforce CRM</li>
        <li><a href="https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions#submit-to-rest-endpoint">Serviços RESTful</a> - Conectar a qualquer ponto de extremidade de API REST</li>
        <li><a href="https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/configure-data-sources">Bancos de Dados RDBMS</a> - Conectar a bancos de dados relacionais</li>
        <li><a href="https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions#send-email">Email</a> - Enviar dados de formulário por email</li>
        <li><a href="https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/introduction-to-forms-portal/save-core-component-based-form-as-draft">Portal do Forms</a> - Enviar para o Portal do Forms para salvar rascunho</li>
        <li><a href="https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions#send-pdf-via-email">Enviar PDF por email</a> - Enviar por email uma versão PDF do formulário enviado</li>
        <li><a href="https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions#submit-using-form-data-model">Enviar usando o Modelo de dados de formulário</a> - Enviar dados usando um Modelo de dados de formulário</li>
      </ul>
    </div>
  </div>
</div>

## Introdução ao AEM Forms as a Cloud Service

<div class="card-container" style="display: flex; flex-wrap: wrap; gap: 20px; margin-bottom: 30px;">
  <div class="card" style="flex: 1 1 calc(50% - 20px); min-width: 300px; border: 1px solid #e1e1e1; border-radius: 8px; overflow: hidden; box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1); transition: transform 0.3s ease, box-shadow 0.3s ease;">
    <div class="card-header" style="background-color: #f5f5f5; padding: 15px 20px; border-bottom: 1px solid #e1e1e1;">
      <h3>Para usuários empresariais</h3>
    </div>
    <div class="card-body" style="padding: 20px; background-color: #ffffff;">
      <ol style="margin-top: 10px; padding-left: 25px;">
        <li style="margin-bottom: 8px;"><strong>Entenda as noções básicas</strong>: saiba mais sobre o <a href="https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/creating-adaptive-form-core-components">Forms adaptável</a> e como ele pode ajudar a digitalizar seus processos comerciais.</li>
        <li style="margin-bottom: 8px;"><strong>Explorar modelos</strong>: navegue pelos <a href="https://experienceleague.adobe.com/pt-br/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components">modelos e temas pré-criados</a> para obter uma vantagem inicial sobre os projetos de formulário.</li>
        <li style="margin-bottom: 8px;"><strong>Saiba mais sobre criação de formulários</strong>: siga o <a href="https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-an-adaptive-form-on-forms-cs/introduction-forms-authoring">guia de criação de formulários</a> para criar seu primeiro formulário.</li>
      </ol>
    </div>
  </div>

<div class="card" style="flex: 1 1 calc(50% - 20px); min-width: 300px; border: 1px solid #e1e1e1; border-radius: 8px; overflow: hidden; box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1); transition: transform 0.3s ease, box-shadow 0.3s ease;">
    <div class="card-header" style="background-color: #f5f5f5; padding: 15px 20px; border-bottom: 1px solid #e1e1e1;">
      <h3>Para desenvolvedores</h3>
    </div>
    <div class="card-body" style="padding: 20px; background-color: #ffffff;">
      <ol style="margin-top: 10px; padding-left: 25px;">
        <li style="margin-bottom: 8px;"><strong>Configurar o ambiente</strong>: Configurar o <a href="https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/forms/setup-configure-migrate/setup-local-development-environment">ambiente de desenvolvimento local</a> para o AEM Forms.</li>
        <li style="margin-bottom: 8px;"><strong>Saiba mais sobre a arquitetura</strong>: entenda a <a href="https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/forms/forms-overview/aem-forms-cloud-service-architecture">arquitetura do AEM Forms as a Cloud Service</a>.</li>
        <li style="margin-bottom: 8px;"><strong>Explorar APIs</strong>: familiarize-se com <a href="https://developer-stage.adobe.com/experience-cloud/experience-manager-apis/api/stable/forms/"> as APIs </a> e SDKs disponíveis para estender e integrar o Forms.</li>
      </ol>
    </div>
  </div>

<div class="card" style="flex: 1 1 calc(50% - 20px); min-width: 300px; border: 1px solid #e1e1e1; border-radius: 8px; overflow: hidden; box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1); transition: transform 0.3s ease, box-shadow 0.3s ease;">
    <div class="card-header" style="background-color: #f5f5f5; padding: 15px 20px; border-bottom: 1px solid #e1e1e1;">
      <h3>Para administradores</h3>
    </div>
    <div class="card-body" style="padding: 20px; background-color: #ffffff;">
      <ol style="margin-top: 10px; padding-left: 25px;">
        <li style="margin-bottom: 8px;"><strong>Integrar no Cloud Service</strong>: siga o <a href="https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/forms/setup-configure-migrate/setup-forms-cloud-service">guia de integração</a> para configurar o AEM Forms as a Cloud Service.</li>
        <li style="margin-bottom: 8px;"><strong>Configurar serviços</strong>: configurar <a href="https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/forms/integrate/services/enable-adobe-analytics-adaptive-form-using-experience-cloud-setup-automation">integrações com outros serviços da Adobe</a>, como o Adobe Analytics.</li>
        <li style="margin-bottom: 8px;"><strong>Migrar do AEM 6.5</strong>: se você vem do AEM 6.5, siga o <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/setup-configure-migrate/migrate-to-forms-as-a-cloud-service.html?lang=pt-BR">guia de migração</a> para migrar para o Cloud Service.</li>
      </ol>
    </div>
  </div>
</div>

## Recursos iniciais do adotante

<div class="card" style="flex: 1 1 calc(50% - 20px); min-width: 300px; border: 1px solid #e1e1e1; border-radius: 8px; overflow: hidden; box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1); transition: transform 0.3s ease, box-shadow 0.3s ease; margin-bottom: 30px;">
  <div class="card-header" style="background-color: #f5f5f5; padding: 15px 20px; border-bottom: 1px solid #e1e1e1;">
    <h3>Programa de acesso antecipado do AEM Forms</h3>
  </div>
  <div class="card-body" style="padding: 20px; background-color: #ffffff;">
    <p>O <a href="https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/forms/forms-overview/early-access-ea-features">Programa de Acesso Antecipado do AEM Forms</a> oferece acesso exclusivo a recursos de última geração antes de serem disponibilizados, incluindo:</p>
    <ul style="margin-top: 10px; padding-left: 25px;">
      <li style="margin-bottom: 8px;"><strong>Assistente do AEM Forms AI (Gen AI)</strong> - Crie formulários mais rápido com sugestões alimentadas por IA</li>
      <li style="margin-bottom: 8px;"><strong>AEM Forms Workfront Fusion Connector</strong> - Automatize fluxos de trabalho acionados por envios de formulários</li>
      <li style="margin-bottom: 8px;"><strong>Forms de conversa</strong> - Crie experiências de formulário com estilo de chat em qualquer página do AEM Sites</li>
      <li style="margin-bottom: 8px;"><strong>Criação do WYSIWYG para Edge Delivery</strong> - Crie formulários com o Editor Universal para Edge Delivery Services</li>
      <li style="margin-bottom: 8px;"><strong>Conector do AEM Forms para Marketo</strong> - Integrar envios de formulários com o Marketo Engage</li>
    </ul>
    <p>Para obter uma lista completa das inovações de acesso antecipado e a documentação detalhada, visite a <a href="https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/forms/forms-overview/early-access-ea-features">página do Programa de Acesso Antecipado do AEM Forms</a>.</p>
  </div>
</div>

<div style="background-color: #f0f7ff; border-left: 4px solid #1473e6; padding: 20px; margin: 30px 0; border-radius: 4px;">
  <h3 style="margin-top: 0; color: #1473e6;">Pronto para começar?</h3>
  <p><a href="https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/forms/setup-configure-migrate/setup-forms-cloud-service" style="font-weight: bold; color: #1473e6;">Integre o AEM Forms as a Cloud Service</a> hoje e transforme a experiência de formulários digitais de sua organização.</p>
</div>
