---
title: Notas de versão do  [!DNL Adobe Experience Manager]  as a Cloud Service 2022.5.0.
description: Notas de versão do  [!DNL Adobe Experience Manager]  as a Cloud Service 2022.5.0.
exl-id: 1b867582-e34c-435b-b8f8-fc71dddcaccb
feature: Release Information
role: Admin
source-git-commit: 281a8efcd18920dd926d92db9c757c0513d599fd
workflow-type: tm+mt
source-wordcount: '799'
ht-degree: 64%

---

# Notas de versão do [!DNL Adobe Experience Manager] as a Cloud Service 2022.5.0 {#release-notes}

A seção a seguir descreve as Notas de versão do recurso para a versão 2022.5.0 do as a Cloud Service [!DNL Experience Manager].

>[!NOTE]
>
>A partir daqui, você pode navegar até as notas de versão das versões anteriores; por exemplo, para aquelas em 2020, 2021 e assim por diante.

>[!NOTE]
>
>Consulte [Atualizações recentes na documentação](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=pt-BR) para obter detalhes de atualizações de documentação não relacionadas diretamente a uma versão.

## Data de lançamento {#release-date}

A data de lançamento da versão atual (2022.5.0) do [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] é 9 de junho de 2022.
A próxima versão (2022.6.0) está planejada para 30 de junho de 2022.

## Vídeo da versão {#release-video}

Assista ao vídeo de visão geral da versão de maio de 2022, que exibe um resumo dos recursos adicionados na versão 2022.5.0:

