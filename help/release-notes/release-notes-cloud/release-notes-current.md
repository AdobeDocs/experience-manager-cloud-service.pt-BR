---
title: Notas de versão atuais do  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Notas de versão atuais do  [!DNL Adobe Experience Manager]  as a Cloud Service.
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
source-git-commit: 6d0e3ee08862030e9eb7d068b251d13bc3e8e08f
workflow-type: tm+mt
source-wordcount: '1926'
ht-degree: 13%

---

# Notas de versão atuais do [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

A seção a seguir descreve as notas da versão de recurso atual (mais recente) do [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>A partir desta seção, você pode navegar até as notas das versões anteriores, como as de 2021 ou 2022.
>
>Dê uma olhada no [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=pt-BR) para saber mais sobre as próximas ativações de recursos do [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Consulte [Atualizações recentes na documentação](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=pt-BR) para obter detalhes de atualizações de documentação não relacionadas diretamente a uma versão.

## Data de lançamento {#release-date}

A data de lançamento de [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] A versão atual do recurso (2023.8.0) é 31 de agosto de 2023. A próxima versão do recurso (2023.9.0) está planejada para 28 de setembro de 2023.

## Vídeo da versão {#release-video}

Assista ao vídeo Visão geral da versão de agosto de 2023 que exibe um resumo dos recursos adicionados na versão 2023.8.0:

>[!VIDEO](https://video.tv.adobe.com/v/3423535/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Novos recursos no [!DNL Experience Manager Sites] {#sites-features}

* A variável [Console de fragmentos de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/content-fragments/content-fragments-console.html?lang=pt-BR) O agora permite que os usuários visualizem tags e pesquisem por tags aplicadas como metadados aos fragmentos de conteúdo. Os usuários não precisarão mais alternar para a interface do Assets para esse recurso, reduzindo a alternância de contexto e melhorando a eficiência.

  ![Marcação no Console de fragmentos de conteúdo](/help/assets/content-fragments-console-tags.png)
* O novo Editor de fragmento de conteúdo agora está disponível no AEM as a Cloud Service. Ele torna os autores de conteúdo mais produtivos, simplificando suas tarefas de criação e reduzindo a necessidade de alternar entre diferentes aplicativos durante a edição do conteúdo.
  ![Novo editor de fragmento de conteúdo](/help/release-notes/assets/newCFEditor.png)

O novo editor de Fragmento de conteúdo fornece os seguintes benefícios que não estão disponíveis no editor original:
* Salvamento automático para melhorar a eficiência da criação e evitar a perda acidental de edições.
* Visualização hierárquica de um fragmento de conteúdo e suas referências usando a árvore de estrutura para navegação rápida em um fragmento profundamente estruturado.
  ![Árvore de estrutura no editor de fragmento de conteúdo](/help/release-notes/assets/newCFEditor_StructureTree.png)

* Upload em linha de ativos como referências de conteúdo sem precisar carregá-los no DAM de ativos primeiro
* Visualização ad-hoc da experiência renderizada entregue pelo fragmento de conteúdo para ajudar os autores a visualizar a aparência do conteúdo no aplicativo de front-end
* 1-Clique em publicar e desfazer a publicação do fragmento de conteúdo no editor
* Visualização e navegação para cópias de idioma ao editar um fragmento de conteúdo
  ![Cópias de idioma no editor de fragmento de conteúdo](/help/release-notes/assets/newCFEditor_LanguageCopies.PNG)

* Visualização de versões para ajudar a rastrear a linha do tempo de um fragmento de conteúdo

  ![Versões no Editor de fragmento de conteúdo](/help/release-notes/assets/newCFEditor_Versionhistory.PNG)

* Exibir referências principais para ajudar os autores a entender o impacto de suas edições

  ![Referências principais no editor de fragmento de conteúdo](/help/release-notes/assets/newCFEditor_Parentreferences.PNG)

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Novos recursos na visualização de ativos {#assets-view-features}

<!--

**Assign metadata form to a folder**

You can now assign metadata form to a specific folder within your Assets Essentials deployment. All assets in the folder, including assets in the sub-folders, then display properties defined in the assigned metadata form.

![assign metadata form to a folder](/help/release-notes/assets/assign-to-folder.png)

-->

* **Importar ativos em massa de fontes de dados**: os administradores agora têm o [capacidade de importar um grande número de ativos](/help/assets/bulk-import-assets-view.md) de uma fonte de dados para o AEM Assets. Os administradores não precisam mais fazer upload de ativos ou pastas individuais para o AEM Assets. As fontes de dados compatíveis com a importação em massa incluem o Azure, o AWS, a Google Cloud e o Dropbox.

  ![Importar ativos em massa de uma fonte de dados](/help/release-notes/assets/bulk-import.png)

* **Ferramentas de edição de imagens possibilitadas pelo Adobe Express**: fácil e intuitivo [ferramentas de edição de imagens viabilizadas pelo Adobe Express](/help/assets/edit-images-assets-view.md) disponível diretamente no AEM Assets para aumentar a reutilização de conteúdo e acelerar a velocidade do conteúdo.

  ![Edição de imagens com o Adobe Express](/help/release-notes/assets/edit-adobe-express.png)

* **Flexibilidade ao fixar itens para o Acesso rápido ao My Workspace**: capacidade de selecionar e fixar itens para você, para toda a organização ou para uma lista de grupos para que sejam exibidos no [Seção Acesso rápido do Meu Espaço de Trabalho](/help/assets/my-workspace-assets-view.md) com base na sua seleção.

  ![Fixar itens para grupos](/help/release-notes/assets/pin-items-for-groups.png)

### Novos recursos na exibição do Administrador {#admin-view-features}

**Aprimoramentos de pesquisa**

* Agora, os administradores podem [configurar o tamanho do lote de ativos](/help/assets/search-assets.md#configure-asset-batch-size) que são exibidos quando você executa uma pesquisa. Os resultados da pesquisa de ativos são exibidos em múltiplos do número de tamanho de lote configurado ao rolar a tela para baixo para carregar os resultados. Você pode selecionar entre os tamanhos de lote disponíveis de 200, 500 e 1000 ativos. Definir um número de tamanho de lote mais baixo resulta em tempos de resposta de pesquisa mais rápidos.

  ![Configuração do tamanho do lote de ativos](/help/release-notes/assets/assets-batch-size-configuration.png)

* O Experience Manager Assets agora inclui uma nova versão 9 do `damAssetLucene` índice. `damAssetLucene-9` altera o comportamento da contagem facetada da consulta do Oak para [não avalia mais o controle de acesso nas contagens de facetas](/help/assets/search-assets.md) retornados pelo índice de pesquisa subjacente, o que resulta em tempos de resposta de pesquisa mais rápidos.

### Recursos de pré-lançamento disponíveis em [!DNL Experience Manager Assets] {#prerelease-features-assets}

* **Dynamic Media**: [Suporte a faixas de várias legendas e áudio para vídeos no Dynamic Media](/help/assets/dynamic-media/video.md#about-msma)—Agora é possível adicionar facilmente várias legendas e faixas de áudio a um vídeo principal. Esse recurso significa que os vídeos estão acessíveis em um público-alvo global. Você pode personalizar um único vídeo principal publicado para um público-alvo global em vários idiomas e seguir as diretrizes de acessibilidade para diferentes regiões geográficas. Os autores também podem gerenciar as legendas e faixas de áudio em uma única guia na interface do usuário do.

  ![Guia Legendas e faixas de áudio na página Propriedades de um ativo de vídeo selecionado.](/help/release-notes/assets/msma-aem-cs.png)*Guia Legendas e faixas de áudio na página Propriedades de um ativo de vídeo selecionado.*

* **Assets**: Capacidade de selecionar arquivos ZIP gerenciados no Experience Manager e [extração de arquivos diretamente no Experience Manager](/help/assets/manage-digital-assets.md#extract-zip-archives) sem baixá-los.

  ![Fixar itens para grupos](/help/release-notes/assets/extract-archive.png)


## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Recursos de pré-lançamento disponíveis em [!DNL Forms] {#pre-release-features-available-in-forms-channel}

* [**Suporte corporativo ao Google reCAPTCHA**](/help/forms/captcha-adaptive-forms-core-components.md): use o Google reCAPTCHA Enterprise em um formulário adaptável para fornecer proteção aprimorada contra atividades fraudulentas e spam, proporcionando uma experiência mais segura ao usuário. Com a análise de risco avançada e a integração perfeita, os usuários genuínos podem enviar formulários facilmente, enquanto os bots são bloqueados de maneira eficaz.

* **Adobe Analytics com automação de configuração do Experience Cloud para Forms**: Agora você pode ativar o Adobe Analytics com a Automação de configuração do Experience Cloud girando alguns botões. Ele permite conectar o AEM Forms as a Cloud Service com tags Experience Platform e o Adobe Analytics para capturar e rastrear métricas de desempenho para seus formulários publicados.

* **Modelo de relatório do Adobe Analytics para o Adaptive Forms**: o Forms as a Cloud Service agora fornece um relatório do Adobe Analytics OOTB. Ele ajuda você a entender facilmente o desempenho de seus formulários. As métricas no nível do formulário fornecem um insight sobre o desempenho do formulário em vários indicadores principais de desempenho (KPIs), como representações, visitantes, envios e tempo médio de preenchimento. Ao rastrear o comportamento do usuário e o feedback, você pode identificar áreas do formulário que estão causando confusão e orientar melhorias no design e na funcionalidade do formulário.

  ![Relatório de engajamento do usuário no formulário adaptável do adobe analytics](/help/forms/assets/forms-analytics-report.png)

* **[Fragmento de formulário no Forms adaptável com base nos Componentes principais](/help/forms/adaptive-form-fragments-core-components.md)**: diga adeus à duplicação, otimize seu inventário digital e melhore a colaboração à medida que você eleva sua experiência de criação de formulários com Fragmentos de formulário. Esses componentes reutilizáveis se integram perfeitamente em vários formulários, simplificando a criação de formulários consistentes e com aparência profissional. Os fragmentos de formulário garantem a reutilização, a padronização e a consistência da marca por meio da funcionalidade &quot;alterar uma vez e refletir em todos os lugares&quot;. Experimente maior capacidade de manutenção e eficiência, já que as atualizações feitas em um local são propagadas automaticamente em todos os formulários que utilizam esses fragmentos.

* **[Etapa de fluxo de trabalho aprimorada do Adobe Sign](/help/forms/aem-forms-workflow-step-reference.md#sign-document-step-sign-document-step)**: a etapa Fluxo de trabalho do Adobe Sign foi aprimorada para incluir o seguinte:
   * **Autenticação com base em ID do governo para o Adobe Sign**: a autenticação baseada em ID do governo da Adobe Acrobat Sign oferece uma camada adicional de verificação, permitindo que os usuários autentiquem sua identidade usando IDs emitidas pelo governo (CNH, identificação nacional, passaporte). Ao utilizar documentos de identificação confiáveis, esse aprimoramento adiciona um nível extra de confiança ao processo de assinatura, tornando-o ideal para cenários que exigem maior segurança, conformidade e validação do usuário.

   * **Trilha de auditoria para documentos do Adobe Sign**: use o recurso Trilha de auditoria para obter insights detalhados sobre o ciclo de vida dos documentos do Adobe Sign. Com a Trilha de auditoria, agora é possível manter um registro abrangente de todas as ações e interações relacionadas aos documentos. Isso inclui detalhes como quem visualizou, editou ou assinou o documento, além de carimbos de data e hora para cada evento. Esse aprimoramento é fundamental para manter a conformidade, resolver disputas e garantir a integridade de seus contratos digitais.

   * **Novas funções para destinatários do Contrato além do Signatário**: a Adobe Acrobat Sign tem a opção de expandir as funções dos recipients do Contrato além apenas do Signatário para melhor corresponder aos requisitos de fluxo de trabalho. Quando habilitado, cada recipient em um Contrato tem sua função configurável individualmente, sendo que Signatário é o padrão.

* **[Protect seus documentos com APIs de garantia de documentos (parte das APIs de comunicação)](/help/forms/aem-forms-cloud-service-communications-introduction.md#document-assurance-doc-assurance)**: As APIs do Document Assurance permitem proteger informações confidenciais, assinando e criptografando os documentos. Por meio da criptografia, o conteúdo de um documento é transformado em um formato ilegível, garantindo que somente usuários autorizados possam ter acesso. Essa camada fortificada de proteção não apenas protege dados valiosos de olhos não autorizados, mas também proporciona tranquilidade. As APIs de assinatura permitem que sua organização proteja a segurança e a privacidade dos documentos do Adobe PDF que distribui e recebe. Esse serviço usa assinaturas digitais e certificação para garantir que somente os recipients desejados possam alterar os documentos.

* **Suporte à contagem de páginas em APIs de comunicação**: Agora, juntamente com a recuperação do documento por meio das APIs de comunicação, você também pode receber as informações valiosas sobre o número de páginas contidas no documento.

* **[Tratamento de erros com manipuladores de erros personalizados no editor de regras](/help/forms/add-custom-error-handler-adaptive-forms-core-components.md)**: agora você pode chamar uma função personalizada em resposta a um erro retornado por um serviço externo e fornecer uma resposta personalizada para os usuários finais. Por exemplo, você pode acionar um fluxo de trabalho personalizado no back-end para códigos de erro específicos ou informar ao cliente que o serviço está inativo.

* **[Versão de 64 bits do AEM Forms Designer](/help/forms/installing-configuring-designer.md)**: A versão de 64 bits do AEM Forms Designer oferece desempenho, escalabilidade e gerenciamento de memória aprimorados para potencializar a experiência de criação de formulários. Com a arquitetura de 64 bits, você pode executar projetos ainda maiores e mais complexos com facilidade, garantindo fluxos de trabalho de design ininterruptos e eficiência otimizada. Aumente os recursos de design de formulário e abrace o futuro do AEM Forms Designer com esta versão de última geração.


### Programa de adoção antecipada {#forms-early-adopter}

* **[Protect seus documentos com as APIs DocAssurance (Parte das APIs de comunicação)](/help/forms/aem-forms-cloud-service-communications-introduction.md#document-assurance-doc-assurance)**: As APIs do DocAssurance permitem proteger informações confidenciais, assinando e criptografando os documentos. Por meio da criptografia, o conteúdo de um documento é transformado em um formato ilegível, garantindo que somente usuários autorizados possam ter acesso. Essa camada fortificada de proteção não apenas protege dados valiosos de olhos não autorizados, mas também proporciona tranquilidade. As APIs de assinatura permitem que sua organização proteja a segurança e a privacidade dos documentos do Adobe PDF que distribui e recebe. Esse serviço usa assinaturas digitais e certificação para garantir que somente os recipients desejados possam alterar os documentos.

  Você pode conectar o Suporte ao Adobe para participar do programa de adoção antecipada das APIs DocAssurance.

* **[Forms adaptável headless](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html?lang=pt-BR)**: use o Headless Adaptive Forms para permitir que os desenvolvedores criem, publiquem e gerenciem formulários interativos que podem ser acessados e interagidos por meio de APIs, em vez de uma interface gráfica tradicional. Os formulários adaptáveis headless ajudam a:

   * criar formulários multicanal de alta qualidade na linguagem de programação de sua escolha
   * integrar formulários nativamente a seus aplicativos móveis e de desktop, sites e aplicativos de bate-papo
   * reutilizar os componentes de interface de sua propriedade com aplicativos de formulários
   * aproveitar o potencial do Adobe Experience Manager Forms

  Você pode enviar um email para `aem-forms-headless@adobe.com` utilizando sua ID de email oficial para participar do programa de adoção antecipada.


## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Logs CDN {#cdn-logs}

Baixe logs de CDN do Cloud Manager, que é útil para otimização da taxa de ocorrência do cache e maior visibilidade do fluxo de entrega de conteúdo. [Saiba mais sobre](/help/implementing/developing/introduction/logging.md#cdn-log) o formato de log CDN. Esse recurso será gradualmente lançado para os clientes no início de setembro.

### Programa de adoção antecipada das regras CDN e WAF {#waf-early-adopter}

Filtrar o tráfego na CDN com base em:
* cabeçalhos e propriedades de solicitação (por exemplo, endereço IP)
* padrões de tráfego conhecidos por estarem associados a tráfego mal-intencionado

Interessado em experimentar o recurso e compartilhar feedback? Enviar um email para **aemcs-waf-adopter@adobe.com** da sua ID de e-mail oficial para saber mais sobre o programa dos participantes antecipados. O espaço é limitado.

Saiba mais sobre o recurso no artigo [aqui](/help/security/cdn-and-waf-rules.md).


## Notas da versão de manutenção {#maintenance}

Encontre as notas de versão de manutenção mais recentes [aqui](/help/release-notes/maintenance/latest.md).

## Cloud Manager {#cloud-manager}

Você pode encontrar uma lista completa de versões mensais do Cloud Manager [aqui](/help/implementing/cloud-manager/release-notes/current.md).

## Ferramentas de migração {#migration-tools}

Você pode encontrar uma lista completa de versões das ferramentas de migração [aqui](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
