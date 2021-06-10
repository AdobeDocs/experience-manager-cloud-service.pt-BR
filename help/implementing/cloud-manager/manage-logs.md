---
title: Gerenciar registros - Cloud Service
description: Gerenciar registros - Cloud Service
exl-id: f17274ce-acf5-4e7d-b875-75d4938806cd
source-git-commit: 2411c2d1472abaa2af7b2a71938d753bb98db95c
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 17%

---

# Acesso e gerenciamento de registros {#manage-logs}

Os usuários podem acessar uma lista de arquivos de log disponíveis para o ambiente selecionado usando o Cartão de Ambiente.  Os usuários podem acessar uma lista de arquivos de log disponíveis para o ambiente selecionado.

Esses arquivos podem ser baixados por meio da interface do usuário, na página **Visão geral**:

![](assets/download-logs1.png)

Ou a página **Ambientes**:

![](assets/download-logs.png)

>[!NOTE]
>Independentemente de onde ele seja aberto, a mesma caixa de diálogo é exibida e permite que um arquivo de log individual seja baixado.

![](assets/download-logs2.png)

## Baixando registros para o serviço de visualização {#download-preview-service}

O usuário pode baixar logs para o serviço de visualização

1. Navegue até o cartão **Ambientes** na página **Visão geral** do Cloud Manager.

1. Selecione os logs de download no menu ... .

1. Nas opções suspensas do serviço, selecione **Visualizar** ou **Visualizar Dispatcher**, seguido de clicar no ícone de download.

   >[!NOTE]
   >Essa ação também pode ser realizada na página de detalhes do Ambiente .

   ![](assets/download-preview.png)


## Faz logon pela API {#logs-through-api}

Além de baixar logs por meio da interface do usuário, os logs estarão disponíveis por meio da API e da Interface da linha de comando.

Por exemplo, para baixar os arquivos de log para um ambiente específico, o comando seria algo sozinho nas linhas de

```java
$ aio cloudmanager:download-logs --programId 5 1884 author aemerror
```

O comando a seguir permite o rastreamento dos logs:

```java
$ aio cloudmanager:tail-log --programId 5 1884 author aemerror
```

Para obter a ID de ambiente (1884 neste caso) e as opções de serviço ou nome de log disponíveis, você pode usar:

```java
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

>[!NOTE]
>Embora os **Downloads de registro** estejam disponíveis na interface do usuário e na API, o **Resíduo de registro** é somente API/CLI.

### Recursos adicionais {#resources}

Consulte os seguintes recursos adicionais para saber mais sobre a API do Cloud Manager e a CLI do Adobe I/O:

* [Documentação da API do Cloud Manager](https://www.adobe.io/apis/experiencecloud/cloud-manager/docs.html)
* [Adobe I/O CLI](https://github.com/adobe/aio-cli-plugin-cloudmanager)
