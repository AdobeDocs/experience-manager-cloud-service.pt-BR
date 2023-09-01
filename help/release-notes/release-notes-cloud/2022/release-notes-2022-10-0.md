---
title: Notas de versão do  [!DNL Adobe Experience Manager]  as a Cloud Service 2022.10.0.
description: Notas de versão do  [!DNL Adobe Experience Manager]  as a Cloud Service 2022.10.0.
exl-id: 8fce7c50-f322-4bcf-bd76-390faedfd5b7
source-git-commit: 87630d9530194fd0c6d88e05a17db108b765ccb6
workflow-type: tm+mt
source-wordcount: '836'
ht-degree: 79%

---

# Notas de versão do [!DNL Adobe Experience Manager] as a Cloud Service 2022.10.0 {#release-notes}

A seção a seguir descreve as notas de versão de recurso da versão 2022.10.0 do [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>A partir daqui, você pode navegar até as notas de versão das versões anteriores; por exemplo, para aquelas em 2020, 2021 e assim por diante.

>[!NOTE]
>
>Consulte [Atualizações recentes na documentação](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=pt-BR) para obter detalhes de atualizações de documentação não relacionadas diretamente a uma versão.

## Data de lançamento {#release-date}

A data de lançamento da versão atual (2022.10.0) do [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] é 10 de novembro de 2022. A próxima versão (2023.1.0) mensal está planejada para 9 de fevereiro de 2023.

## Vídeo da versão {#release-video}

Assista ao vídeo de Visão geral da versão de outubro de 2022 que exibe um resumo dos recursos adicionados na versão 2022.10.0:

>[!VIDEO](https://video.tv.adobe.com/v/3409801/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}


### Novos recursos no [!DNL Sites] {#sites-features}

* A variável [Guia Personalização para Fragmentos de experiência](/help/sites-cloud/authoring/fundamentals/experience-fragments.md#personalization-experience-fragment) O permite recursos de especificação de segmentação para o Editor de fragmento de experiência e a flexibilidade para criar Fragmentos de experiência aninhados, nos quais as variações de cabeçalhos e rodapés podem ser criadas para vários segmentos. Antes do lançamento desse recurso, a personalização oferecida pelo AEM só está disponível para páginas do site, mas não para Fragmentos de experiência

* O [Console do Fragmento do conteúdo](/help/sites-cloud/administering/content-fragments/managing.md#content-fragments-console) agora permite que os usuários gerenciem com eficiência fragmentos de conteúdo traduzidos. Um acesso de 1 clique também foi fornecido para exibir todas as cópias de idioma. Os usuários também podem filtrar a exibição de tabela pela localidade de seu interesse.

![Idiomas de Fragmentos de conteúdo](/help/release-notes/assets/cfconsole-languages.png)

* Reduza ainda mais o tempo de carregamento de página para visitantes otimizando as configurações de tamanhos de imagem em modelos. Encontre mais informações para o componente de imagem em [Componente WCM principal](https://github.com/adobe/aem-core-wcm-components)

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Novos recursos no [!DNL Assets] {#assets-features}

* O Experience Manager Assets agora permite fazer upload de documentos em outros tipos de formato compatíveis e[visualizá-los usando o visualizador de Document Cloud incluído](/help/assets/manage-pdf-documents.md). Os tipos de formato compatíveis incluem TXT, RTF, DOC, DOCX, PPT, PPTX, XLS e XLSX.

  ![Representação de PDF para outros formatos](/help/release-notes/assets/multi-page-other-formats.png)


### Novos recursos no pré-lançamento do [!DNL Assets] {#prerelease-features-assets}

* O Experience Manager Assets agora usa uma estrutura de inteligência artificial aprimorada para tags inteligentes de imagem. Essa inteligência de conteúdo resulta em melhor relevância e precisão das Tags inteligentes disponíveis para todos os ativos de imagem na assimilação. Além disso, as informações de orientação são preenchidas em `cq:tags`, o que permite melhores resultados de pesquisa através da utilização do filtro de Orientação.

  Se você estiver interessado em participar da versão beta, [preencha este formulário](https://forms.office.com/pages/responsepage.aspx?id=Wht7-jR7h0OUrtLBeN7O4epXZrTVKKdJkUiHeolccf9UNEwyNEpHVEFaODdBNFZQSlFDREZQOVRRTy4u) até 14 de novembro.

* O Experience Manager Assets agora [é compatível com o token SAS](/help/assets/add-assets.md#asset-bulk-ingestor) além da Chave de acesso para autenticação ao conectar-se à fonte de dados do Armazenamento de Blobs do Azure para assimilar ativos usando a ferramenta Importação em massa.

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Novos recursos disponíveis no canal de pré-lançamento do [!DNL Forms] {#prerelease-features-forms}

* **Editor de modelo adaptável do Forms**: o editor de modelos permite que você predefina a estrutura básica e a aparência do Forms adaptável de uma organização. Esta versão traz as seguintes melhorias para o editor de modelo:
   * **[Modelo de dados de formulário no editor de modelos](/help/forms/creating-adaptive-form.md#edit-form-model-properties-of-an-adaptive-form-edit-form-model)**: você pode associar um esquema de Modelo de dados de formulário a um modelo de formulário adaptável no editor de modelos. Isso ajuda a reduzir o tempo gasto para criar um Formulário adaptável. A opção também é adicionada ao editor de Formulários adaptáveis para permitir que os usuários selecionem ou alterem o Modelo de Dados de Formulário para formulários existentes.
   * **[Documento de Registro no editor de modelo](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#document-of-record-support-in-adaptive-form-editor-dor-support-in-adaptiveform)**: Agora é possível padronizar a geração de Documento de Registro para todos os formulários criados usando um modelo. Isso ajuda a aprimorar a conformidade e a padronização dos requisitos da organização.

* **[Iniciar o assistente de Formulário Adaptável em uma página do AEM Sites](/help/forms/embed-adaptive-form-aem-sites.md)**: A página AEM Sites tem suporte estendido para o Formulários Adaptáveis. Agora é possível criar um novo Formulário Adaptável ou incorporar um Formulário Adaptável existente, permanecendo na página do AEM Sites.
* **[Alterar o alinhamento de exibição para caixas de seleção e botões de rádio no DoR](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#customize-the-branding-information-in-document-of-record-customize-the-branding-information-in-document-of-record)**: Agora é possível definir o alinhamento desejado (Horizontal, Vertical, Igual ao Adaptive Forms) para as caixas de seleção e os botões de rádio no Documento de Registro. Essa opção determina o posicionamento das opções de caixa de seleção e botão de opção no Documento de registro.

## Complemento CIF {#cloud-services-cif}

### Novidades {#what-is-new-cif}

* Os autores podem enriquecer dinamicamente listas de produtos com Fragmentos de experiência (por exemplo: colocar banner entre as listas de produtos).
* O componente de lista agora oferece suporte às páginas de produto/categoria associadas para mostrar dinamicamente páginas relacionadas.
* Foi adicionado suporte para componentes do Peregrine 12.5.
* Foi adicionado suporte para o carregamento de preço no lado do cliente no teaser e no carrossel do produto.

## [!DNL Experience Manager as a Cloud Service] Foundation {#foundation}

### Novidades {#what-is-new-foundation}

* O AEM as a Cloud Service (Serviços do autor) agora está integrado com o Unified Shell para melhorar a experiência dos usuários e unificá-lo com todos os outros aplicativos da Experience Cloud. Ver AEM como um [Cloud Service no shell unificado](/help/overview/aem-cloud-service-on-unified-shell.md) para obter mais detalhes.

* Conforme mencionado anteriormente nas notas de versão, o uso da tela de administrador do agente de replicação ou da API de replicação para distribuir pacotes de conteúdo maiores que 10 MB (nós com propriedades, sem incluir binários) agora está obsoleto e é aplicado. Consulte [Gerenciar publicação](/help/operations/replication.md#manage-publication) ou o [Fluxo de trabalho de publicação da árvore de conteúdo](/help/operations/replication.md#publish-content-tree-workflow) para obter abordagens sugeridas para replicar esses pacotes de conteúdo grandes.

* A configuração do Dispatcher agora faz referência a um arquivo que lista parâmetros de consulta de campanha de marketing comuns. Os clientes podem optar por remover o comentário dos parâmetros que são relevantes para eles, resultando em um melhor armazenamento em cache. Consulte [Parâmetros da campanha de marketing](/help/implementing/dispatcher/caching.md#marketing-parameters) para obter mais detalhes.

## Cloud Manager {#cloud-manager}

Você pode encontrar uma lista completa de versões mensais do Cloud Manager [aqui](/help/implementing/cloud-manager/release-notes/current.md).

## Ferramentas de migração {#migration-tools}

Você pode encontrar uma lista completa de versões das ferramentas de migração [aqui](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
