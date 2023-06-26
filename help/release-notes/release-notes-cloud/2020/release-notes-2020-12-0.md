---
title: Notas de versão do [!DNL Adobe Experience Manager]  as a Cloud Service 2020.12.0.
description: Notas de versão do [!DNL Adobe Experience Manager]  as a Cloud Service 2020.12.0.
exl-id: 16875180-1f23-477d-9d4d-e220998c4983
source-git-commit: f0e9fe0bdf35cc001860974be1fa2a7d90f7a3a9
workflow-type: tm+mt
source-wordcount: '691'
ht-degree: 18%

---

# Notas de versão do [!DNL Adobe Experience Manager] as a Cloud Service  {#release-notes}

A seção a seguir descreve as Notas de versão gerais do [!DNL Experience Manager] as a Cloud Service.

## Data de lançamento {#release-date}

A data de lançamento do [!DNL Adobe Experience Manager] O as a Cloud Service 2020.12.0 é 17 de dezembro de 2020.
A versão seguinte (2021.1.0) será lançada em 28 de janeiro de 2021.

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

* **[API HTTP do fragmento de conteúdo](/help/assets/content-fragments/assets-api-content-fragments.md)**: adicione a capacidade de adicionar/atualizar e excluir variações de Fragmento de conteúdo usando a API HTTP.

## [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

* Integração com [!DNL Adobe InDesign Server] agora está disponível para [!DNL Experience Manager] as a [!DNL Cloud Service]. Ele fornece automação para processamento [!DNL Adobe InDesign] arquivos usando [!DNL Adobe InDesign Server] script e permite que os usuários usem [!DNL Assets] interface de modelos para criar folhetos ou anúncios. Somente [!DNL InDesign Server] hospedado por [!DNL Adobe Managed Services] é compatível com [!DNL Experience Manager as a Cloud Service]. <!-- TBD: Add link to article. -->

* [!DNL Experience Manager] O é aprimorado para rastrear e exibir referências de ativos quando um ativo é usado em um local remoto [!DNL Experience Manager Sites] implantação usando a funcionalidade Connected Assets. Um novo [!UICONTROL Referências] no do ativo [!UICONTROL Propriedades] A página agora lista referências locais e remotas do ativo. As referências permitem que os usuários do DAM rastreiem a utilização dos ativos no [!DNL Sites] páginas e em ativos compostos no [!DNL Assets]. Consulte [configurar e usar Connected Assets](/help/assets/use-assets-across-connected-assets-instances.md).

* [!DNL Dynamic Media] Os recursos do agora estão acessíveis por meio de [!DNL Sites] Componentes principais baseados em imagem. Os autores podem configurar rapidamente os componentes para usar Predefinições de imagem, Recorte inteligente e Modificadores de imagem ao criar páginas da Web. Consulte [Versão 2.13.0 dos Componentes principais](https://github.com/adobe/aem-core-wcm-components/releases/tag/core.wcm.components.reactor-2.13.0).

* [!DNL Experience Manager] O aplicativo de desktop permite que os usuários façam o upload de arquivos e pastas arrastando os arquivos do Windows Explorer ou do Mac Finder na interface do aplicativo de desktop. Consulte [adicionar ativos usando o aplicativo de desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#upload-and-add-new-assets-to-aem).

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novidades {#what-is-new-commerce}

* Lançamento do site de referência CIF Venia em 2020.12.01 que inclui a versão mais recente dos componentes principais CIF v1.6.0. Consulte [Site de referência CIF Venia](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2020.12.01) para obter mais detalhes.

* Lançamento de componentes principais CIF v1.6.0. Consulte [Componentes principais da CIF](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.6.0) para obter mais detalhes.

## Cloud Manager {#cloud-manager}

### Data de lançamento {#release-date-cm}

A data de lançamento do Cloud Manager no AEM as a Cloud Service 2020.12.0 é 10 de dezembro de 2020.

### Novidades do [!DNL Cloud Manager] {#what-is-new-cm}

* Gerenciamento de autoatendimento do [Certificados SSL](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md) e [Nomes de domínio personalizados](/help/implementing/cloud-manager/custom-domain-names/introduction.md).

* Gerenciamento de autoatendimento do [LISTAS DE PERMISSÕES IP](/help/implementing/cloud-manager/ip-allow-lists/introduction.md).

* A página de detalhes atualizada do **Ambiente** agora permite que os usuários gerenciem Nomes de domínio personalizados e Listas de permissões de IP em seus ambientes.

### Correções de erros {#bug-fixes-cloud-manager}

* Algumas ocorrências de falhas na fase de verificação do código sem fornecer os resultados abordados.

* O cartão de Ambiente não exibia de maneira consistente o botão **Adicionar**.

## Ferramentas de refatoração de código {#code-refactoring-tools}

### Novidades do [!DNL Code Refactoring Tools] {#what-is-new-crt}

* Nova versão do plug-in AIO-CLI lançada. A versão mais recente deste plug-in inclui correções de erros para o AEM Dispatcher Converter e o Repository Modernizer, além de oferecer suporte a um novo utilitário: Conversor de índice. Consulte [Experiência unificada](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/unified-experience.html?lang=en#benefits) para saber mais sobre este plug-in.

* O Conversor de índice é um utilitário que pode ser usado para transformar as Definições de índice OAK personalizado de um cliente em Definições de índice OAK compatíveis com AEM as a Cloud Service. Consulte [Conversor de índice](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/index-converter) para obter mais detalhes.

* Novo recurso adicionado a [Modernizador de repositório](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer) que cria um pacote separado `ui.config` para conter todas as configurações de OSGi.

### Correções de erros {#crt-bug-fixes}

* Várias correções de erros feitas nas ferramentas Conversor do Dispatcher do AEM e Modernizador do repositório. Consulte [Conversor do Dispatcher do AEM](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter) e [Modernizador de repositório](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer).

### Data de lançamento {#release-date-ctt}

A data de lançamento da ferramenta de Transferência de conteúdo v1.1.20 é 8 de janeiro de 2021.

### Novidades do [!DNL Content Transfer Tool] {#what-is-new-ctt}

* Agora os usuários podem saber se o token de acesso expirou, passando o mouse sobre o ícone de status na interface do usuário da Ferramenta de transferência de conteúdo (CTT). Eles também serão notificados na interface do usuário Detalhes do conjunto de migração de que não conseguem se conectar à instância do Cloud Service.

### Correções de erros {#ctt-bug-fixes}

* O status da interface do usuário da Ferramenta de transferência de conteúdo (CTT) de um conjunto de migração não persistiu e foi alterado após um período de inatividade. Isso foi corrigido.
* A opção para visualizar logs estava desativada se os logs não estivessem disponíveis. Isso foi corrigido e mensagens foram adicionadas para notificar o usuário sobre os logs ausentes.
* O status da interface do usuário da Ferramenta de transferência de conteúdo foi mostrado *FALHA* quando o usuário interrompeu uma assimilação. Isso foi corrigido para ser exibido *PARADO* em vez disso.
