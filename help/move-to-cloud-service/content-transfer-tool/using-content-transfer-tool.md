---
title: Usar a ferramenta Transferência de conteúdo
description: Usar a ferramenta Transferência de conteúdo
translation-type: tm+mt
source-git-commit: 7648adc4b1d9c5849363beb4162de2f42eac7cfd
workflow-type: tm+mt
source-wordcount: '1582'
ht-degree: 91%

---


# Usar a ferramenta Transferência de conteúdo {#using-content-transfer-tool}

## Considerações importantes sobre o uso da ferramenta Transferência de conteúdo {#pre-reqs}

Siga a seção abaixo para entender as considerações importantes ao executar a ferramenta Transferência de conteúdo:

* O requisito mínimo do sistema para a ferramenta Transferência de conteúdo é o AEM 6.3 + e o JAVA 8. Se você estiver em uma versão inferior do AEM, precisará atualizar seu repositório de conteúdo para o AEM 6.5 para usar a ferramenta Transferência de conteúdo.

* If you are using a *Sandbox Environment*, ensure that your environment is upgraded to June 10 2020 Release or later. Se você estiver usando um *Ambiente de produção*, ele será atualizado automaticamente.

* Para usar a Ferramenta de transferência de conteúdo, você precisará ser um usuário administrador na instância de origem e pertencer ao grupo de administradores do AEM na instância do Cloud Service para a qual você está transferindo conteúdo. Os usuários sem privilégios não poderão recuperar o token de acesso para usar a ferramenta Transferência de conteúdo.

* Durante a fase de extração, a ferramenta Transferência de conteúdo é executada em uma instância de origem do AEM ativa.

* A *Fase de assimilação* do autor diminuirá a implantação do autor inteiro. Isso significa que o AEM do autor não estará disponível durante todo o processo de ingestão.

* O limite máximo recomendado para o tamanho do repositório que a Ferramenta de transferência de conteúdo pode suportar por vez é de 20 GB.

## Disponibilidade {#availability}

A Ferramenta de transferência de conteúdo pode ser baixada como um arquivo zip (Content Transfer Tool v1.0.0) do Portal de distribuição de software. Você pode instalar o pacote por meio do Gerenciador de pacotes na sua instância de origem do Adobe Experience Manager (AEM).

>[!NOTE]
>Baixe a Ferramenta de transferência de conteúdo, no portal de distribuição [de](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html) software.

## Execução da ferramenta Transferência de conteúdo {#running-tool}

