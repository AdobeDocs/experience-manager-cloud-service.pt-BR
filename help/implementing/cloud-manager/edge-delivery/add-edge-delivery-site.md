---
title: Adicionar um site do Edge Delivery ao Cloud Manager
description: Saiba como adicionar um site do Edge Delivery ao seu programa de produção ou de sandbox.
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: c952e69aa637b30abec4deba0e643b4287d84330
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 2%

---


# Adicionar um site do Edge Delivery ao Cloud Manager {#adding}

Você pode adicionar um site do Edge Delivery ao seu programa de produção ou de sandbox.

É necessário adicionar um site do Edge Delivery ao Cloud Manager para [registrar um tíquete de suporte para o seu projeto do Edge Delivery](/help/edge/overview.md##support-ticket).

Consulte também [Introdução a Edge Delivery Services no Cloud Manager](/help/implementing/cloud-manager/edge-delivery/introduction-to-edge-delivery-services.md).

**Para adicionar um site do Edge Delivery ao Cloud Manager:**

1. Faça logon no Cloud Manager em [`https://my.cloudmanager.adobe.com`](https://my.cloudmanager.adobe.com/) e selecione o programa apropriado.
1. Siga uma das seguintes opções:

   * Na página **Visão geral do programa**, clique na guia **Edge Delivery**. Em seguida, próximo ao canto inferior direito da página, clique em **Adicionar site do Edge Delivery**.

     ![Adicionar site do Edge Delivery na guia Edge Delivery](/help/implementing/cloud-manager/assets/cm-eds-add1.png)

   * No canto superior esquerdo da página, clique no ícone de hambúrguer para exibir o menu de navegação esquerdo. No cabeçalho **Serviços**, clique em **Sites do Edge Delivery**. Próximo ao canto superior direito da página, clique em **Adicionar site**.

     ![Adicionar site do Edge Delivery pelo botão Sites do Edge Delivery](/help/implementing/cloud-manager/assets/cm-eds-add2.png)

1. Na caixa de diálogo **Adicionar site do Edge Delivery**, forneça as seguintes informações nos campos obrigatórios:

   | Campo de texto | Dados a fornecer |
   | --- | --- |
   | Nome do site | Insira o nome do site do Edge Delivery que você está adicionando. O nome serve como um identificador exclusivo do site no Cloud Manager. |
   | URL do repositório | Esse campo se refere ao repositório Git onde o código do site está armazenado. Esse campo permite que o Cloud Manager extraia o código desse repositório durante o processo de implantação. |
   | Descrição do site (opcional) | Insira uma breve descrição do site do Edge Delivery que você está adicionando. Esta descrição ajuda a identificar e diferenciar o site, facilitando o gerenciamento e o reconhecimento entre outros sites adicionados. |

1. No canto inferior direito da caixa de diálogo, clique em **Adicionar**.

1. A caixa de diálogo **Verificar propriedade do repositório** é aberta. Com ele aberto, execute as seguintes etapas:

   1. Adicione um arquivo com o caminho e o nome `well-known/adobe/cloudmanager-challenge.txt` à ramificação `main` do repositório Git listado no campo **URL do Repositório**.
      * Se necessário, clique no ícone **Copiar** para copiar o caminho para a área de transferência.
      * *não* adicione um ponto no início do caminho do local.
   1. Adicione o código do campo **Step &amp;num; 1** ao arquivo criado na etapa anterior.
      * Se necessário, clique no ícone **Copiar** para copiar o código para a área de transferência.
   1. No repositório Git, crie uma solicitação de pull para as alterações recém-criadas e mescle-a com `main`.

1. Clique em **Verificar**.

Depois que o repositório é verificado, seu status na tabela Sites de delivery do Edge muda para um círculo verde com uma marca de seleção branca dentro dele.
