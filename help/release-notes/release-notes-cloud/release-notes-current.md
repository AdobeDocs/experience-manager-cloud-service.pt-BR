---
title: Notas de versão atuais do  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Notas de versão atuais do  [!DNL Adobe Experience Manager] as a Cloud Service.
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: bbf66195593032eb2ccf073ec78685c9d9726235
workflow-type: tm+mt
source-wordcount: '1092'
ht-degree: 14%

---

# Notas de versão atuais do [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

A seção a seguir descreve as notas da versão de recurso atual (mais recente) do [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>A partir desta seção, você pode navegar até as notas das versões anteriores, como as de 2023 ou 2024.
>
>Dê uma olhada no [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para saber mais sobre as próximas ativações de recursos do [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Para receber uma notificação por email mensal sobre atualizações nas notas de versão do Experience Cloud, assine a [Atualização prioritária de produto da Adobe](https://www.adobe.com/subscription/priority-product-update.html).

## Data de lançamento {#release-date}

A data de lançamento da versão atual (2025.3.0) do [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] é sexta-feira, 27 de março de 2025. O próximo lançamento de recursos (2025.4.0) está planejado para sexta-feira, 24 de abril de 2025.

## Notas da versão de manutenção {#maintenance}

Encontre as notas de versão de manutenção mais recentes [aqui](/help/release-notes/maintenance/latest.md).

<!-- 

## Release Video {#release-video}

Have a look at the February 2025 Release Overview video for a summary of the features added in the 2025.2.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3440920?quality=12)

-->

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Novos recursos no Dynamic Media {#new-features-dynamic-media}

**Suporte a formulários longos para vídeos entregues com o Dynamic Media com API aberta**

O Dynamic Media com OpenAPI agora é compatível com vídeos de formulários longos. Os vídeos de formato longo podem suportar até 50 GB e 2 horas.

### Dynamic Media Classic {#dmc}

<!-- CARRY OVER TO APRIL 2025 RELEASE NOTES -->

The Bandwidth tab in the Dynamic Media Classic reporting dashboard is no longer supported as of April 2025.

See [Bandwidth and Storage, Types of reports](https://experienceleague.adobe.com/en/docs/dynamic-media-classic/using/setup/administration-setup#types-of-reports).


## Novos recursos na visualização de ativos {#new-features-assets-view}


**Suporte para marcas raiz**

O AEM Assets agora oferece suporte ao mapeamento de uma propriedade de tag em um formulário de metadados para metadados personalizados. Além disso, como administrador, você pode restringir a disponibilidade de tags aos usuários, restringindo o acesso a uma tag raiz específica e às tags existentes na tag raiz.

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Recursos de acesso antecipado no AEM Forms {#forms-new-early-access-features}

O programa de acesso antecipado da AEM Forms oferece uma oportunidade única para você obter acesso exclusivo a inovações de última geração e ajudar a moldar seu desenvolvimento.

Estas notas de versão listam as inovações fornecidas na versão atual. Para obter a lista completa de inovações disponíveis no Programa de Acesso Antecipado, consulte a [documentação do Programa de Acesso Antecipado do AEM Forms](/help/forms/early-access-ea-features.md).

#### Modelos de email do HTML no Adaptive Forms

O Adaptive Forms permite usar [modelos de email do HTML](/help/forms/html-email-templates-in-adaptive-forms.md). Os templates de email do HTML permitem enviar emails avançados, personalizados e visualmente atraentes quando um formulário é enviado. Esses emails podem ser personalizados com dados de formulário e aprimorados usando várias tags de email, como imagens e links. Com o Adaptive Forms, você pode fazer upload de um arquivo contendo um modelo do HTML ou usar um editor de texto simples para criar esses modelos.

![modelos de email do HTML](/help/forms/assets/html-email.png)

#### Suporte ao armazenamento na nuvem aprimorado: upload direto do PDF para o armazenamento Azure Blob

AEM Forms Document Generation APIs now let you [directly upload generated PDF documents](/help/forms/early-access-ea-features.md#doc-generation-api) to Azure Blob Storage. Esse aprimoramento simplifica o armazenamento e a recuperação, melhorando a eficiência e a integração com fluxos de trabalho em nuvem.

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Suporte ao Java 21 {#java21}

A partir da versão de janeiro, você pode criar código com o Java 21 e Java 17. Você obtém acesso a novos recursos, como correspondência de padrões, classes lacradas e várias melhorias de desempenho. Para obter as etapas de configuração, incluindo a atualização das versões do projeto e da biblioteca Maven, consulte o artigo [Ambiente de compilação](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#using-java-support).

O Java 21 **runtime** de maior desempenho é implantado automaticamente quando uma compilação Java 17 ou 21 é detectada. However, Adobe also recommends opting into the Java 21 runtime for environments built with Java 11, by emailing [aemcs-java-adopter@adobe.com](mailto:aemcs-java-adopter@adobe.com). Saiba mais sobre [requisitos de tempo de execução do Java 21](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements).

>[!IMPORTANT]
>
> O Java 21 **runtime** foi implantado em seus ambientes dev/RDE em fevereiro; ele será aplicado em seus ambientes de preparo/produção em **28 e 29**. Observe que o **código de construção** com Java 21 (ou Java 17) é independente do tempo de execução do Java 21 — você deve tomar etapas explicitamente para criar o código com Java 21 (ou Java 17).

### Encaminhamento de logs do AEM para mais destinos - Programa Beta {#log-forwarding-earlyadopter}

Agora na versão beta, você pode encaminhar logs do AEM para o New Relic (usando HTTPS), Amazon S3 e Sumo Logic. Observe que os logs do AEM (incluindo o Apache/Dispatcher) são compatíveis, mas não os logs CDN. Email [aemcs-logforwarding-beta@adobe.com](mailto:aemcs-logforwarding-beta@adobe.com) para acesso.

Embora os logs possam ser baixados da Cloud Manager, muitas organizações acham útil transmitir esses logs para um destino de registro preferencial. O AEM já oferece suporte ao (GA) encaminhamento de logs do AEM e do CDN para o Armazenamento de blobs do Azure, Datadog, HTTPS, Elasticsearch (e OpenSearch) e Splunk. Esse recurso é configurado de maneira automatizada e implantado usando o Pipeline de configuração.

Saiba mais na [documentação sobre encaminhamento de logs](/help/implementing/developing/introduction/log-forwarding.md).

### Computação Edge - Solicitação de feedback! {#edge-computing-feedback}

A computação Edge aproxima o processamento de dados do navegador, o que traz benefícios, inclusive latência reduzida. A Adobe gostaria de saber se você acha que essa tecnologia é útil para o AEM Publish Delivery e para projetos Edge Delivery Services. Além disso, informe-nos sobre o que você planeja usar como entrada no roteiro de produtos.

Alguns casos de uso possíveis:

* Autenticação com um IdP para portar o acesso ao conteúdo
* Renderização de conteúdo dinâmico (personalizado, localizado) com base na geolocalização, tipo de dispositivo, atributos do usuário etc.
* Manipulação avançada de imagem
* Middleware entre a CDN e uma origem
* Uma camada entre o navegador e uma API de terceiros, talvez para reformatar a resposta da API
* Agregar dados de várias origens para facilitar a renderização pelo navegador do cliente

Email [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com) com perguntas e comentários!

### APIs baseadas em OpenAPI - Early Adoter Program {#open-apis-earlyadopter}

Os desenvolvedores podem integrar profundamente os recursos do AEM as Cloud Service em seus próprios aplicativos e ferramentas. As novas APIs do AEM as a Cloud Service seguem a especificação OpenAPI, com o objetivo de serem consistentes, bem documentadas e fáceis de usar. As credenciais para endpoints que exigem autenticação são geradas ao criar projetos do Adobe Developer Console.

Saiba mais sobre as [APIs do AEM baseadas em OpenAPI](/help/implementing/developing/open-api-based-apis.md) e experimente um [tutorial completo](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/aem-apis/openapis/invoke-api-using-oauth-s2s) que ilustra a configuração e o uso.

Especificamente, os endpoints de API listados abaixo estão disponíveis como parte de um programa de adoção antecipada. Se estiver interessado, envie um email para [aem-apis@adobe.com](mailto:aem-apis@adobe.com) descrevendo como você pretende usá-los.

* [APIs de fragmentos de conteúdo do Sites](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/sites/)
* [APIs do Assets](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/assets/author/)
* [APIs de Sites e Pastas do Assets](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/folders/)
* [APIs de comunicações do Forms](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/)

### Novo AEM Developer Console (Beta público) {#aem-developer-console-beta}

Experimente um [AEM Developer Console](/help/implementing/developing/introduction/aem-developer-console.md) renovado, que oferece uma experiência mais interativa para depurar código em ambientes na nuvem.

Qualquer pessoa pode acessar o beta público clicando no botão *Novo Console Disponível* no Developer Console do AEM atual. A Adobe agradece o feedback, que você pode enviar por email para [aemcs-new-devconsole-ui-beta@adobe.com](mailto:aemcs-new-devconsole-ui-beta@adobe.com)

## Guias do [!DNL Experience Manager] {#guides}

Você pode encontrar uma lista completa de recursos novos e aprimorados da versão mais recente do Adobe Experience Manager Guides [aqui](https://experienceleague.adobe.com/en/docs/experience-manager-guides/using/release-info/release-notes/cloud-release-notes/2025-releases/2502-release/whats-new-2025-02-0).

<!-- THE FOLLOWING URL WAS USED ABOVE BUT IT WAS 404. IT WAS REPLACED WITH THE URL ABOVE 
(https://experienceleague.adobe.com/en/docs/experience-manager-guides/using/release-info/release-notes/cloud-release-notes/2024-releases/2410-release/2410-0-release/whats-new-2024-10-0). -->

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
