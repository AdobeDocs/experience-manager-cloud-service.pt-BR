---
title: Notas de versão do [!DNL Adobe Experience Manager] as a Cloud Service 2022.5.0.
description: Notas de versão do [!DNL Adobe Experience Manager] as a Cloud Service 2022.5.0.
source-git-commit: 9c76ff2e0b789894ef5492ee940ce79cddb47e11
workflow-type: tm+mt
source-wordcount: '805'
ht-degree: 16%

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

A data de lançamento do [!DNL Adobe Experience Manager] como [!DNL Cloud Service] versão atual (2022.5.0) é 9 de junho de 2022.
A próxima versão (2022.6.0) está planejada para 30 de junho de 2022.

## Vídeo da versão {#release-video}

Assista ao vídeo Visão geral da versão de maio de 2022 para obter um resumo dos recursos adicionados na versão 2022.5.0:

>[!VIDEO](https://video.tv.adobe.com/v/343321/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Novos recursos disponíveis no canal de pré-lançamento do [!DNL Sites] {#prerelease-features-sites}

* Várias funcionalidades GraphQL
* A [novo console](/help/headless/content-fragments/content-fragment-console.md) otimizado para uso sem cabeçalho dos fragmentos de conteúdo

## [!DNL Experience Manager Assets] como [!DNL Cloud Service] {#assets}

### Novos recursos no [!DNL Assets] {#assets-features}

* [Imagens inteligentes do Dynamic Media](https://medium.com/adobetech/one-solution-fits-all-smart-imaging-with-aem-dynamic-media-be690b62df9f) agora é compatível com o formato de arquivo AVIF - aprimore o Google Core Web Vital (Pintor de maior conteúdo), com o AVIF fornecendo 20% de redução extra do tamanho em relação ao WebP. No total, a AVIF fornece redução média de até 41% no tamanho do JPEG (em algumas imagens até 76%).

* [!UICONTROL Experience Manager Assets Brand Portal] O agora executa trabalhos automáticos a cada doze horas para excluir todos os ativos do Brand Portal publicados no AEM. Como resultado, não é necessário excluir os ativos na pasta Contribuição manualmente para manter o tamanho da pasta abaixo do limite. Consulte [Novidades no Experience Manager Assets Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/whats-new.html).

### Novos recursos disponíveis no canal de pré-lançamento do [!DNL Assets] {#prerelease-features-assets}

O Experience Manager Assets usa os recursos da Adobe Sensei AI para agora [distinguir entre cores em uma imagem e aplicá-las automaticamente como tags na assimilação](/help/assets/color-tag-images.md). Essas tags permitem uma experiência de pesquisa aprimorada, com base na composição de cores da imagem. Você pode configurar o número de cores, dentro de um intervalo de uma a quarenta, que são marcadas em uma imagem, para que possa pesquisar por imagens com base nessas cores posteriormente.


## [!DNL Experience Manager Forms] como [!DNL Cloud Service] {#forms}

### Novos recursos disponíveis no canal de pré-lançamento do [!DNL Forms] {#prerelease-features-forms}

* **Integrar o Adaptive Forms com o Microsoft® Power Automate**: Agora é possível configurar um Formulário adaptável para executar um fluxo da Microsoft® Power Automate Cloud no envio. O formulário adaptável configurado envia dados capturados, anexos e documentos de registro para o Power Automate Cloud Flow para processamento. Ele ajuda você a criar uma experiência personalizada de captura de dados, aproveitando o poder do Microsoft® Power Automate para criar lógicas comerciais sobre dados capturados e automatizar os fluxos de trabalho do cliente.

* **Assistente para criar um formulário adaptável**: Você pode usar o assistente empresarial para criar rapidamente o Adaptive Forms. O assistente fornece uma navegação de guia rápida para selecionar facilmente o modelo pré-configurado, o estilo, os campos e as opções de envio para criar um formulário adaptável.

   ![Assistente para criar um formulário adaptável](/help/release-notes/assets/wizard.png)

## Complemento CIF {#cloud-services-cif}

### Novidades {#what-is-new-cif}

* Acesso rápido ao cockpit de produtos: Acesse facilmente as informações completas e detalhadas do produto com um clique no Editor de sites

   ![Habilitar lista de desejos](/help/assets/CIF/enable-wishlist.png)

* Suporte para componentes adicionais de comércio de marketing: Os componentes podem ser configurados para mostrar uma chamada para ação de adição ao carrinho e de lista de desejos

   ![Atalho do editor de sites para o cockpit de produtos](/help/assets/CIF/sites-editor-shortcut-to-cockpit.png)


## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Novidades {#what-is-new-foundation}

* A opção &quot;Adicionar árvore&quot; na tela do administrador do agente de replicação **Guia Distribuir**, que foi anunciado anteriormente como obsoleto, será removido em 20 de junho de 2022 ou logo depois. Os pacotes com uma hierarquia de árvore de conteúdo devem ser replicados usando [Gerenciar publicação](/help/operations/replication.md#manage-publication) ou [Fluxo de trabalho da Árvore de conteúdo de publicação](/help/operations/replication.md#publish-content-tree-workflow).

* O uso da tela de administrador do agente de replicação ou da API de replicação para distribuir pacotes de conteúdo maiores que 10 MB (nós com propriedades, sem incluir binários) está obsoleto e será aplicado em 12 de setembro de 2022 ou logo em seguida. Em vez disso, [Gerenciar publicação](/help/operations/replication.md#manage-publication) ou [Fluxo de trabalho da Árvore de conteúdo de publicação](/help/operations/replication.md#publish-content-tree-workflow) deve ser usada para replicar esses pacotes de conteúdo grandes. Em julho, uma mensagem de aviso será exibida na tela do administrador do agente de replicação **Guia Distribuir** se estiver tentando replicar esses pacotes de conteúdo grandes e também no registro de erros de AEM sempre que a API de replicação for usada para replicar esses pacotes de conteúdo grandes. Em setembro, os avisos serão substituídos por erros. Ajuste seus processos de acordo.

### Novos recursos disponíveis no canal de pré-lançamento do [!DNL Experience Manager] {#prerelease-features-foundation}

* AEM as a Cloud Service agora está integrado ao Unified Shell para melhorar a experiência do usuário e unificá-la com todos os outros aplicativos do Experience Cloud. Consulte [AEM as a Cloud Service no shell unificado](/help/overview/aem-cloud-service-on-unified-shell.md) para obter mais detalhes.

## [!DNL Experience Manager] como [!DNL Cloud Service] Segurança da fundação {#foundation-security}

### Substituição de TLS 1.0, 1.1

A partir de 30 de junho de 2022, o Experience Manager as a Cloud Service exigirá uma comunicação de rede mais segura e troca de dados com os sistemas dos usuários. AEM usará exclusivamente o protocolo TLS (Transport Layer Security), 1.2. As versões anteriores do TLS 1.0 e 1.1 serão substituídas.

Se você continuar usando versões mais antigas do TLS como 1.0, 1.1, poderá perder o acesso ao Experience Manager as a Cloud Service.

## Cloud Manager {#cloud-manager}

Você pode encontrar uma lista completa de versões mensais do Cloud Manager [here](/help/implementing/cloud-manager/release-notes-cloud-manager/release-notes-cm-current.md).

## Ferramentas de migração {#migration-tools}

Você pode encontrar uma lista completa das versões das Ferramentas de migração [here](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
