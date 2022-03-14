---
title: Notas de versão do  [!DNL Adobe Experience Manager] as a Cloud Service 2021.7.0.
description: Notas de versão do  [!DNL Adobe Experience Manager] as a Cloud Service 2021.7.0.
exl-id: 848f6a29-2e0f-4976-8ed7-6b7f69408c1b
source-git-commit: 96a0dacf69f6f9c5744f224d1a48b2afa11fb09e
workflow-type: tm+mt
source-wordcount: '1315'
ht-degree: 13%

---

# Notas de versão atuais do [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

A seção a seguir descreve as Notas de versão gerais da versão atual (mais recente) do [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>A partir daqui, você pode navegar até as notas de versão das versões anteriores; por exemplo, para aqueles em 2020, 2021 e assim por diante.

>[!NOTE]
>
>Consulte [Atualizações recentes na documentação](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=pt-BR) para obter detalhes de atualizações de documentação não relacionadas diretamente a uma versão.

## Data de lançamento {#release-date}

A data de lançamento do [!DNL Adobe Experience Manager] como [!DNL Cloud Service] a versão atual (2021.7.0) é 29 de julho de 2021.
A seguinte versão (2021.8.0) é em 26 de agosto de 2021.

## Vídeo da versão {#release-video}

Dê uma olhada no [Visão geral da versão de julho de 2021](https://video.tv.adobe.com/v/335580) vídeo para obter um resumo dos recursos adicionados.

## Experience Manager Foundation as a Cloud Service {#foundation}

### Novidades {#what-is-new-foundation}

* Configuração mais flexível do dispatcher: Os projetos podem ser mais facilmente organizados. Por exemplo, agora você pode incluir vários arquivos de regras de regravação que refletem a estrutura do site. [Saiba mais sobre](/help/implementing/dispatcher/disp-overview.md#validation-debug) esse modo flexível, incluindo como estruturar a configuração do dispatcher para aproveitar.
* A interface de usuário de replicação em árvore na guia &quot;Distribuir&quot; do agente de replicação deve ser considerada obsoleta e deve ser removida após 30 de setembro. [Saiba mais sobre](/help/operations/replication.md#tree-activation) estratégias alternativas de replicação.
* Pacote `org.apache.sling.datasource-1.0.4.jar` O para suporte à fonte de dados do Sling foi removido, pois a funcionalidade foi desatualizada e não está sendo usada pelos clientes.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Novos recursos no [!DNL Assets] {#assets-features}

* A funcionalidade de Automação de conteúdo permite [!DNL Experience Manager Assets] utilize o [!DNL Adobe Creative Cloud] APIs para automatizar a produção de ativos em escala. Melhora a velocidade do conteúdo diminuindo drasticamente o tempo gasto e as iterações necessárias para criar variações do mesmo ativo. A funcionalidade não requer programação e funciona no DAM. Consulte [gerar variações de ativos usando a integração Creative Cloud](/help/assets/cc-api-integration.md).

* [!DNL Experience Manager Assets] inclui a [!DNL Document Cloud] Visualizador de PDF para visualizar documentos PDF nativamente. Esse recurso permite que os usuários visualizem arquivos PDF de várias páginas sem qualquer processamento ou conversão de arquivos. Esse recurso melhora a paridade com [!DNL Experience Manager] 6.5. Os controles disponíveis no visualizador incluem zoom, navegar até páginas, cancelar a âncora dos controles e exibir em tela cheia. O caso Usuários também visualiza e salta para páginas e marcadores. Comentários no próprio arquivo são suportados, comentários e anotações sobre o conteúdo no arquivo PDF serão adicionados em uma versão futura.

   ![Visualizar arquivos do PDF em [!DNL Experience Manager] usando o Visualizador de PDF](/help/assets/assets/preview-pdf-file-viewer.png)

* A funcionalidade de download do Linkshare usa downloads assíncronos que aumentam a velocidade de download. Consulte [Baixar ativos compartilhados usando o compartilhamento de link](/help/assets/download-assets-from-aem.md#link-share-download).

   ![Baixar caixa de entrada](/help/assets/assets/download-inbox.png)

* As configurações de exibição são aprimoradas para permitir que os usuários escolham uma exibição padrão e um parâmetro de classificação padrão.

   ![Defina a exibição padrão em [!UICONTROL Exibir configurações]](/help/assets/assets/view-settings-for-defaults.png)

* Os usuários podem pesquisar e filtrar as pastas com base em predicados de propriedade.

   ![Filtrar pastas de pesquisa usando predicados de pesquisa](/help/assets/assets/search-folders-via-predicates.png)

### Novos recursos disponíveis na [!DNL Assets] canal de pré-lançamento {#assets-prerelease-features}

<!-- TBD: Not sure about GA of these enh. Shall check with the team.

* A user experience enhancements displays the number of assets present in a folder. For more than 1000 assets in a folder, [!DNL Assets] displays 1000+.

  ![Number of assets in a folder are displayed on the interface](/help/assets/assets/browse-folder-number-of-assets.png)

* You can directly apply a metadata schemas to a folder in its [!UICONTROL Properties].

  ![Add metadata schema from folder properties](/help/assets/assets/metadata-schema-folder-properties.png)
-->

* Ao compartilhar ativos digitais como um link, os usuários podem copiar o URL para a área de transferência. O aprimoramento permite compartilhar ativos de maneira mais rápida e conveniente.

### Erros corrigidos em [!DNL Assets] {#assets-bugs-fixed}

A API `com.day.cq.dam.api.collection.SmartCollection` não está disponível em [!DNL Experience Manager] como [!DNL Cloud Service]. (CQ-4326322)

## [!DNL Experience Manager Forms] como [!DNL Cloud Service] {#forms}

### Novidades do [!DNL Forms] {#what-is-new-forms}

* Agora você pode usar o serviço Automated forms conversion para [converter PDF forms em francês, alemão e espanhol](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?#language-specific-meta-model) para formulários adaptáveis.
* Adição de um painel separado ao editor de modelo para exibir erros relacionados aos componentes de formulário adaptáveis. Ele ajuda a consolidar todos os erros de formulário adaptável em um local e a reduzir o tempo de resolução.

### Novos recursos disponíveis no canal de pré-lançamento do [!DNL Forms] {#beta-features-forms}

* **[!DNL AEM Forms as a Cloud Service - Communications]**: [APIs de comunicação](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/aem-forms-cloud-service-communications.html?lang=pt-BR) Ajudar a combinar modelos XDP e dados XML para gerar documentos de impressão em vários formatos. O serviço permite gerar documentos no modo síncrono. As APIs permitem criar aplicativos que possibilitam a você:
   * Gerar documentos preenchendo arquivos de modelo com dados XML.
   * Gerar formulários de saída em vários formatos, incluindo fluxos de impressão de PDF não interativos.
   * Gere arquivos PDF de impressão a partir de um PDF de formulário XFA e do Formulário Adobe Acrobat.

* **Externalizador de dados de variáveis**: Você pode salvar dados de variáveis de Fluxo de trabalho AEM em um sistema de armazenamento externo gerenciado por sua organização.

* **Documento de registro baseado em formulário**: Você também pode [usar o Adobe Acrobat Form PDF (Acroform PDF)](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/create-an-adaptive-form/generate-document-of-record-for-non-xfa-based-adaptive-forms.html) como um modelo para o Documento de registro além do modelo de formulário baseado em XFA.

* **Conector do armazenamento de dados do Microsoft Azure**: Agora você pode [conectar o Modelo de Dados de Formulário ao Armazenamento do Microsoft Azure](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/use-form-data-model/configure-azure-storage.html). Ele permite recuperar e armazenar dados de formulário adaptáveis para o Microsoft Azure Storage como um BLOB.

## Complemento CIF {#cloud-services-cif}

### Novidades {#what-is-new-cif}

* Componentes principais da CIF v2
   * Configurações simplificadas e aprimoradas para URL PDP/PLP e SEO
   * Indicador visual para dados de produto preparados no modo de criação para melhor visibilidade das alterações futuras
   * Novo componente de mapa de site para páginas de conteúdo e comércio

* Suporte para [Adobe Commerce Sensei Product Recommendation, com a tecnologia Adobe Sensei](https://business.adobe.com/products/magento/product-recommendations.html) no AEM Storefront usando recomendações predefinidas ou criadas dinamicamente

## [!DNL Experience Manager Screens] como [!DNL Cloud Service] {#screens}

### Correções de erros {#bug-fixes-screens}

* As configurações do Provedor de conteúdo agora são validadas durante a criação ou atualização.

* Todas as exibições têm coluna de pastas.

* É possível expandir a Estrutura de conteúdo do Screens.

* `bulk-offline-update-service` estava faltando todas as permissões para alguns ambientes.

* Atualização do link Ajuda para corresponder à nova documentação da nuvem de telas.

* Cancelar a atribuição de listas de reprodução e não permitir a remoção de listas de reprodução com reprodutor(es) atribuído(s), agora funciona.

* O reprodutor agora faz o download de Ativos novamente quando o Cache &quot;ALL&quot; é limpo.

* A repetição do agendamento agora funciona, se a variável *Hora de Término* é definido para o dia seguinte.

* `Back&Forward` agora funciona na interface do usuário as a Cloud Service do Screens.

* Tags com o mesmo nome, mas namespaces diferentes, não puderam ser criadas anteriormente.

## Documentação XML para Experience Manager as a Cloud Service {#xml-documentation}

### Novidades {#what-is-new-xml-documentation}

A Documentação XML para Experience Manager as a Cloud Service geralmente está disponível. Ele permite que os clientes do Experience Manager as a Cloud Service adquiram a Documentação XML e importem, criem, gerenciem e entreguem conteúdo técnico em vários canais, incluindo o Experience Manager Sites.

## Cloud Manager {#cloud-manager}

Esta seção descreve as Notas de versão do Cloud Manager no AEM as a Cloud Service 2021.7.0.

### Data de lançamento {#release-cm-july}

A data de lançamento do Cloud Manager AEM as a Cloud Service 2021.7.0 é 15 de julho de 2021.
A próxima versão está planejada para 12 de agosto de 2021.

### Novidades {#what-is-new-cm-july}

* Os clientes agora podem usar os JDKs do Azul 8 e 11 para seus processos de build do Cloud Manager e podem optar por usar um desses JDKs para plug-ins Maven compatíveis com cadeias de ferramentas *ou* a execução inteira do processo Maven.

* O IP de saída agora será registrado no arquivo de log da etapa de compilação.

* Ambientes de Preparo e Produção que executam versões antigas de AEM agora relatarão um status de **Atualização disponível**.

* Os certificados SSL máximos suportados aumentaram para 20 por programa.

* O número máximo de domínios que podem ser configurados aumentou para 500 por ambiente.

* O **Gerenciar Git** os botões foram redefinidos para **Acessar informações do Git** e a caixa de diálogo foi atualizada visualmente.

* A versão do AEM Project Archetype usada pelo Cloud Manager foi atualizada para a versão 28.

### Correções de erros {#bug-fixes-cm-july}

* Em algumas situações, a Visualização não era uma opção disponível ao vincular uma Lista de permissões de IP a um ambiente.

* Navegar manualmente para a página de detalhes da execução de uma execução não existente não exibia um erro, apenas uma tela de carregamento infinita.

* A mensagem de erro exibida quando o número máximo de certificados SSL foi atingido não foi útil.

* Em algumas circunstâncias, pode haver uma discrepância na versão de lançamento mostrada na placa de pipeline na variável **Visão geral** página.

* O assistente de adição de programa declarou incorretamente que o nome não pode ser alterado após a criação.

### Problemas conhecidos {#known-issues-cm-july}

Os clientes que alternam para usar os JDKs do Azul devem estar cientes de que nem todos os aplicativos existentes serão compilados sem erro no JDK do Azul. É altamente recomendável testar localmente antes de trocar.

## Cloud Acceleration Manager {#cam}

### Data de lançamento {#release-date-july-cam}

A data de lançamento do Cloud Acceleration Manager é 15 de julho de 2021.

### Novidades {#what-is-new-cam}

O Cloud Acceleration Manager é um aplicativo baseado em nuvem projetado para orientar suas equipes de TI durante toda a jornada de transição, começando pelo planejamento até a ativação do Cloud Service. Configure suas equipes para uma migração bem-sucedida com práticas recomendadas, dicas, documentação e ferramentas do Adobe, recomendadas para ajudar em cada fase da jornada a AEM como Cloud Service. Saiba mais [here](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/getting-started-cam.html?lang=en).

>[!NOTE]
>
> Verifique isso [Vídeo de demonstração do Cloud Acceleration Manager](https://video.tv.adobe.com/v/335547).
