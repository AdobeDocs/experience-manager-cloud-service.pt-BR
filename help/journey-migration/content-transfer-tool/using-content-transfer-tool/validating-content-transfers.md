---
title: Validar transferências de conteúdo
description: Usar a ferramenta Transferência de conteúdo para validar as transferências de conteúdo
exl-id: a12059c3-c15a-4b6d-b2f4-df128ed0eea5
feature: Migration
role: Admin
source-git-commit: 9b05ed38e8eb337b3a07ee2051c6a0d530088af2
workflow-type: tm+mt
source-wordcount: '1220'
ht-degree: 1%

---


# Validar transferências de conteúdo {#validating-content-transfers}

## Introdução {#getting-started}

Os usuários podem determinar com confiança se todo o conteúdo que foi extraído pela ferramenta Transferência de conteúdo foi assimilado com êxito na instância de destino. Esse recurso de validação funciona comparando um resumo dos caminhos de todos os nós envolvidos durante a extração, com um resumo dos caminhos de todos os nós envolvidos durante a assimilação. Se houver caminhos de nó incluídos no resumo de extração que estejam ausentes no resumo de assimilação, a validação será considerada como tendo falhado, e talvez seja necessária uma validação manual adicional.

>[!INFO]
>
>Esse recurso estará disponível a partir da versão 1.8.x da Ferramenta de transferência de conteúdo (CTT). O ambiente de destino do AEM Cloud Service deve estar executando a versão 6158 ou superior. Também requer que o ambiente de origem seja configurado para executar a [pré-cópia](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md#setting-up-pre-copy-step). O recurso de validação procura o arquivo azcopy.config na origem. Se não encontrar esse arquivo, a validação não será executada. Para saber mais sobre como configurar um arquivo azcopy.config, consulte [Lidar com repositórios de conteúdo grandes - Configurar um arquivo azcopy.config](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md#configure-azcopy-config-file).

A validação de uma transferência de conteúdo é um recurso opcional. Habilitar esse recurso aumentará o tempo necessário para executar uma extração e uma assimilação. Para usar o recurso, ative-o no Console do sistema do ambiente do AEM de origem seguindo estas etapas:

1. Navegue até o Console da Web do Adobe Experience Manager na instância de origem, acessando **Ferramentas - Operações - Console da Web** ou diretamente para a URL em *https://serveraddress:serverport/system/console/configMgr*
1. Pesquisar por **Configuração do serviço de extração da ferramenta de transferência de conteúdo**
1. Use o botão de ícone de lápis para editar seus valores de configuração
1. Habilite a configuração **Habilitar Validação de Migração durante a extração** e pressione **Salvar**:

   ![imagem](/help/journey-migration/content-transfer-tool/assets/CTTvalidation1.png)

Com essa configuração ativada e com o ambiente do AEM Cloud Service de destino executando uma versão compatível, a validação da migração ocorrerá durante toda a extração e assimilações subsequentes.

Para obter mais informações sobre como instalar a Ferramenta de transferência de conteúdo, consulte [Introdução à Ferramenta de transferência de conteúdo](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/getting-started-content-transfer-tool.md).

## Como validar uma transferência de conteúdo {#how-to-validate-a-content-transfer}

Com a validação de migração ativada no ambiente do AEM de origem, comece uma extração.

Se **Substituir o contêiner de preparação durante a extração** estiver habilitado, todos os nós envolvidos na extração serão registrados no resumo do caminho de extração. Quando essa configuração é usada, é importante habilitar a configuração **Limpar conteúdo existente na instância da nuvem antes de assimilar** durante a assimilação, caso contrário, pode parecer que faltam nós no resumo da assimilação. Esses são os nós que já estão presentes no target nas assimilações anteriores.

Para obter uma ilustração gráfica, consulte os seguintes exemplos:

### Exemplo 1 {#example-1}

* **Extração (Substituir)**

  ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/example1-extraction.png)

* **Assimilação (Apagar)**

  ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/validation-02.png)

* **Notas**

  Essa combinação de &quot;Substituir&quot; e &quot;Limpar&quot; resultará em resultados de validação consistentes, mesmo para assimilações repetidas.

### Exemplo 2 {#example-2}

* **Extração**

  ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/example2-extraction.png)

* **Assimilação**

  ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/validation-04.png)

* **Notas**

  Essa combinação de &quot;Substituir&quot; e &quot;Limpar&quot; resultará em resultados de validação consistentes para a assimilação inicial.

  Se a assimilação for repetida, o resumo da assimilação fica vazio e a validação parece ter falhado. O resumo de assimilação está vazio porque todos os nós desta extração já estarão presentes no destino.

Quando a extração estiver concluída, comece a assimilação.

A parte superior do log de assimilação conterá uma entrada, semelhante a `aem-ethos/tools:1.2.438`. Verifique se o número da versão é **1.2.438** ou superior; caso contrário, a versão do AEM as a Cloud Service que você está usando não oferece suporte à validação.

