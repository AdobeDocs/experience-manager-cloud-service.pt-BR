---
title: Notas de versão do  [!DNL Adobe Experience Manager]  as a Cloud Service 2023.8.0.
description: Notas de versão do  [!DNL Adobe Experience Manager]  as a Cloud Service 2023.8.0.
exl-id: a0ffa6cf-64ae-468c-93f4-ac6805ef907e
feature: Release Information
role: Admin
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1691'
ht-degree: 18%

---

# Notas de versão do [!DNL Adobe Experience Manager] as a Cloud Service 2023.8.0 {#release-notes}

A seção a seguir descreve as notas da versão de recursos do [!DNL Experience Manager] as a Cloud Service 2023.8.0.

## Data de lançamento {#release-date}

A data de lançamento da versão atual (2023.8.0) do [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] é sexta-feira, 31 de agosto de 2023. O próximo lançamento de recursos (2023.9.0) está planejado para sexta-feira, 28 de setembro de 2023.

## Vídeo da versão {#release-video}

Assista ao vídeo Visão geral da versão de agosto de 2023 que exibe um resumo dos recursos adicionados na versão 2023.8.0:

>[!VIDEO](https://video.tv.adobe.com/v/3423535/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Novos recursos no [!DNL Experience Manager Sites] {#sites-features}

* O [Console de fragmentos de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/content-fragments/content-fragments-console.html) agora permite que os usuários exibam marcas e pesquisem por marcas aplicadas como metadados aos fragmentos de conteúdo. Os usuários não precisarão mais alternar para a interface do Assets para esse recurso, reduzindo a alternância de contexto e melhorando a eficiência.

  ![Marcação no Console de Fragmentos de Conteúdo](/help/assets/content-fragments-console-tags.png)
* O novo Editor de fragmento de conteúdo agora está disponível no AEM as a Cloud Service. Ele torna os autores de conteúdo mais produtivos, simplificando suas tarefas de criação e reduzindo a necessidade de alternar entre diferentes aplicativos durante a edição do conteúdo.
  ![Novo editor de fragmento de conteúdo](/help/release-notes/assets/newCFEditor.png)

O novo editor de Fragmento de conteúdo fornece os seguintes benefícios que não estão disponíveis no editor original:

* Salvamento automático para melhorar a eficiência da criação e evitar a perda acidental de edições.
* Visualização hierárquica de um fragmento de conteúdo e suas referências usando a árvore de estrutura para navegação rápida em um fragmento profundamente estruturado.
  ![Árvore de estrutura no Editor de fragmento de conteúdo](/help/release-notes/assets/newCFEditor_StructureTree.png)

* Upload em linha de ativos como referências de conteúdo sem precisar carregá-los no DAM de ativos primeiro
* Visualização ad-hoc da experiência renderizada entregue pelo fragmento de conteúdo para ajudar os autores a visualizar a aparência do conteúdo no aplicativo de front-end
* 1-Clique em publicar e desfazer a publicação do fragmento de conteúdo no editor
* Visualização e navegação para cópias de idioma ao editar um fragmento de conteúdo
  ![Cópias de idioma no Editor de fragmento de conteúdo](/help/release-notes/assets/newCFEditor_LanguageCopies.PNG)

* Visualização de versões para ajudar a rastrear a linha do tempo de um fragmento de conteúdo

  ![Versões no Editor de Fragmento de Conteúdo](/help/release-notes/assets/newCFEditor_Versionhistory.PNG)

* Exibir referências principais para ajudar os autores a entender o impacto de suas edições

  ![Referências principais no Editor de Fragmento de Conteúdo](/help/release-notes/assets/newCFEditor_Parentreferences.PNG)

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Novos recursos na visualização de ativos {#assets-view-features}

<!--

**Assign metadata form to a folder**

You can now assign metadata form to a specific folder within your Assets Essentials deployment. All assets in the folder, including assets in the sub-folders, then display properties defined in the assigned metadata form.

![assign metadata form to a folder](/help/release-notes/assets/assign-to-folder.png)

-->

* **Importar ativos em massa de fontes de dados**: os administradores agora têm a [capacidade de importar um grande número de ativos](/help/assets/bulk-import-assets-view.md) de uma fonte de dados para a AEM Assets. Não é mais necessário fazer upload de ativos ou pastas individuais para o AEM Assets. As fontes de dados compatíveis com a importação em massa incluem Azure, AWS, Google Cloud e Dropbox.

  ![Importação em massa de ativos de uma fonte de dados](/help/release-notes/assets/bulk-import.png)

* **Ferramentas de edição de imagens viabilizadas pelo Adobe Express**: [ferramentas de edição de imagens viabilizadas pelo Adobe Express](/help/assets/edit-images-assets-view.md) fáceis e intuitivas, disponíveis diretamente no AEM Assets para aumentar a reutilização de conteúdo e acelerar a velocidade do conteúdo.

  ![Edição de imagens com o Adobe Express](/help/release-notes/assets/edit-adobe-express.png)

* **Flexibilidade ao fixar itens em Meu Acesso Rápido ao Workspace**: capacidade de selecionar e fixar itens para você, para toda a sua organização ou para uma lista de grupos, de modo que eles sejam exibidos na [seção Acesso Rápido de Meu Workspace](/help/assets/my-workspace-assets-view.md) com base na sua seleção.

  ![Fixação de itens para grupos](/help/release-notes/assets/pin-items-for-groups.png)

### Novos recursos na exibição do Administrador {#admin-view-features}

**Aprimoramentos de pesquisa**

* Agora os administradores podem [configurar o tamanho do lote dos ativos](/help/assets/search-assets.md#configure-asset-batch-size) exibidos quando você realizar uma pesquisa. Os resultados da pesquisa de ativos são exibidos em múltiplos do número de tamanho de lote configurado ao rolar a tela para baixo para carregar os resultados. Você pode selecionar entre os tamanhos de lote disponíveis de 200, 500 e 1000 ativos. Definir um número de tamanho de lote mais baixo resulta em tempos de resposta de pesquisa mais rápidos.

  ![Configuração de tamanho de lote do Assets](/help/release-notes/assets/assets-batch-size-configuration.png)

* O Experience Manager Assets agora inclui uma nova versão 9 do índice `damAssetLucene`. `damAssetLucene-9` altera o comportamento da contagem facetada da Consulta do Oak para [não avaliar mais o controle de acesso nas contagens facetadas](/help/assets/search-assets.md) retornadas pelo índice de pesquisa subjacente, o que resulta em tempos de resposta de pesquisa mais rápidos.

### Recursos de pré-lançamento disponíveis em [!DNL Experience Manager Assets] {#prerelease-features-assets}

* **Dynamic Media**: [Suporte a várias legendas e faixas de áudio para vídeos no Dynamic Media](/help/assets/dynamic-media/video.md#about-msma)—Agora é possível adicionar facilmente várias legendas e faixas de áudio a um vídeo principal. Esse recurso significa que os vídeos estão acessíveis em um público-alvo global. Você pode personalizar um único vídeo principal publicado para um público-alvo global em vários idiomas e seguir as diretrizes de acessibilidade para diferentes regiões geográficas. Os autores também podem gerenciar as legendas e faixas de áudio em uma única guia na interface do usuário do.

  ![Guia Legendas e Faixas de áudio na página Propriedades de um ativo de vídeo selecionado.](/help/release-notes/assets/msma-aem-cs.png)*Guia Legendas e Faixas de áudio na página Propriedades de um ativo de vídeo selecionado.*

* **Assets**: capacidade de selecionar arquivos ZIP gerenciados no Experience Manager e [extrair os arquivos diretamente no Experience Manager](/help/assets/manage-digital-assets.md#extract-zip-archives) sem baixá-los.

  ![Fixação de itens para grupos](/help/release-notes/assets/extract-archive.png)


## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Novos recursos disponíveis em [!DNL Forms] {#new-features-available-in-forms-channel}

* [**Suporte empresarial para o Google reCAPTCHA**](/help/forms/captcha-adaptive-forms.md): use o Google reCAPTCHA Enterprise em um Formulário adaptável para fornecer proteção aprimorada contra atividades fraudulentas e spam, proporcionando uma experiência mais segura para o usuário. Com a análise de risco avançada e a integração perfeita, os usuários genuínos podem enviar formulários facilmente, enquanto os bots são bloqueados de maneira eficaz.


### Recursos de pré-lançamento disponíveis em [!DNL Forms] {#pre-release-features-available-in-forms-channel}

* **Adobe Analytics com Automação de Instalação do Experience Cloud para Forms**: agora é possível habilitar o Adobe Analytics com Automação de Instalação do Experience Cloud com alguns botões. Ela permite conectar o AEM Forms as a Cloud Service com tags da Experience Platform e Adobe Analytics para capturar e rastrear métricas de desempenho para seus formulários publicados.

* **Modelo de relatório do Adobe Analytics para o Adaptive Forms**: o Forms as a Cloud Service agora fornece um relatório do Adobe Analytics OOTB. Ele ajuda você a entender facilmente o desempenho de seus formulários. As métricas no nível do formulário fornecem uma insight sobre o desempenho do formulário em vários indicadores-chave de desempenho (KPIs), como representações, visitantes, envios e tempo médio de preenchimento. Ao rastrear o comportamento do usuário e o feedback, você pode identificar áreas do formulário que estão causando confusão e orientar melhorias no design e na funcionalidade do formulário.

  ![Relatório do adobe analytics de engajamento do usuário do formulário adaptável](/help/forms/assets/forms-analytics-report.png)

* **[Fragmento de formulário no Adaptive Forms com base nos Componentes principais](/help/forms/adaptive-form-fragments-core-components.md)**: Diga adeus à duplicação, otimize seu inventário digital e melhore a colaboração à medida que você eleva sua experiência de criação de formulários com Fragmentos de formulário. Esses componentes reutilizáveis se integram perfeitamente em vários formulários, simplificando a criação de formulários consistentes e com aparência profissional. Os fragmentos de formulário garantem a reutilização, a padronização e a consistência da marca por meio da funcionalidade &quot;alterar uma vez e refletir em todos os lugares&quot;. Experimente maior capacidade de manutenção e eficiência, já que as atualizações feitas em um local são propagadas automaticamente em todos os formulários que utilizam esses fragmentos.

* **[Etapa aprimorada do fluxo de trabalho do Adobe Sign](/help/forms/aem-forms-workflow-step-reference.md#sign-document-step-sign-document-step)**: a etapa do fluxo de trabalho do Adobe Sign foi aprimorada para incluir o seguinte:
   * **Autenticação com base em ID do governo para o Adobe Sign**: a autenticação com base em ID do governo da Adobe Acrobat Sign oferece uma camada adicional de verificação, permitindo que os usuários autentiquem sua identidade usando IDs emitidas pelo governo (CNH, identificação nacional, passaporte). Ao usar documentos de identificação confiáveis, esse aprimoramento adiciona um nível extra de confiança ao processo de assinatura, tornando-o ideal para cenários que exigem maior segurança, conformidade e validação do usuário.

   * **Trilha de auditoria para documentos do Adobe Sign**: use o recurso de Trilha de auditoria para obter insights detalhados sobre o ciclo de vida dos documentos do Adobe Sign. Com a Trilha de auditoria, agora é possível manter um registro abrangente de todas as ações e interações relacionadas aos documentos. Isso inclui detalhes como quem visualizou, editou ou assinou o documento, além de carimbos de data e hora para cada evento. Esse aprimoramento é fundamental para manter a conformidade, resolver disputas e garantir a integridade de seus contratos digitais.

   * **Novas funções para destinatários do Contrato além apenas do Signatário**: a Adobe Acrobat Sign tem a opção de expandir as funções para destinatários do Contrato além apenas do Signatário para melhor corresponder aos requisitos de fluxo de trabalho. Quando habilitado, cada recipient em um Contrato tem sua função configurável individualmente, sendo que Signatário é o padrão.

* **[Proteger seus documentos com as APIs do Document Assurance (Parte das APIs de Comunicação)](/help/forms/aem-forms-cloud-service-communications-introduction.md#document-assurance-doc-assurance)**: as APIs do Document Assurance permitem que você proteja informações confidenciais ao assinar e criptografar os documentos. Por meio da criptografia, o conteúdo de um documento é transformado em um formato ilegível, garantindo que somente usuários autorizados possam ter acesso. Essa camada fortificada de proteção não apenas protege dados valiosos de olhos não autorizados, mas também proporciona tranquilidade. As APIs de assinatura permitem que sua organização proteja a segurança e a privacidade dos documentos do Adobe PDF que distribui e recebe. Esse serviço usa assinaturas digitais e certificação para garantir que somente os recipients desejados possam alterar os documentos.

* **Suporte para Contagem de Páginas em APIs de Comunicação**: Agora, juntamente com a recuperação do documento por meio das APIs de Comunicação, você também pode receber as informações valiosas sobre o número de páginas contidas no documento.

* **[Tratamento de erros com manipuladores de erros personalizados no editor de regras](/help/forms/add-custom-error-handler-adaptive-forms-core-components.md)**: agora é possível invocar uma função personalizada em resposta a um erro retornado por um serviço externo e fornecer uma resposta personalizada aos usuários finais. Por exemplo, você pode acionar um fluxo de trabalho personalizado no back-end para códigos de erro específicos ou informar ao cliente que o serviço está inativo.


### Programa de adoção antecipada de formulários adaptáveis headless {#forms-early-adopter}

Use [Formulários adaptáveis Headless](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html?lang=pt-BR) para permitir que seus desenvolvedores criem, publiquem e gerenciem formulários interativos que podem ser acessados e manuseados por meio de APIs, em vez de utilizar uma interface gráfica tradicional. Os formulários adaptáveis headless ajudam a:

* criar formulários multicanal de alta qualidade na linguagem de programação de sua escolha
* integrar formulários nativamente a seus aplicativos móveis e de desktop, sites e aplicativos de bate-papo
* reutilizar os componentes de interface de sua propriedade com aplicativos de formulários
* aproveitar o potencial do Adobe Experience Manager Forms

Você pode enviar um email para `aem-forms-headless@adobe.com` utilizando sua ID de email oficial para participar do programa de adoção antecipada.


## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Logs CDN {#cdn-logs}

Baixe logs CDN do Cloud Manager, que é útil para otimização da taxa de ocorrência do cache e maior visibilidade do fluxo de entrega de conteúdo. [Saiba mais sobre](/help/implementing/developing/introduction/logging.md#cdn-log) o formato de log da CDN. Esse recurso será gradualmente lançado para os clientes no início de setembro.

### Programa de adoção antecipada das Regras CDN e WAF {#waf-early-adopter}

Filtrar o tráfego na CDN com base em:

* cabeçalhos e propriedades de solicitação (por exemplo, endereço IP)
* padrões de tráfego conhecidos por estarem associados a tráfego mal-intencionado

Interessado em experimentar o recurso e compartilhar feedback? Envie um email para **aemcs-waf-adopter@adobe.com** a partir da sua ID de email oficial para saber mais sobre o programa de adoção antecipada. O espaço é limitado.

Saiba mais sobre o recurso no artigo [aqui](/help/security/traffic-filter-rules-including-waf.md).


## Notas da versão de manutenção {#maintenance}

Encontre as notas de versão de manutenção mais recentes [aqui](/help/release-notes/maintenance/latest.md).

## Cloud Manager {#cloud-manager}

Você pode encontrar uma lista completa de versões mensais do Cloud Manager [aqui](/help/implementing/cloud-manager/release-notes/current.md).

## Ferramentas de migração {#migration-tools}

Você pode encontrar uma lista completa de versões das ferramentas de migração [aqui](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
