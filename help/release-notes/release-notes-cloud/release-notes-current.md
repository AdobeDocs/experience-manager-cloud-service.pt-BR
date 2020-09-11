---
title: Notas de versão do  [!DNL Adobe Experience Manager] as a Cloud Service 2020.9.0.
description: 'Notas de versão do [!DNL Adobe Experience Manager] as a Cloud Service 2020.9.0 '
translation-type: tm+mt
source-git-commit: cca8aff3ada327252bfabd2207e7aa86fdf00033
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 24%

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
