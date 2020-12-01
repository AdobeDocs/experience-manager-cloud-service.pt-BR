---
title: Notas de versão do  [!DNL Adobe Experience Manager] as a Cloud Service 2020.9.0.
description: '[!DNL Adobe Experience Manager] como notas de versão de Cloud Service para 2020.9.0.'
translation-type: tm+mt
source-git-commit: 701d9ff3c9553c28bce0ef417487facedb22373f
workflow-type: tm+mt
source-wordcount: '726'
ht-degree: 11%

---


# Notas de versão do [!DNL Adobe Experience Manager] as a Cloud Service 2020.9.0 {#release-notes}

A seção a seguir descreve as Notas de versão gerais de [!DNL Experience Manager] como um Cloud Service 2020.9.0.

## Data de lançamento {#release-date}

A data de lançamento de [!DNL Adobe Experience Manager] como Cloud Service 2020.9.0 é 24 de setembro de 2020.

## [!DNL Adobe Experience Manager Sites] como um Cloud Service  {#sites}

### Novidades em [!DNL Sites] {#what-is-new-sites}

* O SDK JavaScript do Editor de aplicativos de página única (SPA) [agora é open source.](/help/implementing/developing/hybrid/reference-materials.md)

## [!DNL Adobe Experience Manager Assets] como um Cloud Service  {#assets}

### Novidades em [!DNL Assets] {#what-is-new-assets}

* Arquivos de imagem de marca d&#39;água são suportados para representações geradas com microserviços de ativos. Ele pode ser configurado como um Perfil de processamento e usa um arquivo PNG como uma marca d&#39;água. Consulte [marca d&#39;água em seus ativos](/help/assets/watermark-assets.md).

* Melhorias em [!DNL Dynamic Media]

   * Publicação seletiva - agora é possível para uma equipe de marketing acessar [!DNL Dynamic Media] imagens de recorte inteligente e representações dinâmicas que são sincronizadas com [!DNL Dynamic Media] para que possam criar materiais promocionais, tudo isso sem a necessidade de publicar esses ativos em [!DNL Dynamic Media] para o delivery global. [!DNL Experience Manager] e a  [!DNL Dynamic Media] publicação é dissociada e pode ocorrer separadamente para alcançar isso. Consulte [publicação seletiva](/help/assets/dynamic-media/selective-publishing.md).
   * Os administradores agora podem redefinir a senha [!DNL Dynamic Media] Cloud Service recebida no provisionamento. A redefinição pode ser feita na [!DNL Experience Manager] interface do usuário, sem a necessidade de usar o [!DNL Dynamic Media Classic] aplicativo de desktop.

* Para saber mais sobre os seguintes aprimoramentos, consulte [Novidades do Brand Portal](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/introduction/whats-new.html).

   * Pré-visualização de PDF aprimorada com a integração do SDK da Visualização Adobe Document Cloud.
   * Funcionalidade de download de clique único.
   * Novas configurações de administração para a experiência de download.

<!--
### Bugs Fixed {#bugs-fixed-assets}

TBD: list of Assets aaCS bugs that are fixed.
-->

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novidades {#what-is-new-commerce}

* Componentes principais CIF lançados v1.3.0. Consulte [CIF Componentes principais](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.3.0) para obter mais detalhes.

* A capacidade de pré-visualização com produto/categoria para modelos de produto e categoria já está disponível. Isso permite que os usuários/profissionais de marketing AEM visualizações os modelos de produto/categoria com dados reais.

* A página Propriedades foi adicionada aos produtos e categorias para permitir que os usuários corporativos visualizações detalhes associados ao SKU do produto/ID da categoria.

* Recurso de classificação adicionado ao Console do produto para permitir a classificação de produtos/categorias por nome ou atributos de preço.

* Funcionalidade de pesquisa do produto adicionada ao Console do produto.

### Correções de erros {#bug-fixes-commerce}

* As configurações de Commerce Cloud não respeitavam a herança. Isso foi corrigido para garantir que a configuração herde valores.

## Cloud Manager {#cloud-manager}

### Data de lançamento {#release-date-cm}

A data de lançamento da versão 2020.9.0 [!UICONTROL Cloud Manager] é 3 de setembro de 2020.

### Novidades {#what-is-new-cloud-manager}

* A Auditoria de conteúdo foi renomeada como Auditoria de experiência.
* O processo de compilação foi separado em três comandos Maven separados.
* Se o Repositório Git não for clonado, ele será retentado até três vezes.

### Correções de erros {#bug-fixes-cm}

* A guia Auditoria de conteúdo exibia incorretamente o URL base usando o domínio do autor em vez do domínio de publicação.

## Cloud Readiness Analyzer {#cloud-readiness-analyzer}

Siga esta seção para saber mais sobre as novidades e as atualizações do Cloud Readiness Analyzer versão v1.1.0.

### Novidades {#what-is-new-cra}

* O CRA (Cloud Readiness Analyzer) tem um console de estado de start que exibe um botão **Gerar relatório** explícito para que o usuário clique em para executar o CRA.

* A interface do usuário CRA exibe o progresso enquanto está em execução. Exibe itens que estão sendo analisados e descobertas encontradas durante a execução.

* O relatório CRA exibe um resumo e o número de conclusões em um formato de tabela organizado pelo tipo de descoberta e o nível de importância. Clicar no número dessa descoberta rolar automaticamente para o local da descoberta no relatório.

### Correções de erros {#cra-bug-fixes}

* Em certos casos, o relatório CRA não era atualizado depois de forçar uma atualização. Isso foi corrigido nesta versão.

## Ferramenta Transferência de conteúdo {#content-transfer-tool}

Siga esta seção para saber mais sobre as novidades e as atualizações da Content Transfer Tool Release v1.1.10.

### Novidades {#what-is-new-ctt}

* A Ferramenta de Transferência de Conteúdo (CTT) suporta o Armazenamento de Dados do Azure Blob Store.

* A interface do usuário CTT tem um recurso de recarregamento automático que recarrega a página de visão geral a cada 30 segundos.

* Botão adicionado à interface do usuário CTT para recuperar *Token de acesso* facilmente.

* Mensagem de validação descritiva adicionada para *URL* e *Nome do Conjunto de Migrações*.

## Ferramentas de refatoração de código {#code-refactoring}

Siga esta seção para saber mais sobre as novidades e as atualizações das Ferramentas de Refatoração de Código.

### Novidades {#what-is-new-refactoring}

* O plug-in AIO-CLI suporta o Repository Modernizer e permite que os usuários executem a ferramenta usando o plug-in.

   Consulte [Recurso Git: aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration) para obter mais detalhes.

* O utilitário Repository Modernizer pode ser usado para reestruturar pacotes de projetos existentes em pacotes compatíveis com a estrutura do projeto definida para AEM como um Cloud Service.

   Consulte [Recurso Git: Modernizador do repositório](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer) para obter mais detalhes.

