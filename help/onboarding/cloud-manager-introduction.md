---
title: Introdução ao Cloud Manager
description: Saiba mais sobre como o Cloud Manager suporta seu projeto de AEM por meio de programas, ambientes e pipelines.
exl-id: b743f126-b34e-4f48-a3f0-5dbd4e1ac34e
source-git-commit: 2d793f22e554c2a4bde8831b5053d1640ba07c70
workflow-type: tm+mt
source-wordcount: '834'
ht-degree: 5%

---

# Introdução ao Cloud Manager {#intro-cloud-manager}

O Cloud Manager é um componente essencial AEM as a Cloud Service e serve como ponto de entrada único para sua equipe. Seus pipelines de CI/CD criados com propósito são equipados para garantir testes completos e a mais alta qualidade do código para fornecer experiências excepcionais. Para garantir que os clientes possam iniciar rapidamente seus projetos, o Cloud Manager fornece tudo o que é necessário de maneira automatizada, incluindo a capacidade de criar recursos e ambientes de nuvem e acessar repositórios Git. Esses recursos suportam configurações de desenvolvimento empresarial para que as equipes possam trabalhar para realizar alterações com frequência, fornecer rapidamente experiências digitais excepcionais e acelerar o tempo de implantação.

O administrador do sistema é responsável pela configuração da equipe do Cloud Manager, que incluirá indivíduos que criarão os recursos e desenvolvedores da nuvem. Para obter mais informações sobre como configurar e dimensionar sua equipe de desenvolvimento empresarial e ver como AEM as a Cloud Service pode suportar seu processo de desenvolvimento, consulte o documento [Configuração de desenvolvimento para equipes corporativas para AEM as a Cloud Service.](/help/implementing/cloud-manager/managing-code/enterprise-team-dev-setup.md)

## Navegar até a página Visão geral do Cloud Manager {#navigate-cloud-manager}

Siga estas etapas para navegar até o Cloud Manager.

1. Navegue até a página de logon do Cloud Manager em [`https://my.cloudmanager.adobe.com`.](https://my.cloudmanager.adobe.com/).

1. Selecione o programa no **Programas e produtos** para iniciar a página **Visão geral** página.

Você também pode navegar até a página Programas e produtos do Cloud Manager na página inicial do Adobe Experience Cloud seguindo essas etapas.

1. Navegue até a Adobe Experience Cloud em [`https://experience.adobe.com`](https://experience.adobe.com) e faça logon usando sua Adobe ID.

1. Certifique-se de estar na organização correta, fazendo referência ao nome da organização exibido na parte superior direita da barra de ferramentas.

1. Selecionar **Experience Manager**.

1. No **Cloud Manager** cartão, clique em **Launch**

## Permissões baseadas em funções no Cloud Manager {#role-based-permissions}

| Permissão | Descrição | Proprietário da empresa | Gerenciador de implantação | Gerenciador de programas | Desenvolvedor |
|--- |--- |--- |--- |--- |--- |
| Adicionar programa<br>Editar programa | Adicionar um novo programa<br>Adicionar ou remover soluções ou complementos | x |  |  |  |
| Criar ambiente | Criar ambientes de produção+armazenamento temporário e desenvolvimento | x | x |  |  |
| Ambiente de atualização | Atualizar ambientes de produção+armazenamento temporário e desenvolvimento | x | x |  |  |
| Excluir ambiente de desenvolvimento | Excluir ambientes de desenvolvimento | x | x |  |  |
| Configuração de pipeline | Configurar e editar pipelines |  | x |  |  |
| Execução de pipeline | Iniciar pipelines | x | x |  |  |
| Execução de pipeline | Rejeitar/aprovar falhas importantes de porta de qualidade de 3 níveis | x | x | x |  |
| Execução de pipeline | Fornecer aprovação ao vivo | x | x | x |  |
| Execução de pipeline | Agendar implantações de produção | x | x | x |  |
| Exclusão de pipeline | Permitir exclusão de pipeline |  | x |  |  |
| Cancelamento de execução | Cancelar execução atual |  | x |  |  |
| Gerar Token de Acesso Pessoal | Git de acesso |  | x |  | x |

>[!NOTE]
>
>Um usuário pode ser atribuído a várias funções. Por exemplo, atribuir ambos **Proprietário da empresa** e **Gerenciador de implantação** As funções de um usuário fornecem ao usuário a soma dessas permissões.

## Programas do Cloud Manager {#cloud-manager-programs}

Os programas do Cloud Manager representam conjuntos de ambientes do Cloud Manager que oferecem suporte a agrupamentos lógicos de iniciativas de negócios. Normalmente, esses agrupamentos correspondem a um Contrato de nível de serviço (SLA) adquirido. Por exemplo, um programa pode representar os recursos AEM para suportar o site público de uma organização, enquanto outro programa representa um DAM interno.


Veja isto [vídeo](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/programs.html) para saber mais sobre como usar os programas do Cloud Manager.

Um usuário pode criar um **Sandbox** ou **Produção** programa.

* A **programa de produção** é criado para permitir o tráfego ao vivo no momento adequado no futuro.
   * Consulte o documento [Introdução aos programas de produção](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-production-programs.md) para obter mais detalhes.

* A **programa sandbox** O é normalmente criado para servir os propósitos de treinamento, execução de demonstrações, ativação, criação de POCs ou para documentação.
   * Não se destina a transportar tráfego vivo e terá restrições que um programa de produção não irá.
   * Ele inclui Sites e Ativos e é fornecido automaticamente com uma ramificação Git que inclui código de amostra, um ambiente de desenvolvimento e um pipeline não relacionado à produção.
   * Consulte o documento [Introdução aos programas de sandbox](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-sandbox-programs.md) para obter mais detalhes.

## Ambientes do Cloud Manager {#cloud-manager-environments}

Seus ambientes de nuvem serão criados, acessados e visualizados pelo Cloud Manager. Esses ambientes podem ser ambientes de produção, armazenamento temporário ou desenvolvimento. Ambientes diferentes atendem a diferentes propósitos e podem ser usados com diferentes pipelines de CI/CD. Os ambientes são compostos de serviços como:

* [Serviços de criação de AEM](#author-services)
* [Serviços de publicação de AEM](#publish-services)
* [Serviços do Dispatcher](#dispatcher-services)

>[!TIP]
>
> Consulte o vídeo [Uso de ambientes do Adobe Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/environments.html) uma visão geral dos ambientes disponíveis.
>
>Consulte o documento [Gerenciar ambientes](/help/implementing/cloud-manager/manage-environments.md) para saber mais sobre tipos de ambiente que um usuário pode criar e como ele pode criar um ambiente.

### Serviço de criação de AEM {#author-services}

Um serviço de criação de AEM é incluído em ambientes em que o conteúdo do site e os ativos digitais são criados, gerenciados e atualizados. Normalmente, somente os usuários internos têm acesso ao serviço de criação e ele é mantido atrás de uma tela de logon. O serviço de criação atua como um ambiente de criação e visualização.

### Serviço de publicação de AEM {#publish-services}

Um serviço de publicação de AEM está incluído em ambientes que hospedam a experiência do usuário final, como um site. Esse é o serviço que os visitantes do site visualizarão e interagirão. Normalmente, o serviço de publicação está disponível publicamente.

### AEM Serviço Dispatcher {#dispatcher-services}

O dispatcher é um `Apache HTTP Web server` módulo que fornece uma camada de segurança e desempenho que fica na frente do serviço de publicação de AEM.
