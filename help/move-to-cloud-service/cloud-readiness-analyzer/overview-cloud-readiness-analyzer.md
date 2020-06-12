---
title: Visão geral do Cloud Readiness Analyzer
description: Visão geral do Cloud Readiness Analyzer
translation-type: tm+mt
source-git-commit: f0e69dba5d670d141c82e762069f4831c2527dbe
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---


# Visão geral {#overview-cloud-readiness-analyzer}

O Cloud Readiness Analyzer ajuda a acelerar os processos de avaliação da prontidão para passar de uma implantação existente do Adobe Experience Manager (AEM) para o AEM como um serviço em nuvem.

Essa ferramenta gera um relatório que identifica áreas de potencial refatoração, que é o primeiro passo na jornada de transição para o AEM como um serviço em nuvem.

## Relatório de resumo no Cloud Readiness Analyzer {#summary-report}

O relatório resumido do Analisador de disponibilidade em nuvem é usado para obter um alto nível de compreensão da disponibilidade geral de atualização. O relatório consiste em descobertas em categorias de problemas que devem ser solucionados antes de uma implantação bem-sucedida no AEM como um serviço em nuvem.

O relatório de resumo inclui as seguintes categorias:

* Funcionalidade do aplicativo que deve ser refatorizada
* Itens do repositório que devem ser movidos para um local suportado
* Diálogos e componentes herdados da interface do usuário que devem ser modernizados
* Problemas de implantação e configuração
* Recursos do AEM 6.x que foram substituídos por novas funcionalidades ou que não são suportados no momento no AEM como um serviço em nuvem

Informações adicionais sobre as categorias e possíveis implicações e soluções associadas a essas categorias são fornecidas por meio de links no relatório resumido.

>[!NOTE]
>O relatório do Analisador de prontidão da nuvem acelera o processo de estimar o tempo e o custo necessários para a transição ao AEM como um serviço da nuvem, fornecendo informações que, de outra forma, precisariam ser coletadas e avaliadas manualmente.

Você também pode baixar o relatório de resumo da interface do usuário do AEM. Consulte **Visualização dos resultados em um formato** CSV para obter mais detalhes pendentes.