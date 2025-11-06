---
title: Configurar um site do Edge Delivery para usar um repositório Git externo
description: Saiba como vincular um site do Edge Delivery a um repositório Git privado ou corporativo.
feature: Cloud Manager, Developing
role: Admin, Developer
exl-id: 1dbaef34-efa3-4287-b7b1-f60db938146d
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 1%

---

# Configurar um site do Edge Delivery para usar um repositório Git externo

Você pode configurar seu site do Edge Delivery para obter o código de qualquer repositório Git privado já integrado no Cloud Manager.

**Fornecedores do Git com Suporte**

| Nível de suporte | Fornecedores | Notas |
| --- | --- | --- |
| Disponibilidade geral | · GitHub Enterprise (versão auto-hospedada)<br>· Bitbucket (versão em nuvem)<br>· GitLab (versão em nuvem e auto-hospedada) | Conectar sem solicitações de ativação |
| Programa Alpha | Azure DevOps (versão para nuvem) | [Solicitar acesso](mailto:grp-cloudmanager_byog@adobe.com) |
| Programa Beta | Repositório hospedado pela Adobe (criado no Cloud Manager) | [Solicitar acesso](mailto:grp-cloudmanager_byog@adobe.com) |

**Para configurar um site do Edge Delivery para usar um repositório Git externo:**

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione o programa apropriado.
1. No console **[Meus programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, selecione o programa com o Edge Delivery Services configurado, no qual você deseja configurar um site do Edge Delivery para usar um repositório Git externo.
1. No painel à esquerda, no cabeçalho **Programa**, clique em **![Ícone de visão geral](/help/implementing/cloud-manager/edge-delivery/assets/overview.svg) Visão geral**.
1. Na página **Visão Geral do Programa**, clique na guia **Edge Delivery**.
1. Na tabela **Sites da Edge Delivery**, clique em ![Ícone de mais](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) no final de uma linha cujo site você deseja configurar para usar um repositório externo e clique em **Trazer seu próprio Git**.
1. Na caixa de diálogo Traga seu próprio Git, na lista suspensa **Nome do Repositório**, escolha um repositório Git com o status `READY` e clique em **Confirmar**.

   O Cloud Manager retorna um token secreto único. Se você reconfigurar o site, o Cloud Manager gerará um novo token secreto.

1. Copie o token e adicione-o à configuração do site em **helix-admin**, conforme descrito no [Guia do Git BYO](https://www.aem.live/developer/byo-git).
1. De volta ao Cloud Manager, clique em ![Mais ícone](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) no final de uma linha cujo site você acabou de configurar para usar um repositório externo e clique em **Sincronizar código**.
1. Escolha a ramificação a ser sincronizada e clique em **Sincronizar**.

Cada confirmação em qualquer ramificação agora aciona uma sincronização automática. Use **Sincronizar código** novamente sempre que uma sincronização manual completa for necessária.
