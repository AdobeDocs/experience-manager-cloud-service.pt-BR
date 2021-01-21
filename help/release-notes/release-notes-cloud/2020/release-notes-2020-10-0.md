---
title: Notas de versão do  [!DNL Adobe Experience Manager] as a Cloud Service 2020.10.0.
description: '[!DNL Adobe Experience Manager] como notas de versão de Cloud Service para 2020.10.0.'
translation-type: tm+mt
source-git-commit: 13774cc8684166c98f85bf4096d2c7de8d257746
workflow-type: tm+mt
source-wordcount: '1044'
ht-degree: 18%

---


# Notas de versão do [!DNL Adobe Experience Manager] as a Cloud Service 2020.10.0 {#release-notes}

A seção a seguir descreve as Notas de versão gerais de [!DNL Experience Manager] como um Cloud Service 2020.10.0.

## Data de lançamento {#release-date}

A data de lançamento para [!DNL Adobe Experience Manager] como Cloud Service 2020.10.0 é 28 de outubro de 2020.
A seguinte versão (2020.11.0) será lançada em 1º de dezembro de 2020.

## [!DNL Adobe Experience Manager Sites] como um Cloud Service  {#sites}

### Novidades em [!DNL Sites] {#what-is-new-sites}

* **[Componentes principais 2.12.0](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html)**: A AEM como Cloud Service beneficia-se de atualizações automáticas para a versão mais recente dos Componentes principais. A versão 2.12.0 inclui as melhorias mais recentes que a comunidade contribuiu, como [um novo manipulador de formulários de POST;](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/forms/form-container.html#post-data) a capacidade de incluir tags personalizadas CSS, Javascript e metadados [por meio de configuração sensível ao contexto;](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/including-clientlibs.html#context-aware-loading) e um utilitário [`DataLayerBuilder`](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/data-layer/integrations.html#enabling-custom-components) para simplificar a integração da Camada de dados de Adobe nos componentes personalizados. Consulte a lista [de alterações](https://github.com/adobe/aem-core-wcm-components/releases/tag/core.wcm.components.reactor-2.12.0) em 2.12.0.

* **[Tipo de Arquivo do Projeto 24](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)**: A base recomendada para start de um novo projeto AEM melhorou, agora incluindo a nova Camada [ de Dados do Cliente ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/data-layer/overview.html)Adobe, a opção de  [fornecer site na AMP ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/amp.html) e novos pontos de  [extensão para adicionar CSS/JS do projeto.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/including-clientlibs.html#context-aware-loading)

* **[Pastas](/help/sites-cloud/authoring/personalization/contexthub-segmentation.md#organizing-segments)** do ContextHub: Capacidade de criar pastas de audiência para organizar, localizar e selecionar facilmente segmentos de audiência a serem usados para recursos de direcionamento de oferta do ContextHub.

## [!DNL Adobe Experience Manager Assets] como um Cloud Service  {#assets}

* **[!DNL Adobe Sensei]Marcação** inteligente de vídeo: Ao utilizar modelos do AI para analisar o conteúdo de vídeo para tags de objeto e ação específicas, os usuários do DAM podem gastar menos tempo adicionando tags e mais tempo usando as informações avançadas expostas para fornecer a experiência certa aos clientes. Consulte [Ativos de vídeo de tags inteligentes](/help/assets/smart-tags-video-assets.md).

* **Aprimoramentos** do Brand Portal: Os novos recursos a seguir e muito mais estão disponíveis em  [!DNL Brand Portal]. Para obter detalhes, consulte [[!DNL Brand Portal] notas de versão](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/introduction/brand-portal-release-notes.html).

   * [Experiência de download aprimorada ](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/download/brand-portal-download-assets.html) para downloads rápidos e simplificados. Configurações adicionais de download podem ser configuradas pelos administradores para oferta de uma experiência que atenda às necessidades dos usuários e empresas.
   * Navegação com um clique para Arquivos, [Coleções](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/share/brand-portal-share-collection.html) e Links compartilhados agora são possíveis em qualquer página.
   * Os usuários podem [selecionar e baixar representações específicas](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/download/brand-portal-download-assets.html#download-assets-from-asset-details-page) agora. A nova opção de download de representação está disponível no painel Representações na página Detalhes do ativo.
   * Um tempo limite de 15 minutos para sessões de usuário convidado garante uma melhor experiência para todos os usuários simultâneos.

* **[!DNL Adobe Asset Link]versão 2.1**: Uma nova versão do  [Adobe Asset ](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/manage-assets-using-adobe-asset-link.ug.html) Linkextension para  [!DNL Adobe Photoshop],  [!DNL Adobe Illustrator]e  [!DNL Adobe InDesign] está disponível. Ele acrescenta compatibilidade com os aplicativos [!DNL Adobe Creative Cloud] mais recentes com a versão 2021, lançada em outubro de 2020.

* **[!DNL Assets]Suporte** a arquivos WebP:  [!DNL Assets] como Cloud Service agora oferece suporte ao formato de imagem WebP. WebP é um formato de imagem emergente criado pelo Google. As imagens no formato de arquivo WebP são visualmente indistinguíveis dos arquivos JPG ou PNG e os arquivos são muito menores. O tamanho reduzido de arquivos de ativos melhora o tempo de carregamento da página e ajuda os criadores de conteúdo a proporcionarem uma experiência mais rápida na Web. Consulte como usar o WebP em [criar perfil de processamento](/help/assets/asset-microservices-configure-and-use.md#create-standard-profile).

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novidades {#what-is-new-commerce}

* Lançamento do site de referência CIF Venia - 2020.10.2 que inclui a versão mais recente dos componentes principais CIF v1.4.0. Consulte [CIF Site de Referência de Venia](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2020.10.2) para obter mais detalhes.

* Componentes principais CIF lançados v1.4.0. Consulte [CIF Componentes principais](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.4.0) para obter mais detalhes.

### Correções de erros {#bug-fixes-commerce}

* As solicitações de GraphQL no Console de produto e nos Seletores foram feitas por POST HTTP. Isso foi corrigido para garantir que o cliente Apollo GraphQL respeitasse a configuração na configuração OSGi do cliente GraphQL para suportar solicitações de GET, se configuradas.

* CIF Cloud config UI exibiu os botões &quot;Salvar e fechar&quot; para configurações em /lib e /apps/. Mas essas são somente leitura, portanto, a interface do usuário foi corrigida para exibir somente o botão &quot;Fechar&quot;.

## Cloud Manager {#cloud-manager}

### Data de lançamento {#release-date-cm}

A data de lançamento do Cloud Manager no AEM como Cloud Service 2020.10.0 é 2 de outubro de 2020.

### Novidades em [!DNL Cloud Manager] {#what-is-new-cm}

* A página Ambientes foi reprojetada.

* A página de ambientes hibernados agora mostra um status discreto no Cloud Manager.

* O container de compilação do Cloud Manager agora oferece suporte à compilação de projetos usando Java 8 ou Java 11. O suporte para Java 11 é fornecido pelo sistema de cadeias de ferramentas Maven.

* O número de variáveis por ambiente aumentou para 200.

* A placa de Ambiente na página Visão geral agora lista até três ambientes. Os usuários podem selecionar o botão **Mostrar tudo** para navegar até a página de resumo do Ambiente para visualização de uma tabela com uma lista completa de ambientes.
Consulte [Visualizando Ambiente](/help/implementing/cloud-manager/manage-environments.md#viewing-environment) para obter mais detalhes.

### Correções de erros {#bug-fixes-cloud-manager}

* Devido a um erro, o link do Cloud Manager para o Console do desenvolvedor estava ativo antes dos ambientes serem totalmente criados.

* O link direto do Cloud Manager para o Console do desenvolvedor não exibia a opção de desibernar/hibernar para ambientes do Programa de sandbox.

* Os botões Cancelar e Salvar na página Edição de Pipeline de Não Produção nem sempre estavam visíveis.

* Certas falhas no processo de qualidade do código podiam resultar na geração incorreta do arquivo de log.

* Às vezes, o nome sugerido na criação de um novo programa retornava um duplicado de um nome de programa existente.

* Grandes logs de etapas de pipeline não podiam ser baixados consistentemente pela interface do usuário.

* A validação de nomes de ambientes apresentava um erro off-by-one.

* A página Ambientes às vezes mostrava segmentos do Publish e do Dispatcher sem que estivessem presentes.

## Adobe Experience Manager as a Cloud Service Foundation {#cloud-service-foundation}

### Fluxos de trabalhos {#workflows}

* Foi adicionado suporte para pesquisar instâncias de fluxo de trabalho com base em Título do fluxo de trabalho, Modelo do fluxo de trabalho, Status, Iniciador, Caminho da carga e Data do Start. Consulte [Pesquisar Instâncias do Fluxo de Trabalho](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/sites/administering/workflows-administering.html).

## Ferramenta Transferência de conteúdo {#content-transfer-tool}

Siga esta seção para saber mais sobre as novidades e as atualizações da [Ferramenta de transferência de conteúdo](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html) Versão v1.1.12.

### Novidades {#what-is-new-ctt}

* A experiência do usuário para registros foi aprimorada. Carimbos de data e hora adicionados aos registros de Extração e ingestão. Mensagem adicionada para indicar se os logs estão vazios.

### Correções de erros {#ctt-bug-fixes}

* A Ferramenta de transferência de conteúdo ignorava os arquivos de conteúdo se o conjunto de migração contivesse caminhos que tivessem nomes de arquivos parcialmente semelhantes. Isso foi corrigido.
