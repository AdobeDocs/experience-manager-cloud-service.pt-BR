---
title: Notas de versão atuais para [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de versão atuais para [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
mini-toc-levels: 1
source-git-commit: 2f08b1487c1a7fc7b94678e78f8fd72054ff51cb
workflow-type: tm+mt
source-wordcount: '1632'
ht-degree: 2%

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

A data de lançamento de [!DNL Adobe Experience Manager] como uma [!DNL Cloud Service] versão atual (2021.7.0) é 29 de julho de 2021.
A seguinte versão (2021.8.0) é em 26 de agosto de 2021.

## Lançamento de vídeo {#release-video}

Assista ao vídeo [Visão geral da versão de julho de 2021](https://video.tv.adobe.com/v/335580) para ver um resumo dos recursos adicionados.

## [!DNL Experience Manager] como  [!DNL Cloud Service] fundação {#foundation}

### Novidades {#what-is-new-foundation}

* Configuração mais flexível do dispatcher: Os projetos podem ser mais facilmente organizados. Por exemplo, agora você pode incluir vários arquivos de regras de regravação que refletem a estrutura do site. [Saiba mais ](/help/implementing/dispatcher/disp-overview.md#validation-debug) sobre esse modo flexível, incluindo como estruturar sua configuração de dispatcher para aproveitar isso.
* A interface de usuário de replicação em árvore na guia &quot;Distribuir&quot; do agente de replicação deve ser considerada obsoleta e deve ser removida após 30 de setembro. [Saiba mais ](/help/operations/replication.md#tree-activation) sobre estratégias de replicação alternativas.
* O pacote `org.apache.sling.datasource-1.0.4.jar` para suporte à fonte de dados do Sling foi removido, pois tem funcionalidade desatualizada e não está em uso pelos clientes.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Novos recursos em [!DNL Assets] {#assets-features}

* A funcionalidade de Automação de conteúdo permite que [!DNL Experience Manager Assets] aproveite as APIs [!DNL Adobe Creative Cloud] para automatizar a produção de ativos em escala. Melhora a velocidade do conteúdo diminuindo drasticamente o tempo gasto e as iterações necessárias para criar variações do mesmo ativo. A funcionalidade não requer programação e funciona no DAM. Consulte [gerar variações de ativos usando a integração do Creative Cloud](/help/assets/cc-api-integration.md).

* [!DNL Experience Manager Assets] O inclui o Visualizador de  [!DNL Document Cloud] PDF para visualizar documentos PDF nativamente. Esse recurso permite que os usuários visualizem arquivos PDF de várias páginas sem qualquer processamento ou conversão de arquivos. Este recurso melhora a paridade com [!DNL Experience Manager] 6.5. Os controles disponíveis no visualizador incluem zoom, navegar até páginas, desancorar controles e exibir em tela cheia. O caso Usuários também visualiza e salta para páginas e marcadores. Comentários no próprio arquivo são suportados, comentários e anotações sobre o conteúdo no arquivo PDF serão adicionados em uma versão futura.

   ![Visualizar arquivos PDF no  [!DNL Experience Manager] uso do Visualizador de PDF](/help/assets/assets/preview-pdf-file-viewer.png)

* A funcionalidade de download do Linkshare usa downloads assíncronos que aumentam a velocidade de download. Consulte [Baixar ativos compartilhados usando o compartilhamento de link](/help/assets/download-assets-from-aem.md#link-share-download).

   ![Baixar caixa de entrada](/help/assets/assets/download-inbox.png)

* As configurações de exibição são aprimoradas para permitir que os usuários escolham uma exibição padrão e um parâmetro de classificação padrão.

   ![Definir exibição padrão em Configurações  [!UICONTROL de exibição]](/help/assets/assets/view-settings-for-defaults.png)

* Os usuários podem pesquisar e filtrar as pastas com base em predicados de propriedade.

   ![Filtrar pastas de pesquisa usando predicados de pesquisa](/help/assets/assets/search-folders-via-predicates.png)

### Novos recursos disponíveis no canal de pré-lançamento [!DNL Assets] {#assets-prerelease-features}

<!-- TBD: Not sure about GA of these enh. Shall check with the team.

* A user experience enhancements displays the number of assets present in a folder. For more than 1000 assets in a folder, [!DNL Assets] displays 1000+.

  ![Number of assets in a folder are displayed on the interface](/help/assets/assets/browse-folder-number-of-assets.png)

* You can directly apply a metadata schemas to a folder in its [!UICONTROL Properties].

  ![Add metadata schema from folder properties](/help/assets/assets/metadata-schema-folder-properties.png)
-->

* Ao compartilhar ativos digitais como um link, os usuários podem copiar o URL para a área de transferência. O aprimoramento permite compartilhar ativos de maneira mais rápida e conveniente.

### Erros corrigidos em [!DNL Assets] {#assets-bugs-fixed}

A API `com.day.cq.dam.api.collection.SmartCollection` não está disponível em [!DNL Experience Manager] como [!DNL Cloud Service]. (CQ-4326322)

## [!DNL Experience Manager Forms] como  [!DNL Cloud Service] {#forms}

### Novidades em [!DNL Forms] {#what-is-new-forms}

* Agora você pode usar o serviço Automated forms conversion para [converter PDF forms em francês, alemão e espanhol](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?#language-specific-meta-model) para formulários adaptáveis.
* Adição de um painel separado ao editor de modelo para exibir erros relacionados aos componentes de formulário adaptáveis. Ele ajuda a consolidar todos os erros de formulário adaptável em um local e a reduzir o tempo de resolução.

### Novos recursos disponíveis no canal de pré-lançamento [!DNL Forms] {#beta-features-forms}

* **[!DNL AEM Forms as a Cloud Service - Communications]**:  [A ](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/aem-forms-cloud-service-communications.html) APIshelp de comunicação permite combinar modelos XDP e dados XML para gerar documentos de impressão em vários formatos. O serviço permite gerar documentos no modo síncrono. As APIs permitem criar aplicativos que permitem:
   * Gere documentos preenchendo arquivos de modelo com dados XML.
   * Gere formulários de saída em vários formatos, incluindo fluxos de impressão PDF não interativos.
   * Gere arquivos PDF de impressão a partir de um formulário XFA PDF e Formulário Adobe Acrobat.

* **Externalizador** de dados de variável: Você pode salvar dados de variáveis de Fluxo de trabalho AEM em um sistema de armazenamento externo gerenciado por sua organização.

* **Documento de registro** baseado em formulário: Também é possível  [usar o PDF do formulário Adobe Acrobat (Acroform PDF)](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/create-an-adaptive-form/generate-document-of-record-for-non-xfa-based-adaptive-forms.html) como um modelo de Documento de registro além do modelo de formulário baseado em XFA.

* **Conector** do repositório de dados do Microsoft Azure: Agora você pode  [conectar o Modelo de Dados de Formulário ao Armazenamento do Microsoft Azure](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/use-form-data-model/configure-azure-storage.html). Ele permite recuperar e armazenar dados de formulário adaptáveis para o Armazenamento do Microsoft Azure como um BLOB.

## Complemento CIF {#cloud-services-cif}

### Novidades {#what-is-new-cif}

* Componentes principais da CIF v2
   * Configurações simplificadas e aprimoradas para URL PDP/PLP e SEO
   * Indicador visual para dados de produto preparados no modo de criação para melhor visibilidade das alterações futuras
   * Novo componente de mapa de site para páginas de conteúdo e comércio

* Suporte para [Recomendação de produto do Adobe Commerce Sensei, viabilizado pelo Adobe Sensei](https://business.adobe.com/products/magento/product-recommendations.html) em AEM Storefront usando recomendações predefinidas ou criadas de forma instantânea

## [!DNL Experience Manager Screens] como  [!DNL Cloud Service] {#screens}

### Correções de erros {#bug-fixes-screens}

* As configurações do Provedor de conteúdo agora são validadas durante a criação ou atualização.

* Todas as exibições têm coluna de pastas.

* É possível expandir a Estrutura de conteúdo do Screens.

* `bulk-offline-update-service` estava faltando todas as permissões para alguns ambientes.

* Atualização do link Ajuda para corresponder à nova documentação da nuvem de telas.

* Cancelar a atribuição de listas de reprodução e não permitir a remoção de listas de reprodução com reprodutor(es) atribuído(s), agora funciona.

* O reprodutor agora faz o download de Ativos novamente quando o Cache &quot;ALL&quot; é limpo.

* Repetir o Agendamento agora funciona, se a *Hora Final* estiver definida para o dia seguinte.

* `Back&Forward` O agora funciona no Screens as a Cloud Service UI.

* Tags com o mesmo nome, mas namespaces diferentes, não puderam ser criadas anteriormente.

## Documentação XML do Experience Manager as a Cloud Service {#xml-documentation}

### Novidades {#what-is-new-xml-documentation}

A Documentação XML do Experience Manager as a Cloud Service está disponível. Ele permite que os clientes do Experience Manager como Cloud Service adquiram a Documentação XML e importem, criem, gerenciem e entreguem conteúdo técnico em vários canais, incluindo o Experience Manager Sites.

## Cloud Manager {#cloud-manager}

Esta seção descreve as Notas de versão do Cloud Manager no AEM as a Cloud Service 2021.8.0 e 2021.7.0.

## Data de lançamento {#release-date-cm-aug}

A Data de lançamento do Cloud Manager no AEM as a Cloud Service 2021.8.0 é 12 de agosto de 2021.
A próxima versão está planejada para 09 de setembro de 2021.

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

### Data de lançamento {#release-cm-july}

A data de lançamento do Cloud Manager no AEM as a Cloud Service 2021.7.0 é 15 de julho de 2021.
A próxima versão está planejada para 12 de agosto de 2021.

### Novidades {#what-is-new-cm-july}

* Os clientes agora podem usar os JDKs do Azul 8 e 11 para seus processos de build do Cloud Manager e podem optar por usar um desses JDKs para plug-ins Maven compatíveis com cadeias de ferramentas *ou* em toda a execução do processo Maven.

* O IP de saída agora será registrado no arquivo de log da etapa de compilação.

* Ambientes de Preparo e Produção que executam versões antigas de AEM agora relatarão um status de **Atualizar Disponível**.

* Os certificados SSL máximos suportados aumentaram para 20 por programa.

* O número máximo de domínios que podem ser configurados aumentou para 500 por ambiente.

* Os botões **Gerenciar Git** foram renomeados para **Acessar informações do Git** e a caixa de diálogo foi atualizada visualmente.

* A versão do AEM Project Archetype usada pelo Cloud Manager foi atualizada para a versão 28.

### Correções de erros {#bug-fixes-cm-july}

* Em algumas situações, a Visualização não era uma opção disponível ao vincular uma Lista de permissões de IP a um ambiente.

* Navegar manualmente para a página de detalhes da execução de uma execução não existente não exibia um erro, apenas uma tela de carregamento infinita.

* A mensagem de erro exibida quando o número máximo de certificados SSL foi atingido não foi útil.

* Em algumas circunstâncias, pode haver uma discrepância na versão de lançamento mostrada na placa de pipeline na página **Visão geral**.

* O assistente de adição de programa declarou incorretamente que o nome não pode ser alterado após a criação.

### Problemas conhecidos {#known-issues-cm-july}

Os clientes que alternam para usar os JDKs do Azul devem estar cientes de que nem todos os aplicativos existentes serão compilados sem erro no JDK do Azul. É altamente recomendável testar localmente antes de trocar.

## Ferramenta Transferência de conteúdo {#content-transfer-tool}

### Data de lançamento {#release-date-ctt-latest}

A Data de lançamento da ferramenta Transferência de conteúdo v1.5.6 é 11 de agosto de 2021.

### Correções de erros {#bug-fixes-ctt}

* Em alguns casos, nem todos os usuários foram migrados para a instância de destino. Para obter essa correção, o CTT v1.5.6 é necessário juntamente com o aem-ethos-tools 1.2.354 ou versão posterior no target AEM como uma instância do Cloud Service.

* O botão **Parar assimilação** estava sendo desativado durante a assimilação na instância de publicação. Isso não é necessário porque não há uma etapa de restauração de mongo durante a assimilação de Publicação.

* A CTT não limpou o diretório `/tmp` após uma extração bem-sucedida. Isso às vezes levava a problemas de espaço em disco.


## Cloud Acceleration Manager {#cam}

### Data de lançamento {#release-date-july-cam}

A data de lançamento do Cloud Acceleration Manager é 15 de julho de 2021.

### Novidades {#what-is-new-cam}

O Cloud Acceleration Manager é um aplicativo baseado em nuvem projetado para orientar suas equipes de TI durante toda a jornada de transição, começando pelo planejamento até a ativação do Cloud Service. Configure suas equipes para uma migração bem-sucedida com práticas recomendadas, dicas, documentação e ferramentas do Adobe, recomendadas para ajudar em cada fase da jornada a AEM como Cloud Service. Saiba mais [aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/getting-started-cam.html?lang=en).

>[!NOTE]
>
> Verifique este [vídeo de demonstração do Cloud Acceleration Manager](https://video.tv.adobe.com/v/335547).
