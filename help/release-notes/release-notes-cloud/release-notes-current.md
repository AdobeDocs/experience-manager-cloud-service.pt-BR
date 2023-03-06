---
title: Notas de versão atuais do  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Notas de versão atuais do  [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
mini-toc-levels: 1
source-git-commit: e4346c4fb8c8d29d3a2772a6db8ba408b287d1bf
workflow-type: tm+mt
source-wordcount: '1032'
ht-degree: 23%

---


# Notas de versão atuais do [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

A seção a seguir descreve as notas de versão de recursos da versão atual (mais recente) do [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>A partir daqui, você pode navegar até as notas de versão das versões anteriores; por exemplo, para aquelas em 2021, 2022 e assim por diante.
>
>Dê uma olhada no [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=pt-BR) para saber mais sobre as próximas ativações de recursos do [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Consulte [Atualizações recentes na documentação](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=pt-BR) para obter detalhes de atualizações de documentação não relacionadas diretamente a uma versão.

## Data de lançamento {#release-date}

A data de lançamento de [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] a versão atual do recurso (2023.1.0) é 9 de fevereiro de 2023. A próxima versão do recurso (2023.2.0) está planejada para 30 de março de 2023.

## Vídeo da versão {#release-video}

Assista ao vídeo Visão geral da versão de janeiro de 2023 que exibe um resumo dos recursos adicionados na versão 2023.1.0:

>[!VIDEO](https://video.tv.adobe.com/v/3413479/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Novos recursos no pré-lançamento do [!DNL Sites] {#prerelease-features-sites}

* A API de entrega de conteúdo AEM GraphQL agora é compatível com o GraphQL [Paginação](/help/headless/graphql-api/content-fragments.md#paging) e [Classificação](/help/headless/graphql-api/content-fragments.md#sorting), para tornar mais eficiente a busca e a renderização de grandes conjuntos de conteúdo. A paginação do GraphQL permite melhorar o tempo de resposta da consulta, retornando os resultados em subconjuntos, e não de uma só vez. A classificação do GraphQL permite colocar conjuntos de conteúdo em uma ordem desejada, facilitando o processamento do conteúdo por um aplicativo cliente.  O tempo de resposta da consulta é aprimorado ainda mais com a Filtragem híbrida no mecanismo do AEM GraphQL. O conteúdo agora é lido do JCR em conjuntos menores que correspondem aos filtros de consulta.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Novos recursos no [!DNL Assets] {#assets-features}

* Os relatórios de ativos agora incluem a capacidade de os administradores [gerar relatórios de download de ativos](/help/assets/asset-reports.md) da implantação as a Cloud Service do Experience Manager Assets. Esses dados capacitam ainda mais os administradores a obter insights das principais métricas de sucesso para medir a adoção de ativos na sua empresa e por clientes.

   ![Representação de PDF para outros formatos](/help/release-notes/assets/choose_report.png)

* O Experience Manager Assets agora [é compatível com o token SAS](/help/assets/add-assets.md#asset-bulk-ingestor) além da Chave de acesso para autenticação ao conectar-se à fonte de dados do Armazenamento de Blobs do Azure para assimilar ativos usando a ferramenta Importação em massa.

* Gerenciamento aprimorado de imagens CMYK no Asset compute, permitindo gerar Recorte inteligente e Tags inteligentes para imagens CMYK.

### Novos recursos no pré-lançamento do [!DNL Assets] {#prerelease-features-assets}

* O Experience Manager Assets agora é compatível [assimilação em grande escala de ativos da Google Cloud Platform](/help/assets/add-assets.md#asset-bulk-ingestor) usando a ferramenta Importação em massa.

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Novos recursos disponíveis em [!DNL Forms] {#new-features-available-in-channel}

* **[Etapas do fluxo de trabalho para gerar documentos PDF não interativos e saída imprimível](/help/forms/aem-forms-workflow-step-reference.md)**: automatize a criação de documentos de PDF não interativos e saída imprimível para seus processos comerciais com etapas do fluxo de trabalho AEM, simplificando seu processo de geração de documentos e economizando tempo.
* **[Use as notas de rodapé para fornecer citações ou informações adicionais no Adaptive Forms](/help/forms/footnotes-richtextsupport.md)**: Use Notas de rodapé em um formulário adaptável para exibir as informações sobre como preencher ou usar um formulário. Você também pode usá-la para fornecer informações entre parênteses, permissões de direitos autorais e outras informações úteis.

### Novos recursos no pré-lançamento do [!DNL Forms] {#prerelease-features-forms}

* **[Usar componentes principais de captura de dados para criar o Forms adaptável](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=en)**: [Usar o editor Forms adaptável](/help/forms/creating-adaptive-form-core-components.md) para criar formulários com base em componentes de captura de dados padronizados (Componentes principais). Esses componentes fornecem recursos de personalização, tempo de desenvolvimento reduzido e custos de manutenção mais baixos para suas experiências de inscrição digital.
* **[Suporte a pipeline de front-end para estilizar o Forms adaptável baseado em componentes principais](/help/forms/using-themes-in-core-components.md)**: Utilize temas facilmente personalizáveis baseados em BEM para o Adaptive Forms baseado em Componentes principais, implantando-os com o pipeline de Implantação de front-end para aprimorar a aparência de seus formulários.
* **[Gerar documento de registro para o componente principal baseado no Forms adaptável](/help/forms/generate-document-of-record-core-components.md)**: crie um registro para o formulário adaptável baseado em componente principal no envio para arquivamento de longo prazo, em impressão ou no formato de documento.

![https://www.aemcomponents.dev/](/help/forms/assets/sample-core-components-based-adaptive-form.png)

* **[Enviar Forms adaptável para o Microsoft SharePoint e o Microsoft OneDrive](/help/forms/configuring-submit-actions.md)**: agilize o envio de dados com a capacidade de enviar dados do Formulário adaptável diretamente para o Microsoft SharePoint e o Microsoft OneDrive. Você pode enviar dados baseados em esquema e sem esquema. Essas ações de envio são adicionais às ações de envio já disponíveis.
* **[Construção eficiente de formulários com o recurso Salvar um formulário adaptável como modelo](/help/forms/template-editor.md#save-an-adaptive-form-as-template-saving-adaptive-form-as-template)**: simplifique o processo de criação de formulários salvando um Formulário adaptável como modelo e reutilizando os modelos para o próximo Formulário adaptável.
* **[Conectar o AEM Forms a bancos de dados compatíveis com JDBC](/help/forms/configure-data-sources.md#configure-relational-database-configure-relational-database)**: conecte facilmente seu modelo de dados do AEM Forms a bancos de dados que oferecem suporte ao JDBC, permitindo ler e gravar dados perfeitamente.
* **[Integrar com endpoints REST usando a API aberta 3.0](/help/forms/configure-data-sources.md#configure-restful-services-open-api-specification-version-20-configure-restful-services-swagger-version30)**: conecte os Modelos de dados de formulário as a Cloud Service do AEM Forms aos endpoints REST que oferecem suporte à especificação Open API versão 3.0, permitindo enviar e receber dados com facilidade.
* **[Compartilhar um formulário adaptável para revisão](/help/forms/create-reviews-forms.md)**: use o mecanismo de revisão Adaptive Forms para permitir que um ou mais revisores revisem o formulário.


## Complemento CIF {#cloud-services-cif}

### Novidades {#what-is-new-cif}

* Os autores podem enriquecer dinamicamente listas de produtos com Fragmentos de experiência (por exemplo: colocar banner entre as listas de produtos).
* O componente de lista agora oferece suporte às páginas de produto/categoria associadas para mostrar dinamicamente páginas relacionadas.
* Foi adicionado suporte para componentes do Peregrine 12.5.
* Foi adicionado suporte para o carregamento de preço no lado do cliente no teaser e no carrossel do produto.

## [!DNL Experience Manager as a Cloud Service] Foundation {#foundation}

### Novidades {#what-is-new-foundation}

* [Ambientes de desenvolvimento rápido](/help/implementing/developing/introduction/rapid-development-environments.md) - Os RDEs permitem que os desenvolvedores solucionem problemas rapidamente e implantem novos recursos no AEM as a Cloud Service.

   Os ambientes de desenvolvimento rápido são um novo tipo de ambiente de nuvem criado como uma maneira rápida, consistente e extensível de validar se o código que funciona localmente também funciona conforme esperado na nuvem. Usando as Ferramentas de linha de comando, &quot;sincronize&quot; rapidamente pacotes de conteúdo, pacotes, arquivos de conteúdo, configuração OSGI ou configuração do dispatcher para o RDE. Veja isso em ação no vídeo abaixo:

   >[!VIDEO](https://video.tv.adobe.com/v/3413508/?quality=12&learn=on)

   Depois de validar o código com êxito no RDE, é recomendável implantar em um Ambiente de desenvolvimento da nuvem para utilizar os quality gates (portais de qualidade) do Cloud Manager, antes de implantar por meio do pipeline de produção em ambientes de preparo e produção.

   Cada programa inclui um RDE e, opcionalmente, mais podem ser licenciados.

   >[!NOTE]
   >
   >Os RDEs serão lançados gradualmente nas próximas semanas; você pode enviar um email para aemcs-rde-support@adobe.com para pular para a frente da linha.

* [Suporte estendido para tokens de acesso de API do lado do servidor](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md) - Agora é possível gerar várias credenciais, o que é útil para cenários em que as APIs têm características diferentes. Agora também é possível revogar credenciais de maneira automatizada.

## Notas de versão de manutenção {#maintenance}

Encontre as notas de versão de manutenção mais recentes [aqui](/help/release-notes/maintenance/latest.md).

## Cloud Manager {#cloud-manager}

Você pode encontrar uma lista completa de versões mensais do Cloud Manager [aqui.](/help/implementing/cloud-manager/release-notes/current.md)

## Ferramentas de migração {#migration-tools}

Você pode encontrar uma lista completa de versões das ferramentas de migração [aqui](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
