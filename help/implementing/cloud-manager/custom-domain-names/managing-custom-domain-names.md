---
title: Gerenciar nomes de domínio personalizados
description: Saiba como usar o Cloud Manager para exibir, atualizar, substituir e excluir nomes de domínio personalizados.
exl-id: 6cab8cf2-22c0-4f4b-9c54-a1425e74ddd0
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 8e2fc0d4ee82e79d1a822a528b1a46acce3c192a
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 32%

---


# Gerenciar nomes de domínio personalizados {#managing-custom-domain-names}

O Cloud Manager permite editar, atualizar, substituir e excluir nomes de domínio personalizados.

## Editar uma configuração personalizada de nome de domínio {#view-and-update}

No Adobe Cloud Manager, talvez você queira editar uma configuração de nome de domínio personalizado pelos seguintes motivos:

* **Alternar ambientes**: para aplicar a configuração correta, dependendo se você está disponibilizando conteúdo para usuários finais (Publish) ou usuários internos (Autor).
* **Atualizações de segurança**: para atualizar para um certificado SSL mais recente para fins de segurança avançada ou conformidade.
* **Alterando estratégia de implantação**: para garantir que o certificado SSL correto seja aplicado a um ambiente específico para criptografia e acesso ao site adequados.

**Para editar uma configuração personalizada de nome de domínio:**

1. Faça logon no Cloud Manager, em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/), e selecione a organização apropriada.

1. No console **[Meus Programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, selecione o programa.

1. No canto superior esquerdo da página, clique no ícone de hambúrguer para exibir o menu de navegação esquerdo.
1. No cabeçalho **Serviços**, clique em **Configurações de CDN**.
1. Na página **Configurações de CDN**, clique nas reticências ao final de uma linha cujo CDN você deseja editar.
1. Clique em **Editar**.
1. Na caixa de diálogo **Editar configuração da CDN**, faça o seguinte:
   * Na lista suspensa **Camada**, selecione a camada (Autor ou Publish) que deseja usar.
   * Na lista suspensa **Certificado SSL**, selecione o certificado SSL que deseja usar.
1. Clique em **Atualizar**.


## Atualizar um certificado SSL de nome de domínio personalizado {#update-cert}

Você pode seguir [as mesmas etapas para exibir e atualizar um nome de domínio personalizado](#view-and-update) para atualizar um certificado SSL.

>[!NOTE]
>
>O certificado SSL deve ser válido, [já configurado](/help/implementing/cloud-manager/managing-ssl-certifications/introduction-to-ssl-certificates.md), e conter o nome de domínio personalizado que você está atualizando.


## Excluir um nome de domínio personalizado {#deleting}

Um usuário com a função de **Proprietário da empresa** ou **Gerente de implantação** pode usar o Cloud Manager para excluir um nome de domínio personalizado.

### Excluir um nome de domínio personalizado de todos os ambientes associados {#delete-cdn-all}

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriados.

1. Navegue até a página **Configurações de Domínio** a partir da tela **Visão Geral**.

1. Identifique a linha do nome de domínio personalizado que deseja excluir.

1. Clique no botão de reticências localizado na extremidade direita da linha.

1. Selecione **Excluir**.

1. Confirme seu envio.


### Excluir um nome de domínio personalizado de um ambiente específico {#delete-cdn-specific}

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriado.
1. Acesse a tela **Ambientes** a partir da página **Visão geral**.
1. Na página **Ambientes**, navegue até uma tela de detalhes do ambiente de interesse.
1. Na tabela de nomes de domínio, identifique a linha do nome de domínio personalizado que deseja excluir.
1. Clique no botão de reticências localizado na extremidade direita da linha.
1. Selecione **Excluir**.
1. Confirme seu envio.