Depois que a assimilação estiver concluída e a validação estiver começando, a seguinte entrada de log será anotada no log de assimilação:

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

Este é um exemplo de validação bem-sucedida, pois não havia entradas ausentes no resumo de assimilação presentes no resumo da extração.

Para comparar, veja a seguir como um relatório de validação seria exibido se a validação falhasse (ou se uma migração complementar fosse executada):

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
See our Migration Validation FAQ (https://www.adobe.com/go/aem_cloud_ctt_validation_en) or open a ticket with Customer Care.
There are 4635 entries present in the extraction digest that are missing from the ingestion digest.
/content/dam/bruce
/content/dam/bruce-assets
... more paths listed (up to 10k) ...
----------------------------------------------------------
Comparing the path digests took 0 seconds
Migration validation took 0 minutes
```

O exemplo de falha acima foi obtido executando uma assimilação e, em seguida, executando novamente a mesma assimilação com Limpar desativado, de modo que nenhum nó estivesse envolvido durante a assimilação — tudo já estava presente no destino.

Além de ser incluído no log de assimilação, o relatório de validação também pode ser acessado da interface do usuário **Trabalhos de assimilação** no Cloud Acceleration Manager. Para fazer isso, clique nos três pontos (**...**) e clique em **Relatório de validação** no menu suspenso para exibir o relatório de validação.


![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/CTTvalidationreportnew.png)

## Como validar a migração principal {#how-to-validate-group-migration}

Consulte [Migração de Grupos](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/group-migration.md) para ler os detalhes da migração principal e por que ela é necessária.

Depois que a extração e a assimilação forem concluídas com êxito, um resumo e um relatório da migração principal estarão disponíveis. Essas informações podem ser usadas para validar quais grupos foram migrados com êxito e, talvez, para determinar por que alguns não foram migrados.

Para exibir essas informações, acesse Cloud Acceleration Manager. Clique no cartão do projeto e no cartão Transferência de conteúdo. Navegue até **Trabalhos de assimilação** e localize a assimilação que você deseja verificar. Clique nos três pontos (**...**) dessa assimilação e clique em **Exibir resumo da entidade** na lista suspensa.

![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-principal-action.png)

Você verá uma caixa de diálogo com as informações de resumo. Use os ícones de ajuda para ler uma descrição mais completa. Para baixar o Relatório de Migração de Entidade de Segurança (CSV) separado por vírgula, selecione **Relatório de Migração de Entidade de Segurança** na lista suspensa em **Baixar um arquivo...** e clique no botão **Download**. Observe também que no final deste relatório está o Relatório do usuário, que pode ser usado para o gerenciamento de usuários após a migração.

![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-principal-dialog.png)

O relatório de migração principal indicará:

* Cada grupo migrado e o primeiro caminho de conteúdo que o acionou; o grupo também pode estar em outros caminhos, mas somente o primeiro encontrado para um determinado grupo é relatado. Ele também relata se foi encontrado em uma ACL ou em uma política CUG.
* Cada grupo migrado como um grupo local terá a palavra &quot;local&quot; indicada na linha do grupo.
* Cada grupo não foi migrado e o motivo da migração.  Normalmente, será por um destes motivos:
   * É um grupo incorporado
   * Já está no sistema de destino
   * Não está em uma política de ACL ou CUG no conteúdo que está sendo migrado
   * Ele tem um campo exclusivo duplicado (um de rep:principalName, rep:authorizableId, jcr:uuid ou rep:externalId já está no destino, mas todos devem ser exclusivos)

## Resolução de problemas {#troubleshooting}

### Falha na validação. E agora? {#validation-fail}

A primeira etapa é determinar se a assimilação realmente falhou ou se o conteúdo extraído já está presente no ambiente de destino. Isso pode ocorrer se uma assimilação for repetida com a opção **Limpar conteúdo existente na instância da nuvem antes de assimilar** desabilitada.

Para verificar, escolha um caminho no relatório de validação e verifique se ele está presente no ambiente de destino. Se esse for um ambiente de publicação, talvez você esteja limitado a verificar as páginas e os ativos diretamente. Abra um tíquete no Atendimento ao cliente se precisar de assistência com esta etapa.

### A contagem de nós é menor do que eu esperava. Por que isso ocorre? {#node-count-lower-than-expected}

Alguns caminhos dos resumos de extração e assimilação são excluídos de propósito para manter o tamanho desses arquivos gerenciável, com o objetivo de poder calcular o resultado da validação de migração dentro de duas horas após a conclusão da assimilação.

Os caminhos que excluímos atualmente dos resumos incluem: `cqdam.text.txt` representações, nós dentro de `/home` e nós dentro de `/jcr:system`.

### Grupos de usuários fechados {#validating-cugs}

Consulte [Migrando Grupos de Usuários Fechados](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/closed-user-groups-migration.md) para considerações adicionais ao usar uma política de Grupo de Usuários Fechado (CUG).
