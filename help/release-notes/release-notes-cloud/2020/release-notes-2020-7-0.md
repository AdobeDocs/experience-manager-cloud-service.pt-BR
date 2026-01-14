---
title: Notas de versão do  [!DNL Adobe Experience Manager] as a Cloud Service 2020.7.0.
description: Notas de versão do as a Cloud Service [!DNL Adobe Experience Manager] para 2020.7.0.
exl-id: 75d354a3-6987-4de0-aec8-24043461c516
feature: Release Information
role: Admin
source-git-commit: 281a8efcd18920dd926d92db9c757c0513d599fd
workflow-type: tm+mt
source-wordcount: '1012'
ht-degree: 74%

---

# Notas de versão do [!DNL Adobe Experience Manager] as a Cloud Service 2020.7.0 {#release-notes}

A seção a seguir descreve as Notas de versão gerais do Experience Manager as a Cloud Service 2020.7.0.

## Data de lançamento {#release-date}

O [!DNL Experience Manager] as a Cloud Service 2020.7.0 foi lançado em 30 de julho de 2020.

## Adobe Experience Manager Sites as a Cloud Service {#cloud-services-sites}

### Novidades {#what-is-new-sites}

Os conectores do [!DNL Experience Manager] as a Cloud Service para o [!DNL Adobe Target] e o [!DNL Adobe Analytics] incluem as seguintes melhorias:

* Uma nova implementação da interface do usuário substitui a implementação com base na interface clássica.

* Os diálogos da interface do usuário foram simplificados, deixando a criação da estrutura para mapeamento variável e outras configurações para o [!DNL Adobe Launch]. Consulte [Integração do Adobe Analytics](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/integrations/integrating-adobe-analytics.html) e [Integração do Adobe Target](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/integrations/integrating-adobe-target.html).

* As configurações agora são armazenadas em `/conf` e não em `/etc/cloudsettings` no repositório do Experience Manager.

## as a Cloud Service [!DNL Adobe Experience Manager Assets] {#assets}

### Novidades do [!DNL Assets] {#what-is-new-assets}

* O [!DNL Asset Compute Service] é um serviço dimensionável e extensível para processar ativos. Os administradores podem configurar o [!DNL Experience Manager] para chamar aplicativos personalizados criados com o [!DNL Asset Compute Service]. Os desenvolvedores podem usar o serviço para criar aplicativos personalizados especializados que atendam a casos de uso complexos. Este serviço da Web pode gerar miniaturas para diferentes tipos de arquivos, renderizações de imagem de alta qualidade de formatos de arquivo do Adobe, codificar vídeos (no futuro), extrair metadados, extrair texto completo como precursor para indexação e executar um ativo por meio de todos os serviços do [!DNL AI] disponíveis. consulte [usar microsserviços de ativos e perfis de processamento](/help/assets/asset-microservices-configure-and-use.md).

* A configuração inicial do [!DNL Dynamic Media] no [!DNL Experience Manager] as a Cloud Service foi aprimorada para ficar mais robusta. Agora, ela informa o progresso dos processos aos administradores.

* A publicação de ativos no [!DNL Dynamic Media] está mais simples e robusta e agora faz parte do pipeline de processamento de ativos global usando microsserviços de ativos e melhorando o back-end de publicação em lote.

* As etapas de fluxo de trabalho que não são compatíveis com uma implantação do Cloud Service agora são marcadas com um aviso no editor de [!UICONTROL modelo de fluxo de trabalho]. Além disso, ao executar os fluxos de trabalho existentes no ambiente do Cloud Service, as etapas do fluxo de trabalho incompatíveis são ignoradas.

* Os modelos de fluxo de trabalho criados pelos clientes implantados em `/conf/global` no projeto Git associado ao ambiente em [!DNL Cloud Manager] são implantados automaticamente em `/var` e, portanto, disponibilizados em [!DNL Experience Manager]. Os modelos de fluxo de trabalho do produto em `/libs` que foram alterados pelo cliente não são implantados automaticamente em `/var`.

### Erros corrigidos {#assets-bugs-fixed}

