---
title: Visualização de conteúdo
description: Saiba como usar o serviço de visualização do AEM para visualizar o conteúdo antes de ele ser publicado.
exl-id: 6b4b57f6-2e66-4c83-94d9-bc1e0daab0f3
source-git-commit: dc55bd43641c03dd022a891c8b85569d9be28ebe
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 100%

---


# Visualização de conteúdo {#previewing-content}

O AEM oferece um serviço de visualização do Sites que permite que desenvolvedores e autores de conteúdo visualizem a experiência final de um site antes que ele chegue ao ambiente de publicação e esteja disponível publicamente.

Ele facilita a visualização de experiências de página que de outra forma não estariam visíveis no ambiente do autor, como transições de página e demais conteúdos disponíveis somente do lado da publicação.

Para obter mais detalhes sobre os ambientes de visualização, consulte o documento [Gerenciar ambientes.](/help/implementing/cloud-manager/manage-environments.md#access-preview-service)

>[!NOTE]
>
>A publicação de um fragmento de experiência para visualização segue basicamente o mesmo procedimento de publicação de uma página, mas a partir do console ou do editor de fragmentos de experiência.

## Publicar conteúdo na visualização {#publishing-content-to-preview}

É possível publicar conteúdo no serviço de visualização usando a interface de **Publicação gerenciada**.

1. No console do Sites, selecione a(s) página(s) que deseja enviar para visualização e clique no botão **Gerenciar publicação** 
1. No assistente a seguir, selecione **Visualizar** como destino

   ![publicação gerenciada](/help/sites-cloud/authoring/assets/previewmanagedpublication.png)

1. Clique em **Próximo** e depois em **Publicar** para confirmar.

1. Uma caixa de diálogo exibirá os URLs para acessar o conteúdo no ambiente de visualização.


Como alternativa ao uso dos URLs exibidos no assistente para ver o conteúdo da visualização, você também pode anexar `preview-` ao URL de publicação da sua instância de produção.

```
https://preview-p<programID>-e>environmentID>.adobeaemcloud.com/<pathtopage>.html
```

Consulte o documento [Gerenciamento de ambientes](/help/implementing/cloud-manager/manage-environments.md) para obter mais informações sobre como recuperar os URLs de seus ambientes.

O conteúdo também pode ser publicado para visualização usando uma [árvore de fluxo de trabalho de conteúdo de publicação](/help/operations/replication.md#publish-content-tree-workflow) com o parâmetro `agentId` definido como `preview` ou usando a [API de replicação](/help/operations/replication.md#replication-api) com um `AgentFilter` configurado para visualização.

## Cancelar publicação de conteúdo da visualização {#unpublishing-content-from-preview}

Cancelar a publicação de conteúdo do seu ambiente de **visualização** é basicamente o mesmo processo que [desfazer a publicação de páginas](/help/sites-cloud/authoring/fundamentals/publishing-pages.md#unpublishing-pages) do **Publicar** ambiente.

A única diferença é que você pode selecionar o **destino** a ser **visualizado**.

## Configurações do OSGi para o nível de visualização {#configuring-osgi-settings-for-the-preview-tier}

Os valores da propriedade OSGi do nível de visualização são herdados do nível de publicação. No entanto, os valores do nível de visualização podem ser distintos do nível de publicação, definindo o parâmetro `service` para o valor `preview`. O exemplo a seguir de uma propriedade OSGi determina o URL de um endpoint de integração.

```
[
{
"name":"INTEGRATION_URL",
"type":"string",
"value":"http://s2.integrationvendor.com",
"service": "preview"
}
]
```

Para obter mais informações, consulte [esta seção](/help/implementing/deploying/configuring-osgi.md#author-vs-publish-configuration) da documentação de configuração do OSGi.

## Depuração da visualização usando o Console do desenvolvedor {#debugging-preview-using-the-developer-console}

Siga estas etapas para depurar o nível de visualização usando o Console do Desenvolvedor:

* No [Console do Desenvolvedor](/help/implementing/developing/introduction/development-guidelines.md#aem-as-a-cloud-service-development-tools), selecione **-- Todas as visualizações --** ou um ambiente de produção que inclua **prev** no nome
* Gere as informações relevantes para a instância de visualização 
Consulte [Gerenciamento de ambientes](/help/implementing/cloud-manager/manage-environments.md) para obter mais informações sobre como obter os URLs para seus ambientes.
