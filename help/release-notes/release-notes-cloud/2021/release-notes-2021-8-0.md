---
title: Notas de versão do  [!DNL Adobe Experience Manager] as a Cloud Service 2021.8.0.
description: Notas de versão do  [!DNL Adobe Experience Manager] as a Cloud Service 2021.8.0.
exl-id: 8b041934-1c4a-4670-9b03-d38f683b99e5
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '1032'
ht-degree: 12%

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

A data de lançamento do [!DNL Adobe Experience Manager] como [!DNL Cloud Service] a versão atual (2021.8.0) é 26 de agosto de 2021.
A seguinte versão (2021.9.0) é em 6 de outubro de 2021.

## Vídeo da versão {#release-video}

Dê uma olhada no [Visão geral da versão de agosto de 2021](https://video.tv.adobe.com/v/336277) vídeo para obter um resumo dos recursos adicionados.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Novos recursos no [!DNL Assets] {#assets-features}

* Ao compartilhar ativos digitais como um link, os usuários podem copiar o URL para a área de transferência imediatamente. O aprimoramento permite compartilhar ativos de maneira mais rápida e conveniente. Essa funcionalidade permite um compartilhamento de ativos mais rápido e prático.

   ![Opção Copiar URL ao compartilhar um ativo como um link](/help/assets/assets/link-share-copy-URL-option.png)
   *Figura: Ao compartilhar um ativo como um link, agora é possível copiar o URL para compartilhá-lo separadamente.*

* Ao fazer upload de arquivos TXT, os microsserviços de ativos geram automaticamente uma miniatura. A miniatura de PNG é uma representação do arquivo TXT que ajuda os usuários a identificar o conteúdo ou os arquivos até certo ponto, sem abrir os arquivos. Essa funcionalidade não requer configuração e funciona por padrão.

   ![Uma representação de um arquivo TXT é gerada automaticamente por [!DNL Assets] em formato PNG](/help/assets/assets/thumbnail-rendition-txt-file.png)
   *Figura: Uma representação de um arquivo TXT é gerada automaticamente para ajudar a identificar o arquivo sem abri-lo.*

### Novo recurso na [!DNL Assets] canal de pré-lançamento {#assets-prerelease-features}

* Os usuários agora podem classificar os ativos exibidos nos resultados da pesquisa nas exibições Coluna e Cartão. A classificação funciona nas colunas Nome, Criado, Modificado ou Nenhum.

   ![Classifique os resultados da pesquisa em [!DNL Assets] nas exibições Coluna e Cartão](/help/assets/assets/sort-searched-assets.png)
   *Figura: Classifique os resultados da pesquisa em [!DNL Assets] nas exibições Coluna e Cartão.*

### Erros corrigidos em [!DNL Assets] {#assets-bugs-fixed}

* Quando um membro do grupo do colaborador navega até a variável [!DNL Assets] Console, um `POST` é gerada para tentar criar uma Coleção. Essa solicitação não é necessária, falha devido a problemas de permissões e cria muitos erros nos logs. (CQ-4328856)
* Quando os usuários visualizam um ativo e selecionam a variável [!UICONTROL Linha do tempo] no menu pop-up do painel esquerdo, um erro é exibido. Nos logs, muitos avisos são registrados devido a uma consulta incorreta. (CQ-4328919)

## [!DNL Experience Manager Forms] como [!DNL Cloud Service] {#forms}

### Novidades do [!DNL Forms] {#what-is-new-forms}

* O serviço Automated forms conversion pode [converter PDF forms em italiano e português](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?#language-specific-meta-model) para Adaptive Forms.

* **Documento de registro baseado em formulário**: O AEM Forms as a Cloud Service oferece suporte ao uso do [Adobe Acrobat Form PDF (Acroform PDF)](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/create-an-adaptive-form/generate-document-of-record-for-non-xfa-based-adaptive-forms.html) como um modelo para o Documento de registro além do modelo de formulário baseado em XFA.

* **Conector do armazenamento de dados do Microsoft Azure**: Agora você pode [conectar o Modelo de Dados de Formulário ao Armazenamento do Microsoft Azure](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/use-form-data-model/configure-azure-storage.html). Ele permite recuperar e armazenar dados de formulário adaptáveis para o Microsoft Azure Storage como um BLOB.

### Novos recursos disponíveis no canal de pré-lançamento do [!DNL Forms] {#prerelease-features-forms}

* **Usar as funções do Adobe Sign em um formulário adaptável**: Os níveis de serviço Adobe Sign for business and enterprise têm a opção de expandir as funções para os recipients do Agreement, além apenas do Signer, para melhor corresponder aos seus requisitos de fluxo de trabalho. Agora você pode habilitar cada recipient do contrato para configurar sua função em um Formulário adaptável, com o Assinante sendo a função padrão.

* **Analytics para Adaptive Forms**: Agora é possível capturar e rastrear o comportamento do usuário final por meio do Adobe Analytics para o Adaptive Forms para coletar insights do usuário final. Ajuda a tomar decisões informadas com base em dados para melhorar a experiência do usuário final.

* **Conecte facilmente o AEM Forms com o Microsoft Dynamics e o Salesforce.com**: O serviço fornece configuração de fonte de dados e modelos de dados prontos para uso para o Microsoft Dynamics e Salesforce.com, tornando mais rápido e fácil para os desenvolvedores configurar o Microsoft Dynamics e o Salesforce.com como fontes de dados para um formulário adaptável.

## Complemento CIF {#cloud-services-cif}

### Novidades {#what-is-new-cif}

* Nova interface do usuário do Seletor de categorias para melhorar a experiência do usuário, aumentar a eficiência e oferecer melhor suporte para catálogos de produtos complexos

   ![Novo seletor de categorias](/help/assets/CIF/category-picker.png)

* Melhor suporte A11Y para os Componentes principais da CIF

## Cloud Manager {#cloud-manager}

Esta seção descreve as Notas de versão do Cloud Manager AEM as a Cloud Service 2021.8.0 e 2021.7.0.

## Data de lançamento {#release-date-cm-aug}

A Data de lançamento do Cloud Manager AEM as a Cloud Service 2021.8.0 é 12 de agosto de 2021.
A próxima versão está planejada para 09 de setembro de 2021.

### Novidades {#what-is-new-aug}

* Os clientes do Cloud Service agora podem visualizar os relatórios do Contrato de nível de serviço (SLA) no Cloud Manager. Esta informação será disponibilizada progressivamente nos próximos meses.
Consulte [Relatórios de SLA](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/sla-reporting.html) para saber mais.

* O tipo e a gravidade do IndexType e `IndexDamAssetLucene` as regras de qualidade foram alteradas. Estes são agora os dois Bugs do Bloqueador *servidão*.

* Novas regras de qualidade do índice Oak foram introduzidas para abranger configurações assíncronas e tika.

* Aumente o número máximo de certificados SSL por programa para 50.

* Capacidade de autoatendimento para permitir que os usuários criem e gerenciem vários repositórios por meio da interface do usuário do Cloud Manager.

* SonarQube estava lendo desnecessariamente os dados do histórico do Git. Em bases de código grandes, isso poderia resultar em uma penalidade desnecessária no desempenho da build.

* Agora há uma API disponível para invalidar o cache de dependência Maven por pipeline.

* A versão do AEM Project Archetype usada pelo Cloud Manager foi atualizada para a versão 29.

### Correções de erros {#bug-fixes-aug}

* O status Atualizar disponível não deve ser exibido quando a versão mais recente for menor que a versão atual.

* A integração inicial estava falhando para novas organizações com nomes muito longos.

* Ocasionalmente, quando um pipeline é acionado duas vezes por algum motivo, resulta em uma das execuções falhar com *não é possível atualizar o status de execução do pipeline* erro.

## Ferramenta Transferência de conteúdo {#content-transfer-tool}

### Data de lançamento {#release-date-ctt-latest}

A Data de lançamento da ferramenta Transferência de conteúdo v1.5.6 é 11 de agosto de 2021.

### Correções de erros {#bug-fixes-ctt}

* Em alguns casos, nem todos os usuários foram migrados para a instância de destino. Para obter essa correção, o CTT v1.5.6 é necessário juntamente com o aem-ethos-tools 1.2.354 ou versão posterior na instância as a Cloud Service do target AEM.

* O **Parar Assimilação** estava sendo desativado durante a assimilação na instância de publicação. Isso não é necessário porque não há uma etapa de restauração de mongo durante a assimilação de Publicação.

* O CTT não limpou o `/tmp` após uma extração bem-sucedida. Isso às vezes levava a problemas de espaço em disco.
