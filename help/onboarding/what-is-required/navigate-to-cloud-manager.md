---
title: Navegar para o Cloud Manager
description: Siga esta página para saber como navegar até a página de aterrissagem do Cloud Manager
exl-id: 9cf25d1d-a351-4ea0-b2e9-1df6ca4915b7
source-git-commit: e7f8e7daa88c5bf8bb13c2a635fb84724f8bd7bb
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 6%

---

# Navegar para o Cloud Manager {#cloud-manager}

O Cloud Manager é uma parte importante do AEM as a Cloud Service. Ela permite que as organizações autogerenciem o Experience Manager na nuvem. Inclui uma estrutura de integração contínua e entrega contínua (CI/CD) que permite que as equipes de TI e os parceiros de implementação acelerem a entrega de personalizações ou atualizações, sem comprometer o desempenho ou a segurança. Usando a interface do usuário, você pode configurar e iniciar o pipeline de CI/CD.

Assim que o Administrador do sistema conceder acesso ao Cloud Manager, você receberá um email que o levará para a página inicial do [Adobe Experience Cloud](https://experience.adobe.com).

>[!NOTE]
>Você deve ser adicionado como um usuário e deve ser atribuído pelo menos a uma Função do Cloud Manager (Perfil do produto no Admin Console) pelo Administrador do sistema.

1. No email de boas-vindas, clique em **Introdução**, conforme mostrado na figura abaixo.
   ![](/help/onboarding/what-is-required/assets/get-started-email.png)

   >[!NOTE]
   >Como alternativa, você também pode navegar diretamente para a página de logon do Cloud Manager de [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/). Dependendo das funções atribuídas no [!UICONTROL Cloud Manager] e do estado do aplicativo, você verá telas diferentes ao usar a interface do [!UICONTROL Cloud Manager]. Consulte a seção abaixo, [Página de aterrissagem do Cloud Manager](#cloud-manager-landing) para obter mais detalhes.

1. Selecione **Experience Manager**.
   ![](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/landing-page1.png)

1. Clique em **Iniciar** no cartão do Cloud Manager. Depois de fazer logon no [!UICONTROL Cloud Manager] com êxito, você estará pronto para usar a interface do usuário (UI).
   ![](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/landing-page2.png)


## Página de aterrissagem do Cloud Manager {#cloud-manager-landing}

Após o logon bem-sucedido, você será direcionado para a página inicial do Cloud Manager.

>[!NOTE]
>Dependendo das funções atribuídas no [!UICONTROL Cloud Manager] e do estado do aplicativo, você verá telas diferentes ao usar a interface do [!UICONTROL Cloud Manager].

Você verá uma das três opções, descritas abaixo:

* **Quando nenhum programa existe no Cloud Manager**

   Se não houver programas em sua organização, a landing page direcionará você para criar seu primeiro programa, como mostrado na figura abaixo.
   ![](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin0.png)

* **Quando programas já existem no Cloud Manager**

   Se o(s) programa(s) já existir(em) em sua Organização, a landing page o direcionará para adicionar outro programa e exibirá todos os programas existentes também, como mostrado na figura abaixo.

   ![](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin1.png)

* **Quando um programa existe e o usuário é o Administrador do sistema**

   Se programas já existirem em sua organização e você for um Administrador do sistema, sua landing page exibirá o botão **Gerenciar acesso** junto com a opção **Adicionar programa**, conforme mostrado na figura abaixo.

   ![](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/admin-console-4.png)

A partir daqui, um usuário com as permissões certas, como uma função de Proprietário comercial no Cloud Manager, pode selecionar **Adicionar programa** para iniciar o [Assistente para adicionar programa](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/production-programs/creating-production-program.html?lang=en#getting-access).

Para saber como adicionar um programa no Cloud Manager, consulte:

* Criação de um programa de produção
* Criação de um programa de sandbox