---
title: Notas de versão do  [!DNL Adobe Experience Manager]  as a Cloud Service 2025.3.0.
description: Notas de versão do  [!DNL Adobe Experience Manager]  as a Cloud Service 2025.3.0.
feature: Release Information
role: Admin
exl-id: b9353092-88a0-477c-85f4-f916a4b8ba8f
source-git-commit: 420b02e8398a433d0ff93ed0f60e01560ae786b8
workflow-type: tm+mt
source-wordcount: '1123'
ht-degree: 16%

---

# Notas de versão do [!DNL Adobe Experience Manager] as a Cloud Service 2025.3.0 {#release-notes}

A seção a seguir descreve as notas da versão de recursos do [!DNL Experience Manager] as a Cloud Service 2025.3.0.

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

## Vídeo da versão {#release-video}

Assista ao vídeo Visão geral da versão de março de 2025 que exibe um resumo dos recursos adicionados na versão 2025.3.0:

>[!VIDEO](https://video.tv.adobe.com/v/3463860?quality=12)

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Novos recursos no Dynamic Media {#new-features-dynamic-media}

**Suporte a formulários longos para vídeos entregues com o Dynamic Media com API aberta**

O Dynamic Media com OpenAPI agora é compatível com vídeos de formulários longos. Os vídeos de formato longo podem suportar até 50 GB e 2 horas.

### Dynamic Media Classic {#dmc}

<!-- CARRY OVER TO APRIL 2025 RELEASE NOTES -->

A guia Largura de banda no painel de relatórios do Dynamic Media Classic não é mais compatível desde abril de 2025.

Consulte [Largura de Banda e Armazenamento, Tipos de relatórios](https://experienceleague.adobe.com/en/docs/dynamic-media-classic/using/setup/administration-setup#types-of-reports).


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

As APIs de geração de documentos do AEM Forms agora permitem [carregar diretamente documentos gerados do PDF](/help/forms/early-access-ea-features.md#doc-generation-api) para o Armazenamento de blobs do Azure. Esse aprimoramento simplifica o armazenamento e a recuperação, melhorando a eficiência e a integração com fluxos de trabalho em nuvem.

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Suporte ao Java 21 {#java21}

A partir da versão de janeiro, você pode criar código com o Java 21 e Java 17. Você obtém acesso a novos recursos, como correspondência de padrões, classes lacradas e várias melhorias de desempenho. Para obter as etapas de configuração, incluindo a atualização das versões do projeto e da biblioteca Maven, consulte o artigo [Ambiente de compilação](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#using-java-support).

O Java 21 **runtime** de maior desempenho é implantado automaticamente quando uma compilação Java 17 ou 21 é detectada. No entanto, a Adobe também recomenda aceitar o tempo de execução do Java 21 para ambientes criados com o Java 11, enviando um email para [aemcs-java-adopter@adobe.com](mailto:aemcs-java-adopter@adobe.com). Saiba mais sobre [requisitos de tempo de execução do Java 21](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements).

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
