---
title: Saiba o que é o Cloud Manager
description: Siga esta página para saber mais sobre o Cloud Manager, os programas do Cloud Manager e os ambientes.
exl-id: b743f126-b34e-4f48-a3f0-5dbd4e1ac34e
source-git-commit: 900bcfd2b05b7c996c7ef51118d1f09a16020332
workflow-type: tm+mt
source-wordcount: '756'
ht-degree: 1%

---

# Introdução ao Cloud Manager {#intro-cloud-manager}

O Cloud Manager é um componente essencial do AEM como um Cloud Service e serve como ponto de entrada único para sua equipe.

Para oferecer suporte a clientes com configurações de desenvolvimento empresarial, o AEM as a Cloud Service integra-se totalmente ao Cloud Manager e seus pipelines de CI/CD criados especificamente, que são equipados para garantir testes completos e a mais alta qualidade do código para fornecer experiências excepcionais.

Para garantir que os clientes possam começar rapidamente com o AEM as a Cloud Service, o Cloud Manager fornece tudo o que é necessário para começar a usar de autoatendimento, incluindo a capacidade de criar recursos e ambientes de nuvem. Dessa forma, seus desenvolvedores de AEM podem acessar o repositório Git por meio do Cloud Manager. Usando o Cloud Manager, as equipes de desenvolvimento podem trabalhar para confirmar as alterações com frequência de forma automatizada.

O Administrador do sistema será responsável pela configuração da equipe do Cloud Manager, que incluirá indivíduos que criarão os recursos e desenvolvedores da nuvem. Consulte [Configuração de desenvolvimento de equipe empresarial para AEM as a1/> para saber como o Cloud Manager suporta na Configuração de desenvolvimento de equipe empresarial.](/help/implementing/cloud-manager/enterprise-team-dev-setup.md)

## Navegar até a página Visão geral do Cloud Manager {#navigate-cloud-manager}

Siga as etapas abaixo para navegar até o Cloud Manager:

1. Navegue diretamente para a página de logon do Cloud Manager de [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/).

   >[!NOTE]
   >Marque esta página como referência futura e para ajudá-lo a navegar diretamente para a página de aterrissagem do Cloud Manager.

1. Selecione o programa na página **Programas e Produtos** do Cloud Manager para iniciar a página **Visão geral**.

Além disso, também é possível navegar até a página Programas e produtos do Cloud Manager na página inicial do Adobe Experience Cloud. Siga as etapas abaixo:

1. Navegue diretamente para [Adobe Experience Cloud](https://experience.adobe.com/#/@foundationinternal/home) e faça logon usando sua Adobe ID.

1. Selecione **Experience Manager**.

1. Clique em **Iniciar** no cartão do Cloud Manager. Depois de fazer logon no Cloud Manager com êxito, você estará pronto para usar a interface do usuário (UI).

Após o logon bem-sucedido, você será direcionado para a página inicial do Cloud Manager.

## Programas do Cloud Manager {#cloud-manager-programs}

Os Programas do Cloud Manager representam conjuntos de ambientes do Cloud Manager que oferecem suporte a conjuntos lógicos de iniciativas de negócios, normalmente correspondendo a um SLA (Service Level Agreement, contrato de nível de serviço) adquirido. Por exemplo, um Programa pode representar os recursos AEM para suportar os sites públicos globais, enquanto outro Programa representa um DAM central interno. Assista a este [vídeo](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/programs.html?lang=en) para saber mais sobre como usar os programas do Cloud Manager.

Um usuário pode criar um programa de **Sandbox** ou **Produção**.

* Um *Programa de produção* é criado para ativar o tráfego ao vivo no momento adequado no futuro.
Consulte [Introdução aos programas de produção](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/production-programs/introduction-production-programs.html?lang=en) para obter mais detalhes.

* Um *Programa de sandbox* normalmente é criado para servir os propósitos de treinamento, execução de demonstração, ativação, POC&#39;s ou documentação. Não se destina a transportar tráfego vivo e terá restrições que um programa de produção não irá. Ele incluirá Sites e Ativos e será fornecido automaticamente com uma ramificação Git que inclui código de amostra, um ambiente de desenvolvimento e um pipeline não relacionado à produção.
Consulte [Introdução aos programas de sandbox](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/sandbox-programs/introduction-sandbox-programs.html?lang=en) para obter mais detalhes.

## Ambientes do Cloud Manager {#cloud-manager-environments}

Seus ambientes de nuvem serão criados, acessados e visualizados pelo Cloud Manager. Pode ser um ambiente de Produção, Ambiente de Preparo ou Ambiente de Desenvolvimento. Ambientes diferentes são compatíveis com diferentes finalidades e podem ser envolvidos usando diferentes pipeline de CI/CD. Os ambientes são compostos de serviços como:

* [Serviços de criação do AEM](#author-services)
* [Serviços de publicação do AEM](#publish-services)
* [Serviços do Dispatcher](#dispatcher-services)

   >[!NOTE]
   > Consulte o vídeo [Uso de ambientes do Adobe Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/environments.html?lang=en#cloud-manager) para saber mais sobre os ambientes disponíveis. Além disso, consulte [Gerenciar ambientes](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html?lang=en) para saber mais sobre os tipos de ambientes que um usuário pode criar e como o usuário pode criar um ambiente.

### Serviço de criação do AEM {#author-services}

O AEM Author Service é incluído em um ambiente em que o conteúdo do site e os ativos digitais são criados, gerenciados e atualizados. Normalmente, somente os usuários internos têm acesso ao Serviço de autor e estão atrás de uma tela de logon. O Serviço de criação foi criado como um ambiente de criação e visualização.

### Serviço de publicação do AEM {#publish-services}

O AEM Publish Service está incluído em um ambiente que hospeda a experiência do usuário final, como um site. Esse é o serviço que os visitantes do site visualizarão e interagirão. Normalmente, o Serviço de publicação está disponível publicamente.

### AEM Serviço Dispatcher {#dispatcher-services}

O Dispatcher é um módulo `Apache HTTP Web server` que fornece uma camada de segurança e desempenho que fica na frente do AEM Publish Service.
