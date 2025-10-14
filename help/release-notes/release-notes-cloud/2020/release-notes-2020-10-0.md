---
title: Notas de versão do  [!DNL Adobe Experience Manager]  as a Cloud Service 2020.10.0.
description: Notas de versão do as a Cloud Service [!DNL Adobe Experience Manager] para 2020.10.0.
exl-id: ac741744-5b47-47a4-b5af-e1089e92c3f0
feature: Release Information
role: Admin
source-git-commit: 9af552b17421e320b6139d6bd6ecaa42428de397
workflow-type: tm+mt
source-wordcount: '1103'
ht-degree: 23%

---

# Notas de versão do [!DNL Adobe Experience Manager] as a Cloud Service 2020.10.0 {#release-notes}

A seção a seguir descreve as Notas de Versão gerais do [!DNL Experience Manager] as a Cloud Service 2020.10.0.

## Data de lançamento {#release-date}

A Data de Lançamento do [!DNL Adobe Experience Manager] as a Cloud Service 2020.10.0 é 28 de outubro de 2020.
A versão seguinte (2020.11.0) será lançada em 1 de dezembro de 2020.

## as a Cloud Service [!DNL Adobe Experience Manager Sites] {#sites}

### Novidades do [!DNL Sites] {#what-is-new-sites}

