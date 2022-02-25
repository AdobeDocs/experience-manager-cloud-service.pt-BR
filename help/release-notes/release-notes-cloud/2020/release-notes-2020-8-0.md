---
title: Notas de versão do  [!DNL Adobe Experience Manager] as a Cloud Service 2020.8.0.
description: '"[!DNL Adobe Experience Manager] Notas de versão as a Cloud Service para 2020.8.0."'
exl-id: 83413130-ae90-4419-bcf7-42fdc740452b
source-git-commit: bc4da79735ffa99f8c66240bfbfd7fcd69d8bc13
workflow-type: tm+mt
source-wordcount: '1046'
ht-degree: 7%

---

# Notas de versão do [!DNL Adobe Experience Manager] as a Cloud Service 2020.8.0 {#release-notes}

A seção a seguir descreve as Notas de versão gerais do Experience Manager as a Cloud Service 2020.8.0.


## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

### Novidades do [!DNL Sites] {#what-is-new-sites}

* Capacidade de [restaurar páginas e subpáginas (árvores de página) para uma versão anterior](/help/sites-cloud/authoring/features/page-versions.md#reinstating-versions).

* Capacidade de [criar lançamentos](/help/sites-cloud/authoring/launches/overview.md) em AEM [Editor de SPA.](/help/implementing/developing/hybrid/introduction.md)


## [!DNL Adobe Experience Manager Assets] as a Cloud Service {#assets}

### Novidades do [!DNL Assets] {#what-is-new-assets}

* A transcodificação de vídeo agora é compatível com microsserviços de ativos. Uma nova seção na [!UICONTROL Processando perfis] a configuração permite definir a taxa de bits e as dimensões do vídeo. O formato de saída é MP4 com codec H.264. Para obter detalhes, consulte [gerenciar ativos de vídeo](/help/assets/manage-video-assets.md#transcode-video). Para obter mais opções de transcodificação e para a entrega de vídeo, use [!DNL Dynamic Media] complemento.

* Em novos [!DNL Experience Manager Assets] implantações, a funcionalidade de marcação inteligente agora é configurada por padrão. Não é necessário integrar manualmente com [!DNL Adobe Developer Console]. Em implantações existentes, os administradores configuram a integração de tags inteligentes como antes.

* Um novo [experiência de download de ativos](/help/assets/download-assets-from-aem.md) permite,

   * Download assíncrono de downloads grandes para que os usuários não precisem esperar.
   * Uma nova API modular para extensibilidade do desenvolvedor.

* A extração de metadados para microsserviços de ativos tem um desempenho aprimorado. Isso aumenta a taxa de transferência geral da assimilação de ativos.

* Use um perfil de processamento para gerar metadados personalizados usando o Serviço de computação. Consulte [Metadados personalizados usando o perfil de processamento](/help/assets/manage-metadata.md#metadata-compute-service).

* Uma experiência de download mais simples para usuários do Brand Portal que os administradores podem configurar. Consulte [visão geral da experiência de download](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/whats-new.html#download-configurations).

* As visualizações de documento do PDF nativo e de alta fidelidade agora estão disponíveis no Brand Portal. Consulte [visão geral do visualizador de documentos](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/whats-new.html#doc-viewer).

* Agora você pode invalidar o cache CDN (Content Delivery Network) diretamente de [!DNL Dynamic Media] em AEM as a Cloud Service (em vez de usar [!DNL Dynamic Media Classic]). Isso garante que os ativos mais recentes sejam disponibilizados em minutos em vez de horas. Consulte [Invalidar o cache do CDN por meio do Dynamic Media](/help/assets/dynamic-media/invalidate-cdn-cache-dynamic-media.md).

* O suporte de acessibilidade aprimorado é adicionado aos controles da interface do usuário, navegação, navegação e experiência de pesquisa no [!DNL Assets].

   * Se você pressionar a tecla Escape depois de selecionar [!UICONTROL Adicionar representação] , o foco retorna à barra de ferramentas. <!-- via CQ-4293594-->
   * O foco do teclado funciona conforme o esperado ao usar a caixa de combinação Email . <!-- via CQ-4286215 -->
   * Os elementos acordeões na seção Filtros de pesquisa são interpretados como opções expansíveis padrão. <!-- via CQ-4273103 -->
   * Ao aplicar uma tag a um ativo, a caixa de diálogo exibe tags como elementos de árvore. Os atributos ARIA são aplicados adequadamente aos elementos da árvore para torná-los acessíveis agora. <!-- via CQ-4272964 -->

* [!DNL AEM Desktop app] A versão 2.0.3 já está disponível. Melhora a compatibilidade com o [!DNL Experience Manager] 6.5.5 service pack e tem uma lista atualizada de compatibilidade do SO cliente. [!DNL Windows] 7 e [!DNL macOS] versões anteriores à 10.14 não são compatíveis.

### Erros corrigidos em [!DNL Assets] {#bugs-fixed}

* A opção Relate and unrelated não responde ao clicar pela primeira vez. (CQ-4299022)
* Ao baixar um ativo, se você selecionar a opção para recebê-lo por email, o email não será enviado. (CQ-4299146)

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novidades {#what-is-new-commerce}

* O recurso Console do produto agora está disponível. Isso permite que profissionais de marketing/autores no AEM visualizem e naveguem em categorias e produtos armazenados no backend de comércio. Também é fornecido suporte para propriedades de categorias e produtos no Console do produto .

* Os seletores de produto e categoria foram aprimorados para permitir que os profissionais de marketing selecionem o produto via SKU ou selecionem a categoria por meio da ID da categoria.

## Cloud Manager {#cloud-manager}

### Data de lançamento {#release-date-cm}

A data de lançamento para [!UICONTROL Cloud Manager] A versão 2020.8.0 é 6 de agosto de 2020.

### Novidades {#what-is-new-cloud-manager}

* A Auditoria de conteúdo é um recurso ativado nos Pipelines de produção de sites do Cloud Manager. A configuração Pipeline de produção para programas com Sites agora inclui uma terceira guia chamada **Auditoria de conteúdo**. Sempre que um pipeline de produção for executado, uma nova etapa de Auditoria de conteúdo será incluída no pipeline após um teste funcional personalizado que avaliará o site em relação a várias dimensões, incluindo desempenho, SEO (Otimização de mecanismo de pesquisa), acessibilidade, práticas recomendadas e PWA (Aplicativo web progressivo).


   >[!NOTE]
   >A Auditoria de conteúdo foi renomeada para Auditoria de experiência.

   Consulte [Teste de auditoria de experiência](/help/implementing/cloud-manager/experience-audit-testing.md) para obter mais detalhes.

* Os ambientes recém-criados nos programas do Assets agora serão configurados automaticamente com os Serviços de conteúdo inteligente.

* Ambientes hibernados podem ser removidos da hibernação no do Cloud Manager **Visão geral** página.

* Capacidade de executar verificações de experiência em páginas, acionadas pelo Google Lighthouse. Como parte do pipeline do Cloud Manager , até 25 páginas podem ser verificadas e validadas em relação aos KPIs de experiência, e as pontuações são exibidas na interface do usuário do Cloud Manager.

### Correções de erros {#bug-fixes-cm}

* Alguns plug-ins desnecessários e indesejados do SonarQube estavam sendo executados como parte da verificação de qualidade do código.

* Na página de execução do pipeline, o nome da ramificação estava formatado incorretamente.

* Em alguns casos, as execuções de pipeline concluídas não foram registradas com êxito como tendo sido concluídas, impedindo assim novas execuções do pipeline.

* Ocasionalmente, as execuções de pipeline receberiam *preso* devido a problemas de comunicação interna.

* Ao provisionar uma nova organização, alguns usuários com funções administrativas diferentes dos administradores de sistema receberam erroneamente acesso ao Cloud Manager.

* Sob determinadas condições, o trabalho de índices de atualização foi iniciado várias vezes em paralelo, resultando em uma falha de implantação.

* A dica de ferramenta nos cartões de programa não estava consistentemente correta.

* A interface do usuário permitiu erroneamente que as operações fossem tentadas em um ambiente enquanto eram excluídas.

* Havia uma incompatibilidade de cores no Cloud Manager **Visão geral** página.

### Problemas conhecidos {#known-issues-cm}

* Páginas inválidas são incluídas, trazendo a Pontuação média de auditoria de conteúdo abaixo do que deveriam ser.

* A guia Auditoria de conteúdo exibe incorretamente o URL base usando o domínio do autor em vez do domínio de publicação.

* Para ativar a etapa Auditoria de conteúdo , os usuários devem editar o pipeline e, opcionalmente, adicionar páginas. Se nenhuma página for adicionada, a página inicial será auditada.

## Ferramenta Transferência de conteúdo {#content-transfer-tool}

Siga esta seção para saber mais sobre as novidades e as atualizações da versão v1.0.4 da ferramenta Transferência de conteúdo.

### Novidades {#what-is-new-ctt}

* A ferramenta Transferência de conteúdo agora é compatível com o DataStore S3 compartilhado.

### Correções de erros {#ctt-bug-fixes}

* Adição de tempos limite adicionais para que a ferramenta conclua as ações.

* A interface de usuário da versão anterior às vezes exibia extração bem-sucedida, mesmo que o log mostrasse erros.

## Ferramentas de refatoração de código {#code-refactoring-tools}

Siga esta seção para saber mais sobre as novidades e as atualizações das Ferramentas de refatoração de código.

### Novidades {#what-is-new-refactoring}

* Lançamento do plug-in AIO-CLI para unificar as ferramentas de refatoração de código para permitir que os desenvolvedores chamem e executem ferramentas de refatoração de código de um só lugar. Consulte [Recurso Git: aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration) para obter mais detalhes.

* AEM o Dispatcher Converter foi estendido para suportar conversões de configurações no local e do Adobe Managed Services Dispatcher em AEM configurações do Dispatcher compatíveis com as a Cloud Service. Consulte [Recurso Git: Conversor do Dispatcher do AEM Cloud Service](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter) para obter mais detalhes.

* AEM Dispatcher Converter reescrito em ` node.js ` e integrado ao plug-in AIO-CLI.
