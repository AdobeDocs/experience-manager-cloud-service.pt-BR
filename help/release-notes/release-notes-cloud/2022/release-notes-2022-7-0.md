---
title: Notas de versão do  [!DNL Adobe Experience Manager]  as a Cloud Service 2022.7.0.
description: Notas de versão do  [!DNL Adobe Experience Manager]  as a Cloud Service 2022.7.0.
exl-id: b339ab48-e836-4589-a573-9c50917b9280
feature: Release Information
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '935'
ht-degree: 81%

---

# Notas de versão 202278.0 para [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

A seção a seguir descreve as notas de versão de recurso da versão 2022.7.0 do [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>A partir daqui, você pode navegar até as notas de versão das versões anteriores; por exemplo, para aquelas em 2020, 2021 e assim por diante.

>[!NOTE]
>
>Consulte [Atualizações recentes na documentação](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=pt-BR) para obter detalhes de atualizações de documentação não relacionadas diretamente a uma versão.

## Data de lançamento {#release-date}

A data de lançamento da versão atual do [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] (2022.7.0) é 8 de agosto de 2022.

A próxima versão (2022.8.0) está planejada para 1º de setembro de 2022.

## Vídeo da versão {#release-video}

Assista ao vídeo Visão geral da versão de julho de 2022 para ver um resumo dos recursos adicionados na versão 2022.7.0:

>[!VIDEO](https://video.tv.adobe.com/v/345409/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Novos recursos no [!DNL Sites] {#sites-features}

* O [Console de fragmentos de conteúdo](/help/sites-cloud/administering/content-fragments/managing.md#content-fragments-console) agora é compatível com [atalhos de teclado](/help/sites-cloud/administering/content-fragments/keyboard-shortcuts.md).

* AEM como Cloud Service [entrega de imagens otimizadas para a Web](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/web-optimized-image-delivery.html?lang=pt-BR) O permite melhorar significativamente a velocidade da página, fornecendo formatos como o WebP. Esse novo serviço também oferece opções mais flexíveis de redimensionamento e transformação de imagem. Todas as versões do [Componente de imagem principal](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/image.html?lang=pt-BR) Permitem usar este serviço e fornecer imagens em formato WebP clicando em uma opção na política do componente de imagem.

* As atividades de personalização do AEM agora podem usar fragmentos de experiência no lugar de nossas ofertas herdadas. Este recurso:
   * permite um caminho de migração, onde o conteúdo do AEM promoveria ofertas de fragmentos de experiência, em vez de ofertas de bibliotecas herdadas, para fornecer conteúdo com estilo adequado e alinhado com a personalização em escala a partir de agora.
   * impede que os autores de conteúdo forneçam acidentalmente conteúdo não estilizado no site.
   * permite que o modo de direcionamento de qualquer componente seja convertido em um fragmento de experiência (dos tipos JSON e HTML) que usa modelos editáveis.

>[!NOTE]
>
>As atividades de personalização existentes que já usam ofertas herdadas podem continuar a fazê-lo. No entanto, novas atividades de personalização devem ser criadas como fragmentos de experiência, pois essa é a abordagem recomendada a partir de agora.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Novos recursos disponíveis no canal de pré-lançamento do [!DNL Assets] {#prerelease-features-assets}

Agora é possível configurar o Adobe Experience Manager Assets para [restringir os tipos de ativos que os usuários podem fazer upload com base no tipo de MIME](/help/assets/configure-asset-upload-restrictions.md).

![Restrições de upload de ativos](/help/assets/assets/asset-upload-restrictions.png)

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Novos recursos no [!DNL Forms] {#forms-features}

* **[Compatibilidade com entrada de teclado para assinaturas escritas](/help/forms/signing-forms-using-scribble.md)**: os formulários adaptáveis são cada vez mais usados em dispositivos de toque, e um requisito comum é a compatibilidade com assinaturas. Assinar documentos em dispositivos de toque se tornou uma maneira aceita de assinar formulários. Os formulários adaptáveis têm compatibilidade nativa com assinaturas escritas e com o Adobe Sign para esses casos de uso. Agora, juntamente com outras opções já compatíveis, também é possível usar o teclado para criar assinaturas escritas em um formulário adaptável. Isso também ajuda a melhorar a conformidade de acessibilidade.

![Compatibilidade com entrada de teclado para assinaturas escritas no iPhone](/help/release-notes/assets/scribble-keyboard-mobile.png)

* **Usar o assistente de formulários adaptáveis no idioma local**: você pode usar o assistente no idioma de sua escolha. Agora, ele aceita todos os idiomas compatíveis com o Adobe Experience Manager.

### Novos recursos disponíveis no canal de pré-lançamento do [!DNL Forms] {#prerelease-features-forms}

<!-- 

* **[Launch Adaptive Form creation wizard from embed form component](/help/forms/using/embed-adaptive-form-aem-sites.md)**: You can now launch Adaptive Form creation wizard from embed form component. It helps improve content and forms authoring workflows for Sites and Forms practitioners trying to add enrollment experiences to a web page. 

![Keyboard input support for Scribble signatures on iphone](/help/release-notes/assets/froms-container.png) 

-->

* **[Chamar DDX - uma etapa do fluxo de trabalho do AEM](/help/forms/aem-forms-workflow-step-reference.md#invokeddx)**: o Document Description XML (DDX) é uma linguagem de marcação declarativa cujos elementos representam os blocos fundamentais de documentos. Esses blocos fundamentais incluem documentos PDF e XDP, além de outros elementos, como comentários, marcadores e texto estilizado. Os documentos DDX são modelos de documentos e descrevem as características desejadas dos documentos de origem que devem aparecer nos documentos resultantes. Um único DDX pode ser usado com uma variedade de documentos de origem. Você pode usar a etapa Chamar do fluxo de trabalho do AEM para executar várias operações, como montar e desmontar documentos, criar e modificar formulários do Acrobat e do XFA, além de outras operações descritas na documentação de [referência do DDX](https://helpx.adobe.com/content/dam/help/en/experience-manager/forms-cloud-service/ddxRef.pdf).

* **[Converter em PDF/A - Uma etapa do fluxo de trabalho AEM](/help/forms/aem-forms-workflow-step-reference.md##convert-pdfa)**: PDF/A é um formato para arquivamento destinado a preservação do conteúdo do documento a longo prazo; todas as fontes são incorporadas e o arquivo é descompactado. Agora, é possível usar a etapa Converter em PDF/A do fluxo de trabalho do AEM para converter documentos ou arquivos de qualquer formato para o formato PDF/A.


## Complemento CIF {#cloud-services-cif}

### Novidades {#what-is-new-cif}

* O enriquecimento do catálogo de produtos agora é compatível com as páginas do AEM. Isso permite que os autores gerenciem a associação entre página e produto.

* Várias melhorias nos Componentes principais da CIF

### Correções de erros {#bug-fixes-cif}

* Adicionar token de logon à busca de preços no lado do cliente

* Componente de página incorreto no datalayer

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Novidades {#what-is-new-foundation}

* Agora, o [Navegador do repositório](/help/implementing/developing/tools/repository-browser.md) tem um campo de entrada de caminho, permitindo navegar diretamente para uma pasta específica na hierarquia do repositório
* A Distribuição de conteúdo do Sling (SCD) agora é compatível com uma ação de &quot;invalidação&quot; explícita para invalidar o conteúdo sem que ele seja publicado. Consulte [Armazenamento em cache no AEM as a Cloud Service](/help/implementing/dispatcher/caching.md#explicit-invalidation) para obter mais detalhes.
* O módulo mod_macro agora está disponível no AEM as a Cloud Service. Consulte [esta tabela](/help/implementing/dispatcher/disp-overview.md) para obter uma lista de módulos compatíveis do Apache.

### Aprimoramentos das ferramentas do Dispatcher do SDK do AEM as a Cloud Service {#dispatcher-tools-enhancements}

* O Apache pode ser iniciado com o script `docker_run_hot_reload.sh`, que carregará e validará automaticamente quaisquer alterações subsequentes na configuração do Apache e do Dispatcher, melhorando assim a velocidade do desenvolvedor. Compatível apenas com o modo flexível de ferramentas do Dispatcher. Além disso, consulte [Depuração da configuração do Apache e Dispatcher](/help/implementing/dispatcher/validation-debug.md#automatic-reloading) para obter detalhes adicionais sobre recarregamento e validação automáticos.
* A configuração local do Apache/Dispatcher monitorará mais detalhadamente as alterações em ambientes de nuvem, aumentando a paridade entre os dois ambientes.

### Novos recursos disponíveis no canal de pré-lançamento do [!DNL Experience Manager] {#prerelease-features-foundation}

* O AEM as a Cloud Service agora está integrado ao shell unificado para melhorar a experiência do usuário e unificá-la com todos os outros aplicativos da Experience Cloud. Consulte [AEM as a Cloud Service no shell unificado](/help/overview/aem-cloud-service-on-unified-shell.md) para obter mais detalhes.

## Conectores do Adobe Learning Manager {#learn-manage}

* O novo Adobe Learning Manager possui conectores de integração ao Adobe Experience Manager Sites, Marketo Engage e Adobe Commerce. Para saber mais, consulte: [Guia do usuário do Adobe Learning Manager](https://helpx.adobe.com/br/learning-manager/user-guide.html).

## Cloud Manager {#cloud-manager}

Você pode encontrar uma lista completa de versões mensais do Cloud Manager [aqui](/help/implementing/cloud-manager/release-notes/current.md).

## Ferramentas de migração {#migration-tools}

Você pode encontrar uma lista completa de versões das ferramentas de migração [aqui](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
