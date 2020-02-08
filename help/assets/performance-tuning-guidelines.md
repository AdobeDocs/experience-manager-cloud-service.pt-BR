---
title: Guia de ajuste de desempenho dos ativos
description: Principais áreas de foco sobre a configuração do AEM, alterações no hardware, software e componentes de rede para remover gargalos e otimizar o desempenho dos ativos AEM.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 991d4900862c92684ed92c1afc081f3e2d76c7ff

---


# Guia de ajuste de desempenho dos ativos{#assets-performance-tuning-guide}

Uma configuração do Adobe Experience Manager (AEM) Assets contém vários componentes de hardware, software e rede. Dependendo do cenário de implantação, talvez você precise de alterações específicas na configuração de hardware, software e componentes de rede para remover gargalos de desempenho.

Além disso, identificar e seguir determinadas diretrizes de otimização de hardware e software ajuda a criar uma base sólida que permite que a implantação dos ativos AEM atenda às expectativas de desempenho, escalabilidade e confiabilidade.

O baixo desempenho nos ativos AEM pode afetar a experiência do usuário em relação ao desempenho interativo, processamento de ativos, velocidade de download e outras áreas.

Na verdade, a otimização de desempenho é uma tarefa fundamental que você executa antes de estabelecer métricas de direcionamento para qualquer projeto.

Estas são algumas áreas de foco chave em torno das quais você descobre e corrige problemas de desempenho antes que eles afetem os usuários.

## Plataforma {#platform}

Embora o AEM seja suportado em várias plataformas, a Adobe encontrou o maior suporte para ferramentas nativas no Linux e no Windows, o que contribui para o desempenho ideal e a facilidade de implementação. O ideal é que você implante um sistema operacional de 64 bits para atender aos altos requisitos de memória de uma implantação do AEM Assets. Assim como com qualquer implantação do AEM, você deve implementar o TarMK sempre que possível. Embora o TarMK não possa ser dimensionado além de uma única instância do autor, ele tem um desempenho melhor do que o MongoMK. Você pode adicionar instâncias de descarregamento TarMK para aumentar o poder de processamento do fluxo de trabalho de sua implantação do AEM Assets.

### Pasta temporária {#temp-folder}

Para melhorar os tempos de carregamento dos ativos, use armazenamento de alto desempenho para o diretório temporário Java. No Linux e no Windows, uma unidade de RAM ou SSD pode ser usada. Em ambientes baseados em nuvem, pode ser usado um tipo de armazenamento de alta velocidade equivalente. Por exemplo, no Amazon EC2, uma unidade [&quot;ephemeral drive&quot;](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/InstanceStorage.html) pode ser usada para a pasta temp.

Supondo que o servidor tenha ampla memória, configure uma unidade RAM. No Linux, execute estes comandos para criar uma unidade de RAM de 8 GB:

```
mkfs -q /dev/ram1 800000
 mkdir -p /mnt/aem-tmp
 mount /dev/ram1 /mnt/aem-tmp
 df -H | grep aem-tmp
```

No Windows OS, você precisaria usar um driver de terceiros para criar uma unidade de RAM ou usar apenas armazenamento de alto desempenho, como SSD.

Quando o volume temporário de alto desempenho estiver pronto, defina o parâmetro JVM -Djava.io.tmpdir. Por exemplo, você pode adicionar o parâmetro JVM abaixo à variável CQ_JVM_OPTS no script bin/start do AEM:

`-Djava.io.tmpdir=/mnt/aem-tmp`

## Configuração do Java {#java-configuration}

### Versão do Java {#java-version}

Como a Oracle parou de lançar atualizações para o Java 7 a partir de abril de 2015, a Adobe recomenda implantar os ativos AEM no Java 8. Em alguns casos, demonstrou um melhor desempenho.

### Parâmetros JVM {#jvm-parameters}

Você deve definir os seguintes parâmetros JVM:

* `-XX:+UseConcMarkSweepGC`
* `-Doak.queryLimitInMemory`=500000
* `-Doak.queryLimitReads`=100000
* `-Dupdate.limit`=250000
* `-Doak.fastQuerySize`=verdadeiro

