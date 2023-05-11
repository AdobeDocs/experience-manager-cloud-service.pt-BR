---
title: Criar ambientes
description: Saiba como usar o Cloud Manager para criar seus primeiros ambientes.
role: Admin, User, Developer
exl-id: 31940e1e-fe27-4c5f-b67f-41affebea63a
source-git-commit: 5c5db0d133adfbbb678930ef27d8ade10fd0c3be
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 86%

---

# Criar ambientes {#create-environments}

Nesta parte da [jornada de integração,](overview.md) você aprenderá a usar o Cloud Manager para criar seus primeiros ambientes.

## Objetivo {#objective}

Tendo lido o documento [Criação de programas](create-program.md) desta jornada de integração, agora você tem seu próprio programa do Cloud Manager. Agora você pode aprender a usar o Cloud Manager para criar seus primeiros ambientes para esse programa.

Depois de ler este documento, você deverá:

* Entender o que é um ambiente.
* Saber a diferença entre os diferentes ambientes.
* Ser capaz de criar seu próprio ambiente.

## O que é um ambiente? {#environments}

Os ambientes ficam abaixo dos programas na hierarquia do Cloud Manager. Embora os programas permitam organizar sua solução e conceder acesso a membros de uma equipe específica a esses programas, os ambientes pertencem a programas específicos e são instâncias individuais das soluções da Adobe nesses programas. Os ambientes são usados para um propósito específico, como autoria de conteúdo ou teste de novos desdobramentos. Os pipelines de CI/CD do Cloud Manager facilitam a implantação do código nesses ambientes a partir de repositórios Git.

Recordando o exemplo teórico da WKND Travel and Adventure Enterprises, que é um locatário com foco em mídias relacionadas a viagens, eles podem ter dois programas: um programa do Sites para a divisão WKND Magazine e um programa do Assets para a divisão WKND Media. Cada programa provavelmente terá alguns ambientes, como um ambiente de produção para atender o tráfego real do site e um ambiente de desenvolvimento para testar o novo código do aplicativo.

Há quatro tipos diferentes de ambientes:

* **Produção e preparo** - Os ambientes de produção e preparo estão disponíveis como um par e são usados para fins de produção e teste, respectivamente.
* **Desenvolvimento** - Um ambiente de desenvolvimento pode ser criado para fins de desenvolvimento e testes, e pode ser associado apenas a pipelines de não produção.
* **Desenvolvimento rápido**: um ambiente de desenvolvimento rápido (RDE) permite que um desenvolvedor implante e revise alterações rapidamente, minimizando o tempo necessário para testar recursos que comprovadamente funcionam em um ambiente de desenvolvimento local.

Para os propósitos dessa jornada de integração, a fim de começar a usar o mínimo possível, você criará um ambiente de desenvolvimento que poderá ser usado para explorar AEM recursos do as a Cloud Service.

## Criar ambientes {#creating-environments}

1. Faça logon no Cloud Manager, em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/), e selecione a organização apropriada.

1. Clique no programa ao qual deseja adicionar um ambiente.

1. Na página **Visão geral do programa**, clique em **Adicionar ambiente** no cartão **Ambientes** para adicionar um ambiente.

   ![Cartão Ambientes](/help/implementing/cloud-manager/assets/no-environments.png)

   * A opção **Adicionar ambiente** também está disponível na guia **Ambientes**.

      ![Guia Ambientes](/help/implementing/cloud-manager/assets/environments-tab.png)

   * A opção **Adicionar ambiente** pode estar desativada devido à falta de permissões ou dependendo dos recursos licenciados.

1. Na caixa de diálogo **Adicionar ambiente**:

   * Selecione um **Tipo de ambiente**.
      * O número de ambientes disponíveis/usados é exibido entre parênteses atrás do tipo de ambiente de desenvolvimento.
   * Forneça o **Nome do ambiente**.
   * Forneça a **Descrição do ambiente**.
   * Selecione a **Região da nuvem**.

   ![Caixa de diálogo Adicionar ambiente](/help/implementing/cloud-manager/assets/add-environment2.png)

1. Clique em **Salvar** para adicionar o ambiente especificado.

Quando o ambiente estiver disponível, os membros da sua organização serão atribuídos ao perfil de produto **Desenvolvedor** para fazer logon no Cloud Manager e gerenciar os repositórios Git do Cloud Manager.

## O que vem a seguir {#whats-next}

Agora que leu esta parte da jornada de integração, você deve:

* Entender o que é um ambiente.
* Saber a diferença entre os diferentes ambientes.
* Ser capaz de criar seu próprio ambiente.

Seus recursos de nuvem foram criados e estão prontos para serem acessados pela sua equipe. Como administrador do sistema, primeiro você deve atribuir os membros da equipe aos perfis de produto do AEM as a Cloud Service no Adobe Admin Console para que eles acessem esses recursos.

Portanto, você deve continuar sua jornada de integração revisando em seguida o documento [Atribuição de membros da equipe aos perfis de produto do AEM as a Cloud Service.](assign-profiles-aem.md) Nesse documento, você aprenderá a conceder aos membros da equipe os direitos necessários para acessar seus novos ambientes.

## Recursos adicionais {#additional-resources}

Veja a seguir recursos adicionais e opcionais, caso deseje ir além do conteúdo da jornada de integração.

* [Gerenciamento de ambientes](/help/implementing/cloud-manager/manage-environments.md) - Saiba mais sobre os tipos de ambientes que você pode criar e como criá-los para o seu projeto do Cloud Manager.
* [Uso do Adobe Cloud Manager - Ambientes](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/environments.html?lang=pt-BR) - Os ambientes do Cloud Manager incluem os serviços de autoria, publicação e dispatcher do AEM. Saiba como diferentes ambientes oferecem suporte a funções e podem ser envolvidos usando diferentes pipeline de CI/CD.
* [Dicas e truques do AEM Campeão - Tipos de Ambiente do Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/expert-resources/aem-champions/environment-types.md) - Assista a este vídeo para obter uma visão geral dos tipos de ambiente do Cloud Manager de um campeão de AEM.
* [Ambientes de desenvolvimento rápido](/help/implementing/developing/introduction/rapid-development-environments.md) - Consulte esta documentação para obter detalhes sobre como usar um RDE
