---
title: Notas de versão da versão 2020.7.0 [!DNL Adobe Experience Manager] como Cloud Service.
description: '[!DNL Adobe Experience Manager] como notas de versão do Cloud Service para 2020.7.0.'
translation-type: tm+mt
source-git-commit: 4211a4d95be6e625b283e3142609923245da8d31
workflow-type: tm+mt
source-wordcount: '1056'
ht-degree: 35%

---


# Release Notes for [!DNL Adobe Experience Manager] as a Cloud Service 2020.7.0 {#release-notes}

A seção a seguir descreve as Notas de versão gerais do Experience Manager as a Cloud Service 2020.7.0.

## Data de lançamento {#release-date}

The release date for [!DNL Experience Manager] as a Cloud Service 2020.7.0 is July 30, 2020.

## Adobe Experience Manager Sites como Cloud Service {#cloud-services-sites}

### Novidades {#what-is-new-sites}

[!DNL Experience Manager] como conectores Cloud Service para [!DNL Adobe Target] e [!DNL Adobe Analytics] são aprimorados das seguintes maneiras:

* Uma nova implementação da interface do usuário substitui a implementação com base na interface clássica.

* Diálogos simplificados da interface do usuário, deixando a criação da estrutura para mapeamento variável e outras configurações para [!DNL Adobe Launch]. Consulte [Integração do Adobe Analytics](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/sites/integrations/integrating-adobe-analytics.html) e [integração do Adobe Target](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/sites/integrations/integrating-adobe-target.html).

* As configurações agora são armazenadas no repositório `/conf` , e não `/etc/cloudsettings` no repositório Experience Manager.

## [!DNL Adobe Experience Manager Assets] como um Cloud Service {#assets}

### What is new in [!DNL Assets] {#what-is-new-assets}

* [!DNL Asset Compute Service] é um serviço dimensionável e extensível para processar ativos. Os administradores podem configurar [!DNL Experience Manager] para chamar aplicativos personalizados criados usando o [!DNL Asset Compute Service]. Os desenvolvedores podem usar o serviço para criar aplicativos personalizados especializados que atendam a casos de uso complexos. Esse serviço da Web pode gerar miniaturas para diferentes tipos de arquivos, renderizações de imagem de alta qualidade de formatos de arquivo Adobe, codificar vídeos (futuros), extrair metadados, extrair texto completo como precursor para indexação e executar um ativo por meio de todos os [!DNL Sensei] serviços disponíveis. consulte [usar microserviços de ativos e perfis](/help/assets/asset-microservices-configure-and-use.md)de processamento.

* A configuração inicial do [!DNL Dynamic Media] in [!DNL Experience Manager] como um Cloud Service é aprimorada para ser mais robusta. Agora, ele fornece o progresso dos processos aos administradores.

* A publicação de ativos para [!DNL Dynamic Media] é simplificada e tornada mais robusta, tornando-a parte integrante do pipeline de processamento de ativos global usando microserviços de ativos e melhorando o backend de publicação em lote.

* As etapas de fluxo de trabalho que não são compatíveis com uma implantação de Cloud Service agora são marcadas com um aviso no editor de modelo [!UICONTROL de] fluxo de trabalho. Além disso, ao executar os workflows existentes no ambiente, as etapas do fluxo de trabalho incompatíveis são ignoradas.

* Os modelos de fluxo de trabalho criados pelos clientes implantados `/conf/global` no projeto Git associado ao ambiente em [!DNL Cloud Manager] são implantados automaticamente `/var` e, portanto, disponíveis em [!DNL Experience Manager]. Os modelos de fluxo de trabalho do produto em `/libs` que foram alterados pelo cliente não são implantados automaticamente para `/var`.

### Erros corrigidos {#assets-bugs-fixed}

