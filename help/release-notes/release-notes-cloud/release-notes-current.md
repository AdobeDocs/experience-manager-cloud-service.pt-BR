---
title: Notas de versão atuais do  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Notas de versão atuais do  [!DNL Adobe Experience Manager]  as a Cloud Service.
mini-toc-levels: 1
source-git-commit: 085ce15ebe4d48d32a437f13e728f60cfc57d0fa
workflow-type: tm+mt
source-wordcount: '733'
ht-degree: 33%

---


# Notas de versão atuais do [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

A seção a seguir descreve as notas da versão de recurso atual (mais recente) do [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>A partir daqui, você pode navegar até as notas de versão anteriores; por exemplo, as de 2021, 2022 e assim por diante.
>
>Dê uma olhada no [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=pt-BR) para saber mais sobre as próximas ativações de recursos do [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Consulte [Atualizações recentes na documentação](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=pt-BR) para obter detalhes de atualizações de documentação não relacionadas diretamente a uma versão.

## Data de lançamento {#release-date}

A data de lançamento do [!DNL Adobe Experience Manager] como [!DNL Cloud Service] a versão do recurso atual (2023.2.0) é 12 de abril de 2023. A próxima versão de recurso (2023.4.0) está planejada para 27 de abril de 2023.

## Vídeo da versão {#release-video}

Assista ao vídeo Visão geral da versão de fevereiro de 2023 para obter um resumo dos recursos adicionados na versão 2023.2.0:

>[!VIDEO](https://video.tv.adobe.com/v/3416885/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Novos recursos no [!DNL Experience Manager Sites] pré-lançamento {#prerelease-sites}

* Exporte fragmentos de conteúdo do AEM as a cloud service para o Adobe target como ofertas JSON.
* O suporte para paginação e classificação do GraphQL, juntamente com aprimoramentos internos de cache, agora ajuda a melhorar o desempenho de aplicativos clientes dissociados ao buscar grandes conjuntos de conteúdo de AEM usando consultas e filtros complexos do GraphQL.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Novos recursos no [!DNL Assets] {#assets-features}

* Novo suporte ao protocolo (DASH - Dynamic Adaptive Streaming over HTTP) lançado para o streaming adaptável na entrega de vídeo do Dynamic Media (com CMAF ativado):
   * O streaming adaptável (DASH/HLS) garante uma melhor experiência de visualização do usuário final para vídeos
   * DASH é o protocolo padrão internacional para transmissão de vídeo adaptável e é amplamente adotado no setor
   * Disponível em NA, para ser habilitado por meio de tíquete de suporte, em breve em APAC, EMEA

* Adição de suporte para imagens WebP para extrair metadados automaticamente, gerar miniaturas e representações personalizadas. Os recursos de Tag inteligente e Recorte inteligente também são compatíveis com esses arquivos.

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Novos recursos disponíveis em [!DNL Forms] {#new-features-available-in-channel}

* **[Use componentes principais de captura de dados para criar formulários adaptáveis](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=pt-BR)**: o [editor de formulários adaptáveis](/help/forms/creating-adaptive-form-core-components.md) pode ser usado para criar formulários com base em componentes de captura de dados padronizados (componentes principais). Esses componentes fornecem recursos de personalização, tempo de desenvolvimento reduzido e custos de manutenção mais baixos para suas experiências de inscrição digital.

* **[Suporte a pipeline de fronteira para o Forms adaptável baseado em componentes principais de estilo](/help/forms/using-themes-in-core-components.md)**: Utilize temas padronizados baseados em BEM para o Forms adaptativo baseado em componentes principais, implantando-os com o pipeline de implantação do front-end para aprimorar a aparência de seus formulários e alinhar-se às diretrizes de design aprovadas pela marca de sua organização.

* **[Gerar documento de registro para Forms adaptável baseado em componentes principais](/help/forms/generate-document-of-record-core-components.md)**: Crie um documento de registro contendo dados enviados para o Adaptive Forms criado usando componentes principais para arquivamento ou referência para usuários finais, na impressão ou no formato do documento.

![https://www.aemcomponents.dev/](/help/forms/assets/sample-core-components-based-adaptive-form.png)

* **[Criação eficiente de formulários com o recurso Salvar um formulário adaptável como modelo](/help/forms/template-editor.md#save-an-adaptive-form-as-template-saving-adaptive-form-as-template)**: Acelere e padronize o desenvolvimento de formulários, salvando formulários já aprovados como modelos de formulário para reutilização rápida.

* **[Conectar o AEM Forms a bancos de dados compatíveis com JDBC](/help/forms/configure-data-sources.md#configure-relational-database-configure-relational-database)**: Conecte-se a bancos de dados corporativos diretamente do serviço AEM Cloud usando o protocolo JDBC, sem a necessidade de expô-los sobre a REST API.

* **[Integre com endpoints REST usando a API 3.0 aberta](/help/forms/configure-data-sources.md#configure-restful-services-open-api-specification-version-20-configure-restful-services-swagger-version30)**: Integre-se perfeitamente aos sistemas de registro que oferecem suporte à API 3.0 aberta para armazenar e buscar dados usando modelos de dados de formulário.

* **[Compartilhar um formulário adaptável para revisão](/help/forms/create-reviews-forms.md)**: use o mecanismo de revisão de formulários adaptáveis para permitir que um ou mais revisores revisem o formulário.


### Recursos em [!DNL Forms] pré-lançamento {#prerelease-features-forms}

* **[Enviar Forms adaptável para o Microsoft SharePoint e Microsoft OneDrive](/help/forms/configuring-submit-actions.md)**: Melhore a agilidade do usuário empresarial para iniciar novos formulários rapidamente e armazenar dados enviados em ferramentas diárias usadas como o site Microsoft SharePoint ou a pasta OneDrive.

![Enviar Forms adaptável para o Microsoft SharePoint e Microsoft OneDrive](/help/forms/assets/onedrive-and-sharepoint.jpg)


## Programa de usuários antecipados da Adaptive Forms sem cabeçalho {#forms-early-adopter}

Use o Headless Adaptive Forms para permitir que seus desenvolvedores criem, publiquem e gerenciem formulários interativos que podem ser acessados e interagidos por meio de APIs, em vez de por meio de uma interface gráfica tradicional. Os formulários adaptáveis sem interface ajudam a:

* crie formulários multicanal de alta qualidade na linguagem de programação de sua escolha
* Integre nativamente formulários a aplicativos móveis, sites e aplicativos de bate-papo
* reutilize seus componentes proprietários da interface do usuário com aplicativos de formulários
* aproveitar o potencial do Adobe Experience Manager Forms

Você pode enviar um email para aem-forms-headless@adobe.com a partir de sua ID de email oficial para participar do programa de adotante antecipado.

## Notas da versão de manutenção {#maintenance}

Encontre as notas de versão de manutenção mais recentes [aqui](/help/release-notes/maintenance/latest.md).

## Cloud Manager {#cloud-manager}

Você pode encontrar uma lista completa de versões mensais do Cloud Manager [aqui.](/help/implementing/cloud-manager/release-notes/current.md)

## Ferramentas de migração {#migration-tools}

Você pode encontrar uma lista completa de versões das ferramentas de migração [aqui](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
