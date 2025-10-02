---
title: Adicionar um site do Edge Delivery ao Cloud Manager
description: Saiba como adicionar um site do Edge Delivery ao seu programa de produção ou de sandbox.
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
exl-id: 17e842c9-599a-4877-9834-1e7220f508a8
source-git-commit: ddf2d80330ecfddad4af8a05c95cdba7f968a986
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 3%

---

# Adicionar um site do Edge Delivery ao Cloud Manager {#adding}

>[!IMPORTANT]
>
>Saiba por que você deve integrar seu site do Edge Delivery Services ao Cloud Manager.
>&#x200B;>Consulte [Vantagens de usar o caminho recomendado pela Adobe para o Edge Delivery Services](/help/implementing/cloud-manager/edge-delivery/introduction-to-edge-delivery-services.md#recommended-path-eds).

**Para adicionar um site do Edge Delivery ao Cloud Manager:**

1. Certifique-se de criar seu programa com uma licença do Edge Delivery Services antes de integrar um site do Edge Delivery no Cloud Manager.
Consulte [Criar um programa de produção](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md).
1. Entre no Cloud Manager em [experience.adobe.com](https://experience.adobe.com).
1. Na seção **Acesso rápido**, clique em **Experience Manager**.
1. No painel lateral esquerdo, clique em **Cloud Manager**.
1. Selecione a organização desejada.
1. No console **Meus Programas**, clique em um programa.
1. Siga uma das seguintes opções:

   * Na página **Visão geral do programa**, clique na guia **Edge Delivery**. Em seguida, próximo ao canto inferior direito da página, clique em **Adicionar site do Edge Delivery**.

     ![Adicionar site do Edge Delivery na guia Edge Delivery](/help/implementing/cloud-manager/assets/cm-eds-add1.png)

   * No canto superior esquerdo da página, clique em ![Mostrar ícone de menu](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) para exibir o menu do lado esquerdo.
No cabeçalho **Serviços**, clique em ![ícone da página da Web](https://spectrum.adobe.com/static/icons/workflow_18/Smock_WebPages_18_N.svg) **Edge Delivery Sites**.
Próximo ao canto superior direito da página, clique no ícone ![Link ou Adicionar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Link_18_N.svg) **Adicionar site do Edge Delivery**.

     ![Adicionar site do Edge Delivery pelo botão Sites do Edge Delivery](/help/implementing/cloud-manager/assets/cm-eds-add2.png)

1. Na caixa de diálogo **Adicionar site do Edge Delivery**, forneça as seguintes informações nos campos obrigatórios:

   | Campo de texto | Descrição |
   | - | --- |
   | Nome do site | Insira o nome do site do Edge Delivery que você está adicionando.<br>O nome serve como um identificador exclusivo para o site no Cloud Manager. |
   | Origem do Edge Delivery | Esse valor especifica o caminho do URL para a fonte de conteúdo do site no Edge Delivery Services. Ele também vincula o Cloud Manager ao seu site ativo.<br>A URL normalmente inclui a *ramificação*, o *projeto* e o *locatário*, como no exemplo a seguir (somente para fins de ilustração):<br>`https://main--{site}--{org}.aem.live` |
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
