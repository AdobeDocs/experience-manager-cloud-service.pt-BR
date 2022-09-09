---
title: Acesso e gerenciamento de registros
description: Saiba como acessar e gerenciar logs para auxiliar seu processo de desenvolvimento AEM as a Cloud Service.
exl-id: f17274ce-acf5-4e7d-b875-75d4938806cd
source-git-commit: a9303c659730022b7417fc9082dedd26d7cbccca
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 8%

---


# Acesso e gerenciamento de registros {#manage-logs}

Saiba como acessar e gerenciar logs para auxiliar seu processo de desenvolvimento AEM as a Cloud Service.

Você pode acessar uma lista de arquivos de log disponíveis para o ambiente selecionado usando o **Ambientes** do cartão **Visão geral** página ou página Detalhes do ambiente .

## Download de logs {#download-logs}

Siga estas etapas para baixar logs.

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriados.

1. Navegue até o **Ambientes** do cartão **Visão geral** página.

1. Selecionar **Baixar logs** no menu reticências.

   ![Item de menu dos logs de download](assets/download-logs1.png)

1. No **Baixar logs** , selecione o **Serviço** no menu suspenso

   ![Caixa de diálogo Baixar logs](assets/download-preview.png)

1. Após selecionar seu serviço, clique no ícone de download ao lado do log que deseja recuperar.

Você também pode acessar seus logs do **Ambientes** página.

![Logs da tela Ambientes](assets/download-logs.png)

## Logs via API {#logs-through-api}

Além de baixar logs por meio da interface do usuário, os logs estão disponíveis por meio da API e da interface da linha de comando.

Para baixar os arquivos de log de um ambiente específico, o comando seria semelhante ao seguinte.

```shell
$ aio cloudmanager:download-logs --programId 5 1884 author aemerror
```

Também é possível rastrear logs por meio da interface da linha de comando.

```shell
$ aio cloudmanager:tail-log --programId 5 1884 author aemerror
```

Para obter a ID de ambiente (1884 neste exemplo) e as opções de serviço ou nome de log disponíveis, você pode usar os seguintes comandos.

```shell
$ aio cloudmanager:list-environments
Environment Id Name                     Type  Description                          
1884           FoundationInternal_dev   dev   Foundation Internal Dev environment  
1884           FoundationInternal_stage stage Foundation Internal STAGE environment
1884           FoundationInternal_prod  prod  Foundation Internal Prod environment
 
 
$ aio cloudmanager:list-available-log-options 1884
Environment Id Service    Name         
1884           author     aemerror     
1884           author     aemrequest   
1884           author     aemaccess    
1884           publish    aemerror     
1884           publish    aemrequest   
1884           publish    aemaccess    
1884           dispatcher httpderror   
1884           dispatcher aemdispatcher
1884           dispatcher httpdaccess
```

### Recursos adicionais {#resources}

Consulte os seguintes recursos adicionais para saber mais sobre a API do Cloud Manager e a CLI do Adobe I/O:

* [Documentação da API do Cloud Manager](https://www.adobe.io/apis/experiencecloud/cloud-manager/docs.html)
* [Adobe I/O CLI](https://github.com/adobe/aio-cli-plugin-cloudmanager)
