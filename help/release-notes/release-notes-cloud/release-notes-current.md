---
title: Notas de versão atuais do  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Notas de versão atuais para  [!DNL Adobe Experience Manager] as a Cloud Service.
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: d424b6f2e0a2ec40ab607dcbdcba3120c7f45a58
workflow-type: tm+mt
source-wordcount: '1778'
ht-degree: 9%

---

# Notas de versão atuais do [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

A seção a seguir descreve as notas da versão de recurso atual (mais recente) do [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>A partir desta seção, você pode navegar até as notas das versões anteriores, como as de 2022 ou 2023.
>
>Dê uma olhada no [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para saber mais sobre as próximas ativações de recursos do [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Para receber uma notificação por email mensal sobre atualizações nas notas de versão do Experience Cloud, assine a [Atualização de Produto Prioritária do Adobe](https://www.adobe.com/subscription/priority-product-update.html).

## Data de lançamento {#release-date}

A data de lançamento da versão atual (2024.11.0) do [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] é sexta-feira, 21 de novembro de 2024. O próximo lançamento de recursos (2025.1.0) está planejado para quarta-feira, 30 de janeiro de 2024.

## Notas da versão de manutenção {#maintenance}

Encontre as notas de versão de manutenção mais recentes [aqui](/help/release-notes/maintenance/latest.md).

<!-- ## Release Video {#release-video}

Have a look at the November 2024 Release Overview video for a summary of the features added in the 2024.11.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3434847?quality=12)

-->

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

**[!DNL Edge Delivery Services]modelos de página com criação no Editor Universal**

Transforme rapidamente qualquer página do Edge Delivery em um modelo de página. Isso permite iniciar uma nova página com uma estrutura e conteúdo predefinidos, em vez de uma página em branco. [Leia mais](/help/sites-cloud/authoring/universal-editor/templates.md).

**[!DNL Edge Delivery Services]Importador de CSV para publicação via instância AEM**

Gerencie seus dados de planilha do Edge Delivery (por exemplo, redirecionamentos) com eficiência em sua ferramenta de planilha favorita e faça upload para o AEM por meio do novo importador de CSV. [Leia mais](/help/edge/wysiwyg-authoring/tabular-data.md#importing).

### Recursos de pré-lançamento no AEM Sites

[Referência de fragmento de conteúdo aprimorada com referências exclusivas baseadas em ID](/help/headless/graphql-api/uuid-reference-upgrade.md), garantindo links estáveis que permaneçam válidos mesmo quando ativos ou fragmentos forem movidos, eliminando a necessidade de atualizações ou republicação. Limitação atual: as referências de página ainda não são compatíveis com IDs exclusivas. Se as páginas forem referenciadas em Fragmentos de conteúdo, esse recurso não deverá ser usado.

### Programa de adoção antecipada {#sites-early-adopter}

AEM **OpenAPI REST para Entrega de Fragmento de Conteúdo**

A [OpenAPI REST para Entrega de Fragmento de Conteúdo](/help/headless/aem-rest-openapi-content-fragment-delivery.md) do AEM está disponível agora para o AEM as a Cloud Service.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Recursos de acesso antecipado no Dynamic Media {#dm-early-access}

**Legendas de vídeo geradas por IA**

Legendas de vídeo geradas por IA no Adobe Dynamic Media usam inteligência artificial para gerar legendas automaticamente para conteúdo de vídeo. Esse recurso foi projetado para melhorar a acessibilidade e a experiência do usuário, fornecendo legendas precisas e em tempo real. A IA analisa a faixa de áudio do vídeo para transcrever a fala e criar legendas, que podem ser editadas para precisão ou personalização. Essas legendas ajudam a atender aos requisitos de acessibilidade e melhorar o envolvimento com o vídeo para públicos-alvo que dependem ou preferem suporte de vídeo baseado em texto.

Para obter acesso antecipado ao suporte a legendas geradas por IA em sua conta da Dynamic Media, [crie e envie um caso de Suporte ao Cliente do Adobe](/help/assets/dynamic-media/video.md##enable-dash).

**Relatório de entrega do Dynamic Media**

Obtenha insights de entrega para ativos fornecidos com o Dynamic Media, com contagem de entrega no nível do ativo, informações do referenciador, caminho do ativo no AEM Assets e ID exclusiva do ativo. Os relatórios podem ser gerados para todos os ativos entregues por meio do Dynamic Media para o repositório do AEM Assets ou para uma hierarquia de pastas específica no AEM Assets. Os insights ajudam a medir o ROI dos ativos entregues, medir o desempenho do canal e a realizar tarefas informadas de gerenciamento de ativos para ativos.

Para obter acesso antecipado ao Relatório de Entrega da Dynamic Media em sua conta da Dynamic Media, [crie e envie um caso de Suporte ao Cliente Adobe](https://helpx.adobe.com/br/enterprise/using/support-for-experience-cloud.html).

### Novos recursos na visualização de ativos {#assets-view-new-features}

**painel do Dynamic Media**

A visualização do Assets agora permite que você acesse o Dynamic Media e o Dynamic Media com representações OpenAPI de um painel separado disponibilizado para você. Você pode optar por copiar o URL de entrega ou baixar as representações com base no ativo e no tipo de representação. Para obter mais informações, consulte [representações do Dynamic Media](/help/assets/renditions.md#dynamic-media-renditions) e [representações do Dynamic Media com recursos OpenAPI](/help/assets/renditions.md#dm-with-openapi-renditions).

![representações dinâmicas](/help/assets/assets/dm-scene7-renditions.png)

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Novos recursos no AEM Forms {#forms-new-features}

* **[Atualizar escopos do Adobe Sign facilmente](/help/forms/adobe-sign-integration-adaptive-forms.md)**: você pode modificar os escopos de uma configuração do Adobe Sign diretamente da página Configurações de Nuvem do AEM, tornando mais rápido e fácil atualizar as configurações existentes.

* **[Suporte a função assíncrona para Forms Adaptável](/help/forms/using-async-funct-in-rule-editor.md)**: quando o Formulário Adaptável requer operações assíncronas, como aguardar processos externos ou recuperação de dados, você pode implementar essas operações com funções personalizadas e configurá-las no Editor de Regras.

### Recursos de pré-lançamento no AEM Forms {#forms-new-prerelease-features}

* **Gerenciar Publicação**: você pode usar o fluxo de trabalho Gerenciar Publicação para publicar ou desfazer a publicação de formulários entre ambientes, normalmente da instância de criação para as instâncias de publicação e visualização. Ele permite que os usuários publiquem, desfaçam a publicação ou agendem a publicação de conteúdo de maneira simplificada.

* **[Salvar automaticamente um rascunho para os Componentes principais com base no Forms adaptável](/help/forms/save-core-component-based-form-as-draft.md)**: os usuários agora podem se beneficiar de um recurso de salvamento automático que salva automaticamente um formulário parcialmente preenchido como rascunho. Eles podem retornar mais tarde para terminar de preenchê-lo no mesmo dispositivo ou em outro. Esse recurso melhora as taxas de conversão para organizações ao reduzir o abandono de formulário, pois os usuários não precisam começar novamente o preenchimento do formulário desde o início.

* **[Aprimoramentos do editor de regras](/help/forms/invoke-service-enhancements-rule-editor.md)**: para o Adaptive Forms com base em Componentes principais, você agora pode preencher opções suspensas usando a saída do Invoke Service, definir painéis repetíveis usando a saída do Invoke Service, definir painéis individuais usando a saída do Invoke Service e usar o parâmetro de saída do Invoke Service para validar outros campos.

* **[Aprimorar a Experiência do Usuário com Botões de Navegação em Layouts de Painel](/help/forms/rule-editor-core-components-usecases.md#navigating-among-panels-using-button)**: Agora é possível adicionar botões de navegação aos layouts de painel, como Guias Horizontais, Guias Verticais, Acordeões ou Assistente. Esses botões melhoram a experiência do usuário simplificando as transições entre painéis, com foco no painel selecionado.


### Recursos de acesso antecipado no AEM Forms {#forms-new-early-access-features}

O programa de acesso antecipado da AEM Forms oferece uma oportunidade única para você obter acesso exclusivo a inovações de última geração e ajudar a moldar seu desenvolvimento.

Estas notas de versão listam as inovações fornecidas na versão atual. Para obter a lista completa de inovações disponíveis no Programa de Acesso Antecipado, consulte a [documentação do Programa de Acesso Antecipado do AEM Forms](/help/forms/early-access-ea-features.md).

#### Integrações

* **[Integrar o Adaptive Forms com o Adobe Marketo Engage](/help/forms/integrate-form-to-marketo-engage.md)**: o AEM Forms as a Cloud Service inclui uma opção fácil de usar para conectar o Adaptive Forms com o Adobe Marketo Engage. Essa integração permite criar o Forms adaptável diretamente com a captura de leads Marketo Engage e objetos personalizados relacionados. Agora é possível preencher previamente os campos de formulário com dados do Marketo Engage e enviar os dados de volta para automatizar os fluxos de trabalho, como campanhas inteligentes e automação de email. Você também pode conectar um Formulário adaptável à biblioteca do Munchkin para rastrear o número de visitas, cliques e envios de formulários.

#### Forms adaptável e HTML5 Forms

* **[Criar Forms adaptável com base no modelo XFA existente](/help/forms/create-adaptive-form-using-xfa-templates.md)**: agora você pode criar Forms adaptável com base em Componentes principais usando modelos de formulário XFA (arquivos *.XDP). AEM Forms Esse recurso facilita a adoção da AEM Forms as a Cloud Service pelos clientes locais com investimentos existentes na tecnologia XFA.

* **HTML5 Forms (Formulários web baseados em XFA)**: agora, os clientes locais da AEM Forms que usam a tecnologia XFA podem fazer a transição para o AEM Forms sem esforço, as a Cloud Service preservando sua experiência de usuário existente com o HTML5 Forms (Formulários web baseados em XFA). Esse recurso permite a renderização de modelos de formulário XFA no formato HTML5, tornando os formulários acessíveis em dispositivos que não oferecem suporte a PDF forms baseados em XFA.

  ![HTML Forms (Formulários Web Baseados em XFA)](/help/forms/assets/html-forms-xfa-based-web-forms.png)


* Suporte a Cadeia de Caracteres Codificada em **[Base64 para Anexo de Arquivo](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/file-attachment#basic-tab)**: o componente Anexo de Arquivo no Forms Adaptável baseado em Componentes Principais agora inclui uma opção para enviar arquivos anexados como cadeias de caracteres codificadas em Base64.

#### APIs de comunicações interativas e comunicação

* **Editor de Comunicação Interativa**: o Editor de Comunicação Interativa é uma ferramenta de design de comunicação gráfica amigável que simplifica a criação de correspondências personalizadas orientadas por dados e é executado em qualquer navegador moderno. Ele oferece suporte à integração perfeita de dados, definição de lógica complexa e integração de mídia avançada, garantindo documentos profissionais e compatíveis, comunicação e geração de modelos para várias necessidades de negócios.

  ![Editor de Comunicação Interativa](/help/forms/assets/ic-editor.png)


* **[Aprimoramentos de conformidade com PDF/A](/help/forms/aem-forms-cloud-service-communications-introduction.md#convert-to-and-validate-pdfa-compliant-documents)**: agora você pode usar APIs de comunicação para converter documentos PDF para formatos PDF/A (1a, 2a, 3a) para fins de arquivamento, garantindo a acessibilidade e verificando a conformidade com esses padrões.


* **[API de assinatura (Document Assurance)](/help/forms/aem-forms-cloud-service-communications-introduction.md#document-assurance)**: uma nova API RESTful em APIs de comunicação permite um fácil gerenciamento de assinaturas de PDF. Ele oferece suporte a operações como:
   * Limpar assinatura: remove uma assinatura de um campo especificado.
   * Remover Campo de Assinatura: Deleta um campo de assinatura especificado.


<!-- 
* **Hamburger Menu Layout in Adaptive Forms**: Adaptive Forms now offers a responsive hamburger menu layout for mobile devices. This collapsible menu organizes form sections, making navigation more 
intuitive and improving the mobile form-filling experience.

* **Masked Field with Eye Icon (Password Box Component)**: The Password Box is a text input field that masks the characters typed into it by displaying placeholder symbols. It allows users to securely input sensitive information, such as passwords and enables them to toggle visibility on demand using the eye icon.

-->

## Serviço de conversão automática de formulários

* **[Converter PDF forms em Componentes principais com base na Forms adaptável](https://experienceleague.adobe.com/en/docs/aem-forms-automated-conversion-service/using/convert-existing-forms-to-adaptive-forms)**: agora você pode usar o Automated forms conversion Service para transformar PDF forms, AcroForms ou formulários baseados em XFA em Componentes principais com base na Forms adaptável.


>[!IMPORTANT]
>
> Interessado em participar do Programa de acesso antecipado para qualquer inovação da Forms? Envie um email de seu endereço oficial para [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) com a lista de recursos nos quais você está interessado.## Complemento CIF {#cloud-services-cif}

## Complemento CIF {#cif}

### Correções de erros {#bug-fixes-cif}

* Correção dos testes de interface do usuário para funcionarem corretamente com os componentes principais do CIF.
* Solução de um problema em que o formato de URL da categoria não funcionava como esperado na instância da nuvem.

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Melhor desempenho de replicação da árvore (e descontinuação do fluxo de trabalho da árvore de conteúdo do Publish) {#tree-replication-performance}

A [Etapa do Fluxo de Trabalho de Ativação da Árvore](/help/operations/replication.md#tree-activation) é uma nova etapa do modelo de fluxo de trabalho recomendada para replicar hierarquias de conteúdo profundo. É importante observar que ela permite que replicações independentes (por exemplo, por meio de publicação rápida ou gerenciamento de publicação) prossigam em paralelo ao fluxo de trabalho de replicação de árvore em andamento. Isso é particularmente útil se você precisar publicar conteúdo com detecção de tempo enquanto uma replicação em massa ainda estiver em andamento. A etapa Replicação de árvore substitui o Fluxo de trabalho da árvore de conteúdo do Publish e sua etapa do fluxo de trabalho relacionada, que agora estão obsoletos.

### APIs baseadas em OpenAPI - Early Adoter Program {#open-apis-earlyadopter}

Os desenvolvedores podem integrar profundamente os recursos do AEM as Cloud Service em seus próprios aplicativos e ferramentas. As novas APIs do AEM as a Cloud Service seguirão a especificação da OpenAPI, com o objetivo de serem consistentes, bem documentadas e fáceis de usar. As credenciais para endpoints que exigem autenticação serão geradas ao criar projetos do Adobe Developer Console.

Saiba mais sobre [APIs de AEM baseadas em OpenAPI](/help/implementing/developing/open-api-based-apis.md) e experimente um [tutorial completo](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/aem-apis/invoke-openapi-based-aem-apis) que ilustra a configuração e o uso.

Especificamente, os endpoints de API listados abaixo estão disponíveis como parte de um programa de adoção antecipada. Se estiver interessado, envie um email para [aem-apis@adobe.com](mailto:aem-apis@adobe.com) descrevendo como você pretende usá-los.
* [APIs de fragmentos de conteúdo do Sites](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/sites/)
* [APIs do Assets](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/assets/author/)
* [APIs de Sites e Pastas do Assets](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/folders/)
* [APIs de comunicações do Forms](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/)

### Computação Edge - Solicitação de feedback! {#edge-computing-feedback}

A computação Edge aproxima o processamento de dados do navegador, o que traz benefícios, inclusive latência reduzida. Como contribuição para o roteiro, adoraríamos saber se essa tecnologia seria útil para a entrega do AEM Publish e para os projetos Edge Delivery Services e para o que você prevê usá-la. Email [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com) com perguntas e comentários!

### Novo AEM Developer Console (Beta público) {#aem-developer-console-beta}

Experimente um [AEM Developer Console](/help/implementing/developing/introduction/aem-developer-console.md) renovado, que oferece uma experiência mais interativa para depurar código em ambientes na nuvem.

Qualquer pessoa pode acessar o beta público clicando no botão *Novo Console Disponível* no Developer Console AEM atual. O Adobe recebe o feedback, que você pode enviar para [aemcs-new-devconsole-ui-beta@adobe.com](mailto:aemcs-new-devconsole-ui-beta@adobe.com)

## Guias do [!DNL Experience Manager] {#guides}

Você pode encontrar uma lista completa de recursos novos e aprimorados da versão mais recente do Adobe Experience Manager Guides [aqui](https://experienceleague.adobe.com/en/docs/experience-manager-guides/using/release-info/release-notes/cloud-release-notes/2024-releases/2410-release/2410-0-release/whats-new-2024-10-0).

## Cloud Manager {#cloud-manager}

Você pode encontrar uma lista completa de versões mensais do Cloud Manager [aqui](/help/implementing/cloud-manager/release-notes/current.md).

## Ferramentas de migração {#migration-tools}

Você pode encontrar uma lista completa de versões das ferramentas de migração [aqui](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).

## Editor universal {#universal-editor}

Você pode encontrar uma lista completa de versões do Universal Editor [aqui](/help/release-notes/universal-editor/current.md).

## Gerar variações {#generate-variations}

Você pode encontrar uma lista completa de versões de Gerar Variações [aqui](/help/generative-ai/release-notes-generate-variations.md).

## Notas de versão da Experience Cloud {#experience-cloud}

Você pode encontrar informações sobre lançamentos de outros aplicativos Experience Cloud [aqui](https://experienceleague.adobe.com/pt-br/docs/release-notes/experience-cloud/current).
