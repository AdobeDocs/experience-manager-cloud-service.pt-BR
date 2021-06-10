---
title: Gerenciar ambientes - Cloud Service
description: Gerenciar ambientes - Cloud Service
exl-id: 93fb216c-c4a7-481a-bad6-057ab3ef09d3
source-git-commit: 0a0bb01dfc2786edc4ebd331ddad44b12ca64fa2
workflow-type: tm+mt
source-wordcount: '1623'
ht-degree: 3%

---

# Gerenciamento de ambientes {#manage-environments}

A seção a seguir descreve os tipos de ambiente que um usuário pode criar e como ele pode criar um ambiente.

## Tipos de ambiente {#environment-types}

Um usuário com as permissões necessárias pode criar os seguintes tipos de ambiente (dentro dos limites do que está disponível para o locatário específico).

* **Ambiente** de produção e preparo: A Produção e o Estágio estão disponíveis como um duo e são usados para fins de teste e produção.

* **Desenvolvimento**: Um ambiente de desenvolvimento pode ser criado para fins de desenvolvimento e teste e será associado apenas a pipelines não relacionados à produção.

   >[!NOTE]
   >Um ambiente de desenvolvimento criado automaticamente em um programa de sandbox será configurado para incluir soluções do Sites e do Assets.

   A tabela a seguir resume os tipos de ambientes e seus atributos:

   | Nome | Camada do autor | Publicar camada | O usuário pode criar | O usuário pode excluir | Pipeline que pode ser associado ao ambiente |
   |--- |--- |--- |--- |---|---|
   | Produção | Sim | Sim se Sites incluídos | Sim | Não | Gasoduto de produção |
   | Estágio | Sim | Sim se Sites incluídos | Sim | Não | Gasoduto de produção |
   | Desenvolvimento | Sim | Sim se Sites incluídos | Sim | Sim | Gasoduto de não produção |

   >[!NOTE]
   >A Produção e o Estágio estão disponíveis como um duo e são usados para fins de teste e produção.  O usuário não poderá criar somente o ambiente de Preparo ou Produção.

## Adicionar ambiente {#adding-environments}

1. Clique em **Adicionar ambiente** para adicionar um ambiente. Esse botão será acessível na tela **Ambientes**.
   ![](assets/environments-tab.png)

   A opção **Adicionar ambiente** também está disponível no cartão **Ambientes** quando há zero ambientes no programa.

   ![](assets/no-environments.png)

   >[!NOTE]
   >A opção **Adicionar Ambiente** será desativada com base na falta de permissões ou no que pode ser contratado.

1. A caixa de diálogo **Adicionar ambiente** é exibida. O usuário precisa enviar detalhes como **Tipo de ambiente** e **Nome do ambiente** e **Descrição do ambiente** (dependendo do objetivo do usuário ao criar o ambiente dentro dos limites do que está disponível para o locatário específico).

   ![](assets/add-environment2.png)

   >[!NOTE]
   >Ao criar um ambiente, uma ou mais *integrações* são criadas no Adobe I/O. Elas estão visíveis para os usuários clientes que têm acesso ao console Adobe I/O e não devem ser excluídas. Isso é descartado na descrição no console do Adobe I/O.

   ![](assets/add-environment-image1.png)

1. Clique em **Save** para adicionar um ambiente com os critérios preenchidos.  Agora a tela *Visão geral* exibe o cartão de onde você pode configurar o pipeline.

   >[!NOTE]
   >Caso ainda não tenha configurado o pipeline de não produção, a tela *Visão geral* exibe o cartão de onde você pode criar o pipeline de não produção.

## Detalhes do ambiente {#viewing-environment}

O cartão **Ambientes** na página Visão geral lista até três ambientes.

1. Selecione o botão **Mostrar tudo** para navegar até a página de resumo **Ambiente** para exibir uma tabela com uma lista completa de ambientes.

   ![](assets/environment-view-1.png)

1. A página **Ambientes** exibe a lista de todos os ambientes existentes.

   ![](assets/environment-view-2.png)

