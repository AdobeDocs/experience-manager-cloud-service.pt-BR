---
title: Notas de versão atuais para [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de versão atuais para [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
mini-toc-levels: 1
source-git-commit: e06a8d28eef4faaa23603adc846033ab5ef55000
workflow-type: tm+mt
source-wordcount: '1630'
ht-degree: 3%

---


# Notas de versão atuais para [!DNL Adobe Experience Manager] como um Cloud Service {#release-notes}

A seção a seguir descreve as Notas de versão gerais para a versão atual (mais recente) de [!DNL Experience Manager] como um Cloud Service.

>[!NOTE]
>
>A partir daqui, você pode navegar até as notas de versão das versões anteriores; por exemplo, para aqueles em 2020, 2021 e assim por diante.

>[!NOTE]
>
>Consulte [Atualizações recentes na documentação](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html) para obter detalhes das atualizações de documentação não diretamente relacionadas a uma versão.

## Data de lançamento {#release-date}

A data de lançamento de [!DNL Adobe Experience Manager] como uma [!DNL Cloud Service] versão atual (2021.8.0) é 26 de agosto de 2021.
A seguinte versão (2021.9.0) é em 30 de setembro de 2021.

## Lançamento de vídeo {#release-video}

Assista ao vídeo [Visão geral da versão de agosto de 2021](https://video.tv.adobe.com/v/336277) para obter um resumo dos recursos adicionados.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Novos recursos em [!DNL Assets] {#assets-features}

* Ao compartilhar ativos digitais como um link, os usuários podem copiar o URL para a área de transferência imediatamente. O aprimoramento permite compartilhar ativos de maneira mais rápida e conveniente. Essa funcionalidade permite um compartilhamento de ativos mais rápido e prático.

   ![Opção Copiar URL ao compartilhar um ativo como um link](/help/assets/assets/link-share-copy-URL-option.png)
   *Figura: Ao compartilhar um ativo como um link, agora é possível copiar o URL para compartilhá-lo separadamente.*

* Ao fazer upload de arquivos TXT, os microsserviços de ativos geram automaticamente uma miniatura. A miniatura de PNG é uma representação do arquivo TXT que ajuda os usuários a identificar o conteúdo ou os arquivos até certo ponto, sem abrir os arquivos. Essa funcionalidade não requer configuração e funciona por padrão.

   ![Uma representação de um arquivo TXT é gerada automaticamente por  [!DNL Assets] em um formato PNG](/help/assets/assets/thumbnail-rendition-txt-file.png)
   *Figura: Uma representação de um arquivo TXT é gerada automaticamente para ajudar a identificar o arquivo sem abri-lo.*

### Novo recurso no canal de pré-lançamento [!DNL Assets] {#assets-prerelease-features}

* Os usuários agora podem classificar os ativos exibidos nos resultados da pesquisa nas exibições Coluna e Cartão. A classificação funciona nas colunas Nome, Criado, Modificado ou Nenhum.

   ![Classifique os resultados da pesquisa  [!DNL Assets] nas exibições Coluna e Cartão](/help/assets/assets/sort-searched-assets.png)
   *Figura: Classifique os resultados da pesquisa  [!DNL Assets] nas exibições Coluna e Cartão.*

### Erros corrigidos em [!DNL Assets] {#assets-bugs-fixed}

* Quando um membro do grupo do colaborador navega até o [!DNL Assets] Console, uma solicitação `POST` extra é gerada para tentar criar uma Coleção. Essa solicitação não é necessária, falha devido a problemas de permissões e cria muitos erros nos logs. (CQ-4328856)
* Quando os usuários visualizam um ativo e selecionam a [!UICONTROL Linha do tempo] no menu pop-up no painel esquerdo, um erro é exibido. Nos logs, muitos avisos são registrados devido a uma consulta incorreta. (CQ-4328919)

## [!DNL Experience Manager Forms] como  [!DNL Cloud Service] {#forms}

### Novidades em [!DNL Forms] {#what-is-new-forms}

<!-- * Automated Forms Conversion service can [convert PDF Forms in Italian and Portuguese language](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?#language-specific-meta-model) to Adaptive Forms. -->

* AEM projeto do Archetype para Forms as a Cloud Service agora inclui [modelos de dados de formulário para Microsoft Dynamics e Salesforce.com](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/setup-environment/setup-local-development-environment.html?#forms-cloud-service-local-development-environment).

* **Documento de registro** baseado em formulário: O AEM Forms as a Cloud Service suporta o uso do PDF de formulário  [Adobe Acrobat (Acroform PDF)](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/create-an-adaptive-form/generate-document-of-record-for-non-xfa-based-adaptive-forms.html) como um modelo para Documento de registro além do modelo de formulário baseado em XFA.

* **Conector** do repositório de dados do Microsoft Azure: Agora você pode  [conectar o Modelo de Dados de Formulário ao Armazenamento do Microsoft Azure](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/use-form-data-model/configure-azure-storage.html). Ele permite recuperar e armazenar dados de formulário adaptáveis para o Armazenamento do Microsoft Azure como um BLOB.

### Recurso beta de [!DNL Forms] {#aug-what-is-new-forms-prerelease}

* **Conector de armazenamento unificado:** use o Conector de armazenamento unificado para externalizar dados em processo em repositórios gerenciados pelo cliente. Por exemplo, você pode
   * Habilite a funcionalidade de salvar e retomar do Forms Portal e armazene rascunhos de formulários adaptáveis em um repositório de dados gerenciado pelo cliente.
   * Armazene dados de fluxos de trabalho em andamento AEM (dados AEM variáveis de fluxo de trabalho) que contêm dados confidenciais pessoais (SPD) em um repositório gerenciado pelo cliente.

* **[!DNL AEM Forms as a Cloud Service - Communications]**:  [A ](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/aem-forms-cloud-service-communications.html) APIshelp de comunicação permite combinar modelos XDP e dados XML para gerar documentos de impressão em vários formatos. O serviço permite gerar documentos no modo síncrono. As APIs permitem criar aplicativos que permitem:
   * Gere documentos preenchendo arquivos de modelo com dados XML.
   * Gere formulários de saída em vários formatos, incluindo fluxos de impressão PDF não interativos.
   * Gere arquivos PDF de impressão a partir de um formulário XFA PDF e Formulário Adobe Acrobat.

Você pode gravar em [!DNL formscsbeta@adobe.com] para se inscrever no programa beta.

### Novos recursos disponíveis no canal de pré-lançamento [!DNL Forms] {#prerelease-features-forms}

* **Usar as funções do Adobe Sign em um formulário** adaptável: Os níveis de serviço Adobe Sign for business and enterprise têm a opção de expandir as funções para os recipients do Agreement, além apenas do Signer, para melhor corresponder aos seus requisitos de fluxo de trabalho. Agora você pode [habilitar cada recipient de contrato para configurar sua função em um Formulário adaptável](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/create-an-adaptive-form/use-adobe-sign/working-with-adobe-sign.html?#addsignerstoanadaptiveform), com o Assinante sendo a função padrão.

* **Analytics para Adaptive Forms**: Agora é possível capturar e rastrear o comportamento do usuário final por meio do Adobe Analytics para o Adaptive Forms para coletar insights do usuário final. Ajuda a tomar decisões informadas com base em dados para melhorar a experiência do usuário final.

* **Conecte facilmente o AEM Forms com o Microsoft Dynamics e o Salesforce.com**: O serviço fornece configuração de fonte de dados e modelos de dados prontos para uso para o Microsoft Dynamics e Salesforce.com, tornando  [mais rápido e fácil para os desenvolvedores configurar o Microsoft Dynamics e o Salesforce.com como fontes de dados para um formulário](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/use-form-data-model/configure-msdynamics-salesforce.html) adaptável.

## [!DNL Experience Manager Screens] como  [!DNL Cloud Service] {#screens}

### Novidades {#what-is-new-screens}

* O Screens as a Cloud Service agora oferece suporte ao monitoramento básico de reprodução. O reprodutor reportará várias métricas de reprodução a cada ping (o padrão é 30 segundos). Com base nas métricas, ele fornece a capacidade de detectar vários casos de borda (experiência travada, tela em branco, problema de agendamento, etc.). Esse recurso permite que a equipe monitore remotamente se um player estiver reproduzindo conteúdo corretamente, melhora a reatividade em telas em branco ou falha de experiências no campo e diminui o risco de mostrar uma experiência quebrada para o usuário final.
Consulte [Monitoramento básico da reprodução](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/manage-player-registration/installing-screens-cloud-player.html?lang=en#playback-monitoring) para obter mais detalhes.

* Agora, o suporte em miniatura para vídeos do agora é compatível com o Screens as a Cloud Service. Um autor de conteúdo pode definir uma miniatura de vídeos para que a imagem possa ser usada como um espaço reservado e testar corretamente a reprodução e o direcionamento do conteúdo, enquanto o vídeo real está sendo finalizado pela equipe apropriada. A imagem também pode ser usada caso a reprodução do vídeo falhe.
Consulte [Suporte de miniaturas para vídeos](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/core-product-features/thumbnail-support-videos.html?lang=en) para obter mais detalhes.

### Correções de erros {#bug-fixes-screens}

* O reprodutor não pôde mostrar o conteúdo da página Incorporada e esse problema foi corrigido.

* Após um logon bem-sucedido, a navegação para a página padrão (canais) terminou em uma página de Erro interno do servidor.

* As entradas de tag associadas não foram removidas ao remover listas de reprodução.


## Complemento CIF {#cloud-services-cif}

### Novidades {#what-is-new-cif}

* Nova interface do usuário do Seletor de categorias para melhorar a experiência do usuário, aumentar a eficiência e oferecer melhor suporte para catálogos de produtos complexos

   ![Novo seletor de categorias](/help/assets/CIF/category-picker.png)

* Melhor suporte A11Y para os Componentes principais da CIF

## Cloud Manager {#cloud-manager}

Esta seção descreve as Notas de versão do Cloud Manager no AEM as a Cloud Service 2021.9.0 e 2021.8.0.

## Data de lançamento {#release-date-cm-sept}

A Data de lançamento do Cloud Manager no AEM as a Cloud Service 2021.9.0 é 9 de setembro de 2021.
A próxima versão está planejada para 07 de outubro de 2021.

### Novidades {#what-is-new-cm-sept}

* A versão do AEM Project Archetype usada pelo Cloud Manager foi atualizada para a versão 30.

* Os cartões de programa na página de aterrissagem do Cloud Manager e a experiência associada foram atualizados.

* O Log de Etapa de Qualidade do Código agora inclui informações de log detalhadas no processo de varredura do OakPal.

* As opções de menu da página Atividade agora incluirão uma opção para **Baixar log** para execuções concluídas do Gerador de código. Ao selecionar essa opção, o log da etapa de build será baixado.

* Clicar diretamente no cartão do Programa agora navegará até a página Visão geral do Cloud Manager .


### Correções de erros {#bug-fixes-sept}

* O usuário verá uma mensagem mais compreensível ao tentar adicionar uma nova Lista de permissões IP em um programa que atingiu o número máximo permitido de Listas de permissões IP que podem ser configuradas.

* URL incorreto foi copiado ao selecionar a opção de menu copiar URL na tela Repositórios.

## Data de lançamento {#release-date-cm-aug}

A Data de lançamento do Cloud Manager no AEM as a Cloud Service 2021.8.0 é 12 de agosto de 2021.

### Novidades {#what-is-new-aug}

* Os clientes do Cloud Service agora podem visualizar os relatórios do Contrato de nível de serviço (SLA) no Cloud Manager. Esta informação será disponibilizada progressivamente nos próximos meses.
Consulte [Relatórios do SLA](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/sla-reporting.html) para saber mais.

* O tipo e a gravidade das regras de qualidade IndexType e `IndexDamAssetLucene` foram alterados. Agora, ambos são Bugs do Blocker *serverity*.

* Novas regras de qualidade do índice Oak foram introduzidas para abranger configurações assíncronas e tika.

* Aumente o número máximo de certificados SSL por programa para 50.

* Capacidade de autoatendimento para permitir que os usuários criem e gerenciem vários repositórios por meio da interface do usuário do Cloud Manager.

* SonarQube estava lendo desnecessariamente os dados do histórico do Git. Em bases de código grandes, isso poderia resultar em uma penalidade desnecessária no desempenho da build.

* Agora há uma API disponível para invalidar o cache de dependência Maven por pipeline.

* A versão do AEM Project Archetype usada pelo Cloud Manager foi atualizada para a versão 29.

### Correções de erros {#bug-fixes-aug}

* O status Atualizar disponível não deve ser exibido quando a versão mais recente for menor que a versão atual.

* A integração inicial estava falhando para novas organizações com nomes muito longos.

* Ocasionalmente, quando um pipeline é acionado duas vezes por algum motivo, resulta em uma das execuções falhando com o erro *cannot update pipeline execution status* .

## Ferramenta Transferência de conteúdo {#content-transfer-tool}

### Data de lançamento {#release-date-ctt-latest}

A Data de lançamento da ferramenta Transferência de conteúdo v1.5.6 é 11 de agosto de 2021.

### Correções de erros {#bug-fixes-ctt}

* Em alguns casos, nem todos os usuários foram migrados para a instância de destino. Para obter essa correção, o CTT v1.5.6 é necessário juntamente com o aem-ethos-tools 1.2.354 ou versão posterior no target AEM como uma instância do Cloud Service.

* O botão **Parar assimilação** estava sendo desativado durante a assimilação na instância de publicação. Isso não é necessário porque não há uma etapa de restauração de mongo durante a assimilação de Publicação.

* A CTT não limpou o diretório `/tmp` após uma extração bem-sucedida. Isso às vezes levava a problemas de espaço em disco.

## Analisador de práticas recomendadas {#best-practices-analyzer}

### Data de lançamento {#release-date-bpa-latest}

A data de lançamento do Analisador de práticas recomendadas v2.1.18 é 2 de setembro de 2021.

### Novidades {#what-is-new}

* Capacidade de detectar e relatar a contagem total de nós.

* Capacidade de detectar e relatar no tipo e tamanho do armazenamento do nó.

### Correções de erros {#bug-fixes-bpa}

* O BPA detectou falsamente a presença da Commerce Integration Framework.

