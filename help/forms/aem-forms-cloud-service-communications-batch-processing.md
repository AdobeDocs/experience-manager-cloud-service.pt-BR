---
title: Criação de PDF sem esforço - Domine a arte com processamento em lote - Seu guia de autoajuda para gerar milhões de documentos de PDF!
description: Como criar comunicações personalizadas e orientadas à marca?
feature: Adaptive Forms, APIs & Integrations
role: Admin, Developer, User
exl-id: 542c8480-c1a7-492e-9265-11cb0288ce98
source-git-commit: 2b76f1be2dda99c8638deb9633055e71312fbf1e
workflow-type: tm+mt
source-wordcount: '1706'
ht-degree: 2%

---

# Processamento em lote das comunicações as a Cloud Service do AEM Forms

As comunicações permitem criar, montar e fornecer comunicações personalizadas e orientadas à marca, como correspondências comerciais, documentos, declarações, cartas de processamento de solicitações, avisos de benefícios, faturas mensais e kits de boas-vindas. Você pode usar APIs de comunicações para combinar um modelo (XFA ou PDF) com os dados do cliente para gerar documentos nos formatos PDF, PS, PCL, DPL, IPL e ZPL.

As comunicações fornecem APIs para geração de documentos sob demanda e programada. Você pode usar APIs síncronas para APIs sob demanda e em lote (APIs assíncronas) para a geração agendada de documentos:

* As APIs síncronas são adequadas para casos de uso de geração de documento de registro único, latência baixa e sob demanda. Essas APIs são mais adequadas para casos de uso baseados em ações do usuário. Por exemplo, gerar um documento após um usuário preencher um formulário.

* As APIs em lote (APIs assíncronas) são adequadas para casos de uso programados de alta taxa de transferência na geração de vários documentos. Essas APIs geram documentos em lotes. Por exemplo, contas telefônicas, demonstrativos de cartão de crédito e demonstrativos de benefícios gerados todo mês.

<!-- The following skills are required to create templates and use HTTP APIs: 

* Understanding of Adobe Forms Designer or Acrobat Forms to create templates

* Understanding of HTTP APIs and experience of using HTTP APIs

* Basic understanding of Adobe Experience Manager -->


## Operações em lote {#batch-operations}

Uma operação em lote é um processo de geração de vários documentos de tipo semelhante para um conjunto de registros em intervalos programados. Uma operação em lote tem duas partes: configuração (definição) e execução.

* **Configuração (definição)**: uma configuração em lote armazena informações sobre vários ativos e propriedades a serem definidas para documentos gerados. Por exemplo, ele fornece detalhes sobre o modelo XDP ou PDF e o local dos dados do cliente a serem usados, juntamente com a especificação de várias propriedades para documentos de saída.

* **Execução**: para iniciar uma operação em lote, passe o nome da configuração do lote para a API de execução de lote.

### Componentes de uma operação em lote {#components-of-a-batch-operations}

**Configuração na nuvem**: a configuração da Experience Manager Cloud ajuda a conectar uma instância do Experience Manager ao Armazenamento do Microsoft Azure de propriedade do cliente. Ele permite especificar as credenciais da conta do Microsoft Azure de propriedade do cliente para se conectar a ele.

**Configuração do armazenamento de dados em lote (USC)**: a configuração de dados em lote ajuda a configurar uma instância específica do armazenamento de Blob para APIs em lote. Ele permite especificar os locais de entrada e saída no armazenamento do Microsoft Azure Blob de propriedade do cliente.

**APIs em lote**: permite criar configurações em lote e executar as execuções em lote com base nessas configurações para mesclar um modelo PDF ou XDP com dados e gerar saída nos formatos PDF, PS, PCL, DPL, IPL e ZPL. As comunicações fornecem APIs em lote para gerenciamento de configuração e execução em lote.

![data-merge-table](assets/communications-batch-structure.png)

**Armazenamento**: as APIs de comunicação usam o armazenamento na nuvem do Microsoft Azure de propriedade do cliente para buscar registros do cliente e armazenar documentos gerados. Você configura o Armazenamento do Microsoft Azure na Configuração de Experience Manager Cloud Service.

**Aplicativo**: Seu aplicativo personalizado para usar as APIs de lote para gerar e consumir documentos.

## Gerar vários documentos usando operações em lote {#generate-multiple-documents-using-batch-operations}

Você pode usar operações em lote para gerar vários documentos em intervalos programados.

