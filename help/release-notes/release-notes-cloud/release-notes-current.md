---
title: Notas de versão atuais do  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Notas de versão atuais do  [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
mini-toc-levels: 1
source-git-commit: a3e18349c3cf2240cc68275a3862abeb75ea372a
workflow-type: tm+mt
source-wordcount: '955'
ht-degree: 15%

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

A data de lançamento do [!DNL Adobe Experience Manager] como [!DNL Cloud Service] a versão atual (2022.7.0) é 8 de agosto de 2022.

A próxima versão (2022.8.0) está planejada para 25 de agosto de 2022.

## Vídeo da versão {#release-video}

Assista ao vídeo Visão geral da versão de julho de 2022 para obter um resumo dos recursos adicionados na versão 2022.7.0:

>[!VIDEO](https://video.tv.adobe.com/v/345409/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Novos recursos no [!DNL Sites] {#sites-features}

* O [Console do fragmento do conteúdo](/help/sites-cloud/administering/content-fragments/content-fragments-console.md) agora suporta [atalhos do teclado](/help/sites-cloud/administering/content-fragments/content-fragments-console-keyboard-shortcuts.md).

* AEM como Cloud Service [entrega de imagem otimizada para a Web](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/web-optimized-image-delivery.html) O permite melhorar significativamente a velocidade da página, fornecendo formatos como o WebP. Esse novo serviço também oferece opções mais flexíveis de redimensionamento e transformação de imagem. Todas as versões do [Componente de imagem principal](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/image.html?lang=pt-BR) permite aproveitar esse serviço e fornecer imagens como WebP ao clicar em uma opção na política do componente de imagem.

* AEM atividades de personalização agora podem aproveitar fragmentos de experiência no lugar de nossas ofertas herdadas. Este recurso:
   * permite um caminho de migração, onde AEM conteúdo promoveria ofertas de fragmento de experiência, em vez de ofertas de biblioteca herdadas, para fornecer conteúdo com o estilo adequado, alinhado com a personalização na escala a partir de agora.
   * impede que os autores de conteúdo vejam acidentalmente o conteúdo com estilo não estilizado em seu site.
   * O permite que o modo de direcionamento de qualquer componente seja convertido em um fragmento de experiência (JSON e tipos de HTML) que usa modelos editáveis.

>[!NOTE]
>
>As atividades de personalização existentes que já usam ofertas herdadas podem continuar a fazê-lo, mas novas atividades de personalização devem ser criadas como fragmentos de experiência, pois essa é a abordagem recomendada a partir de agora.

## [!DNL Experience Manager Assets] como [!DNL Cloud Service] {#assets}

### Novos recursos disponíveis no canal de pré-lançamento do [!DNL Assets] {#prerelease-features-assets}

Agora você pode configurar os Ativos Adobe Experience Manager para [restringir o tipo de ativos que os usuários podem fazer upload com base no tipo MIME](/help/assets/configure-asset-upload-restrictions.md).

![Restrições de upload de ativos](/help/assets/assets/asset-upload-restrictions.png)

## [!DNL Experience Manager Forms] como [!DNL Cloud Service] {#forms}

### Novos recursos no [!DNL Forms] {#forms-features}

* **Suporte de entrada de teclado para assinaturas Scribble**: Os Forms adaptáveis são cada vez mais usados em dispositivos de toque, e um requisito comum é o suporte a assinaturas. Assinar documentos em dispositivos de toque se tornou uma maneira aceita de assinar formulários. O Adaptive Forms tem suporte nativo para Assinaturas do Scribble e Adobe Sign para esses casos de uso. Agora, juntamente com outras opções já suportadas, você também pode usar o teclado para Assinaturas do Scribble em um formulário adaptável. Também ajuda a melhorar a conformidade de acessibilidade.

![Suporte de entrada de teclado para assinaturas Scribble no iphone](/help/release-notes/assets/scribble-keyboard-mobile.png)

* **Usar o assistente do Adaptive Forms no idioma local**: Você pode usar o assistente no idioma de sua escolha. Agora, ele é compatível com todos os idiomas suportados pelo Adobe Experience Manager.

### Novos recursos disponíveis no canal de pré-lançamento do [!DNL Forms] {#prerelease-features-forms}

<!-- * **[Launch Adaptive Form creation wizard from embed form component](/help/forms/using/embed-adaptive-form-aem-sites.md)**: You can now launch Adaptive Form creation wizard from embed form component. It helps improve content and forms authoring workflows for Sites and Forms practitioners trying to add enrollment experiences to a web page. 

![Keyboard input support for Scribble signatures on iphone](/help/release-notes/assets/froms-container.png) -->

* **Invocar - Uma etapa AEM do fluxo de trabalho**: Document Description XML (DDX) é uma linguagem de marcação declarativa cujos elementos representam blocos de construção de documentos. Esses blocos fundamentais incluem documentos PDF e XDP e outros elementos, como comentários, marcadores e texto estilizado. Os documentos DDX são modelos para os documentos e descrevem as características desejadas dos documentos de origem que devem aparecer nos documentos resultantes. Um único DDX pode ser usado com um intervalo de documentos de origem. Você pode usar a etapa Chamar e o Fluxo de trabalho AEM para executar várias operações, como montar documentos de desmontagem, criar e modificar o Acrobat e o XFA Forms e outras operações descritas em [Referência DDX](https://helpx.adobe.com/content/dam/help/en/experience-manager/forms-cloud-service/ddxRef.pdf) documentação.

* **Converter em PDF/A - uma etapa do fluxo de trabalho AEM**: PDF/A é um formato de arquivo para a preservação de longo prazo do conteúdo do documento, todas as fontes são incorporadas e o arquivo é descompactado. Agora, você pode usar a etapa Converter em PDF/A e o Fluxo de trabalho AEM para converter documentos ou arquivos em qualquer formato no formato PDF/A.


## Complemento CIF {#cloud-services-cif}

### Novidades {#what-is-new-cif}

* O enriquecimento do catálogo de produtos agora é compatível com páginas AEM. Isso permite que os autores gerenciem a associação de página e produto.

* Várias melhorias nos Componentes principais da CIF

### Correções de bugs {#bug-fixes-cif}

* Adicionar token de logon à busca de preços no lado do cliente

* Componente de página incorreto no datalayer

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Novidades {#what-is-new-foundation}

* O [Navegador de Repositório](/help/implementing/developing/tools/repository-browser.md) O agora tem um campo de entrada de caminho, permitindo ir diretamente para uma pasta específica na hierarquia do repositório
* A Distribuição de conteúdo de sling (SCD) agora oferece suporte a uma ação de &quot;invalidação&quot; explícita para invalidar o conteúdo sem que ele seja publicado. Consulte a [Armazenamento em cache em AEM as a Cloud Service](/help/implementing/dispatcher/caching.md#explicit-invalidation) para obter mais detalhes.
* mod_macro agora está disponível AEM as a Cloud Service. Consulte [esta tabela](/help/implementing/dispatcher/disp-overview.md) para obter uma lista de módulos Apache suportados.

### AEM aprimoramentos as a Cloud Service das ferramentas do Dispatcher do SDK {#dispatcher-tools-enhancements}

* O Apache pode ser iniciado com `update_sdk.sh` , que carregará e validará automaticamente quaisquer alterações subsequentes na configuração do apache e do dispatcher, melhorando assim a velocidade do desenvolvedor. Só há suporte para o modo flexível de ferramentas do dispatcher. Além disso, consulte [Depuração da configuração do Apache e Dispatcher](/help/implementing/dispatcher/validation-debug.md#automatic-loading) para obter detalhes adicionais sobre carregamento e validação automáticos.
* A configuração local do apache/dispatcher monitorará mais detalhadamente as alterações em ambientes de nuvem, aumentando a paridade entre os dois ambientes.

### Novos recursos disponíveis no canal de pré-lançamento do [!DNL Experience Manager] {#prerelease-features-foundation}

* AEM as a Cloud Service agora está integrado ao Unified Shell para melhorar a experiência do usuário e unificá-la com todos os outros aplicativos do Experience Cloud. Consulte [AEM as a Cloud Service no shell unificado](/help/overview/aem-cloud-service-on-unified-shell.md) para obter mais detalhes.

## Conectores do gerenciador de aprendizado do Adobe {#learn-manage}

* O novo Gerente de aprendizado do Adobe tem conectores com Adobe Experience Manager Sites, Marketo Engage e Adobe Commerce. Para saber mais, consulte: [Guia do usuário do Adobe Learning Manager](https://helpx.adobe.com/learning-manager/user-guide.html).


## Cloud Manager {#cloud-manager}

Você pode encontrar uma lista completa de versões mensais do Cloud Manager [aqui](/help/implementing/cloud-manager/release-notes-cloud-manager/release-notes-cm-current.md).

## Ferramentas de migração {#migration-tools}

Você pode encontrar uma lista completa das versões das Ferramentas de migração [here](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
