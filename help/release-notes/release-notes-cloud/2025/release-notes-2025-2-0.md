---
title: Notas de versão do  [!DNL Adobe Experience Manager]  as a Cloud Service 2025.2.0.
description: Notas de versão do  [!DNL Adobe Experience Manager]  as a Cloud Service 2025.2.0.
feature: Release Information
role: Admin
exl-id: b893663d-35f1-43ae-a029-4c249b117f2d
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1527'
ht-degree: 12%

---

# Notas de versão do [!DNL Adobe Experience Manager] as a Cloud Service 2025.2.0 {#release-notes}

A seção a seguir descreve as notas da versão de recursos do [!DNL Experience Manager] as a Cloud Service 2025.2.0.

>[!NOTE]
>
>A partir desta seção, você pode navegar até as notas das versões anteriores, como as de 2023 ou 2024.
>
>Dê uma olhada no [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para saber mais sobre as próximas ativações de recursos do [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Para receber uma notificação por email mensal sobre atualizações nas notas de versão do Experience Cloud, assine a [Atualização prioritária de produto da Adobe](https://www.adobe.com/subscription/priority-product-update.html).

## Data de lançamento {#release-date}

A data de lançamento da versão atual (2025.2.0) do [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] é quarta-feira, 4 de março de 2025. O próximo lançamento de recursos (2025.3.0) está planejado para sexta-feira, 27 de março de 2025.

## Notas da versão de manutenção {#maintenance}

Encontre as notas de versão de manutenção mais recentes [aqui](/help/release-notes/maintenance/latest.md).

## Vídeo da versão {#release-video}

Assista ao vídeo de visão geral da versão de fevereiro de 2025 para obter um resumo dos recursos adicionados na versão 2025.2.0:

>[!VIDEO](https://video.tv.adobe.com/v/3458080?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Novos recursos no AEM Sites {#new-features-sites}

**Marcação automática de fragmento de conteúdo**

Ao criar fragmentos de conteúdo, agora é possível herdar automaticamente as tags que foram atribuídas ao modelo de conteúdo. Isso permite uma classificação automática avançada do conteúdo armazenado nos Fragmentos de conteúdo.

**Suporte a UUID de fragmento de conteúdo**

O suporte para UUID do fragmento de conteúdo agora está disponível. O novo recurso não altera o comportamento baseado em caminho de operações no AEM, como mover, renomear, implantar, em que os caminhos estão sendo ajustados automaticamente, mas pode tornar o consumo externo de fragmentos de conteúdo mais fácil e estável, especialmente ao usar consultas do GraphQL que direcionam fragmentos individuais diretamente com consultas ByPath. Essas consultas podem ser interrompidas se um caminho de fragmento for alterado. Ao usar o novo tipo de consulta ById, a consulta agora permanece estável, pois a UUID de um fragmento não é alterada nos casos em que os caminhos o fazem.

**Suporte ao Dynamic Media com OpenAPI no Editor de Fragmento de Conteúdo e no GraphQL**

Os Assets armazenados em diferentes Programas AEM as a Cloud Service que não Fragmentos de conteúdo e que estão ativados com o novo recurso Dynamic Media com OpenAPI agora podem ser usados em Fragmentos de conteúdo. O seletor de imagens no novo Editor de fragmento de conteúdo agora permite selecionar repositórios &quot;remotos&quot; como a origem para que os ativos de imagem sejam referenciados no fragmento. E na entrega desses fragmentos de conteúdo usando o AEM GraphQL, a resposta JSON agora inclui as propriedades necessárias para ativos remotos (assetId, repositoryId) para que os aplicativos clientes possam criar o respectivo Dynamic Media com URLs OpenAPI para buscar a imagem.

**Implantação do editor de fragmento de conteúdo**

Continuaremos habilitando o novo [Editor de Fragmento de Conteúdo](/help/sites-cloud/administering/content-fragments/authoring.md) no AEM as a Cloud Service, usando o [Shell Unificado](/help/overview/aem-cloud-service-on-unified-shell.md) (usando a Interface do Usuário do Espectro). Depois de se tornar o padrão para todos os ambientes do Cloud Service Developer em novembro de 2024, ele será definido como padrão para todos os ambientes de preparo em 1º de abril de 2025 e para todos os ambientes de produção em 1º de maio de 2025. Em todos os casos, os usuários ainda terão a opção de reverter para o Editor de fragmento de conteúdo tradicional na interface para toque do AEM.

**API HTTP de tradução**

A API REST HTTP do AEM Translation que está no modo de adoção inicial há algum tempo está disponível. A documentação pode ser encontrada [aqui.](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/translation/) A API permite automatizar as etapas necessárias no processo de gerenciamento de tradução para conteúdo no AEM.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Novos recursos no AEM Assets {#new-features-assets}

**Nova estrutura de empacotamento do Dynamic Media**

Uma estrutura de empacotamento atualizada do Dynamic Media agora está disponível para se alinhar melhor às expectativas do mercado e ao rastreamento de suporte. A nova estrutura de embalagem compreende:

* Dynamic Media Prime, que inclui Dynamic Media com OpenAPIs e vídeo para aprimorar a entrega.

* O Dynamic Media Ultimate adiciona recursos de entrega e transformação para atender a requisitos de uso mais pesados.

Você deve ter o Assets as a Cloud Service Prime ou o Ultimate para se beneficiar da nova estrutura de pacotes.

**Legendas de vídeo geradas por IA**

Legendas de vídeo geradas por IA no Adobe Dynamic Media usam inteligência artificial para gerar legendas automaticamente para conteúdo de vídeo. Esse recurso foi projetado para melhorar a acessibilidade e a experiência do usuário, fornecendo legendas precisas. As legendas são geradas a partir do áudio original, todas as faixas de áudio adicionais ou legendas extras são fornecidas na guia &quot;Legendas e áudio&quot; na página de propriedades do vídeo. Com suporte para mais de 60 idiomas, as legendas podem ser revisadas e visualizadas antes da publicação do vídeo.

**Personalizar filtros de pesquisa**

Os filtros de pesquisa personalizados melhoram a precisão e a eficiência da localização de informações relevantes. Ele permite pesquisas mais personalizadas, filtrando dados de acordo com atributos específicos, como marca, produto, categoria ou outros identificadores principais. Isso melhora a organização, reduz o tempo gasto na verificação de resultados irrelevantes e permite uma tomada de decisão mais rápida. Também oferece suporte à escalabilidade, à medida que grandes conjuntos de dados se tornam mais fáceis de navegar e analisar.

![personalizar filtros de pesquisa](/help/assets/assets/custom-search-filters.png)

### Recursos de acesso antecipado no Content Hub {#early-access-content-hub}

O Content Hub agora permite visualizar e baixar representações dinâmicas e de Recorte inteligente, além das representações estáticas existentes. Como administrador do Content Hub, você também pode configurar a disponibilidade dessas representações para os usuários usando a Interface do usuário de configuração.

![representações dinâmicas](/help/assets/assets/download-single-asset-renditions-dynamic.png)

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

Conforme mencionado nas notas de versão de janeiro, agora é possível criar código com o Java 21, que inclui novos recursos (por exemplo, correspondência de padrões para instruções switch, classes lacradas) e melhorias de desempenho; as builds do Java 17 também são recém-compatíveis. Para obter as etapas de configuração, incluindo a atualização das versões do projeto e da biblioteca Maven, consulte o artigo [Criar ambiente](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#using-java-support).

O Java 21 **runtime** de maior desempenho será implantado automaticamente quando uma compilação Java 17 ou 21 for detectada. No entanto, também recomendamos a opção pelo tempo de execução do Java 21 para ambientes criados com o Java 11, enviando um email para [aemcs-java-adopter@adobe.com](mailto:aemcs-java-adopter@adobe.com). Saiba mais sobre [requisitos de tempo de execução do Java 21](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements).

>[!IMPORTANT]
>
> Em fevereiro, o Java 21 **runtime** foi implantado em ambientes dev/RDE (além daqueles já criados com o Java 17 ou 21, que já têm o runtime do Java 21). O Java 21 será aplicado a ambientes de preparo/produção em abril.

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

Saiba mais sobre as [APIs do AEM baseadas em OpenAPI](/help/implementing/developing/open-api-based-apis.md) e experimente um [tutorial completo](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/aem-apis/invoke-openapi-based-aem-apis) que ilustra a configuração e o uso.

Especificamente, os endpoints de API listados abaixo estão disponíveis como parte de um programa de adoção antecipada. Se estiver interessado, envie um email para [aem-apis@adobe.com](mailto:aem-apis@adobe.com) descrevendo como você pretende usá-los.

* [APIs de fragmentos de conteúdo do Sites](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/sites/)
* [APIs do Assets](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/assets/author/)
* APIs de pastas de sites e Assets
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
