---
title: Integração do AEM Assets com o InDesign Server
description: Saiba como integrar os ativos AEM ao InDesign Server.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 991d4900862c92684ed92c1afc081f3e2d76c7ff

---


# Integração do AEM Assets com o InDesign Server {#integrating-aem-assets-with-indesign-server}

Os ativos Adobe Experience Manager (AEM) usam:

* Um proxy para distribuir a carga de determinadas tarefas de processamento. Um proxy é uma instância do AEM que se comunica com um funcionário proxy para realizar uma tarefa específica e outras instâncias do AEM para fornecer os resultados.
* Um funcionário proxy para definir e gerenciar uma tarefa específica.
Estas podem abranger uma grande variedade de tarefas; por exemplo, usar um InDesign Server para processar arquivos.

Para fazer upload completo de arquivos para os ativos AEM criados com o Adobe InDesign, um proxy é usado. Isso usa um funcionário proxy para se comunicar com o Adobe InDesign Server, onde [scripts](https://www.adobe.com/devnet/indesign/documentation.html#idscripting) são executados para extrair metadados e gerar várias execuções para ativos AEM. O trabalho proxy permite a comunicação bidirecional entre o InDesign Server e as instâncias do AEM em uma configuração em nuvem.

>[!NOTE]
>
>O Adobe InDesign é fornecido como dois produtos:
>
>* [InDesign](https://www.adobe.com/products/indesign.html)
   >  Isso permite que você crie layouts de página para distribuição impressa e/ou digital.
   >
   >
* [InDesign Server](https://www.adobe.com/products/indesignserver.html)
   >  Esse mecanismo permite que você crie documentos automatizados de forma programática com base no que você criou com o InDesign. Ele opera como um serviço que oferece uma interface para seu mecanismo [ExtendScript](https://www.adobe.com/devnet/scripting.html) .
   >  Os scripts são gravados em extendscript, que é semelhante ao javascript. Para obter informações sobre scripts do Indesign, consulte [https://www.adobe.com/devnet/indesign/documentation.html#idscripting](https://www.adobe.com/devnet/indesign/documentation.html#idscripting).
>



## Como funciona a extração {#how-the-extraction-works}

O Adobe InDesign Server pode ser integrado aos ativos AEM para que os arquivos INDD criados com o InDesign possam ser carregados, as execuções geradas, todas as mídias extraídas (por exemplo, vídeo) e armazenados como ativos:

>[!NOTE]
>
>As versões anteriores do AEM podiam extrair XMP e a miniatura, agora todas as mídias podem ser extraídas.

1. Carregue o arquivo INDD nos ativos AEM.
1. Uma estrutura envia scripts de comando para o InDesign Server via SOAP (Simple Object Access Protocol).
Esse script de comando:

   * Recupere o arquivo INDD.
   * Executar comandos do InDesign Server:

      * A estrutura, o texto e quaisquer arquivos de mídia são extraídos.
      * Execuções de PDF e JPG são geradas.
      * Execuções HTML e IDML são geradas.
   * Poste os arquivos resultantes de volta aos ativos AEM.
   >[!NOTE]
   >
   >O IDML é um formato baseado em XML que renderiza *tudo* no arquivo do InDesign. É armazenado como um pacote compactado usando a compactação [Zip](https://www.techterms.com/definition/zip) .
   >
   >
   >Consulte [Adobe Press - InDesign Interchange Formats INX e IDML](https://www.adobepress.com/articles/article.asp?p=1381880&seqNum=8) para obter mais informações.

   >[!CAUTION]
   >
   >Se o InDesign Server não estiver instalado ou configurado, você ainda poderá carregar um arquivo INDD no AEM. No entanto, as renderizações geradas serão limitadas a PNG e JPEG. Não será possível gerar HTML, .idml ou as execuções da página.

1. Após a geração de extração e representação:

   * A estrutura é replicada para um `cq:Page` (tipo de representação).
   * O texto e os arquivos extraídos são armazenados nos ativos AEM.
   * Todas as execuções são armazenadas nos ativos AEM, no próprio ativo.

## Integração do InDesign Server com o AEM {#integrating-the-indesign-server-with-aem}

Para integrar o InDesign Server para uso com os ativos AEM e após configurar seu proxy, é necessário:

1. [Instale o InDesign Server](#installing-the-indesign-server).
1. Se necessário, [configure o fluxo de trabalho](#configuring-the-aem-assets-workflow)dos ativos AEM.
Isso só é necessário se os valores padrão não forem apropriados para sua instância.

1. Configure um funcionário [proxy para o InDesign Server](#configuring-the-proxy-worker-for-indesign-server).

### Instalação do InDesign Server {#installing-the-indesign-server}

Para instalar e iniciar o InDesign Server para uso com o AEM:

1. Baixe e instale o Adobe InDesign Server.

   >[!NOTE]
   >
   >InDesign Server (CS6 e superior).

1. Se necessário, você pode personalizar a configuração da sua instância do InDesign Server.

1. Na linha de comando, inicie o servidor:

   `<*ids-installation-dir*>/InDesignServer.com -port 8080`

   Isso iniciará o servidor com o plug-in SOAP escutando na porta 8080. Todas as mensagens de registro e saída são gravadas diretamente na janela de comando.

   >[!NOTE]
   >
   >Se desejar salvar as mensagens de saída em um arquivo, use redirecionamento; por exemplo, em Windows:
   >
   >
   >`<ids-installation-dir>/InDesignServer.com -port 8080 > ~/temp/INDD-logfile.txt 2>&1`

### Configuração do fluxo de trabalho dos ativos AEM {#configuring-the-aem-assets-workflow}

Os ativos AEM têm um fluxo de trabalho pré-configurado para Atualizar ativo **** DAM, que tem várias etapas de processo especificamente para o InDesign:

* [Extração de mídia](#media-extraction)
* [Extração de página](#page-extraction)

<!--
BROKEN LINK This workflow is setup with default values that can be adapted for your setup on the various author instances (this is a standard workflow, so further information is available under [Editing a Workflow](/help/sites-developing/workflows-models.md#configuring-a-workflow-step)). If you are using the default values (including the SOAP port), then no configuration is needed. BROKEN LINK
-->

Após a configuração, o upload de arquivos do InDesign para os ativos AEM (por qualquer um dos métodos habituais) acionará o fluxo de trabalho necessário para processar o ativo e preparar as várias execuções. Teste sua configuração fazendo upload de um `.indd` arquivo para os ativos AEM para confirmar que você vê as diferentes execuções criadas pelo IDS em `<*your_asset*>.indd/Renditions`

#### Extração de mídia {#media-extraction}

Esta etapa controla a extração de mídia do arquivo INDD.

Para personalizar, edite a guia **Argumentos** da etapa Extração **de** mídia.

![Argumentos de extração de mídia e caminhos de script](assets/media_extraction_arguments_scripts.png)

Argumentos de extração de mídia e caminhos de script

* **Biblioteca** ExtendScriptEssa é uma biblioteca de métodos http get/post simples, exigida pelos outros scripts.

* **Estender scripts** Você pode especificar diferentes combinações de scripts aqui. Se você quiser que seus próprios scripts sejam executados no InDesign Server, salve os scripts em `/apps/settings/dam/indesign/scripts`.
Para obter informações sobre scripts do Indesign, consulte:
   [https://www.adobe.com/devnet/indesign/documentation.html#idscripting](https://www.adobe.com/devnet/indesign/documentation.html#idscripting)

>[!CAUTION]
>
>Não **altere a biblioteca** **** ExtendScript.

>Esta biblioteca fornece a funcionalidade HTTP necessária para se comunicar com o Sling. Essa configuração especifica a biblioteca a ser enviada para o InDesign Server para uso lá.
>
O `ThumbnailExport.jsx` script executado pela etapa do fluxo de trabalho de Extração de mídia gera uma execução em miniatura no formato .jpg. Essa execução é usada pela etapa de fluxo de trabalho Processar miniaturas para gerar as execuções estáticas exigidas pelo AEM.

Você pode configurar a etapa de fluxo de trabalho Processar miniaturas para gerar representações estáticas em tamanhos diferentes. Certifique-se de não remover os padrões, pois eles são exigidos pela interface do usuário do AEM Assets. Por fim, a etapa do fluxo de trabalho Excluir representação de visualização de imagem remove a execução de miniatura .jpg, pois ela não é mais necessária.

#### Extração de página {#page-extraction}

Isso cria uma página do AEM a partir dos elementos extraídos. Um manipulador de extração é usado para extrair dados de uma execução (atualmente HTML ou IDML). Esses dados são usados para criar uma página usando o PageBuilder.

Para personalizar, edite a guia **Argumentos** da etapa Extração **de** página.

![chlimage_1-96](assets/chlimage_1-96.png)

* **Manipulador** de extração de página Na lista suspensa, selecione o manipulador que deseja usar. Um manipulador de extração opera em uma representação específica, escolhida por um relacionado `RenditionPicker` (consulte a `ExtractionHandler` API).
Em uma instalação padrão do AEM, o seguinte está disponível:

   * Processador de extração de exportação IDMLopera na `IDML` execução gerada na etapa MediaExtract.

* **Nome** da páginaEspecifique o nome que deseja atribuir à página resultante. Se deixado em branco, o nome será &quot;page&quot; (ou um derivado se &quot;page&quot; já existir).

* **Título** da páginaEspecifique o título que deseja atribuir à página resultante.

* **Caminho**raiz da páginaO caminho para o local raiz da página resultante.
Se deixado em branco, o nó que contém as representações do ativo será usado.

* **Modelo** de páginaO modelo a ser usado ao gerar a página resultante.

* **Design** da páginaO design da página a ser usado ao gerar a página resultante.

### Configuração do trabalho proxy para o InDesign Server {#configuring-the-proxy-worker-for-indesign-server}

>[!NOTE]
O trabalhador reside na instância do proxy.

1. No console Ferramentas, expanda Configurações **de serviços em** nuvem no painel esquerdo. Em seguida, expanda Configuração **de proxy da** Cloud.

1. Clique duas vezes no **IDS worker** para abrir a configuração.

1. Clique em **[!UICONTROL Editar]** para abrir a caixa de diálogo de configuração e definir as configurações necessárias:

   ![proxy_idsworkerconfig](assets/proxy_idsworkerconfig.png)

   * **Pool** IDS Os pontos de extremidade SOAP a serem usados para comunicação com o InDesign Server. Você pode adicionar, remover e ordenar itens necessários.

1. Clique em OK para salvar.

### Configuração do Externalizador de links CQ de dia {#configuring-day-cq-link-externalizer}

Se o servidor do InDesign e o AEM forem executados em hosts diferentes ou se ambos os aplicativos não forem executados em portas padrão, configure o **Day CQ Link Externalizer** para definir o nome do host, a porta e o caminho do conteúdo para o servidor do InDesign.

1. Acesse o Configuration Manager no URL `https://[aem_server]:[port]/system/console/configMgr`.
1. Localize o Externalizador **de links do** Day CQ e clique no ícone **Editar** para abri-lo.
1. Especifique o nome do host e o caminho de contexto para o servidor do Indesign e clique em **Salvar**.

   ![chlimage_1-97](assets/chlimage_1-97.png)

### Ativação do processamento de trabalho paralelo para os servidores InDesign {#enabling-parallel-job-processing-for-indesign-server-s}

Agora você pode ativar o processamento paralelo de tarefas para IDS.

Primeiro, é necessário determinar o número máximo de trabalhos paralelos (`x`) que um InDesign Server pode processar:

* Em uma única máquina com vários processadores, o número máximo de trabalhos paralelos (x) que um InDesign Server pode processar é um menor que o número de processadores executando IDS.
* Ao executar IDS em várias máquinas, é necessário contar o número total de processadores disponíveis (ou seja, em todas as máquinas) e subtrair o número total de máquinas.

Para configurar o número de trabalhos de IDS paralelos:

1. Abra a guia **Configurações** do Console Felix; por exemplo: `https://[aem_server]:[port]/system/console/configMgr`.

1. Selecione a fila de processamento IDS em:

   `Apache Sling Job Queue Configuration`

1. Ajustar:

   * **Tipo** - `Parallel`
   * **Máximo de Trabalhos** Paralelos - `<*x*>` (conforme calculado acima)

1. Salve essas alterações.
1. Ative o suporte multisessão para a CS6 (e superior) verificando:

   `enable.multisession.name` caixa de seleção

   Em:

   `com.day.cq.dam.ids.impl.IDSJobProcessor.name configuration`

1. Crie um [pool de funcionários de `<*x*>` IDS adicionando pontos de extremidade SOAP à configuração](#configuring-the-proxy-worker-for-indesign-server)do IDS Worker.

   Se houver várias máquinas executando os InDesign Servers, adicione pontos de extremidade SOAP (número de processadores por máquina -1) para cada máquina.

   >[!NOTE]
   Você pode optar por ativar a Lista negra de trabalhadores IDS ao trabalhar com um pool de trabalhadores.
   Para fazer isso, ative a caixa de seleção &quot;enable.retry.name&quot;, na `com.day.cq.dam.ids.impl.IDSJobProcessor.name` configuração, que ativa as tentativas de trabalho do IDS.
   Além disso, na `com.day.cq.dam.ids.impl.IDSPoolImpl.name` configuração, defina um valor positivo para o `max.errors.to.blacklist` parâmetro que determina o número de tentativas de tarefa antes de excluir uma IDS da lista de manipuladores de trabalho
   Por padrão, após o tempo configurável (retry.interval.to.whitelist.name) em minutos, o IDS worker é revalidado. Se o trabalhador for encontrado online, ele será removido da lista negra

## Habilitar suporte para o InDesign Server 10.0 ou superior {#enabling-support-for-indesign-server-or-higher}

Para o InDesign Server 10.0 ou superior, execute as seguintes etapas para habilitar o suporte a várias sessões.

1. Abra o Configuration Manager na instância dos ativos AEM `https://[aem_server]:[port]/system/console/configMgr`.
1. Edite a configuração `com.day.cq.dam.ids.impl.IDSJobProcessor.name`.
1. Selecione a opção **[!UICONTROL ids.cc.enable]** e clique em **[!UICONTROL Salvar]**.

>[!NOTE]
Para a integração do InDesign Server com os ativos AEM, use um processador multi-core porque o recurso de suporte à sessão necessário para a integração não é suportado em sistemas de núcleo único.

## Configurar credenciais do AEM {#configure-aem-credentials}

Você pode alterar as credenciais padrão do administrador (nome de usuário e senha) para acessar o servidor do InDesign a partir da instância do AEM sem interromper a integração com o servidor do InDesign.

1. Ir para `/etc/cloudservices/proxy.html`.
1. Na caixa de diálogo, especifique o novo nome de usuário e senha.
1. Salve as credenciais.
