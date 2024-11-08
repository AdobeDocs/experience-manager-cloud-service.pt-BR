---
title: Publicar páginas com o DAM Assets usando o Edge Delivery Services
description: Saiba quais configurações são necessárias para garantir que os ativos DAM das suas páginas sejam publicados perfeitamente no Edge Delivery Services.
feature: Edge Delivery Services
role: Admin, Architect, Developer
source-git-commit: 65a3b4d923a91702e7ea9b13356802836fa4ce0b
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 2%

---


# Publicar páginas com o DAM Assets usando o Edge Delivery Services {#dam-assets}

Saiba quais configurações são necessárias para garantir que os ativos DAM das suas páginas sejam publicados perfeitamente no Edge Delivery Services.

## Universal Editor, DAM Assets e Edge Delivery {#overview}

Ao editar o conteúdo para o Editor universal, é claro que você pode selecionar ativos do DAM. Ao publicar seu conteúdo no Edge Delivery Services, o conteúdo do DAM relacionado também é publicado.

Para garantir esse comportamento contínuo, o AEM e os Edge Delivery Services devem ter acesso adequado ao DAM para publicar. Isso inclui:

* [Garantia de que as pastas de ativos estejam acessíveis.](#accessible)
* [Verificando se a pasta de ativos recebeu a configuração adequada (conforme necessário).](#configuration)

## Garantia de que as pastas do Assets estejam acessíveis {#accessible}

Ao publicar páginas do AEM no Edge Delivery Services, [uma conta técnica](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md) é usada. Essa conta, com um nome no formato `<hash>@techacct.adobe.com`, é criada automaticamente como um usuário no AEM pela Cloud Manager sempre que você publica pela primeira vez uma página criada com o Editor Universal.

![Conta técnica](/help/edge/wysiwyg-authoring/assets/dam-assets/technical-account.png)

Essa conta técnica deve ter direitos de acesso a todas as pastas do DAM para publicar seu conteúdo. Você pode:

* Não usar pastas privadas do DAM.
* Conceda acesso de usuário da conta técnica às pastas do DAM.

## Verificando se a pasta do Assets recebeu a configuração correta {#configuration}

Geralmente, garantir que sua conta técnica tenha acesso aos ativos no DAM é suficiente para publicar seus ativos, juntamente com suas páginas, nos Edge Delivery Services.

A configuração adicional é necessária em dois casos adicionais, no entanto:

* Se desejar publicar páginas com ativos que não são de imagem, como PDF ou vídeos, no Edge Delivery Services.
* Se desejar publicar ativos de imagem em Edge Delivery Services independentemente das páginas.

Para dar suporte a ambos os casos de uso, uma [configuração](/help/implementing/developing/introduction/configurations.md) deve ser atribuída à pasta do DAM.

1. Faça logon no ambiente de criação do AEM.
1. Em **Sites**, selecione o site no qual você está publicando seus ativos ou o site ao qual os ativos serão associados.
1. Toque ou clique em **Propriedades** na barra de ferramentas.
1. Na guia **Avançado** da janela de propriedades, anote a configuração no campo **Configuração da nuvem**.
   * Isso é criado automaticamente quando você cria seu site no formato `/conf/<site-name>`.
1. Toque ou clique em **Cancelar** na janela de propriedades, navegue até **Assets** -> **Arquivos** e selecione sua pasta DAM.
1. Toque ou clique em **Propriedades** na barra de ferramentas.
1. Na guia **Cloud Service** da janela de propriedades, no campo **Configuração da Nuvem**, selecione a mesma configuração anotada anteriormente.
1. Toque ou clique em **Salvar e fechar**.
