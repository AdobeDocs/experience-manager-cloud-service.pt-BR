---
title: Adicionar um site do Edge Delivery ao Cloud Manager
description: Saiba como adicionar um site do Edge Delivery ao seu programa de produção ou de sandbox.
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: b222b4384b1c2a21ecbb244d149ce7e51cc7990f
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 2%

---


## Adicionar um site do Edge Delivery ao Cloud Manager {#eds-add-site}

Depois de adicionar Edge Delivery Services a um programa de produção, sua licença de Edge Delivery Services é aplicada a ele.

Uma guia clicável chamada **Edge Delivery** é exibida na página Visão geral. Clicar na guia exibe uma tabela que lista cada site do Edge Delivery adicionado. No painel de navegação esquerdo, no agrupamento **Serviços**, observe a opção de menu denominada **Edge Delivery Sites**.

![Página de visão geral mostrando o Edge Delivery Sites no painel de navegação esquerdo e a guia Edge Delivery à direita da guia Entrega do Publish](/help/implementing/cloud-manager/assets/cm-overview-eds.png)

**Para adicionar um site do Edge Delivery ao Cloud Manager:**

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione o programa apropriado.
1. No console **[Meus Programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, selecione o programa com o Edge Delivery Services configurado, ao qual você deseja adicionar um site do Edge Delivery.
1. Siga um destes procedimentos:
   * Na página **Visão geral do programa**, clique na guia **Edge Delivery**. Em seguida, próximo ao canto inferior direito da página, clique em **Adicionar site do Edge Delivery**.

     ![Adicionar site do Edge Delivery na guia Edge Delivery](/help/implementing/cloud-manager/assets/cm-eds-add1.png)

     A **lista de tarefas do Edge Delivery**, como vista na imagem acima, é um guia opcional de lista de verificação de integração destinado a ajudá-lo a começar a usar o Edge Delivery. Consulte [Sobre a lista de tarefas do Edge Delivery](#ed-todo-list).

   * No canto superior esquerdo da página, clique no ícone de hambúrguer para exibir o menu de navegação esquerdo. No cabeçalho **Serviços**, clique em **Sites do Edge Delivery**. Próximo ao canto superior direito da página, clique em **Adicionar site**.

     ![Adicionar site do Edge Delivery pelo botão Sites do Edge Delivery](/help/implementing/cloud-manager/assets/cm-eds-add2.png)

1. Na caixa de diálogo **Adicionar site do Edge Delivery**, faça o seguinte:

   | Campo de texto | O que fazer |
   | --- | --- |
   | Nome do site | Insira o nome do site do Edge Delivery que você está adicionando. O nome serve como um identificador exclusivo do site no Cloud Manager. |
   | URL do repositório | Esse campo se refere ao repositório Git onde o código do site está armazenado.<br>Insira a URL do repositório Git que contém os arquivos e recursos necessários (como HTML, CSS, JavaScript e outros ativos da Web) para o site do Edge Delivery. Essa organização permite que o Cloud Manager extraia o código desse repositório durante o processo de implantação. |
   | Descrição do site (opcional) | Insira uma breve descrição do site do Edge Delivery que você está adicionando.<br>Esta descrição ajuda a identificar e diferenciar o site, facilitando o gerenciamento e o reconhecimento entre outros sites adicionados. Você pode querer incluir detalhes sobre a finalidade, o conteúdo ou qualquer outra informação relevante do site que possa ajudar a esclarecer sua função ou escopo. |

1. No canto inferior direito da caixa de diálogo, clique em **Adicionar**.

1. Na caixa de diálogo **Verificar propriedade do repositório**, siga um destes procedimentos:

   | Etapa | Descrição |
   | --- | --- |
   | 1 | Adicione um arquivo com o caminho do local à ramificação `main` do repositório Git listado no campo **URL do Repositório**. Se necessário, clique no ícone Copiar para copiar o caminho para a área de transferência.<br> O caminho do local é:<br>`well-known/adobe/cloudmanager-challenge.txt`.<br><br>Fazer *não* adicionar um ponto no início do caminho do local, está em:<br>`.well-known/adobe/cloudmanager-challenge.txt` |
   | 2 | Adicione o código gerado ao arquivo criado na Etapa 1. Se necessário, clique no ícone Copiar para copiar o código para a área de transferência. |
   | 3 | No repositório Git, crie uma solicitação de pull e, em seguida, mescle-a para confirmar o código. |

1. Clique em **Verificar**. Depois que o repositório é verificado, seu status na tabela Sites de delivery do Edge muda para um círculo verde com uma marca de seleção branca dentro dele.
