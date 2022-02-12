---
title: Arquitetura de AEM sem Cabeça
description: Saiba mais sobre a arquitetura de alto nível do Adobe Experience Manager, pois ela se relaciona a uma implantação sem periféricos. Entenda a função dos serviços de Autor, Visualização e Publicação do AEM e o padrão de implantação recomendado para aplicativos sem cabeçalho.
feature: Content Fragments,GraphQL API
source-git-commit: 64b2beb4af2297e19e39ad534856bce33ffcfcf8
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 0%

---


# Arquitetura de AEM sem Cabeça

Um ambiente de AEM típico é composto de um Serviço de criação, Serviço de publicação e um Serviço de visualização opcional.

* **O serviço Autor** é onde os usuários internos criam, gerenciam e visualizam o conteúdo.

* **O serviço de publicação** O é considerado o ambiente &quot;Live&quot; e normalmente é com o que os usuários finais interagem. O conteúdo, após ser editado e aprovado no serviço Autor, é distribuído ao serviço de Publicação. O padrão de implantação mais comum com AEM aplicativos sem cabeçalho é ter a versão de produção do aplicativo conectada a um serviço de publicação do AEM.

* **O serviço de Pré-visualização** é funcionalmente igual ao **Serviço de publicação**. No entanto, ele é disponibilizado apenas para usuários internos. Isso torna o sistema ideal para os aprovadores revisarem as alterações futuras no conteúdo antes de serem disponibilizadas para os usuários finais.

* **O Dispatcher** é um servidor Web estático aumentado com o módulo Dispatcher do AEM. Ele fornece recursos de armazenamento em cache e outra camada de segurança. O **Dispatcher** fica na frente do **Publicar** e **Visualizar** serviços.

Em um Programa AEM as a Cloud Service, você pode ter vários ambientes, Dev, Stage e Prod. Cada ambiente teria seu próprio **Autor**, **Publicar** e **Visualizar** serviços. Saiba mais sobre como gerenciar [ambientes aqui](/help/implementing/cloud-manager/manage-environments.md)

## Modelo de publicação do autor

O padrão de implantação mais comum com AEM aplicativos sem cabeçalho é ter a versão de produção do aplicativo conectada a um serviço de publicação do AEM.

![Arquitetura de publicação de autor](assets/autho-publish-architecture-diagram.png)

O diagrama acima descreve esse padrão de implantação comum.

1. A **Autor do conteúdo** O usa o serviço Autor do AEM para criar, editar e gerenciar conteúdo.
1. O **Autor do conteúdo** e outros usuários internos podem visualizar o conteúdo diretamente no serviço Autor. É possível configurar uma versão de Visualização do aplicativo que se conecta ao serviço Autor.
1. Depois que o conteúdo é aprovado, ele pode ser publicado no serviço de publicação do AEM.
1. O **Dispatcher** é uma camada na frente do **Publicar** que pode armazenar em cache determinadas solicitações e fornece uma camada de segurança.
1. Os usuários finais interagem com a versão Produção do aplicativo. O aplicativo Production se conecta ao serviço de Publicação por meio do Dispatcher e usa as APIs GraphQL para solicitar e consumir conteúdo.

## Implantação de publicação da visualização do autor

Outra opção para implantações sem periféricos é incorporar um **Visualização de AEM** serviço. Com essa abordagem, o conteúdo pode ser publicado primeiro na **Visualizar** e uma versão de visualização do aplicativo sem cabeçalho pode se conectar a ele. A vantagem dessa abordagem é que a variável **Visualizar** pode ser configurado com os mesmos requisitos e permissões de autenticação que o **Publicar** , facilitando a simulação da experiência de produção.

![Arquitetura de visualização e publicação do autor](assets/author-preview-publish-architecture-diagram.png)

1. A **Autor do conteúdo** O usa o serviço Autor do AEM para criar, editar e gerenciar conteúdo.
1. O conteúdo é publicado pela primeira vez no serviço de Visualização de AEM.
1. É possível configurar uma versão de Visualização do aplicativo que se conecta ao serviço de Visualização.
1. Depois que o conteúdo é revisado e aprovado, ele pode ser publicado no serviço de publicação do AEM.
1. Os usuários finais interagem com a versão Produção do aplicativo. O aplicativo Production se conecta ao serviço de Publicação por meio do Dispatcher e usa as APIs GraphQL para solicitar e consumir conteúdo.

