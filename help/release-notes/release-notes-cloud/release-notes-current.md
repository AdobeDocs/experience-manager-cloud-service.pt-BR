---
title: Notas de versão do  [!DNL Adobe Experience Manager] as a Cloud Service 2020.8.0.
description: 'Notas de versão do [!DNL Adobe Experience Manager] as a Cloud Service 2020.8.0 '
translation-type: tm+mt
source-git-commit: 561345f58ce8e448176507e3bba114324dc18256
workflow-type: tm+mt
source-wordcount: '1058'
ht-degree: 7%

---


# Notas de versão do [!DNL Adobe Experience Manager] as a Cloud Service 2020.8.0 {#release-notes}

A seção a seguir descreve as Notas de versão gerais do Experience Manager as a Cloud Service 2020.8.0.

## Data de lançamento {#release-date}

The release date for [!DNL Experience Manager] as a Cloud Service 2020.8.0 is August 27, 2020.

## [!DNL Adobe Experience Manager Sites] como um Cloud Service {#sites}

### What is new in [!DNL Sites] {#what-is-new-sites}

* Capacidade de [restaurar páginas e subpáginas (árvores de página) para uma versão](/help/sites-cloud/authoring/features/page-versions.md#reinstating-versions)anterior.

* Capacidade de criar Inicializações no Editor SPA AEM.

## [!DNL Adobe Experience Manager Assets] como um Cloud Service {#assets}

### What is new in [!DNL Assets] {#what-is-new-assets}

* A transcodificação de vídeo agora é compatível com microserviços de ativos, com uma nova seção Vídeo na tela Perfis [!UICONTROL de] processamento que suporta a configuração de taxa de bits e dimensões de vídeo (o formato de saída é MP4 com codec H.264). Para obter detalhes, consulte [gerenciar ativos](/help/assets/manage-video-assets.md#transcode-video)de vídeo. Para obter mais opções de transcodificação, é possível usar o complemento delivery de vídeo [!DNL Dynamic Media] .

* Em novas [!DNL Experience Manager Assets] implantações, a funcionalidade de marcação inteligente agora é configurada por padrão. Não há necessidade de integração manual com [!DNL Adobe Developer Console]. Em implantações existentes, os administradores [configuram a integração](/help/assets/smart-tags-configuration.md#aio-integration) de tags inteligentes como antes.

* Uma nova experiência [de download de](/help/assets/download-assets-from-aem.md) ativos permite:

   * Download assíncrono para downloads grandes para que os usuários não precisem esperar.

   * Uma nova API modular para extensibilidade do desenvolvedor.

* [!DNL Experience Manager] melhorou o desempenho da extração de metadados para microserviços de ativos. Isso aumenta a taxa de transferência geral de ingestão de ativos.

* Use o perfil de processamento para gerar metadados personalizados usando o Serviço de computação. Consulte Metadados [personalizados usando o perfil de processamento](/help/assets/manage-metadata.md#metadata-compute-service)

* Uma experiência de download mais simples para usuários do Brand Portal que os administradores podem configurar. Consulte Visão geral [da experiência de](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/introduction/whats-new.html#download-configurations)download.

* Pré-visualizações de documentos PDF nativas e de alta fidelidade estão disponíveis no Portal de marcas. Consulte Visão geral [do visualizador de](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/introduction/whats-new.html#doc-viewer)documentos.

* Agora você pode invalidar o cache CDN (Content Delivery Network) diretamente de [!DNL Dynamic Media] dentro do AEM como Cloud Service (em vez de usar [!DNL Dynamic Media Classic]) para garantir que os ativos mais recentes sejam atendidos em minutos em vez de horas. Consulte [Invalidar o cache CDN por meio do Dynamic Media](/help/assets/dynamic-media/invalidate-cdn-cache-dynamic-media.md)

* O suporte de acessibilidade aprimorado é adicionado aos controles da interface do usuário, navegação, navegação e experiência de pesquisa no [!DNL Assets].

   * Se você pressionar a tecla Escape depois de selecionar a opção [!UICONTROL Adicionar representação] , o foco retornará à barra de ferramentas. <!-- via CQ-4293594-->
   * O foco do teclado funciona como esperado ao usar a caixa de combinação Email. <!-- via CQ-4286215 -->
   * Os elementos acordeons na seção filtros de pesquisa são interpretados como acordeões expansíveis padrão. <!-- via CQ-4273103 -->
   * Ao aplicar uma tag a um ativo, a caixa de diálogo exibe tags como elementos de árvore. Os atributos ARIA são aplicados adequadamente aos elementos de árvore para torná-los acessíveis agora. <!-- via CQ-4272964 -->

* [!DNL AEM Desktop app] A versão 2.0.3 agora está disponível, melhorando a compatibilidade com a versão [!DNL AEM] 6.5.5 [!DNL Service Pack] e atualizando a lista de compatibilidade do SO do cliente (removendo [!DNL Windows] 7 e [!DNL MacOS] versões anteriores à 10.14).

### Erros corrigidos em [!DNL Assets] {#bugs-fixed}

* A opção Relacionar e não relacionar não responde quando clicada pela primeira vez. (CQ-4299022)
* Ao baixar um ativo, se você selecionar a opção para recebê-lo por email, o email não será enviado. (CQ-4299146)

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novidades {#what-is-new-commerce}

* O recurso Console do produto agora está disponível. Isso permite que os profissionais de marketing/autores em AEM visualizações e naveguem por categorias e produtos armazenados no backend de comércio. Também é fornecido suporte para propriedades para categoria e produtos no console de produtos.

* Os seletores de produto e Categoria foram aprimorados para permitir que os profissionais de marketing selecionem o produto por SKU ou selecionem a categoria por meio da ID da categoria.

## Cloud Manager {#cloud-manager}

### Data de lançamento {#release-date-cm}

The Release Date for [!UICONTROL Cloud Manager] Version 2020.8.0 is August 06, 2020.

### Novidades {#what-is-new-cloud-manager}

* A Auditoria de conteúdo é um recurso ativado nos Pipelines de Produção de Sites do Cloud Manager. A configuração do pipeline de produção para programas com Sites agora inclui uma terceira guia chamada Auditoria **de** conteúdo. Sempre que um pipeline de produção for executado, uma nova etapa de Auditoria de conteúdo será incluída no pipeline após um teste funcional personalizado que avaliará o site em relação a várias dimensões, incluindo desempenho, SEO (Search Engine Otimization), acessibilidade, práticas recomendadas e PWA (Progressive Web App).

   >[!NOTE]
   >A Auditoria de conteúdo foi renomeada para Auditoria de experiência.

   Consulte Teste [de auditoria de](/help/implementing/cloud-manager/experience-audit-testing.md) experiência para obter mais detalhes.

* Ambientes recém-criados em programas do Assets agora serão configurados automaticamente com o Smart Content Services.

* Ambientes hibernados podem ser removidos da hibernação na página **Visão geral** do Gerenciador de nuvem.

* Capacidade de executar verificações de experiência em páginas, acionadas pelo Google Lighthouse. Como parte do pipeline do Cloud Manager, até 25 páginas podem ser verificadas e validadas em relação aos KPIs de experiência, e as pontuações são exibidas na interface do usuário do Cloud Manager.

### Correções de erros {#bug-fixes-cm}

* Alguns plug-ins SonarQube desnecessários e indesejados estavam sendo executados como parte da verificação de qualidade de código.

* Na página de execução de pipeline, o nome da ramificação estava formatado incorretamente.

* Em alguns casos, as execuções de pipeline concluídas não foram registradas com êxito como tendo sido concluídas, impedindo assim novas execuções do pipeline.

* Ocasionalmente, as execuções de pipeline ficariam *presas* devido a problemas de comunicação interna.

* Ao provisionar uma nova organização, alguns usuários com funções administrativas diferentes dos administradores de sistema receberam erroneamente acesso ao Cloud Manager.

* Em determinadas condições, o trabalho de índices de atualização foi iniciado várias vezes em paralelo, resultando em uma falha de implantação.

* A dica de ferramenta nos cartões de programa não estava consistentemente correta.

* A interface do usuário permitia erroneamente que as operações fossem tentadas em um ambiente durante sua exclusão.

* Ocorreu uma incompatibilidade de cores na página **Visão geral** do Gerenciador de nuvem.

### Problemas conhecidos {#known-issues-cm}

* As páginas inválidas são incluídas, colocando a Pontuação média de auditoria de conteúdo abaixo do que deveriam ser.

* A guia Auditoria de conteúdo exibe incorretamente o URL base usando o domínio do autor em vez do domínio de publicação.

* Para ativar a etapa Auditoria de conteúdo, os usuários devem editar o pipeline e, opcionalmente, adicionar páginas. Se nenhuma página for adicionada, a página inicial será auditada.

## Ferramenta Transferência de conteúdo {#content-transfer-tool}

Siga esta seção para saber mais sobre as novidades e as atualizações da Content Transfer Tool Release v1.0.4.

### Novidades {#what-is-new-ctt}

* A Ferramenta de transferência de conteúdo agora é compatível com o Shared S3 DataStore.

### Correções de erros {#ctt-bug-fixes}

* Tempo limite adicional adicionado para a ferramenta concluir ações.

* A interface do usuário da versão anterior às vezes exibia extração bem-sucedida mesmo se o log mostrasse erros.

## Ferramentas de refatoração de código {#code-refactoring-tools}

Siga esta seção para saber mais sobre as novidades e as atualizações das Ferramentas de Refatoração de Código.

### Novidades {#what-is-new-refactoring}

* Plug-in AIO-CLI lançado para unificar as ferramentas de refatoração de código para permitir que os desenvolvedores chamem e executem ferramentas de refatoração de código de um só lugar. Consulte Recurso [Git: aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration) para obter mais detalhes.

* AEM Dispatcher Converter expandiu para suportar conversões de configurações On-premise e Adobe Managed Services Dispatcher em AEM como configurações do Dispatcher compatíveis com Cloud Service. Consulte Recurso [Git: AEM Cloud Service Dispatcher Converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter) para obter mais detalhes.

* AEM Dispatcher Converter foi reescrito em ` node.js ` e integrado ao plug-in AIO-CLI.
