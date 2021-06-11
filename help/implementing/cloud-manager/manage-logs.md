---
title: Gerenciar registros - Cloud Service
description: Gerenciar registros - Cloud Service
exl-id: f17274ce-acf5-4e7d-b875-75d4938806cd
source-git-commit: fa1dd46798d2b8f9b0476e5ad8eb74679fb4beb7
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 13%

---

# Acesso e gerenciamento de registros {#manage-logs}

Os usuários podem acessar uma lista de arquivos de log disponíveis para o ambiente selecionado usando o Cartão de Ambiente.

## Fazendo download de logs {#download-logs}

Siga as etapas abaixo para baixar os logs:

1. Você pode baixar logs por meio da interface do usuário, no cartão **Ambientes** da página **Visão geral**:

![](assets/download-logs1.png)

Ou, na página Detalhes do ambiente :

![](assets/download-logs.png)

>[!NOTE]
>Independentemente de onde ele seja aberto, a mesma caixa de diálogo é exibida e permite que um arquivo de log individual seja baixado.

1. Selecione **Baixar logs** no **..Menu**.

1. No menu suspenso **Service**, selecione opções como **Preview** ou **Preview Dispatcher**, em seguida, clicando no ícone de download. Essa ação também pode ser realizada na página de detalhes do Ambiente .

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
