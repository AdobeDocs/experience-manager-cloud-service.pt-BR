---
title: Criar um site do Edge Delivery no Cloud Manager com um clique
description: Saiba como criar rapidamente um site do Edge Delivery no Cloud Manager com apenas um clique.
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 8034fc8454fca41c2430fa1179f80d2d2ab80563
workflow-type: tm+mt
source-wordcount: '657'
ht-degree: 0%

---


# Sobre Criar um site do Edge Delivery no Cloud Manager com um clique {#about-one-click-edge-delivery-site}

O One Click Edge Delivery Service (EDS) foi projetado para automatizar a integração e a implantação de sites do Edge Delivery no Cloud Manager. Ele simplifica bastante o processo, fazendo você clicar em um único botão. Esse clique único provisiona a infraestrutura necessária, integra-se ao GitHub para controle de versão e configura o armazenamento de documentos e ativos no Google Drive.

Essa automação ajuda a reduzir o esforço manual necessário para configurar o site inicial. Ele garante fluxos de trabalho perfeitos, escalabilidade e melhora o desempenho de suas equipes quando se trata de gerenciar conteúdo na borda.

## Principais conceitos {#key-concepts}

Principais conceitos ao usar um clique para criar um site do Edge Delivery.

| Conceito principal | Descrição |
| --- | --- |
| Implantação automatizada do Edge | <ul><li>Os usuários podem criar e configurar sites do Edge Delivery instantaneamente.</li><li>Ele reduz ou elimina a necessidade de processos manuais de integração usando a integração da Cloud Manager com o fluxo de trabalho de CI/CD.</li><li>Integrado ao Cloud Manager para fluxos de trabalho de CI/CD ininterruptos.</li></ul> |
| Integração com o Cloud Manager | <ul><li>Usa a interface do usuário do Cloud Manager para acionar o processo Edge Delivery com um clique.</li><li>Fornece acesso à criação e implantação automatizadas do repositório.</li></ul> |
| Controle de versão baseado no GitHub | <ul><li>Cria um repositório GitHub em uma organização usando modelos padronizados predefinidos para padronizar implantações.</li><li>Links com AEM Bot para atualizações de conteúdo.</li></ul> |
| Integração de armazenamento de documentos e ativos | <ul><li>Gera uma pasta do Google Drive para armazenamento.<li>Instala o aplicativo de sincronização de código do AEM no repositório, garantindo sincronização e implantação ininterruptas.</li></li><li>Permite que vários colaboradores gerenciem documentos facilmente.</li></ul> |
| Segurança e escalabilidade | <ul><li>Garante a conformidade com os padrões de segurança corporativa.</li><li>O é compatível com vários sites do Edge Delivery em diferentes locatários da Cloud Manager.</li></ul> |



## Crie um site do Edge Delivery no Cloud Manager com um clique {#one-click-edge-delivery-site}

Para criar um site do Adobe Edge Delivery com um clique, sua organização deve ter uma licença da Edge Delivery Services disponível. Esta licença faz parte do Adobe Experience Manager (AEM) e é necessária para criar o Edge Delivery Services no Cloud Manager.

Em termos de permissões, você deve ser membro da função Proprietário da empresa ou ter recebido as permissões apropriadas para adicionar ou editar programas no Cloud Manager. Esse nível de acesso permite gerenciar a integração do Edge Delivery Services em seus programas.

Consulte também [Introdução ao Edge Delivery Services no Cloud Manager](/help/implementing/cloud-manager/edge-delivery/introduction-to-edge-delivery-services.md).

AS CONFIGURAÇÕES ADEQUADAS DE BOT DO AEM DEVEM ESTAR EM VIGOR PRIMEIRO PARA ATUALIZAÇÕES AUTOMÁTICAS DE CONTEÚDO? VERDADEIRO? FALSO?

**Para criar um site do Edge Delivery no Cloud Manager com um clique:**

1. Faça logon no Cloud Manager em [`https://my.cloudmanager.adobe.com`](https://my.cloudmanager.adobe.com/) e selecione o programa apropriado.
1. No canto superior esquerdo da página, clique em ![Mostrar ícone de menu](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) para exibir o menu do lado esquerdo.
1. No menu do lado esquerdo, no cabeçalho **Serviços**, clique em ![ícone da página da Web](https://spectrum.adobe.com/static/icons/workflow_18/Smock_WebPages_18_N.svg) **Edge Delivery Sites**.
1. Na página Edge Delivery, na caixa de diálogo **Lista de tarefas do Edge Delivery**, na caixa de grupo **Prerequisitos completos**, clique em **Provisionar**.
1. Na caixa de diálogo **Provisionar site do Edge Delivery**, no campo de texto **Nome do projeto**, digite o nome do site e clique em **Provisionar**.
Uma janela aparece perto do centro superior da tela informando que o provisionamento do site do Edge Delivery foi iniciado.
Quando o provisionamento estiver concluído e o site for validado, o nome do site aparecerá na área **Sites do Edge Delivery** na página do Edge Delivery.

### Explorar um site do Edge Delivery recém-criado


1. Clique no link Repositório Git à direita do nome do site.

Publicar.

Clique em Nome do site,

faça algumas alterações e publique

Visualizar página em Visualização, em seguida, alterar URL para visualizar versão ao vivo.

Adicionar colaboradores.


## Pré-visualize um site do Edge Delivery com um clique

## Publicar um site do Edge Delivery com um clique





## Adicione colaboradores a um site do Edge Delivery com um clique


































Esses aprimoramentos têm como objetivo melhorar a automação, simplificar os processos de configuração e aprimorar a colaboração para os usuários do Edge Delivery Services. <!-- CMGR-59362 -->

![Crie um site do Edge Delivery com um clique](/help/implementing/cloud-manager/release-notes/assets/eds-one-click-60.png)

![Caixa de diálogo Provisionar site do Edge Delivery](/help/implementing/cloud-manager/release-notes/assets/eds-provision-60.png)