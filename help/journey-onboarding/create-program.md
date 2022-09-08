---
title: Criar um programa
description: Saiba como usar o Cloud Manager para criar seu primeiro programa.
role: Admin, User, Developer
exl-id: ade4bb43-5f48-4938-ac75-118009f0a73b
source-git-commit: fbf1e0b7cefb1dc981d7ee106283280fb2225007
workflow-type: tm+mt
source-wordcount: '648'
ht-degree: 4%

---

# Criar um programa {#create-program}

Nesta parte do [jornada de integração,](overview.md) você aprenderá a usar o Cloud Manager para criar seu primeiro programa.

## Objetivo {#objective}

Depois de revisar o documento anterior nesta jornada de integração, [Access Cloud Manager,](cloud-manager.md) você garantiu o acesso apropriado ao Cloud Manager. Agora você pode criar seu primeiro programa.

Após ler este documento, você:

* Entenda o que é um programa.
* Conheça a diferença entre programas de produção e sandbox.
* Pode criar seu próprio programa.

## O que é um programa? {#programs}

Os programas são o mais alto nível de organização no Cloud Manager. Dependendo da sua licença com o Adobe, os programas permitem organizar sua solução e conceder acesso a membros de uma equipe específica para esses programas.

Os programas do Cloud Manager representam conjuntos de ambientes do Cloud Manager. Esses programas suportam conjuntos lógicos de iniciativas de negócios, normalmente correspondentes a um Contrato de nível de serviço (SLA) licenciado. Por exemplo, um programa pode representar os recursos AEM para suportar um site público global de uma organização, enquanto outro programa representa um DAM interno e central.

Se você se lembrar do exemplo teórico da WKND Travel and Adventure Enterprises, que é um locatário com foco em mídia relacionada a viagens, eles podem ter dois programas: um programa Sites para a divisão WKND Magazine e um programa Assets para a divisão WKND Media. Os diferentes membros da equipe teriam então acesso aos diferentes programas devido à sua própria divisão das necessidades laborais.

Existem dois tipos diferentes de programas:

* A **programa de produção** é criado para ativar o tráfego ao vivo em seu site. Este é o seu ambiente &quot;real&quot;.
* A **programa sandbox** O é normalmente criado para servir os propósitos de treinamento, execução de demonstrações, ativação, POCs ou documentação.

Como atendem a diferentes objetivos, os diferentes ambientes têm diferentes opções. No entanto, o processo de criação é semelhante. Para essa jornada de integração, criaremos um ambiente sandbox.

>[!NOTE]
>
>Por padrão, um usuário com acesso a um ambiente de AEM também terá a função Cloud > Gerenciar usuário . Essa função em si mesma é insuficiente para dar ao usuário acesso à visualização dos detalhes do programa. Esse usuário com apenas a função de usuário do Cloud Manager pode navegar pelas opções de menu do programa até o URL do autor do ambiente de AEM (se existirem ambientes). Esses usuários devem entrar em contato com o administrador se quiserem obter acesso no nível do programa.

## Criação de um programa de sandbox {#create-sandbox}

Siga estas etapas para criar um programa sandbox.

1. Faça logon no Cloud Manager, em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/), e selecione a organização apropriada.

1. Na página de aterrissagem do Cloud Manager, clique em **Adicionar programa** no canto superior direito da tela.

   ![Página de aterrissagem do Cloud Manager](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin1.png)

1. No assistente criar programa, selecione **Configurar uma sandbox**, forneça um nome de programa e clique em **Criar**.

   ![Criação do tipo de programa](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/create-sandbox.png)

Você verá um novo cartão de programa sandbox na página de aterrissagem com um indicador de status conforme o processo de configuração avança.

![Criação de sandbox a partir da página de visão geral](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/program-create-setupdemo2.png)

Quando o programa estiver concluído, os membros de sua organização serão atribuídos ao **Desenvolvedor** o perfil de produto pode fazer logon no Cloud Manager e gerenciar repositórios git do Cloud Manager.

## O que vem a seguir {#whats-next}

Agora que seu primeiro programa foi criado, você pode criar ambientes para ele. Você deve continuar sua jornada de integração ao revisar o documento [Criar ambientes.](create-environments.md)

## Recursos adicionais {#additional-resources}

Siga os recursos adicionais para saber mais sobre:

* [Programas e tipos de programas](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md) - Saiba mais sobre a hierarquia do Cloud Manager e como os diferentes tipos de programas se encaixam em sua estrutura e como diferem.
* [Criação de programas de sandbox](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md) - Saiba como usar o Cloud Manager para criar seu próprio programa sandbox para treinamento, demonstração, POC ou outros fins que não sejam de produção.
* [Criação de programas de produção](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md) - Saiba como usar o Cloud Manager para criar seu próprio programa de produção para hospedar o tráfego ao vivo.
* [Uso do Adobe Cloud Manager - Programas](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/programs.html) - Os programas do Cloud Manager representam conjuntos de ambientes de AEM que oferecem suporte a conjuntos lógicos de iniciativas de negócios, normalmente correspondendo a um SLA (Service Level Agreement, contrato de nível de serviço) adquirido.
