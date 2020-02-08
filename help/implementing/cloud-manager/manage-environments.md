---
title: Gerenciar ambientes - Serviço em nuvem
description: Gerenciar ambientes - Serviço em nuvem
translation-type: tm+mt
source-git-commit: 81f993325b80c0de17d6032a45ebd61c22169d39

---


# Gerenciamento de ambientes {#manage-environments}

A seção a seguir descreve os tipos de ambiente que um usuário pode criar e como ele pode criar um ambiente.

## Tipos de ambiente {#environment-types}

Um usuário com as permissões necessárias pode criar os seguintes tipos de ambiente (dentro dos limites do que está disponível para o locatário específico).

* **Ambiente**de produção e estágio:
A Produção e a Fase estão disponíveis como uma dupla e são utilizadas para fins de teste e produção.

* **Desenvolvimento**: Um ambiente de desenvolvimento pode ser criado para fins de desenvolvimento e teste e será associado apenas a gasodutos de não produção.

   >[!NOTE]
   >Um ambiente de desenvolvimento criado automaticamente em um programa Sandbox será configurado para incluir soluções Sites e Ativos.

   A tabela a seguir resume os tipos de Ambiente e seus atributos:

   | Nome | Camada do autor | Publicar camada | O usuário pode criar | O usuário pode excluir | Gasoduto que pode ser associado ao ambiente |
   |--- |--- |--- |--- |---|---|
   | Produção | Sim | Sim se os sites estiverem incluídos | Sim | Não | Gasoduto de produção |
   | Estágio | Sim | Sim se os sites estiverem incluídos | Sim | Não | Gasoduto de produção |
   | Desenvolvimento | Sim | Sim se os sites estiverem incluídos | Sim | Sim | Gasoduto de não produção |

   >[!NOTE]
   >
A Produção e a Fase estão disponíveis como uma dupla e são utilizadas para fins de teste e produção.  O usuário não poderá criar somente o Stage ou somente o ambiente Production.

## Adicionar um ambiente {#adding-environments}


1. O usuário clica no botão **Adicionar ambiente** para adicionar um ambiente.

   ![](assets/add-environment.png)

1. A caixa de diálogo **Adicionar ambiente** é exibida. O usuário precisa enviar detalhes como tipo **de** Ambiente e nome **do** Ambiente e descrição **do** Ambiente (dependendo do objetivo do usuário em criar o ambiente dentro dos limites do que está disponível para o locatário específico).

   ![](assets/add-environment2.png)

   >[!NOTE]
   >Ao criar um ambiente, uma ou mais *integrações* são criadas na E/S da Adobe. Eles estão visíveis para usuários clientes que têm acesso ao console de E/S da Adobe e não devem ser excluídos. Isso é descartado na descrição no console de E/S da Adobe.

   ![](assets/add-environment-image1.png)

1. Clique em **Salvar** para adicionar um ambiente com os critérios preenchidos.  Agora a tela *Visão geral* exibe o cartão de onde você pode configurar seu pipeline.

   >[!NOTE]
   >Caso ainda não tenha configurado o pipeline de não-produção, a tela *Visão geral* exibe o cartão de onde você pode criar o pipeline de não-produção.


## Atualização do ambiente {#updating-dev-environment}

As atualizações dos ambientes Stage e Production são gerenciadas automaticamente pela Adobe.

Os usuários do programa gerenciam atualizações para ambientes de desenvolvimento. Quando um ambiente não estiver executando a versão mais recente do AEM disponível publicamente, o status no Cartão do ambiente na tela inicial mostrará **ATUALIZAÇÃO DISPONÍVEL**.

![](assets/manage-environments2.png)
)

Quando esse status for exibido, a opção **Atualizar** estará disponível no menu suspenso, tanto no Cartão de ambiente quanto no menu **Gerenciar** , se você clicar em **Detalhes** no cartão **AMBIENTES** .

![](assets/add-environment4.png)

Selecionar isso no menu suspenso permitirá que um Gerenciador de implantação atualize o pipeline associado a esse ambiente para a versão mais recente e execute o pipeline.

Se o pipeline já tiver sido atualizado, o usuário será solicitado a executar o pipeline.
