---
title: Notas de versão atuais do  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Notas de versão atuais do  [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
mini-toc-levels: 1
source-git-commit: 8008bd1076b2f2170f2c95685017854f8bf09646
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 27%

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

A data de lançamento do [!DNL Adobe Experience Manager] como [!DNL Cloud Service] a versão atual (2022.8.0) é 1º de setembro de 2022.
A próxima versão (2022.10.0) está planejada para 10 de novembro de 2022.

## Vídeo da versão {#release-video}

Assista ao vídeo Visão geral da versão de agosto de 2022 para obter um resumo dos recursos adicionados na versão 2022.8.0:

>[!VIDEO](https://video.tv.adobe.com/v/346608/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Novos recursos no [!DNL Sites] {#sites-features}

* O componente Email permite a criação de conteúdo no AEM, que é então entregue como emails via Campaign Classic. O Componente Principal De Email:
   * é baseado no [Componente WCM principal](https://github.com/adobe/aem-core-wcm-components) que suporta Modelos editáveis e o Sistema de estilos.
   * O fornece 10 componentes de produção otimizados por email (Página, Contêiner, Título, Texto, Imagem, Botão, Teaser, Fragmento de experiência, Fragmento de conteúdo, Segmentação).
   * O oferece personalização e segmentação avançadas, graças à [inserção de variáveis de Campanha](https://github.com/adobe/aem-core-email-components/wiki/RTE-Personalization) na maioria dos campos de diálogo, e para o [Componente de segmentação](https://github.com/adobe/aem-core-email-components/wiki/Segmentation-component-(Technical-Documentation)).
   * O fornece a saída de HTML amigável para email ideal, graças ao [Estilos CSS em invólucro](https://github.com/adobe/aem-core-email-components/wiki/HTML-Inliner:-Technical-documentation), o [Intransmissões de atributo HTML](https://github.com/adobe/aem-core-email-components/wiki/HTML-Inliner:-Technical-documentation)e o [HTML sanitizer](https://github.com/adobe/aem-core-email-components/wiki/HTML-sanitizing:-Technical-documentation).
   * permite a criação de emails em qualquer lugar.

### Novos recursos disponíveis no canal de pré-lançamento do [!DNL Sites] {#prerelease-features-sites}

* O [Console do fragmento do conteúdo](/help/sites-cloud/administering/content-fragments/content-fragments-console.md) O fornece aos usuários uma opção para exibir o número total de cópias de idioma associadas a um fragmento de conteúdo. Um acesso de 1 clique foi fornecido para exibir todas as cópias de idioma também. Os usuários também podem filtrar a exibição de tabela pelo local de seu interesse.

![Idiomas de fragmentos de conteúdo](/help/release-notes/assets/cfconsole-languages.png)

## [!DNL Experience Manager Assets] como [!DNL Cloud Service] {#assets}

### Novos recursos no [!DNL Assets] {#features-assets}

* Agora é possível configurar o Adobe Experience Manager Assets para [restringir os tipos de ativos que os usuários podem fazer upload com base no tipo de MIME](/help/assets/configure-asset-upload-restrictions.md).

   ![Restrições de upload de ativos](/help/assets/assets/asset-upload-restrictions.png)

## [!DNL Experience Manager Forms] como [!DNL Cloud Service] {#forms}

### Novos recursos disponíveis no canal de pré-lançamento do [!DNL Forms] {#prerelease-features-forms}

* [Assistente adaptável Forms](/help/forms/creating-adaptive-form.md): O AEM Forms fornece um assistente para usuários empresariais para criar rapidamente o Adaptive Forms. O assistente tem uma navegação de guia rápida para selecionar facilmente o modelo pré-configurado, o estilo, os campos e as opções de envio para criar um formulário adaptável. Esta versão traz as seguintes melhorias ao assistente:

   * Selecionar ou desmarcar campos: O assistente permite criar um formulário adaptável com base em esquemas JSON e do Modelo de dados de formulário. Agora é possível selecionar um subconjunto de campos em um esquema para incluir em um Formulário adaptável. Os campos selecionados são convertidos em componentes de captura de dados do formulário adaptável correspondentes para criar rapidamente os formulários adaptáveis desejados.

   * Usar modelos estáticos: Os clientes com investimentos existentes em modelos estáticos herdados podem continuar sua jornada de adoção da nuvem usando modelos estáticos no assistente para criar formulários adaptáveis. Isso oferece mais tempo para os clientes migrarem modelos estáticos antigos para modelos editáveis modernos.

* [Remover campos ocultos de um Documento de registro (DoR) durante o processamento no servidor](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md): Você pode gerar o documento de PDF de registro para usuários finais contendo apenas os campos que estavam visíveis para eles durante a experiência de captura de dados. Após o envio do formulário, o servidor valida quais campos estavam ocultos para o usuário final com base nos dados enviados e exclui do documento de registro para fins de consistência.

## Complemento CIF {#cloud-services-cif}

### Novidades {#what-is-new-cif}

* Associação de páginas de AEM a produtos e categorias por meio das propriedades AEM página mais visão geral do cockpit de produtos
   ![associação da página de cockpit do produto](/help/assets/CIF/product_cockpit_page_association.png)

## Cloud Manager {#cloud-manager}

Você pode encontrar uma lista completa de versões mensais do Cloud Manager [aqui](/help/implementing/cloud-manager/release-notes-cloud-manager/release-notes-cm-current.md).

## Ferramentas de migração {#migration-tools}

Você pode encontrar uma lista completa de versões das ferramentas de migração [aqui](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
