---
title: Validar transferências de conteúdo
description: Use a ferramenta Transferência de conteúdo para validar transferências de conteúdo
exl-id: a12059c3-c15a-4b6d-b2f4-df128ed0eea5
source-git-commit: b6c9d7411e84b18926aa525efe25296002c2d3d2
workflow-type: tm+mt
source-wordcount: '890'
ht-degree: 2%

---

# Validar transferências de conteúdo {#validating-content-transfers}

## Introdução {#getting-started}

Os usuários têm a capacidade de determinar de forma confiável se todo o conteúdo que foi extraído pela ferramenta Transferência de conteúdo foi assimilado com êxito na instância de destino. Esse recurso de validação funciona comparando um resumo dos caminhos de todos os nós envolvidos durante a extração, com um resumo dos caminhos de todos os nós envolvidos durante a assimilação. Se houver caminhos de nó incluídos no resumo de extração que estejam ausentes no resumo de assimilação, a validação será considerada como uma falha e poderá ser necessária uma validação manual adicional.

>[!INFO]
>
>Esse recurso estará disponível a partir da versão 1.8.x da Ferramenta de transferência de conteúdo (CTT). O ambiente de destino do AEM Cloud Service deve estar em execução pelo menos na versão 6158 ou posterior. Também requer que o ambiente de origem seja configurado para execução [pré-cópia](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md#setting-up-pre-copy-step). O recurso de validação procura o arquivo azcopy.config na origem. Se ele não encontrar esse arquivo, a validação não será executada. Para saber mais sobre como configurar um arquivo azcopy.config, consulte [esta página](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md#configure-azcopy-config-file).

Validar uma transferência de conteúdo é um recurso opcional. Ativar esse recurso aumentará o tempo necessário para executar uma extração e uma assimilação. Para usar o recurso, ative-o no Console do sistema do ambiente de origem AEM seguindo estas etapas:

1. Navegue até o Adobe Experience Manager Web Console na instância de origem, acessando **Ferramentas - Operações - Console da Web** ou diretamente para o URL em *https://serveraddress:serverport/system/console/configMgr*
1. Procurar por **Configuração do serviço de extração da ferramenta de transferência de conteúdo**
1. Use o botão de ícone de lápis para editar seus valores de configuração
1. Ative o **Habilitar validação de migração durante a extração** e pressione **Salvar**:

   ![imagem](/help/journey-migration/content-transfer-tool/assets/CTTvalidation1.png)

Com essa configuração ativada e o ambiente AEM Cloud Service de destino executando uma versão compatível, a validação da migração ocorrerá durante toda a extração e assimilações subsequentes.

Para obter mais informações sobre como instalar a ferramenta Transferência de conteúdo, consulte [Introdução à ferramenta Transferência de conteúdo](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/getting-started-content-transfer-tool.md).

## Como validar uma transferência de conteúdo {#how-to-validate-a-content-transfer}

Com a validação de migração ativada no ambiente de AEM de origem, inicie uma extração.

If **Substituir contêiner de preparação durante a extração** estiver habilitado, todos os nós envolvidos com a extração serão registrados no resumo do caminho de extração. Quando essa configuração for usada, é importante ativar a variável **Limpar o conteúdo existente na instância do Cloud antes da assimilação** durante a ingestão, caso contrário, pode parecer que há nós ausentes no resumo da ingestão. Esses são os nós que já estão presentes no target a partir de ingestões anteriores.

Para obter uma ilustração gráfica, consulte os exemplos abaixo:

### Exemplo 1 {#example-1}

* **Extração (Substituir)**

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/validation-01.png)

* **Assimilação (Varrer)**

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/validation-02.png)

* **Notas**

   Essa combinação de &quot;Substituir&quot; e &quot;Limpar&quot; resultará em resultados de validação consistentes, mesmo para ingestões repetidas.

### Exemplo 2 {#example-2}

* **Extração**

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/validation-03.png)

* **Assimilação**

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/validation-04.png)

* **Notas**

   Essa combinação de &quot;Substituir&quot; e &quot;Limpar&quot; resultará em resultados de validação consistentes para a assimilação inicial.

   Se a assimilação for repetida, o resumo da assimilação estará vazio e a validação parecerá ter falhado. O resumo de assimilação estará vazio porque todos os nós dessa extração já estarão presentes no target.

