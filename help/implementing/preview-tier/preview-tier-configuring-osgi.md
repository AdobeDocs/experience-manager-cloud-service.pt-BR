---
title: Configurações do OSGi para o nível de visualização
description: Saiba como configurar o serviço de visualização de AEM para visualizar o conteúdo antes de entrar em vigor.
source-git-commit: 7b56bb05e31d7a61d7a8fb13e2bd0ff6e4fb301d
workflow-type: tm+mt
source-wordcount: '222'
ht-degree: 64%

---


# Configurações do OSGi para o nível de visualização {#configure-osgi-preview-tier}

O AEM oferece um serviço de visualização do Sites que permite que desenvolvedores e autores de conteúdo visualizem a experiência final de um site antes que ele chegue ao ambiente de publicação e esteja disponível publicamente.

Ele facilita a visualização de uma variedade de experiências que de outra forma não estariam visíveis no ambiente do autor. Por exemplo, transições de página, fragmentos de experiência e outro conteúdo somente do lado da publicação.

Os valores da propriedade OSGi do nível de visualização são herdados do nível de publicação. No entanto, os valores do nível de visualização podem ser distintos do nível de publicação, definindo o parâmetro `service` para o valor `preview`.

>[!NOTE]
>
>Para obter mais detalhes sobre os ambientes de visualização, consulte o documento [Gerenciar ambientes.](/help/implementing/cloud-manager/manage-environments.md#access-preview-service)

## Definição das configurações do OSGi para a camada de visualização {#configuring-osgi-settings-for-the-preview-tier}

O exemplo a seguir de uma propriedade OSGi determina o URL de um endpoint de integração.

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
