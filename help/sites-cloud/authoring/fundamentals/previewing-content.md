---
title: Visualização de conteúdo
description: Saiba como usar o Serviço de visualização de AEM para visualizar o conteúdo antes de entrar no ar.
source-git-commit: 9b4ac173c55380cbc06de64677470818aa801df4
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 0%

---


# Visualizar conteúdo {#previewing-content}

>[!NOTE]
>
>O recurso de Visualização faz parte da versão 2021.5.0 e será lançado gradualmente nas próximas semanas.

O AEM oferece um Serviço de visualização de sites desenvolvido para permitir que desenvolvedores e autores de conteúdo visualizem a experiência final de um site antes que ele chegue ao ambiente de publicação e esteja disponível publicamente.

Ele facilita a visualização de experiências de página que de outra forma não estariam visíveis no ambiente do autor, como transições de página e outro conteúdo somente do lado da publicação.

## Publicar conteúdo na visualização {#publishing-content-to-preview}

Você pode publicar conteúdo no Serviço de visualização usando a interface do usuário de publicação gerenciada da seguinte maneira:

1. Selecione as páginas que deseja enviar para visualização no console de sites e clique no botão **Gerenciar publicação**
1. No assistente a seguir, selecione **Preview** como destino

   ![publicação gerenciada](/help/sites-cloud/authoring/assets/previewmanagedpublication.png)

1. Clique em **Next** e em **Publish** para confirmar.

O conteúdo da visualização é exibido, anexe **preview** ao URL de publicação da instância de produção. O URL deve ser construído desta forma:

```
https://preview-p[programID]-e[environmentID].adobeaemcloud.com/pathtopage.html
```

Consulte [Gerenciar seus ambientes](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/manage-your-environment.html?lang=en) para obter mais informações sobre como obter os URLs dos seus ambientes.

