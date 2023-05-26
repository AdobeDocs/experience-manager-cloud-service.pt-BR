---
title: Notas de versão atuais do  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Notas de versão atuais do  [!DNL Adobe Experience Manager]  as a Cloud Service.
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
source-git-commit: 11e0a0872e5bd0ce18043e227fdcd3e609cf28d8
workflow-type: tm+mt
source-wordcount: '730'
ht-degree: 98%

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

A data de lançamento da versão atual (2023.2.0) do [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] é 12 de abril de 2023. O próximo lançamento de recursos (2023.4.0) está planejado para 31 de maio de 2023.

## Vídeo da versão {#release-video}

Assista ao vídeo de visão geral da versão de fevereiro de 2023 para obter um resumo dos recursos adicionados na versão 2023.2.0:

>[!VIDEO](https://video.tv.adobe.com/v/3416885/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Novos recursos no [!DNL Experience Manager Sites] pré-lançamento {#prerelease-sites}

* Exporte fragmentos de conteúdo do AEM as a Cloud Service para o Adobe Target como ofertas JSON.
* O suporte para os recursos de paginação e classificação de GraphQL, juntamente com aprimoramentos internos de armazenamento em cache, agora ajuda a melhorar o desempenho de aplicativos clientes dissociados ao buscar grandes conjuntos de conteúdo do AEM usando consultas e filtros de GraphQL complexos.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Novos recursos no [!DNL Assets] {#assets-features}

* Lançamento de um novo suporte de protocolo (DASH, Dynamic Adaptive Streaming over HTTP) para a transmissão adaptável na entrega de vídeos do Dynamic Media (com CMAF habilitado):
   * A transmissão adaptável (DASH/HLS) garante uma melhor experiência de exibição de vídeos ao usuário final
   * DASH é o protocolo internacional padrão para transmissão de vídeo adaptável e é amplamente adotado no setor
   * Disponível na América do Norte (habilitado por meio de um tíquete de suporte); em breve para as regiões da APAC e EMEA

* Adição de suporte para imagens WebP para extrair metadados automaticamente e gerar miniaturas e representações personalizadas. O recurso de tag inteligente agora também é compatível com esses arquivos.

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Novos recursos disponíveis em [!DNL Forms] {#new-features-available-in-channel}

* **[Use componentes principais de captura de dados para criar formulários adaptáveis](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=pt-BR)**: o [editor de formulários adaptáveis](/help/forms/creating-adaptive-form-core-components.md) pode ser usado para criar formulários com base em componentes de captura de dados padronizados (componentes principais). Esses componentes fornecem recursos de personalização, tempo de desenvolvimento reduzido e custos de manutenção mais baixos para suas experiências de inscrição digital.

* **[Suporte a pipeline de front-end para estilização de formulários adaptáveis baseados em componentes principais](/help/forms/using-themes-in-core-components.md)**: utilize temas padronizados baseados em BEM em formulários adaptáveis baseados em componentes principais, implantando-os por meio do pipeline de implantação de front-end para aprimorar a aparência de seus formulários e alinhar-se com as diretrizes de design aprovadas pela marca da sua organização.

* **[Gerar documento de registro para formulários adaptáveis baseados em componentes principais](/help/forms/generate-document-of-record-core-components.md)**: crie um documento de registro contendo dados enviados para formulários adaptáveis criados com componentes principais para arquivamento ou como referência para usuários finais, na impressão ou no formato de documento.

![https://www.aemcomponents.dev/](/help/forms/assets/sample-core-components-based-adaptive-form.png)

* **[Criação eficiente de formulários com o recurso Salvar um formulário adaptável como modelo](/help/forms/template-editor.md#save-an-adaptive-form-as-template-saving-adaptive-form-as-template)**: acelere e padronize o desenvolvimento salvando os formulários já aprovados para a marca como modelos de formulário para reutilização rápida.

* **[Conectar o AEM Forms a bancos de dados compatíveis com JDBC](/help/forms/configure-data-sources.md#configure-relational-database-configure-relational-database)**: conecte-se a bancos de dados corporativos diretamente do AEM Cloud Service usando o protocolo JDBC, sem a necessidade de os expor através da API REST.

* **[Integrar a pontos de acesso REST usando a API 3.0 aberta](/help/forms/configure-data-sources.md#configure-restful-services-open-api-specification-version-20-configure-restful-services-swagger-version30)**: integre-se perfeitamente aos sistemas de registro compatíveis com a API 3.0 aberta para armazenar e buscar dados usando modelos de dados de formulário.

* **[Compartilhar um formulário adaptável para revisão](/help/forms/create-reviews-forms.md)**: use o mecanismo de revisão de formulários adaptáveis para permitir que um ou mais revisores revisem o formulário.


### Recursos no pré-lançamento do [!DNL Forms] {#prerelease-features-forms}

* **[Enviar formulários adaptáveis para o Microsoft SharePoint e o Microsoft OneDrive](/help/forms/configuring-submit-actions.md)**: melhore o processo do usuário empresarial, agilizando o lançamento de novos formulários e permitindo o armazenamento de dados enviados em ferramentas usadas diariamente, como o site do Microsoft SharePoint ou a pasta do OneDrive.

![Enviar formulários adaptáveis para o Microsoft SharePoint e o Microsoft OneDrive](/help/forms/assets/onedrive-and-sharepoint.jpg)


## Programa de adoção antecipada de formulários adaptáveis headless {#forms-early-adopter}

Use formulários adaptáveis hedless para permitir que seus desenvolvedores criem, publiquem e gerenciem formulários interativos que podem ser acessados e manuseados por meio de APIs, em vez de utilizar uma interface gráfica tradicional. Os formulários adaptáveis headless ajudam a:

* criar formulários multicanal de alta qualidade na linguagem de programação de sua escolha
* integrar formulários nativamente a seus aplicativos móveis e de desktop, sites e aplicativos de bate-papo
* reutilizar os componentes de interface de sua propriedade com aplicativos de formulários
* aproveitar o potencial do Adobe Experience Manager Forms

Você pode enviar um email para aem-forms-headless@adobe.com utilizando sua ID de email oficial para participar do programa de adoção antecipada.

## Notas da versão de manutenção {#maintenance}

Encontre as notas de versão de manutenção mais recentes [aqui](/help/release-notes/maintenance/latest.md).

## Cloud Manager {#cloud-manager}

Você pode encontrar uma lista completa de versões mensais do Cloud Manager [aqui.](/help/implementing/cloud-manager/release-notes/current.md)

## Ferramentas de migração {#migration-tools}

Você pode encontrar uma lista completa de versões das ferramentas de migração [aqui](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
