---
title: Visualização de conteúdo
description: Saiba como usar o serviço de visualização de AEM para visualizar o conteúdo antes de entrar em funcionamento.
exl-id: 6b4b57f6-2e66-4c83-94d9-bc1e0daab0f3
source-git-commit: e70e6ee055c2542752e66e53aa70a9378b1bc5c0
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 1%

---


# Visualização de conteúdo {#previewing-content}

O AEM oferece um serviço de visualização do Sites permite que desenvolvedores e autores de conteúdo visualizem a experiência final de um site antes que ele chegue ao ambiente de publicação e esteja disponível publicamente.

Ela facilita a visualização de experiências de página que de outra forma não estariam visíveis no ambiente do autor, como transições de página e outro conteúdo somente do lado da publicação.

Para obter mais detalhes sobre os ambientes de visualização, consulte o documento [Gerenciar ambientes.](/help/implementing/cloud-manager/manage-environments.md#access-preview-service).

## Publicar conteúdo na visualização {#publishing-content-to-preview}

Você pode publicar conteúdo no serviço de visualização usando o **Publicação gerenciada** IU.

1. No console Sites , selecione as páginas que deseja enviar para visualização e clique no link **Gerenciar publicação** botão
1. No assistente a seguir, selecione **Visualizar** como destino

   ![publicação gerenciada](/help/sites-cloud/authoring/assets/previewmanagedpublication.png)

1. Clique em **Próximo** e depois **Publicar** para confirmar.

1. Uma caixa de diálogo exibirá os URLs para acessar o conteúdo no ambiente de visualização.


Como alternativa usar os URLs exibidos no assistente para ver o conteúdo de visualização, você também pode anexar como prefixo `preview-` para o URL de publicação da sua instância de produção.

```
https://preview-p<programID>-e>environmentID>.adobeaemcloud.com/<pathtopage>.html
```

Consulte o documento [Gerenciamento de ambientes](/help/implementing/cloud-manager/manage-environments.md) para obter mais informações sobre como recuperar os URLs de seus ambientes.

O conteúdo também pode ser publicado para visualização usando um [fluxo de trabalho da árvore de conteúdo de publicação](/help/operations/replication.md#publish-content-tree-workflow) com o `agentId` parâmetro definido como `preview` ou usando o [API de replicação](/help/operations/replication.md#replication-api) com um `AgentFilter` configurado para visualização.

## Configurações do OSGi para a camada de visualização {#configuring-osgi-settings-for-the-preview-tier}

Os valores da propriedade OSGi da camada de visualização são herdados do nível de publicação. No entanto, os valores da camada de visualização podem ser distintos do nível de publicação, definindo a variável `service` para o valor `preview`. O exemplo a seguir de uma propriedade OSGi determina o URL de um endpoint de integração.

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

Siga estas etapas para depurar a camada de visualização usando o Console do desenvolvedor:

* No [Console do desenvolvedor](/help/implementing/developing/introduction/development-guidelines.md#aem-as-a-cloud-service-development-tools), selecione **— Todas as visualizações —** ou um ambiente de produção que inclua **prev** em seu nome
* Gere as informações relevantes para a instância de pré-visualização Consulte [Gerenciamento de ambientes](/help/implementing/cloud-manager/manage-environments.md) para obter mais informações sobre como obter os URLs para seus ambientes.
