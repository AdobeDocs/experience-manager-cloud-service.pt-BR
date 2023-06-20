---
title: Notas de versão do [!DNL Adobe Experience Manager]  as a Cloud Service 2021.4.0.
description: Notas de versão do [!DNL Adobe Experience Manager]  as a Cloud Service 2021.4.0.
exl-id: 775332b5-24ce-430e-97a2-6eeb80877c64
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '1533'
ht-degree: 25%

---

# Notas de versão atuais do [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

A seção a seguir descreve as Notas de versão gerais da versão atual (mais recente) do [!DNL Adobe Experience Manager] as a Cloud Service.

>[!NOTE]
>A partir daqui, você pode navegar até as notas de versão das versões anteriores; por exemplo, para aquelas em 2020, 2021 e assim por diante.

>[!NOTE]
>
>Consulte [Atualizações recentes na documentação](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=pt-BR) para obter detalhes de atualizações de documentação não relacionadas diretamente a uma versão.

## Data de lançamento {#release-date}

A data de lançamento do [!DNL Adobe Experience Manager] O as a Cloud Service 2021.4.0 é 6 de maio de 2021.
A versão seguinte (2021.5.0) será lançada em 27 de maio de 2021.

## Fundação as a Cloud Service AEM{#aem-as-a-cloud-service-foundation}

### Novidades {#what-is-new-foundation}

