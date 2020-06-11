---
title: Uso do Cloud Readiness Analyzer
description: Uso do Cloud Readiness Analyzer
translation-type: tm+mt
source-git-commit: 47773a56f8bb24342281068a8c4d03d6edfb9277
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 0%

---


# Uso do Cloud Readiness Analyzer {#using-cloud-readiness-analyzer}

## Considerações importantes sobre o uso do Cloud Readiness Analyzer {#imp-considerations}

Siga a seção abaixo para entender as considerações importantes ao executar o CRA (Cloud Readiness Analyzer):

* O CRA é compatível com instâncias de AEM de origem com a versão 6.1 e superior
* O CRA pode ser executado em qualquer ambiente (de preferência, *Stage* ambiente)

   >[!NOTE]
   >Para aumentar a taxa de detecção e evitar qualquer lentidão em instâncias essenciais aos negócios, é recomendável executar a CRA nos ambientes de armazenamento temporário do autor de origem que estejam o mais próximos possível dos de produção nas áreas de personalizações, configurações, conteúdo e aplicativos do usuário. Como alternativa, também pode ser executado em um clone do ambiente *Publicar* .

## Disponibilidade {#availability}

O Analisador de disponibilidade em nuvem pode ser baixado como um arquivo zip do portal de distribuição de software. Você pode instalar o pacote por meio do Gerenciador de pacotes na instância de origem do Adobe Experience Manager (AEM).

>[!NOTE]
>Baixe o Cloud Readiness Analyzer do Portal de distribuição de software *pendente*.

## Execução do Analisador de disponibilidade da nuvem {#running-tool}

Siga esta seção para saber como executar o Cloud Readiness Analyzer:

1. Selecione o Adobe Experience Manager e navegue até Ferramentas -> **Operações** -> Analisador de prontidão da **nuvem**.

### Exibição dos resultados {#viewing-the-results}

>[!IMPORTANT]
>Os relatórios gerados pelo Cloud Readiness Analyzer são baseados nos Detectores de padrão. Consulte Detectores de [padrões](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/upgrading/pattern-detector.html) para obter mais detalhes.

Há duas maneiras de visualização da saída do Analisador de prontidão da nuvem:

1. **Usando o Relatório Organizado**

   >[!NOTE]
   >O relatório organizado está disponível no AEM versão 6.3 e superior.

   Ou,

1. **Visualização da saída do CRA**

   Siga as etapas abaixo para visualização da saída do Analisador de prontidão da nuvem:

   >[!NOTE]
   >As etapas abaixo são aplicáveis ao AEM versão 6.1 e superior.

   1. Navegue até **AEM Web Console** usando `https://serveraddress:serverport/system/console/configMgr`.

   1. Select **Status (Selecionar status) - Detector** de padrões, conforme mostrado na figura abaixo.

#### Exibição do relatório em instâncias do AEM 6.1 {#aem-instances-report}

Você pode baixar o relatório csv para o AEM 6.1.Isso está pendente.

#### Como entender os níveis de importância no relatório {#importance-levels}

A tabela a seguir descreve o significado dos vários níveis de importância do Detector de padrões e do Analisador de prontidão da nuvem.

| Nível de importância | Descrição |
|--- |--- |
| INFORMAÇÃO/0 | Esta constatação é fornecida para fins informativos. |
| CONSULTIVO/1 | Essa descoberta pode ser um problema de atualização. Recomenda-se uma investigação mais aprofundada. |
| MAJOR/2 | Essa descoberta provavelmente será um problema de atualização que deve ser resolvido. |
| CRÍTICO/3 | Essa descoberta provavelmente será um problema de atualização que deve ser resolvido para evitar perda de função ou desempenho. |