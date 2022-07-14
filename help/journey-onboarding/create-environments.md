---
title: Criar ambientes
description: Saiba como usar o Cloud Manager para criar seus primeiros ambientes.
role: Admin, User, Developer
source-git-commit: 709a80683357b0d56280ff14aa5f4ba6bf2c6b23
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 0%

---


# Criar ambientes {#create-environments}

Nesta parte do [jornada de integração,](overview.md) você aprenderá a usar o Cloud Manager para criar seus primeiros ambientes.

## Objetivo {#objective}

Após ler o documento anterior nesta jornada de integração, [Criação de programas,](create-program.md) agora você tem seu próprio programa Cloud Manager. Agora você pode aprender a usar o Cloud Manager para criar seus primeiros ambientes para esse programa.

Após ler este documento, você:

* Entenda o que é um ambiente.
* Conheça a diferença entre os diferentes ambientes.
* Ser capaz de criar seu próprio ambiente.

## O que é um ambiente? {#environments}

Os ambientes ficam abaixo dos programas na hierarquia do Cloud Manager. Embora os programas permitam organizar sua solução e conceder acesso a membros de uma equipe específica para esses programas, os ambientes pertencem a programas específicos e são instâncias individuais das soluções do Adobe nesses programas. Os ambientes são usados para um propósito específico, como criação de conteúdo ou teste de novos desenvolvimentos. Os pipelines de CI/CD do Cloud Manager facilitam a implantação do código para esses ambientes a partir de repositórios Git.

Se você se lembrar do exemplo teórico da WKND Travel and Adventure Enterprises, que é um locatário com foco em mídia relacionada a viagens, eles podem ter dois programas: um programa Sites para a divisão WKND Magazine e um programa Assets para a divisão WKND Media. Cada programa provavelmente terá alguns ambientes, como um ambiente de produção que serve o tráfego real do site e um ambiente de desenvolvimento para testar o novo código do aplicativo.

Existem três tipos diferentes de ambientes:

* **Produção e Estágio** - Os ambientes de produção e de preparo estão disponíveis como um par e são usados para fins de produção e teste, respectivamente.
* **Desenvolvimento** - Pode ser criado um ambiente de desenvolvimento para fins de desenvolvimento e de ensaio e pode ser associado apenas a gasodutos não relacionados com a produção.

Para fins dessa jornada de integração, você criará um ambiente de desenvolvimento.

## Criar ambientes {#creating-environments}

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização apropriada.

1. Clique no programa para o qual deseja adicionar um ambiente.

1. No **Visão geral do programa** clique em **Adicionar ambiente** no **Ambientes** cartão para adicionar um ambiente.

   ![Cartão de ambientes](/help/implementing/cloud-manager/assets/no-environments.png)

   * O **Adicionar ambiente** também está disponível no **Ambientes** guia .

      ![Guia Ambientes](/help/implementing/cloud-manager/assets/environments-tab.png)

   * O **Adicionar ambiente** pode ser desativada devido à falta de permissões ou dependendo dos recursos licenciados.

1. No **Adicionar ambiente** exibida:

   * Selecione um **Tipo de ambiente**.
      * O número de ambientes disponíveis/usados é exibido entre parênteses atrás do tipo de ambiente de desenvolvimento.
   * Forneça uma **Nome do ambiente**.
   * Forneça uma **Descrição do ambiente**.
   * Selecione um **Região da nuvem**.

   ![Caixa de diálogo Adicionar ambiente](/help/implementing/cloud-manager/assets/add-environment2.png)

1. Clique em **Salvar** para adicionar o ambiente especificado.

Quando o ambiente estiver disponível, os membros de sua organização serão atribuídos à **Desenvolvedor** O perfil de produto pode fazer logon no Cloud Manager e gerenciar repositórios git do Cloud Manager.

## O que vem a seguir {#whats-next}

Agora que você leu esta parte da jornada de integração, deve:

* Entenda o que é um ambiente.
* Conheça a diferença entre os diferentes ambientes.
* Ser capaz de criar seu próprio ambiente.

Seus recursos de nuvem foram criados e estão prontos para serem acessados pela sua equipe. Como administrador do sistema, você deve primeiro atribuir membros da equipe a AEM perfis de produto as a Cloud Service do Adobe Admin Console para que eles acessem esses recursos.

Portanto, você deve continuar sua jornada de integração ao revisar o documento em seguida [Atribuindo membros da equipe a AEM perfis de produto as a Cloud Service.](assign-profiles-aem.md)  Nesse documento, você aprenderá a conceder aos membros da equipe os direitos necessários para acessar seus novos ambientes.

## Recursos adicionais {#additional-resources}

Siga os recursos adicionais para saber mais sobre:

* [Gerenciamento de ambientes](/help/implementing/cloud-manager/manage-environments.md) - Saiba mais sobre os tipos de ambientes que você pode criar e como criá-los para o seu projeto do Cloud Manager
* [Uso do Adobe Cloud Manager - Ambientes](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/environments.html) - Os ambientes do Cloud Manager são compostos de AEM criação, publicação e serviços do dispatcher. Saiba como diferentes ambientes oferecem suporte a funções e podem ser envolvidos usando diferentes pipeline de CI/CD.
