---
title: Notas de versão do  [!DNL Adobe Experience Manager]  as a Cloud Service 2020.10.0.
description: "[!DNL Adobe Experience Manager] Notas de versão as a Cloud Service para 2020.10.0."
exl-id: ac741744-5b47-47a4-b5af-e1089e92c3f0
feature: Release Information
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '1103'
ht-degree: 23%

---

# Notas de versão do [!DNL Adobe Experience Manager] as a Cloud Service 2020.10.0 {#release-notes}

A seção a seguir descreve as Notas de versão gerais do [!DNL Experience Manager] as a Cloud Service 2020.10.0.

## Data de lançamento {#release-date}

A data de lançamento do [!DNL Adobe Experience Manager] O as a Cloud Service 2020.10.0 é 28 de outubro de 2020.
A versão seguinte (2020.11.0) será lançada em 1 de dezembro de 2020.

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

### Novidades do [!DNL Sites] {#what-is-new-sites}

* **[Componentes principais 2.12.0](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=pt-BR)**: o Adobe Experience Manager as a Cloud Service se beneficia de atualizações automáticas para a versão mais recente dos Componentes principais. A versão 2.12.0 inclui as melhorias mais recentes fornecidas pela comunidade. As melhorias incluem [um novo manipulador de formulários POST;](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/forms/form-container.html#post-data) a capacidade de incluir CSS personalizado, JavaScript e metadados [tags por meio da configuração com reconhecimento de contexto;](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/including-clientlibs.html#context-aware-loading) e uma [`DataLayerBuilder`](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/data-layer/integrations.html#enabling-custom-components) para simplificar a integração da Camada de dados Adobe em componentes personalizados. Consulte a [lista de alterações](https://github.com/adobe/aem-core-wcm-components/releases/tag/core.wcm.components.reactor-2.12.0) na versão 2.12.0.

* **[Arquétipo de Projeto 24](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=pt-BR)**: a base recomendada para iniciar um novo projeto Experience Manager ficou melhor. Agora inclui o novo [Camada de dados de clientes Adobe](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/data-layer/overview.html?lang=pt-BR), opção para [site de entrega no AMP,](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/amp.html) e novos [pontos de extensão para adicionar o projeto CSS/JS.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/including-clientlibs.html#context-aware-loading)

* **[Pastas do ContextHub](/help/sites-cloud/authoring/personalization/contexthub-segmentation.md#organizing-segments)**: capacidade de criar pastas de público-alvo para organizar, localizar e selecionar segmentos de público-alvo facilmente para usar nos recursos de direcionamento de ofertas do ContextHub.

## [!DNL Adobe Experience Manager Assets] as a Cloud Service {#assets}

* **[!DNL Adobe Sensei]marcação inteligente de vídeo ativada**: ao aplicar modelos de IA para analisar o conteúdo de vídeo para tags específicas de objeto e ação, os usuários do DAM podem gastar menos tempo adicionando tags e mais tempo usando as informações ricas e expostas. Por sua vez, você fornece a experiência certa aos clientes. Consulte [Ativos de vídeo de tag inteligente](/help/assets/smart-tags-video-assets.md).

* **Aprimoramentos do Brand Portal**: os novos recursos a seguir e muitos outros estão disponíveis em [!DNL Brand Portal]. Para obter detalhes, consulte [[!DNL Brand Portal] notas de versão](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/brand-portal-release-notes.html).

   * [Experiência aprimorada de download](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/download/brand-portal-download-assets.html) para downloads rápidos e simplificados. Configurações adicionais de downloads podem ser configuradas por administradores para uma experiência que atenda às necessidades de usuários e empresas.
   * Navegação até os Arquivos com um clique, [Coleções](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/share/brand-portal-share-collection.html)O e os Links compartilhados agora são possíveis de qualquer página.
   * Os usuários podem [selecionar e baixar representações específicas](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/download/brand-portal-download-assets.html#download-assets-from-asset-details-page) agora. A nova opção de download de representações está disponível no painel Representações na página de detalhes dos Ativos.
   * Um tempo limite de 15 minutos para sessões de usuários visitantes garante uma experiência otimizada a todos os usuários concomitantes.

* **[!DNL Adobe Asset Link]versão 2.1**: uma nova versão do [Adobe Asset Link](https://helpx.adobe.com/br/enterprise/using/manage-assets-using-adobe-asset-link.html) extensão para [!DNL Adobe Photoshop], [!DNL Adobe Illustrator], e [!DNL Adobe InDesign] está disponível. Ele adiciona compatibilidade com o mais recente [!DNL Adobe Creative Cloud] aplicativos com a versão 2021, lançada em outubro de 2020.

* **[!DNL Assets]Suporte a arquivo WebP**: [!DNL Assets] O as a Cloud Service agora é compatível com o formato de imagem WebP. WebP é um formato de imagem emergente criado pelo Google. As imagens no formato de arquivo WebP são visualmente indistinguíveis dos arquivos JPG ou PNG e os arquivos são muito menores. A redução do tamanho do arquivo dos ativos melhora os tempos de carregamento da página e ajuda os criadores de conteúdo a fornecer uma experiência mais rápida na Web. Veja como usar o WebP no [criar perfil de processamento](/help/assets/asset-microservices-configure-and-use.md#create-standard-profile).

## [!DNL Adobe Experience Manager Forms] as a Cloud Service {#forms-oct-2021}

### Novidades do [!DNL Forms] {#what-is-new-forms-oct-2021}

* **Analytics para Forms adaptável**: agora é possível capturar e rastrear o comportamento de logado e não conectado (anônimo) por meio do Adobe Analytics for Adaptive Forms para coletar insights do usuário. Ele ajuda os usuários empresariais a tomar decisões informadas sobre o conteúdo, o layout e o estilo do formulário adaptável com base nos insights coletados.

### Novos recursos disponíveis no canal de pré-lançamento do [!DNL Forms] {#prerelease-features-forms-oct-2021}

* **Externalizar dados do fluxo de trabalho do AEM para processamento seguro**: você pode armazenar dados de variáveis do fluxo de trabalho de AEM em andamento que contêm elementos de Dados pessoais confidenciais (SPD) em um repositório gerenciado pelo cliente para processamento seguro. Durante o processamento do workflow, os dados armazenados nas variáveis do workflow não são mantidos no repositório do AEM. Ele é obtido sob demanda do repositório gerenciado pelo cliente.

### Recursos beta do [!DNL Forms] {#sep-what-is-new-forms-oct-prerelease}

* **[!DNL AEM Forms as a Cloud Service - Communications]**: [APIs de comunicação](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications.html) ajuda a combinar um modelo e dados XML para gerar documentos em vários formatos. O serviço permite gerar documentos em modo sincronizado e em lote.

Você pode escrever para [!DNL formscsbeta@adobe.com] para se inscrever no programa beta.

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novidades {#what-is-new-commerce}

* Lançamento do site de referência CIF Venia - 2020.10.2 que inclui a versão mais recente dos componentes principais CIF v1.4.0. Consulte [Site de referência CIF Venia](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2020.10.2) para obter mais detalhes.

* Lançamento de componentes principais de CIF v1.4.0. Consulte [Componentes principais do CIF](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.4.0) para obter mais detalhes.

### Correções de erros {#bug-fixes-commerce}

* As solicitações do GraphQL que estavam no Console do produto e os seletores foram feitas por meio do POST HTTP. Esse problema foi corrigido para garantir que o cliente Apollo GraphQL respeite a configuração na configuração OSGi do cliente GraphQL para suportar solicitações GET, se estiver configurada.

* A interface de configuração do CIF Cloud exibia botões &quot;Salvar e fechar&quot; para configurações em /lib e /apps/. Mas essas interfaces são somente leitura, portanto, a interface foi corrigida para exibir apenas o botão &quot;Fechar&quot;.

## Cloud Manager {#cloud-manager}

### Data de lançamento {#release-date-cm}

A data de lançamento do Cloud Manager no Experience Manager as a Cloud Service 2020.10.0 é 2 de outubro de 2020.

### Novidades do [!DNL Cloud Manager] {#what-is-new-cm}

* A página de ambientes foi renovada.

* A página de ambientes hibernados agora mostra um status discreto no Cloud Manager.

* O &quot;contêiner de criação&quot; do Cloud Manager agora é compatível com a compilação de projetos usando Java™ 8 ou Java™ 11. O suporte ao Java™ 11 é fornecido pelo sistema de cadeias de ferramentas Maven.

* O número de variáveis por ambiente aumentou para 200.

* O cartão Ambiente na página Visão geral agora lista até três ambientes. Os usuários podem selecionar o botão **Mostrar tudo** para navegar até a página de resumo do ambiente a fim de exibir uma tabela com uma lista completa de ambientes.
Consulte [Exibição de ambiente](/help/implementing/cloud-manager/manage-environments.md#viewing-environment) para obter mais detalhes.

### Correções de erros {#bug-fixes-cloud-manager}

* Devido a um erro, o link do Cloud Manager para o Console do desenvolvedor estava ativo antes dos ambientes serem totalmente criados.

* O link direto do Cloud Manager para o Console do desenvolvedor não exibia a opção de cancelar hibernação/hibernar para ambientes do Programa de sandbox.

* Os botões Cancelar e Salvar nem sempre estavam visíveis na página de edição do pipeline de não produção.

* Certas falhas no processo de qualidade do código podiam resultar na geração incorreta do arquivo de log.

* Às vezes, o nome sugerido na criação de um programa retornava uma duplicata de um nome de programa existente.

* Grandes logs de etapas de pipeline não podiam ser baixados consistentemente pela interface do usuário.

* A validação de nomes de ambientes apresentava um erro off-by-one.

* A página Ambientes às vezes mostrava segmentos do Publish e do Dispatcher sem que estivessem presentes.

## Adobe Experience Manager as a Cloud Service Foundation {#cloud-service-foundation}

### Fluxos de trabalhos {#workflows}

* Foi adicionado suporte para pesquisar instâncias de fluxo de trabalho com base no Título do fluxo de trabalho, Modelo do fluxo de trabalho, Status, Iniciador, Caminho da carga e Data de início. Consulte [Pesquisar instâncias de fluxo de trabalho](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/administering/workflows-administering.html).

## Ferramenta Transferência de conteúdo {#content-transfer-tool}

Saiba mais sobre as novidades e atualizações do [Ferramenta Transferência de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html) Versão v1.1.12.

### Novidades {#what-is-new-ctt}

* Experiência do usuário para logs aprimorada. Carimbos de data e hora adicionados aos logs de Extração e assimilação. Mensagem adicionada para indicar se os logs estão vazios.

### Correções de erros {#ctt-bug-fixes}

* A Ferramenta de transferência de conteúdo ignorava arquivos de conteúdo se o conjunto de migração contivesse caminhos com nomes de arquivo parcialmente semelhantes.