* **[Componentes principais 2.12.0](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=pt-BR)**: o Adobe Experience Manager as a Cloud Service se beneficia das atualizações automáticas da versão mais recente dos Componentes principais. A versão 2.12.0 inclui as melhorias mais recentes fornecidas pela comunidade. As melhorias incluem [um novo manipulador de formulário POST;](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/forms/form-container.html?lang=pt-BR#post-data) a capacidade de incluir CSS personalizado, JavaScript e [&#x200B; tags de metadados por meio da configuração com reconhecimento de contexto;](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/including-clientlibs.html?lang=pt-BR#context-aware-loading) e um utilitário [`DataLayerBuilder`](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/data-layer/integrations.html?lang=pt-BR#enabling-custom-components) para simplificar a integração da Camada de Dados Adobe em componentes personalizados. Consulte a [lista de alterações](https://github.com/adobe/aem-core-wcm-components/releases/tag/core.wcm.components.reactor-2.12.0) na 2.12.0.

* **[Arquétipo de Projeto 24](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=pt-BR)**: a base recomendada para iniciar um novo projeto do Experience Manager ficou melhor. Agora inclui a nova [Camada de Dados de Clientes Adobe](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/data-layer/overview.html?lang=pt-BR), a opção para [entregar site no AMP](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/amp.html?lang=pt-BR) e os novos [pontos de extensão para adicionar o projeto CSS/JS](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/including-clientlibs.html?lang=pt-BR#context-aware-loading).

* **[Pastas do ContextHub](/help/sites-cloud/authoring/personalization/contexthub-segmentation.md#organizing-segments)**: capacidade de criar pastas de público-alvo para organizar, localizar e selecionar facilmente segmentos de público-alvo a serem usados para os recursos de direcionamento de ofertas do ContextHub.

## as a Cloud Service [!DNL Adobe Experience Manager Assets] {#assets}

* Marcação inteligente de vídeo **[!DNL Adobe Sensei]ativada**: ao aplicar modelos de IA para analisar o conteúdo de vídeo para tags específicas de objeto e ação, os usuários do DAM podem gastar menos tempo adicionando tags e mais tempo usando informações expostas e avançadas. Por sua vez, você fornece a experiência certa aos clientes. Consulte [Ativos de vídeo de marca inteligente](/help/assets/smart-tags-for-videos.md).

* **Aprimoramentos do Brand Portal**: os novos recursos a seguir e muitos outros estão disponíveis em [!DNL Brand Portal]. Para obter detalhes, consulte as [[!DNL Brand Portal] notas de versão](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/brand-portal-release-notes.html?lang=pt-BR).

   * [Experiência aprimorada de download](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/download/brand-portal-download-assets.html?lang=pt-BR) para downloads rápidos e simplificados. Configurações adicionais de downloads podem ser configuradas por administradores para uma experiência que atenda às necessidades de usuários e empresas.
   * A navegação com um clique para Arquivos, [Coleções](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/share/brand-portal-share-collection.html?lang=pt-BR) e Links compartilhados agora é possível de qualquer página.
   * Os usuários podem [selecionar e baixar representações específicas](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/download/brand-portal-download-assets.html?lang=pt-BR#download-assets-from-asset-details-page) agora. A nova opção de download de representações está disponível no painel Representações na página de detalhes dos Ativos.
   * Um tempo limite de 15 minutos para sessões de usuários visitantes garante uma experiência otimizada a todos os usuários concomitantes.

* **[!DNL Adobe Asset Link]versão 2.1**: uma nova versão da extensão do [Adobe Asset Link](https://helpx.adobe.com/br/enterprise/using/manage-assets-using-adobe-asset-link.html) para [!DNL Adobe Photoshop], [!DNL Adobe Illustrator] e [!DNL Adobe InDesign] está disponível. Ele adiciona compatibilidade com os aplicativos [!DNL Adobe Creative Cloud] mais recentes com a versão 2021, lançada em outubro de 2020.

* **[!DNL Assets]Suporte a arquivo WebP**: [!DNL Assets] O as a Cloud Service agora oferece suporte ao formato de imagem WebP. WebP é um formato de imagem emergente criado pelo Google. As imagens no formato de arquivo WebP são visualmente indistinguíveis dos arquivos JPG ou PNG e os arquivos são muito menores. A redução do tamanho do arquivo dos ativos melhora os tempos de carregamento da página e ajuda os criadores de conteúdo a fornecer uma experiência mais rápida na Web. Veja como usar o WebP em [criar perfil de processamento](/help/assets/asset-microservices-configure-and-use.md#create-standard-profile).

## as a Cloud Service [!DNL Adobe Experience Manager Forms] {#forms-oct-2021}

### Novidades do [!DNL Forms] {#what-is-new-forms-oct-2021}

* **Analytics para Forms adaptável**: agora é possível capturar e rastrear o comportamento de logon e não logon (anônimo) por meio do Adobe Analytics para Forms adaptável para coletar insights do usuário. Ele ajuda os usuários empresariais a tomar decisões informadas sobre o conteúdo, o layout e o estilo do formulário adaptável com base nos insights coletados.

### Novos recursos disponíveis no canal de pré-lançamento do [!DNL Forms] {#prerelease-features-forms-oct-2021}

* **Externalizar dados do Fluxo de Trabalho do AEM para processamento seguro**: Você pode armazenar dados de variáveis de Fluxo de Trabalho em andamento do AEM que contenham elementos de Dados Pessoais Sensíveis (SPD) em um repositório gerenciado pelo cliente para processamento seguro. Durante o processamento do fluxo de trabalho, os dados armazenados nas variáveis de fluxo de trabalho não são mantidos no repositório do AEM. Ele é obtido sob demanda do repositório gerenciado pelo cliente.

### Recursos do Beta de [!DNL Forms]  {#sep-what-is-new-forms-oct-prerelease}

* **[!DNL AEM Forms as a Cloud Service - Communications]**: [APIs de comunicação](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications.html?lang=pt-BR) ajudam a combinar os modelos e os dados XML para gerar documentos em vários formatos. O serviço permite gerar documentos em modo sincronizado e em lote.

Você pode enviar um email a [!DNL formscsbeta@adobe.com] para se cadastrar no programa beta.

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novidades {#what-is-new-commerce}

* Lançamento do site de referência CIF Venia - 2020.10.2 que inclui a versão mais recente dos componentes principais do CIF v1.4.0. Consulte [Site de referência CIF Venia](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2020.10.2) para obter mais detalhes.

* Lançamento de componentes principais do CIF v1.4.0. Consulte [Componentes principais do CIF](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.4.0) para obter mais detalhes.

### Correções de erros {#bug-fixes-commerce}

* As solicitações do GraphQL que estavam no Console do produto e os seletores foram feitas por meio de HTTP POST. Esse problema foi corrigido para garantir que o cliente Apollo GraphQL respeite a configuração na configuração OSGi do cliente GraphQL para suportar solicitações GET, se estiver configurada.

* A interface de configuração do CIF Cloud exibia botões &quot;Salvar e fechar&quot; para configurações em /lib e /apps/. Mas essas interfaces são somente leitura, portanto, a interface foi corrigida para exibir apenas o botão &quot;Fechar&quot;.

## Cloud Manager {#cloud-manager}

### Data de lançamento {#release-date-cm}

A data de lançamento do Cloud Manager no Experience Manager as a Cloud Service 2020.10.0 é 2 de outubro de 2020.

### Novidades do [!DNL Cloud Manager] {#what-is-new-cm}

* A página de ambientes foi renovada.

* A página de ambientes hibernados agora mostra um status discreto no Cloud Manager.

* O &quot;build container&quot; do Cloud Manager agora é compatível com a compilação de projetos usando Java™ 8 ou Java™ 11. O suporte ao Java™ 11 é fornecido pelo sistema de cadeias de ferramentas Maven.

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

* Foi adicionado suporte para pesquisar instâncias de fluxo de trabalho com base no Título do fluxo de trabalho, Modelo do fluxo de trabalho, Status, Iniciador, Caminho da carga e Data de início. Consulte [Pesquisar Instâncias do Fluxo de Trabalho](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/administering/workflows-administering.html?lang=pt-BR).

## Ferramenta Transferência de conteúdo {#content-transfer-tool}

Saiba mais sobre as novidades e atualizações da [Ferramenta de Transferência de Conteúdo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?lang=pt-BR) Versão v1.1.12.

### Novidades {#what-is-new-ctt}

* Experiência do usuário para logs aprimorada. Carimbos de data e hora adicionados aos logs de Extração e assimilação. Mensagem adicionada para indicar se os logs estão vazios.

### Correções de erros {#ctt-bug-fixes}

* A Ferramenta de transferência de conteúdo ignorava arquivos de conteúdo se o conjunto de migração contivesse caminhos com nomes de arquivo parcialmente semelhantes.
