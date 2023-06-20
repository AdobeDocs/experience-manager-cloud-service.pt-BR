---
title: Validar transferências de conteúdo
description: Usar a ferramenta Transferência de conteúdo para validar as transferências de conteúdo
exl-id: a12059c3-c15a-4b6d-b2f4-df128ed0eea5
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '1062'
ht-degree: 2%

---

# Validar transferências de conteúdo {#validating-content-transfers}

## Introdução {#getting-started}

Os usuários podem determinar com confiança se todo o conteúdo que foi extraído pela ferramenta Transferência de conteúdo foi assimilado com sucesso na instância de destino. Esse recurso de validação funciona comparando um resumo dos caminhos de todos os nós envolvidos durante a extração, com um resumo dos caminhos de todos os nós envolvidos durante a assimilação. Se houver caminhos de nó incluídos no resumo de extração que estejam ausentes no resumo de assimilação, a validação será considerada como tendo falhado, e talvez seja necessária uma validação manual adicional.

>[!INFO]
>
>Esse recurso estará disponível a partir da versão 1.8.x da Ferramenta de transferência de conteúdo (CTT). O ambiente de destino do AEM Cloud Service deve estar em execução na versão 6158 ou superior. Também requer que o ambiente de origem seja configurado para ser executado [pré-cópia](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md#setting-up-pre-copy-step). O recurso de validação procura o arquivo azcopy.config na origem. Se não encontrar esse arquivo, a validação não será executada. Para saber mais sobre como configurar um arquivo azcopy.config, consulte [esta página](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md#configure-azcopy-config-file).

A validação de uma transferência de conteúdo é um recurso opcional. Habilitar esse recurso aumentará o tempo necessário para executar uma extração e uma assimilação. Para usar o recurso, ative-o no Console do sistema do ambiente AEM de origem seguindo estas etapas:

1. Navegue até o Console da Web do Adobe Experience Manager na instância de origem, acessando **Ferramentas - Operações - Console da Web** ou diretamente para o URL em *https://serveraddress:serverport/system/console/configMgr*
1. Pesquisar por **Configuração do serviço de extração da ferramenta Transferência de conteúdo**
1. Use o botão de ícone de lápis para editar seus valores de configuração
1. Ativar o **Ativar validação de migração durante a extração** , depois pressione **Salvar**:

   ![imagem](/help/journey-migration/content-transfer-tool/assets/CTTvalidation1.png)

Com essa configuração ativada e o ambiente AEM Cloud Service de destino executando uma versão compatível, a validação da migração ocorrerá durante toda a extração e assimilação seguintes.

Para obter mais informações sobre como instalar a ferramenta Transferência de conteúdo, consulte [Introdução à ferramenta Transferência de conteúdo](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/getting-started-content-transfer-tool.md).

## Como validar uma transferência de conteúdo {#how-to-validate-a-content-transfer}

Com a validação da migração ativada no ambiente AEM de origem, comece uma extração.

Se **Substituir container de preparo durante a extração** estiver ativado, todos os nós envolvidos na extração serão registrados no resumo do caminho de extração. Quando essa configuração for usada, é importante ativar o **Apagar conteúdo existente na instância da nuvem antes da assimilação** configuração durante a assimilação, caso contrário, pode parecer que faltam nós no resumo da assimilação. Esses são os nós que já estão presentes no target nas assimilações anteriores.

Para obter uma ilustração gráfica, consulte os exemplos abaixo:

### Exemplo 1 {#example-1}

* **Extração (Substituir)**

  ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/validation-01.png)

* **Assimilação (Varrer)**

  ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/validation-02.png)

* **Notas**

  Essa combinação de &quot;Substituir&quot; e &quot;Limpar&quot; resultará em resultados de validação consistentes, mesmo para assimilações repetidas.

### Exemplo 2 {#example-2}

* **Extração**

  ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/validation-03.png)

* **Assimilação**

  ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/validation-04.png)

