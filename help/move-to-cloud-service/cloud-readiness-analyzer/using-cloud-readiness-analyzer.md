---
title: Uso do Cloud Readiness Analyzer
description: Uso do Cloud Readiness Analyzer
translation-type: tm+mt
source-git-commit: 1739f81d4894f3e04cc4119f344a3bea5bd042d8
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 1%

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

   ![image](/help/move-to-cloud-service/cloud-readiness-analyzer/assets/cra-1.png)

1. Após clicar em **Cloud Readiness Analyzer**, os start de ferramenta que geram o relatório e, após alguns minutos, o relatório de resumo estará disponível na sua instância do AEM.

   >[!NOTE]
   >Será necessário rolar a página para baixo para visualização do relatório completo.

   ![image](/help/move-to-cloud-service/cloud-readiness-analyzer/assets/cra-2.png)

### Exibição dos resultados no relatório resumido {#viewing-the-results}

>[!IMPORTANT]
>Os relatórios gerados pelo Cloud Readiness Analyzer são baseados nos Detectores de padrão. Consulte Detectores de [padrões](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/upgrading/pattern-detector.html) para obter mais detalhes.

Depois de rolar a página para baixo para visualização do relatório de resumo completo, você poderá ver as seguintes informações para cada categoria realçada no relatório:

1. **Nível de importância**

   A tabela a seguir descreve o significado dos vários níveis de importância do Detector de padrões e do Analisador de prontidão da nuvem.

   | Nível de importância | Descrição |
   |--- |--- |
   | INFORMAÇÃO/0 | Esta constatação é fornecida para fins informativos. |
   | CONSULTIVO/1 | Essa descoberta pode ser um problema de atualização. Recomenda-se uma investigação mais aprofundada. |
   | MAJOR/2 | Essa descoberta provavelmente será um problema de atualização que deve ser resolvido. |
   | CRÍTICO/3 | Essa descoberta provavelmente será um problema de atualização que deve ser resolvido para evitar perda de função ou desempenho. |

1. **Descrição** A descrição fornece informações sobre a categoria reportada.

1. **URL** da documentação O URL da documentação permite que você visualização a documentação técnica do tipo associado.

1. **Mensagem** Uma descrição da descoberta em uma única mensagem.

### Exibição dos resultados em um formato CSV {#viewing-the-results-csv}

O relatório de resumo está disponível na interface do usuário do AEM. Você pode baixar o relatório completo em um formato CSV (valores separados por vírgula) que seja útil durante o processo de refatoração.

Siga as etapas abaixo para gerar um formato CSV do seu relatório de resumo:

1. 
   1. Selecione o Adobe Experience Manager e navegue até Ferramentas -> **Operações** -> Analisador de prontidão da **nuvem**.

1. Quando o relatório estiver disponível, clique em **CSV** para baixar o relatório de resumo completo no formato CSV (valores separados por vírgula), como mostrado na figura abaixo.

![image](/help/move-to-cloud-service/cloud-readiness-analyzer/assets/cra-3.png)


#### Exibição do relatório em instâncias do AEM 6.1 {#aem-instances-report}

Siga as etapas abaixo para baixar o relatório CSV do Adobe Experience Manager (AEM) 6.1:

1. Navegue até **Adobe Experience Manager Web ConsoleConfiguração** usando `https://serveraddress:serverport/system/console/configMgr`.

1. Selecione a guia **Status** e procure **Pattern Detector** na lista suspensa, como mostrado na figura abaixo.

   ![image](/help/move-to-cloud-service/cloud-readiness-analyzer/assets/cra-4.png)

1. Você pode baixar o relatório de resumo em uma pasta zip ou em um formato JSON.


