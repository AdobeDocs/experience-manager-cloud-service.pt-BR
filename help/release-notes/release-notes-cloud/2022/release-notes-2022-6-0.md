---
title: Notas de versão do  [!DNL Adobe Experience Manager]  as a Cloud Service 2022.6.0.
description: Notas de versão do  [!DNL Adobe Experience Manager]  as a Cloud Service 2022.6.0.
exl-id: cf2133dc-56cd-4a07-ab11-72e16f015ff5
feature: Release Information
role: Admin
source-git-commit: 281a8efcd18920dd926d92db9c757c0513d599fd
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 75%

---

# Notas de versão do [!DNL Adobe Experience Manager] as a Cloud Service 2022.6.0 {#release-notes}

A seção a seguir descreve as Notas de versão do recurso para a versão 2022.6.0 do as a Cloud Service [!DNL Experience Manager].

>[!NOTE]
>
>A partir daqui, você pode navegar até as notas de versão das versões anteriores; por exemplo, para aquelas em 2020, 2021 e assim por diante.

>[!NOTE]
>
>Consulte [Atualizações recentes na documentação](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=pt-BR) para obter detalhes de atualizações de documentação não relacionadas diretamente a uma versão.

## Data de lançamento {#release-date}

A data de lançamento da versão atual (2022.6.0) do [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] é 30 de junho de 2022.

A próxima versão (2022.7.0) está planejada para 8 de agosto de 2022.

## Vídeo da versão {#release-video}

Assista ao vídeo de Visão geral da versão de junho de 2022 para ver um resumo dos recursos adicionados na versão 2022.6.0:

>[!VIDEO](https://video.tv.adobe.com/v/344308/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Novos recursos no [!DNL Sites] {#sites-features}

* Uma nova [interface de usuário](/help/sites-cloud/administering/content-fragments/managing.md#content-fragments-console) está disponível para que administradores e autores de conteúdo possam gerenciar (como publicar, desfazer a publicação, copiar, mover etc.), pesquisar/filtrar e criar fragmentos de conteúdo com eficiência para casos de uso Headless.

  ![Console de fragmentos de conteúdo](/help/release-notes/assets/cf-ui.png)

* O novo [Componente de índice](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/tableofcontents.html?lang=pt-BR) funciona não apenas com os Componentes principais, mas com todos os componentes, renderizando índices automaticamente nas páginas de conteúdo. E como ele é renderizado no lado do servidor e totalmente armazenado em cache pelo Dispatcher, seu carregamento também é eficiente.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Novos recursos no [!DNL Assets] {#assets-features}

Agora, o Experience Manager Assets usa os recursos de IA do Adobe para [distinguir cores em uma imagem e aplicá-las automaticamente como marcas na assimilação](/help/assets/color-tag-images.md). Essas tags permitem uma experiência de pesquisa aprimorada, com base na composição de cores da imagem. Você pode configurar o número de cores, dentro de um intervalo de um a 40, que são marcados em uma imagem para que você possa pesquisar imagens com base nessas cores posteriormente.

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Novos recursos no [!DNL Forms] {#forms-features}

* **[Integrar formulários adaptáveis com o Microsoft® Power Automate](/help/forms/forms-microsoft-power-automate-integration.md)**: agora é possível configurar um formulário adaptável para executar um fluxo da nuvem do Microsoft® Power Automate no envio. O formulário adaptável configurado envia dados capturados, anexos e documentos de registro para processamento no fluxo da nuvem do Power Automate. Ele ajuda você a criar uma experiência personalizada de captura de dados, aproveitando o poder do Microsoft® Power Automate para criar lógicas de negócios sobre dados capturados e automatizar os fluxos de trabalho do cliente.

* **Assistente para criar um formulário adaptável**: você pode usar o assistente empresarial para criar formulários adaptáveis rapidamente. O assistente fornece uma navegação rápida por guias para selecionar facilmente o modelo pré-configurado, o estilo, os campos e as opções de envio para criar um formulário adaptável.

  ![Assistente para criar um formulário adaptável](/help/release-notes/assets/wizard.png)

## Complemento CIF {#cloud-services-cif}

### Novidades {#what-is-new-cif}

* Nova página de propriedades do cockpit do produto para obter uma visão geral melhor e simplificada

![visão geral das propriedades do cockpit do produto](/help/assets/CIF/product_cockpit_properties_overview.png)

* Aprimoramento da compatibilidade e robustez de conectores de terceiros no I/O Runtime

* Aprimoramento do suporte para substituições de configuração de cliente GQL (por exemplo, definir comportamento de armazenamento em cache personalizado)

* Agora, vários pontos de acesso de comércio são nativamente compatíveis e podem ser configurados por meio do Cloud Manager. Você pode encontrar detalhes no blog da CIF [aqui](https://medium.com/adobetech/use-aem-as-a-cloud-service-with-multiple-adobe-commerce-systems-9295612a9554).


### Correções de erros {#bug-fixes-cif}

* O campo seletor de produtos de vários valores mostra o 2º produto e os demais produtos como inválidos

* Ocasionalmente, o seletor de produto fica oculto atrás dos componentes

## Complemento de demonstrações de referência {#cloud-services-demos}

### Novidades {#what-is-new-demos}

* Novo modelo de conteúdo e comércio do WKND, que estende o WKND por meio de uma experiência de compra E2E com catálogo de produtos, carrinho de compras, check-out e conta pessoal. Esse modelo usa a CIF e os Componentes principais da CIF. Portanto, é necessário instalar o complemento CIF. Você pode encontrar detalhes no blog da CIF [aqui](https://medium.com/adobetech/learn-how-to-create-a-shoppable-experience-with-the-new-wknd-reference-site-and-cif-b3b2c161f67e).

![Loja WKND](/help/assets/CIF/wknd_shop.png)

![WKND pdp](/help/assets/CIF/wknd_pdp.png)

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Novidades {#what-is-new-foundation}

* Conforme mencionado nas notas de versão de maio (2022.5.0), a opção &quot;Adicionar árvore&quot;, na guia **Distribuir** da tela do administrador do agente de replicação, foi removida. Os pacotes com uma hierarquia de árvore de conteúdo devem ser replicados usando o fluxo de trabalho [Gerenciar publicação](/help/operations/replication.md#manage-publication) ou [Publicar árvore de conteúdo](/help/operations/replication.md#manage-publication#publish-content-tree-workflow).

## Cloud Manager {#cloud-manager}

Você pode encontrar uma lista completa de versões mensais do Cloud Manager [aqui](/help/implementing/cloud-manager/release-notes/current.md).

## Ferramentas de migração {#migration-tools}

Você pode encontrar uma lista completa de versões das ferramentas de migração [aqui](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
