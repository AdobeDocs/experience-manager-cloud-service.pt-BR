---
title: Notas de versão do  [!DNL Adobe Experience Manager] as a Cloud Service 2020.9.0.
description: 'Notas de versão do [!DNL Adobe Experience Manager] as a Cloud Service 2020.9.0 '
translation-type: tm+mt
source-git-commit: 9bb087cb0570a1f3bbffb989a9399d3274f9c5e1
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 22%

---


# Notas de versão do [!DNL Adobe Experience Manager] as a Cloud Service 2020.9.0 {#release-notes}

A seção a seguir descreve as Notas de versão gerais do Experience Manager as a Cloud Service 2020.9.0.

## [!DNL Adobe Experience Manager Sites] como um Cloud Service {#sites}

### What is new in [!DNL Sites] {#what-is-new-sites}

* O SDK do Javascript do Editor de aplicativo de página única (SPA) agora [é de código aberto.](/help/implementing/developing/spa/reference-materials.md)

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

