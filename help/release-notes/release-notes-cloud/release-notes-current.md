---
title: Current Release Notes for [!DNL Adobe Experience Manager] as a Cloud Service.
description: Current Release Notes for [!DNL Adobe Experience Manager] as a Cloud Service.
translation-type: tm+mt
source-git-commit: 4bce4fceab08a95fc2c1c8334f84fd54204228ba
workflow-type: tm+mt
source-wordcount: '886'
ht-degree: 5%

---


# Notas de versão do [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

The following section outlines the general Release Notes for [!DNL Experience Manager] as a Cloud Service.

## Data de lançamento {#release-date}

The Release Date for [!DNL Adobe Experience Manager] as a Cloud Service 2020.10.0 is October 28, 2020.
A seguinte versão (2020.11.0) será lançada em 1º de dezembro de 2020.

## [!DNL Adobe Experience Manager Sites] como um Cloud Service {#sites}

### What is new in [!DNL Sites] {#what-is-new-sites}

<!-- add when release done: * **Core Components 2.12.0**: With Core Components being on auto-update, benefit from the latest improvements contributed by the community. See list of changes since 2.11.1: Release Notes -->

* **Tipo de Arquivo do Projeto 24**: A base recomendada para start de um novo projeto AEM melhorou, agora incluindo a nova Camada de dados do cliente Adobe, para fornecer site na AMP e novos pontos de extensão para adicionar CSS/JS do projeto.

* **Pastas** do ContextHub: Capacidade de criar pastas de audiência para organizar, localizar e selecionar facilmente segmentos de audiência a serem usados para recursos de direcionamento de oferta do ContextHub.

## [!DNL Adobe Experience Manager Assets] como um Cloud Service {#assets}

### What is new in [!DNL Assets] {#what-is-new-assets}

* **[!DNL Adobe Sensei]Marcação** inteligente de vídeo: Ao utilizar modelos do AI para analisar o conteúdo de vídeo para tags de objeto e ação específicas, os usuários do DAM podem gastar menos tempo adicionando tags e mais tempo usando as informações avançadas expostas para fornecer a experiência certa aos clientes. Consulte Ativos [de vídeo com tags](/help/assets/smart-tags-video-assets.md)inteligentes.