## Configuração do armazenamento de dados e da memória {#data-store-and-memory-configuration}

### Configuração do armazenamento de dados de arquivo {#file-data-store-configuration}

É recomendável separar o armazenamento de dados do armazenamento de segmentos para todos os usuários do AEM Assets. Além disso, configurar os parâmetros `maxCachedBinarySize` e `cacheSizeInMB` pode ajudar a maximizar o desempenho. Defina `maxCachedBinarySize` para o menor tamanho de arquivo que pode ser mantido no cache. Especifique o tamanho do cache na memória a ser usado para o armazenamento de dados no `cacheSizeInMB`. A Adobe recomenda que você defina esse valor entre 2 a 10% do tamanho total do heap. No entanto, o teste de carga/desempenho pode ajudar a determinar a configuração ideal.

### Configurar o tamanho máximo do cache de imagem em buffer {#configure-the-maximum-size-of-the-buffered-image-cache}

Ao fazer upload de grandes quantidades de ativos para o Adobe Experience Manager, para permitir picos inesperados no consumo de memória e para evitar falhas de JVM com OutOfMemoryErrors, reduza o tamanho máximo configurado do cache de imagem em buffer. Considere um exemplo de que você tem um sistema com um heap máximo (- `Xmx`param) de 5 GB, um BlobCache Oak definido em 1 GB e um cache de documento definido em 2 GB. Nesse caso, o cache armazenado em buffer levaria no máximo 1,25 GB e memória, o que deixaria apenas 0,75 GB de memória para picos inesperados.

Configure o tamanho do cache armazenado em buffer no console da Web OSGi. Em `https://host:port/system/console/configMgr/com.day.cq.dam.core.impl.cache.CQBufferedImageCache`, defina a propriedade `cq.dam.image.cache.max.memory` em bytes. Por exemplo, 1073741824 é 1 GB (1024 x 1024 x 1024 = 1 GB).

