---
title: Gerenciar Ambientes - Cloud Service
description: Gerenciar Ambientes - Cloud Service
translation-type: tm+mt
source-git-commit: 1304a0cfa67c38943b1a36c105fbd5eafb3f8c4f
workflow-type: tm+mt
source-wordcount: '1249'
ht-degree: 4%

---


# Gerenciamento de ambientes {#manage-environments}

A seção a seguir descreve os tipos de ambientes que um usuário pode criar e como ele pode criar um ambiente.

## Tipos de ambientes {#environment-types}

Um usuário com as permissões necessárias pode criar os seguintes tipos de ambientes (dentro dos limites do que está disponível para o locatário específico).

* **Produção e Ambiente** de estágio: A Produção e a Fase estão disponíveis como uma dupla e são utilizadas para fins de teste e produção.

* **Desenvolvimento**: Um ambiente de desenvolvimento pode ser criado para fins de desenvolvimento e teste e será associado apenas a pipelines de não-produção.

   >[!NOTE]
   >Um ambiente de desenvolvimento criado automaticamente em um programa Sandbox será configurado para incluir as soluções Sites e Ativos.

   A tabela a seguir resume os tipos de Ambientes e seus atributos:

   | Nome | Camada do autor | Publicar camada | O usuário pode criar | O usuário pode excluir | Pipeline que pode ser associado ao ambiente |
   |--- |--- |--- |--- |---|---|
   | Produção | Sim | Sim se os sites estiverem incluídos | Sim | Não | Gasoduto de produção |
   | Estágio | Sim | Sim se os sites estiverem incluídos | Sim | Não | Gasoduto de produção |
   | Desenvolvimento | Sim | Sim se os sites estiverem incluídos | Sim | Sim | Gasoduto de não produção |

   >[!NOTE]
   >A Produção e a Fase estão disponíveis como uma dupla e são utilizadas para fins de teste e produção.  O usuário não poderá criar apenas o Estágio ou somente o ambiente de Produção.

## Adicionando Ambiente {#adding-environments}

1. Clique em **Adicionar Ambiente** para adicionar um ambiente. Este botão estará acessível na tela **Ambientes**.
   ![](assets/environments-tab.png)

   A opção **Adicionar Ambiente** também está disponível no cartão **Ambientes** quando não há nenhum ambiente no programa.

   ![](assets/no-environments.png)

   >[!NOTE]
   >A opção **Adicionar Ambiente** será desativada com base na falta de permissões ou no que pode ser contratado.

1. A caixa de diálogo **Adicionar ambiente** é exibida. O usuário precisa enviar detalhes como **Tipo de ambiente** e **Nome do ambiente** e **Descrição do ambiente** (dependendo do objetivo do usuário ao criar o ambiente dentro dos limites do que está disponível para o locatário específico).

   ![](assets/add-environment2.png)

   >[!NOTE]
   >Ao criar um ambiente, uma ou mais *integrações* são criadas no Adobe I/O. Elas estão visíveis para usuários clientes que têm acesso ao Adobe I/O Console e não devem ser excluídas. Isso é descartado na descrição no Adobe I/O Console.

   ![](assets/add-environment-image1.png)

1. Clique em **Salvar** para adicionar um ambiente com os critérios preenchidos.  Agora a tela *Visão geral* exibe o cartão de onde você pode configurar seu pipeline.

   >[!NOTE]
   >Caso ainda não tenha configurado o pipeline de não-produção, a tela *Visão Geral* exibirá o cartão de onde você pode criar o pipeline de não-produção.


## Visualizando Ambiente {#viewing-environment}

A placa **Ambientes** na página Visão geral lista até três ambientes.

1. Selecione o botão **Mostrar tudo** para navegar até a página de resumo **Ambiente** para visualização de uma tabela com uma lista completa de ambientes.

   ![](assets/environment-view-1.png)

1. A página **Ambientes** exibe a lista de todos os ambientes existentes.

   ![](assets/environment-view-2.png)

1. Selecione qualquer um dos ambientes da lista para visualização dos detalhes do ambiente.

   ![](assets/environment-view-3.png)


## Atualização do Ambiente {#updating-dev-environment}

As atualizações de ambientes de Estágio e Produção são gerenciadas automaticamente pelo Adobe.

As atualizações dos ambientes de desenvolvimento são gerenciadas pelos usuários do programa. Quando um ambiente não estiver executando a versão mais recente do AEM disponível publicamente, o status no Cartão de Ambientes na tela inicial mostrará **ATUALIZAR DISPONÍVEL**.

![](assets/environ-update.png)


A opção **Update** está disponível no cartão **Ambientes**.
Essa opção também está disponível se você clicar em **Detalhes** no cartão **Ambientes**. A página **Ambientes** é aberta e, depois que você selecionar o ambiente de desenvolvimento, clique em **...** e selecione **Atualizar**, conforme mostrado na figura abaixo:

![](assets/environ-update2.png)

Selecionar essa opção permitirá que um Gerenciador de implantação atualize o pipeline associado a esse ambiente para a versão mais recente e execute o pipeline.

Se o pipeline já tiver sido atualizado, o usuário será solicitado a executar o pipeline.

## Excluindo Ambiente {#deleting-environment}

O usuário com as permissões necessárias poderá excluir um ambiente de desenvolvimento.