* **Notas**

  Essa combinação de &quot;Substituir&quot; e &quot;Limpar&quot; resultará em resultados de validação consistentes para a assimilação inicial.

  Se a assimilação for repetida, o resumo da assimilação fica vazio e a validação parece ter falhado. O resumo de assimilação está vazio porque todos os nós desta extração já estarão presentes no destino.

Quando a extração estiver concluída, comece a assimilação.

A parte superior do log de assimilação conterá uma entrada, semelhante a `aem-ethos/tools:1.2.438`. Certifique-se de que esse número de versão seja **1.2.438** ou superior, caso contrário, a validação não será suportada pela versão do AEM as a Cloud Service que você está usando.

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

Para comparar, veja a seguir como um relatório de validação seria exibido se a validação falhasse:

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

O exemplo de falha acima foi obtido executando uma assimilação e, em seguida, executando novamente a mesma assimilação com Limpar desativado, de modo que nenhum nó estivesse envolvido durante a assimilação — tudo já estava presente no destino.

Além de ser incluído no log de assimilação, o relatório de validação também pode ser acessado no **Tarefas de assimilação** no Cloud Acceleration Manager. Para fazer isso, clique nos três pontos (**..**) e clique em **Relatório de validação** no menu suspenso para exibir o relatório de validação.


![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/CTTvalidationreportnew.png)

## Como validar a migração principal {#how-to-validate-principal-migration}

Consulte [Mapeamento de usuários e migração de entidade de segurança](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/user-mapping-and-migration.md) para ler os detalhes das migrações principais e por que isso é necessário.

Depois que a extração e a assimilação forem concluídas com êxito, um resumo e um relatório da migração principal estarão disponíveis. Essas informações podem ser usadas para validar quais usuários e grupos foram migrados com êxito e, talvez, para determinar por que alguns não foram migrados.

Para exibir essas informações, acesse Cloud Acceleration Manager. Clique no cartão do projeto e clique no cartão Transferência de conteúdo. Navegue até **Tarefas de assimilação** e localize a assimilação que deseja verificar. Clique nos três pontos (**..**) para essa assimilação, em seguida, clique em **Exibir resumo principal** no menu suspenso.

![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-principal-action.png)

Você verá uma caixa de diálogo com as informações de resumo. Use os ícones de ajuda para ler uma descrição mais completa. Clique em **Baixar relatório** botão para baixar o relatório separado por vírgula (CSV) completo.

![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-principal-dialog.png)

>[!NOTE]
>
>Se o mapeamento de usuários estiver desativado, outra variante dessa caixa de diálogo será exibida. Ele indicará que o mapeamento de usuários foi desativado e não mostrará os três campos que fornecem valores de mapeamento de usuários.

## Resolução de problemas {#troubleshooting}

### Falha na validação. E agora? {#validation-fail}

A primeira etapa é determinar se a assimilação realmente falhou ou se o conteúdo extraído já está presente no ambiente de destino. Isso pode ocorrer se uma assimilação for repetida com o **Apagar conteúdo existente na instância da nuvem antes da assimilação** opção desativada.

Para verificar, escolha um caminho no relatório de validação e verifique se ele está presente no ambiente de destino. Se esse for um ambiente de publicação, talvez você esteja limitado a verificar as páginas e os ativos diretamente. Abra um tíquete no Atendimento ao cliente se precisar de assistência com esta etapa.

### A contagem de nós é menor do que eu esperava. Por que isso ocorre? {#node-count-lower-than-expected}

Alguns caminhos dos resumos de extração e assimilação são excluídos de propósito para manter o tamanho desses arquivos gerenciável, com o objetivo de poder calcular o resultado da validação de migração dentro de duas horas após a conclusão da assimilação.

Os caminhos que atualmente excluímos dos resumos incluem: `cqdam.text.txt` representações, nós dentro `/home`e nós dentro de `/jcr:system`.
