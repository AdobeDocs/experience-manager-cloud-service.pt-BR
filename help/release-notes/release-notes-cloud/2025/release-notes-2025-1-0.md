---
title: Notas de versão do  [!DNL Adobe Experience Manager]  as a Cloud Service 2025.1.0.
description: Notas de versão do  [!DNL Adobe Experience Manager]  as a Cloud Service 2025.1.0.
feature: Release Information
role: Admin
source-git-commit: f899398182f9d0991123828ca217379653a4e397
workflow-type: tm+mt
source-wordcount: '1513'
ht-degree: 11%

---

# Notas de versão do [!DNL Adobe Experience Manager] as a Cloud Service 2025.1.0 {#release-notes}

A seção a seguir descreve as notas da versão de recursos do [!DNL Experience Manager] as a Cloud Service 2025.1.0.

>[!NOTE]
>
>A partir desta seção, você pode navegar até as notas das versões anteriores, como as de 2023 ou 2024.
>
>Dê uma olhada no [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para saber mais sobre as próximas ativações de recursos do [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Para receber uma notificação por email mensal sobre atualizações nas notas de versão do Experience Cloud, assine a [Atualização prioritária de produto da Adobe](https://www.adobe.com/subscription/priority-product-update.html).

## Data de lançamento {#release-date}

A data de lançamento da versão atual (2025.1.0) do [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] é sexta-feira, 30 de janeiro de 2025. O próximo lançamento de recursos (2025.2.0) está planejado para quarta-feira, 4 de março de 2025.

## Notas da versão de manutenção {#maintenance}

Encontre as notas de versão de manutenção mais recentes [aqui](/help/release-notes/maintenance/latest.md).

<!-- 

## Release Video {#release-video}

Have a look at the January 2025 Release Overview video for a summary of the features added in the 2025.1.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3440920?quality=12)

-->

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

**Comentários no Editor de fragmento do conteúdo agora geralmente disponíveis**

Colabore facilmente com os colegas de trabalho ao criar fragmentos de conteúdo do AEM usando o serviço de comentários novo e modernizado no Editor de fragmentos de conteúdo do AEM.
[Leia mais](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/sites/administering/content-fragments/authoring?#commenting-on-your-fragment).

**Editor de fragmento do conteúdo e interfaces de usuário do administrador, suporte atualizado para a versão do AEM as a Cloud Service**

A versão mínima do AEM as a Cloud Service compatível com as novas interfaces do usuário do administrador e do editor de fragmento de conteúdo agora é 2023.8.13099. As versões anteriores da versão de disponibilidade geral das novas interfaces de usuário não são mais compatíveis

### Programa de adoção antecipada {#sites-early-adopter}

**Fragmentos de conteúdo aprimorados**

[Referência de fragmento de conteúdo aprimorada com referências exclusivas baseadas em ID](/help/headless/graphql-api/uuid-reference-upgrade.md), ajudando a garantir que as consultas do GraphQL para fragmentos de conteúdo individuais possam permanecer estáveis, mesmo que o fragmento tenha sido movido para outro local. Isso agora é possível com queries &quot;ByID&quot;. Embora os caminhos possam mudar, possivelmente quebrando consultas &quot;ByPath&quot;, as UUIDs são estáveis. As novas IDs também podem ser retornadas como propriedades em qualquer query ou outra solicitação de API aplicável. Limitação atual (2025.1): as referências de página ainda não são compatíveis com IDs exclusivas. Se as páginas forem referenciadas em Fragmentos de conteúdo, esse recurso não deverá ser usado. A limitação está planejada para ser removida na próxima versão do AEM as a Cloud Service.

**OpenAPI REST do AEM para entrega de fragmentos de conteúdo**

A [OpenAPI REST do AEM para Entrega de Fragmento de Conteúdo](/help/headless/aem-rest-openapi-content-fragment-delivery.md) está disponível agora para o AEM as a Cloud Service.

### Recursos obsoletos {#sites-deprecated}

#### Editor SPA {#spa-editor}

[O Editor de SPA](/help/implementing/developing/hybrid/introduction.md) foi descontinuado para novos projetos a partir da versão 2025.1.0. O Editor SPA permanece compatível com projetos existentes, mas não deve ser usado para novos projetos.

Os editores preferidos para gerenciar conteúdo headless no AEM agora são:

* [O Editor Universal](/help/edge/wysiwyg-authoring/authoring.md) para edição visual.
* [O Editor de Fragmento de Conteúdo](/help/assets/content-fragments/content-fragments-managing.md) para edição baseada em formulário.

#### Recursos do PWA {#pwa-features}

[Os recursos do aplicativo web progressivo (PWA)](/help/sites-cloud/authoring/sites-console/enable-pwa.md) para AEM Sites foram descontinuados para novos projetos a partir da versão 2025.1.0. Esse recurso ainda é compatível com projetos existentes, mas não deve ser usado para novos projetos

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Novos recursos na exibição do AEM Assets {#new-features-assets}

**Personalizar filtros de pesquisa**

Os filtros de pesquisa personalizados melhoram a precisão e a eficiência da localização de informações relevantes. Ele permite pesquisas mais personalizadas, filtrando dados de acordo com atributos específicos, como marca, produto, categoria ou outros identificadores principais. Isso melhora a organização, reduz o tempo gasto na verificação de resultados irrelevantes e permite uma tomada de decisão mais rápida. Também oferece suporte à escalabilidade, à medida que grandes conjuntos de dados se tornam mais fáceis de navegar e analisar.

![filtros de pesquisa personalizados](/help/assets/assets/custom-search-filters.png)

### Novos recursos no Content Hub {#new-features-content-hub}

Descrição

### Recursos de acesso antecipado no AEM Assets {#early-access-features-assets}

**Legendas de vídeo geradas por IA**

Legendas de vídeo geradas por IA no Adobe Dynamic Media usam inteligência artificial para gerar legendas automaticamente para conteúdo de vídeo. Esse recurso foi projetado para melhorar a acessibilidade e a experiência do usuário, fornecendo legendas precisas e em tempo real. As legendas são geradas a partir do áudio original, de qualquer trilha de áudio adicional ou de legendas extras fornecidas na guia &quot;Legendas e áudio&quot; na página de propriedades do vídeo. Com suporte para mais de 60 idiomas, as legendas podem ser revisadas e visualizadas antes da publicação do vídeo.

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Novos recursos no AEM Forms {#forms-new-features}

* **Gerenciar Publicação**: você pode usar o fluxo de trabalho [Gerenciar Publicação](/help/forms/manage-publication.md#publish-forms-using-the-manage-publication-option) para publicar ou desfazer a publicação de formulários entre ambientes, normalmente da instância de criação para as instâncias de publicação e visualização. Ele permite que os usuários publiquem, desfaçam a publicação ou agendem a publicação de conteúdo de maneira simplificada.

* **[Salvar automaticamente um rascunho para os Componentes principais com base no Forms adaptável](/help/forms/save-core-component-based-form-as-draft.md)**: os usuários agora podem se beneficiar de um recurso de salvamento automático que salva automaticamente um formulário parcialmente preenchido como rascunho. Eles podem retornar mais tarde para terminar de preenchê-lo no mesmo dispositivo ou em outro. Esse recurso melhora as taxas de conversão para organizações ao reduzir o abandono de formulário, pois os usuários não precisam começar novamente o preenchimento do formulário desde o início.

* **[Aprimoramentos no editor de regras](/help/forms/invoke-service-enhancements-rule-editor.md)**: para o Adaptive Forms com base em Componentes principais, você pode usar a saída do Invoke Service para preencher opções suspensas e definir painéis repetíveis ou individuais. Além disso, essa saída pode ser usada para validar outros campos.

* **[Aprimorar a Experiência do Usuário com Botões de Navegação em Layouts de Painel](/help/forms/rule-editor-core-components-usecases.md#navigating-among-panels-using-button)**: Agora é possível adicionar botões de navegação aos layouts de painel, como Guias Horizontais, Guias Verticais, Acordeões ou Assistente. Esses botões melhoram a experiência do usuário simplificando as transições entre painéis, com foco no painel selecionado.


### Recursos de acesso antecipado no AEM Forms {#forms-new-early-access-features}

O programa de acesso antecipado da AEM Forms oferece uma oportunidade única para você obter acesso exclusivo a inovações de última geração e ajudar a moldar seu desenvolvimento.

Estas notas de versão listam as inovações fornecidas na versão atual. Para obter a lista completa de inovações disponíveis no Programa de Acesso Antecipado, consulte a [documentação do Programa de Acesso Antecipado do AEM Forms](/help/forms/early-access-ea-features.md).

#### [Modelos de email do HTML no Forms Adaptável](/help/forms/html-email-templates-in-adaptive-forms.md)

O Forms adaptável permite usar modelos de email do HTML. Os templates de email do HTML permitem enviar emails avançados, personalizados e visualmente atraentes quando um formulário é enviado. Esses emails podem ser personalizados com dados de formulário e aprimorados usando várias tags de email, como imagens e links. Com o Adaptive Forms, você pode fazer upload de um arquivo contendo um modelo do HTML ou usar um editor de texto simples para criar esses modelos.

![modelos de email do HTML](/help/forms/assets/html-email.png)

#### Suporte ao armazenamento na nuvem aprimorado: upload direto do PDF para o armazenamento Azure Blob

As APIs de geração de documentos do AEM Forms agora oferecem suporte ao upload direto de documentos gerados do PDF para o Armazenamento de blobs do Azure. Esse aprimoramento simplifica o armazenamento e a recuperação, melhorando a eficiência e a integração com fluxos de trabalho em nuvem.

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Suporte ao Java 21 {#java21}

Agora você pode criar código com o Java 21, que inclui novos recursos (por exemplo, correspondência de padrões para instruções switch, classes lacradas) e melhorias de desempenho; as builds do Java 17 também são recém-compatíveis. Para obter as etapas de configuração, incluindo a atualização das versões do projeto e da biblioteca Maven, consulte o artigo [Criar ambiente](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#using-java-support).

O Java 21 **runtime** de maior desempenho será implantado automaticamente quando uma compilação Java 17 ou 21 for detectada. No entanto, também recomendamos a opção pelo tempo de execução do Java 21 para ambientes criados com o Java 11, enviando um email para [aemcs-java-adopter@adobe.com](mailto:aemcs-java-adopter@adobe.com). Saiba mais sobre [requisitos de tempo de execução do Java 21](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements).

>[!IMPORTANT]
>
> O **tempo de execução** do Java 21 será implantado gradualmente em **todos** ambientes (além daqueles já criados com o Java 17 ou 21, que já têm o tempo de execução do Java 21), começando com sandboxes e dev/RDE em fevereiro e depois prepare/production em abril.

### Programas de sandbox oferecem suporte a pipelines de configuração {#sandbox-config-pipelines}

Os programas de sandbox agora oferecem suporte a pipelines de configuração, que podem ser configurados no Cloud Manager para implantar arquivos yaml mantidos no Git.

[Saiba mais](/help/operations/config-pipeline.md) sobre pipelines de configuração, que permitem a configuração da CDN, o encaminhamento de logs e as tarefas de manutenção de limpeza de versão/limpeza de logs de auditoria.

### APIs baseadas em OpenAPI - Early Adoter Program {#open-apis-earlyadopter}

Os desenvolvedores podem integrar profundamente os recursos do AEM as Cloud Service em seus próprios aplicativos e ferramentas. As novas APIs do AEM as a Cloud Service seguem a especificação OpenAPI, com o objetivo de serem consistentes, bem documentadas e fáceis de usar. As credenciais para endpoints que exigem autenticação são geradas ao criar projetos do Adobe Developer Console.

Saiba mais sobre as [APIs do AEM baseadas em OpenAPI](/help/implementing/developing/open-api-based-apis.md) e experimente um [tutorial completo](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/aem-apis/invoke-openapi-based-aem-apis) que ilustra a configuração e o uso.

Especificamente, os endpoints de API listados abaixo estão disponíveis como parte de um programa de adoção antecipada. Se estiver interessado, envie um email para [aem-apis@adobe.com](mailto:aem-apis@adobe.com) descrevendo como você pretende usá-los.

* [APIs de fragmentos de conteúdo do Sites](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/sites/)
* [APIs do Assets](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/assets/author/)
* [APIs de Sites e Pastas do Assets](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/folders/)
* [APIs de comunicações do Forms](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/)

### Computação Edge - Solicitação de feedback! {#edge-computing-feedback}

A computação Edge aproxima o processamento de dados do navegador, o que traz benefícios, inclusive latência reduzida. A Adobe gostaria de saber se você acha essa tecnologia útil para o AEM Publish Delivery e para projetos Edge Delivery Services. Além disso, informe-nos sobre o que você planeja usar como entrada no roteiro de produtos. Email [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com) com perguntas e comentários!

### Novo AEM Developer Console (Beta público) {#aem-developer-console-beta}

Experimente um [AEM Developer Console](/help/implementing/developing/introduction/aem-developer-console.md) renovado, que oferece uma experiência mais interativa para depurar código em ambientes na nuvem.

Qualquer pessoa pode acessar o beta público clicando no botão *Novo Console Disponível* no Developer Console do AEM atual. A Adobe agradece o feedback, que você pode enviar por email para [aemcs-new-devconsole-ui-beta@adobe.com](mailto:aemcs-new-devconsole-ui-beta@adobe.com)

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

Você pode encontrar informações sobre versões de outros aplicativos da Experience Cloud [aqui](https://experienceleague.adobe.com/pt-br/docs/release-notes/experience-cloud/current).