A opção **Delete** está disponível no menu suspenso no cartão **Ambientes**. Clique em **...** para um ambiente de desenvolvimento que você deseja excluir.

![](assets/environ-delete.png)

A opção de exclusão também estará disponível se você clicar em **Detalhes** no cartão **Ambientes**. A página **Ambientes** é aberta e, depois que você selecionar o ambiente de desenvolvimento, clique em **...** e selecione **Delete**, conforme mostrado na figura abaixo:

![](assets/environ-delete2.png)


>[!NOTE]
>
>Este recurso não está disponível para ambientes de produção/estágio definidos em uma configuração regular de programa para fins de produção. No entanto, o recurso está disponível para ambientes de produção/estágio em um programa Sandbox.

## Gerenciando o Acesso {#managing-access}

Selecione **Gerenciar acesso** no menu suspenso no cartão **Ambientes**. Você pode navegar para a instância do autor diretamente e gerenciar o acesso do seu ambiente.

Consulte [Gerenciando o Acesso à Instância do Autor](/help/onboarding/getting-access-to-aem-in-cloud/navigation.md#manage-access-aem) para saber mais.

![](assets/environ-access.png)


## Acessar o Console do desenvolvedor {#accessing-developer-console}

Selecione **Console do desenvolvedor** no menu suspenso no cartão **Ambientes**. Isso abrirá uma nova guia no seu navegador com a página de logon em **Developer Console**.

Somente um usuário na função de Desenvolvedor terá acesso ao **Developer Console**. A exceção é para Programas Sandbox, nos quais qualquer usuário com acesso ao Programa Sandbox do Cloud Manager terá acesso ao **Developer Console**.

Consulte [Hibernando e Deshibernando Ambientes Sandbox](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/onboarding/getting-access/cloud-service-programs/sandbox-programs.html#hibernating-introduction) para obter mais detalhes.


![](assets/environ-devconsole.png)

Essa opção também está disponível se você clicar em **Detalhes** no cartão **Ambientes**. A página **Ambientes** é aberta e, depois que você selecionar um ambiente, clique em **...** e selecione **Console do desenvolvedor**.

## Fazer logon localmente {#login-locally}

Selecione **Logon local** no menu suspenso no cartão **Ambientes** para efetuar login localmente no Adobe Experience Manager.

![](assets/environ-login-locally.png)

Além disso, você pode fazer logon localmente na página de resumo **Ambientes**.

![](assets/environ-login-locally-2.png)

## Gerenciando Nomes de Domínio Personalizados {#manage-cdn}

Navegue até a página de detalhes **Ambientes** na página Resumo dos Ambientes.

As seguintes ações podem ser executadas no serviço de publicação do seu ambiente, conforme descrito abaixo:

1. [Adicionando um nome de domínio personalizado](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)

1. [Exibindo e Atualizando um Nome de Domínio Personalizado](/help/implementing/cloud-manager/custom-domain-names/view-update-replace-custom-domain-name.md)

1. [Excluindo um Nome de Domínio Personalizado](/help/implementing/cloud-manager/custom-domain-names/delete-custom-domain-name.md)

## Gerenciando Listas de permissões IP {#manage-ip-allow-lists}

Navegue até a página de detalhes do Ambiente na página Resumo dos Ambientes. Você pode executar as seguintes ações nos serviços de Publicação e/ou Autor do seu ambiente aqui.

### Aplicação de uma Lista de permissões IP {#apply-ip-allow-list}

A aplicação de uma Lista de permissões IP é o processo pelo qual todos os intervalos IP incluídos na definição da Lista de permissões são associados a um serviço de Autor ou Publicação em um ambiente. Um usuário na função Proprietário da empresa ou Gerenciador de implantação deve estar conectado para poder aplicar uma Lista de permissões de IP.

>[!NOTE]
>A Lista de permissões IP deve existir no Gerenciador de nuvem para aplicá-la a um serviço de ambiente. Para saber mais sobre Listas de permissões de IP no Cloud Manager, navegue até [Introdução às Listas de permissões de IP no Cloud Manager](/help/implementing/cloud-manager/ip-allow-lists/introduction.md).

Siga as etapas abaixo para aplicar uma Lista de permissões IP:

1. Navegue até o ambiente específico na página de detalhes **Ambientes** e navegue até a tabela **Listas de permissões IP**.
1. Use os campos de entrada na parte superior da tabela Lista de permissões IP para selecionar a Lista de permissões IP e o serviço Autor ou Publicação ao qual deseja aplicá-la.
1. Clique em **Aplicar** e confirme seu envio.

### Desaplicando uma Lista de permissões IP {#unapply-ip-allow-list}

Desaplicar uma Lista de permissões IP é o processo pelo qual todos os intervalos IP incluídos na definição da Lista de permissões são desassociados de um serviço Autor ou Editor em um ambiente. Um usuário na função Proprietário da empresa ou Gerenciador de implantação deve estar conectado para poder desaplicar uma Lista de permissões de IP.

Siga as etapas abaixo para desaplicar uma Lista de permissões IP:

1. Navegue até a página de detalhes **Ambientes** específica da tela Ambientes e navegue até a tabela **Listas de permissões IP**.
1. Identifique a linha na qual a regra de Lista de permissões IP que você deseja desaplicar está listada.
1. Selecione **...** na extremidade direita da linha.
1. Selecione a opção **Desaplicar** e confirme sua submissão.


