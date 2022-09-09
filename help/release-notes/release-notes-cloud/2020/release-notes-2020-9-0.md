---
title: Notas de versão do  [!DNL Adobe Experience Manager]  as a Cloud Service 2020.9.0.
description: "[!DNL Adobe Experience Manager] Notas de versão as a Cloud Service para 2020.9.0."
exl-id: 2332512f-8c52-4569-a006-faa36a7670a1
source-git-commit: bc4da79735ffa99f8c66240bfbfd7fcd69d8bc13
workflow-type: tm+mt
source-wordcount: '724'
ht-degree: 14%

---

# Notas de versão do [!DNL Adobe Experience Manager] as a Cloud Service 2020.9.0 {#release-notes}

A seção a seguir descreve as Notas de versão gerais de [!DNL Experience Manager] as a Cloud Service 2020.9.0.

## Data de lançamento {#release-date}

A data de lançamento para [!DNL Adobe Experience Manager] O as a Cloud Service 2020.9.0 é 24 de setembro de 2020.

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

### Novidades do [!DNL Sites] {#what-is-new-sites}

* O SDK JavaScript do editor de Aplicativos de Página Única (SPA) [agora é open source.](/help/implementing/developing/hybrid/reference-materials.md)

## [!DNL Adobe Experience Manager Assets] as a Cloud Service {#assets}

### Novidades do [!DNL Assets] {#what-is-new-assets}

* Arquivos de imagem de marca d&#39;água são aceitos para representações geradas com microsserviços de ativos. Ele pode ser configurado como um Perfil de processamento e usa um arquivo PNG como uma marca d&#39;água. Consulte [marca d&#39;água em seus ativos](/help/assets/watermark-assets.md).

* Melhorias no [!DNL Dynamic Media]

   * Publicação seletiva - agora é possível que uma equipe de marketing acesse [!DNL Dynamic Media] imagens de recorte inteligente e representações dinâmicas que são sincronizadas com [!DNL Dynamic Media] para que possam criar materiais promocionais, tudo sem a necessidade de publicar esses ativos para [!DNL Dynamic Media] para entrega global. [!DNL Experience Manager] e [!DNL Dynamic Media] A publicação é dissociada e pode ocorrer separadamente para isso. Consulte [publicação seletiva](/help/assets/dynamic-media/selective-publishing.md).
   * Agora, os administradores podem redefinir [!DNL Dynamic Media] Senha de Cloud Service recebida no provisionamento. A redefinição pode ser feita em [!DNL Experience Manager] interface do usuário, sem a necessidade de usar o [!DNL Dynamic Media Classic] aplicativo de desktop.

* Para saber mais sobre os seguintes aprimoramentos, consulte [novidades no Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/whats-new.html?lang=pt-BR).

   * Visualização do PDF aprimorada com a integração do SDK do Adobe Document Cloud View.
   * Funcionalidade de download de clique único.
   * Novas configurações de administração para a experiência de download.

<!--
### Bugs Fixed {#bugs-fixed-assets}

TBD: list of Assets aaCS bugs that are fixed.
-->

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novidades {#what-is-new-commerce}

* Lançamento de componentes principais CIF v1.3.0. Consulte [Componentes principais da CIF](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.3.0) para obter mais detalhes.

* O recurso de visualização com produto/categoria para modelos de produto e categoria já está disponível. Isso permite que usuários/profissionais de marketing no AEM visualizem os modelos de produto/categoria com dados reais.

* A página Propriedades foi adicionada aos produtos e categorias para permitir que os usuários corporativos visualizem detalhes associados à SKU do produto/ID da categoria.

* Adição do recurso de classificação ao Console do produto para permitir a classificação de produtos/categorias por nome ou atributos de preço.

* Adição da funcionalidade de pesquisa do produto ao Console do produto.

### Correções de erros {#bug-fixes-commerce}

* As configurações de Commerce Cloud não respeitavam a herança. Isso foi corrigido para garantir que a configuração herde valores.

## Cloud Manager {#cloud-manager}

### Data de lançamento {#release-date-cm}

A data de lançamento para [!UICONTROL Cloud Manager] A versão 2020.9.0 é 3 de setembro de 2020.

### Novidades {#what-is-new-cloud-manager}

* A Auditoria de conteúdo foi renomeada como Auditoria de experiência.
* O processo de build foi separado em três comandos Maven separados.
* Se o Repositório Git não for clonado, haverá mais três tentativas.

### Correções de erros {#bug-fixes-cm}

* A guia Auditoria de conteúdo exibia incorretamente o URL base usando o domínio do autor em vez do domínio de publicação.

## Cloud Readiness Analyzer {#cloud-readiness-analyzer}

Siga esta seção para saber mais sobre as novidades e as atualizações do Cloud Readiness Analyzer versão v1.1.0.

### Novidades {#what-is-new-cra}

* O CRA (Cloud Readiness Analyzer) tem um console de estado de início que exibe um **Gerar relatório** para o usuário clicar em para executar o CRA.

* A interface do usuário do CRA exibe o progresso enquanto está em execução. Ele exibe itens que estão sendo analisados e descobertas encontradas durante a execução.

* O relatório do CRA exibe um resumo e o número de conclusões em um formato de tabela organizado pelo tipo de descoberta e o nível de importância. Clicar no número dessa conclusão rolar-se-á automaticamente para o local da descoberta no relatório.

### Correções de erros {#cra-bug-fixes}

* Em certos casos, o relatório do CRA não era atualizado após forçar uma atualização. Isso foi corrigido nesta versão.

## Ferramenta Transferência de conteúdo {#content-transfer-tool}

Siga esta seção para saber mais sobre as novidades e as atualizações da ferramenta Transferência de conteúdo versão v1.1.10.

### Novidades {#what-is-new-ctt}

* A Ferramenta de transferência de conteúdo (CTT) é compatível com o Armazenamento de dados do Azure Blob Store.

* A interface do usuário da CTT tem um recurso de recarregamento automático que recarrega a página de visão geral a cada 30 segundos.

* Botão adicionado à interface do usuário da CTT para recuperar *Token de acesso* facilmente.

* Mensagem de validação descritiva adicionada para *URL* e *Nome do conjunto de migração*.

## Ferramentas de refatoração de código {#code-refactoring}

Siga esta seção para saber mais sobre as novidades e as atualizações das Ferramentas de refatoração de código.

### Novidades {#what-is-new-refactoring}

* O plug-in AIO-CLI é compatível com o Repository Modernizer e permite que os usuários executem a ferramenta usando o plug-in.

   Consulte [Recurso Git: aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration) para obter mais detalhes.

* O utilitário Repository Modernizer pode ser usado para reestruturar pacotes de projetos existentes em pacotes compatíveis com a estrutura do projeto definida para AEM as a Cloud Service.

   Consulte [Recurso Git: Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer) para obter mais detalhes.
