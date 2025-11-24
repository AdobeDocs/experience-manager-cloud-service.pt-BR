---
title: APIs de comunicações do AEM Forms - Visão geral
description: Visão geral das APIs de comunicações do AEM Forms, incluindo métodos de autenticação e referência completa da API
role: Developer, User
feature: Adaptive Forms, APIs & Integrations
hide: true
hidefromtoc: true
index: false
source-git-commit: 580d6505ffdf25f7bfb3a3a84f054dcf76c05cdd
workflow-type: tm+mt
source-wordcount: '1098'
ht-degree: 4%

---


# APIs de comunicações do AEM Forms - Visão geral

As APIs de comunicação da AEM Forms fornecem um conjunto abrangente de APIs nativas em nuvem criadas para ajudar as empresas a automatizar fluxos de trabalho de documentos.

As APIs do AEM Forms são estruturadas e acessadas por meio de dois consoles principais:

* [Adobe Developer Console (ADC)](https://developer.adobe.com/developer-console/) - O Adobe Developer Console é o gateway para APIs, Eventos, Tempo de Execução e App Builder da Adobe.

* [AEM Developer Console](https://experienceleague.adobe.com/pt-br/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console) - O AEM Developer Console fornece ferramentas para depurar e inspecionar ambientes AEM as a Cloud Service.

Cada console fornece acesso a diferentes APIs e serviços para tarefas de processamento, geração, conversão, criptografia e comunicação de documentos. As APIs oferecem suporte a [métodos de autenticação](#authentication-methods) diferentes.

## Métodos de autenticação

As APIs oferecem suporte a vários métodos de autenticação para uma integração segura entre seus aplicativos e serviços da Adobe:

| Aspecto | Servidor para servidor OAuth (recomendado) | JWT (JSON Web Token) |
|-------------|------------------------------------------|---------------------------|
| Descrição | Método moderno e seguro para acesso à API sem interação com o usuário. | Método mais antigo usando tokens assinados para acesso. |
| Local da configuração | ADOBE DEVELOPER CONSOLE e AEM DEVELOPER CONSOLE | Somente AEM Developer Console |
| Segurança | Alto - usa credenciais e escopos do cliente | Moderado - depende do gerenciamento de chaves |
| Escalabilidade | Altamente escalável para integrações de back-end | Limitado, adequado para uso herdado |
| Gerenciamento de token | Geração e renovação automáticas | Rotação e assinatura manual dos tokens |
| Status | Recomendado | Obsoleto |


>[!NOTE]
>
> Clique nos links abaixo para saber mais sobre :-
> 
> * [Servidor a servidor OAuth (Recomendado)](/help/forms/oauth-api-authetication.md)
> * [JWT (JSON Web Token)](/help/forms/jwt-api-authentication.md)

<!--### Execution Models

The following table highlights the key differences between Synchronous (On-Demand) and Asynchronous (Batch) execution models supported in AEM Forms Communications APIs:

| Feature | Synchronous (On-Demand) | Batch (Asynchronous) |
|---------|-------------------------|----------------------|
| **Execution Model** | Real-time, immediate | Queued, scheduled |
| **Response Time** | Seconds | Minutes to hours |
| **Volume** | Single or few documents | Hundreds to thousands |
| **Testing Environment** | Author & Publish | Author Only |
| **Use Case** | User-triggered actions | Scheduled bulk operations |
| **Console Access** | ADC & AEM Developer Console | AEM Developer Console Only |-->

## Visão geral da classificação de API

Todas as APIs do AEM Forms estão divididas em duas partes principais:

* [APIs de entrega e tempo de execução de formulários adaptáveis](https://developer-stage.adobe.com/experience-cloud/experience-manager-apis/api/stable/forms/)

* [APIs de comunicação do AEM Forms](#aem-forms-communications-apis)

| Detalhes | APIs de entrega e tempo de execução de formulários adaptáveis | APIs de comunicação |
|--------------|----------------------------|--------------------------|
| Propósito | Lidar com operações de entrega e tempo de execução do Formulário adaptável | Geração e manipulação de documentos |
| Casos de uso | - Renderização do formulário<br>- Preenchimento prévio de dados<br>- Envios de formulário<br>- Gerenciamento de rascunhos | - Geração de PDF<br>- Mesclagem de documentos<br>- Processamento em lote<br>- Operações de impressão |
| Método de autorização | Suporta métodos de autenticação de servidor para servidor/usuário OAuth. | Suporta somente autenticação de servidor para servidor OAuth. |

### APIs de comunicações do AEM Forms

As APIs de comunicação são o foco principal das operações centradas em documentos.

A tabela abaixo lista todas as [APIs de Comunicações do AEM Forms](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/), juntamente com seus métodos de autenticação e modelos de execução compatíveis:

#### APIs de geração de documento


| Endpoint da API | Descrição | Modelo de execução | Método de autenticação |
| ----- | ------ |------- | ------ |
| [/adobe/forms/batch/output/config](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-batch/#tag/Batch-Configuration/operation/CreateBatchConfig) | Cria uma nova configuração de lote para trabalhos de geração de documento. | Assíncrono/Em Lote | [Servidor OAuth para servidor](/help/forms/oauth-api-authetication.md)/[JWT](/help/forms/jwt-api-authentication.md) |
| [/adobe/forms/batch/output/config/{configName}](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-batch/#tag/Batch-Configuration/operation/GetBatchConfigbyName) | Recupera detalhes de uma configuração de lote específica. | Assíncrono/Em Lote | [Servidor OAuth para servidor](/help/forms/oauth-api-authetication.md)/[JWT](/help/forms/jwt-api-authentication.md) |
| [/adobe/forms/batch/output/config/configs](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-batch/#tag/Batch-Configuration/operation/GetAllBatchConfigs) | Retorna uma lista de todas as configurações de lote disponíveis. | Assíncrono/Em Lote | [Servidor OAuth para servidor](/help/forms/oauth-api-authetication.md)/[JWT](/help/forms/jwt-api-authentication.md) |
| [/adobe/forms/batch/output/config/{configName}/execution](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-batch/#tag/Batch-Execution/operation/StartBatchRun) | Inicia uma execução de geração de saída em lote usando uma configuração. | Assíncrono/Em Lote | [Servidor OAuth para servidor](/help/forms/oauth-api-authetication.md)/[JWT](/help/forms/jwt-api-authentication.md) |
| [/adobe/forms/batch/output/config/{configName}/execution/{executionId}](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-batch/#tag/Batch-Execution/operation/GetBatchRunInstanceState) | Recupera o status de execução de um trabalho em lotes. | Assíncrono/Em Lote | [Servidor OAuth para servidor](/help/forms/oauth-api-authetication.md)/[JWT](/help/forms/jwt-api-authentication.md) |
| [/adobe/forms/batch/output/config/{configName}/executions](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-batch/#tag/Batch-Execution/operation/GetAllRunningInstancesForBatch) | Lista todas as instâncias em execução de uma configuração de lote específica. | Assíncrono/Em Lote | [Servidor OAuth para servidor](/help/forms/oauth-api-authetication.md)/[JWT](/help/forms/jwt-api-authentication.md) |
| [/adobe/forms/doc/v1/generatePDFOutput](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-sync/#tag/Communications-Services/paths/~1adobe~1forms~1doc~1v1~1generatePDFOutput/post) | Gera saída do PDF de forma síncrona com base em modelos e dados. | Sincrônico | [Servidor OAuth para servidor](/help/forms/oauth-api-authetication.md)/[JWT](/help/forms/jwt-api-authentication.md) |
| [/adobe/forms/doc/v1/generatePrintedOutput](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-sync/#tag/Batch-Execution/operation/GetAllRunningInstancesForBatch) | Gera formatos de saída prontos para impressão (por exemplo, PCL, PostScript). | Sincrônico | [Servidor OAuth para servidor](/help/forms/oauth-api-authetication.md)/[JWT](/help/forms/jwt-api-authentication.md) |
| [/adobe/forms/doc/v1/generate/afp](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-sync/#tag/Communications-Services/paths/~1adobe~1forms~1doc~1v1~1generate~1afp/post) | Gera saída AFP para impressão em alto volume. | Sincrônico | [Servidor OAuth para servidor](/help/forms/oauth-api-authetication.md)/[JWT](/help/forms/jwt-api-authentication.md) |
| [/adobe/document/generate/pdfform](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#operation/renderPDFForm) | Renderiza um formulário do PDF (XFA/XDP) com dados mesclados. | Sincrônico | [Servidor OAuth para servidor](/help/forms/oauth-api-authetication.md) |
| [/adobe/document/generate/pdfform/jobs/{id}/status](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#operation/renderPDFFormJobStatus) | Recupera o status de um trabalho de geração de formulário do PDF. | Sincrônico | [Servidor OAuth para servidor](/help/forms/oauth-api-authetication.md) |
| [/adobe/document/generate/pdfform/jobs/{id}/result](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#operation/renderPDFFormJobResult) | Busca a saída/resultado de um trabalho de formulário do PDF concluído. | Sincrônico | [Servidor OAuth para servidor](/help/forms/oauth-api-authetication.md) |


#### APIs de manipulação de documentos

| Endpoint da API | Descrição | Modelo de execução | Método de autenticação |
| ------------------ | ---------------- | ----------| ---------- |
| [/adobe/forms/assembler/ddx/invoke](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/assembler-sync/#tag/DDX-execution/operation/InvokeDDX) | Executa instruções do DDX para combinar, dividir ou manipular PDFs. | Sincrônico | [Servidor OAuth para servidor](/help/forms/oauth-api-authetication.md)/[JWT](/help/forms/jwt-api-authentication.md) |
| [/adobe/forms/assembler/pdfa/convert](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/assembler-sync/#tag/Document-conversion/operation/ConvertToPDFA) | Converte um documento do PDF no formato PDF/A. | Sincrônico | [Servidor OAuth para servidor](/help/forms/oauth-api-authetication.md)/[JWT](/help/forms/jwt-api-authentication.md) |
| [/adobe/forms/assembler/pdfa/validate](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/assembler-sync/#tag/Document-validation/operation/CheckIsPDFA) | Valida se um PDF está em conformidade com o padrão PDF/A | Sincrônico | [Servidor OAuth para servidor](/help/forms/oauth-api-authetication.md)/[JWT](/help/forms/jwt-api-authentication.md) |

#### APIs de conversão de documento

| Endpoint da API | Descrição | Modelo de execução | Método de autenticação |
|--------- | -------|---------|----------------------|
| [/adobe/document/convert/pdftoxdp](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Conversion/paths/~1convert~1pdftoxdp/post) | Converte um formulário do PDF em formato XDP. | Sincrônico | [Servidor OAuth para servidor](/help/forms/oauth-api-authetication.md) |

#### APIs de extração de documento

| Endpoint da API | Descrição | Modelo de execução | Método de autenticação |
|---------| -------|---------|----------------------|
| [/adobe/forms/doc/v1/extract/pdfproperties](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Extraction/paths/~1extract~1pdfproperties/post) | Extrai propriedades e informações estruturais de uma PDF. | Sincrônico | [Servidor OAuth para servidor](/help/forms/oauth-api-authetication.md) |
| [/adobe/forms/doc/v1/extract/usagerrights](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#operation/extractUsageRights) | Extrai direitos de uso incorporados em uma PDF. | Sincrônico | [Servidor OAuth para servidor](/help/forms/oauth-api-authetication.md) |
| [/adobe/forms/doc/v1/extract/metadata](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Extraction/paths/~1extract~1metadata/post) | Extrai metadados como título, autor e palavras-chave. | Sincrônico | [Servidor OAuth para servidor](/help/forms/oauth-api-authetication.md) |
| [/adobe/forms/doc/v1/extract/data](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#operation/exportData) | Extrai dados de formulário (XML/JSON) do PDF forms. | Sincrônico | [Servidor OAuth para servidor](/help/forms/oauth-api-authetication.md) |
| [/adobe/document/extract/security](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Extraction/paths/~1extract~1security/post) | Extrai configurações de segurança, como permissões e criptografia. | Sincrônico | [Servidor OAuth para servidor](/help/forms/oauth-api-authetication.md) |

#### APIs de transformação de documento


| Endpoint da API | Descrição | Modelo de execução | Método de autenticação |
|--------|---------|---------|----------------------|
| [/adobe/document/transform/metadata](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Transformation/paths/~1transform~1metadata/post) | Atualiza ou adiciona metadados em um documento do PDF. | Sincrônico | [Servidor OAuth para servidor](/help/forms/oauth-api-authetication.md) |
| [/adobe/document/field/signature/add](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Transformation/paths/~1field~1signature~1add/post) | Adiciona um campo de assinatura digital a uma PDF. | Sincrônico | [Servidor OAuth para servidor](/help/forms/oauth-api-authetication.md) |
| [/adobe/document/field/signature/clear](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Transformation/paths/~1field~1signature~1clear/post) | Limpa o conteúdo de um campo de assinatura. | Sincrônico | [Servidor OAuth para servidor](/help/forms/oauth-api-authetication.md) |
| [/adobe/document/field/signature/remove](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Transformation/paths/~1field~1signature~1remove/post) | Remove um campo de assinatura de uma PDF. | Sincrônico | [Servidor OAuth para servidor](/help/forms/oauth-api-authetication.md) |

#### Documentar APIs do Assurance

| Endpoint da API | Descrição | Modelo de execução | Método de autenticação |
|---------|-------|---------|----------------------|
| [/adobe/document/sure/usagerrights](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#operation/applyUsageRights) | Aplica direitos de uso a uma PDF (por exemplo, comentário, preenchimento, sinal). | Sincrônico | [Servidor OAuth para servidor](/help/forms/oauth-api-authetication.md) |
| [/adobe/document/sure/encrypt](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Assurance/paths/~1assure~1encrypt/post) | Criptografa uma PDF com segurança de senha ou certificado. | Sincrônico | [Servidor OAuth para servidor](/help/forms/oauth-api-authetication.md) |
| [/adobe/document/sure/decrypt](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Assurance/paths/~1assure~1decrypt/post) | Descriptografa um documento PDF protegido. | Sincrônico | [Servidor OAuth para servidor](/help/forms/oauth-api-authetication.md) |
| [/adobe/document/sure/sign](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Assurance/paths/~1assure~1sign/post) | Assina digitalmente um documento do PDF. | Sincrônico | [Servidor OAuth para servidor](/help/forms/oauth-api-authetication.md) |
| [/adobe/document/sure/certify](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Assurance/paths/~1assure~1certify/post) | Certifica uma PDF com um certificado digital. | Sincrônico | [Servidor OAuth para servidor](/help/forms/oauth-api-authetication.md) |


## Próximas etapas

Saiba como definir o ambiente para APIs de comunicações síncronas (sob demanda) e assíncronas (em lote) do Forms:

<!-- START CARDS HTML - DO NOT MODIFY BY HAND -->
<div class="columns">
    <!-- Synchronous APIs Card -->
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="AEM Forms Communications APIs - Synchronous">
        <div class="card" style="height: 100%; display: flex; flex-direction: column;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="/help/forms/aem-forms-cloud-service-communications-on-demand-processing.md" title="APIs síncronas" target="_self" rel="referrer">
                        <img class="is-bordered-r-small" src="/help/forms/assets/sync-api.png" alt="APIs síncronas"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="/help/forms/aem-forms-cloud-service-communications-on-demand-processing.md" target="_self" rel="referrer" title="APIs de comunicações do AEM Forms - síncronas">APIs de Comunicações do AEM Forms - Síncronas</a>
                    </p>
                    <p class="is-size-6">Saiba como configurar um ambiente para APIs síncronas (sob demanda) de comunicações do Forms que geram ou processam documentos instantaneamente. </p>
                </div>
                <a href="/help/forms/aem-forms-cloud-service-communications-on-demand-processing.md" target="_self" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Saiba mais</span>
                </a>
            </div>
        </div>
    </div>
    <!-- Asynchronous APIs Card -->
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="AEM Forms Communications APIs - Asynchronous">
        <div class="card" style="height: 100%; display: flex; flex-direction: column;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="/help/forms/aem-forms-cloud-service-communications-batch-processing.md" title="APIs de comunicações do AEM Forms - Assíncronas" target="_self" rel="referrer">
                        <img class="is-bordered-r-small" src="/help/forms/assets/async-api.png" alt="APIs assíncronas"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="/help/forms/aem-forms-cloud-service-communications-batch-processing.md" target="_self" rel="referrer" title="APIs assíncronas">APIs de Comunicações do AEM Forms - Assíncrono (Lote)</a>
                    </p>
                    <p class="is-size-6">Saiba como configurar um ambiente para APIs assíncronas (em lote) de comunicações do Forms que geram ou processam vários documentos de maneira programada.</p>
                </div>
                <a href="/help/forms/aem-forms-cloud-service-communications-batch-processing.md" target="_self" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Saiba mais</span>
                </a>
            </div>
        </div>
    </div>
</div>
<!-- END CARDS HTML - DO NOT MODIFY BY HAND -->


>[!MORELIKETHIS]
>
>* [Introdução às Comunicações do AEM Forms as a Cloud Service](/help/forms/aem-forms-cloud-service-communications-introduction.md)
>* [Arquitetura do AEM Forms as a Cloud Service para APIs de comunicação e Forms adaptável](/help/forms/aem-forms-cloud-service-architecture.md)
>* [Processamento da comunicação - APIs síncronas](/help/forms/aem-forms-cloud-service-communications.md)
>* [Processamento de comunicação - APIs em lote](/help/forms/aem-forms-cloud-service-communications-batch-processing.md)
>* [Processamento de comunicação - APIs por demanda](/help/forms/aem-forms-cloud-service-communications-on-demand-processing.md)