* O assistente Mover ativo não é carregado conforme esperado para os ativos incluídos nas Coleções. (CQ-4296756)
* Os valores de `dam:size` e `dam:sha1` são excluídos XMP write-back. (CQ-4237355)
* Ao cancelar a publicação de ativos em massa, [!DNL Brand Portal] gera um erro que sugere que o URI da solicitação é muito longo. (CQ-4299474)

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novidades {#what-is-new-commerce}

AEM Comércio está disponível no Cloud Service.

Consulte [Introdução ao Comércio AEM como Cloud Service](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/commerce/getting-started.html) para obter mais detalhes.

## Componentes principais {#core-components}

### Novidades {#what-is-new-core-components}

Release 2.11.0 of the [AEM Core Components](https://docs.adobe.com/content/help/br/experience-manager-core-components/using/introduction.html) is now available as part of AEM Sites including:

* Introdução de um novo componente [do visualizador de](https://aemcomponents.dev/content/core-components-examples/library/page-authoring/pdf-viewer.html)PDF.

* O suporte para Accelerated Mobile Pages (AMP) dos Componentes principais está disponível. Ele ajuda a produzir experiências mais rápidas do cliente, tornando a página transição instantaneamente ao entrar no site a partir de um resultado de pesquisa móvel do Google, o que melhora a participação do usuário e a SEO.
Consulte Suporte à [AMP para os componentes](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/amp.html) principais para obter mais detalhes.

* Compatibilidade com a versão 1.0.2 da Camada [de dados do cliente](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/data-layer/overview.html)Adobe.

* Correções de erros e melhorias na qualidade do código.

## Cloud Manager {#cloud-manager}

### Data de lançamento {#release-date-cm}

A data de lançamento da versão 2020.7.0 do [!UICONTROL Cloud Manager] é 9 de julho de 2020.

### Novidades {#what-is-new-cloud-manager}

* A página de ambientes foi renovada.

* A página de ambientes hibernados agora mostra um status discreto no Cloud Manager.

* O número de variáveis por ambiente aumentou para 200.

* Os pipelines do Cloud Manager agora oferecem suporte a variáveis e segredos definidos pelo cliente.

   Consulte [Variáveis de pipeline](/help/onboarding/getting-access-to-aem-in-cloud/creating-aem-application-project.md#pipeline-variables) para saber mais.

* Agora há suporte para Repositórios de Maven Privado com vínculo de autenticação.

* O container de build do Cloud Manager agora é compatível com Java 8 e Java 11.
Consulte [Uso do suporte](/help/onboarding/getting-access-to-aem-in-cloud/creating-aem-application-project.md#using-java-support) Java 11 para obter mais detalhes.

### Correções de erros {#bug-fixes-cm}

* Devido a um erro, o link do Cloud Manager para o Console do desenvolvedor estava ativo antes dos ambientes serem totalmente criados.

* O link direto do Cloud Manager para o Console do desenvolvedor não exibia a opção de desibernar/hibernar para ambientes do Programa de sandbox.

* As opções **Cancelar** e **Salvar** nem sempre estavam visíveis na página de edição do pipeline de não produção.

* Certas falhas no processo de qualidade do código podiam resultar na geração incorreta do arquivo de log.

* Às vezes, o nome sugerido na criação de um novo programa retornava um duplicado de um nome de programa existente.

* Grandes logs de etapas de pipeline não podiam ser baixados consistentemente pela interface do usuário.

* A validação de nomes de ambientes apresentava um erro off-by-one.

* A página Ambientes às vezes mostrava segmentos do Publish e do Dispatcher sem que estivessem presentes.

### Problemas conhecidos {#known-issues}

* Devido a uma mudança na forma como a cobertura de código é calculada, a versão *mínima* do plug-in Jacoco agora é a 0.7.5.201505241946 (lançada em maio de 2015). Os clientes que referenciam explicitamente uma versão mais antiga recebem uma mensagem de erro no processo de qualidade do código.

## Adobe Experience Manager as a Cloud Service Foundation {#cloud-foundation}

### Novidades {#what-is-new-foundations}

* [Os registros podem ser encaminhados para contas](/help/implementing/developing/introduction/logging.md#splunk-logs)de partes separadas, o que permite que as organizações aproveitem seu investimento de partes.

* [Um endereço](/help/implementing/developing/introduction/development-guidelines.md#dedicated-egress-ip-address) IP de saída estático e dedicado pode ser atribuído para tráfego externo programado no código Java, que pode ser útil para algumas integrações.

* AEM da interface do usuário do serviço de nuvem do Analytics da interface clássica para a nova interface do AEM. Além disso, a localização do serviço em nuvem do Analytics AEM repositório foi movida de `/etc` para `/conf`, para alinhar com outros serviços em nuvem do AEM.

* AEM interface do usuário do serviço em nuvem do Público alvo da interface clássica para a nova interface do usuário AEM. Também foi movida a localização do serviço de nuvem de Público alvo em AEM repositório de `/etc` para `/conf`, para alinhar com outros serviços de nuvem do AEM.

## Cloud Readiness Analyzer {#cloud-readiness-analyzer}

Siga esta seção para saber mais sobre as novidades e as atualizações do Cloud Readiness Analyzer versão v1.0.2.

### Correções de erros {#cra-bug-fixes}

* Não foi possível executar a versão anterior do CRA no Adobe Experience Manager (AEM) 6.1. Foi adicionado suporte direto para permitir usuários no grupo de administradores.

   Consulte [Instalação do CRA no AEM 6.1](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/moving/cloud-migration/cloud-readiness-analyzer/using-cloud-readiness-analyzer.html#installing-on-aem61) para obter mais detalhes.

* O carimbo de data e hora de expiração exibido no relatório de resumo estava incorreto.

* O CRA estava detectando componentes personalizados duplicados.

* No AEM 6.1, a inspeção de conteúdo era encerrada antes de concluir a inspeção completa. Adição de um gerenciamento de exceções para permitir que o inspetor pule e continue até que a inspeção completa seja concluída.
