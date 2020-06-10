---
title: Uso do Cloud Readiness Analyzer
description: Uso do Cloud Readiness Analyzer
translation-type: tm+mt
source-git-commit: 3d818278c53f3d3b4c5b53aa5b78d06d876bf05f
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 0%

---


# Uso do Cloud Readiness Analyzer {#using-cloud-readiness-analyzer}

## Considerações importantes sobre o uso do Cloud Readiness Analyzer {#imp-considerations}

Siga a seção abaixo para entender as considerações importantes ao executar o CRA (Cloud Readiness Analyzer):

* O CRA é compatível com instâncias de AEM de origem com a versão 6.1 e superior.
* O CRA pode ser executado em qualquer ambiente.

   >[!NOTE]
   >Para aumentar a taxa de detecção e evitar qualquer lentidão em instâncias essenciais aos negócios, é recomendável executar a CRA nos ambientes de armazenamento temporário do autor de origem que estejam o mais próximos possível dos de produção nas áreas de personalizações, configurações, conteúdo e aplicativos do usuário. Como alternativa, também pode ser executado em um clone do ambiente de publicação.

## Disponibilidade {#availability}

O CRA (Cloud Readiness Analyzer) pode ser baixado como um arquivo zip do portal de distribuição de software. Você pode instalar o pacote por meio do Gerenciador de pacotes na instância de origem do Adobe Experience Manager (AEM).

>[!NOTE]
>Baixe o CRA (Cloud Readiness Analyzer) de *pendente*.

## Execução do Analisador de disponibilidade da nuvem {#running-tool}

Siga esta seção para saber como executar o Cloud Readiness Analyzer:

1. Selecione o Adobe Experience Manager e navegue até Ferramentas -> **Operações** -> Analisador de prontidão da **nuvem**.

### Exibição dos resultados {#viewing-the-results}

Há duas maneiras de visualização da saída do CRA:

1. Uso do relatório organizado

   >[!NOTE]
   >O relatório organizado está disponível no AEM versão 6.3 e superior.

Consulte Planejamento e Status do Documento CRA para descrever os níveis de importância no relatório

1. Exibir a saída do CRA (pode ser usado com o AEM versão 6.1 e superior):

   1. Navegue até o console da Web do AEM.

   1. Selecione Status - Analisador de prontidão para nuvem, conforme mostrado na imagem abaixo.

#### Como entender os níveis de importância no relatório {#importance-levels}

A tabela a seguir descreve o significado dos vários níveis de importância do Detector de padrões e do Analisador de prontidão da nuvem.

| Nível de importância | Descrição |
|--- |--- |
| INFORMAÇÃO/0 | Esta constatação é fornecida para fins informativos. |
| CONSULTIVO/1 | Essa descoberta pode ser um problema de atualização. Recomenda-se uma investigação mais aprofundada. |
| MAJOR/2 | Essa descoberta provavelmente será um problema de atualização que deve ser resolvido. |
| CRÍTICO/3 | Essa descoberta provavelmente será um problema de atualização que deve ser resolvido para evitar perda de função ou desempenho. |