>[!VIDEO](https://video.tv.adobe.com/v/35460/?quality=12&learn=on)

Siga esta seção para saber como usar a ferramenta Transferência de conteúdo para migrar o conteúdo para o AEM as a Cloud Service (Autor/Publicação):

1. Selecione o Adobe Experience Manager e navegue até Ferramentas -> **Operações** -> **Transferência de conteúdo**.

   ![imagem](/help/move-to-cloud-service/content-transfer-tool/assets/content1.png)

1. Clique em **Criar conjunto de migração** para criar um novo conjunto de migração. A tela **Detalhes do conjunto de migração de conteúdo** é exibida.

   >[!NOTE]
   >Você visualizará os conjuntos de migração existentes nessa tela com seu status atual.

   ![imagem](/help/move-to-cloud-service/content-transfer-tool/assets/ctt-img4.png)

1. Preencha os campos na tela **Detalhes do conjunto de migração de conteúdo**, conforme descrito abaixo.

   ![imagem](/help/move-to-cloud-service/content-transfer-tool/assets/content-3.png)


   1. **Nome**: insira o nome do conjunto de migração.
      >[!NOTE]
      >Nenhum caractere especial é permitido para o nome do conjunto de migração.

   1. **Configuração do Cloud Service**: insira a URL do autor do AEM as a Cloud Service.

      >[!NOTE]
      >Você pode criar e manter no máximo quatro conjuntos de migração por vez durante a atividade de transferência de conteúdo.
      >Além disso, é necessário criar uma migração separadamente para cada um dos ambientes específicos - *Preparação*, *Desenvolvimento* ou *Produção*.

   1. **Token de acesso**: insira o token de acesso.

      >[!NOTE]
      >Você pode recuperar o token de acesso da instância do autor navegando até `/libs/granite/migration/token.json`. O token de acesso é recuperado da instância do autor do Cloud Service.

   1. **Parâmetros**: selecione os seguintes parâmetros para criar o conjunto de migração:

      1. **Incluir versão**: selecione conforme necessário.

      1. **Caminhos a serem incluídos**: use o navegador de caminhos para selecionar os caminhos que precisam ser migrados.

         >[!IMPORTANT]
         >Os seguintes caminhos estão restritos ao criar um conjunto de migração:
         >* `/apps`
         >* `/libs`
         >* `/home`
         >* `/etc`


1. Clique em **Salvar**  depois de preencher todos os campos na tela **Detalhes do conjunto de migração de conteúdo**.

1. Você visualizará seu conjunto de migração na página *Visão geral*.

   ![imagem](/help/move-to-cloud-service/content-transfer-tool/assets/ctt-img4.png)

   Todos os conjuntos de migração existentes nessa tela serão exibidos na página *Visão geral* com suas informações de status atuais.

   * Uma *nuvem vermelha* indica que não é possível concluir o processo de extração.
   * Uma *nuvem verde* indica que você pode concluir o processo de extração.
   * Um *ícone amarelo* indica que você não criou o conjunto de migração existente e o específico é criado por algum outro usuário na mesma instância.

1. Selecione um conjunto de migração na página de visão geral e clique em **Propriedades** para visualização ou editar as propriedades desse conjunto de migração.

   ![imagem](/help/move-to-cloud-service/content-transfer-tool/assets/ctt-img6.png)

### Processo de extração na transferência de conteúdo {#extraction-process}

Siga as etapas abaixo para extrair seu conjunto de migração da ferramenta Transferência de conteúdo:

1. Selecione um conjunto de migração na página *Visão geral* e clique em **Extrair** para iniciar a extração.

   ![imagem](/help/move-to-cloud-service/content-transfer-tool/assets/extraction-img1.png)

1. A caixa de diálogo **Extração do conjunto de migração** é exibida. Clique em **Extrair** para concluir a fase de extração.

   >[!NOTE]
   >Você tem a opção de substituir o containercontêiner de preparação durante a fase de extração.

   ![imagem](/help/move-to-cloud-service/content-transfer-tool/assets/extract-2.png)

1. O campo **EXTRAÇÃO** agora exibe o status **EM EXECUÇÃO** para o processo de extração em andamento.

   ![imagem](/help/move-to-cloud-service/content-transfer-tool/assets/extract-3.png)

   Quando a extração for concluída, o status do conjunto de migração será atualizado para **CONCLUÍDO**, e um ícone de nuvem *verde sólido* será exibido abaixo do campo **INFO** .

   ![imagem](/help/move-to-cloud-service/content-transfer-tool/assets/extract-4.png)

   >[!NOTE]
   >Será necessário atualizar a página para visualizar o status atualizado.
   >Quando a fase de extração for iniciada, o bloqueio de gravação é criado e liberado após *60 segundos*. Em seguida, se uma extração for interrompida, você precisará esperar um minuto até que o bloqueio seja liberado antes de reiniciar a extração.

#### Extração complementar {#top-up-extraction-process}

A ferramenta Transferência de conteúdo tem um recurso que oferece suporte a atualizações complementares de conteúdo diferencial, com o qual é possível transferir somente as alterações feitas desde a atividade de transferência de conteúdo anterior.

>[!NOTE]
>Após a transferência inicial do conteúdo, é recomendável fazer atualizações complementares frequentes de conteúdo diferencial para reduzir o período de congelamento de conteúdo para a transferência final de conteúdo diferencial antes de entrar online no Cloud Service.

Quando o processo de extração estiver concluído, você poderá transferir o conteúdo delta usando o método de extração complementar. Siga as etapas abaixo:

1. Navegue até a página *Visão geral* e selecione o conjunto de migração para o qual você deseja realizar a extração complementar.

1. Clique em **Extrair** para iniciar a extração complementar.

   ![imagem](/help/move-to-cloud-service/content-transfer-tool/assets/extraction-img1.png)

1. A caixa de diálogo **Extração do conjunto de migração** é exibida.

   >[!IMPORTANT]
   >Você deve desativar a opção **Substituir containercontêiner de preparação durante a extração**.
   ![imagem](/help/move-to-cloud-service/content-transfer-tool/assets/extract-topup-1.png)

### Processo de assimilação na transferência de conteúdo {#ingestion-process}

Siga as etapas abaixo para assimilar seu conjunto de migração da ferramenta Transferência de conteúdo:

1. Selecione um conjunto de migração na página *Visão geral* e clique em **Assimilar** para iniciar a extração.

   ![imagem](/help/move-to-cloud-service/content-transfer-tool/assets/ingest-1.png)

1. A caixa de diálogo **Assimilação do conjunto de migração** é exibida.

   ![imagem](/help/move-to-cloud-service/content-transfer-tool/assets/ingest-2.png)

   Para fins de demonstração, a opção **Assimilar conteúdo na instância do autor** do autor está desativada. É possível assimilar conteúdo para Autor e Publicação ao mesmo tempo.

   ![imagem](/help/move-to-cloud-service/content-transfer-tool/assets/ingest-3.png)

   Clique em **Assimilar** para concluir a fase de assimilação.

1. Quando a assimilação estiver concluída, o status no campo **ASSIMILAÇÃO DO AUTOR** será atualizado para **CONCLUÍDO**, e um ícone de nuvem verde sólido será exibido abaixo do campo **INFO**.
   ![imagem](/help/move-to-cloud-service/content-transfer-tool/assets/ingest-4.png)

   >[!NOTE]
   > Será necessário atualizar a página para visualizar o status atualizado.

#### Ingestão complementar {#top-up-ingestion-process}

A ferramenta Transferência de conteúdo tem um recurso que oferece suporte a *atualizações complementares* de conteúdo diferencial, com o qual é possível transferir somente as alterações feitas desde a atividade de transferência de conteúdo anterior.

>[!NOTE]
>Após a transferência inicial do conteúdo, é recomendável fazer atualizações complementares frequentes de conteúdo diferencial para reduzir o período de congelamento de conteúdo para a transferência final de conteúdo diferencial antes de entrar online no Cloud Service.

Quando o processo de assimilação estiver concluído, você poderá usar o conteúdo delta por meio do método de ingestão complementar. Siga as etapas abaixo:

1. Navegue até a página *Visão geral* e selecione o conjunto de migração para o qual você deseja realizar a assimilação complementar.

1. Clique em **Assimilar** para iniciar a extração complementar.

   ![imagem](/help/move-to-cloud-service/content-transfer-tool/assets/ingest-1.png)

1. A caixa de diálogo **Assimilação do conjunto de migração** é exibida.

   >[!NOTE]
   >Você deve desativar a opção *Varrer* para evitar que o conteúdo existente seja excluído da atividade de assimilação anterior.
   ![imagem](/help/move-to-cloud-service/content-transfer-tool/assets/ingest-topup-1.png)

### Visualização de logs para um conjunto de migração {#viewing-logs-migration-set}

Você pode visualizar logs de um conjunto de migração existente na página *Visão geral*.
Siga as etapas abaixo:

1. Navegue até a página *Visão geral*, selecione o conjunto de migração que você deseja excluir e clique em **Exibir log** na barra de ações.

   ![imagem](/help/move-to-cloud-service/content-transfer-tool/assets/view-log1.png)

1. A caixa de diálogo **Logs** é exibida. Clique em **Logs de extração** para visualizar os logs em uma nova guia.

   ![imagem](/help/move-to-cloud-service/content-transfer-tool/assets/view-log2.png)
Ou,

   Você também pode visualizar logs para o seu conjunto de migração na tela *Visão geral*. Selecione o conjunto de migração e clique no status do campo **EXTRAÇÃO**. Nesse caso, clique em **CONCLUÍDO** para visualizar os logs em uma nova guia.

   ![imagem](/help/move-to-cloud-service/content-transfer-tool/assets/view-log3.png)

1. Para rastrear os registros sem usar a interface do usuário, você pode SSH no ambiente AEM de origem e rastrear o conteúdo `crx-quickstart/cloud-migration/extraction-XXXXX/output.log file`.

### Exclusão de um conjunto de migração {#deleting-migration-set}

Você pode excluir o conjunto de migração na página *Visão geral*.
Siga as etapas abaixo:

1. Navegue até a página *Visão geral*, selecione o conjunto de migração que você deseja excluir e clique em **Excluir** na barra de ações.

   ![imagem](/help/move-to-cloud-service/content-transfer-tool/assets/delete-1.png)

1. Clique em **Excluir** na caixa de diálogo **Excluir conjunto de migração** para confirmar a exclusão.

   ![imagem](/help/move-to-cloud-service/content-transfer-tool/assets/delete-3.png)

## Resolução de Problemas{#troubleshooting}

### IDs de blob ausentes {#missing-blobs}

Se houver IDs de blob ausentes reportados, como mencionado abaixo, será necessário executar uma verificação de consistência no repositório existente e restaurar os blobs ausentes.
`ERROR o.a.j.o.p.b.AbstractSharedCachingDataStore - Error retrieving record [ba45c53f8b687e7056c85dceebf8156a0e6abc7e]`

O seguinte comando é executado

>[!NOTE]
> `--verbose` o sinalizador é necessário para relatar os caminhos de nó de onde os blobs são referenciados.

**Para repositórios AEM 6.5 (Oak 1.8 e inferior)**

```shell
java -jar oak-run.jar datastorecheck --consistency --store [<SEGMENT_STORE_PATH>|<MONGO_URI>] --[s3ds|fds] <DATASTORE_CFG> --verbose <OUT_DIR> --dump
```

**Para repositórios com Oak > 1.10**

```shell
java -jar oak-run.jar datastore --check-consistency [<SEGMENT_STORE_PATH>|<MONGO_URI>] --[s3ds|fds|azureds] <DATASTORE_CFG> --out-dir <OUT_DIR> --work-dir <TEMP_DIR> --verbose
```

Consulte [Jar executável do Oak](https://github.com/apache/jackrabbit-oak/tree/trunk/oak-run) para obter mais detalhes.

Os arquivos criados no *OUT_DIR* especificado acima para fins de consistência podem ser verificados quanto a caminhos com binários ausentes e à ação apropriada a ser realizada, como restauração de um backup, exclusão dos caminhos, reindexação e assim por diante.

### Comportamento da interface do usuário {#ui-behavior}

Como usuário, você pode ver as seguintes alterações de comportamento na interface do usuário da ferramenta Transferência de conteúdo:

* O usuário cria um conjunto de migração para uma URL de autor (Desenvolvimento/Preparação/Produção) e realiza com sucesso a extração e a assimilação.

* Em seguida, o usuário cria um novo conjunto de migração para a mesmo URL do autor e realiza a extração e a assimilação no novo conjunto de migração. A interface do usuário mostra que o status de assimilação do primeiro conjunto de migração muda para **FALHA** e nenhum log está disponível.

* Isso não significa que a assimilação do primeiro conjunto de migração falhou. Esse comportamento é visto porque, quando um novo trabalho de assimilação é iniciado, ele exclui o trabalho de ingestão anterior. Portanto, o status das alterações no primeiro conjunto de migração deve ser ignorado.

* Os ícones na interface do usuário da ferramenta Transferência de conteúdo podem parecer diferentes das capturas de tela mostradas neste guia ou podem não aparecer, dependendo da versão da instância do AEM de origem.


