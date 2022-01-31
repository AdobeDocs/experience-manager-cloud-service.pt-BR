---
title: 'Problemas conhecidos '
description: Práticas recomendadas de comunicações, problemas conhecidos e limitações
source-git-commit: 06da7d2a5063e163aa1534bedbc79ae50ef27515
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 2%

---


# Perguntas frequentes, práticas recomendadas, problemas conhecidos e limitações {#best-practices-known-issues-and-limitations}

Antes de começar a usar as APIs de comunicação, perguntas frequentes, analise os seguintes problemas conhecidos e limitações:

## Problemas conhecidos

- Você pode usar um tipo de renderização específico (PDF, IMPRESSÃO) apenas uma vez na lista de opções de impressão. Por exemplo, você não pode ter duas opções de IMPRESSÃO, cada uma especificando um tipo de renderização PCL.

- Para uma configuração de lote, apenas uma instância da combinação de valores de OutputType(PDF, PRINT) e RenderType(PostScript, PCL, IPL, ZPL, etc.) é permitido.

## Práticas recomendadas    

- O Adobe recomenda hospedar arquivos de dados no armazenamento do contêiner de blob na região de nuvem usada pelo AEM Cloud Service.

## Perguntas frequentes {#faq}

**Posso usar uma pasta monitorada ou outros mecanismos de armazenamento para armazenar entrada e saída?**

No momento, você pode usar o Armazenamento do Microsoft Azure para salvar dados de entrada e documentos gerados. O armazenamento do Microsoft Azure fornece várias opções para [automatizar operações de movimentação de dados](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10).

**Uma conta de armazenamento do Microsoft Azure está incluída na licença do Experience Manager Forms Cloud Service?**

A conta de armazenamento do Microsoft Azure é independente da licença do Experience Manager Forms Cloud Service.

**As APIs do Communication armazenam dados nos servidores do Experience Manager Forms Cloud Service?**

Os dados de entrada e saída são salvos somente no Armazenamento do Microsoft Azure.

**As APIs de comunicação estão disponíveis apenas para o Experience Manager Forms Cloud Service? Posso obter funcionalidade semelhante no ambiente local?**

Você pode usar o serviço AEM Forms Output para combinar um modelo (XFA ou PDF) com dados do cliente para gerar documentos nos formatos PDF, PS, PCL e ZPL.

Em comparação com o ambiente local, o Cloud Service oferece benefícios adicionais de dimensionamento automático e economia de custos.

<!--**Where is data processed?**

**Who has access to data?**

**Is data encrypted?**

**Where is data hosted?** -->

**Posso executar várias operações em lote simultaneamente?**
Sim, você pode executar várias operações em lote de maneira semelhante. Sempre use pastas de origem e de destino diferentes para cada operação para evitar conflitos.
