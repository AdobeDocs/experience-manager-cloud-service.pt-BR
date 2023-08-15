---
title: Notas de versão do [!DNL Adobe Experience Manager] as a Cloud Service 2021.8.0.
description: Notas de versão do [!DNL Adobe Experience Manager] as a Cloud Service 2021.8.0.
exl-id: 8b041934-1c4a-4670-9b03-d38f683b99e5
source-git-commit: 5ad33f0173afd68d8868b088ff5e20fc9f58ad5a
workflow-type: tm+mt
source-wordcount: '1027'
ht-degree: 34%

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

A data de lançamento da versão atual do [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] (2021.8.0) é 26 de agosto de 2021.
A data de lançamento da versão seguinte (2021.9.0) é 6 de outubro de 2021.

## Vídeo da versão {#release-video}

Dê uma olhada no [Visão geral da versão de agosto de 2021](https://video.tv.adobe.com/v/336277) vídeo para obter um resumo dos recursos adicionados.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Novos recursos no [!DNL Assets] {#assets-features}

* Ao compartilhar ativos digitais como um link, os usuários podem copiar o URL para a área de transferência imediatamente. O aprimoramento permite compartilhar ativos de maneira mais rápida e prática. Essa funcionalidade permite um compartilhamento de ativos mais rápido e prático.

  ![Opção Copiar URL ao compartilhar um ativo como um link](/help/assets/assets/link-share-copy-URL-option.png)
  *Figura: ao compartilhar um ativo como um link, agora é possível copiar o URL para compartilhá-lo separadamente.*

* Ao fazer upload de arquivos TXT, os microsserviços de ativos geram automaticamente uma miniatura. A miniatura de PNG é uma representação do arquivo TXT que ajuda os usuários a identificar o conteúdo ou os arquivos até certo ponto, sem abrir os arquivos. Essa funcionalidade não requer configuração e funciona por padrão.

  ![Uma representação de um arquivo TXT é gerada automaticamente pelo [!DNL Assets] em formato PNG](/help/assets/assets/thumbnail-rendition-txt-file.png)
  *Figura: uma representação de um arquivo TXT é gerada automaticamente para ajudá-lo a identificar o arquivo sem abri-lo.*

### Novo recurso na [!DNL Assets] canal de pré-lançamento {#assets-prerelease-features}

* Agora os usuários podem classificar os ativos exibidos nos resultados da pesquisa nas visualizações de Coluna e Cartão. A classificação funciona nas colunas Nome, Criado, Modificado ou Nenhum.

  ![Classificar os resultados da pesquisa em [!DNL Assets] nas Visualizações de coluna e cartão](/help/assets/assets/sort-searched-assets.png)
  *Figura: Classificar os resultados da pesquisa em [!DNL Assets] nas Visualizações de coluna e cartão.*

### Bugs corrigidos em [!DNL Assets] {#assets-bugs-fixed}

* Quando um membro do grupo de colaboradores navega até a [!DNL Assets] Console, um extra `POST` é gerada para criar uma coleção. Essa solicitação não é necessária; ela falha devido a problemas de permissão e cria muitos erros nos logs. (CQ-4328856)
* Quando os usuários visualizam um ativo e selecionam o [!UICONTROL Linha do tempo] no menu pop-up do painel esquerdo, um erro é exibido. Nos logs, muitos avisos são registrados devido a uma consulta inválida. (CQ-4328919)

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Novidades do [!DNL Forms] {#what-is-new-forms}

* O serviço do Automated forms conversion pode [converter PDF forms em italiano e português](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?#language-specific-meta-model) para o Forms adaptável.

* **Documento de registro baseado em acroforma**: o AEM Forms as a Cloud Service suporta o uso de [PDF do Adobe Acrobat Form (Acroform PDF)](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/create-an-adaptive-form/generate-document-of-record-for-non-xfa-based-adaptive-forms.html) como um modelo para o Documento de registro além do modelo de formulário baseado em XFA.

* **Conector do armazenamento de dados do Microsoft Azure**: Agora você pode [conectar o Modelo de dados do formulário ao Armazenamento do Microsoft Azure](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/use-form-data-model/configure-azure-storage.html). Ele permite recuperar e armazenar dados de formulário adaptáveis para o Armazenamento do Microsoft Azure como um BLOB.

### Novos recursos disponíveis no canal de pré-lançamento do [!DNL Forms] {#prerelease-features-forms}

* **Usar funções do Adobe Sign em um formulário adaptável**: a Adobe Sign para níveis de serviço corporativo e comercial tem a opção de expandir as funções para os recipients do Contrato, além apenas do Signatário, para melhor corresponder aos requisitos de fluxo de trabalho. Agora você pode habilitar cada recipient do contrato para configurar sua função em um Formulário adaptável, sendo que Signatário é a função padrão.

* **Analytics para Forms adaptável**: agora você pode capturar e rastrear o comportamento do usuário final por meio do Adobe Analytics para Adaptive Forms para coletar insights do usuário final. Ele ajuda a tomar decisões informadas com base em dados para melhorar a experiência do usuário final.

* **Conecte facilmente o AEM Forms ao Microsoft Dynamics e Salesforce.com**: o serviço fornece configuração de fonte de dados pronta para uso e modelos de dados para o Microsoft Dynamics e o Salesforce.com, tornando mais rápido e fácil para os desenvolvedores configurarem o Microsoft Dynamics e o Salesforce.com como fontes de dados para um formulário adaptável.

## Complemento CIF {#cloud-services-cif}

### Novidades {#what-is-new-cif}

* Nova interface do seletor de categorias para melhorar a experiência do usuário, aumentar a eficiência e melhorar o suporte para catálogos de produtos complexos

  ![Novo Seletor de Categoria](/help/assets/CIF/category-picker.png)

* Melhor suporte A11Y para os Componentes principais da CIF

## Cloud Manager {#cloud-manager}

Esta seção descreve as notas de versão do Cloud Manager no AEM as a Cloud Service 2021.8.0 e 2021.7.0.

## Data de lançamento {#release-date-cm-aug}

A data de lançamento do Cloud Manager no AEM as a Cloud Service 2021.8.0 é 12 de agosto de 2021.
A próxima versão está planejada para 9 de setembro de 2021.

### Novidades {#what-is-new-aug}

* Os clientes do Cloud Service agora podem visualizar os relatórios do Contrato de Nível de Serviço (SLA) no Cloud Manager. Essa informação será disponibilizada progressivamente nos próximos meses.
Consulte [Relatórios de SLA](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/sla-reporting.html?lang=pt-BR) para saber mais.

* O tipo e a gravidade do IndexType e as regras de qualidade `IndexDamAssetLucene` foram alteradas. Estes passaram a ser erros com *servidão* limitante.

* Novas regras de qualidade do índice Oak foram introduzidas para abranger configurações assíncronas e tika.

* O número máximo de certificados SSL por programa foi aumentado para 50.

* Capacidade de autoatendimento para permitir que os usuários criem e gerenciem vários repositórios por meio da interface do usuário do Cloud Manager.

* O SonarQube estava lendo desnecessariamente dados de histórico do Git. Em bases de código grandes, isso poderia resultar em uma penalidade desnecessária no desempenho de compilação.

* Agora há uma API disponível para invalidar o cache de dependência do Maven por pipeline.

* A versão do Arquétipo de Projetos AEM usada pelo Cloud Manager foi atualizada para a versão 29.

### Correções de erros {#bug-fixes-aug}

* A opção Atualizar status disponível não deve ser exibida quando a versão mais recente for inferior à versão atual.

* A integração inicial não estava funcionando para novas organizações com nomes muito longos.

* Ocasionalmente, quando um pipeline é acionado duas vezes por algum motivo, isso resulta na falha de uma das execuções com o erro *não é possível atualizar o status de execução do pipeline*.

## Ferramenta Transferência de conteúdo {#content-transfer-tool}

### Data de lançamento {#release-date-ctt-latest}

A data de lançamento da ferramenta de Transferência de conteúdo v1.5.6 é 11 de agosto de 2021.

### Correções de erros {#bug-fixes-ctt}

* Em alguns casos, nem todos os usuários foram migrados para a instância de destino. Para obter essa correção, a CTT v1.5.6 é necessária junto com o aem-ethos-tools 1.2.354 ou versão posterior na instância AEM as a Cloud Service de destino.

* A variável **Interromper assimilação** O botão estava sendo desativado durante a assimilação na instância de publicação. Isso não é necessário porque não há etapa de restauração do Mongo durante a assimilação de publicação.

* A CTT não limpou o `/tmp` diretório após uma extração bem-sucedida. Isso às vezes levava a problemas de espaço em disco.
