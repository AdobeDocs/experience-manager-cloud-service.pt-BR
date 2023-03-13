---
title: Notas de versão do  [!DNL Adobe Experience Manager]  as a Cloud Service 2022.4.0.
description: Notas de versão do  [!DNL Adobe Experience Manager]  as a Cloud Service 2022.4.0.
exl-id: 6c86838a-cabf-4770-b1ae-618af70193a2
source-git-commit: 9a08514f11c86b783ae68940a0c3c58fcada3dc2
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 100%

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

A data de lançamento da versão atual (2022.4.0) do [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] é 5 de maio de 2022.
A próxima versão (2022.5.0) está planejada para 9 de junho de 2022.

## Vídeo da versão {#release-video}

Assista ao vídeo [Visão geral da versão de abril de 2022](https://video.tv.adobe.com/v/342612?quality=12) que exibe um resumo dos recursos adicionados na versão 2022.4.0.

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Novos recursos no [!DNL Sites] {#sites-features}

* Os tipos de dados do modelo de conteúdo agora podem ser definidos como [traduzíveis](/help/assets/content-fragments/content-fragments-models.md#properties) usando uma caixa de seleção simples no editor do modelo de conteúdo. Além disso, as regras e configurações de tradução do AEM são atualizadas automaticamente.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Novos recursos no [!DNL Assets] {#assets-features}

* Agora você pode [classificar tags](/help/assets/organize-assets.md#use-tags-to-organize-assets) na janela do seletor de tags em ordem crescente ou decrescente com base no nome da tag, data de criação ou data de modificação.


## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Novidades do [!DNL Forms] {#what-is-new-forms}

* **Comunicações — Compatibilidade com APIs de manipulação de documentos no SDK do Forms as a Cloud Service**: [APIs de manipulação de documentos](/help/forms/aem-forms-cloud-service-communications.md) ajudam a combinar, reorganizar e validar documentos PDF. Agora você pode usar as Comunicações, que são APIs de geração de documentos, em um ambiente de desenvolvimento local com a ajuda do SDK do AEM Forms as a Cloud Service.

* **Usar XCI personalizado para gerar um documento de registro**[: agora você pode usar um arquivo XCI personalizado para definir várias propriedades de um documento de registro](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#use-a-custom-xci-file). Ele substitui o XCI principal pelas alterações personalizadas. Ele oferece mais controle sobre a geração de documentos de registro, aumentando as oportunidades de personalização e customização.

* **Usar CAPTCHA invisível em um formulário adaptável**[: é possível usar o CAPTCHA invisível para exibir o teste CAPTCHA somente no caso de uma atividade suspeita](/help/forms/captcha-adaptive-forms.md). Se nenhuma atividade suspeita for encontrada, o teste CAPTCHA não será exibido. Isso ajuda a avaliar o preenchimento de formulários por humanos sem requisitos de caixa de seleção, reduz os esforços de personalização e melhora a experiência do usuário final.

* **Configurações do modelo de dados de formulário**: agora você pode [reutilizar configurações do modelo de dados de formulário entre ambientes](/help/forms/create-form-data-models.md#runmode-specific-context-aware-config), simplificando as integrações de dados e reduzindo os custos de TI.


## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Analisadores de build do SDK {#sdk-build-analyzers}

O plug-in para Maven do Analisador de build do SDK do AEM as a Cloud Service detecta problemas em um projeto Maven, incluindo dependências ausentes. Ele oferece aos desenvolvedores uma oportunidade de descobrir problemas durante o desenvolvimento local, bem antes da implantação em ambientes da nuvem com o Cloud Manager.

Recentemente, foi adicionado um novo analisador:

* `content-packages-validation` - valida a qualidade de composição da sintaxe e da estrutura do conteúdo de pacotes que serão instalados durante a implantação

É altamente recomendável atualizar seu projeto Maven para utilizar a versão mais recente do analisador ou incluí-lo se ainda não tiver feito isso. Para obter mais informações, consulte a documentação [aqui](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html?lang=pt-BR).

## Segurança do [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation-security}

### Descontinuidade do TLS 1.0 e 1.1

A partir de 30 de junho de 2022, o Experience Manager as a Cloud Service exigirá comunicações de rede e trocas de dados mais seguras com os sistemas dos usuários. O AEM usará exclusivamente o protocolo TLS (Transport Layer Security) 1.2. As versões anteriores do TLS (1.0 e 1.1) serão descontinuadas.

Se você continuar a usar versões mais antigas do TLS (como 1.0 e 1.1), poderá perder o acesso ao Experience Manager as a Cloud Service.

## Cloud Manager {#cloud-manager}

Você pode encontrar uma lista completa de versões mensais do Cloud Manager [aqui.](/help/implementing/cloud-manager/release-notes/current.md)

## Ferramentas de migração {#migration-tools}

Você pode encontrar uma lista completa de versões das ferramentas de migração [aqui](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
