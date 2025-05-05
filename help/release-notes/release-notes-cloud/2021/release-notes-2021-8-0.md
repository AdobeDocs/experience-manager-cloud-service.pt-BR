---
title: Notas de versão do  [!DNL Adobe Experience Manager]  as a Cloud Service 2021.8.0.
description: Notas de versão do  [!DNL Adobe Experience Manager]  as a Cloud Service 2021.8.0.
exl-id: 8b041934-1c4a-4670-9b03-d38f683b99e5
feature: Release Information
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '1011'
ht-degree: 23%

---

# Notas de versão atuais do [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

A seção a seguir descreve as Notas de versão gerais da versão atual (mais recente) do [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Aqui, você pode navegar até as notas de versão de versões anteriores. Por exemplo, para aqueles em 2020 e 2021.

>[!NOTE]
>
>Consulte [Atualizações recentes na documentação](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=pt-BR) para obter detalhes de atualizações de documentação não relacionadas diretamente a uma versão.

## Data de lançamento {#release-date}

A data de lançamento da versão atual (2021.8.0) do [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] é sexta-feira, 26 de agosto de 2021.
A versão seguinte (2021.9.0) será lançada em quinta-feira, 6 de outubro de 2021.

## Vídeo da versão {#release-video}

Assista ao vídeo [Visão geral da versão de agosto de 2021](https://video.tv.adobe.com/v/336277) para ver um resumo dos recursos adicionados.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Novos recursos no [!DNL Assets] {#assets-features}

* Ao compartilhar ativos digitais como um link, o usuário pode copiar o URL para a área de transferência imediatamente. O aprimoramento permite compartilhar ativos de maneira mais rápida e prática. Essa funcionalidade permite um compartilhamento de ativos mais rápido e prático.

  ![Opção Copiar URL ao compartilhar um ativo como um link](/help/assets/assets/link-share-copy-URL-option.png)
  *Figura: ao compartilhar um ativo como um link, agora é possível copiar a URL para compartilhá-lo separadamente.*

* Ao fazer upload de arquivos TXT, os microsserviços de ativos geram automaticamente uma miniatura. A miniatura de PNG é uma representação de um arquivo TXT que ajuda os usuários a identificar o conteúdo ou os arquivos até certo ponto, sem abrir os arquivos. Essa funcionalidade não requer configuração e funciona por padrão.

  ![Uma representação de um arquivo TXT é gerada automaticamente por [!DNL Assets] em formato PNG](/help/assets/assets/thumbnail-rendition-txt-file.png)
  *Figura: uma representação de um arquivo TXT é gerada automaticamente para ajudá-lo a identificar o arquivo sem abri-lo.*

### Novo recurso no canal de pré-lançamento do [!DNL Assets] {#assets-prerelease-features}

* Agora os usuários podem classificar os ativos exibidos nos resultados da pesquisa nas visualizações de Coluna e Cartão. A classificação funciona nas colunas Nome, Criado, Modificado ou Nenhum.

  ![Classificar os resultados da pesquisa em [!DNL Assets] nos modos de exibição de Coluna e Cartão](/help/assets/assets/sort-searched-assets.png)
  *Figura: Classifique os resultados da pesquisa em [!DNL Assets] nos modos de exibição Coluna e Cartão.*

### Bugs corrigidos em [!DNL Assets] {#assets-bugs-fixed}

* Quando um membro do grupo de colaboradores navega até o Console [!DNL Assets], uma solicitação `POST` extra é gerada para criar uma Coleção. Essa solicitação não é necessária; ela falha devido a problemas de permissão e cria muitos erros nos logs. (CQ-4328856)
* Quando os usuários visualizam um ativo e selecionam a [!UICONTROL Linha do tempo] no menu pop-up no painel esquerdo, um erro é exibido. Nos logs, muitos avisos são registrados devido a uma consulta inválida. (CQ-4328919)

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Novidades do [!DNL Forms] {#what-is-new-forms}

* O serviço Automated forms conversion pode [converter PDF forms em italiano e português](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?lang=pt-BR&#language-specific-meta-model) para o Adaptive Forms.

* **Documento de Registro baseado em acroforma**: o AEM Forms as a Cloud Service suporta o uso do [PDF de Formulário Adobe Acrobat (PDF de acroforma)](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/generate-document-of-record-for-non-xfa-based-adaptive-forms.html?lang=pt-br) como um modelo para Documento de Registro além do modelo de formulário baseado em XFA.

* **Conector do armazenamento de dados do Microsoft® Azure**: agora é possível [conectar o Modelo de dados do formulário ao Armazenamento do Microsoft® Azure](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/configure-azure-storage.html?lang=pt-BR). Ele permite recuperar e armazenar dados de formulário adaptáveis para o Armazenamento do Microsoft® Azure como um BLOB.

### Novos recursos disponíveis no canal de pré-lançamento do [!DNL Forms] {#prerelease-features-forms}

* **Usar funções do Adobe Sign em um Formulário adaptável** - O Adobe Sign para níveis de serviço corporativo e empresarial pode, opcionalmente, expandir as funções para os destinatários do Contrato, além apenas do Signatário, para melhor corresponder aos requisitos de fluxo de trabalho. Agora você pode habilitar cada recipient do contrato para configurar sua função em um Formulário adaptável, sendo que Signatário é a função padrão.

* **Analytics para Forms adaptável** - Agora é possível capturar e rastrear o comportamento do usuário final por meio do Adobe Analytics para Forms adaptável para coletar insights do usuário final. Ele ajuda a tomar decisões informadas com base em dados para melhorar a experiência do usuário final.

* **Conecte facilmente o AEM Forms com o Microsoft® Dynamics e Salesforce.com** - O serviço fornece configuração de fonte de dados pronta para uso e modelos de dados para o Microsoft® Dynamics e Salesforce.com. Isso torna mais rápido e fácil para os desenvolvedores configurarem o Microsoft® Dynamics e o Salesforce.com como fontes de dados para um formulário adaptável.

## Complemento CIF {#cloud-services-cif}

### Novidades {#what-is-new-cif}

* Nova interface do Seletor de categorias para melhorar a experiência do usuário, aumentar a eficiência e melhorar o suporte para catálogos de produtos complexos

  ![Novo Seletor de Categoria](/help/assets/CIF/category-picker.png)

* Melhor suporte A11Y para os Componentes principais do CIF

## Cloud Manager {#cloud-manager}

Esta seção descreve as Notas de versão do Cloud Manager no AEM as a Cloud Service 2021.8.0 e 2021.7.0.

## Data de lançamento {#release-date-cm-aug}

A data de lançamento do Cloud Manager no AEM as a Cloud Service 2021.8.0 é 12 de agosto de 2021.
A próxima versão está planejada para 9 de setembro de 2021.

### Novidades {#what-is-new-aug}

* Os clientes do Cloud Service agora podem visualizar os relatórios do Contrato de Nível de Serviço (SLA) no Cloud Manager. Isso será disponibilizado progressivamente nos próximos meses.
Consulte [Relatórios de SLA](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/sla-reporting.html?lang=pt-BR).

* O tipo e a gravidade do IndexType e as regras de qualidade `IndexDamAssetLucene` foram alteradas. Estes são agora Bugs de *severidade* do bloqueador.

* Novas regras de qualidade do índice Oak foram introduzidas para abranger configurações assíncronas e do Tika.

* O número máximo de certificados SSL por programa foi aumentado para 50.

* Capacidade de autoatendimento para permitir que os usuários criem e gerenciem vários repositórios por meio da interface do Cloud Manager.

* O SonarQube estava lendo desnecessariamente dados de histórico do Git. Em bases de código grandes, isso poderia resultar em uma penalidade desnecessária no desempenho de compilação.

* Agora há uma API disponível para invalidar o cache de dependência do Maven por pipeline.

* A versão do Arquétipo de Projetos AEM usada pelo Cloud Manager foi atualizada para a versão 29.

### Correções de erros {#bug-fixes-aug}

* A opção Atualizar status disponível não deve aparecer quando a versão mais recente for anterior à versão atual.

* A integração inicial falhava para novas organizações com nomes longos.

* Ocasionalmente, quando um pipeline é acionado duas vezes por algum motivo, isso resulta na falha de uma das execuções com um erro *`cannot update pipeline execution status`*.

## Ferramenta Transferência de conteúdo {#content-transfer-tool}

### Data de lançamento {#release-date-ctt-latest}

A data de lançamento da ferramenta de Transferência de conteúdo v1.5.6 é 11 de agosto de 2021.

### Correções de erros {#bug-fixes-ctt}

* Às vezes, nem todos os usuários eram migrados para a instância de destino. Para obter essa correção, a CTT v1.5.6 é necessária junto com o aem-ethos-tools 1.2.354 ou versão posterior na instância do AEM as a Cloud Service de destino.

* O botão **Parar assimilação** estava sendo desativado durante a assimilação na instância do Publish. Isso não é necessário porque não há etapa de restauração do Mongo durante a assimilação do Publish.

* A CTT não limpou o diretório `/tmp` após uma extração bem-sucedida. Isso às vezes levava a problemas de espaço em disco.
