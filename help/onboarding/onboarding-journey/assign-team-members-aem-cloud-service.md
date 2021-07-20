---
title: 'Atribuindo membros da equipe ao AEM como perfis de produto do Cloud Service '
description: Siga esta página para saber como atribuir membros da equipe ao AEM como perfis de produto do Cloud Service
hide: true
hidefromtoc: true
index: false
source-git-commit: 8b30fc9494e152aa742cf17c02f982f5c9479473
workflow-type: tm+mt
source-wordcount: '678'
ht-degree: 2%

---


# Atribuir ao AEM como perfis de produto do Cloud Service {#assign-team-members-cloud-service}

## Objetivo {#objective}

Este documento ajuda você a entender as etapas que o administrador do sistema deve tomar para atribuir os membros da equipe ao AEM como perfis de produto do Cloud Service e por que é crucial permitir que os autores do AEM iniciem sua jornada com o AEM.

Após ler esta seção, você deve:

* Entenda por que e como os membros da equipe são atribuídos ao AEM como perfis de produto do Cloud Service
* Saiba como adicionar membros da equipe AEM perfil de produto do usuário
* Saiba como adicionar membros da equipe ao perfil de produto Administradores AEM


## Introdução {#introduction}

Para receber acesso ao AEM como Cloud Service, os usuários devem pertencer a um dos dois perfis de produto, &quot;AEM usuários&quot; ou &quot;AEM administradores&quot;. Os membros da equipe devem receber permissões para a instância do AEM, pois as permissões para administrar o Cloud Manager não serão suficientes. Saiba mais.

>[!NOTE]
>Todos os usuários atribuídos a AEM perfil de produto do Usuário pelo administrador do sistema terão (somente leitura) acesso ao Cloud Manager.

## Pré-requisitos {#prerequisites}

* Entender AEM como perfis de produto Cloud Service
* Familiarize-se com o Admin Console
* Os perfis de produto do Cloud Manager foram atribuídos aos membros de sua equipe, conforme apropriado, e os recursos de nuvem foram configurados
* Detalhes sobre o membro da equipe: O administrador do sistema deve ter os nomes e endereços de email e as funções e responsabilidades dos membros da equipe que precisarão acessar o AEM como Cloud Service. Para fins de integração, recomendamos que você adicione inicialmente usuários que participarão das tarefas imediatas, como administradores, desenvolvedores e autores de conteúdo. Você pode continuar o resto da integração sem adicionar todos os usuários. Depois de concluir a integração, você pode dimensionar para um número maior de usuários posteriormente.


1. Faça logon no Admin Console
(Igual a antes)

1. Revisar AEM como perfis de produto do Cloud Service
No Admin Console, é possível ver a lista de Perfis do Cloud Manager. Para fazer isso:

1. Depois de fazer logon no Adobe Admin Console, selecione Adobe Experience Manager as a Cloud Service no cartão Produtos e serviços :

1. Navegue e selecione a instância (Instância do autor do ambiente de desenvolvimento), conforme mostrado na figura abaixo.



   Agora é possível ver a lista de AEM como um perfil de produto do Cloud Service que será necessário atribuir a um usuário com base em sua função. Para saber mais sobre isso, acesse AEM as a Cloud Service Product Profiles.




## Adicionar membros da equipe ao Perfil de Produto AEM Usuário ou Administrador AEM {#add-team-members}

Para receber acesso à instância do AEMaaCS, os usuários devem pertencer a um dos dois perfis de produto &quot;AEM usuários&quot; ou &quot;AEM administradores&quot;.

>[!NOTE]
>Você deve receber permissões para a instância. As permissões para administrar o Cloud Manager não serão suficientes. Saiba mais.

As etapas abaixo devem ser seguidas pelo administrador do sistema que também está na função de Proprietário comercial.

1. No Cloud Manager, navegue até o Cloud Manager e selecione o botão Gerenciar acesso no contexto do ambiente de interesse, conforme mostrado abaixo:

1. Depois de clicar em Gerenciar acesso, uma nova GUIA navega até o Admin Console, de onde você tem acesso à instância do autor do ambiente. Selecione &quot;Administradores AEM&quot; ou &quot;Usuários AEM&quot; com base nas permissões que esse indivíduo precisa dar. Saiba mais sobre o AEM as a Cloud Service product profiles.

1. Selecione Adicionar usuário como mostrado abaixo e envie os detalhes necessários para concluir a adição do membro da equipe:


1. Você desejará repetir essas etapas para todos os ambientes, incluindo Desenvolvimento, Estágio e Produção, se tiver as informações dos membros da equipe que precisam de acesso disponíveis.

   O usuário adicionado agora terá acesso ao AEM como um Cloud Service Author services!


## O que vem a seguir {#whats-next}

Os usuários atribuídos aos perfis de produto do AEMaaCS agora estão prontos para aprender como acessar o Author e se familiarizar com a criação de páginas no AEM as a Cloud Service. Saiba mais.

## Recursos adicionais {#additional-resources}

Configuração do acesso ao AEM (Passagem do vídeo)
Guia de início rápido para a criação de páginas