Uma vez concluída a extração, comece a ingestão.

A parte superior do log de assimilação conterá uma entrada, semelhante a `aem-ethos/tools:1.2.438`. Certifique-se de que este número de versão esteja **1.2.438** ou superior, caso contrário, a validação não será suportada pela versão de AEM as a Cloud Service que você está usando.

Quando a assimilação estiver concluída e a validação estiver sendo iniciada, a seguinte entrada de log será anotada no log de assimilação:

```
Gathering artifacts for migration validation...  
```

Os detalhes da validação seguirão esta entrada. Encontre um exemplo de uma grande migração abaixo:

```
Beginning publish migration validation. Migration job id=[3aba1f96-84b6-4bd0-8642-c61c0d528387]
Extraction path digest is being processed...
Extraction path digest processing took 982 seconds
Ingestion path digest is being processed...
Ingestion path digest processing took 999 seconds
Comparing the Extraction and Ingestion path digests...
----------------------------------------------------------
EXTRACTION: Number of nodes extracted: 51674784
INGESTION: Number of nodes ingested: 51674784
----------------------------------------------------------
Validation succeeded! No entries were detected to be missing from the ingestion digest.
----------------------------------------------------------
Comparing the path digests took 29 seconds
Migration validation took 33 minutes
```

Este é um exemplo de validação que foi bem-sucedida, pois não havia entradas ausentes no resumo de assimilação que estivessem presentes no resumo da extração.

Para comparar, veja como seria um relatório de validação se a validação falhasse:

```
Beginning publish migration validation. Migration job id=[ac217e5a-a08d-4e81-cbd6-f39f88b174ce]
Extraction path digest is being processed...
Extraction path digest processing took 0 seconds
Ingestion path digest is being processed...
Ingestion path digest processing took 0 seconds
Comparing the Extraction and Ingestion path digests...
----------------------------------------------------------
EXTRACTION: Number of nodes extracted: 4635
INGESTION: Number of nodes ingested: 0
----------------------------------------------------------
Validation failed. However, the following nodes may already be present in the target environment.
Please refer to our Migration Validation FAQ (https://www.adobe.com/go/aem_cloud_ctt_validation_en) or open a ticket with Customer Care.
There are 4635 entries present in the extraction digest that are missing from the ingestion digest.
/content/dam/bruce
/content/dam/bruce-assets
... more paths listed (up to 10k) ...
----------------------------------------------------------
Comparing the path digests took 0 seconds
Migration validation took 0 minutes
```

O exemplo de falha acima foi obtido executando uma assimilação e, em seguida, executando novamente a mesma assimilação com a Varrer desativada, de modo que nenhum nó foi envolvido durante a assimilação — tudo já estava presente no destino.

Além de ser incluído no log de assimilação, o relatório de validação também pode ser acessado do **Trabalhos de assimilação** interface do usuário no Cloud Acceleration Manager. Para fazer isso, clique nos três pontos (**...**) e clique em **Relatório de validação** na lista suspensa para exibir o relatório de validação.


![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/CTTvalidationreportnew.png)

## Resolução de problemas {#troubleshooting}

### Falha na validação. E agora? {#validation-fail}

A primeira etapa é determinar se a assimilação realmente falhou ou se o conteúdo extraído já está presente no ambiente de destino. Isso pode ocorrer se uma ingestão for repetida com o **Limpar o conteúdo existente na instância do Cloud antes da assimilação** opção desabilitada.

Para verificar, escolha um caminho no relatório de validação e verifique se ele está presente no ambiente de destino. Se este for um ambiente de publicação, você pode se limitar a verificar páginas e ativos diretamente. Abra um ticket no Atendimento ao cliente se precisar de assistência com esta etapa.

### A contagem de nós é inferior à que eu esperava. Por que isso ocorre? {#node-count-lower-than-expected}

Alguns caminhos dos digests de extração e assimilação são excluídos com o objetivo de manter o tamanho desses arquivos gerenciável, com o objetivo de poder calcular o resultado da validação da migração dentro de duas horas após a conclusão da assimilação.

Os caminhos que atualmente excluímos dos digests incluem: `cqdam.text.txt` representações, nós em `/home`e nós dentro de `/jcr:system`.
