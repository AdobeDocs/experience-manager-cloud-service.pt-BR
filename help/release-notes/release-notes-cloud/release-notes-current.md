---
title: Notas de versão atuais do  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Notas de versão atuais do  [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
mini-toc-levels: 1
source-git-commit: 75621ba378d59bd36146b15995823c43c458d349
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 20%

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

A data de lançamento do [!DNL Adobe Experience Manager] como [!DNL Cloud Service] versão atual (2022.6.0) é 30 de junho de 2022.

A próxima versão (2022.7.0) está planejada para 8 de agosto de 2022.

## Vídeo da versão {#release-video}

Assista ao vídeo Visão geral da versão de junho de 2022 para ver um resumo dos recursos adicionados na versão 2022.6.0:

>[!VIDEO](https://video.tv.adobe.com/v/344308/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Novos recursos no [!DNL Sites] {#sites-features}

* Um novo [interface do usuário](/help/sites-cloud/administering/content-fragments/content-fragments-console.md) O agora está disponível para administradores de conteúdo e autores de conteúdo gerenciarem com eficiência (realizar ações como publicar, cancelar a publicação, copiar, mover etc.), pesquisar/filtrar e criar fragmentos de conteúdo para casos de uso sem cabeçalho.

   ![Console do fragmento do conteúdo](/help/release-notes/assets/cf-ui.png)

* O novo [Componente Índice](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/tableofcontents.html) O funciona não apenas com os Componentes principais, mas com todos os componentes, renderizando automaticamente ToCs nas páginas de conteúdo. E como ele é renderizado no lado do servidor e totalmente armazenado em cache pelo dispatcher, também é eficiente carregar.

## [!DNL Experience Manager Assets] como [!DNL Cloud Service] {#assets}

### Novos recursos no [!DNL Assets] {#assets-features}

O Experience Manager Assets usa os recursos da Adobe Sensei AI para agora [distinguir entre cores em uma imagem e aplicá-las automaticamente como tags na assimilação](../../assets/color-tag-images.md). Essas tags permitem uma experiência de pesquisa aprimorada, com base na composição de cores da imagem. Você pode configurar o número de cores, dentro de um intervalo de uma a quarenta, que são marcadas em uma imagem, para que possa pesquisar por imagens com base nessas cores posteriormente.

## [!DNL Experience Manager Forms] como [!DNL Cloud Service] {#forms}

### Novos recursos no [!DNL Forms] {#forms-features}

* **[Integrar o Adaptive Forms com o Microsoft® Power Automate](/help/forms/forms-microsoft-power-automate-integration.md)**: Agora é possível configurar um Formulário adaptável para executar um fluxo da Microsoft® Power Automate Cloud no envio. O formulário adaptável configurado envia dados capturados, anexos e documentos de registro para o Power Automate Cloud Flow para processamento. Ele ajuda você a criar uma experiência personalizada de captura de dados, aproveitando o poder do Microsoft® Power Automate para criar lógicas comerciais sobre dados capturados e automatizar os fluxos de trabalho do cliente.

* **Assistente para criar um formulário adaptável**: Você pode usar o assistente empresarial para criar rapidamente o Adaptive Forms. O assistente fornece uma navegação de guia rápida para selecionar facilmente o modelo pré-configurado, o estilo, os campos e as opções de envio para criar um formulário adaptável.

   ![Assistente para criar um formulário adaptável](/help/release-notes/assets/wizard.png)

## Complemento CIF {#cloud-services-cif}

### Novidades {#what-is-new-cif}

* Nova página de propriedades do cockpit de produtos para obter uma visão geral melhor e simplificada

![visão geral das propriedades do cockpit de produtos](/help/assets/CIF/product_cockpit_properties_overview.png)

* Aprimoramento da compatibilidade e robustez de conectores de terceiros na I/O Runtime

* Suporte aprimorado para substituições de configuração de cliente GQL (por exemplo, definir o comportamento de armazenamento em cache personalizado)

* Vários endpoints de comércio agora são compatíveis prontos e podem ser configurados por meio do Cloud Manager. Você pode encontrar detalhes no blog da CIF [here](https://medium.com/adobetech/use-aem-as-a-cloud-service-with-multiple-adobe-commerce-systems-9295612a9554).


### Correções de bugs {#bug-fixes-cif}

* O campo seletor de produtos de vários valores mostra o 2º e os produtos adicionais como inválidos

* Ocasionalmente, o Seletor de produto fica oculto atrás dos componentes

## Complemento de Demonstrações de Referência {#cloud-services-demos}

### Novidades {#what-is-new-demos}

* Novo modelo de conteúdo e comércio WKND que estende a WKND a uma experiência de compra E2E com catálogo de produtos, carrinho de compras, check-out e myAccount. Esse modelo usa a CIF e os Componentes principais da CIF, portanto, é necessário instalar o complemento CIF. Você pode encontrar detalhes no blog da CIF [here](https://medium.com/adobetech/learn-how-to-create-a-shoppable-experience-with-the-new-wknd-reference-site-and-cif-b3b2c161f67e).

![Loja WKND](/help/assets/CIF/wknd_shop.png)

![pdp WKND](/help/assets/CIF/wknd_pdp.png)

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Novidades {#what-is-new-foundation}

* Conforme mencionado nas notas de versão de maio (2022.5.0), a opção &quot;Adicionar árvore&quot; na tela do administrador do agente de replicação **Distribuir** foi removida. Os pacotes com uma hierarquia de árvore de conteúdo devem ser replicados usando [Gerenciar publicação](/help/operations/replication.md#manage-publication) ou [Publicar árvore de conteúdo](/help/operations/replication.md#manage-publication#publish-content-tree-workflow) fluxo de trabalho.

## Cloud Manager {#cloud-manager}

Você pode encontrar uma lista completa de versões mensais do Cloud Manager [aqui](/help/implementing/cloud-manager/release-notes-cloud-manager/release-notes-cm-current.md).

## Ferramentas de migração {#migration-tools}

Você pode encontrar uma lista completa das versões das Ferramentas de migração [here](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
