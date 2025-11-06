---
title: Notas de versão do  [!DNL Adobe Experience Manager]  as a Cloud Service 2024.11.0.
description: Notas de versão do  [!DNL Adobe Experience Manager]  as a Cloud Service 2024.11.0.
feature: Release Information
role: Admin
exl-id: 3fd6482e-66f0-48ee-983c-4cb6b7742dcd
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1810'
ht-degree: 11%

---

# Notas de versão do [!DNL Adobe Experience Manager] as a Cloud Service 2024.11.0 {#release-notes}

A seção a seguir descreve as notas da versão de recursos do [!DNL Experience Manager] as a Cloud Service 2024.11.0.

>[!NOTE]
>
>A partir desta seção, você pode navegar até as notas das versões anteriores, como as de 2022 ou 2023.
>
>Dê uma olhada no [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/pt-br/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para saber mais sobre as próximas ativações de recursos do [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Para receber uma notificação por email mensal sobre atualizações nas notas de versão do Experience Cloud, assine a [Atualização prioritária de produto da Adobe](https://www.adobe.com/subscription/priority-product-update.html).

## Data de lançamento {#release-date}

A data de lançamento da versão atual (2024.11.0) do [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] é sexta-feira, 21 de novembro de 2024. O próximo lançamento de recursos (2025.1.0) está planejado para sexta-feira, 30 de janeiro de 2025.

## Notas da versão de manutenção {#maintenance}

Encontre as notas de versão de manutenção mais recentes [aqui](/help/release-notes/maintenance/latest.md).

## Vídeo da versão {#release-video}

Assista ao vídeo Visão geral da versão de novembro de 2024 que exibe um resumo dos recursos adicionados na versão 2024.11.0:

>[!VIDEO](https://video.tv.adobe.com/v/3440920?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

**[!DNL Edge Delivery Services]modelos de página com criação no Editor Universal**

Transforme rapidamente qualquer página do Edge Delivery em um modelo de página. Isso permite iniciar uma nova página com uma estrutura e conteúdo predefinidos, em vez de uma página em branco. [Leia mais](/help/sites-cloud/authoring/universal-editor/templates.md).

**[!DNL Edge Delivery Services]Importador de CSV para publicação através de uma instância do AEM**

Gerencie seus dados de planilha do Edge Delivery (por exemplo, redirecionamentos) com eficiência em sua ferramenta de planilha favorita e faça upload deles para a AEM por meio do novo importador de CSV. [Leia mais](https://www.aem.live/docs/authoring-tabular-data).

### Recursos de pré-lançamento no AEM Sites

[Referência de fragmento de conteúdo aprimorada com referências exclusivas baseadas em ID](/help/headless/graphql-api/uuid-reference-upgrade.md), garantindo links estáveis que permaneçam válidos mesmo quando ativos ou fragmentos forem movidos, eliminando a necessidade de atualizações ou republicação. Limitação atual: as referências de página ainda não são compatíveis com IDs exclusivas. Se as páginas forem referenciadas em Fragmentos de conteúdo, esse recurso não deverá ser usado.

### Programa de adoção antecipada {#sites-early-adopter}

**OpenAPI REST do AEM para entrega de fragmentos de conteúdo**

A [OpenAPI REST do AEM para Entrega de Fragmento de Conteúdo](/help/headless/aem-content-fragment-delivery-with-openapi.md) está disponível agora para o AEM as a Cloud Service.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Recursos de acesso antecipado no Dynamic Media {#dm-early-access}

**Legendas de vídeo geradas por IA**

Legendas de vídeo geradas por IA no Adobe Dynamic Media usam inteligência artificial para gerar legendas automaticamente para conteúdo de vídeo. Esse recurso foi projetado para melhorar a acessibilidade e a experiência do usuário, fornecendo legendas precisas e em tempo real. A IA analisa a faixa de áudio do vídeo para transcrever a fala e criar legendas, que podem ser editadas para precisão ou personalização. Essas legendas ajudam a atender aos requisitos de acessibilidade e melhorar o envolvimento com o vídeo para públicos-alvo que dependem ou preferem suporte de vídeo baseado em texto.

Para obter acesso antecipado ao suporte a legendas geradas por IA em sua conta do Dynamic Media, [crie e envie um caso de Suporte ao Cliente da Adobe](/help/assets/dynamic-media/video.md##enable-dash).

**Relatório de entrega do Dynamic Media**

Obtenha insights de entrega para ativos entregues com o Dynamic Media, com contagem de entregas no nível do ativo, informações do referenciador, caminho do ativo no AEM Assets e ID exclusiva do ativo. Os relatórios podem ser gerados para todos os ativos entregues por meio do Dynamic Media para o repositório do AEM Assets ou para uma hierarquia de pastas específica no AEM Assets. Os insights ajudam a medir o ROI dos ativos entregues, medir o desempenho do canal e a realizar tarefas informadas de gerenciamento de ativos para ativos.

Para obter acesso antecipado ao Relatório de Entrega do Dynamic Media na sua conta do Dynamic Media, [crie e envie um caso de Suporte ao Cliente da Adobe](https://helpx.adobe.com/br/enterprise/using/support-for-experience-cloud.html).

### Novos recursos na visualização de ativos {#assets-view-new-features}

**Painel do Dynamic Media**

A exibição do Assets agora permite acessar o Dynamic Media e o Dynamic Media com representações OpenAPI de um painel separado disponibilizado para você. Você pode optar por copiar o URL de entrega ou baixar as representações com base no ativo e no tipo de representação. Para obter mais informações, consulte [representações do Dynamic Media](/help/assets/renditions.md#dynamic-media-renditions) e [Dynamic Media com representações de recursos OpenAPI](/help/assets/renditions.md#dm-with-openapi-renditions).

![representações dinâmicas](/help/assets/assets/dm-scene7-renditions.png)

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Novos recursos no AEM Forms {#forms-new-features}

* **[Atualize facilmente os escopos do Adobe Sign](/help/forms/adobe-sign-integration-adaptive-forms.md)**: você pode modificar os escopos de uma configuração do Adobe Sign diretamente da página Configurações de nuvem do AEM, tornando mais rápido e fácil atualizar as configurações existentes.

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

* **[Integrar o Adaptive Forms com o Adobe Marketo Engage](/help/forms/integrate-form-to-marketo-engage.md)**: o AEM Forms as a Cloud Service agora inclui uma opção fácil de usar para conectar o Adaptive Forms com o Adobe Marketo Engage. Essa integração permite criar o Adaptive Forms diretamente com a captura de leads da Marketo Engage e objetos personalizados relacionados. Agora é possível preencher previamente os campos de formulário com dados do Marketo Engage e enviar os dados de volta para automatizar os fluxos de trabalho, como campanhas inteligentes e automação de email. Você também pode conectar um Formulário adaptável à biblioteca do Munchkin para rastrear o número de visitas, cliques e envios de formulários.

#### Forms adaptável e HTML5 Forms

* **[Criar Forms adaptável com base no modelo XFA existente](/help/forms/create-adaptive-form-using-xfa-templates.md)**: agora você pode criar Forms adaptável com base em Componentes principais usando modelos de formulário XFA (arquivos *.XDP). AEM Forms Esse recurso facilita a adoção do AEM Forms as a Cloud Service por clientes locais com investimentos existentes na tecnologia XFA.

* **HTML5 Forms (Formulários Web baseados em XFA)**: agora, os clientes locais da AEM Forms que usam a tecnologia XFA podem fazer a transição para o AEM Forms as a Cloud Service sem esforço, preservando a experiência do usuário existente com o HTML5 Forms (Formulários Web baseados em XFA). Esse recurso permite a renderização de modelos de formulário XFA no formato HTML5, tornando os formulários acessíveis em dispositivos que não oferecem suporte para PDF forms baseado em XFA.

  ![HTML Forms (Formulários Web baseados em XFA)](/help/forms/assets/html-forms-xfa-based-web-forms.png)


* Suporte a Cadeia de Caracteres Codificada em **[Base64 para Anexo de Arquivo](https://experienceleague.adobe.com/pt-br/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/file-attachment#basic-tab)**: o componente Anexo de Arquivo no Forms Adaptável baseado em Componentes Principais agora inclui uma opção para enviar arquivos anexados como cadeias de caracteres codificadas em Base64.

#### APIs de comunicações interativas e comunicação

* **Editor de Comunicação Interativa**: o Editor de Comunicação Interativa é uma ferramenta de design de comunicação gráfica amigável que simplifica a criação de correspondências personalizadas orientadas por dados e é executado em qualquer navegador moderno. Ele oferece suporte à integração perfeita de dados, definição de lógica complexa e integração de mídia avançada, garantindo documentos profissionais e compatíveis, comunicação e geração de modelos para várias necessidades de negócios.

  ![Editor de Comunicação Interativa](/help/forms/assets/ic-editor.png)


* **[Aprimoramentos de conformidade do PDF/A](/help/forms/aem-forms-cloud-service-communications-introduction.md#convert-to-and-validate-pdfa-compliant-documents)**: agora você pode usar APIs de comunicação para converter documentos do PDF para formatos do PDF/A (1a, 2a, 3a) para fins de arquivamento, garantindo a acessibilidade e verificando a conformidade com esses padrões.


* **[API de assinatura (Document Assurance)](/help/forms/aem-forms-cloud-service-communications-introduction.md#document-assurance)**: uma nova API RESTful em APIs de comunicação permite um fácil gerenciamento de assinaturas PDF. Ele oferece suporte a operações como:
   * Limpar assinatura: remove uma assinatura de um campo especificado.
   * Remover Campo de Assinatura: Deleta um campo de assinatura especificado.

<!-- 
* **Hamburger Menu Layout in Adaptive Forms**: Adaptive Forms now offers a responsive hamburger menu layout for mobile devices. This collapsible menu organizes form sections, making navigation more 
intuitive and improving the mobile form-filling experience.

* **Masked Field with Eye Icon (Password Box Component)**: The Password Box is a text input field that masks the characters typed into it by displaying placeholder symbols. It allows users to securely input sensitive information, such as passwords and enables them to toggle visibility on demand using the eye icon.

-->

## Serviço de conversão automática de formulários

* **[Converter o PDF forms em Componentes principais com base no Forms Adaptável](https://experienceleague.adobe.com/pt-br/docs/aem-forms-automated-conversion-service/using/convert-existing-forms-to-adaptive-forms)**: agora você pode usar o Serviço de Conversão Automatizada de Formulários para transformar formulários do PDF forms, AcroForms ou baseados em XFA em formulários do Forms Adaptável com base nos Componentes principais.

>[!IMPORTANT]
>
> Interessado em participar do Programa de acesso antecipado para qualquer inovação da Forms? Envie um email de seu endereço oficial para [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) com a lista de recursos nos quais você está interessado.## Complemento do CIF {#cloud-services-cif}

## Complemento CIF {#cif}

### Correções de erros {#bug-fixes-cif}

* Correção dos testes de interface do usuário para funcionarem corretamente com componentes principais do CIF.
* Solução de um problema em que o formato de URL da categoria não funcionava como esperado na instância da nuvem.

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Melhor desempenho de replicação da árvore (e descontinuação do fluxo de trabalho de publicação da árvore de conteúdo) {#tree-replication-performance}

A [Etapa do Fluxo de Trabalho de Ativação da Árvore](/help/operations/replication.md#tree-activation) é uma nova etapa do modelo de fluxo de trabalho recomendada para replicar hierarquias de conteúdo profundo. É importante observar que ela permite que replicações independentes (por exemplo, por meio de publicação rápida ou gerenciamento de publicação) prossigam em paralelo ao fluxo de trabalho de replicação de árvore em andamento. Isso é particularmente útil se você precisar publicar conteúdo com detecção de tempo enquanto uma replicação em massa ainda estiver em andamento. A Etapa de replicação da árvore substitui o Fluxo de trabalho da árvore de conteúdo de publicação e sua Etapa de fluxo de trabalho relacionada, que agora estão obsoletos.

### APIs baseadas em OpenAPI - Early Adoter Program {#open-apis-earlyadopter}

Os desenvolvedores podem integrar profundamente os recursos do AEM as Cloud Service em seus próprios aplicativos e ferramentas. As novas APIs do AEM as a Cloud Service seguirão a especificação da OpenAPI, com o objetivo de serem consistentes, bem documentadas e fáceis de usar. As credenciais para endpoints que exigem autenticação serão geradas ao criar projetos do Adobe Developer Console.

Saiba mais sobre as [APIs do AEM baseadas em OpenAPI](/help/implementing/developing/open-api-based-apis.md) e experimente um [tutorial completo](https://experienceleague.adobe.com/pt-br/docs/experience-manager-learn/cloud-service/aem-apis/invoke-openapi-based-aem-apis) que ilustra a configuração e o uso.

Especificamente, os endpoints de API listados abaixo estão disponíveis como parte de um programa de adoção antecipada. Se estiver interessado, envie um email para [aem-apis@adobe.com](mailto:aem-apis@adobe.com) descrevendo como você pretende usá-los.

* [APIs de fragmentos de conteúdo do Sites](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/sites/)
* [APIs do Assets](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/assets/author/)
* APIs de pastas de sites e Assets
* [APIs de comunicações do Forms](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/)

### Computação Edge - Solicitação de feedback! {#edge-computing-feedback}

A computação Edge aproxima o processamento de dados do navegador, o que traz benefícios, inclusive latência reduzida. Como entrada no roteiro, adoraríamos saber se você acharia essa tecnologia útil para a entrega de publicações do AEM e para os projetos do Edge Delivery Services, e para que você imagina usá-la. Email [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com) com perguntas e comentários!

### Novo AEM Developer Console (Beta público) {#aem-developer-console-beta}

Experimente um [AEM Developer Console](/help/implementing/developing/introduction/aem-developer-console.md) renovado, que oferece uma experiência mais interativa para depurar código em ambientes na nuvem.

Qualquer pessoa pode acessar o beta público clicando no botão *Novo Console Disponível* no Developer Console do AEM atual. A Adobe agradece o feedback, que você pode enviar por email para [aemcs-new-devconsole-ui-beta@adobe.com](mailto:aemcs-new-devconsole-ui-beta@adobe.com)

## Guias do [!DNL Experience Manager] {#guides}

Você pode encontrar uma lista completa de recursos novos e aprimorados da versão mais recente do Adobe Experience Manager Guides [aqui](https://experienceleague.adobe.com/pt-br/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap).

## Cloud Manager {#cloud-manager}

Você pode encontrar uma lista completa de versões mensais do Cloud Manager [aqui](/help/implementing/cloud-manager/release-notes/current.md).

## Ferramentas de migração {#migration-tools}

Você pode encontrar uma lista completa de versões das ferramentas de migração [aqui](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).

## Editor universal {#universal-editor}

Você pode encontrar uma lista completa de versões do Universal Editor [aqui](/help/release-notes/universal-editor/current.md).

## Gerar variações {#generate-variations}

Você pode encontrar uma lista completa de versões de Gerar Variações [aqui](/help/generative-ai/release-notes-generate-variations.md).

## Notas de versão da Experience Cloud {#experience-cloud}

Você pode encontrar informações sobre versões de outros aplicativos da Experience Cloud [aqui](https://experienceleague.adobe.com/pt-br/docs/release-notes/experience-cloud/current).
