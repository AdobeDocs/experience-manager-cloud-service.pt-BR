---
title: Notas de versão atuais para [!DNL Adobe Experience Manager] como um Cloud Service.
description: Notas de versão atuais para [!DNL Adobe Experience Manager] como um Cloud Service.
translation-type: tm+mt
source-git-commit: a09377df02225e9ad58ea4a8a0671fc40bd7d703
workflow-type: tm+mt
source-wordcount: '692'
ht-degree: 5%

---


# Notas de versão do [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

A seção a seguir descreve as Notas de versão gerais de [!DNL Experience Manager] como um Cloud Service.

## Data de lançamento {#release-date}

A data de lançamento de [!DNL Adobe Experience Manager] como Cloud Service 2020.12.0 é 17 de dezembro de 2020.
A seguinte versão (2021.1.0) será lançada em 28 de janeiro de 2021.

## [!DNL Adobe Experience Manager Sites] como um Cloud Service  {#sites}

* **[API](/help/assets/content-fragments/assets-api-content-fragments.md)** HTTP do fragmento de conteúdo: Adicione a capacidade de adicionar/atualizar e excluir variações do fragmento de conteúdo usando a API HTTP.

## [!DNL Adobe Experience Manager Assets] como uma  [!DNL Cloud Service] {#assets}

* A integração com [!DNL Adobe InDesign Server] agora está disponível para [!DNL Experience Manager] como [!DNL Cloud Service]. Ele fornece automação para processar [!DNL Adobe InDesign] arquivos usando [!DNL Adobe InDesign Server] scripts e permite que os usuários usem [!DNL Assets] modelos de interface do usuário para criar folhetos ou anúncios. Somente [!DNL InDesign Server] hospedado por [!DNL Adobe Managed Services] é suportado por [!DNL Experience Manager as a Cloud Service]. <!-- TBD: Add link to article. -->

* [!DNL Experience Manager] é aprimorada para rastrear e exibir referências de ativos quando um ativo é usado em uma  [!DNL Experience Manager Sites] implantação remota usando a funcionalidade Ativos conectados. Uma nova guia [!UICONTROL Referências] na página [!UICONTROL Propriedades] do ativo agora lista referências locais e remotas do ativo. As referências permitem que os usuários do DAM rastreiem a utilização de ativos em [!DNL Sites] páginas e em ativos compostos em [!DNL Assets]. Consulte [configurar e usar os ativos conectados](/help/assets/use-assets-across-connected-assets-instances.md).

* [!DNL Dynamic Media] agora são acessíveis por meio dos Componentes principais baseados em  [!DNL Sites] imagem. Os autores podem configurar rapidamente os componentes para usar as Predefinições de imagem, o Recorte inteligente e os Modificadores de imagem ao criar páginas da Web. Consulte [Versão dos componentes principais 2.13.0](https://github.com/adobe/aem-core-wcm-components/releases/tag/core.wcm.components.reactor-2.13.0).

* [!DNL Experience Manager] o aplicativo para desktop permite que os usuários carreguem arquivos e pastas arrastando os arquivos do Windows Explorer ou do Mac Finder na interface do aplicativo para desktop. Consulte [adicionar ativos usando o aplicativo de desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#upload-and-add-new-assets-to-aem).

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novidades {#what-is-new-commerce}

* Lançamento do site de referência CIF Venia - 2020.12.01 que inclui a versão mais recente dos componentes principais CIF v1.6.0. Consulte [CIF Site de Referência de Venia](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2020.12.01) para obter mais detalhes.

* Componentes principais CIF lançados v1.6.0. Consulte [CIF Componentes principais](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.6.0) para obter mais detalhes.

## Cloud Manager {#cloud-manager}

### Data de lançamento {#release-date-cm}

A data de lançamento do Cloud Manager no AEM como Cloud Service 2021.1.0 é 14 de janeiro de 2021.

### Correções de erros {#bug-fixes-cloud-manager}

* A instância Produção de ativos pode, ocasionalmente, mostrar o status do Portal de marcas na página de detalhes **Ambientes** como *Pendente* sem permitir que o usuário execute nenhuma ação.

* Ao disparar uma hibernação do Gerenciador de nuvem, às vezes uma mensagem de falha era exibida mesmo quando a hibernação era iniciada com êxito.

* Casos raros de falha encontrados na criação ou exclusão de ambientes foram abordados.

## Ferramentas de refatoração de código {#code-refactoring-tools}

### Novidades em [!DNL Code Refactoring Tools] {#what-is-new-crt}

* Nova versão do plug-in AIO-CLI lançada. A versão mais recente deste plug-in inclui correções de erros para o AEM Dispatcher Converter e o Repository Modernizer, além de oferecer suporte a um novo utilitário - Index Converter. Consulte [Experiência unificada](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/unified-experience.html?lang=en#benefits) para saber mais sobre este plug-in.

* Index Converter é um utilitário que pode ser usado para transformar as Definições de índice OAK personalizado de um cliente em AEM como Definições de índice OAK compatíveis com Cloud Service. Consulte [Index Converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/index-converter) para obter mais detalhes.

* Novo recurso adicionado ao [Modernizador do repositório](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer) que cria um pacote separado `ui.config` para conter todas as configurações de OSGi.

### Correções de erros {#crt-bug-fixes}

* Várias correções de erros feitas nas ferramentas AEM Dispatcher Converter e Repository Modernizer. Consulte [AEM Dispatcher Converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter) e [Modernizador do Repositório](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer).

## Ferramentas de transição para a nuvem {#code-transition-tools}

### Data de lançamento {#release-date-ctt}

A data de lançamento da Content Transfer Tool v1.1.20 é 8 de janeiro de 2021.

### Novidades em [!DNL Content Transfer Tool] {#what-is-new-ctt}

* Os usuários agora podem saber se o Token de acesso expirou passando o mouse sobre o ícone de status na interface do usuário da Ferramenta de transferência de conteúdo (CTT). Eles também serão notificados na interface do usuário Detalhes do Conjunto de Migrações de que não conseguem se conectar à instância do Cloud Service.

### Correções de erros {#ctt-bug-fixes}

* O status da interface do usuário da Ferramenta de transferência de conteúdo (CTT) para um conjunto de migração não persistiu e foi alterado após um período de inatividade. Isso foi corrigido.
* A opção para registros de visualizações foi desativada se os registros não estivessem disponíveis. Isso foi corrigido e as mensagens foram adicionadas para notificar ao usuário por que os logs estão ausentes.
* O status da interface do usuário da Ferramenta de transferência de conteúdo mostrava FALHA quando o usuário parava uma ingestão. Isso foi corrigido para exibir *PARADO*.

