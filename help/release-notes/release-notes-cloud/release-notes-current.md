---
title: Notas de versão atuais do  [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de versão atuais do  [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
mini-toc-levels: 1
source-git-commit: 9857376cb196b8aaa9fac64636727b5ad20a0360
workflow-type: tm+mt
source-wordcount: '617'
ht-degree: 30%

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

A data de lançamento do [!DNL Adobe Experience Manager] como [!DNL Cloud Service] a versão atual (2022.4.0) é 5 de maio de 2022.
A próxima versão (2022.5.0) está planejada para 26 de maio de 2022.

## Vídeo da versão {#release-video}

Dê uma olhada no [Visão geral da versão de abril de 2022](https://video.tv.adobe.com/v/342612?quality=12) vídeo para obter um resumo dos recursos adicionados na versão 2022.4.0.

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Novos recursos no [!DNL Sites] {#sites-features}

* Os tipos de dados do modelo de conteúdo agora podem ser definidos como [traduzível](/help/assets/content-fragments/content-fragments-models.md#properties) usar uma caixa de seleção simples no editor de modelo de conteúdo. Além disso, AEM regras e configurações de tradução são atualizadas automaticamente.

## [!DNL Experience Manager Assets] como [!DNL Cloud Service] {#assets}

### Novos recursos no [!DNL Assets] {#assets-features}

* Agora você pode [classificar tags](/help/assets/organize-assets.md#use-tags-to-organize-assets) na janela do seletor de tags em ordem crescente ou decrescente com base no nome da tag, data de criação ou data de modificação.

## [!DNL Experience Manager Forms] como [!DNL Cloud Service] {#forms}

### Novidades do [!DNL Forms] {#what-is-new-forms}

* **Comunicações - Suporte a APIs de manipulação de documentos no SDK as a Cloud Service do Forms**: [APIs de manipulação de documentos](/help/forms/aem-forms-cloud-service-communications.md) ajuda a combinar, reorganizar e validar documentos do PDF. Agora você pode usar as Comunicações - APIs de geração de documentos em um ambiente de desenvolvimento local com a ajuda do SDK as a Cloud Service da AEM Forms.

* **Usar XCI personalizado para gerar um documento de registro**[: agora você pode usar um arquivo XCI personalizado para definir várias propriedades de um documento de registro](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#use-a-custom-xci-file). Ele substitui o XCI principal pelas alterações personalizadas. Ele oferece mais controle sobre a geração de Documentos de registro, aumento da personalização e oportunidades de personalização.

* **Usar CAPTCHA invisível em um formulário adaptável**[: é possível usar o CAPTCHA invisível para exibir o teste CAPTCHA somente no caso de uma atividade suspeita](/help/forms/captcha-adaptive-forms.md). Se nenhuma atividade suspeita for encontrada, o teste CAPTCHA não será exibido. Ajuda a avaliar o preenchimento de formulários humanos sem os requisitos da caixa de seleção, reduzir os esforços de personalização e melhorar a experiência do usuário final.

* **Configurações do Modelo de dados de formulário**: Agora você pode [reutilizar configurações do Modelo de dados de formulário em ambientes](/help/forms/create-form-data-models.md#runmode-specific-context-aware-config), simplificando as integrações de dados e reduzindo os custos de TI.

## Complemento CIF {#cloud-services-cif}

### Novidades {#what-is-new-cif}

* Acesso rápido ao cockpit de produtos: Acesse facilmente as informações completas e detalhadas do produto com um clique no Editor de sites

   ![Habilitar lista de desejos](/help/assets/CIF/enable-wishlist.png)

* Suporte para componentes adicionais de comércio de marketing: Os componentes podem ser configurados para mostrar uma chamada para ação de adição ao carrinho e de lista de desejos

   ![Atalho do editor de sites para o cockpit de produtos](/help/assets/CIF/sites-editor-shortcut-to-cockpit.png)

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Analisadores de build do SDK {#sdk-build-analyzers}

O AEM plug-in Maven do Analisador de build do SDK as a Cloud Service detecta problemas em um projeto maven, incluindo dependências ausentes. Ela oferece aos desenvolvedores uma oportunidade de descobrir problemas durante o desenvolvimento local, bem antes de implantar em ambientes do Cloud com o Cloud Manager.

Recentemente, foi adicionado um novo analisador:

* `content-packages-validation` - valida para sintaxe e estrutura de conteúdo bem formadas para pacotes que serão instalados durante a implantação

É altamente recomendável atualizar seu projeto maven com a versão mais recente do analisador ou incluí-lo se ainda não tiver feito isso. Para obter mais informações, consulte a documentação [here](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html).

## [!DNL Experience Manager] como [!DNL Cloud Service] Segurança da fundação {#foundation-security}

### Substituição de TLS 1.0, 1.1

A partir de 30 de junho de 2022, o Experience Manager as a Cloud Service exigirá uma comunicação de rede mais segura e troca de dados com os sistemas dos usuários. AEM usará exclusivamente o protocolo TLS (Transport Layer Security), 1.2. As versões anteriores do TLS 1.0 e 1.1 serão substituídas.

Se você continuar usando versões mais antigas do TLS como 1.0, 1.1, poderá perder o acesso ao Experience Manager as a Cloud Service.

## Cloud Manager {#cloud-manager}

Você pode encontrar uma lista completa de versões mensais do Cloud Manager [here](/help/implementing/cloud-manager/release-notes-cloud-manager/release-notes-cm-current.md).

## Ferramentas de migração {#migration-tools}

Você pode encontrar uma lista completa das versões das Ferramentas de migração [here](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