* O assistente Mover ativo não carrega como esperado os ativos que estão incluídos em Coleções. (CQ-4296756)
* Os valores de `dam:size` e `dam:sha1` são excluídos do write-back do XMP. (CQ-4237355)
* Ao cancelar a publicação de ativos em massa, [!DNL Brand Portal] gera um erro sugerindo que o URI da solicitação é muito longo. (CQ-4299474)

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novidades {#what-is-new-commerce}

O AEM Commerce agora está disponível no Cloud Service.

Consulte [Introdução ao AEM Commerce as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/commerce/getting-started.html) para obter mais detalhes.

## Componentes principais {#core-components}

### Novidades {#what-is-new-core-components}

A versão 2.11.0 dos [Componentes principais do AEM](https://experienceleague.adobe.com/pt-br/docs/experience-manager-core-components/using/introduction) agora está disponível como parte do AEM Sites, incluindo:

* Introdução de um novo [Visualizador de PDF](https://www.aemcomponents.dev/content/core-components-examples/library/core-content/pdf-viewer.html).

* O suporte para Accelerated Mobile Pages (AMP) dos Componentes principais já está disponível. As páginas AMP ajudam a produzir experiências mais rápidas para o cliente, fazendo a transição da página de maneira instantânea ao entrar no site a partir de um resultado de pesquisa do Google para dispositivos móveis, o que melhora o engajamento do usuário e o SEO.
Consulte [Suporte ao AMP para os Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/amp.html) para obter mais detalhes.

* Compatibilidade com a versão 1.0.2 da [Camada de dados do cliente da Adobe](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/data-layer/overview.html?lang=pt-BR).

* Correções de erros e melhorias na qualidade do código.

## Cloud Manager {#cloud-manager}

### Data de lançamento {#release-date-cm}

A data de lançamento da versão 2020.7.0 do [!UICONTROL Cloud Manager] é 9 de julho de 2020.

### Novidades {#what-is-new-cloud-manager}

* A página de ambientes foi renovada.

* A página de ambientes hibernados agora mostra um status discreto no Cloud Manager.

* O número de variáveis por ambiente aumentou para 200.

* Os pipelines do Cloud Manager agora oferecem suporte a variáveis e segredos definidos pelo cliente.

  Consulte as variáveis de pipeline para obter mais detalhes.

* Agora há suporte aos Repositórios Maven privados vinculados à autenticação.

* O container de build do Cloud Manager agora é compatível com Java 8 e Java 11.
Consulte Como utilizar o suporte do Java 11 para obter mais detalhes.

### Correções de erros {#bug-fixes-cm}

* Devido a um erro, o link do Cloud Manager para o Console do desenvolvedor estava ativo antes dos ambientes serem totalmente criados.

* O link direto do Cloud Manager para o Console do desenvolvedor não exibia a opção de cancelar hibernação/hibernar para ambientes do Programa de sandbox.

* As opções **Cancelar** e **Salvar** nem sempre estavam visíveis na página de edição do pipeline de não produção.

* Certas falhas no processo de qualidade do código podiam resultar na geração incorreta do arquivo de log.

* Às vezes, o nome sugerido na criação de um programa retornava uma duplicata de um nome de programa existente.

* Grandes logs de etapas de pipeline não podiam ser baixados consistentemente pela interface do usuário.

* A validação de nomes de ambientes apresentava um erro off-by-one.

* A página Ambientes às vezes mostrava segmentos do Publish e do Dispatcher sem que estivessem presentes.

### Problemas conhecidos {#known-issues}

* Devido a uma mudança na forma como a cobertura de código é calculada, a versão *mínima* do plug-in Jacoco agora é a 0.7.5.201505241946 (lançada em maio de 2015). Os clientes que indicarem uma versão mais antiga receberão uma mensagem de erro no processo de qualidade do código.

## Adobe Experience Manager as a Cloud Service Foundation {#cloud-foundation}

### Novidades {#what-is-new-foundations}

* [Os logs podem ser encaminhados para contas do Splunk](/help/implementing/developing/introduction/logging.md#splunk-logs), permitindo que as organizações usem o investimento feito no Splunk.

* [Um endereço IP de saída estático e dedicado](/help/implementing/developing/introduction/development-guidelines.md#dedicated-egress-ip-address) pode ser atribuído para tráfego externo programado no código Java, que pode ser útil para algumas integrações.

* A interface do AEM Analytics Cloud Service foi transferida da interface clássica para a nova interface do AEM. Além disso, a localização do Analytics Cloud Service no repositório do AEM foi movida de `/etc` para `/conf`, para alinhar com outros serviços em nuvem AEM.

* A interface do AEM Target Cloud Service foi transferida da clássica para a nova interface do AEM. Além disso, a localização do serviço na nuvem do Target no repositório do AEM foi movida de `/etc` para `/conf`, para alinhar com outros serviços em nuvem AEM.

## Cloud Readiness Analyzer {#cloud-readiness-analyzer}

Siga esta seção para saber mais sobre as novidades e as atualizações do Cloud Readiness Analyzer versão v1.0.2.

### Correções de erros {#cra-bug-fixes}

* Não foi possível executar a versão anterior do CRA no Adobe Experience Manager (AEM) 6.1. Foi adicionado suporte direto para permitir usuários no grupo de administradores.

  Consulte [Instalando o CRA no AEM 6.1](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/cloud-readiness-analyzer/using-cloud-readiness-analyzer.html#installing-on-aem61) para obter mais detalhes.

* O carimbo de data e hora de expiração exibido no relatório de resumo estava incorreto.

* O CRA estava detectando componentes personalizados duplicados.

* No AEM 6.1, a inspeção de conteúdo era encerrada antes de concluir a inspeção completa. Adição de um gerenciamento de exceções para permitir que o inspetor pule e continue até que a inspeção completa seja concluída.