1. Selecione qualquer um dos ambientes na lista para exibir os detalhes do ambiente.

   >[!NOTE]
   >O Serviço de Pré-visualização será implantado continuamente em todos os Programas. Os clientes serão notificados no produto quando o Programa estiver ativado para o Serviço de visualização. Consulte a seção [Acesso ao serviço de visualização](#access-preview-service) para obter mais detalhes.

   ![](assets/environ-preview1.png)


### Acesso ao Serviço de visualização {#access-preview-service}

O recurso Serviço de visualização fornece um Serviço de visualização (publicação) adicional para cada AEM como um ambiente de Cloud Service via Cloud Manager.

Visualize a experiência final de um site antes que ele chegue ao ambiente de publicação e esteja disponível publicamente. Alguns indicadores antes de visualizar e usar o Serviço de visualização:

1. **Versão** AEM: Seu ambiente deve estar AEM versão  `2021.5.5343.20210542T070738Z` ou superior. Certifique-se de que um pipeline de atualização tenha sido executado com êxito em seu ambiente para fazer isso.

1. **Bloqueio** de Lista de permissões IP padrão: Após a primeira criação, você deve desaplicar ativamente a Lista de permissões IP padrão do Serviço de visualização em seu ambiente para habilitar o acesso.

1. **Publicar conteúdo na visualização**: Você pode publicar conteúdo no Serviço de visualização usando a interface Gerenciar publicação no AEM. Consulte [Visualização de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/authoring/fundamentals/previewing-content.html?lang=en) para obter mais detalhes.

Um usuário com as permissões necessárias deve executar um dos seguintes procedimentos para *desbloquear* o acesso ao serviço de visualização e fornecer o acesso desejado:

1. Crie uma Lista de permissões IP apropriada e a aplique ao serviço de visualização. Siga isto imediatamente ao desaplicar `Preview Default [Env ID] IP Allow List` do Serviço de Pré-visualização.

   OU,

1. Use o fluxo de trabalho de atualização da Lista de permissões de IP para remover o IP padrão e adicionar IP(s) conforme apropriado. Consulte [Visualização e atualização de uma Lista de permissões de IP](/help/implementing/cloud-manager/ip-allow-lists/view-update-ip-allow-list.md)para saber mais.

   >[!NOTE]
   >As etapas acima devem ser feitas antes de compartilhar o URL do serviço de visualização com qualquer uma das equipes, para garantir que os membros apropriados de sua equipe possam acessar o URL de visualização.

   Quando o acesso ao serviço de visualização estiver desbloqueado, o ícone de bloqueio não será mais exibido, como mostrado abaixo.

   ![](/help/implementing/cloud-manager/assets/preview-service1.png)

## Atualização do ambiente {#updating-dev-environment}

As atualizações de ambientes de Preparo e Produção são gerenciadas automaticamente pelo Adobe.

As atualizações para ambientes de desenvolvimento são gerenciadas pelos usuários do programa. Quando um ambiente não estiver executando a versão de AEM mais recente disponível publicamente, o status no Cartão de ambientes na tela inicial mostrará **ATUALIZAR DISPONÍVEL**.

![](assets/environ-update.png)


A opção **Update** está disponível no cartão **Ambientes**.
Essa opção também estará disponível se você clicar em **Detalhes** no cartão **Ambientes**. A página **Ambientes** é aberta e, depois de selecionar o Ambiente de desenvolvimento, clique em **...** e selecione **Atualizar**, conforme mostrado na figura abaixo:

![](assets/environ-update2.png)

Selecionar essa opção permitirá que um Gerenciador de implantação atualize o pipeline associado a esse ambiente para a versão mais recente e, em seguida, execute o pipeline.

Se o pipeline já tiver sido atualizado, o usuário será solicitado a executar o pipeline.

## Excluindo o ambiente {#deleting-environment}

O usuário com as permissões necessárias poderá excluir um ambiente de desenvolvimento.

A opção **Delete** está disponível no menu suspenso no cartão **Ambientes**. Clique em **...** para um ambiente de desenvolvimento que você deseja excluir.

![](assets/environ-delete.png)

A opção de exclusão também estará disponível se você clicar em **Detalhes** no cartão **Ambientes**. A página **Ambientes** é aberta e, depois de selecionar o Ambiente de desenvolvimento, clique em **...** e selecione **Delete**, conforme mostrado na figura abaixo:

![](assets/environ-delete2.png)


>[!NOTE]
>Esse recurso não está disponível para o ambiente de Produção/Estágio definido em um programa de Produção configurado para fins de produção. No entanto, o recurso está disponível para ambientes de Produção/Estágio em um programa de sandbox.

## Gerenciamento de acesso {#managing-access}

Selecione **Gerenciar acesso** no menu suspenso do cartão **Ambientes**. Você pode navegar diretamente para a instância do autor e gerenciar o acesso do seu ambiente.

Consulte [Gerenciando o Acesso à Instância do Autor](/help/onboarding/what-is-required/accessing-aem-instance.md) para saber mais.

![](assets/environ-access.png)


## Acessar o Console do desenvolvedor {#accessing-developer-console}

Selecione **Console do Desenvolvedor** no menu suspenso do cartão **Ambientes**. Isso abrirá uma nova guia no navegador com a página de logon em **Console do desenvolvedor**.

Somente um usuário na função Desenvolvedor terá acesso ao **Console do Desenvolvedor**. A exceção é para Programas de sandbox, em que qualquer usuário com acesso ao Programa de sandbox do Cloud Manager terá acesso ao **Console do desenvolvedor**.

Consulte [Hibernando e removendo ambientes de sandbox](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/cloud-service-programs/sandbox-programs.html#hibernating-introduction) para obter mais detalhes.


![](assets/environ-devconsole.png)

Essa opção também estará disponível se você clicar em **Detalhes** no cartão **Ambientes**. A página **Ambientes** é aberta e, depois de selecionar um ambiente, clique em **...** e selecione **Console do desenvolvedor**.

## Fazer logon localmente {#login-locally}

Selecione **Logon local** no menu suspenso do cartão **Ambientes** para fazer logon localmente no Adobe Experience Manager.

![](assets/environ-login-locally.png)

Além disso, você pode fazer logon localmente na página de resumo **Ambientes**.

![](assets/environ-login-locally-2.png)


## Gerenciando Nomes de Domínio Personalizados {#manage-cdn}

Navegue até a página de detalhes **Ambientes** na página Resumo dos ambientes .

>[!NOTE]
>Agora, os nomes de domínio personalizados são compatíveis com os programas do Cloud Manager for Sites para Serviços de publicação e visualização. Cada Ambiente do Cloud Manager pode hospedar até 250 domínios personalizados por ambiente.

As seguintes ações podem ser executadas no serviço de Publicação para o seu ambiente, conforme descrito abaixo:

1. [Adicionar um nome de domínio personalizado](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)

1. [Visualização e atualização de um nome de domínio personalizado](/help/implementing/cloud-manager/custom-domain-names/view-update-replace-custom-domain-name.md)

1. [Excluindo um Nome de Domínio Personalizado](/help/implementing/cloud-manager/custom-domain-names/delete-custom-domain-name.md)

1. [Verificando o status do ](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md#pre-existing-cdn) nome de domínio personalizado ou de um certificado  [SSL](/help/implementing/cloud-manager/managing-ssl-certifications/check-status-ssl-certificate.md#pre-existing-cdn).

1. [Verificando o status de uma Lista de permissões IP](/help/implementing/cloud-manager/ip-allow-lists/check-ip-allow-list-status.md#pre-existing-cdn)


## Gerenciando Listas de permissões IP {#manage-ip-allow-lists}

Navegue até a página Detalhes do ambiente na página Resumo dos ambientes . Você pode executar as seguintes ações no(s) serviço(s) de Publicação e/ou Autor para seu ambiente aqui.

>[!NOTE]
>O recurso Lista de permissões de IP agora é compatível com o Cloud Manager para Autor, Publicação e Serviços de visualização (disponível nos programas Sites).

### Aplicação de uma Lista de permissões IP {#apply-ip-allow-list}

A aplicação de uma Lista de permissões IP é o processo pelo qual todos os intervalos IP incluídos na definição da Lista de permissões são associados a um serviço de Autor ou Publicação em um ambiente. Um usuário na função Proprietário comercial ou Gerente de implantação deve estar conectado para poder aplicar uma Lista de permissões de IP.

>[!NOTE]
>A Lista de permissões IP deve existir no Cloud Manager para ser aplicada a um serviço do ambiente. Para saber mais sobre Listas de permissões de IP no Cloud Manager, navegue até [Introdução às Listas de permissões de IP no Cloud Manager](/help/implementing/cloud-manager/ip-allow-lists/introduction.md).

Siga as etapas abaixo para aplicar uma Lista de permissões IP:

1. Navegue até o ambiente específico na página de detalhes **Ambientes** e navegue até a tabela **Listas de permissões IP**.
1. Use os campos de entrada na parte superior da tabela Lista de permissões de IP para selecionar a Lista de permissões de IP e o serviço de Autor ou Publicação ao qual deseja aplicá-la.
1. Clique em **Aplicar** e confirme seu envio.

### Desaplicar uma Lista de permissões IP {#unapply-ip-allow-list}

Desaplicar uma Lista de permissões IP é o processo pelo qual todos os intervalos IP incluídos na definição da Lista de permissões são desassociados de um serviço Autor ou Editor em um ambiente. Um usuário na função Proprietário comercial ou Gerente de implantação deve estar conectado para poder Desaplicar uma Lista de permissões IP.

Siga as etapas abaixo para desaplicar uma Lista de permissões IP:

1. Navegue até a página de detalhes **Ambientes** específica da tela Ambientes e navegue até a tabela **Listas de permissões IP**.
1. Identifique a linha na qual a regra de Lista de permissões IP que você deseja desaplicar está listada.
1. Selecione o **...** a partir da extremidade direita da linha.
1. Selecione a opção **Unapply** e confirme seu envio.
