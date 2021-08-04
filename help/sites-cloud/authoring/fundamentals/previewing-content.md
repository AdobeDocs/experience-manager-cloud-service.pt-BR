---
title: Visualização de conteúdo
description: Saiba como usar o Serviço de visualização de AEM para visualizar o conteúdo antes de entrar no ar.
exl-id: 6b4b57f6-2e66-4c83-94d9-bc1e0daab0f3
source-git-commit: 78c5649c6b9c04cb459f5730161affeb452c916c
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 0%

---

# Visualização de conteúdo {#previewing-content}

>[!NOTE]
>
>Para ativar o recurso de visualização em ambientes criados antes de 3 de agosto de 2021, verifique se o ambiente está AEM versão 2021.05.5368.20210529T101701Z ou superior e execute um pipeline iniciado pelo cliente.

O AEM oferece um Serviço de visualização de sites desenvolvido para permitir que desenvolvedores e autores de conteúdo visualizem a experiência final de um site antes que ele chegue ao ambiente de publicação e esteja disponível publicamente.

Ele facilita a visualização de experiências de página que de outra forma não estariam visíveis no ambiente do autor, como transições de página e outro conteúdo somente do lado da publicação.

Leia também sobre [como acessar o serviço de Visualização](/help/implementing/cloud-manager/manage-environments.md#access-preview-service).

## Publicar conteúdo na visualização {#publishing-content-to-preview}

Você pode publicar conteúdo no Serviço de visualização usando a interface do usuário de publicação gerenciada da seguinte maneira:

1. Selecione as páginas que deseja enviar para visualização no console de sites e clique no botão **Gerenciar publicação**
1. No assistente a seguir, selecione **Preview** como destino

   ![publicação gerenciada](/help/sites-cloud/authoring/assets/previewmanagedpublication.png)

1. Clique em **Next** e em **Publish** para confirmar.

1. Uma caixa de diálogo exibirá os URLs para acessar o conteúdo no ambiente de Visualização.

   Ou para ver o conteúdo da visualização, você também pode anexar **preview** ao URL de publicação da instância de produção.

   O URL deve ser construído desta forma:

   ```
   https://preview-p[programID]-e[environmentID].adobeaemcloud.com/pathtopage.html
   ```

Consulte [Gerenciamento de ambientes](/help/implementing/cloud-manager/manage-environments.md) para obter mais informações sobre como obter os URLs dos seus ambientes.

O conteúdo também pode ser publicado para visualização usando um [Fluxo de trabalho da árvore de conteúdo de publicação](/help/operations/replication.md#publish-content-tree-workflow) com o parâmetro agentId definido para visualização ou usando a [API de replicação](/help/operations/replication.md#replication-api) com um AgentFilter configurado para visualização.

## Configurações do OSGi para a camada de visualização {#configuring-osgi-settings-for-the-preview-tier}

Os valores da propriedade OSGI da camada de visualização são herdados do nível de publicação, mas os valores da camada de visualização podem ser distintos do nível de publicação usando valores específicos do ambiente definindo o parâmetro de serviço com o valor &quot;pré-visualização&quot;. Tome o exemplo abaixo de uma propriedade OSGI que determina o URL de um endpoint de integração:

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

* No [Console do Desenvolvedor](/help/implementing/developing/introduction/development-guidelines.md#aem-as-a-cloud-service-development-tools), selecione **— Todas as visualizações —** ou um ambiente de produção que inclua **prev** no seu nome
* Gerar as informações relevantes para a instância de visualização
Consulte [Gerenciamento de ambientes](/help/implementing/cloud-manager/manage-environments.md) para obter mais informações sobre como obter os URLs dos seus ambientes.
