---
title: Notas de versão do Adobe Experience Manager as a Cloud Service 2020.7.0
description: Notas de versão do Experience Manager para 2020.7.0
translation-type: tm+mt
source-git-commit: 22a025b49444e08d014e0459443751b5a3cfc7bf
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 20%

---


# Notas de versão do AEM as a Cloud Service 2020.7.0{#release-notes}

A seção a seguir descreve as Notas de versão gerais do Experience Manager as a Cloud Service 2020.7.0.

## Novidades do Cloud Manager {#cloud-manager}

Consulte esta seção para saber mais sobre as novidades e atualizações do Cloud Manager no AEM as a Cloud Service, versão 2020.7.0.

### Data de lançamento {#release-date}

A data de lançamento da versão 2020.7.0 do [!UICONTROL Cloud Manager] é 9 de julho de 2020.

### Novidades {#what-is-new-cloud-manager}

* A página ambientes foi reprojetada.

* ambientes hibernados agora mostram um status discreto no Cloud Manager quando hibernados.

* O número de variáveis de ambiente por ambiente aumentou para 200.

* O container de criação do Cloud Manager agora é compatível com Java 8 e Java 11.

### Correções de erros {#bug-fixes-cm}

* O link do Gerenciador de nuvem para o Console do desenvolvedor estava incorretamente ativo antes dos ambientes serem totalmente criados.

* O link para o Console do desenvolvedor diretamente do Gerenciador de nuvem não exibia a opção de cancelar a hibernação/hibernar um ambiente do Programa do Sandbox.

* As opções **Cancelar** e **Salvar** na página de edição do Pipeline de não produção nem sempre estavam visíveis.

* Certas falhas no processo de qualidade do código podem resultar na não geração correta do arquivo de log.

* Ao criar um novo programa, o nome sugerido às vezes retornaria um duplicado de um nome de programa existente.

* Alguns grandes logs de etapas de pipeline não puderam ser baixados consistentemente pela interface do usuário.

* A validação de nomes de ambientes apresentou um erro &quot;off-by-one&quot;.

* A página Ambientes às vezes mostrava segmentos de publicação e despachante quando nenhum estava presente.

## Novidades do Cloud Readiness Analyzer {#cloud-readiness-analyzer}

Siga esta seção para saber mais sobre as novidades e as atualizações do Cloud Readiness Analyzer.

### Correções de erros {#cra-bug-fixes}

* Não foi possível executar a versão anterior do CRA no Adobe Experience Manager (AEM) 6.1. Foi adicionado suporte explícito para permitir usuários no grupo de administradores.

   Consulte [Instalação do CRA no AEM 6.1](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/moving/cloud-migration/cloud-readiness-analyzer/using-cloud-readiness-analyzer.html#installing-on-aem61) para obter mais detalhes.

* O carimbo de data e hora de expiração exibido no relatório de resumo estava incorreto.

* O CRA estava detectando componentes personalizados do duplicado.

* No AEM 6.1, a inspeção de conteúdo era encerrada antes de concluir a inspeção completa. Foi adicionada a manipulação de exceções para permitir que o inspetor pule e continue até que a inspeção completa seja concluída.

