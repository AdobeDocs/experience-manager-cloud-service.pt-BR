---
title: Notas de versão atuais do  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Notas de versão atuais do  [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
mini-toc-levels: 1
source-git-commit: b1715c819a6d049c88de8f0bc7061951bbcd5248
workflow-type: tm+mt
source-wordcount: '914'
ht-degree: 15%

---


# Notas de versão atuais do [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

A seção a seguir descreve as Notas de versão gerais da versão atual (mais recente) do [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>A disponibilidade do SDK AEM as a Cloud Service correspondente está atrasada, com um objetivo de 11 de novembro.

>[!NOTE]
>
>A partir daqui, você pode navegar até as notas de versão das versões anteriores; por exemplo, para aquelas em 2020, 2021 e assim por diante.

>[!NOTE]
>
>Consulte [Atualizações recentes na documentação](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=pt-BR) para obter detalhes de atualizações de documentação não relacionadas diretamente a uma versão.

>[!CAUTION]
>
>**Black Friday e Período de Exclusão de Manutenção de Natal**
>
> Nenhuma manutenção automática do AEMaaCS será executada durante os seguintes períodos de tempo, começando e terminando à meia-noite (00:00) CET:
>
>* segunda-feira, 21 de novembro até segunda-feira, 5 de dezembro
>* segunda-feira, 19 de dezembro a terça-feira, 3 de janeiro
>
> Esses períodos abrangem Black Friday, Cyber Monday, Natal e Ano Novo.

## Data de lançamento {#release-date}

A data de lançamento do [!DNL Adobe Experience Manager] como [!DNL Cloud Service] a versão mensal atual (2022.10.0) é 10 de novembro de 2022. A próxima versão mensal (2023.1.0) está planejada para 26 de janeiro de 2022.

## Vídeo da versão {#release-video}

Assista ao vídeo Visão geral da versão de outubro de 2022 para obter um resumo dos recursos adicionados na versão 2022.10.0:

>[!VIDEO](https://video.tv.adobe.com/v/3409801/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}


### Novos recursos no [!DNL Sites] {#sites-features}

* O [Guia Personalização para fragmentos de experiência](/help/sites-cloud/authoring/fundamentals/experience-fragments.md#personalization-experience-fragment) O permite recursos de especificação de segmentação para o Editor de fragmento de experiência, bem como a flexibilidade para criar Fragmentos de experiência aninhados, onde as variações de cabeçalhos e rodapés podem ser criadas para vários segmentos. Antes do lançamento desse recurso, a personalização oferecida pelo AEM só está disponível para páginas do site, mas não para Fragmentos de experiência

* O [Console do fragmento do conteúdo](/help/sites-cloud/administering/content-fragments/content-fragments-console.md) agora permite que os usuários gerenciem com eficiência fragmentos de conteúdo traduzidos. Um acesso de 1 clique foi fornecido para exibir todas as cópias de idioma também. Os usuários também podem filtrar a exibição de tabela pelo local de seu interesse.

![Idiomas de fragmentos de conteúdo](/help/release-notes/assets/cfconsole-languages.png)

* Reduza ainda mais o tempo de carregamento de página para visitantes, otimizando as configurações de tamanhos de imagem em modelos. Encontre mais informações para o componente de imagem em [Componente WCM principal](https://github.com/adobe/aem-core-wcm-components)

## [!DNL Experience Manager Assets] como [!DNL Cloud Service] {#assets}

### Novos recursos no [!DNL Assets] {#assets-features}

* O Experience Manager Assets agora permite fazer upload de documentos em outros tipos de formato compatíveis e[ visualizá-los usando o Document Cloud viewer incluído](/help/assets/manage-pdf-documents.md). Os tipos de formato compatíveis incluem TXT, RTF, DOC, DOCX, PPT, PPTX, XLS e XLSX.

   ![representação de PDF para outros formatos](/help/release-notes/assets/multi-page-other-formats.png)


### Novos recursos em [!DNL Assets] pré-lançamento {#prerelease-features-assets}

* O Experience Manager Assets agora usa uma estrutura de inteligência artificial aprimorada para tags inteligentes de imagem. Essa inteligência de conteúdo resulta em melhor relevância e precisão das Tags inteligentes disponíveis para todos os ativos de imagem na assimilação. Além disso, as informações de orientação são preenchidas em `cq:tags`, que permite melhores resultados de pesquisa usando o filtro Orientação .

   Se você estiver interessado em participar da versão beta, [preencher este formulário](https://forms.office.com/pages/responsepage.aspx?id=Wht7-jR7h0OUrtLBeN7O4epXZrTVKKdJkUiHeolccf9UNEwyNEpHVEFaODdBNFZQSlFDREZQOVRRTy4u) até 14 de novembro.

* Experience Manager Assets agora [suporta o token SAS](/help/assets/add-assets.md#asset-bulk-ingestor) além da Chave de acesso para autenticação ao conectar-se à fonte de dados do Armazenamento Azure Blob para assimilar ativos usando a ferramenta Importação em massa .

## [!DNL Experience Manager Forms] como [!DNL Cloud Service] {#forms}

### Novos recursos disponíveis no canal de pré-lançamento do [!DNL Forms] {#prerelease-features-forms}

* **Editor de modelo adaptável do Forms**: O editor de modelos permite que você predefina a estrutura básica e a aparência do Adaptive Forms de uma organização. Esta versão traz as seguintes melhorias para o editor de modelo:
   * **[Modelo de dados de formulário no editor de modelos](/help/forms/creating-adaptive-form.md#edit-form-model-properties-of-an-adaptive-form-edit-form-model)**: Você pode associar um esquema de Modelo de dados de formulário a um modelo de Formulário adaptável no editor de modelos. Ajuda a reduzir o tempo gasto para criar um formulário adaptável. A opção também é adicionada ao editor Adaptive Forms para permitir que os usuários selecionem ou alterem o Modelo de dados de formulário para formulários existentes.
   * **[Documento de registro no editor de modelo](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#document-of-record-support-in-adaptive-form-editor-dor-support-in-adaptiveform)**: Agora é possível padronizar a geração de Documento de registro para todos os formulários criados usando um modelo. Isso ajuda a aprimorar a conformidade e a padronização dos requisitos de organização.

* **[Iniciar o assistente de Formulário adaptável em uma página do AEM Sites](/help/forms/embed-adaptive-form-aem-sites.md)**: A página AEM Sites tem suporte estendido para o Adaptive Forms. Agora é possível criar um novo formulário adaptável ou incorporar um formulário adaptável existente, permanecendo na página do AEM Sites.
* **[Alterar o alinhamento de exibição para caixas de seleção e botão de opção no DoR](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#customize-the-branding-information-in-document-of-record-customize-the-branding-information-in-document-of-record)**: Agora é possível definir o alinhamento desejado (horizontal, vertical, igual ao Forms adaptável) para as caixas de seleção e os botões de opção no Documento de registro. Essa opção determina o posicionamento das opções de caixa de seleção e botão de opção no Documento de registro.

## Complemento CIF {#cloud-services-cif}

### Novidades {#what-is-new-cif}

* Os autores podem enriquecer dinamicamente listas de produtos com Fragmentos de experiência (exemplo: colocar banner entre as listas de produtos).
* O componente de lista agora oferece suporte às páginas de produto/categoria associadas para mostrar dinamicamente páginas relacionadas.
* Foi adicionado suporte para componentes do Peregrine 12.5.
* Foi adicionado suporte para o carregamento de preço no lado do cliente no teaser e no carrossel do produto.

## [!DNL Experience Manager as a Cloud Service] Foundation {#foundation}

### Novidades {#what-is-new-foundation}

* AEM as a Cloud Service (Serviço de Autor) agora está integrado ao Unified Shell para melhorar a experiência do usuário e unificá-la com todos os outros aplicativos do Experience Cloud. Consulte AEM como um [Cloud Service no shell unificado](/help/overview/aem-cloud-service-on-unified-shell.md) para obter mais detalhes.

* Conforme mencionado anteriormente nas notas de versão, o uso da tela de administração do agente de replicação ou da API de replicação para distribuição de pacotes de conteúdo maiores que 10 MB (nós com propriedades, não incluindo binários) está obsoleto e será aplicado nos próximos dias. Consulte [Gerenciar publicação](/help/operations/replication.md#manage-publication) ou [Fluxo de trabalho da Árvore de conteúdo de publicação](/help/operations/replication.md#publish-content-tree-workflow) para as abordagens sugeridas para replicar esses pacotes de conteúdo grandes.

* A configuração do Dispatcher agora faz referência a um arquivo que lista parâmetros de consulta de campanha de marketing comuns. Os clientes podem optar por remover o comentário dos parâmetros que são relevantes para eles, resultando em um melhor armazenamento em cache. Consulte [Parâmetros da campanha de marketing](/help/implementing/dispatcher/caching.md#marketing-parameters) para obter mais detalhes.

## Cloud Manager {#cloud-manager}

Você pode encontrar uma lista completa de versões mensais do Cloud Manager [aqui](/help/implementing/cloud-manager/release-notes-cloud-manager/release-notes-cm-current.md).

## Ferramentas de migração {#migration-tools}

Você pode encontrar uma lista completa de versões das ferramentas de migração [aqui](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
