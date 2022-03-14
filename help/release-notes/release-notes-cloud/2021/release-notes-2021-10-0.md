---
title: Notas de versão do  [!DNL Adobe Experience Manager] as a Cloud Service 2021.10.0.
description: Notas de versão do  [!DNL Adobe Experience Manager] as a Cloud Service 2021.10.0.
exl-id: ab584923-5f06-4b54-941b-e00bc1158b81
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '1439'
ht-degree: 48%

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

A data de lançamento do [!DNL Adobe Experience Manager] como [!DNL Cloud Service] a versão atual (2021.10.0) é 4 de novembro de 2021.
A seguinte versão (2021.11.0) é em 2 de dezembro de 2021.

## Vídeo da versão {#release-video}

Dê uma olhada no [Visão geral da versão de outubro de 2021](https://video.tv.adobe.com/v/338253) vídeo para obter um resumo dos recursos adicionados.

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Novo recurso em [!DNL Sites] {#sites-features}

* Os modelos de Fragmento de conteúdo agora são definidos automaticamente em estado somente leitura depois de serem publicados, para evitar a quebra não intencional de consultas de API ativas após a republicação de um modelo editado. Os usuários recebem um aviso ao tentar editar um modelo publicado. A edição é possível após aceitar o aviso.

## [!DNL Experience Manager Assets] como [!DNL Cloud Service] {#assets}

### Novos recursos no [!DNL Assets] {#assets-features}

* [!DNL Experience Manager] O agora é compatível com a geração automática de transcrições de texto dos ativos de áudio e vídeo compatíveis, usando um conector integrado para [!DNL Azure Media Services]. O [tipos de arquivos suportados](/help/assets/file-format-support.md#audio-video-transcription-formats) são transcritos automaticamente e o texto é armazenado no formato WebVTT. As legendas da WebVTT são usadas para pesquisas, legendas ou tradução mais eficientes. Além disso, o recurso melhora a acessibilidade, a descoberta e a localização dos ativos.

### Novo recurso na [!DNL Assets] canal de pré-lançamento {#assets-prerelease-features}

* [!DNL Dynamic Media]O Corte inteligente e a Amostra de imagens do agora são potencializados pelos serviços mais recentes do Sensei, que gera cortes e amostras aprimoradas. Além disso, um aprimoramento foi iniciado para gerar conteúdo de corte diferente, para a mesma proporção, mas em diferentes resoluções. Além disso, qualquer edição manual será preservada durante o reprocessamento, se não houver alteração na largura e na altura do Perfil de imagem.

* As Tags inteligentes são aplicadas automaticamente aos ativos usando microsserviços de ativos, em vez de Serviços de conteúdo inteligente. O modelo subjacente é atualizado para melhorar os resultados da marcação e reduzir o viés. <!-- As it uses asset microservices, it is now possible to develop custom workers using Stock10-based Smart Tags. -->

<!-- Leave this commented.
### Bugs fixed in [!DNL Assets] {#assets-bugs-fixed}

No customer-reported bugs fixed in Oct release. Details in CQDOC-18404.
-->

## [!DNL Experience Manager Forms] como [!DNL Cloud Service] {#forms}

### Novidades do [!DNL Forms] {#what-is-new-forms-oct-2021}

* **Analytics para Adaptive Forms**: Agora é possível capturar e rastrear o comportamento de logon e não conectado (Anônimo) pelo Adobe Analytics para Adaptive Forms para coletar insights do usuário final. Ajuda a tomar decisões informadas com base em dados para melhorar a experiência do usuário final.

### Novos recursos disponíveis no canal de pré-lançamento do [!DNL Forms] {#prerelease-features-forms-oct-2021}

* **Externalizar dados do fluxo de trabalho do AEM para processamento seguro**: Você pode armazenar dados de fluxos de trabalho em andamento do AEM (dados de variáveis de fluxo de trabalho do AEM) que contêm elementos de Dados pessoais sensíveis (SPD) em um repositório gerenciado pelo cliente para processamento seguro. Os elementos de dados e as variáveis de fluxo de trabalho não são armazenados no repositório do AEM e são buscados sob demanda de um repositório gerenciado pelo cliente durante o processamento do fluxo de trabalho.

### Recursos beta de [!DNL Forms] {#what-is-new-forms-oct2021-beta}

* **[!DNL AEM Forms as a Cloud Service - Communications]**: [APIs de comunicação](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/using-communications/aem-forms-cloud-service-communications.html?lang=pt-BR) ajudam a combinar um modelo e dados XML para gerar documentos de impressão em vários formatos. O serviço permite gerar documentos em modos síncronos e em lote. As APIs permitem criar aplicativos que possibilitam a você:

   * Gerar documentos preenchendo arquivos de modelo (PDF e XDP) com dados XML.
   * Gerar formulários de saída em vários formatos, incluindo fluxos de impressão de PDF não interativos.

Você pode escrever para [!DNL formscsbeta@adobe.com] para se inscrever no programa beta.

## Complemento CIF {#cloud-services-cif}

### Novidades {#what-is-new-cif}

* O complemento CIF é compatível com as versões mais recentes do Commerce v2.4.3 com novas APIs e esquemas GraphQL .

* Os autores podem adicionar links para páginas de produtos e catálogos em campos de texto usando o editor de rich text (RTE). Um ícone da CIF foi adicionado à barra de ferramentas do RTE que abrirá os seletores para pesquisar e selecionar rapidamente o produto ou a categoria sem sair do contexto.

* O carrinho de compras pop-up e o check-out existentes foram substituídos por páginas dedicadas AEM carrinho de compras e check-out. Os componentes nessas páginas são criados usando os componentes Peregrine extensíveis do Adobe Commerce

* Os comerciantes podem ocultar determinadas categorias de catálogo de produtos na navegação usando o backend do Commerce. O Componente principal de navegação da CIF respeita a configuração de backend de comércio &quot;incluir no menu&quot; para mostrar/ocultar categorias na navegação

* AEM Storefront Venia retorna o erro HTTP 404 se a página de categoria ou produto não for encontrada

## Cloud Manager {#cloud-manager}

Esta seção descreve as Notas de versão do Cloud Manager no AEM as a Cloud Service 2021.10.0.

### Data de lançamento {#release-date-cm-nov}

A data de lançamento do Cloud Manager no AEM as a Cloud Service 2021.11.0 é 4 de novembro de 2021.
A próxima versão está planejada para 9 de dezembro de 2021.

### Novidades {#what-is-new-cm-nov}

* Os usuários agora podem aproveitar os novos pipelines de front-end para implantar exclusivamente o código de front-end de forma acelerada. Consulte [Pipelines de front-end do Cloud Manager](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end) para saber mais.

   >[!IMPORTANT]
   >Você deve estar AEM versão `2021.10.5933.20211012T154732Z` para utilizar novos pipelines Front-End.

* A duração do pipeline de qualidade de código é significativamente reduzida ao executar a análise de código de uma maneira mais eficiente, sem a necessidade de criar uma imagem completa do AEM. Esta alteração será gradual durante as semanas que se seguem ao lançamento.

* A Git Commit ID agora será exibida nos detalhes de execução do pipeline, facilitando o rastreamento do código que foi criado.

* A Criação de programas agora está disponível por meio da API exposta publicamente.

* A Criação de ambiente agora está disponível por meio da API exposta publicamente.

* O cabeçalho de resposta `x-request-id` agora está visível na API Playground em [www.adobe.io](https://www.adobe.io/). Esse cabeçalho é útil ao enviar problemas de atendimento ao cliente para solução de problemas.

* Como usuário, vejo que o pipeline card com zero pipelines me fornece a orientação apropriada.

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

A Data de lançamento do Cloud Manager AEM as a Cloud Service 2021.10.0 é 14 de outubro de 2021.

### Novidades {#what-is-new-cm-oct}

* Em preparação para algumas alterações futuras, os pipelines de implantação existentes agora serão referenciados e rotulados na interface do usuário como **Pilha completa** Gasodutos.

* O cartão de pipeline foi atualizado para exibir agora uma única face integrada que mostra os pipelines de produção e não de produção, e o usuário pode selecionar Executar/Pausar/Retomar diretamente do menu de ação associado a cada pipeline.

* Um usuário na função Gerenciador de implantação agora pode excluir o pipeline de Produção de maneira automatizada por meio da interface do usuário.

* Adicionar e editar experiências de pipeline foi atualizado para agora usar modais modernos e familiares.

* Os usuários do Cloud Manager agora podem enviar feedback diretamente da interface do usuário por meio do **Feedback** na parte superior direita da landing page.

* Os gráficos de SLA anuais agora podem ser baixados na interface do usuário do Cloud Manager.

* As execuções de pipeline de não produção e qualidade de código agora usam um processo de clonagem superficial mais eficiente durante a etapa de compilação, resultando em um tempo de compilação mais rápido para clientes com repositórios Git especialmente grandes.

* O assistente Adicionar Lista de permissões de IP agora informará o usuário se o número máximo permitido de Listas de permissões de IP tiver sido atingido.

* A documentação da API do Cloud Manager agora inclui um playground interativo que permite que os usuários conectados façam experiências com a API a partir de seu navegador. Consulte [Reprodução da API do Cloud Manager](https://www.adobe.io/experience-cloud/cloud-manager/reference/playground/) para obter mais detalhes.

* A dica de ferramenta no cartão Programa será mais descritiva se uma opção de seleção em &quot;Navegar para&quot; estiver desativada. Agora, ele exibe &quot;Um ambiente de produção não existe&quot;.

### Correções de erros {#bug-fixes-cm-oct}

* Em raras situações, quando uma equipe de Adobe restaurava o ambiente de um cliente, a restauração era considerada concluída antes que o ambiente estivesse totalmente operacional.

* Certas solicitações internas feitas durante a criação do ambiente não foram repetidas.

* Se ocorrer um erro de falha na implantação após a verificação do nome de domínio, a mensagem de erro foi corrigida para solicitar que o cliente entre em contato com o representante do Adobe.

## Analisador de práticas recomendadas {#best-practices-analyzer}

### Data de lançamento {#release-date-bpa-latest}

A data de lançamento do Analisador de práticas recomendadas v2.1.20 é 5 de outubro de 2021.

### Novidades {#what-is-new}

* Capacidade de detectar e relatar o comprimento do nome do nó.

* Capacidade de detectar e relatar o tamanho total do Índice.

* Capacidade de detectar e gerar relatórios sobre ativos que não possuem sua representação original.
