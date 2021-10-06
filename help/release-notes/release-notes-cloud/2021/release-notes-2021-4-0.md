---
title: Notas de versão do  [!DNL Adobe Experience Manager] as a Cloud Service 2021.4.0.
description: Notas de versão do  [!DNL Adobe Experience Manager] as a Cloud Service 2021.4.0.
source-git-commit: 85b78564620dce8f660098a8cbaadd6f5ed0c616
workflow-type: tm+mt
source-wordcount: '1535'
ht-degree: 3%

---


# Notas de versão atuais para [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

A seção a seguir descreve as Notas de versão gerais da versão atual (mais recente) do [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>Desse ponto, você pode navegar até as notas de versão das versões anteriores; por exemplo, para aqueles em 2020, 2021 e assim por diante.

>[!NOTE]
>
>Consulte [Atualizações recentes na documentação](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html) para obter detalhes das atualizações de documentação não diretamente relacionadas a uma versão.

## Data de lançamento {#release-date}

A Data de lançamento para [!DNL Adobe Experience Manager] as a Cloud Service 2021.4.0 é 6 de maio de 2021.
A seguinte versão (2021.5.0) será lançada em 27 de maio de 2021.

## AEM fundação as a Cloud Service{#aem-as-a-cloud-service-foundation}

### Novidades {#what-is-new-foundation}

* [Fluxo de trabalho da Árvore de conteúdo de publicação](/help/operations/replication.md#publish-content-tree-workflow)  - Um novo modelo de fluxo de trabalho e uma etapa proporcionam maior desempenho ao publicar hierarquias profundas de conteúdo.

## [!DNL Adobe Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Novidades em [!DNL Sites] {#what-is-new-sites}

* Endpoints GraphQL - agora é possível habilitar a API GraphQL da AEM para configurações AEM Sites individuais e criar pontos de extremidade GraphQL personalizados para essas configurações usando uma nova interface do usuário do console GraphQL. A interface do usuário também permite o gerenciamento de pontos de extremidade GraphQL.

* Modelos de conteúdo, tipo de dados aprimorado de Data e Hora - agora é possível configurar o tipo de data e hora para permitir a criação apenas de data, hora ou informações de data e hora.

* Modelos de conteúdo, tipo de dados Tags aprimoradas - agora é possível configurar o tipo de dados Tags para permitir a criação de tags únicas ou múltiplas.

* Modelos de conteúdo, novo tipo de dados de Espaço reservado de guia - o novo tipo de dados de Espaço reservado de guia permite agrupar tipos de dados em seções que serão renderizadas em guias no editor de fragmento de conteúdo.

### Correções de erros em [!DNL Sites] {#bug-fixes-sites}

* Fragmentos de conteúdo - mover fragmentos de conteúdo ou pastas agora atualiza referências aninhadas dentro do fragmento (CQ-4320815)

* GraphQL - As consultas persistentes agora oferecem suporte a endpoints definidos pelo usuário que são específicos das configurações do AEM Sites (CQ-4315928)

## [!DNL Adobe Experience Manager Assets] como  [!DNL Cloud Service] {#assets}

### Novidades em [!DNL Assets] {#what-is-new-assets}

* [!DNL Experience Manager] não arquiva downloads de ativos únicos onde o arquivo original é baixado. Esse aprimoramento permite downloads mais rápidos.

* Quando um ativo é baixado por meio da opção linkshare, você pode optar por baixar ou não as representações. Anteriormente, todas as representações de ativos eram baixadas.

* Os administradores podem configurar [!DNL Experience Manager] para excluir a fonte de ativos depois de fazer ingestões de ativos em massa. Consulte [assimilação de ativos em massa](/help/assets/add-assets.md#asset-bulk-ingestor).

* Ao executar uma verificação de integridade para importar ativos em massa, o Experience Manager agora fornece mais motivos de informações para falhas. Consulte [assimilação de ativos em massa](/help/assets/add-assets.md#asset-bulk-ingestor).

* Ao importar ativos usando a ferramenta de importação em massa, os administradores agora têm a opção de excluir os arquivos de origem após a importação ser bem-sucedida. Consulte [assimilação de ativos em massa](/help/assets/add-assets.md#asset-bulk-ingestor).

* Ao editar um esquema de metadados, um novo campo seletor de caminho raiz permite que os administradores façam a seleção de forma rápida e fácil, reduzindo assim o tempo de configuração.

* Ao editar um esquema de metadados, é adicionado um tipo de dados que fornece uma área de texto de forma livre no editor de metadados. Os usuários podem usar essa área de texto para inserir texto de forma livre como metadados de um ativo. Consulte [editor de esquema de metadados](/help/assets/metadata-schemas.md).

* Os metadados de muitos ativos podem ser importados em massa usando um arquivo CSV e podem ser exportados para um arquivo CSV. O formato de data padrão agora é `yyyy-MM-dd'T'HH:mm:ss.SSSXXX`. Os usuários podem aproveitar um formato diferente ao atualizar o cabeçalho da coluna. Por exemplo, adicione `Date: DateFormat: yyyy-MM-dd'T'HH:mm:ssXXX` como o cabeçalho da coluna no arquivo CSV em vez da palavra `Date`.

* Ao navegar pelos ativos na exibição em Coluna, um indicador visual exibe o status aprovado ou rejeitado de cada ativo.

* Ao navegar pelos ativos na exibição em Coluna, um indicador visual é exibido para os ativos expirados.

### Correções de erros em [!DNL Assets] {#bug-fixes-assets}

* Ao tentar mover vários ativos ou pastas, um erro é registrado no console e a operação de movimentação não é concluída. A operação de movimentação falhará se o título não puder ser atualizado. (CQ-4322080)

* Um campo de metadados pode ser oculto com base em uma regra, de modo que, quando uma condição predefinida é atendida, os metadados não são obrigatórios. No entanto, esses campos de metadados ocultos são exibidos como campos obrigatórios. (CQ-4321285)

* A importação de metadados em massa falha devido ao formato de data incorreto. (CQ-4319014)

* Quando uma seleção é feita na página Propriedades para atualizar metadados, a interface fica lenta para responder quando há muitas opções fornecidas pelo esquema. (CQ-4318538)

* Ao atualizar e salvar o valor de metadados em um campo de texto de uma única linha, os valores no menu suspenso são excluídos, mesmo que as edições estejam desativadas no menu suspenso. (CQ-4317077)

* Você pode usar reticências como uma anotação para revisar ativos. Quando uma pequena elipse é usada, a elipse se sobrepõe ao número da anotação na versão impressa. (CQ-4316792)

* A opção de publicação rápida não é exibida quando um ativo é selecionado nos resultados da pesquisa após pesquisá-lo. (CQ-4317748)

## [!DNL Adobe Experience Manager Forms] como  [!DNL Cloud Service] {#forms}

### Novidades em [!DNL Forms] {#what-is-new-forms}

* **Usar o método de autenticação de identidade do Governo no Adobe Sign Adaptive Forms habilitado**

   Alimentado por algoritmos avançados de aprendizado de máquina, o processo de ID do governo da Adobe Sign capacita empresas em todo o mundo com a capacidade de garantir uma autenticação de alta qualidade da identidade do destinatário. Agora, você pode usar o método de autenticação de identidade do Governo no Adobe Sign Adaptive Forms habilitado.

   ID do governo é um método de autenticação de identidade premium que instrui o recipient a [carregar a imagem de um documento de identidade emitido pelo governo (licença de motorista, ID nacional, passaporte)](https://helpx.adobe.com/in/sign/using/adobesign-authentication-government-id.html), e então avalia esse documento para garantir que ele seja autêntico.

* **Suporte para usar a experiência de assinatura no formulário para envios assíncronos de formulários adaptáveis**

   Agora é possível usar a experiência de assinatura no formulário para envios assíncronos de formulários adaptáveis. Você também pode incorporar um formulário adaptável em uma página [!DNL Experience Manager Sites] e usar a experiência de assinatura no formulário para envios de formulários adaptáveis.

* **Suporte para usar uma variável para especificar um anexo ao preencher previamente um Formulário adaptável para uma etapa Atribuir tarefa**

   Ao pré-preencher um formulário adaptável para uma etapa Atribuir tarefa , agora é possível usar uma variável do tipo de documento para selecionar um anexo de entrada para o formulário adaptável.

* **Suporte para usar a opção literal para definir valor para uma variável do tipo JSON**

   Você pode usar a opção literal para definir um valor para uma variável do tipo JSON na etapa Definir variável de um fluxo de trabalho AEM. A opção literal permite especificar um JSON no formato de uma string.

* **Usar o ambiente de desenvolvimento local para criar Documento de registro (DoR)**

   Você pode usar um XDP como modelo de Documento de registro em instâncias do Cloud Service e no SDK as a Cloud Service do AEM Forms (ambiente de desenvolvimento local). Anteriormente, o suporte estava limitado apenas a instâncias Cloud Service.

### Correções de erros em [!DNL Forms] {#bug-fixes-forms}

* Quando um Formulário adaptável configurado para não gerar Documento de registro é enviado a um Fluxo de trabalho AEM configurado para gerar Documento de registro, nenhuma mensagem de erro é exibida e a tarefa não é enviada.

### Outras atualizações {#misc-2021-04-0-forms}

* Para facilitar o reconhecimento de conteúdo, o serviço agora gera uma miniatura em tempo real para arquivos XDP, Dynamic PDF e Schema.
* Adicione a capacidade de mover um arquivo do PDF para uma pasta colocada na interface do usuário do AEM Forms.

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novidades {#what-is-new-commerce}

* Suporte para UID de categoria - Isso desbloqueia integrações de comércio de terceiros para sistemas que usam Strings para ids de categoria

* AEM extensão para PWA Studio incl. integração de exemplo

* Novo componente principal de navegação da CIF que estende o componente principal de navegação do WCM

* Indicador visual para dados de catálogo preparados na loja de AEM

* O endpoint de comércio agora é configurável por meio da interface do usuário do Cloud Manager

### Correções de erros {#bug-fixes-commerce}

* O campo categoria raiz não era exibido na guia Comércio nas propriedades de página das páginas de categoria

## Cloud Manager {#cloud-manager}

Esta seção descreve as Notas de versão do Cloud Manager AEM as a Cloud Service 2021.4.0.

### Data de lançamento {#release-date-cm-april}

A Data de lançamento do Cloud Manager AEM as a Cloud Service 2021.4.0 é 8 de abril de 2021.
A próxima versão está planejada para 06 de maio de 2021.

### Novidades {#what-is-new-april}

* Atualizações da interface do usuário para os fluxos de trabalho Adicionar e editar programa para torná-lo mais intuitivo.

* Um usuário com as permissões necessárias agora pode enviar o ponto final de comércio por meio da interface do usuário do .

* Agora, as variáveis de ambiente podem ser enviadas para um serviço específico, seja de criação ou de publicação. Exige AEM versão `2021.03.5104.20210328T185548Z` ou superior.

* O botão **Gerenciar Git** é exibido no cartão Pipelines mesmo quando nenhum pipeline foi configurado.

* A versão do arquétipo de projeto AEM usado pelo Cloud Manager foi atualizada para a versão 27.

* Os projetos no Console do desenvolvedor do Adobe I/O criados pelo Cloud Manager não podem mais ser editados ou excluídos involuntariamente.

* Quando um usuário adiciona um novo ambiente, ele é informado que, uma vez criado um ambiente, ele não pode ser movido para uma região diferente.

* Agora, as variáveis de ambiente podem ser enviadas para um serviço específico, seja de criação ou de publicação. Exige AEM versão 2021.03.5104.20210328T185548Z ou superior.

* A mensagem de erro ao iniciar um pipeline quando um ambiente foi excluído foi esclarecida.

* Pacotes OSGi fornecidos por projetos Eclipse agora são excluídos da regra `CQBP-84--dependencies`.

### Correções de erros {#bug-fixes-cm-april}

* Ao editar a página Auditoria de experiência de um pipeline, um caminho de entrada que começa com uma barra `( / )` não resultará mais na etapa presa no status pendente.

* Quando um novo pipeline de produção é criado, se nenhuma substituição de auditoria de conteúdo for adicionada pelo usuário, a página inicial padrão não foi auditada.

* Os problemas para `CloudServiceIncompatibleWorkflowProcess` tinham a severidade incorreta no arquivo CSV de problema baixável.

* A verificação `Runmode` estava produzindo falsos positivos em nós que não eram pastas.

## Analisador de práticas recomendadas {#best-practices-analyzer}

### Data de lançamento {#release-date-bpa}

A data de lançamento do Analisador de práticas recomendadas v2.1.12 é 12 de abril de 2021.

### Correções de erros {#bug-fixes-bpa-april}

* Linhas duplicadas foram vistas no BPA relatado. Isso foi corrigido.
* A interface do usuário do BPA AEM versão 6.4.2 estava exibindo um erro de JS que estava desativando o botão Gerar relatório . Isso foi corrigido

