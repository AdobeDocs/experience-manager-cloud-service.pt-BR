---
title: Visão geral do Cloud Readiness Analyzer
description: Visão geral do Cloud Readiness Analyzer
translation-type: tm+mt
source-git-commit: 64b685a7c9fbb105ed66dc4b3212b2bf91dee4af
workflow-type: tm+mt
source-wordcount: '262'
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

O relatório de resumo está disponível na interface do usuário do AEM. Existe uma opção para baixar o relatório completo em um formato CSV (valores separados por vírgula) que é útil durante o processo de refatoração.