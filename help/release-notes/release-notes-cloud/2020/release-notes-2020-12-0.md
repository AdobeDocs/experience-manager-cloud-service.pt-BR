---
title: Notas de versão do  [!DNL Adobe Experience Manager]  as a Cloud Service 2020.12.0.
description: Notas de versão do  [!DNL Adobe Experience Manager]  as a Cloud Service 2020.12.0.
exl-id: 16875180-1f23-477d-9d4d-e220998c4983
feature: Release Information
role: Admin
source-git-commit: 64344b9b2cce8d7c7f05d3e5ba94049346308a9d
workflow-type: tm+mt
source-wordcount: '657'
ht-degree: 9%

---

# Notas de versão para [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

A seção a seguir descreve as Notas de Versão gerais para [!DNL Experience Manager] as a Cloud Service.

## Data de lançamento {#release-date}

A Data de Lançamento do [!DNL Adobe Experience Manager] as a Cloud Service 2020.12.0 é 17 de dezembro de 2020.
A versão seguinte (2021.1.0) é 28 de janeiro de 2021.

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

* **[API HTTP de fragmento de conteúdo](/help/assets/content-fragments/assets-api-content-fragments.md)**: adicione a capacidade de adicionar/atualizar e excluir variações de Fragmento de conteúdo usando a API HTTP.

## [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

* A integração com [!DNL Adobe InDesign Server] agora está disponível para [!DNL Experience Manager] as a [!DNL Cloud Service]. Ela fornece automação para processar arquivos [!DNL Adobe InDesign] usando scripts [!DNL Adobe InDesign Server] e permite que os usuários usem a interface de usuário de modelos [!DNL Assets] para criar folhetos ou anúncios. Somente [!DNL InDesign Server] hospedado por [!DNL Adobe Managed Services] tem suporte para [!DNL Experience Manager as a Cloud Service]. <!-- TBD: Add link to article. -->

* O [!DNL Experience Manager] é aprimorado para rastrear e exibir referências de ativos quando um ativo é usado em uma implantação remota do [!DNL Experience Manager Sites] usando a funcionalidade Connected Assets. Uma nova guia [!UICONTROL Referências] na página [!UICONTROL Propriedades] do ativo agora lista referências locais e remotas do ativo. As referências permitem que os usuários do DAM rastreiem a utilização de ativos em [!DNL Sites] páginas e em ativos compostos em [!DNL Assets]. Consulte [configurar e usar o Connected Assets](/help/assets/use-assets-across-connected-assets-instances.md).

* Os recursos do [!DNL Dynamic Media] agora podem ser acessados por meio dos Componentes principais baseados em imagem do AEM [!DNL Sites]. Os autores podem configurar rapidamente os componentes para usar Predefinições de imagem, Recorte inteligente e Modificadores de imagem ao criar páginas da Web. Consulte [Versão dos Componentes Principais 2.13.0](https://github.com/adobe/aem-core-wcm-components/releases/tag/core.wcm.components.reactor-2.13.0).

* O aplicativo de desktop [!DNL Experience Manager] permite que os usuários façam o upload de arquivos e pastas arrastando os arquivos do Windows Explorer ou do Mac Finder na interface do aplicativo de desktop. Consulte [adicionar ativos usando o aplicativo de desktop](https://experienceleague.adobe.com/en/docs/experience-manager-desktop-app/using/using#upload-and-add-new-assets-to-aem).

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novidades {#what-is-new-commerce}

* Lançamento do site de referência CIF Venia - 2020.12.01 que inclui a versão mais recente dos componentes principais CIF v1.6.0. Consulte [Site de referência de CIF Venia](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2020.12.01) para obter mais detalhes.

* Lançamento de componentes principais de CIF v1.6.0. Consulte [Componentes principais do CIF](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.6.0) para obter mais detalhes.

## Cloud Manager {#cloud-manager}

### Data de lançamento {#release-date-cm}

A data de lançamento do Cloud Manager no Adobe Experience Manager (AEM as a Cloud Service) 2020.12.0 é 10 de dezembro de 2020.

### Novidades do [!DNL Cloud Manager] {#what-is-new-cm}

* Gerenciamento por autoatendimento de [Certificados SSL](/help/implementing/cloud-manager/managing-ssl-certifications/introduction-to-ssl-certificates.md) e [Introdução a Nomes de Domínio Personalizados](/help/implementing/cloud-manager/custom-domain-names/introduction.md).

* Gerenciamento por autoatendimento de [listas de permissão de IP](/help/implementing/cloud-manager/ip-allow-lists/introduction.md).

* A página de detalhes atualizada do **Ambiente** agora permite que os usuários gerenciem Nomes de domínio personalizados e Listas de permissões de IP em seus ambientes.

### Correções de erros {#bug-fixes-cloud-manager}

* Algumas ocorrências de falhas na fase de verificação de código sem fornecer resultados são abordadas.

* O cartão de Ambiente não exibia de maneira consistente o botão **Adicionar**.

## Ferramentas de refatoração de código {#code-refactoring-tools}

### Novidades do [!DNL Code Refactoring Tools] {#what-is-new-crt}

* Nova versão do plug-in AIO-CLI lançada. A versão mais recente deste plug-in inclui correções de erros para o AEM Dispatcher Converter e o Repository Modernizer, além de oferecer suporte a um novo utilitário: Conversor de índice. Consulte [Experiência unificada](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/migration-journey/refactoring-tools/unified-experience#benefits), onde você pode saber mais sobre este plug-in.

* O Conversor de índice é um utilitário que pode ser usado para transformar as Definições de índice Oak personalizadas de um cliente em Definições de índice Oak compatíveis com AEM as a Cloud Service. Consulte [Conversor de Índice](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/index-converter) para obter mais detalhes.

* Novo recurso adicionado ao [Modernizador de repositório](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer) que cria um pacote separado `ui.config` para conter todas as configurações OSGi.

### Correções de erros {#crt-bug-fixes}

* Várias correções de bugs foram feitas nas ferramentas AEM Dispatcher Converter e Repository Modernizer. Consulte [Conversor de Dispatcher do AEM](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter) e [Modernizador de repositório](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer).

### Data de lançamento {#release-date-ctt}

A data de lançamento da ferramenta de Transferência de conteúdo v1.1.20 é 8 de janeiro de 2021.

### Novidades do [!DNL Content Transfer Tool] {#what-is-new-ctt}

* Agora os usuários podem saber se o token de acesso expirou, passando o mouse sobre o ícone de status na interface do usuário da Ferramenta de transferência de conteúdo (CTT). Eles também são notificados na interface do usuário Detalhes do conjunto de migração de que não conseguem se conectar à instância do Cloud Service.

### Correções de erros {#ctt-bug-fixes}

* O status da interface do usuário da Ferramenta de transferência de conteúdo (CTT) de um conjunto de migração não persistiu e foi alterado após um período de inatividade. Esse problema foi corrigido.
* A opção para visualizar logs estava desativada se os logs não estivessem disponíveis. Esse problema foi corrigido e agora as mensagens são adicionadas para notificar os usuários sobre os registros que estão ausentes.
* O status da interface do usuário da Ferramenta de transferência de conteúdo mostrava *FALHA* quando o usuário interrompeu uma assimilação. Esse problema foi corrigido para exibir *PARADO*.
