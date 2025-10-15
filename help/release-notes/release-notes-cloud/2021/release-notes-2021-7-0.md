---
title: Notas de versão do  [!DNL Adobe Experience Manager]  as a Cloud Service 2021.7.0.
description: Notas de versão do  [!DNL Adobe Experience Manager]  as a Cloud Service 2021.7.0.
exl-id: 848f6a29-2e0f-4976-8ed7-6b7f69408c1b
feature: Release Information
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '1292'
ht-degree: 22%

---

# Notas de versão atuais do [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

A seção a seguir descreve as Notas de versão gerais da versão atual (mais recente) do [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Aqui, você pode navegar até as notas de versão das versões anteriores; por exemplo, para aquelas em 2020 e 2021.

>[!NOTE]
>
>Consulte [Atualizações recentes na documentação](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=pt-BR) para obter detalhes de atualizações de documentação não relacionadas diretamente a uma versão.

## Data de lançamento {#release-date}

A data de lançamento da versão atual (2021.7.0) do [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] é sexta-feira, 29 de julho de 2021.
A versão seguinte (2021.8.0) será lançada em sexta-feira, 26 de agosto de 2021.

## Vídeo da versão {#release-video}

Assista ao vídeo [Visão geral da versão de julho de 2021](https://video.tv.adobe.com/v/335580) para ver um resumo dos recursos adicionados.

## Experience Manager Foundation as a Cloud Service {#foundation}

### Novidades {#what-is-new-foundation}

* Configuração mais flexível do Dispatcher: os projetos podem ser organizados mais facilmente. Por exemplo, agora você pode incluir vários arquivos de regras de regravação que refletem a estrutura do site. [Saiba mais sobre](/help/implementing/dispatcher/disp-overview.md#validation-debug) esse modo flexível, incluindo como estruturar sua configuração do Dispatcher para que você possa aproveitá-lo.
* A interface de replicação de árvore na guia &quot;Distribuir&quot; do agente de replicação deve ser considerada obsoleta e foi removida após 30 de setembro de 2021. [Saiba mais sobre](/help/operations/replication.md#tree-activation) estratégias alternativas de replicação.
* O pacote `org.apache.sling.datasource-1.0.4.jar` para suporte à fonte de dados do Sling foi removido, pois tem funcionalidades desatualizadas e não está em uso pelos clientes.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Novos recursos no [!DNL Assets] {#assets-features}

* A funcionalidade de Automatização de Conteúdo permite que o [!DNL Experience Manager Assets] use as APIs do [!DNL Adobe Creative Cloud] para automatizar a produção de ativos em escala. Isso melhora a velocidade do conteúdo diminuindo drasticamente o tempo gasto e as iterações necessárias para criar variações do mesmo ativo. A funcionalidade não requer programação e funciona no DAM. Consulte [gerar variações de ativos usando a integração com o Creative Cloud](/help/assets/cc-api-integration.md).

* [!DNL Experience Manager Assets] inclui o Visualizador de PDF [!DNL Document Cloud] para visualizar documentos PDF nativamente. Esse recurso permite que os usuários visualizem arquivos PDF de várias páginas sem processamento ou conversão de arquivos. Este recurso melhora a paridade com o [!DNL Experience Manager] 6.5. Os controles disponíveis no visualizador incluem zoom, navegar até páginas, desencaixar controles e exibir em tela inteira. Os usuários também podem visualizar e ir para páginas e marcadores. Comentários no próprio arquivo são aceitos. Comentários e anotações sobre o conteúdo no arquivo PDF estão planejados para uma versão futura.

  ![Visualizar arquivos de PDF em [!DNL Experience Manager] usando o Visualizador de PDF](/help/assets/assets/preview-pdf-file-viewer.png)

* A funcionalidade de download Compartilhamento de link usa downloads assíncronos que aumentam a velocidade de download. Para obter mais informações, consulte [Baixar ativos compartilhados usando o compartilhamento de link](/help/assets/download-assets-from-aem.md#link-share-download).

  ![Baixar caixa de entrada](/help/assets/assets/download-inbox.png)

* As configurações de exibição são aprimoradas para permitir que os usuários escolham uma exibição padrão e um parâmetro de classificação padrão.

  ![Definir exibição padrão em [!UICONTROL Configurações de Exibição]](/help/assets/assets/view-settings-for-defaults.png)

* Os usuários podem pesquisar e filtrar as pastas com base em predicados de propriedade.

  ![Filtrar pastas de pesquisa usando predicados de pesquisa](/help/assets/assets/search-folders-via-predicates.png)

### Novos recursos disponíveis no canal de pré-lançamento do [!DNL Assets] {#assets-prerelease-features}

<!-- TBD: Not sure about GA of these enh. Shall check with the team.

* A user experience enhancements displays the number of assets present in a folder. For more than 1000 assets in a folder, [!DNL Assets] displays 1000+.

  ![Number of assets in a folder are displayed on the interface](/help/assets/assets/browse-folder-number-of-assets.png)

* You can directly apply a metadata schemas to a folder in its [!UICONTROL Properties].

  ![Add metadata schema from folder properties](/help/assets/assets/metadata-schema-folder-properties.png)
-->

* Ao compartilhar ativos digitais como um link, os usuários podem copiar o URL para a área de transferência. O aprimoramento permite compartilhar ativos de maneira mais rápida e prática.

### Bugs corrigidos em [!DNL Assets] {#assets-bugs-fixed}

A API `com.day.cq.dam.api.collection.SmartCollection` não está disponível em [!DNL Experience Manager] como [!DNL Cloud Service]. (CQ-4326322)

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Novidades do [!DNL Forms] {#what-is-new-forms}

* Agora você pode usar o serviço Automated forms conversion para [converter PDF forms em francês, alemão e espanhol](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?lang=pt-BR&#language-specific-meta-model) para formulários adaptáveis.
* Adição de um painel separado ao editor de modelo para exibir erros relacionados aos componentes de formulário adaptáveis. Ele ajuda a consolidar todos os erros de formulário adaptável em um local e a reduzir o tempo de resolução.

### Novos recursos disponíveis no canal de pré-lançamento do [!DNL Forms] {#beta-features-forms}

* **[!DNL AEM Forms as a Cloud Service - Communications]**: [APIs de comunicação](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications.html?lang=pt-BR) ajudam a combinar modelos XDP e dados XML para gerar documentos de impressão em vários formatos. O serviço permite gerar documentos em modo síncrono. As APIs permitem criar aplicativos que possibilitam a você:
   * Gerar documentos preenchendo arquivos de modelo com dados XML.
   * Gerar formulários de saída em vários formatos, incluindo fluxos de impressão de PDF não interativos.
   * Gere arquivos de PDF de impressão a partir de um PDF de formulário XFA e do formulário Adobe Acrobat.

* **Externalizador de Dados de Variáveis**: você pode salvar dados de variáveis de Fluxo de Trabalho do AEM em um sistema de armazenamento externo gerenciado por sua organização.

* **Documento de registro baseado em acroforma**: você também pode [usar o PDF do formulário do Adobe Acrobat (PDF de acroforma)](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/generate-document-of-record-for-non-xfa-based-adaptive-forms.html?lang=pt-br) como um modelo para Documento de registro além do modelo de formulário baseado em XFA.

* **Conector do armazenamento de dados do Microsoft® Azure**: agora é possível [conectar o Modelo de dados do formulário ao Armazenamento do Microsoft® Azure](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/configure-azure-storage.html?lang=pt-BR). Ele permite recuperar e armazenar dados de formulário adaptáveis para o Armazenamento do Microsoft® Azure como um BLOB.

## Complemento CIF {#cloud-services-cif}

### Novidades {#what-is-new-cif}

* Componentes principais do CIF v2
   * Configurações simplificadas e aprimoradas para URL e SEO de PDP/PLP
   * Indicador visual para dados de produtos preparados no modo de criação para melhor visibilidade de alterações futuras
   * Novo componente de mapa de site para páginas de conteúdo e comércio

* Suporte para a [Recomendação de produto do Adobe Commerce Sensei, habilitada pelo Adobe Sensei](https://business.adobe.com/br/products/magento/product-recommendations.html) na loja AEM usando recomendações predefinidas ou criadas dinamicamente

## [!DNL Experience Manager Screens] as a [!DNL Cloud Service] {#screens}

### Correções de erros {#bug-fixes-screens}

* As configurações do Provedor de conteúdo agora são validadas durante a criação ou atualização.

* Todas as exibições de exibição têm colunas de pastas.

* É possível expandir a Estrutura de conteúdo do Screens.

* `bulk-offline-update-service` não tinha todas as permissões para alguns ambientes.

* Foi atualizado o link da Ajuda para corresponder à nova documentação da nuvem do Screens.

* Cancela a atribuição de listas de reprodução e proíbe a remoção de listas de reprodução com reprodutores atribuídos, agora funciona.

* O reprodutor agora rebaixa o Assets quando o cache &quot;ALL&quot; é limpo.

* O Agendamento repetido agora funciona se a *Hora de término* estiver definida para o dia seguinte.

* `Back&Forward` agora funciona na interface de usuário as a Cloud Service do Screens.

* Tags com o mesmo nome, mas namespaces diferentes não puderam ser criadas anteriormente.

## XML Documentation para o Experience Manager as a Cloud Service {#xml-documentation}

### Novidades {#what-is-new-xml-documentation}

O XML Documentation para o Experience Manager as a Cloud Service está disponível de modo geral. Ele permite que os clientes do Experience Manager as a Cloud Service obtenham um complemento do XML Documentation para importar, criar, gerenciar e fornecer conteúdo técnico em vários canais, incluindo o Experience Manager Sites.

## Cloud Manager {#cloud-manager}

Esta seção descreve as Notas de versão do Cloud Manager no AEM as a Cloud Service 2021.7.0.

### Data de lançamento {#release-cm-july}

A data de lançamento do Cloud Manager no AEM as a Cloud Service 2021.7.0 é 15 de julho de 2021.
A próxima versão está planejada para 12 de agosto de 2021.

### Novidades {#what-is-new-cm-july}

* Os clientes agora podem usar os JDKs Azul 8 e 11 para seus processos de compilação do Cloud Manager e podem optar por usar um desses JDKs para os plug-ins Maven compatíveis com cadeias de ferramentas *ou* para toda a execução do processo Maven.

* O IP de saída agora está registrado no arquivo de log da etapa de compilação.

* Ambientes de Preparo e Produção que executam versões antigas do AEM agora relatam um status de **Atualização Disponível**.

* O número máximo de certificados SSL suportados aumentou para 20 por programa.

* O número máximo de domínios que podem ser configurados aumentou para 500 por ambiente.

* O botão **Gerenciar Git** foi renomeado como **Acessar Informações do Git** e a caixa de diálogo foi atualizada visualmente.

* A versão do Arquétipo de Projetos AEM usada pelo Cloud Manager foi atualizada para a versão 28.

### Correções de erros {#bug-fixes-cm-july}

* Em algumas situações, a opção Visualizar não estava disponível ao vincular uma inclui na lista de permissões IP a um ambiente.

* Ao navegar manualmente para a página de detalhes de uma execução não existente, nenhum erro era exibido, apenas uma tela de carregamento infinita.

* A mensagem de erro exibida quando o número máximo de certificados SSL era atingido não era útil.

* Em algumas circunstâncias, podia haver uma discrepância na versão de lançamento mostrada no cartão de pipeline na página **Visão geral**.

* O assistente de adição de programas declarou incorretamente que o nome não pode ser alterado após a criação.

### Problemas conhecidos {#known-issues-cm-july}

Os clientes que alternam para usar os JDKs Azul devem saber que nem todos os aplicativos existentes são compilados sem erro no JDK Azul. O Adobe recomenda que você teste localmente antes de alternar.

## Cloud Acceleration Manager {#cam}

### Data de lançamento {#release-date-july-cam}

A data de lançamento do Cloud Acceleration Manager é 15 de julho de 2021.

### Novidades {#what-is-new-cam}

O Cloud Acceleration Manager é um aplicativo baseado em nuvem projetado para orientar suas equipes de TI durante toda a jornada de transição, começando pelo planejamento até a ativação do Cloud Service. Prepare sua equipe para a migração bem-sucedida com práticas recomendadas, dicas, documentação e ferramentas do Adobe para ajudar em cada fase da jornada a AEM como Cloud Service. Saiba mais [aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-acceleration-manager/using-cam/getting-started-cam.html?lang=pt-BR).

>[!NOTE]
>
> Veja este [vídeo de demonstração do Cloud Acceleration Manager](https://video.tv.adobe.com/v/335547).
