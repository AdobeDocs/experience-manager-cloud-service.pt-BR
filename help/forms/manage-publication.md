---
title: Como publicar ou desfazer a publicação de formulários em instâncias de pré-visualização ou publicação?
description: Saiba como publicar ou desfazer a publicação de formulários do ambiente do autor do AEM para visualizar ou publicar instâncias. Se você estiver testando seus formulários em um ambiente de preparo ou implantando-os em tempo real para usuários finais, o AEM fornece ferramentas simplificadas para gerenciar esse processo com eficiência.
Keywords: 6.5 forms to cloud service, 6.5 forms to cs, manage publication, , AEM Forms 6.5 to Cloud Service, AEM form migration to cloud service, Forms Manage publication, AF Manage publication, Adaptive Forms Manage publication, Cloud Manage publication
contentOwner: khsingh
feature: Adaptive Forms
feature-set: Experience Manager Assets,Experience Manager Sites,Experience Manager, Experience Manager Forms, Experience Manager Cloud Manager
role: User, Developer
level: Intermediate
source-git-commit: 242dcbc5bb541dfac601454fb75dec3bdff1ea64
workflow-type: tm+mt
source-wordcount: '834'
ht-degree: 0%

---


# &#x200B;Gerenciar publicação no Experience Manager Forms

Como administrador do Adobe Experience Manager Forms, você pode publicar formulários da instância do autor no Experience Manager Forms. Você pode agendar a publicação de um formulário ou pasta em uma data ou hora posterior. Após a publicação, os usuários podem acessar e preencher os formulários.

É possível publicar ou cancelar a publicação do formulário usando a opção Publish ou Gerenciar publicação disponível na interface do Experience Manager Forms. Se fizer modificações subsequentes nos formulários ou pastas originais no Experience Manager Forms, as alterações não serão refletidas na instância de publicação até que publique novamente pelo Experience Manager Forms. Isso garante que as alterações de trabalho em andamento não estejam disponíveis na instância de publicação. Somente as alterações publicadas por um administrador estão disponíveis na instância de publicação.

## Formulários Publish usando a opção Publish

A opção de publicação permite publicar um formulário imediatamente. No console Experience Manager Forms, navegue até a pasta principal e selecione um formulário que deseja publicar. Clique na opção Publish na barra de ferramentas, veja todos os ativos de referência que seriam publicados com o formulário e clique em Publish.

Uma captura de tela de um computador

Descrição gerada automaticamente

## Publish ou Cancelar publicação de formulários usando Gerenciar publicação


Gerenciar publicação permite publicar ou desfazer a publicação de conteúdo de e para o destino selecionado, adicionar conteúdo à lista de publicação em toda a pasta de formulários e documentos, selecionar referências para publicar e agendar publicações para uma data ou hora posterior.


No console Experience Manager Forms, navegue até a pasta principal e selecione um formulário que deseja publicar. Clique na opção Gerenciar publicação na barra de ferramentas.


Uma captura de tela de um computador

Descrição gerada automaticamente



As seguintes opções estão disponíveis na interface Gerenciar publicação:

* Ações

   * Publish: formulários do Publish para o destino selecionado
   * Cancelar publicação: cancelar a publicação de formulários do destino

* Destino

   * Publish: o Publish se forma à instância do Publish do Experience Manager Forms (AEM).
   * Visualização: formulários do Publish para a instância de visualização do Experience Manager Forms (AEM).

* Programação

   * Agora: formulários do Publish imediatamente
   * Posteriormente: formulários do Publish com base na data ou hora de Ativação



Para continuar, clique em **Avançar**. Na guia Scope, use as opções Add Content para adicionar mais conteúdo para publicação. Por exemplo, você pode adicionar mais arquivos Forms ou Documento de registro.

### Adicionar conteúdo

A publicação no Experience Manager Forms permite adicionar mais conteúdo (formulários, ativos e pastas) à lista de publicação. Você pode adicionar mais formulários, ativos ou pastas à lista da pasta formulários e documentos. Mas não é possível adicionar ativos de várias pastas de uma vez.

Uma captura de tela de um computador

Descrição gerada automaticamente

Clique no botão **Adicionar Conteúdo** para adicionar mais conteúdo. É possível adicionar vários ativos de uma pasta ou adicionar várias pastas de uma vez. Mas não é possível adicionar ativos de várias pastas de uma vez.

Para configurar as referências para publicar ou não publicar para um formulário ou outros ativos, selecione o formulário ou o ativo e clique em Referências publicadas.

Uma captura de tela de um computador

Descrição gerada automaticamente

Na caixa de diálogo Referências publicadas, desmarque os ativos que planeja não publicar novamente e clique em Concluído.


Uma captura de tela de um computador

Descrição gerada automaticamente


## Publish ou cancele a publicação de um formulário mais tarde


Além de permitir a publicação ou o cancelamento da publicação de formulários em uma data e hora posteriores, a opção publicar ou desfazer a publicação mais tarde também permite configurar um fluxo de trabalho. Os formulários são publicados ou não, após a conclusão do fluxo de trabalho. Para agendar um formulário para publicação ou cancelamento da publicação:

1. No console Experience Manager Forms, navegue até a pasta principal e selecione o formulário que deseja agendar a publicação.
1. Clique na opção Gerenciar publicação na barra de ferramentas.
1. Clique em Publish ou em Cancelar publicação da ação e selecione o Destino no qual deseja publicar ou cancelar a publicação do conteúdo.

   * Visualização: use a opção de Visualização para publicar ou desfazer a publicação em um ambiente de visualização do Experience Manager Forms. Os ambientes de visualização do Experience Manager Forms são usados para testar em formulários de desenvolvimento.
   * Publish: use a opção Experience Manager Forms Publish para enviar o formulário ao ambiente de publicação do Experience Manager Forms depois que ele estiver pronto para uso em um ambiente de produção.


1. Selecione Mais tarde em Agendamento.

1. Selecione uma Data de ativação e especifique a data e a hora. Clique em Avançar.

   Uma captura de tela de um computador

   Descrição gerada automaticamente

1. Na guia Scope, Adicionar conteúdo (se necessário). Clique em Avançar.

   Uma captura de tela de um computador

   Descrição gerada automaticamente

1, (Opcional) Na guia Workflows, especifique um título de Workflow. Clique em Publish mais tarde.

Uma captura de tela de um computador

Descrição gerada automaticamente

## Determinação do status de publicação

Há várias maneiras de determinar o status de publicação:

* Faça logon na instância de destino para verificar os formulários publicados e outros ativos (dependendo da data ou hora agendada).

* Use a exibição de linha do tempo para determinar o status da publicação.

* Use o menu de informações da página no editor Forms adaptável.