---
title: Notas de versão do  [!DNL Adobe Experience Manager] as a Cloud Service 2020.10.0.
description: '[!DNL Adobe Experience Manager] as a Cloud Service Release Notes para 2020.10.0.'
exl-id: ac741744-5b47-47a4-b5af-e1089e92c3f0
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '1032'
ht-degree: 26%

---

# Notas de versão do [!DNL Adobe Experience Manager] as a Cloud Service 2020.10.0 {#release-notes}

A seção a seguir descreve as Notas de versão gerais de [!DNL Experience Manager] como um Cloud Service 2020.10.0.

## Data de lançamento {#release-date}

A Data de lançamento de [!DNL Adobe Experience Manager] como Cloud Service 2020.10.0 é 28 de outubro de 2020.
A seguinte versão (2020.11.0) será lançada em 1º de dezembro de 2020.

## [!DNL Adobe Experience Manager Sites] como um Cloud Service {#sites}

### Novidades em [!DNL Sites] {#what-is-new-sites}

* **[Componentes principais 2.12.0](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=pt-BR)**: O AEM como Cloud Service beneficia-se de atualizações automáticas para a versão mais recente dos Componentes principais. A versão 2.12.0 inclui as melhorias mais recentes fornecidas pela comunidade, como [um novo manipulador de formulário POST;](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/forms/form-container.html#post-data) a capacidade de incluir tags CSS personalizadas, Javascript e metadados [por meio de configuração sensível ao contexto;](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/including-clientlibs.html#context-aware-loading) e um utilitário [`DataLayerBuilder`](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/data-layer/integrations.html#enabling-custom-components) para simplificar a integração da Camada de dados Adobe em componentes personalizados. Consulte a lista de alterações [em 2.12.0.](https://github.com/adobe/aem-core-wcm-components/releases/tag/core.wcm.components.reactor-2.12.0)

* **[Arquétipo de projeto 24](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)**: A base recomendada para iniciar um novo projeto de AEM melhorou, agora incluindo a nova Camada [ de dados do cliente do ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/data-layer/overview.html)Adobe, a opção de  [entregar o site na AMP ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/amp.html) e novos pontos de  [extensão para adicionar CSS/JS do projeto.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/including-clientlibs.html#context-aware-loading)

* **[Pastas do ContextHub](/help/sites-cloud/authoring/personalization/contexthub-segmentation.md#organizing-segments)**: Capacidade de criar pastas de público-alvo para organizar, localizar e selecionar segmentos de público-alvo facilmente para usar nos recursos de direcionamento de ofertas do ContextHub.

## [!DNL Adobe Experience Manager Assets] como um Cloud Service {#assets}

* **[!DNL Adobe Sensei]Marcação** inteligente com vídeo alimentado: Ao utilizar modelos de IA para analisar o conteúdo de vídeo para tags específicas de objeto e ação, os usuários do DAM podem gastar menos tempo adicionando tags e mais tempo usando informações avançadas expostas para fornecer a experiência correta aos clientes. Consulte [Ativos de vídeo de tag inteligente](/help/assets/smart-tags-video-assets.md).

* **Melhorias** na Brand Portal: Os novos recursos a seguir e muito mais estão disponíveis em  [!DNL Brand Portal]. Para obter detalhes, consulte as [[!DNL Brand Portal] notas de versão](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/brand-portal-release-notes.html).

   * [Experiência aprimorada ](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/download/brand-portal-download-assets.html) de download para downloads rápidos e simplificados. Configurações adicionais de downloads podem ser configuradas por administradores para uma experiência que atenda às necessidades de usuários e empresas.
   * Navegação até os Arquivos com um só clique, [Coleções](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/share/brand-portal-share-collection.html) e Links compartilhados estão agora possibilitados diretamente de qualquer página.
   * Os usuários agora podem [selecionar e baixar representações específicas](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/download/brand-portal-download-assets.html#download-assets-from-asset-details-page). A nova opção de download de representações está disponível no painel Representações na página de detalhes dos Ativos.
   * Um tempo limite de 15 minutos para sessões de usuários visitantes garante uma experiência otimizada a todos os usuários concomitantes.

* **[!DNL Adobe Asset Link]versão 2.1**: Uma nova versão do  [Adobe Asset ](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/manage-assets-using-adobe-asset-link.ug.html) Linkextension for  [!DNL Adobe Photoshop],  [!DNL Adobe Illustrator]e  [!DNL Adobe InDesign] está disponível. Ele adiciona compatibilidade com os aplicativos [!DNL Adobe Creative Cloud] mais recentes com a versão 2021, lançada em outubro de 2020.

* **[!DNL Assets]Suporte** a arquivos WebP:  [!DNL Assets] o as a Cloud Service agora oferece suporte ao formato de imagem WebP. WebP é um formato de imagem emergente criado pelo Google. As imagens no formato de arquivo WebP são visualmente indistinguíveis dos arquivos JPG ou PNG e os arquivos são muito menores. O tamanho de arquivo reduzido dos ativos melhora o tempo de carregamento de página e ajuda os criadores de conteúdo a oferecerem uma experiência mais rápida na Web. Consulte como usar o WebP em [criar perfil de processamento](/help/assets/asset-microservices-configure-and-use.md#create-standard-profile).

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novidades {#what-is-new-commerce}

* Lançamento do site de referência CIF Venia - 2020.10.2, que inclui a versão mais recente dos Componentes principais CIF v1.4.0. Consulte [Site de referência CIF Venia](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2020.10.2) para obter mais detalhes.

* Lançamento de componentes principais CIF v1.4.0. Consulte [Componentes principais CIF](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.4.0) para obter mais detalhes.

### Correções de erros {#bug-fixes-commerce}

* As solicitações GraphQL no Console do produto e os Seletores foram feitas via HTTP POST. Isso foi corrigido para garantir que o cliente GraphQL da Apollo respeitasse a configuração na configuração OSGi do cliente GraphQL para suportar solicitações GET, se configurada.

* A interface do usuário de configuração da CIF Cloud exibia os botões &quot;Salvar e fechar&quot; para configurações em /lib e /apps/. Mas essas são somente leitura, portanto, a interface do usuário foi corrigida para exibir apenas o botão &quot;Fechar&quot;.

## Cloud Manager {#cloud-manager}

### Data de lançamento {#release-date-cm}

A Data de lançamento do Cloud Manager no AEM as a Cloud Service 2020.10.0 é 2 de outubro de 2020.

### Novidades em [!DNL Cloud Manager] {#what-is-new-cm}

* A página Ambientes foi reprojetada.

* A página de ambientes hibernados agora mostra um status discreto no Cloud Manager.

* O contêiner de build do Cloud Manager agora é compatível com a compilação de projetos usando o Java 8 ou o Java 11. O suporte para o Java 11 é fornecido pelo sistema de cadeias de ferramentas Maven.

* O número de variáveis por ambiente aumentou para 200.

* O cartão Environment na página Visão geral agora listará até três ambientes. Os usuários podem selecionar o botão **Mostrar tudo** para navegar até a página de resumo do ambiente para exibir uma tabela com uma lista completa de ambientes.
Consulte [Ambiente de visualização](/help/implementing/cloud-manager/manage-environments.md#viewing-environment) para obter mais detalhes.

### Correções de erros {#bug-fixes-cloud-manager}

* Devido a um erro, o link do Cloud Manager para o Console do desenvolvedor estava ativo antes dos ambientes serem totalmente criados.

* O link direto do Cloud Manager para o Console do desenvolvedor não exibia a opção de desibernar/hibernar para ambientes do Programa de sandbox.

* Os botões Cancelar e Salvar na página Editar pipeline de não produção nem sempre estavam visíveis.

* Certas falhas no processo de qualidade do código podiam resultar na geração incorreta do arquivo de log.

* Às vezes, o nome sugerido na criação de um novo programa retornava um duplicado de um nome de programa existente.

* Grandes logs de etapas de pipeline não podiam ser baixados consistentemente pela interface do usuário.

* A validação de nomes de ambientes apresentava um erro off-by-one.

* A página Ambientes às vezes mostrava segmentos do Publish e do Dispatcher sem que estivessem presentes.

## Adobe Experience Manager as a Cloud Service Foundation {#cloud-service-foundation}

### Fluxos de trabalhos {#workflows}

* Foi adicionado suporte para pesquisar instâncias de fluxo de trabalho com base em Título do fluxo de trabalho, Modelo do fluxo de trabalho, Status, Iniciador, Caminho da carga útil e Data inicial. Consulte [Pesquisar Instâncias do Fluxo de Trabalho](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/administering/workflows-administering.html).

## Ferramenta Transferência de conteúdo {#content-transfer-tool}

Siga esta seção para saber mais sobre as novidades e as atualizações da [Content Transfer Tool](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html) Versão v1.1.12.

### Novidades {#what-is-new-ctt}

* A experiência do usuário para logs foi aprimorada. Carimbos de data e hora adicionados aos logs de Extração e Assimilação. Mensagem adicionada para indicar se os logs estão vazios.

### Correções de erros {#ctt-bug-fixes}

* A ferramenta Transferência de conteúdo ignorava os arquivos de conteúdo se o conjunto de migração contivesse caminhos que tivessem os nomes de arquivo parcialmente semelhantes. Isso foi corrigido.