* **Aprimoramentos** do Brand Portal: Os novos recursos a seguir e muito mais estão disponíveis em [!DNL Brand Portal]. For details, see [[!DNL Brand Portal] release notes](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/introduction/brand-portal-release-notes.html).

   * [Experiência](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/download/brand-portal-download-assets.html) aprimorada de download para downloads rápidos e simplificados. Configurações adicionais de download podem ser configuradas pelos administradores para oferta de uma experiência que atenda às necessidades dos usuários e empresas.
   * A navegação com um clique para Arquivos, [Coleções](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/share/brand-portal-share-collection.html)e Links compartilhados agora é possível em qualquer página.
   * Os usuários podem [selecionar e baixar execuções](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/download/brand-portal-download-assets.html#download-assets-from-asset-details-page) específicas agora. A nova opção de download de representação está disponível no painel Representações na página Detalhes do ativo.
   * Um tempo limite de 15 minutos para sessões de usuário convidado garante uma melhor experiência para todos os usuários simultâneos.

* **[!DNL Adobe Asset Link]versão 2.1**: Uma nova versão da extensão do [Adobe Asset Link](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/manage-assets-using-adobe-asset-link.ug.html) para [!DNL Adobe Photoshop], [!DNL Adobe Illustrator]e [!DNL Adobe InDesign] está disponível. Ele acrescenta compatibilidade com os [!DNL Adobe Creative Cloud] aplicativos mais recentes da versão 2021, lançada em outubro de 2020.

* **[!DNL Assets]Suporte** a arquivos WebP: [!DNL Assets] como Cloud Service agora oferece suporte ao formato de imagem WebP. WebP é um formato de imagem emergente criado pelo Google. As imagens no formato de arquivo WebP são visualmente indistinguíveis dos arquivos JPG ou PNG e os arquivos são muito menores. O tamanho reduzido de arquivos de ativos melhora o tempo de carregamento da página e ajuda os criadores de conteúdo a proporcionarem uma experiência mais rápida na Web. Consulte [criar um perfil](/help/assets/asset-microservices-configure-and-use.md#create-standard-profile)de processamento padrão.

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novidades {#what-is-new-commerce}

* Lançamento do site de referência CIF Venia - 2020.10.2 que inclui a versão mais recente dos componentes principais CIF v1.4.0. Consulte o site [de referência](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2020.10.2) CIF Venia para obter mais detalhes.

* Componentes principais CIF lançados v1.4.0. Consulte os Componentes [principais](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.4.0) CIF para obter mais detalhes.

### Correções de erros {#bug-fixes-commerce}

* As solicitações de GraphQL no Console de produto e nos Seletores foram feitas por POST HTTP. Isso foi corrigido para garantir que o cliente Apollo GraphQL respeitasse a configuração na configuração OSGi do cliente GraphQL para suportar solicitações de GET, se configuradas.

* CIF Cloud config UI exibiu os botões &quot;Salvar e fechar&quot; para configurações em /lib e /apps/. Mas essas são somente leitura, portanto, a interface do usuário foi corrigida para exibir somente o botão &quot;Fechar&quot;.


## Cloud Manager {#cloud-manager}

### Data de lançamento {#release-date-cm}

A data de lançamento do Cloud Manager no AEM como Cloud Service 2020.11.0 é 12 de novembro de 2020.

### What is new in [!DNL Cloud Manager] {#what-is-new-cm}

* Uma nova opção de menu Logon **** local agora está disponível para os usuários nas opções de menu ambientes nas páginas de resumo do cartão de **Ambientes** e **Ambientes** .
Consulte [Gerenciamento de Ambientes](/help/implementing/cloud-manager/manage-environments.md##login-locally) para obter mais detalhes.

* A guia **Aprendizagem** no Gerenciador de nuvem foi atualizada com novas imagens na interface do usuário.

### Correções de erros {#bug-fixes-cloud-manager}

* O carregamento de dependências feitas antes da execução da compilação exigia o download de um plug-in Maven.
* O link do rodapé do Gerenciador de nuvem para selecionar um idioma agora navegará até o local correto.
* Às vezes, durante a digitalização do código, o processo SonarQube não era start. Isso será detectado automaticamente e uma tentativa de reinicialização será feita.
* Todos os pipelines de produção existentes serão ativados automaticamente com a etapa Auditoria de experiência.

## Adobe Experience Manager as a Cloud Service Foundation {#cloud-service-foundation}

### Fluxos de trabalhos {#workflows}

* Foi adicionado suporte para pesquisar instâncias de fluxo de trabalho com base em Título do fluxo de trabalho, Modelo do fluxo de trabalho, Status, Iniciador, Caminho da carga e Data do Start. Consulte Instâncias [do fluxo de trabalho de](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/sites/administering/workflows-administering.html)pesquisa.

## Ferramenta Transferência de conteúdo {#content-transfer-tool}

Follow this section to learn about what is new and the updates for [Content Transfer Tool](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html) Release v1.1.12.

### Novidades {#what-is-new-ctt}

* A experiência do usuário para registros foi aprimorada. Carimbos de data e hora adicionados aos registros de Extração e ingestão. Mensagem adicionada para indicar se os logs estão vazios.

### Correções de erros {#ctt-bug-fixes}

* A Ferramenta de transferência de conteúdo ignorava os arquivos de conteúdo se o conjunto de migração contivesse caminhos que tivessem nomes de arquivos parcialmente semelhantes. Isso foi corrigido.

## Analisador de práticas recomendadas {#best-practices-analyzer}

### Data de lançamento {#release-date-bpa}

A data de lançamento do Analisador de práticas recomendadas é 13 de novembro de 2020.

### What is new in [!DNL Best Practices Analyzer] {#what-is-new-bpa}

* O Cloud Readiness Analyzer agora é BPA (Best Practices Analyzer). O BPA fornece uma avaliação das práticas recomendadas de sua implementação AEM atual e ajuda a avaliar a prontidão para mudar de uma instância AEM existente para AEM como Cloud Service.

* Foi adicionado um novo detector para detectar o uso de `java.io.InputStream`, o que pode causar problemas se usado em AEM como Cloud Service.

### Correções de erros {#bpa-bug-fixes}

* Foi corrigido o erro que causava os positivos relacionados ao componente de base ** textfield.