---
title: Notas de versão do  [!DNL Adobe Experience Manager] as a Cloud Service 2020.10.0.
description: '[!DNL Adobe Experience Manager] Notas de versão as a Cloud Service para 2020.10.0.'
exl-id: ac741744-5b47-47a4-b5af-e1089e92c3f0
source-git-commit: 95ea603db207d93fa025a2ae20552f790b47f27c
workflow-type: tm+mt
source-wordcount: '1195'
ht-degree: 21%

---

# Notas de versão do [!DNL Adobe Experience Manager] as a Cloud Service 2020.10.0 {#release-notes}

A seção a seguir descreve as Notas de versão gerais de [!DNL Experience Manager] as a Cloud Service 2020.10.0.

## Data de lançamento {#release-date}

A data de lançamento para [!DNL Adobe Experience Manager] O as a Cloud Service 2020.10.0 é 28 de outubro de 2020.
A seguinte versão (2020.11.0) será lançada em 1º de dezembro de 2020.

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

### Novidades do [!DNL Sites] {#what-is-new-sites}

* **[Componentes principais 2.12.0](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=pt-BR)**: A Adobe Experience Manager as a Cloud Service se beneficia de atualizações automáticas para a versão mais recente dos Componentes principais. A versão 2.12.0 inclui as melhorias mais recentes contribuídas pela comunidade. As melhorias incluem [um novo manipulador de POST form;](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/forms/form-container.html#post-data) a capacidade de incluir CSS, JavaScript e metadados personalizados [tags por meio da configuração com reconhecimento de contexto;](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/including-clientlibs.html#context-aware-loading) e [`DataLayerBuilder`](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/data-layer/integrations.html#enabling-custom-components) para simplificar a integração da Camada de dados Adobe em componentes personalizados. Consulte a [lista de alterações](https://github.com/adobe/aem-core-wcm-components/releases/tag/core.wcm.components.reactor-2.12.0) em 2.12.0.

* **[Arquétipo de projeto 24](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)**: A base recomendada para iniciar um novo Experience Manager ficou melhor. Agora inclui o novo [Camada de dados do cliente Adobe](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/data-layer/overview.html), opção para [entregar site no AMP,](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/amp.html) e novos [pontos de extensão para adicionar CSS/JS do projeto.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/including-clientlibs.html#context-aware-loading)

* **[Pastas do ContextHub](/help/sites-cloud/authoring/personalization/contexthub-segmentation.md#organizing-segments)**: Capacidade de criar pastas de público-alvo para organizar, localizar e selecionar facilmente segmentos de público-alvo a serem usados para os recursos de direcionamento de ofertas do ContextHub.

## [!DNL Adobe Experience Manager Assets] as a Cloud Service {#assets}

* **[!DNL Adobe Sensei]Marcação inteligente com vídeo avançado**: Ao aplicar modelos de IA para analisar o conteúdo de vídeo para tags específicas de objeto e ação, os usuários do DAM podem gastar menos tempo adicionando tags e mais tempo usando as informações avançadas e expostas. Por sua vez, você fornece a experiência correta aos clientes. Consulte [Ativos de vídeo de tags inteligentes](/help/assets/smart-tags-video-assets.md).

* **Melhorias na Brand Portal**: Os novos recursos a seguir e muito mais estão disponíveis em [!DNL Brand Portal]. Para obter detalhes, consulte [[!DNL Brand Portal] notas de versão](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/brand-portal-release-notes.html).

   * [Experiência aprimorada de download](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/download/brand-portal-download-assets.html) para downloads rápidos e simplificados. Configurações adicionais de downloads podem ser configuradas por administradores para uma experiência que atenda às necessidades de usuários e empresas.
   * Navegação até os Arquivos com um só clique, [Coleções](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/share/brand-portal-share-collection.html) e Links compartilhados estão agora possibilitados diretamente de qualquer página.
   * Os usuários agora podem [selecionar e baixar representações específicas](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/download/brand-portal-download-assets.html#download-assets-from-asset-details-page). A nova opção de download de representações está disponível no painel Representações na página de detalhes dos Ativos.
   * Um tempo limite de 15 minutos para sessões de usuários visitantes garante uma experiência otimizada a todos os usuários concomitantes.

* **[!DNL Adobe Asset Link]versão 2.1**: Uma nova versão de [Adobe Asset Link](https://helpx.adobe.com/br/enterprise/using/manage-assets-using-adobe-asset-link.html) extensão para [!DNL Adobe Photoshop], [!DNL Adobe Illustrator]e [!DNL Adobe InDesign] está disponível. Ele adiciona compatibilidade com o mais recente [!DNL Adobe Creative Cloud] aplicativos com a versão 2021, lançada em outubro de 2020.

* **[!DNL Assets]Suporte a arquivos WebP**: [!DNL Assets] as a Cloud Service agora oferece suporte ao formato de imagem WebP. WebP é um formato de imagem emergente criado pelo Google. As imagens no formato de arquivo WebP são visualmente indistinguíveis dos arquivos JPG ou PNG e os arquivos são muito menores. O tamanho de arquivo reduzido dos ativos melhora o tempo de carregamento de página e ajuda os criadores de conteúdo a oferecerem uma experiência mais rápida na Web. Veja como usar o WebP em [criar perfil de processamento](/help/assets/asset-microservices-configure-and-use.md#create-standard-profile).

## [!DNL Adobe Experience Manager Forms] as a Cloud Service {#forms-oct-2021}

### Novidades do [!DNL Forms] {#what-is-new-forms-oct-2021}

* **Analytics para Adaptive Forms**: Agora é possível capturar e rastrear o comportamento de ambos, conectado e não conectado (anônimo) pelo Adobe Analytics para Adaptive Forms e coletar insights do usuário final. Ajuda os usuários de negócios a tomar decisões informadas sobre o conteúdo, layout e estilo do formulário adaptável com base nos insights coletados.

### Novos recursos disponíveis em [!DNL Forms] canal de pré-lançamento {#prerelease-features-forms-oct-2021}

* **Externalizar AEM dados do fluxo de trabalho para processamento seguro**: Você pode armazenar dados em andamento AEM variáveis do fluxo de trabalho que contêm elementos Sensíveis de dados pessoais (SPD) em um repositório gerenciado pelo cliente para processamento seguro. Ao processar o workflow, os dados armazenados nas variáveis do workflow não são mantidos em AEM repositório. Ele é buscado sob demanda do repositório gerenciado pelo cliente.

### Recursos beta de [!DNL Forms] {#sep-what-is-new-forms-oct-prerelease}

* **[!DNL AEM Forms as a Cloud Service - Communications]**: [APIs de comunicação](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/aem-forms-cloud-service-communications.html) ajuda a combinar um modelo e dados XML para gerar documentos em vários formatos. O serviço permite gerar documentos no modo síncrono e em lote.

Você pode escrever para [!DNL formscsbeta@adobe.com] para se inscrever no programa beta.

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novidades {#what-is-new-commerce}

* Lançamento do site de referência CIF Venia - 2020.10.2, que inclui a versão mais recente dos Componentes principais CIF v1.4.0. Consulte [Site de referência CIF Venia](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2020.10.2) para obter mais detalhes.

* Lançamento de componentes principais CIF v1.4.0. Consulte [Componentes principais da CIF](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.4.0) para obter mais detalhes.

### Correções de erros {#bug-fixes-commerce}

* As solicitações GraphQL que estavam no Console do produto e os Seletores foram feitas por meio do HTTP POST. Esse problema foi corrigido para garantir que o cliente GraphQL da Apollo respeitasse a configuração na configuração OSGi do cliente GraphQL para suportar solicitações GET, se configurada.

* A interface do usuário de configuração da CIF Cloud exibia os botões &quot;Salvar e fechar&quot; para configurações em /lib e /apps/. Mas essas interfaces são somente leitura, portanto, a interface do usuário foi corrigida para exibir apenas o botão &quot;Fechar&quot;.

## Cloud Manager {#cloud-manager}

### Data de lançamento {#release-date-cm}

A Data de lançamento do Cloud Manager no Experience Manager as a Cloud Service 2020.10.0 é 2 de outubro de 2020.

### Novidades do [!DNL Cloud Manager] {#what-is-new-cm}

* A página Ambientes foi reprojetada.

* A página de ambientes hibernados agora mostra um status discreto no Cloud Manager.

* O &quot;contêiner de criação&quot; do Cloud Manager agora é compatível com a compilação de projetos usando o Java™ 8 ou o Java™ 11. O suporte para o Java™ 11 é fornecido pelo sistema Maven toolchain.

* O número de variáveis por ambiente aumentou para 200.

* O cartão Environment na página Visão geral agora lista até três ambientes. Os usuários podem selecionar a variável **Mostrar tudo** para navegar até a página de resumo do ambiente para exibir uma tabela com uma lista completa de ambientes.
Consulte [Ambiente de visualização](/help/implementing/cloud-manager/manage-environments.md#viewing-environment) para obter mais detalhes.

### Correções de erros {#bug-fixes-cloud-manager}

* Devido a um erro, o link do Cloud Manager para o Console do desenvolvedor estava ativo antes dos ambientes serem totalmente criados.

* O link direto do Cloud Manager para o Console do desenvolvedor não exibia a opção de desibernar/hibernar para ambientes do Programa de sandbox.

* Os botões Cancelar e Salvar na página Editar pipeline de não produção nem sempre estavam visíveis.

* Certas falhas no processo de qualidade do código podiam resultar na geração incorreta do arquivo de log.

* Ao criar um programa, o nome sugerido às vezes retornava uma duplicata de um nome de programa existente.

* Grandes logs de etapas de pipeline não podiam ser baixados consistentemente pela interface do usuário.

* A validação de nomes de ambientes apresentava um erro off-by-one.

* A página Ambientes às vezes mostrava segmentos do Publish e Dispatcher quando nenhum estava presente.

## Adobe Experience Manager as a Cloud Service Foundation {#cloud-service-foundation}

### Fluxos de trabalhos {#workflows}

* Foi adicionado suporte para pesquisar instâncias de fluxo de trabalho com base em Título do fluxo de trabalho, Modelo do fluxo de trabalho, Status, Iniciador, Caminho da carga útil e Data inicial. Consulte [Pesquisar instâncias do fluxo de trabalho](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/administering/workflows-administering.html).

## Ferramenta Transferência de conteúdo {#content-transfer-tool}

Saiba mais sobre as novidades e atualizações do [Ferramenta Transferência de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html) Versão v1.1.12.

### Novidades {#what-is-new-ctt}

* A experiência do usuário para logs foi aprimorada. Carimbos de data e hora adicionados aos logs de Extração e Assimilação. Mensagem adicionada para indicar se os logs estão vazios.

### Correções de erros {#ctt-bug-fixes}

* A ferramenta Transferência de conteúdo ignorava os arquivos de conteúdo se o conjunto de migração contivesse caminhos que tivessem nomes de arquivo parcialmente semelhantes.
