---
title: Notas de versão do  [!DNL Adobe Experience Manager]  as a Cloud Service 2022.8.0.
description: Notas de versão do  [!DNL Adobe Experience Manager]  as a Cloud Service 2022.8.0.
exl-id: 0eff8100-5990-4553-8373-445fb7e6fb27
feature: Release Information
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '604'
ht-degree: 59%

---

# Notas de versão do [!DNL Adobe Experience Manager] as a Cloud Service 2022.8.0 {#release-notes}

A seção a seguir descreve as notas de versão de recurso da versão 2022.8.0 do [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>A partir daqui, você pode navegar até as notas de versão das versões anteriores; por exemplo, para aquelas em 2020, 2021 e assim por diante.

>[!NOTE]
>
>Consulte [Atualizações recentes na documentação](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=pt-BR) para obter detalhes de atualizações de documentação não relacionadas diretamente a uma versão.

## Data de lançamento {#release-date}

A data de lançamento da versão atual (2022.8.0) do [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] é sexta-feira, 1 de setembro de 2022.
A próxima versão (2022.10.0) está planejada para 10 de novembro de 2022.

## Vídeo da versão {#release-video}

Assista ao vídeo Visão geral da versão de agosto de 2022 que exibe um resumo dos recursos adicionados na versão 2022.8.0:

>[!VIDEO](https://video.tv.adobe.com/v/346608/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Novos recursos no [!DNL Sites] {#sites-features}

* O Componente de email permite a criação de conteúdo no AEM, que é então entregue por email através do Campaign Classic. O Componente principal de email:
   * baseia-se no [Componente WCM do núcleo](https://github.com/adobe/aem-core-wcm-components) que aceita Modelos editáveis e o Sistema de estilos.
   * O fornece 10 componentes de produção otimizados para email (página, contêiner, título, texto, imagem, botão, teaser, fragmento de experiência, fragmento de conteúdo e segmentação).
   * O oferece personalização e segmentação avançadas, graças à [inserção de variáveis de campanha](https://github.com/adobe/aem-core-email-components/wiki/RTE-Personalization) na maioria dos campos de diálogo, e para a flexibilidade [Componente de segmentação](https://github.com/adobe/aem-core-email-components/wiki/Segmentation-component-(Technical-Documentation)).
   * O fornece saída de HTML ideal para email, graças à [Estilos CSS incorporados](https://github.com/adobe/aem-core-email-components/wiki/HTML-Inliner:-Technical-documentation), o [inliner de atributo HTML](https://github.com/adobe/aem-core-email-components/wiki/HTML-Inliner:-Technical-documentation), e o [higienizador de HTML](https://github.com/adobe/aem-core-email-components/wiki/HTML-sanitizing:-Technical-documentation).
   * permite a criação de emails em qualquer lugar.

### Novos recursos disponíveis no canal de pré-lançamento do [!DNL Sites] {#prerelease-features-sites}

* A variável [Console de fragmentos de conteúdo](/help/sites-cloud/administering/content-fragments/managing.md#content-fragments-console) O fornece aos usuários uma opção para exibir o número total de cópias de idioma associadas a um fragmento de conteúdo. Um acesso de 1 clique também foi fornecido para exibir todas as cópias de idioma. Os usuários também podem filtrar a exibição de tabela pela localidade de seu interesse.

![Idiomas de Fragmentos de conteúdo](/help/release-notes/assets/cfconsole-languages.png)

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Novos recursos no [!DNL Assets] {#features-assets}

* Agora é possível configurar o Adobe Experience Manager Assets para [restringir os tipos de ativos que os usuários podem fazer upload com base no tipo de MIME](/help/assets/configure-asset-upload-restrictions.md).

  ![Restrições de upload de ativos](/help/assets/assets/asset-upload-restrictions.png)

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Novos recursos disponíveis no canal de pré-lançamento do [!DNL Forms] {#prerelease-features-forms}

* [Assistente de Formulários adaptáveis](/help/forms/creating-adaptive-form.md): o AEM Forms fornece um assistente para usuários empresariais para criar rapidamente Formulários adaptáveis. O assistente fornece uma navegação rápida por guias para selecionar facilmente o modelo pré-configurado, o estilo, os campos e as opções de envio para criar um formulário adaptável. Esta versão traz as seguintes melhorias ao assistente:

   * Selecionar ou desmarcar campos: o assistente permite criar um Formulário adaptável com base em esquemas de modelo de dados de formulário e JSON. Agora é possível selecionar um subconjunto de campos em um esquema para incluir em um Formulário adaptável. Os campos selecionados são convertidos em componentes de captura de dados correspondentes do Formulário adaptável para criar rapidamente os formulários adaptáveis desejados.

   * Usar modelos estáticos: os clientes com investimentos existentes em modelos estáticos herdados podem continuar sua jornada de adoção da nuvem usando modelos estáticos no assistente para criar formulários adaptáveis. Isso oferece mais tempo para os clientes migrarem modelos estáticos antigos para modelos editáveis modernos.

* [Remover campos ocultos de um Documento de registro (DoR) durante o processamento no lado do servidor](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md): você pode gerar o documento de PDF de registro para usuários finais contendo apenas os campos que estavam visíveis para eles durante a experiência de captura de dados. Após o envio do formulário, o servidor valida quais campos estavam ocultos para o usuário com base nos dados enviados e os exclui do documento de registro para fins de consistência.

## Complemento CIF {#cloud-services-cif}

### Novidades {#what-is-new-cif}

* Associação de páginas de AEM a produtos e categorias por meio de propriedades de página de AEM, além de visão geral no cockpit do produto
  ![associação de página do cockpit do produto](/help/assets/CIF/product_cockpit_page_association.png)

## Cloud Manager {#cloud-manager}

Você pode encontrar uma lista completa de versões mensais do Cloud Manager [aqui](/help/implementing/cloud-manager/release-notes/current.md).

## Ferramentas de migração {#migration-tools}

Você pode encontrar uma lista completa de versões das ferramentas de migração [aqui](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
