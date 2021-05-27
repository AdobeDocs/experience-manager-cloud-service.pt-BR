---
title: Notas de versão do  [!DNL Adobe Experience Manager] as a Cloud Service 2020.12.0.
description: Notas de versão do  [!DNL Adobe Experience Manager] as a Cloud Service 2020.12.0.
exl-id: 16875180-1f23-477d-9d4d-e220998c4983
source-git-commit: aeee895e4a4b959125d08091619988d0ffa09ace
workflow-type: tm+mt
source-wordcount: '693'
ht-degree: 7%

---

# Notas de versão do [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

A seção a seguir descreve as Notas de versão gerais para [!DNL Experience Manager] como um Cloud Service.

## Data de lançamento {#release-date}

A Data de lançamento de [!DNL Adobe Experience Manager] como Cloud Service 2020.12.0 é 17 de dezembro de 2020.
A seguinte versão (2021.1.0) será lançada em 28 de janeiro de 2021.

## [!DNL Adobe Experience Manager Sites] como um Cloud Service {#sites}

* **[API](/help/assets/content-fragments/assets-api-content-fragments.md)** HTTP do fragmento de conteúdo: Adicione a capacidade de adicionar/atualizar e excluir variações do Fragmento de conteúdo usando a API HTTP.

## [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

* A integração com [!DNL Adobe InDesign Server] agora está disponível para [!DNL Experience Manager] como um [!DNL Cloud Service]. Ele fornece automação para processar arquivos [!DNL Adobe InDesign] usando scripts [!DNL Adobe InDesign Server] e permite que os usuários usem [!DNL Assets] modelos de interface do usuário para criar brochuras ou anúncios. Somente [!DNL InDesign Server] hospedado por [!DNL Adobe Managed Services] é suportado para [!DNL Experience Manager as a Cloud Service]. <!-- TBD: Add link to article. -->

* [!DNL Experience Manager] O é aprimorado para rastrear e exibir referências de ativos quando um ativo é usado em uma  [!DNL Experience Manager Sites] implantação remota usando a funcionalidade Ativos conectados. Uma nova guia [!UICONTROL Referências] na página [!UICONTROL Propriedades] do ativo agora lista referências locais e remotas do ativo. As referências permitem que os usuários do DAM rastreiem o uso de ativos em [!DNL Sites] páginas e em ativos compostos em [!DNL Assets]. Consulte [configurar e usar o Connected Assets](/help/assets/use-assets-across-connected-assets-instances.md).

* [!DNL Dynamic Media] agora são acessíveis por meio dos Componentes principais baseados em  [!DNL Sites] imagem. Os autores podem configurar rapidamente os componentes para usar Predefinições de imagem, Recorte inteligente e Modificadores de imagem ao criar páginas da Web. Consulte a versão [Componentes principais 2.13.0](https://github.com/adobe/aem-core-wcm-components/releases/tag/core.wcm.components.reactor-2.13.0).

* [!DNL Experience Manager] o aplicativo de desktop permite que os usuários façam upload de arquivos e pastas arrastando os arquivos do Windows Explorer ou do Mac Finder na interface do aplicativo de desktop. Consulte [adicionar ativos usando o aplicativo de desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#upload-and-add-new-assets-to-aem).

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novidades {#what-is-new-commerce}

* Lançamento do site de referência CIF Venia - 2020.12.01, que inclui a versão mais recente dos Componentes principais CIF v1.6.0. Consulte [Site de referência CIF Venia](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2020.12.01) para obter mais detalhes.

* Lançamento de componentes principais CIF v1.6.0. Consulte [Componentes principais CIF](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.6.0) para obter mais detalhes.

## Cloud Manager {#cloud-manager}

### Data de lançamento {#release-date-cm}

A Data de lançamento do Cloud Manager no AEM as a Cloud Service 2020.12.0 é 10 de dezembro de 2020.

### Novidades em [!DNL Cloud Manager] {#what-is-new-cm}

* Gerenciamento de autoatendimento de [Certificados SSL](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md) e [Nomes de Domínio Personalizados](/help/implementing/cloud-manager/custom-domain-names/introduction.md).

* Gerenciamento de autoatendimento de [Listas de permissões IP](/help/implementing/cloud-manager/ip-allow-lists/introduction.md).

* A página de detalhes do **Ambiente** atualizada agora permite que os usuários gerenciem Nomes de Domínio Personalizados e Listas de permissões de IP em seus ambientes.

### Correções de erros {#bug-fixes-cloud-manager}

* Algumas ocorrências de falhas em estágio de digitalização de código sem fornecer resultados abordados.

* O cartão de ambiente não exibia consistentemente o botão **Adicionar**.

## Ferramentas de refatoração de código {#code-refactoring-tools}

### Novidades em [!DNL Code Refactoring Tools] {#what-is-new-crt}

* Nova versão do plug-in AIO-CLI lançada. A versão mais recente deste plug-in inclui correções de erros para o Conversor do Dispatcher AEM e o Repository Modernizer, além de oferecer suporte a um novo utilitário - Conversor de índice. Consulte [Unified Experience](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/unified-experience.html?lang=en#benefits) para saber mais sobre esse plug-in.

* O Conversor de Índice é um utilitário que pode ser usado para transformar as Definições de Índice OAK Personalizado de um cliente em AEM como Definições de Índice OAK compatíveis com Cloud Service. Consulte [Index Converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/index-converter) para obter mais detalhes.

* Novo recurso adicionado ao [Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer) que cria um pacote separado `ui.config` para conter todas as configurações de OSGi.

### Correções de erros {#crt-bug-fixes}

* Várias correções de erros feitas nas ferramentas AEM Dispatcher Converter e Repository Modernizer. Consulte [AEM Dispatcher Converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter) e [Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer).

### Data de lançamento {#release-date-ctt}

A Data de lançamento da ferramenta Transferência de conteúdo v1.1.20 é 8 de janeiro de 2021.

### Novidades em [!DNL Content Transfer Tool] {#what-is-new-ctt}

* Os usuários agora podem saber se o Token de acesso expirou passando o mouse sobre o ícone de status na interface do usuário da Ferramenta de transferência de conteúdo (CTT). Eles também serão notificados na interface do usuário de Detalhes do conjunto de migração de que não conseguem se conectar à instância do Cloud Service.

### Correções de erros {#ctt-bug-fixes}

* O status da interface do usuário da Ferramenta de transferência de conteúdo (CTT) para um conjunto de migração não persistiu e foi alterado após um período de inatividade. Isso foi corrigido.
* A opção para exibir logs estava desativada se os logs não estavam disponíveis. Isso foi corrigido e as mensagens foram adicionadas para notificar o usuário por que os logs estão ausentes.
* O status da interface do usuário da Ferramenta de transferência de conteúdo mostrava *FALHA* quando o usuário parava uma assimilação. Isso foi corrigido para exibir *STOPPED*.