* [Fluxo de trabalho de publicação da árvore de conteúdo](/help/operations/replication.md#publish-content-tree-workflow) - Um novo modelo de fluxo de trabalho e uma nova etapa proporcionam melhor desempenho ao publicar hierarquias profundas de conteúdo.

## [!DNL Adobe Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Novidades do [!DNL Sites] {#what-is-new-sites}

* Terminais do GraphQL - agora é possível habilitar a API AEM do GraphQL para configurações individuais do AEM Sites e criar terminais GraphQL personalizados para essas configurações usando uma nova interface de console do GraphQL. A interface também permite gerenciar endpoints do GraphQL.

* Modelos de conteúdo, tipo de data e hora aprimorado — agora é possível configurar o tipo de data e hora para permitir a criação de informações apenas de data, apenas de hora ou de data e hora.

* Modelos de conteúdo, tipo de dados aprimorado Tags — agora é possível configurar o tipo de dados Tags para permitir a criação de tags únicas ou múltiplas.

* Modelos de conteúdo, novo tipo de dados Espaço reservado de guia — o novo tipo de dados Espaço reservado de guia permite agrupar tipos de dados em seções que são renderizadas em guias no editor de fragmento de conteúdo.

### Correções de erros no [!DNL Sites] {#bug-fixes-sites}

* Fragmentos de conteúdo - mover fragmentos ou pastas de conteúdo agora atualiza referências aninhadas dentro do fragmento (CQ-4320815)

* GraphQL - as consultas persistentes agora oferecem suporte a endpoints definidos pelo usuário que são específicos para configurações do AEM Sites (CQ-4315928)

## [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Novidades do [!DNL Assets] {#what-is-new-assets}

* [!DNL Experience Manager] O não arquiva downloads de ativos únicos em que o arquivo original é baixado. Esse aprimoramento permite downloads mais rápidos.

* Quando um ativo é baixado por meio da opção linkshare, agora é possível optar por baixar ou não as representações. Anteriormente, todas as representações de ativos eram baixadas.

* Os administradores podem configurar [!DNL Experience Manager] para excluir a origem de ativos depois de fazer uma assimilação de ativos em massa. Consulte [assimilação de ativos em massa](/help/assets/add-assets.md#asset-bulk-ingestor).

* Ao executar uma verificação de integridade para importar ativos em massa, o Experience Manager agora fornece mais motivos de informações sobre falhas. Consulte [assimilação de ativos em massa](/help/assets/add-assets.md#asset-bulk-ingestor).

* Ao importar ativos usando a ferramenta de importação em massa, os administradores agora têm a opção de excluir os arquivos de origem após a importação ser bem-sucedida. Consulte [assimilação de ativos em massa](/help/assets/add-assets.md#asset-bulk-ingestor).

* Ao editar um esquema de metadados, um novo campo seletor de caminho raiz permite que os administradores façam a seleção de forma rápida e fácil, reduzindo assim o tempo de configuração.

* Ao editar um esquema de metadados, um tipo de dados que fornece uma área de texto de forma livre no editor de metadados é adicionado. Os usuários podem usar essa área de texto para inserir texto de forma livre como metadados de um ativo. Consulte [editor de esquema de metadados](/help/assets/metadata-schemas.md).

* Os metadados de muitos ativos podem ser importados em massa usando um arquivo CSV e podem ser exportados para um arquivo CSV. O formato de data padrão agora é `yyyy-MM-dd'T'HH:mm:ss.SSSXXX`. Os usuários podem usar um formato diferente atualizando o cabeçalho da coluna. Por exemplo, adicione `Date: DateFormat: yyyy-MM-dd'T'HH:mm:ssXXX` como o cabeçalho da coluna no arquivo CSV em vez da palavra `Date`.

* Ao navegar pelos ativos na exibição Coluna, um indicador visual exibe o status aprovado ou rejeitado de cada ativo.

* Ao navegar pelos ativos na exibição Coluna, um indicador visual é exibido para ativos expirados.

### Correções de erros no [!DNL Assets] {#bug-fixes-assets}

* Ao tentar mover vários ativos ou pastas, um erro é registrado no console e a operação de movimentação não é concluída. A operação de movimentação falha se o título não puder ser atualizado. (CQ-4322080)

* Um campo de metadados pode ser oculto com base em uma regra de forma que, quando uma condição predefinida for atendida, os metadados não sejam obrigatórios. No entanto, esses campos de metadados ocultos são exibidos como campos obrigatórios. (CQ-4321285)

* A importação de metadados em massa falha devido ao formato de data incorreto. (CQ-4319014)

* Quando é feita uma seleção na página Propriedades para atualizar metadados, a interface fica lenta para responder quando há muitas opções fornecidas pelo esquema. (CQ-4318538)

* Ao atualizar e salvar o valor de metadados em um campo de texto de linha única, os valores no menu suspenso são excluídos, mesmo que as edições estejam desativadas no menu suspenso. (CQ-4317077)

* É possível usar reticências como uma anotação para revisar ativos. Quando uma pequena elipse é usada, ela se sobrepõe ao número da anotação na versão impressa. (CQ-4316792)

* A opção de publicação rápida não é exibida quando um ativo é selecionado nos resultados da pesquisa após pesquisá-lo. (CQ-4317748)

## [!DNL Adobe Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Novidades do [!DNL Forms] {#what-is-new-forms}

* **Usar o método de autenticação de ID do governo no Adaptive Forms habilitado para Adobe Sign**

  Alimentado por algoritmos avançados de aprendizado de máquina, o processo de ID do governo da Adobe Sign oferece a empresas do mundo todo a capacidade de garantir uma autenticação de alta qualidade da identidade do recipient. Agora, você pode usar o método de autenticação de ID do governo no Adaptive Forms habilitado para Adobe Sign.

  ID do governo é um método de autenticação de identidade premium que instrui o recipient a [carregar a imagem de um documento de identidade emitido pelo governo (CNH, identificação nacional, passaporte)](https://helpx.adobe.com/in/sign/using/adobesign-authentication-government-id.html)e avalia esse documento para garantir sua autenticidade.

* **Suporte para usar a experiência de assinatura no formulário para envios assíncronos de formulários adaptáveis**

  Agora você pode usar a experiência de assinatura no formulário para envios assíncronos de formulários adaptáveis. Também é possível incorporar um formulário adaptável em uma [!DNL Experience Manager Sites] e use a experiência de assinatura no formulário para envios de formulários adaptáveis.

* **Suporte para usar uma variável para especificar um anexo enquanto preenche um formulário adaptável para uma etapa Atribuir tarefa**

  Ao preencher previamente um formulário adaptável para uma etapa Atribuir tarefa, agora é possível usar uma variável do tipo de documento para selecionar um anexo de entrada para o formulário adaptável.

* **Suporte para usar a opção literal para definir valor para uma variável do tipo JSON**

  Você pode usar a opção literal para definir o valor de uma variável do tipo JSON na etapa Definir variável de um fluxo de trabalho AEM. A opção literal permite especificar um JSON no formato de uma string.

* **Usar o ambiente de desenvolvimento local para criar um Documento de registro (DoR)**

  Você pode usar um XDP como um modelo de Documento de registro em instâncias do Cloud Service e SDK as a Cloud Service do AEM Forms (Ambiente de desenvolvimento local). Anteriormente, o suporte estava limitado apenas a instâncias Cloud Service.

### Correções de erros no [!DNL Forms] {#bug-fixes-forms}

* Quando um Formulário adaptável configurado para não gerar um Documento de registro é enviado a um Fluxo de trabalho do AEM configurado para gerar Documento de registro, nenhuma mensagem de erro é exibida e a tarefa não é enviada.

### Outras atualizações {#misc-2021-04-0-forms}

* Para facilitar o reconhecimento de conteúdo, o serviço agora gera uma miniatura ativa para arquivos XDP, Dynamic PDF e Schema.
* Adicione a capacidade de mover um arquivo PDF para uma pasta colocada na interface do usuário do AEM Forms.

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novidades {#what-is-new-commerce}

* Suporte para UID de categoria - Isso desbloqueia integrações comerciais de terceiros para sistemas que usam Strings para IDs de categoria

* Extensão AEM para PWA Studio incl. exemplo de integração

* Novo componente principal de navegação da CIF que estende o componente principal de navegação do WCM

* Indicador visual para dados de catálogo preparados na loja AEM

* O ponto de extremidade de comércio agora pode ser configurado por meio da interface do usuário do Cloud Manager

### Correções de erros {#bug-fixes-commerce}

* O campo de categoria raiz não era exibido na guia commerce nas propriedades da página de páginas de categoria

## Cloud Manager {#cloud-manager}

Esta seção descreve as Notas de versão do Cloud Manager no AEM as a Cloud Service 2021.4.0.

### Data de lançamento {#release-date-cm-april}

A data de lançamento do Cloud Manager no AEM as a Cloud Service 2021.4.0 é 8 de abril de 2021.
A próxima versão está planejada para 6 de maio de 2021.

### Novidades {#what-is-new-april}

* Atualizações na interface do usuário dos fluxos de trabalho Adicionar e Editar programa para torná-los mais intuitivos.

* Um usuário com as permissões necessárias agora pode enviar o endpoint de comércio por meio da interface do usuário.

* Agora, as variáveis de ambiente podem ser enviadas para um serviço específico, seja de criação ou de publicação. Exige o AEM versão `2021.03.5104.20210328T185548Z` ou superior.

* O botão **Gerenciar Git** é exibido no cartão Pipelines, mesmo quando não houver nenhum pipeline configurado.

* O arquétipo de projeto AEM usado pelo Cloud Manager foi atualizado para a versão 27.

* Os projetos no Console do desenvolvedor do Adobe I/O criados pelo Cloud Manager não podem mais ser editados ou excluídos involuntariamente.

* Quando um usuário adiciona um novo ambiente, ele é informado de que, depois que um ambiente é criado, ele não pode ser movido para uma região diferente.

* Agora, as variáveis de ambiente podem ser enviadas para um serviço específico, seja de criação ou de publicação. Exige o AEM versão 2021.03.5104.20210328T185548Z ou superior.

* A mensagem de erro ao iniciar um pipeline com um ambiente excluído foi esclarecida.

* Os pacotes OSGi fornecidos pelos projetos Eclipse agora são excluídos da regra `CQBP-84--dependencies`.

### Correções de erros {#bug-fixes-cm-april}

* Ao editar a página de auditoria da experiência de um pipeline, um caminho de entrada que começa com uma barra `( / )` não fará mais a etapa ficar travada no status pendente.

* Quando um novo pipeline de produção é criado, se nenhuma substituição de auditoria de conteúdo for adicionada pelo usuário, a página inicial padrão não será auditada.

* Os problemas do `CloudServiceIncompatibleWorkflowProcess` exibiam a gravidade incorreta no arquivo CSV de problemas disponível para download.

* A verificação `Runmode` estava produzindo falsos positivos em nós que não eram pastas.

## Analisador de práticas recomendadas {#best-practices-analyzer}

### Data de lançamento {#release-date-bpa}

A data de lançamento do Analisador de práticas recomendadas v2.1.12 é 12 de abril de 2021.

### Correções de erros {#bug-fixes-bpa-april}

* Linhas duplicadas foram vistas no BPA relatado. Isso foi corrigido.
* A interface do usuário do BPA no AEM versão 6.4.2 gerava um erro JS que desativava o botão Gerar relatório. Isso foi corrigido.
