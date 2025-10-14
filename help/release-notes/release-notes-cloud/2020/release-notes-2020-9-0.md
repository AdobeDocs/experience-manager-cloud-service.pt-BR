---
title: Notas de versão do  [!DNL Adobe Experience Manager]  as a Cloud Service 2020.9.0.
description: as a Cloud Service Notas de versão do [!DNL Adobe Experience Manager] para 2020.9.0.
exl-id: 2332512f-8c52-4569-a006-faa36a7670a1
feature: Release Information
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '711'
ht-degree: 15%

---

# Notas de versão para [!DNL Adobe Experience Manager] as a Cloud Service 2020.9.0 {#release-notes}

A seção a seguir descreve as Notas de Versão gerais do [!DNL Experience Manager] as a Cloud Service 2020.9.0.

## Data de lançamento {#release-date}

A Data de Lançamento do [!DNL Adobe Experience Manager] as a Cloud Service 2020.9.0 é 24 de setembro de 2020.

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

### Novidades do [!DNL Sites] {#what-is-new-sites}

* O SDK JavaScript do Editor de Aplicativos de Página Única (SPA) [&#x200B; agora é open source](/help/implementing/developing/hybrid/reference-materials.md).

## [!DNL Adobe Experience Manager Assets] as a Cloud Service {#assets}

### Novidades do [!DNL Assets] {#what-is-new-assets}

* Arquivos de imagem de marca d&#39;água são aceitos para representações geradas com microsserviços de ativos. Ele pode ser configurado como um Perfil de processamento e usa um arquivo PNG como uma marca d&#39;água. Consulte [marca d&#39;água em seus ativos](/help/assets/watermark-assets.md).

* Aprimoramentos em [!DNL Dynamic Media]

   * Publish seletiva - agora as equipes de marketing podem acessar imagens de recorte inteligente do [!DNL Dynamic Media] e execuções dinâmicas que são sincronizadas com o [!DNL Dynamic Media] para que possam criar materiais promocionais, tudo sem precisar publicar esses ativos no [!DNL Dynamic Media] para entrega global. A publicação de [!DNL Experience Manager] e [!DNL Dynamic Media] está dissociada e pode ocorrer separadamente. Consulte [publicação seletiva](/help/assets/dynamic-media/selective-publishing.md).
   * Os administradores agora podem redefinir a senha do Cloud Service [!DNL Dynamic Media] recebida no provisionamento. A redefinição pode ser feita na interface do usuário [!DNL Experience Manager], sem a necessidade de usar o aplicativo de desktop [!DNL Dynamic Media Classic].

* Para saber mais sobre os seguintes aprimoramentos, consulte [novidades no Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/whats-new.html?lang=pt-BR).

   * Pré-visualização de PDF aprimorada com a integração do SDK com o Adobe Document Cloud View.
   * Funcionalidade de download de clique único.
   * Novas configurações de administração para a experiência de download.

<!--
### Bugs Fixed {#bugs-fixed-assets}

TBD: list of Assets aaCS bugs that are fixed.
-->

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novidades {#what-is-new-commerce}

* Lançamento de componentes principais de CIF v1.3.0. Consulte [Componentes principais do CIF](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.3.0) para obter mais detalhes.

* O recurso de visualização com produto/categoria para modelos de produto e categoria já está disponível. Isso permite que usuários/profissionais de marketing no AEM visualizem os modelos de produto/categoria com dados reais.

* A página Propriedades foi adicionada aos produtos e categorias para permitir que os usuários corporativos visualizem detalhes associados à SKU do produto/ID da categoria.

* Adição do recurso de classificação ao Console do produto para permitir a classificação de produtos/categorias por nome ou atributos de preço.

* Adição da funcionalidade de pesquisa do produto ao Console do produto.

### Correções de erros {#bug-fixes-commerce}

* As configurações de Commerce Cloud não respeitavam a herança. Isso foi corrigido para garantir que a configuração herde valores.

## Cloud Manager {#cloud-manager}

### Data de lançamento {#release-date-cm}

A data de lançamento da versão 2020.9.0 do [!UICONTROL Cloud Manager] é sexta-feira, 3 de setembro de 2020.

### Novidades {#what-is-new-cloud-manager}

* A Auditoria de conteúdo foi renomeada para Auditoria de experiência.
* O processo de compilação foi separado em três comandos Maven separados.
* Se o Repositório Git não for clonado, serão feitas mais três tentativas.

### Correções de erros {#bug-fixes-cm}

* A guia Auditoria de conteúdo exibia incorretamente a URL de base usando o domínio do autor em vez de o domínio de publicação.

## Cloud Readiness Analyzer {#cloud-readiness-analyzer}

Consulte esta seção para saber mais sobre as novidades e atualizações do Cloud Readiness Analyzer versão v1.1.0.

### Novidades {#what-is-new-cra}

* O CRA (Cloud Readiness Analyzer) tem um console de estado de início que exibe um botão **Gerar relatório** explícito para o usuário clicar e executar o CRA.

* A interface do usuário do CRA exibe o progresso enquanto está em execução. Ele exibe itens que estão sendo analisados e descobertas encontradas durante a execução.

* O relatório do CRA exibe um resumo e o número de conclusões em um formato de tabela organizado pelo tipo de descoberta e o nível de importância. Ao clicar no número da descoberta, a tela rola automaticamente para o local da descoberta no relatório.

### Correções de erros {#cra-bug-fixes}

* Em certos casos, o relatório do CRA não era atualizado depois de forçar uma atualização. Isso foi corrigido nesta versão.

## Ferramenta Transferência de conteúdo {#content-transfer-tool}

Siga esta seção para saber mais sobre as novidades e atualizações da Ferramenta de transferência de conteúdo versão v1.1.10.

### Novidades {#what-is-new-ctt}

* A Ferramenta de transferência de conteúdo (CTT) é compatível com o Armazenamento de dados do Azure Blob Store.

* A interface do usuário da CTT tem um recurso de recarregamento automático que recarrega a página de visão geral a cada 30 segundos.

* Adição de um botão à interface de usuário da CTT para recuperar facilmente o *Token de acesso*.

* Adição de mensagem de validação descritiva para *URL* e *Nome do Conjunto de Migração*.

## Ferramentas de refatoração de código {#code-refactoring}

Siga esta seção para saber mais sobre as novidades e atualizações das Ferramentas de refatoração de código.

### Novidades {#what-is-new-refactoring}

* O plug-in AIO-CLI é compatível com o Repository Modernizer e permite que os usuários executem a ferramenta usando o plug-in.

  Consulte [Recurso do Git: aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration) para obter mais detalhes.

* O utilitário Repository Modernizer pode ser usado para reestruturar pacotes de projetos existentes em pacotes compatíveis com a estrutura do projeto definida para o AEM as a Cloud Service.

  Consulte [Recurso do Git: Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer) para obter mais detalhes.
