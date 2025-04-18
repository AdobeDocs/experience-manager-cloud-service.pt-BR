---
title: Adicionar um site do Edge Delivery ao Cloud Manager
description: Saiba como adicionar um site do Edge Delivery ao seu programa de produção ou de sandbox.
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
exl-id: 17e842c9-599a-4877-9834-1e7220f508a8
source-git-commit: a078d45f81fc7081012ebf24fa8f46dc1a218cd7
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 3%

---

# Adicionar um site do Edge Delivery ao Cloud Manager {#adding}

Depois de adicionar um site do Edge Delivery ao programa de produção, sua licença do Edge Delivery Services é aplicada a ele.

É necessário adicionar um site do Edge Delivery ao Cloud Manager para [registrar um tíquete de suporte para o seu projeto do Edge Delivery](/help/edge/overview.md##support-ticket).

Consulte também [Introdução a Edge Delivery Services no Cloud Manager](/help/implementing/cloud-manager/edge-delivery/introduction-to-edge-delivery-services.md).

**Para adicionar um site do Edge Delivery ao Cloud Manager:**

1. Faça logon no Cloud Manager em [`https://my.cloudmanager.adobe.com`](https://my.cloudmanager.adobe.com/) e selecione o programa apropriado.
1. Siga uma das seguintes opções:

   * Na página **Visão geral do programa**, clique na guia **Edge Delivery**. Em seguida, próximo ao canto inferior direito da página, clique em **Adicionar site do Edge Delivery**.

     ![Adicionar site do Edge Delivery na guia Edge Delivery](/help/implementing/cloud-manager/assets/cm-eds-add1.png)

   * No canto superior esquerdo da página, clique em ![Mostrar ícone de menu](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) para exibir o menu do lado esquerdo.
No cabeçalho **Serviços**, clique em ![ícone da página da Web](https://spectrum.adobe.com/static/icons/workflow_18/Smock_WebPages_18_N.svg) **Edge Delivery Sites**.
Próximo ao canto superior direito da página, clique em **Adicionar site**.

     ![Adicionar site do Edge Delivery pelo botão Sites do Edge Delivery](/help/implementing/cloud-manager/assets/cm-eds-add2.png)

1. Na caixa de diálogo **Adicionar site do Edge Delivery**, forneça as seguintes informações nos campos obrigatórios:

   | Campo de texto | Descrição |
   | - | --- |
   | Nome do site | Insira o nome do site do Edge Delivery que você está adicionando.<br>O nome serve como um identificador exclusivo para o site no Cloud Manager. |
   | URL do repositório | Insira o repositório Git onde o código do site está armazenado.<br>Este campo permite que o Cloud Manager extraia o código desse repositório durante o processo de implantação. |
   | Descrição do site (opcional) | Insira uma breve descrição do site do Edge Delivery que você está adicionando.<br>Uma descrição ajuda a identificar e diferenciar o site, facilitando o gerenciamento e o reconhecimento entre outros sites adicionados. |

1. No canto inferior direito da caixa de diálogo, clique em **Adicionar**.

1. Na caixa de diálogo **Verificar propriedade do repositório**, verifique a propriedade do repositório executando as seguintes etapas:

   | Número da etapa | Descrição |
   | - | - |
   | **1** | Adicione um arquivo com o caminho e o nome `well-known/adobe/cloudmanager-challenge.txt` à ramificação `main` do repositório Git listado no campo **URL do Repositório**. *não* adicione um ponto no início do caminho do local.<br>Se necessário, clique em ![Copiar ícone](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg) para copiar o caminho para a área de transferência. |
   | **2** | Adicione o código visto no campo de texto na Etapa 2 ao arquivo que você acabou de criar na Etapa 1.<br>Se necessário, clique em ![Copiar ícone](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg) para copiar o código para a área de transferência. |
   | **3** | Crie uma solicitação de pull no repositório Git para as alterações recém-criadas e mescle-a com `main` para confirmar o código. |

1. Clique em **Verificar**.

Quando o repositório é verificado, seu status na tabela de sites do Edge Delivery é atualizado. Um círculo verde com uma marca de seleção branca indica o status.

Na mesma tabela, clique em ![Informações sobre o ícone do site do Edge Delivery](https://spectrum.adobe.com/static/icons/workflow_18/Smock_InfoOutline_18_N.svg) para exibir detalhes do site. Essas informações incluem o URL do repositório verificado, juntamente com os URLs do site de Pré-visualização e Produção.