>[!VIDEO](https://video.tv.adobe.com/v/338349)

Você pode assistir ao vídeo ou executar as instruções abaixo para saber como gerar documentos usando operações em lote. A documentação de referência da API usada em vídeo está disponível no formato .yaml. Você pode baixar o [APIs em lote](assets/batch-api.yaml) e carregue-o no Postman para verificar a funcionalidade das APIs e acompanhar o vídeo.

### Pré-requisitos {#pre-requisites}

Para usar a API de lote, é necessário o seguinte:

* [Conta de Armazenamento do Microsoft Azure](https://docs.microsoft.com/en-us/azure/storage/common/storage-account-create)
* Modelos PDF ou XDP
* [Dados a serem mesclados com modelos](#form-data)
* Usuários com privilégios de administrador de Experience Manager

### Configurar o ambiente {#setup-your-environment}

Antes de usar uma operação em lote:

* Fazer upload dos dados do cliente (arquivos XML) para o Armazenamento de blobs do Microsoft Azure
* Criar uma configuração na nuvem
* Criar configuração de armazenamento de dados em lote
* Faça upload de modelos e outros ativos para sua instância do Experience Manager Forms Cloud Service

### Fazer upload dos dados do cliente (arquivos XML) para o Armazenamento do Azure {#upload-customer-data-to-Azure-Storage}

No Armazenamento do Microsoft Azure, crie [contêineres](https://docs.microsoft.com/en-us/azure/vs-azure-tools-storage-explorer-blobs) e [fazer upload dos dados do cliente (XML)](https://docs.microsoft.com/en-us/azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container) para o [pastas](https://docs.microsoft.com/en-us/azure/storage/blobs/storage-quickstart-blobs-portal) dentro dos contêineres.
>[!NOTE]
>
>Você pode configurar o armazenamento do Microsoft Azure para limpar automaticamente a pasta de entrada ou mover o conteúdo da pasta de saída para um local diferente em intervalos programados. No entanto, certifique-se de que as pastas não sejam limpas quando uma operação em lote que faz referência às pastas ainda estiver em execução.

### Criar uma configuração na nuvem {#create-a-cloud-configuration}

A configuração da nuvem conecta sua instância do Experience Manager ao Armazenamento do Microsoft Azure. Para criar uma configuração na nuvem:

1. Acesse Ferramentas > Cloud Service > Armazenamento do Azure
1. Abra uma pasta para hospedar a configuração e clique em Criar. Você usa a pasta Global ou cria uma pasta.
1. Especifique o nome da configuração e as credenciais para se conectar ao serviço. Você pode [recuperar essas credenciais do portal de armazenamento do Microsoft Azure](https://docs.microsoft.com/en-us/azure/storage/common/storage-account-keys-manage?tabs=azure-portal#view-account-access-keys).
1. Clique em Criar.

Sua instância do Experience Manager agora está pronta para se conectar ao Armazenamento do Microsoft Azure e usá-la para armazenar e ler conteúdo, quando necessário.

### Criar configuração de armazenamento de dados em lote {#create-batch-data-store-configuration}

A configuração de dados em lote ajuda a configurar containers e pastas para entrada e saída. Você mantém os registros do cliente na Pasta do Source e os documentos gerados são colocados na Pasta de destino.

Para criar a configuração:

1. Acesse Ferramentas > Forms > Conector de armazenamento unificado.
1. Abra uma pasta para hospedar a configuração e clique em Criar. Você usa a pasta Global ou cria uma pasta.
1. Especifique o Título e o Nome da configuração. Em Armazenamento, selecione Armazenamento do Microsoft Azure.
1. Em Caminho de configuração de armazenamento, procure e selecione a Configuração na nuvem que contém credenciais da conta de armazenamento do Azure de propriedade do cliente.
1. Na Pasta do Source, especifique o nome do contêiner de Armazenamento do Azure e a pasta que contém os registros.
1. Na Pasta de destino, especifique o caminho do contêiner de Armazenamento do Azure e a pasta para armazenar os documentos gerados.
1. Clique em Criar.

Sua instância do Experience Manager agora está conectada ao Armazenamento do Microsoft Azure e configurada para recuperar e enviar dados para locais específicos no Armazenamento do Microsoft Azure.

### Faça upload de modelos e outros ativos para sua instância do Experience Manager {#upload-templates-and-other-assets-to-your-AEM-instance}

Uma organização normalmente tem vários modelos. Por exemplo, um modelo para demonstrativos de cartão de crédito, demonstrativos de benefícios e aplicações de reivindicação. Faça upload de todos esses modelos XDP e PDF para sua instância Experience Manager. Para fazer upload de um modelo:

1. Abra a instância do Experience Manager.
1. Vá até Forms > Forms e Documentos
1. Clique em Criar > Pasta e crie uma pasta. Abra a pasta.
1. Clique em Criar > Upload de arquivo e faça upload dos modelos.

## Usar a API em lote para gerar documentos {#use-batch-API-to-generate-documents}

Para usar uma API de lote, crie uma configuração de lote e execute uma execução com base nessa configuração. A documentação da API fornece informações sobre APIs para criar e executar um lote, parâmetros correspondentes e possíveis erros. Você pode baixar o [Arquivo de definição de API](assets/batch-api.yaml) arquivo e carregue-o para [Postman](https://go.postman.co/home) ou software semelhante para testar as APIs para criar e executar uma operação em lote.

### Criar um lote {#create-a-batch}

Para criar um lote, use o `POST /config` API. Inclua as seguintes propriedades obrigatórias no corpo da solicitação HTTP:

* **configName**: especifique o Nome exclusivo do lote. Por exemplo, `wknd-job`
* **dataSourceConfigUri**: especifique o local da configuração do Armazenamento de dados em lote. Pode ser o caminho relativo ou absoluto da configuração. Por exemplo: `/conf/global/settings/forms/usc/batch/wknd-batch`
* **outputTypes**: Especificar formatos de saída: PDF e PRINT. Se você usar o tipo de saída PRINT, em `printedOutputOptionsList` especifique pelo menos uma opção de impressão. As opções de impressão são identificadas por seu tipo de renderização, portanto, no momento, não são permitidas várias opções de impressão com o mesmo tipo de renderização. Os formatos compatíveis são PS, PCL, DPL, IPL e ZPL.

* **modelo**: especifique o caminho absoluto ou relativo do modelo. Por exemplo, `crx:///content/dam/formsanddocuments/wknd/statements.xdp`

Se você especificar um caminho relativo, forneça também uma raiz de conteúdo. Consulte a documentação da API para obter detalhes da raiz do conteúdo.

<!-- For example, you include the following JSON in the body of HTTP APIs to create a batch named wknd-job: -->

Você pode usar `GET /config /[configName]` para ver detalhes da configuração do lote.

### Executar um lote {#run-a-batch}

Para executar (executar) um lote, use o `POST /config /[configName]/execution`. Por exemplo, para executar um lote chamado wknd-demo, use /config/wknd-demo/execution. O servidor retorna o código de resposta HTTP 202 ao aceitar a solicitação. A API não retorna qualquer carga útil, exceto um código exclusivo (identificador de execução) no cabeçalho da resposta HTTP para o trabalho em lote em execução no servidor. Você pode usar o identificador de execução para recuperar o status do lote.

>[!NOTE]
>
>Enquanto o lote estiver em execução, não faça alterações nas pastas de origem e destino correspondentes, na configuração da fonte de dados e na configuração da nuvem do Microsoft Azure.

### Verificar status de um lote {#status-of-a-batch}

Para recuperar o status de um lote, use o `GET /config /[configName]/execution/[execution-identifier]`. O identificador de execução é incluído no cabeçalho da resposta HTTP para a solicitação de execução em lote.

A resposta da solicitação de status contém a seção de status. Ele fornece detalhes sobre o status do trabalho em lote, o número de registros já no pipeline (já lidos e sendo processados) e o status de cada outputType/renderType (número de itens em andamento, com êxito e com falha). O status também inclui as horas inicial e final do processo em lote, juntamente com informações sobre erros, se houver. A hora final é -1 até que a execução do lote seja realmente concluída.

>[!NOTE]
>
>* Quando você solicita vários formatos de IMPRESSÃO, o status contém várias entradas. Por exemplo, PRINT/ZPL, PRINT/IPL.
>* Um processo em lote não lê todos os registros simultaneamente. Em vez disso, o processo continua lendo e incrementando o número de registros. Portanto, o status retorna -1 até que todos os registros tenham sido lidos.

### Visualizar documentos gerados {#view-generated-documents}

Na conclusão do trabalho, os documentos gerados são armazenados no `success` pasta no local de destino especificado na configuração do Armazenamento de dados em lote. Se houver erros, o serviço criará um `failure` pasta. Ela fornece informações sobre o tipo e a razão dos erros.

Vamos entender com a ajuda de um exemplo: suponha que haja um arquivo de dados de entrada `record1.xml` e dois tipos de saída: `PDF` e `PCL`. Em seguida, o local de destino contém duas subpastas `pdf` e `pcl`, um para cada tipo de saída. Vamos supor que a geração de PDF tenha êxito e, em seguida, o `pdf` a subpasta contém o `success` subpasta que contém o documento de PDF gerado `record1.pdf`. Vamos supor que a geração de PCL falhou, então a variável `pcl` a subpasta contém um `failure` subpasta que contém um arquivo de erro `record1.error.txt` que contém detalhes do erro. Além disso, o local de destino contém uma pasta temporária chamada `__tmp__` que contém determinados arquivos necessários durante a execução do lote. Essa pasta pode ser excluída quando não houver execuções de lote ativas que façam referência à pasta de destino.

>[!NOTE]
>
>O processamento de um lote pode levar algum tempo, dependendo do número de registros de entrada e da complexidade do modelo, aguarde alguns minutos antes de verificar as pastas de destino em busca de arquivos de saída.

## Documentação de referência da API

A documentação de referência da API fornece informações detalhadas sobre todos os parâmetros, métodos de autenticação e vários serviços fornecidos pelas APIs. A documentação de referência da API está disponível no formato .yaml. Você pode baixar o [APIs em lote](assets/batch-api.yaml) e carregue-o no Postman para verificar a funcionalidade das APIs.

>[!MORELIKETHIS]
>
>* [Introdução às comunicações as a Cloud Service do AEM Forms](/help/forms/aem-forms-cloud-service-communications-introduction.md)
>* [Arquitetura as a Cloud Service do AEM Forms para APIs de Forms adaptável e comunicação](/help/forms/aem-forms-cloud-service-architecture.md)
>* [Processamento de comunicação - APIs síncronas](/help/forms/aem-forms-cloud-service-communications.md)
>* [Processamento de comunicação - APIs em lote](/help/forms/aem-forms-cloud-service-communications-batch-processing.md)