---
title: Introdução ao Cloud Manager
description: Saiba mais sobre como o Cloud Manager dá suporte ao seu projeto do AEM por meio de programas, ambientes e pipelines.
exl-id: b743f126-b34e-4f48-a3f0-5dbd4e1ac34e
source-git-commit: 6181b066742357169b67f605ac3970685537bb5e
workflow-type: tm+mt
source-wordcount: '864'
ht-degree: 94%

---


# Introdução ao Cloud Manager {#intro-cloud-manager}

O Cloud Manager é um componente essencial do AEM as a Cloud Service e serve como ponto de entrada único para a equipe. Seus pipelines de CI/CD criados com propósitos específicos estão equipados de forma a garantir testes completos e código da mais alta qualidade para fornecer experiências excepcionais. Para garantir que os clientes possam iniciar rapidamente seus projetos, o Cloud Manager fornece tudo o que é necessário de maneira automatizada, incluindo a capacidade de criar recursos e ambientes de nuvem e acessar repositórios Git. Esses recursos dão suporte a configurações de desenvolvimento empresarial para que as equipes possam trabalhar para confirmar alterações com frequência, fornecer experiências digitais excepcionais com rapidez e acelerar o tempo de retorno.

O administrador do sistema é responsável pela configuração da equipe do Cloud Manager, que incluirá desenvolvedores e os indivíduos que criarão os recursos de nuvem. Para obter mais informações sobre como configurar e dimensionar sua equipe de desenvolvimento corporativo e ver como o AEM as a Cloud Service pode apoiar seu processo de desenvolvimento, consulte o documento [Configuração de desenvolvimento de equipes corporativas para o AEM as a Cloud Service](/help/implementing/cloud-manager/managing-code/enterprise-team-dev-setup.md).

## Acesso à página de Visão geral do Cloud Manager {#navigate-cloud-manager}

Siga estas etapas para acessar o Cloud Manager.

