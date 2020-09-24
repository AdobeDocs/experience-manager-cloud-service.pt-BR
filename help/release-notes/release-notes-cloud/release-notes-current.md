---
title: Notas de versão do  [!DNL Adobe Experience Manager] as a Cloud Service 2020.9.0.
description: 'Notas de versão do [!DNL Adobe Experience Manager] as a Cloud Service 2020.9.0 '
translation-type: tm+mt
source-git-commit: 9d73b8339a327643be9f2ea674857b401346087a
workflow-type: tm+mt
source-wordcount: '714'
ht-degree: 15%

---


# Notas de versão do [!DNL Adobe Experience Manager] as a Cloud Service 2020.9.0 {#release-notes}

A seção a seguir descreve as Notas de versão gerais do Experience Manager as a Cloud Service 2020.9.0.

## Data de lançamento {#release-date}

The Release Date for [!DNL Adobe Experience Manager] as a Cloud Service 2020.9.0 is September 24, 2020.

## [!DNL Adobe Experience Manager Sites] como um Cloud Service {#sites}

### What is new in [!DNL Sites] {#what-is-new-sites}

* O SDK do JavaScript do Editor do aplicativo de página única (SPA) agora [é open source.](/help/implementing/developing/spa/reference-materials.md)

## [!DNL Adobe Experience Manager Assets] como um Cloud Service {#assets}

### What is new in [!DNL Assets] {#what-is-new-assets}

* A marcação em água de uma imagem PNG é compatível com renderizações geradas com microserviços de ativos. Ele pode ser configurado como um Perfil de processamento.

* Aprimoramentos em [!DNL Dynamic Media]

   * Publicação seletiva - agora é possível para uma equipe de marketing acessar imagens de corte inteligente e representações dinâmicas que são sincronizadas para [!DNL Dynamic Media] que possam criar materiais promocionais, tudo isso sem a necessidade de publicar esses ativos [!DNL Dynamic Media] [!DNL Dynamic Media] para o delivery global. A AEM e [!DNL Dynamic Media] a publicação são dissociadas e podem ser realizadas separadamente para o conseguir.
   * Os administradores podem redefinir a senha do [!DNL Dynamic Media] Cloud Service recebida no provisionamento diretamente na interface AEM, sem a necessidade de usar o aplicativo de [!DNL Dynamic Media Classic] desktop.

* Para saber mais sobre os seguintes aprimoramentos, consulte [o que há de novo no Brand Portal](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/introduction/whats-new.html).

   * Pré-visualização de PDF aprimorada com a integração do SDK da Visualização Adobe Document Cloud.
   * Funcionalidade de download de clique único.
   * Novas configurações de administração para a experiência de download.

<!--
### Bugs Fixed {#bugs-fixed-assets}

TBD: list of Assets aaCS bugs that are fixed.
-->

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novidades {#what-is-new-commerce}

* Componentes principais CIF lançados v1.3.0. Consulte os Componentes [principais](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.3.0) CIF para obter mais detalhes.

* A capacidade de pré-visualização com produto/categoria para modelos de produto e categoria já está disponível. Isso permite que os usuários/profissionais de marketing AEM visualizações os modelos de produto/categoria com dados reais.

* A página Propriedades foi adicionada aos produtos e categorias para permitir que os usuários corporativos visualizações detalhes associados ao SKU do produto/ID da categoria.

* Recurso de classificação adicionado ao Console do produto para permitir a classificação de produtos/categorias por nome ou atributos de preço.

* Funcionalidade de pesquisa do produto adicionada ao Console do produto.

### Correções de erros {#bug-fixes-commerce}

* As configurações de Commerce Cloud não respeitavam a herança. Isso foi corrigido para garantir que a configuração herde valores.

## Cloud Manager {#cloud-manager}

### Data de lançamento {#release-date-cm}

The Release Date for [!UICONTROL Cloud Manager] Version 2020.9.0 is September 03, 2020.

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

* Botão adicionado à interface do usuário CTT para recuperar facilmente o *Token de acesso* .

* Mensagem de validação descritiva adicionada para *URL* e Nome *do conjunto* de migração.

## Ferramentas de refatoração de código {#code-refactoring}

Siga esta seção para saber mais sobre as novidades e as atualizações das Ferramentas de Refatoração de Código.

### Novidades {#what-is-new-refactoring}

* O plug-in AIO-CLI suporta o Repository Modernizer e permite que os usuários executem a ferramenta usando o plug-in.

   Consulte Recurso [Git: aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration) para obter mais detalhes.

* O utilitário Repository Modernizer pode ser usado para reestruturar pacotes de projetos existentes em pacotes compatíveis com a estrutura do projeto definida para AEM como um Cloud Service.

   Consulte Recurso [Git: Modernizador](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer) do repositório para obter mais detalhes.