No AEM 6.1 SP1, se você estiver usando um `sling:osgiConfig` nó para configurar essa propriedade, certifique-se de definir o tipo de dados como Longo. Para obter mais detalhes, consulte [CQBufferedImageCache consome heap durante os uploads](https://helpx.adobe.com/experience-manager/kb/cqbufferedimagecache-consumes-heap-during-asset-uploads.html)do ativo.

### Armazenamentos de dados compartilhados {#shared-data-stores}

A implementação de um armazenamento de dados de arquivos compartilhados ou S3 pode ajudar a economizar espaço em disco e aumentar o throughput da rede em implementações de larga escala.

### S3 data store {#s-data-store}

A seguinte configuração S3 Data Store ( `org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.cfg`) ajudou a Adobe a extrair 12,8 TB de BLOBs (objetos grandes binários) de um armazenamento de dados de arquivo existente para um armazenamento de dados S3 em um local do cliente:

```
accessKey=<snip>
 secretKey=<snip>
 s3Bucket=<snip>
 s3Region=us-standard
 s3EndPoint=<a href="https://s3.amazonaws.com/">s3.amazonaws.com</a>
 connectionTimeout=120000
 socketTimeout=120000
 maxConnections=80
 writeThreads=60
 concurrentUploadsThreads=30
 asyncUploadLimit=30
 maxErrorRetry=1000
 path=/opt/author/crx-quickstart/repository/datastore
 s3RenameKeys=false
 s3Encryption=SSE_S3
 proactiveCaching=true
 uploadRetries=1000
 migrateFailuresCount=400
```

## Otimização da rede {#network-optimization}

A Adobe recomenda ativar o HTTPS, pois muitas empresas têm firewalls que cheiram o tráfego HTTP, o que afeta negativamente os uploads e corrompe os arquivos. Para fazer uploads de arquivos grandes, verifique se os usuários têm conexões com fio à rede, pois uma rede WiFi fica rapidamente saturada. Para avaliar o desempenho da rede analisando a topologia da rede, consulte Considerações [de rede do](/help/assets/assets-network-considerations.md)Assets.

Principalmente, sua estratégia de otimização de rede depende da quantidade de largura de banda disponível e da carga da sua instância do AEM. Opções comuns de configuração, incluindo firewalls ou proxies, podem ajudar a melhorar o desempenho da rede. Estes são alguns pontos-chave que devem ser levados em conta:

* Dependendo do tipo de instância (pequena, moderada, grande), verifique se você tem largura de banda de rede suficiente para a instância do AEM. A alocação de largura de banda adequada é especialmente importante se o AEM estiver hospedado no AWS.
* Se sua instância do AEM estiver hospedada no AWS, você poderá se beneficiar se tiver uma política de dimensionamento versátil. Atualize a instância se os usuários esperarem carga alta. Baixe-o para uma carga moderada/baixa.
* HTTPS: A maioria dos usuários tem firewalls que cheiram o tráfego HTTP, o que pode afetar negativamente o carregamento de arquivos ou até mesmo arquivos corrompidos durante a operação de upload.
* Carregamentos de arquivos grandes: Verifique se os usuários têm conexões com fio à rede (as conexões WiFi se saturam rapidamente).

## Fluxos de trabalhos {#workflows}

### Fluxos de trabalho transitórios {#transient-workflows}

Sempre que possível, defina o fluxo de trabalho Atualizar ativo DAM como Transitório. A configuração reduz significativamente os custos indiretos necessários para processar fluxos de trabalho porque, nesse caso, os fluxos de trabalho não precisam passar pelos processos normais de rastreamento e arquivamento.

>[!NOTE]
>
>Por padrão, o fluxo de trabalho do Ativo de atualização do DAM está definido como Transitório no AEM 6.3. Nesse caso, você pode ignorar o procedimento a seguir.

1. Navegue até */miscadmin* na instância do AEM a ser configurada (ou seja, [https://localhost:4502/miscadmin)](https://localhost:4502/miscadmin).
1. Na árvore de navegação, expanda **Ferramentas** > **Fluxo de trabalho** > **Modelos** > **dam**.
1. Clique duas vezes em Ativo **de atualização** DAM.
1. No painel de ferramentas flutuante, alterne para a guia **Página** e clique em Propriedades **da página...**
1. Selecione Fluxo de trabalho **temporário** e clique em **OK**.

   >[!NOTE]
   >
   >Alguns recursos não suportam fluxos de trabalho transitórios. Se sua implantação do AEM Assets exigir esses recursos, não configure fluxos de trabalho transitórios.

   Nos casos em que fluxos de trabalho transitórios não podem ser usados, execute a remoção de fluxo de trabalho regularmente para excluir fluxos de trabalho arquivados de Atualização de DAM Asset para garantir que o desempenho do sistema não diminua.

   Normalmente, você deve executar fluxos de trabalho de expurgação semanalmente. No entanto, em cenários com muitos recursos, como durante a ingestão de ativos em larga escala, você pode executá-los com mais frequência.

   Para configurar a remoção do fluxo de trabalho, adicione uma nova configuração de Expurgação do fluxo de trabalho do Adobe Granite por meio do console OSGi. Em seguida, configure e agende o fluxo de trabalho como parte da janela de manutenção semanal.

   Se a limpeza for longa demais, ela expira. Portanto, você deve garantir que suas tarefas de expurgação sejam concluídas para evitar situações em que a expurgação de fluxos de trabalho não seja concluída devido ao alto número de fluxos de trabalho.

   Por exemplo, após executar vários fluxos de trabalho não transitórios (que criam nós de instância do fluxo de trabalho), você pode executar o [ACS AEM Commons Workflow Remover](https://adobe-consulting-services.github.io/acs-aem-commons/features/workflow-remover.html) de forma ad hoc. Ele remove instâncias de fluxo de trabalho redundantes e concluídas imediatamente, em vez de aguardar a execução do programador de Expurgação do Fluxo de Trabalho do Adobe Granite.

### Máximo de trabalhos paralelos {#maximum-parallel-jobs}

Por padrão, o AEM executa um número máximo de trabalhos paralelos igual ao número de processadores no servidor. O problema com essa configuração é que, durante períodos de carga pesada, todos os processadores são ocupados pelos fluxos de trabalho do Ativo de atualização do DAM, retardando a capacidade de resposta da interface e impedindo que o AEM execute outros processos que salvaguardem o desempenho e a estabilidade do servidor. Como prática recomendada, defina esse valor para metade dos processadores disponíveis no servidor, executando as seguintes etapas:

1. No AEM Author, vá para [https://localhost:4502/system/console/slingevent](https://localhost:4702/system/console/slingevent).
1. Clique em Editar em cada fila de fluxo de trabalho relevante para sua implementação, por exemplo, Fila de fluxo de trabalho temporário de granite.
1. Altere o valor de Máximo de Trabalhos Paralelos e clique em Salvar.

Definir uma fila para metade dos processadores disponíveis é uma solução viável para começar. No entanto, talvez seja necessário aumentar ou diminuir esse número para atingir o throughput máximo e ajustá-lo pelo ambiente. Há filas separadas para fluxos de trabalho transitórios e não transitórios, bem como outros processos, como fluxos de trabalho externos. Se várias filas definidas como 50% dos processadores estiverem ativos simultaneamente, o sistema poderá ser sobrecarregado rapidamente. As filas muito usadas variam muito entre as implementações do usuário. Portanto, talvez seja necessário configurá-los cuidadosamente para obter a máxima eficiência sem sacrificar a estabilidade do servidor.

### Configuração do ativo de atualização do DAM {#dam-update-asset-configuration}

O fluxo de trabalho do Ativo de atualização do DAM contém um conjunto completo de etapas configuradas para tarefas, como geração do Scene7 PTIFF e integração do InDesign Server. Entretanto, a maioria dos usuários pode não exigir várias dessas etapas. A Adobe recomenda que você crie uma cópia personalizada do modelo de fluxo de trabalho Atualizar ativo DAM e remova quaisquer etapas desnecessárias. Nesse caso, atualize os iniciadores do Ativo de atualização do DAM para apontar para o novo modelo.

>[!NOTE]
>
>A execução intensiva do fluxo de trabalho do Ativo de atualização do DAM pode aumentar consideravelmente o tamanho do armazenamento de dados do arquivo. Os resultados de um experimento realizado pela Adobe mostraram que o tamanho do armazenamento de dados pode aumentar aproximadamente 400 GB se cerca de 5500 fluxos de trabalho forem executados em 8 horas.
>
>É um aumento temporário e o armazenamento de dados é restaurado para seu tamanho original depois que você executa a tarefa de coleta de lixo do armazenamento de dados.
>
>Normalmente, a tarefa de coleta de lixo do armazenamento de dados é executada semanalmente, juntamente com outras tarefas de manutenção programadas.
>
>Se você tiver um espaço em disco limitado e executar fluxos de trabalho de Atualização de ativos DAM intensivamente, considere programar a tarefa de coleta de lixo com mais frequência.

#### Geração de execução em tempo de execução {#runtime-rendition-generation}

Os clientes usam imagens de vários tamanhos e formatos em seu site ou para distribuição a parceiros comerciais. Como cada renderização adiciona ao espaço ocupado do ativo no repositório, a Adobe recomenda usar esse recurso de forma criteriosa. Para reduzir a quantidade de recursos necessários para processar e armazenar imagens, é possível gerar essas imagens em tempo de execução em vez de representações durante a ingestão.

Muitos clientes do Sites implementam um servlet de imagem que redimensiona e corta imagens no momento em que são solicitadas, o que impõe carga adicional na instância de publicação. Entretanto, enquanto essas imagens puderem ser armazenadas em cache, o desafio poderá ser atenuado.

Uma abordagem alternativa é usar a tecnologia Scene7 para entregar totalmente a manipulação de imagens. Além disso, você pode implantar o Brand Portal que não somente assume as responsabilidades de geração de execução da infraestrutura do AEM, mas também toda a camada de publicação.

### XMP writeback {#xmp-writeback}

O write-back XMP atualiza o ativo original sempre que os metadados são modificados no AEM, o que resulta no seguinte:

* O próprio ativo é modificado
* Uma versão do ativo é criada
* O Ativo de atualização de DAM é executado no ativo

Os resultados referidos consomem recursos consideráveis. Portanto, a Adobe recomenda [desativar o Writeback](https://helpx.adobe.com/experience-manager/kb/disable-xmp-writeback.html)XMP, se não for necessário.

Importar uma grande quantidade de metadados pode resultar em atividade de gravação XMP de uso intenso de recursos se o sinalizador de fluxos de trabalho de execução estiver marcado. Planeje tal importação durante o uso de servidor simplificado para que o desempenho para outros usuários não seja afetado.

## Replicação {#replication}

Ao replicar ativos para um grande número de instâncias de publicação, por exemplo em uma implementação de Sites, a Adobe recomenda o uso da replicação em cadeia. Nesse caso, a instância do autor é replicada para uma única instância de publicação que, por sua vez, é replicada para outras instâncias de publicação, liberando a instância do autor.

### Configurar replicação em cadeia {#configure-chain-replication}

1. Escolha a instância de publicação que deseja usar para encadear as replicações em
1. Nessa instância de publicação, adicione agentes de replicação que apontem para outras instâncias de publicação
1. Em cada um desses agentes de replicação, ative &quot;Ao receber&quot; na guia &quot;Acionadores&quot;

>[!NOTE]
>
>A Adobe não recomenda ativar ativos automaticamente. No entanto, se necessário, a Adobe recomenda fazer isso como a etapa final em um fluxo de trabalho, geralmente Ativo de atualização do DAM.

## Índices de pesquisa {#search-indexes}

Certifique-se de implementar os service packs mais recentes e os hotfixes relacionados ao desempenho, pois eles frequentemente incluem atualizações para índices do sistema. Consulte Dicas [de ajuste de desempenho| 6.x](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html) para algumas otimizações de índice que podem ser aplicadas, dependendo da sua versão do AEM.

<!--
Create custom indexes for queries that you run often. For details, see [methodology for analyzing slow queries](https://aemfaq.blogspot.com/2014/08/oak-query-log-file-analyzer-tool.html) and [crafting custom indexes](/help/sites-deploying/queries-and-indexing.md). For additional insights around query and index best practices, see [Best Practices for Queries and Indexing](/help/sites-deploying/best-practices-for-queries-and-indexing.md).
-->

### Configurações do índice Lucene {#lucene-index-configurations}

Algumas otimizações podem ser feitas nas configurações de índice Oak que podem ajudar a melhorar o desempenho dos ativos AEM:

Atualize as configurações de índice para melhorar o tempo de reindexação:

1. Abra o CRXDe /crx/de/index.jsp e faça logon como um usuário administrativo
1. Navegue até /oak:index/lucene
1. Adicione uma propriedade String[] chamada &quot;excludePaths&quot; com valores &quot;/var&quot;, &quot;/etc/workflow/instance&quot; e &quot;/etc/Replication&quot;
1. Navegue até /oak:index/damAssetLucene
1. Adicionar uma propriedade String[] chamada &quot;includePaths&quot; com um valor &quot;/content/dam&quot;
1. Salvar

(Somente AEM6.1 e 6.2) Atualize o índice ntBaseLucene para melhorar o desempenho de exclusão de ativos e movimentação:

1. Navegue até */oak:index/ntBaseLucene/indexRules/nt:base/properties*
1. Adicione dois nós &quot;slingResource&quot; e &quot;damResolvedPath&quot; em */oak:index/ntBaseLucene/indexRules/nt:base/properties*
1. Defina as propriedades abaixo nos nós (onde as propriedades order e propertyIndex são do tipo *Boolean*:
slingResourcename=&quot;sling:resource&quot;order=falseIndex= truetype=&quot;String&quot;damResolvedPathname=&quot;dam:resolvePath&quot;order=falpropertyIndex=truetype=&quot;String&quot;

1. No nó /oak:index/ntBaseLucene, defina a propriedade *reindex=true*
1. Clique em &quot;Salvar tudo&quot;
1. Monitore o error.log para ver quando a indexação é concluída:
Reindexação concluída para índices: [/carvalho:index/ntBaseLucene]
1. Você também pode ver que a indexação foi concluída atualizando o nó /oak:index/ntBaseLucene no CRXDe, pois a propriedade reindex voltaria para false
1. Quando a indexação for concluída, volte para CRXDe e defina a propriedade &quot;type&quot; como desativada nesses dois índices

   * */oak:index/slingResource*
   * */oak:index/damResolvedPath*

1. Clique em &quot;Salvar tudo&quot;

<!--
Disable Lucene Text Extraction:

If your users don't need to be able to search the contents of assets, for example, searching the text contained in PDF documents, then you can improve index performance by disabling this feature.

1. Go to the AEM package manager /crx/packmgr/index.jsp
1. Upload and install the package below

[Get File](assets/disable_indexingbinarytextextraction-10.zip)
-->

### Total de suposições {#guess-total}

Ao criar consultas que geram grandes conjuntos de resultados, use o `guessTotal` parâmetro para evitar a utilização de memória pesada ao executá-las.

## Problemas conhecidos {#known-issues}

### Arquivos grandes {#large-files}

Há dois problemas conhecidos principais relacionados a arquivos grandes no AEM. Quando os arquivos atingem tamanhos superiores a 2 GB, a sincronização em espera fria pode ocorrer em uma situação de falta de memória. Em alguns casos, impede que a sincronização em espera seja executada. Em outros casos, isso faz com que a instância primária falhe. Esse cenário se aplica a qualquer arquivo no AEM que tenha mais de 2 GB, incluindo pacotes de conteúdo.

Da mesma forma, quando os arquivos atingem 2 GB ao usar um armazenamento de dados S3 compartilhado, pode levar algum tempo para que o arquivo seja totalmente persistente do cache para o sistema de arquivos. Como resultado, ao usar replicação sem binários, é possível que os dados binários não tenham sido persistentes antes da conclusão da replicação. Essa situação pode levar a problemas, especialmente se a disponibilidade de dados for importante.

## Teste de desempenho {#performance-testing}

Para cada implantação do AEM, estabeleça um regime de teste de desempenho que possa identificar e resolver gargalos rapidamente. Aqui estão algumas áreas-chave para se concentrar.

### Teste de rede {#network-testing}

Para todas as preocupações de desempenho de rede do cliente, execute as seguintes tarefas:

* Teste o desempenho da rede na rede do cliente
* Teste o desempenho da rede na rede da Adobe. Para clientes do AMS, trabalhe com seu CSE para testar a partir da rede da Adobe.
* Testar o desempenho da rede de outro ponto de acesso
* Usando uma ferramenta de benchmark de rede
* Teste contra o expedidor

### Teste de instância do AEM {#aem-instance-testing}

Para minimizar a latência e alcançar alta throughput por meio da utilização eficiente da CPU e do compartilhamento de carga, monitore regularmente o desempenho da sua instância do AEM. Nomeadamente:

* Executar testes de carga na instância do AEM
* Monitore o desempenho de upload e a capacidade de resposta da interface do usuário

## Lista de verificação de desempenho do AEM Assets e impacto das tarefas de gerenciamento de ativos {#checklist}

* Ative o HTTPS para contornar qualquer sniffers de tráfego HTTP corporativo
* Usar uma conexão com fio para fazer upload de ativos pesados
* Implantar no Java 8.
* Definir parâmetros JVM ideais
* Configurar um DataStore do sistema de arquivos ou um S3 DataStore
* Ativar fluxos de trabalho transitórios
* Ajustar as filas de fluxo de trabalho Granite para limitar trabalhos simultâneos
* Configurar o ImageMagick para limitar o consumo de recursos
* Remova etapas desnecessárias do fluxo de trabalho Atualizar ativo DAM
* Configurar a depuração de fluxo de trabalho e versão
* Otimize índices com os service packs e hotfixes mais recentes. Consulte o Suporte da Adobe para obter outras otimizações de índice que possam estar disponíveis.
* Use a opção de estimativa total para otimizar o desempenho da consulta.
* Se você configurar o AEM para detectar tipos de arquivos a partir do conteúdo dos arquivos (habilitando o **[!UICONTROL Day CQ DAM Mime Type Service]** no console **[!UICONTROL da Web do]** AEM), faça upload de muitos arquivos em massa durante horas que não sejam de pico, pois ele consome muitos recursos.