1. Acesse a página de logon do Cloud Manager em [`https://my.cloudmanager.adobe.com`.](https://my.cloudmanager.adobe.com/)

1. Selecione o programa na página **Programas e produtos** do Cloud Manager para abrir a página **Visão geral**.

Também é possível navegar até a página Programas e produtos do Cloud Manager na página inicial da Adobe Experience Cloud seguindo estas etapas.

1. Acesse a Adobe Experience Cloud em [`https://experience.adobe.com`](https://experience.adobe.com) e faça logon usando sua Adobe ID.

1. Certifique-se de estar na organização correta, conferindo o nome da organização exibido na parte superior direita da barra de ferramentas.

1. Selecione **Experience Manager**.

1. No **Cloud Manager** , clique em **Launch**

## Permissões com base em funções no Cloud Manager {#role-based-permissions}

| Permissão | Descrição | Proprietário da empresa | Gerente de implantação | Gerente de programas | Desenvolvedor |
|--- |--- |--- |--- |--- |--- |
| Adicionar programa<br>Editar programa | Adicionar um novo programa<br>Adicionar ou remover soluções ou complementos | x |  |  |  |
| Criar ambiente | Criar ambientes de produção+preparo e desenvolvimento | x | x |  |  |
| Atualizar ambiente | Atualizar ambientes de produção+preparo e desenvolvimento | x | x |  |  |
| Excluir ambiente de desenvolvimento | Excluir ambientes de desenvolvimento | x | x |  |  |
| Configuração de pipeline | Configurar e editar pipelines |  | x |  |  |
| Execução de pipeline | Iniciar pipelines | x | x |  |  |
| Execução de pipeline | Rejeitar/aprovar falhas importantes nos quality gates (portais de qualidade) de 3 níveis | x | x | x |  |
| Execução de pipeline | Fornecer aprovação para publicação | x | x | x |  |
| Execução de pipeline | Agendar implantações de produção | x | x | x |  |
| Exclusão de pipeline | Permitir exclusão de pipeline |  | x |  |  |
| Cancelamento de execuções | Cancelar a execução atual |  | x |  |  |
| Gerar token de acesso pessoal | Acesso ao Git |  | x |  | x |
| Criar RDE | Criar um ambiente de desenvolvimento rápido | x |  |  | x |
| Redefinir RDE | Redefinir um ambiente de desenvolvimento rápido | x |  |  | x |
| Criar/modificar conjuntos de conteúdo | Criar ou modificar um conjunto de conteúdo para cópia de conteúdo |  | x |  |  |
| Iniciar/cancelar cópia de conteúdo | Iniciar ou cancelar um processo de cópia de conteúdo |  | x |  |  |

>[!NOTE]
>
>Um usuário pode ser atribuído a várias funções. Por exemplo, atribuir ambas funções **Proprietário da empresa** e **Gerente de implantação** a um usuário resultará na soma dessas permissões.

>[!TIP]
>
>Perfis de permissão personalizados com permissões configuráveis também estão disponíveis. Consulte o documento [Permissões personalizadas](/help/implementing/cloud-manager/custom-permissions.md) para obter mais detalhes.

## Programas do Cloud Manager {#cloud-manager-programs}

Os programas do Cloud Manager representam conjuntos de ambientes do Cloud Manager que oferecem suporte a agrupamentos lógicos de iniciativas de negócios. Normalmente, esses agrupamentos correspondem a um Contrato de nível de serviço (SLA) adquirido. Por exemplo, um programa pode representar os recursos do AEM que dão suporte ao site público de uma organização, enquanto que outro programa representa um DAM interno.


Assista a este [vídeo](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/programs.html?lang=pt-BR) para saber mais sobre como usar os programas do Cloud Manager.

Um usuário pode criar um programa de **Sandbox** ou **Produção**.

* Um **programa de produção** é criado para permitir o tráfego direto em um momento adequado no futuro.
   * Consulte [Introdução aos programas de produção](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-production-programs.md) para obter mais detalhes.

* Um **programa de sandbox** é normalmente criado para fins de treinamento, execução de demonstrações, capacitação, criação de POCs ou documentação.
   * Não se destina a transportar tráfego direto e terá restrições que um programa de produção não terá.
   * Ele inclui sites e ativos e é preenchido automaticamente com uma ramificação Git que inclui o código de amostra, um ambiente de desenvolvimento e um pipeline de não produção.
   * Consulte [Introdução aos programas de sandbox](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-sandbox-programs.md) para obter mais detalhes.

## Ambientes do Cloud Manager {#cloud-manager-environments}

Seus ambientes de nuvem serão criados, acessados e visualizados por meio do Cloud Manager. Eles podem ser ambientes de produção, preparo ou desenvolvimento. Ambientes diferentes atendem a diferentes propósitos e podem ser usados com diferentes pipelines de CI/CD. Os ambientes são compostos de serviços como:

* [Serviços de autoria do AEM](#author-services)
* [Serviços de publicação do AEM](#publish-services)
* [Serviços de Dispatcher](#dispatcher-services)

>[!TIP]
>
> Veja o vídeo [Uso de ambientes do Adobe Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/environments.html?lang=pt-BR), uma visão geral dos ambientes disponíveis.
>
>Consulte o documento [Gerenciar ambientes](/help/implementing/cloud-manager/manage-environments.md) para saber mais sobre os tipos de ambientes que um usuário pode criar e como criá-los.

### Serviço de autoria do AEM {#author-services}

Um serviço de autoria do AEM está incluído em ambientes em que o conteúdo do site e os ativos digitais são criados, gerenciados e atualizados. Normalmente, apenas usuários internos têm acesso ao serviço de autoria e o acesso a ele exige logon. O serviço de autoria atua como um ambiente de autoria e visualização.

### Serviço de publicação do AEM {#publish-services}

Um serviço de publicação do AEM está incluído em ambientes que hospedam a experiência do usuário final, como um site. Esse é o serviço que os visitantes do site visualizarão e com o qual interagirão. Normalmente, o serviço de publicação está disponível ao público.

### Serviço de Dispatcher do AEM {#dispatcher-services}

O dispatcher é um módulo `Apache HTTP Web server` que fornece uma camada de segurança e desempenho que fica na frente do serviço de publicação do AEM.
