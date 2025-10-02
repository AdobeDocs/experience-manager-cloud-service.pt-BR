---
title: Notas de versão do  [!DNL Adobe Experience Manager]  as a Cloud Service 2020.8.0.
description: Notas de versão do as a Cloud Service [!DNL Adobe Experience Manager] para 2020.8.0.
exl-id: 83413130-ae90-4419-bcf7-42fdc740452b
feature: Release Information
role: Admin
source-git-commit: 2aea79d42ef9627a8fc758077a7ee012592888d7
workflow-type: tm+mt
source-wordcount: '1031'
ht-degree: 34%

---

# Notas de versão do [!DNL Adobe Experience Manager] as a Cloud Service 2020.8.0 {#release-notes}

A seção a seguir descreve as Notas de versão gerais do Experience Manager as a Cloud Service 2020.8.0.


## as a Cloud Service [!DNL Adobe Experience Manager Sites] {#sites}

### Novidades do [!DNL Sites] {#what-is-new-sites}

* Capacidade de [restaurar páginas e subpáginas (árvores de página) para uma versão anterior](/help/sites-cloud/authoring/sites-console/page-versions.md#reinstating-versions).

* Capacidade de [criar Inicializações](/help/sites-cloud/authoring/launches/overview.md) no [Editor SPA](/help/implementing/developing/hybrid/introduction.md) do AEM.


## as a Cloud Service [!DNL Adobe Experience Manager Assets] {#assets}

### Novidades do [!DNL Assets] {#what-is-new-assets}

* A transcodificação de vídeo agora é compatível com os microsserviços de ativos. Uma nova seção na configuração [!UICONTROL Processando Perfis] permite definir a taxa de bits e as dimensões do vídeo. O formato de saída é MP4 com codec H.264. Para obter detalhes, consulte [gerenciar ativos de vídeo](/help/assets/manage-video-assets.md#transcode-video). Para obter mais opções de transcodificação e entrega de vídeo, use o complemento [!DNL Dynamic Media].

* Nas novas implantações do [!DNL Experience Manager Assets], a funcionalidade de marcação inteligente agora está configurada por padrão. Não é necessário integrar manualmente com [!DNL Adobe Developer Console]. Em implantações existentes, os administradores configuram a integração de tags inteligentes como antes.

* Uma nova [experiência de download de ativos](/help/assets/download-assets-from-aem.md) permite,

   * Download assíncrono para downloads grandes para que os usuários não precisem aguardar.
   * Uma nova API modular para extensibilidade do desenvolvedor.

* A extração de metadados para microsserviços de ativos melhorou o desempenho. Isso aumenta a taxa de transferência geral da assimilação de ativos.

* Use um perfil de processamento para gerar metadados personalizados usando o Serviço de computação. Consulte [Metadados personalizados usando o perfil de processamento](/help/assets/manage-metadata.md#metadata-compute-service).

* Uma experiência de download mais simples para usuários do Brand Portal que os administradores podem configurar. Consulte [visão geral da experiência de download](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/whats-new.html#download-configurations).

* Visualizações de documentos nativos e de alta fidelidade do PDF agora estão disponíveis no Brand Portal. Consulte [visão geral do visualizador de documentos](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/whats-new.html#doc-viewer).

* Agora você pode invalidar o cache CDN (Content Delivery Network) diretamente do [!DNL Dynamic Media] no AEM as a Cloud Service (em vez de usar [!DNL Dynamic Media Classic]). Ele garante que os ativos mais recentes sejam disponibilizados em minutos em vez de horas. Consulte [Invalidar o cache CDN por meio do Dynamic Media](/help/assets/dynamic-media/invalidate-cdn-cache-dynamic-media.md).

* O suporte de acessibilidade aprimorado foi adicionado aos controles da interface do usuário, navegação, navegação e experiência de pesquisa no [!DNL Assets].

   * Se você pressionar a tecla Escape depois de selecionar a opção [!UICONTROL Adicionar representação], o foco retornará à barra de ferramentas. <!-- via CQ-4293594-->
   * O foco do teclado funciona conforme esperado ao usar a caixa de combinação Email. <!-- via CQ-4286215 -->
   * Os elementos de acordeões na seção filtros de pesquisa são interpretados como acordeões expansíveis padrão. <!-- via CQ-4273103 -->
   * Ao aplicar uma tag a um ativo, a caixa de diálogo exibe tags como elementos de árvore. Os atributos ARIA são aplicados adequadamente aos elementos da árvore para torná-los acessíveis agora. <!-- via CQ-4272964 -->

* A versão 2.0.3 do [!DNL AEM Desktop app] já está disponível. Ele melhora a compatibilidade com o [!DNL Experience Manager] 6.5.5 service pack e tem uma lista atualizada de compatibilidade do SO cliente. Não há suporte para as versões do [!DNL Windows] 7 e do [!DNL macOS] anteriores à 10.14.

### Bugs corrigidos em [!DNL Assets] {#bugs-fixed}

* A opção Relacionar e não relacionar não responde quando clicada pela primeira vez. (CQ-4299022)
* Ao baixar um ativo, se você selecionar a opção para recebê-lo por email, o email não será enviado. (CQ-4299146)

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novidades {#what-is-new-commerce}

* O recurso Console do produto agora está disponível. Isso permite que profissionais de marketing/autores no AEM visualizem e naveguem categorias e produtos armazenados no back-end de comércio. Também é fornecido suporte a propriedades de categorias e produtos no Console do produto.

* Os seletores de categoria e produto foram aprimorados para permitir que os profissionais de marketing selecionem o produto via SKU ou selecionem a categoria por meio da ID da categoria.

## Cloud Manager {#cloud-manager}

### Data de lançamento {#release-date-cm}

A data de lançamento da versão 2020.8.0 do [!UICONTROL Cloud Manager] é sexta-feira, 6 de agosto de 2020.

### Novidades {#what-is-new-cloud-manager}

* A Auditoria de conteúdo é um recurso habilitado nos pipelines de produção do Sites do Cloud Manager. A configuração do pipeline de produção para programas com Sites agora inclui uma terceira guia chamada **Auditoria de conteúdo**. Sempre que um pipeline de produção é executado, uma nova etapa da Auditoria de conteúdo é incluída no pipeline após um teste funcional personalizado que avalia o site em relação a várias dimensões, incluindo desempenho, SEO (Otimização de mecanismo de pesquisa), acessibilidade, práticas recomendadas e PWA (Aplicativo web progressivo).


  >[!NOTE]
  >A Auditoria de conteúdo foi renomeada para Auditoria de experiência.

  Consulte [Teste de auditoria de experiência](/help/implementing/cloud-manager/reports/report-experience-audit.md) para obter mais detalhes.

* Os ambientes recém-criados nos programas do Assets agora serão configurados automaticamente com os Serviços de conteúdo inteligente.

* Os ambientes hibernados podem ter a hibernação cancelada na página **Visão geral** do Cloud Manager.

* Capacidade de executar verificações de experiência em páginas, possibilitadas pelo Google Lighthouse. Como parte do pipeline do Cloud Manager, até 25 páginas podem ser verificadas e validadas em relação aos KPIs de experiência, e as pontuações são exibidas na interface do usuário do Cloud Manager.

### Correções de erros {#bug-fixes-cm}

* Alguns plug-ins desnecessários e indesejados do SonarQube eram executados como parte da verificação de qualidade do código.

* Na página de execução do pipeline, o nome da ramificação era formatado incorretamente.

* Em alguns casos, as execuções de pipeline concluídas não eram registradas com sucesso como concluídas, impedindo assim novas execuções do pipeline.

* Ocasionalmente, as execuções de pipeline eram *interrompidas* devido a problemas de comunicação interna.

* Ao provisionar uma nova organização, alguns usuários com funções administrativas diferentes da dos administradores do sistema recebiam erroneamente acesso ao Cloud Manager.

* Em determinadas condições, o trabalho de atualização de índices era iniciado várias vezes em paralelo, resultando em uma falha de implantação.

* A dica de ferramenta nos cartões de programa não era exibida corretamente de forma consistente.

* A interface do usuário permitia erroneamente que as operações fossem tentadas em um ambiente enquanto ele era excluído.

* As cores não correspondiam na página **Visão geral** do Cloud Manager.

### Problemas conhecidos {#known-issues-cm}

* Páginas inválidas eram incluídas, colocando a pontuação média da auditoria de conteúdo abaixo do que deveriam ser.

* A guia Auditoria de conteúdo exibia incorretamente a URL de base usando o domínio do autor em vez de o domínio de publicação.

* Para ativar a etapa Auditoria de conteúdo, os usuários precisam editar o pipeline e também podem adicionar páginas. Se nenhuma página for adicionada, a página inicial será auditada.

## Ferramenta de transferência de conteúdo {#content-transfer-tool}

Siga esta seção para saber mais sobre as novidades e atualizações da Ferramenta de transferência de conteúdo versão v1.0.4.

### Novidades {#what-is-new-ctt}

* A ferramenta Transferência de conteúdo agora é compatível com o Shared S3 DataStore.

### Correções de erros {#ctt-bug-fixes}

* Foram adicionados tempos limite adicionais para a ferramenta concluir ações.

* Às vezes, a interface da versão anterior exibia uma extração bem-sucedida, mesmo que o log mostrasse erros.

## Ferramentas de refatoração de código {#code-refactoring-tools}

Siga esta seção para saber mais sobre as novidades e atualizações das Ferramentas de refatoração de código.

### Novidades {#what-is-new-refactoring}

* Lançamento do plug-in AIO-CLI para unificar as ferramentas de refatoração de código para permitir que os desenvolvedores chamem e executem ferramentas de refatoração de código de um só lugar. Consulte [Recurso do Git: aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration) para obter mais detalhes.

* O AEM Dispatcher Converter foi estendido para aceitar conversões de configurações no local e do Adobe Managed Services Dispatcher em configurações do AEM as a Cloud Service compatíveis com o Dispatcher. Consulte [Recurso do Git: AEM Cloud Service Dispatcher Converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter) para obter mais detalhes.

* O AEM Dispatcher Converter foi regravado em ` node.js ` e integrado ao plug-in AIO-CLI.