>[!VIDEO](https://video.tv.adobe.com/v/343321/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Novos recursos disponíveis no canal de pré-lançamento do [!DNL Sites] {#prerelease-features-sites}

* Várias funcionalidades do GraphQL
* Um [novo console](/help/sites-cloud/administering/content-fragments/managing.md#content-fragments-console) otimizado para uso headless dos fragmentos de conteúdo

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Novos recursos no [!DNL Assets] {#assets-features}

* O recurso [Imagem inteligente do Dynamic Media](https://medium.com/adobetech/one-solution-fits-all-smart-imaging-with-aem-dynamic-media-be690b62df9f) agora é compatível com o formato de arquivo AVIF — melhore ainda mais o Google Core Web Vital (maior renderização de conteúdo) com o AVIF, que fornece 20% de redução de tamanho em relação ao WebP. No total, o AVIF fornece uma redução média de até 41% no tamanho do JPEG (em algumas imagens, esse valor pode chegar a 76%).

* O [!UICONTROL Experience Manager Assets Brand Portal] agora executa trabalhos automáticos a cada 12 horas para excluir todos os ativos do Brand Portal publicados no AEM. Como resultado, não é necessário excluir manualmente os ativos na pasta Contribuição para manter o tamanho da pasta abaixo do limite. Consulte [Novidades no Experience Manager Assets Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/whats-new.html?lang=pt-BR).

### Novos recursos disponíveis no canal de pré-lançamento do [!DNL Assets] {#prerelease-features-assets}

Agora, o Experience Manager Assets usa os recursos de IA do Adobe para [distinguir cores em uma imagem e aplicá-las automaticamente como marcas na assimilação](/help/assets/color-tag-images.md). Essas tags permitem uma experiência de pesquisa aprimorada, com base na composição de cores da imagem. Você pode configurar o número de cores, dentro de um intervalo de um a 40, que são marcados em uma imagem para que você possa pesquisar imagens com base nessas cores posteriormente.


## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Novos recursos disponíveis no canal de pré-lançamento do [!DNL Forms] {#prerelease-features-forms}

* **Integrar formulários adaptáveis com o Microsoft® Power Automate**: agora é possível configurar um formulário adaptável para executar um fluxo da nuvem do Microsoft® Power Automate no envio. O formulário adaptável configurado envia dados capturados, anexos e documentos de registro para processamento no fluxo da nuvem do Power Automate. Ele ajuda você a criar uma experiência personalizada de captura de dados, aproveitando o poder do Microsoft® Power Automate para criar lógicas de negócios sobre dados capturados e automatizar os fluxos de trabalho do cliente.

* **Assistente para criar um Formulário Adaptável**: você pode usar o assistente empresarial para criar rapidamente o Forms Adaptável. O assistente fornece uma navegação rápida por guias para selecionar facilmente o modelo pré-configurado, o estilo, os campos e as opções de envio para criar um formulário adaptável.

  ![Assistente para criar um formulário adaptável](/help/release-notes/assets/wizard.png)

## Complemento CIF {#cloud-services-cif}

### Novidades {#what-is-new-cif}

* Acesso rápido ao cockpit de produtos: acesse facilmente as informações completas e detalhadas do produto com um clique no Editor de sites

<!-- Image was not found during PR validation despite correct path   ![Enable wantlist](/help/assets/CIF/enable-wishlist.png) -->

* Suporte para componentes adicionais de comércio de marketing: os componentes podem ser configurados para mostrar um call-to-action de lista de desejos e de adição ao carrinho

  ![Atalho do Editor de sites para o cockpit de produtos](/help/assets/CIF/sites-editor-shortcut-to-cockpit.png)


## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Novidades {#what-is-new-foundation}

* A opção &quot;Adicionar árvore&quot;, na **guia Distribuir** da tela de administrador do agente de replicação, que foi anunciada anteriormente como obsoleta, foi removida em 20 de junho de 2022 ou logo após essa data. Os pacotes com uma hierarquia de árvore de conteúdo devem ser replicados usando [Gerenciar publicação](/help/operations/replication.md#manage-publication) ou o [Fluxo de trabalho de publicação da árvore de conteúdo](/help/operations/replication.md#publish-content-tree-workflow).

* O uso da tela de administrador do agente de replicação ou da API de replicação para distribuir pacotes de conteúdo maiores que 10 MB (nós com propriedades, sem incluir binários) foi descontinuado e aplicado em 12 de setembro de 2022 ou logo em seguida. Em vez disso, [Gerenciar publicação](/help/operations/replication.md#manage-publication) ou o [Fluxo de trabalho de publicação da árvore de conteúdo](/help/operations/replication.md#publish-content-tree-workflow) deve ser usado para replicar esses pacotes de conteúdo grandes. Em julho, uma mensagem de aviso será exibida na **guia Distribuir** da tela do administrador do agente de replicação ao tentar replicar esses pacotes de conteúdo grandes e também no log de erros do AEM sempre que a API de replicação for usada para replicar esses pacotes de conteúdo grandes. Em setembro, os avisos foram substituídos por erros. Ajuste seus processos de acordo.

### Novos recursos disponíveis no canal de pré-lançamento do [!DNL Experience Manager] {#prerelease-features-foundation}

* O AEM as a Cloud Service agora está integrado ao shell unificado para melhorar a experiência do usuário e unificá-la com todos os outros aplicativos da Experience Cloud. Consulte [AEM as a Cloud Service no Unified Shell](/help/overview/aem-cloud-service-on-unified-shell.md) para obter mais detalhes.

## Segurança do [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation-security}

### Descontinuidade do TLS 1.0 e 1.1

A partir de 30 de junho de 2022, o Experience Manager as a Cloud Service exigirá uma comunicação de rede e troca de dados com os sistemas dos usuários mais seguras. O AEM usará exclusivamente o protocolo TLS (Transport Layer Security) 1.2. As versões anteriores do TLS (1.0 e 1.1) foram descontinuadas.

Se você continuar a usar versões mais antigas do TLS (como 1.0 e 1.1), poderá perder o acesso ao Experience Manager as a Cloud Service.

## Cloud Manager {#cloud-manager}

Você pode encontrar uma lista completa de versões mensais do Cloud Manager [aqui](/help/implementing/cloud-manager/release-notes/current.md).

## Ferramentas de migração {#migration-tools}

Você pode encontrar uma lista completa de versões das ferramentas de migração [aqui](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
