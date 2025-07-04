---
title: Visualização de conteúdo
description: Saiba como usar o serviço de visualização do AEM para visualizar o conteúdo antes de ele ser publicado.
exl-id: 6b4b57f6-2e66-4c83-94d9-bc1e0daab0f3
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: b93bcb5d26a63babf0b81c92a4fd85d358bfbea7
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 65%

---


# Visualização de conteúdo {#previewing-content}

O AEM oferece um serviço de visualização do Sites que permite que desenvolvedores e autores de conteúdo visualizem a experiência final de um site antes que ele chegue ao ambiente de publicação e esteja disponível publicamente.

Ele facilita a visualização de experiências de página que de outra forma não estariam visíveis no ambiente do autor, como transições de página e demais conteúdos disponíveis somente do lado da publicação.

>[!IMPORTANT]
>
>O acesso ao ambiente de Pré-visualização requer a configuração de um arquivo de inclui na lista de permissões IP. Para obter detalhes, consulte [Acessar o serviço de visualização](/help/implementing/cloud-manager/manage-environments.md#access-preview-service#access-preview-service).
>
>Para obter mais detalhes sobre todos os ambientes, consulte [Gerenciar Ambientes](/help/implementing/cloud-manager/manage-environments.md#access-preview-service).

>[!NOTE]
>
>Como o conteúdo é *publicado* no ambiente de visualização, ele é acessível por URL.

## Publicar conteúdo na visualização {#publishing-content-to-preview}

É possível publicar conteúdo no serviço de visualização usando a interface de **Publicação gerenciada**.

1. No console Sites, selecione a(s) página(s) que deseja enviar para visualização e clique no botão **Gerenciar publicação**.
1. No assistente a seguir, selecione **Visualizar** como destino.

   ![publicação gerenciada](/help/sites-cloud/authoring/assets/previewmanagedpublication.png)

1. Clique em **Próximo** e depois em **Publicar** para confirmar.

1. Uma caixa de diálogo exibirá os URLs para acessar o conteúdo no ambiente de visualização.

   >[!NOTE]
   >
   >Como o conteúdo é *publicado* no ambiente de visualização, ele é acessível por URL (portanto, não precisa de acesso ao AEM).

Como alternativa ao uso dos URLs exibidos no assistente para ver o conteúdo da visualização, você também pode anexar `preview-` ao URL de publicação da sua instância de produção.

```
https://preview-p<programID>-e>environmentID>.adobeaemcloud.com/<pathtopage>.html
```

Consulte [Gerenciamento de ambientes](/help/implementing/cloud-manager/manage-environments.md) para obter mais informações sobre como recuperar as URLs de seus ambientes.

O conteúdo também pode ser publicado para visualização usando uma [árvore de fluxo de trabalho de conteúdo de publicação](/help/operations/replication.md#publish-content-tree-workflow) com o parâmetro `agentId` definido como `preview` ou usando a [API de replicação](/help/operations/replication.md#replication-api) com um `AgentFilter` configurado para visualização.

## Cancelar publicação de conteúdo da visualização {#unpublishing-content-from-preview}

Cancelar a publicação de conteúdo do seu ambiente de **visualização** é basicamente o mesmo processo que [desfazer a publicação de páginas](/help/sites-cloud/authoring/sites-console/publishing-pages.md#unpublishing-pages) do **Publicar** ambiente.

A única diferença é que você pode selecionar o **destino** a ser **visualizado**.
