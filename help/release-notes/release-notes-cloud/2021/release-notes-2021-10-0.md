---
title: Notas de versão do  [!DNL Adobe Experience Manager]  as a Cloud Service 2021.10.0.
description: Notas de versão do  [!DNL Adobe Experience Manager]  as a Cloud Service 2021.10.0.
exl-id: ab584923-5f06-4b54-941b-e00bc1158b81
feature: Release Information
role: Admin
source-git-commit: 281a8efcd18920dd926d92db9c757c0513d599fd
workflow-type: tm+mt
source-wordcount: '1436'
ht-degree: 67%

---

# Notas de versão atuais do [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

A seção a seguir descreve as Notas de versão gerais da versão atual (mais recente) do [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>A partir daqui, você pode navegar até as notas de versão das versões anteriores; por exemplo, para aquelas em 2020, 2021 e assim por diante.

>[!NOTE]
>
>Consulte [Atualizações recentes na documentação](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=pt-BR) para obter detalhes de atualizações de documentação não relacionadas diretamente a uma versão.

## Data de lançamento {#release-date}

A data de lançamento da versão atual (2021.10.0) do [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] é sexta-feira, 4 de novembro de 2021.
A versão seguinte (2021.11.0) será lançada em sexta-feira, 2 de dezembro de 2021.

## Vídeo da versão {#release-video}

Assista ao vídeo [Visão geral da versão de outubro de 2021](https://video.tv.adobe.com/v/338253) para ver um resumo dos recursos adicionados.

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Novo recurso em [!DNL Sites] {#sites-features}

* Os modelos de Fragmento de conteúdo agora são definidos automaticamente no estado somente leitura depois de publicados, para evitar a quebra involuntária de consultas de API ativas após a republicação de um modelo editado. Os usuários recebem um aviso ao tentar editar um modelo publicado. A edição é possível ao aceitar o aviso.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Novos recursos no [!DNL Assets] {#assets-features}

* O [!DNL Experience Manager] agora oferece suporte à geração automática de transcrições de texto dos ativos de áudio e vídeo com suporte, usando um conector integrado para [!DNL Azure Media Services]. Os [tipos de arquivos suportados](/help/assets/file-format-support.md#audio-video-transcription-formats) são transcritos automaticamente e o texto é armazenado no formato WebVTT. As legendas WebVTT são usadas para pesquisa, legendagem ou tradução mais eficientes. Além disso, o recurso melhora a acessibilidade, a descoberta e a localização dos ativos.

### Novo recurso no canal de pré-lançamento do [!DNL Assets] {#assets-prerelease-features}

* O Recorte inteligente e a Amostra de imagens do [!DNL Dynamic Media] agora são potencializados pelos serviços de IA mais recentes, que geram melhores recortes e amostras. Além disso, um aprimoramento foi iniciado para gerar conteúdo de corte diferente, para a mesma proporção, mas em diferentes resoluções. Além disso, as edições manuais são preservadas no reprocessamento, se não houver alteração na largura e na altura do Perfil de imagem.

* As Tags inteligentes são aplicadas automaticamente aos ativos usando microsserviços de ativos, em vez dos Serviços de conteúdo inteligente. O modelo subjacente é atualizado para melhorar os resultados da marcação e reduzir a polarização. <!-- As it uses asset microservices, it is now possible to develop custom workers using Stock10-based Smart Tags. -->

<!-- Leave this commented.
### Bugs fixed in [!DNL Assets] {#assets-bugs-fixed}

No customer-reported bugs fixed in Oct release. Details in CQDOC-18404.
-->

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Novidades do [!DNL Forms] {#what-is-new-forms-oct-2021}

* **Analytics para Forms adaptável**: agora é possível capturar e rastrear o comportamento de logado e não conectado (anônimo) por meio do Adobe Analytics para Forms adaptável para coletar insights do usuário. Ele ajuda a tomar decisões informadas com base em dados para melhorar a experiência do usuário.

### Novos recursos disponíveis no canal de pré-lançamento do [!DNL Forms] {#prerelease-features-forms-oct-2021}

* **Externalizar dados do fluxo de trabalho do AEM para processamento seguro**: Você pode armazenar dados de fluxos de trabalho em andamento do AEM (dados de variáveis de fluxo de trabalho do AEM) que contêm elementos de Dados pessoais sensíveis (SPD) em um repositório gerenciado pelo cliente para processamento seguro. Os elementos de dados e as variáveis de fluxo de trabalho não são armazenados no repositório do AEM e são buscados sob demanda de um repositório gerenciado pelo cliente durante o processamento do fluxo de trabalho.

### Recursos do Beta de [!DNL Forms]  {#what-is-new-forms-oct2021-beta}

* **[!DNL AEM Forms as a Cloud Service - Communications]**: [APIs de comunicação](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/using-communications/aem-forms-cloud-service-communications.html?lang=pt-BR) ajudam a combinar um modelo e dados XML para gerar documentos de impressão em vários formatos. O serviço permite gerar documentos em modos síncronos e em lote. As APIs permitem criar aplicativos que possibilitam a você:

   * Gerar documentos preenchendo arquivos de modelo (PDF e XDP) com dados XML.
   * Gerar formulários de saída em vários formatos, incluindo fluxos de impressão de PDF não interativos.

Você pode enviar um email a [!DNL formscsbeta@adobe.com] para se cadastrar no programa beta.

## Complemento CIF {#cloud-services-cif}

### Novidades {#what-is-new-cif}

* O complemento CIF é compatível com a versão mais recente do Commerce v2.4.3 com novas APIs e esquemas do GraphQL

* Os autores podem adicionar links para páginas de produtos e catálogos em campos de texto usando o editor de rich text (RTE). Um ícone do CIF foi adicionado à barra de ferramentas do RTE, que abre os seletores para pesquisar e selecionar rapidamente o produto ou categoria sem sair do contexto.

* O carrinho de compras pop-up e o check-out foram substituídos por páginas dedicadas de carrinho de compras e check-out do AEM. Os componentes nessas páginas são criados usando os componentes Peregrine extensíveis do Adobe Commerce

* Os comerciantes podem ocultar determinadas categorias de catálogo de produtos na navegação usando o back-end do Commerce. O componente principal de Navegação do CIF respeita a configuração de backend de comércio &quot;incluir no menu&quot; para mostrar/ocultar categorias na navegação

* O AEM Storefront Venia retorna o erro HTTP 404 se a página de categoria ou produto não for encontrada

## Cloud Manager {#cloud-manager}

Esta seção descreve as Notas de versão do Cloud Manager no AEM as a Cloud Service 2021.10.0.

### Data de lançamento {#release-date-cm-nov}

A data de lançamento do Cloud Manager no AEM as a Cloud Service 2021.11.0 é 4 de novembro de 2021.
A próxima versão está planejada para 9 de dezembro de 2021.

### Novidades {#what-is-new-cm-nov}

* Os usuários agora podem aproveitar os novos pipelines de front-end para implantar exclusivamente o código de front-end de forma acelerada. Consulte [Pipelines de front-end do Cloud Manager](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end) para saber mais.

  >[!IMPORTANT]
  >É necessário usar o AEM versão `2021.10.5933.20211012T154732Z` para aproveitar os novos pipelines de Front-End.

* A duração do pipeline de qualidade de código é significativamente reduzida ao executar a análise de código de uma maneira mais eficiente, sem a necessidade de criar uma imagem completa do AEM. Esta alteração será gradual durante as semanas que se seguem ao lançamento.

* A Git Commit ID agora será exibida nos detalhes de execução do pipeline, facilitando o rastreamento do código que foi criado.

* A Criação de programas agora está disponível por meio da API exposta publicamente.

* A Criação de ambiente agora está disponível por meio da API exposta publicamente.

* O cabeçalho de resposta `x-request-id` agora está visível na API Playground em [www.adobe.io](https://www.adobe.io/). Esse cabeçalho é útil ao enviar problemas de atendimento ao cliente para solução de problemas.

* Como usuário, vejo que o cartão do pipeline com zero pipelines me fornece a orientação apropriada.

* Uma nova Página de atividade agora está disponível, em que atividades como pipeline e execuções de código podem ser visualizadas junto a seus detalhes associados. Com o tempo, as atividades listadas nesta página se expandirão em escopo junto com os detalhes fornecidos.

* Uma nova página Pipelines, com um popover de status ao passar o mouse para facilitar a visualização do resumo dos detalhes, está disponível. As execuções de pipeline podem ser visualizadas junto com seus detalhes associados.

* A API Editar pipeline agora oferece suporte à alteração do ambiente usado nas fases de implantação.

* Uma otimização no processo de varredura do OakPal foi introduzida para pacotes grandes.

* O arquivo CSV de problemas de qualidade agora contém o carimbo de data e hora de cada problema de qualidade.

### Correções de erros {#bug-fixes-nov}

* Certas configurações de build não ortodoxas resultaram no armazenamento de arquivos desnecessários no cache de artefatos do Maven no pipeline, o que resultou em I/O de rede irrelevantes ao iniciar e parar o contêiner de compilação.

* A API do PATCH de pipeline falha se a fase de implantação não existir.

* A regra de qualidade `ClientlibProxyResourceCheck` gerava problemas de falso positivo quando havia bibliotecas de clientes com caminhos de base comuns.

* A mensagem de erro quando o número máximo de repositórios era atingido não especificava o motivo do erro.

* Em casos raros, os pipelines estavam falhando devido ao manuseio de novas tentativas inadequado de determinados códigos de resposta.


## Data de lançamento {#release-date-cm-oct}

A data de lançamento do Cloud Manager no AEM as a Cloud Service 2021.10.0 é 14 de outubro de 2021.

### Novidades {#what-is-new-cm-oct}

* Em preparação para algumas alterações futuras, os pipelines de implantação existentes agora serão referenciados e rotulados na interface do usuário como **Pipelines de pilha** completa.

* O cartão do pipeline foi atualizado para exibir uma única face integrada que mostra os pipelines de produção e não produção, e o usuário agora pode selecionar Executar/Pausar/Retomar diretamente do menu de ação associado a cada pipeline.

* Um usuário com a função Gerente de implantação agora pode excluir o pipeline de produção de maneira automatizada por meio da interface do usuário.

* A adição e a edição de experiências de pipeline foram atualizadas para usar modais modernos e familiares.

* Os usuários do Cloud Manager agora podem enviar feedback diretamente da interface do usuário por meio do botão **Feedback** na parte superior direita da página de destino.

* Os gráficos de SLA anuais agora podem ser baixados na interface do usuário do Cloud Manager.

* As execuções de pipeline de não produção e qualidade do código agora usam um processo de clonagem superficial mais eficiente durante a etapa de compilação, resultando em um tempo de compilação mais rápido para clientes com repositórios Git especialmente grandes.

* O assistente e adição de lista de permissões de IP agora informará o usuário se o número máximo permitido de listas tiver sido atingido.

* A documentação da API do Cloud Manager agora inclui um playground interativo que permite que os usuários conectados experimentem a API no navegador. Consulte [Playground da API do Cloud Manager](https://www.adobe.io/experience-cloud/cloud-manager/reference/playground/) para obter mais detalhes.

* A dica de ferramenta no cartão Programa será mais descritiva se a opção “Navegar para” estiver desmarcada. Agora, exibe “Não existe um ambiente de produção”.

### Correções de erros {#bug-fixes-cm-oct}

* Em raras situações, quando uma equipe da Adobe restaurava o ambiente de um cliente, a restauração era considerada concluída antes de o ambiente estar totalmente operacional.

* Certas solicitações internas feitas durante a criação do ambiente não eram repetidas.

* Quando ocorre um erro de falha na implantação após a verificação do nome de domínio, a mensagem de erro foi corrigida para solicitar que o cliente entre em contato com o representante da Adobe.

## Analisador de práticas recomendadas {#best-practices-analyzer}

### Data de lançamento {#release-date-bpa-latest}

A data de lançamento do Analisador de práticas recomendadas v2.1.20 é 5 de outubro de 2021.

### Novidades {#what-is-new}

* Capacidade de detectar e relatar o comprimento do nome do nó.

* Capacidade de detectar e relatar o tamanho total do índice.

* Capacidade de detectar e relatar ativos sem a representação original.
