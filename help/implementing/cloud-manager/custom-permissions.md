---
title: Permissões personalizadas
description: Saiba como você pode usar permissões personalizadas para criar perfis de permissão personalizados com permissões configuráveis para restringir o acesso a programas, pipelines e ambientes para usuários do Cloud Managers.
exl-id: 167da985-7f19-45b3-90a3-884817907da2
solution: Experience Manager
feature: Security, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1490'
ht-degree: 38%

---


# Permissões personalizadas {#custom-permissions}

Saiba como você pode usar permissões personalizadas para criar perfis de permissão personalizados com permissões configuráveis para restringir o acesso a programas, pipelines e ambientes para usuários do Cloud Managers.

## Introdução {#introduction}

O Cloud Manager tem um conjunto de funções predefinidas que controlam o acesso a vários recursos do Cloud Manager:

* Proprietário da empresa
* Gerenciador de programas
* Gerenciador de implantação
* Desenvolvedor

As permissões personalizadas permitem que os usuários criem perfis de permissão personalizados com permissões configuráveis para restringir o acesso dos usuários do Cloud Managers a programas, pipelines e ambientes.

>[!TIP]
>
>Para obter detalhes sobre funções predefinidas, consulte [Perfis de produto e de equipe do AEM as a Cloud Service](/help/onboarding/aem-cs-team-product-profiles.md).

## Uso de permissões personalizadas {#using}

Para criar e usar suas próprias permissões personalizadas, são necessárias três etapas:

1. [Criar um perfil de produto](#create).
1. [Atribuir permissões personalizadas ao perfil de produto](#assign-permissions).
1. [Atribuir usuários ao perfil de produto](#assign-users).

Esta seção detalha essas etapas. Talvez seja útil consultar as sessões [Termos](#terms) e [Permissões configuráveis](#configurable-permissions) ao criar permissões personalizadas.

>[!NOTE]
>
>Você deve ter direitos de administrador de produto no Admin Console para que o Adobe Experience Manager as a Cloud Service crie perfis e gerencie permissões para o Cloud Manager.

### Crie um novo perfil de produto {#create}

Primeiro, crie um perfil de produto ao qual você pode atribuir permissões personalizadas.

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/).

1. Na página de aterrissagem do Cloud Manager, selecione o botão **Gerenciar acesso**.

![Botão Gerenciar Acesso](assets/manage-access.png)

1. Você será redirecionado(a) para a guia **Produtos** do Admin Console, onde é possível gerenciar usuários e permissões do Cloud Manager. Na Admin Console, selecione o botão **Novo Perfil**.

![Botão Novo perfil](assets/admin-console-new-profile.png)

1. Forneça os detalhes gerais sobre o perfil.

   * **Nome do perfil de produto**: um nome descritivo para o perfil
   * **Nome de exibição** - Um nome abreviado que é mostrado na interface (opções)
   * **Descrição**: uma descrição informativa do perfil que explique sua finalidade (opcional)
   * **Notificar usuários por email** - Os usuários recebem uma notificação por email quando são adicionados ou removidos deste perfil.

1. Selecione **Salvar** ao concluir.

O novo perfil de produto é salvo e torna-se visível na lista de perfis de produto no Admin Console.

### Atribuir permissões personalizadas ao perfil {#assign-permissions}

Agora que você tem um novo perfil de produto, é possível atribuir permissões personalizadas.

1. Na Admin Console, selecione o nome do [novo perfil de produto que você criou](#create).

1. Na janela aberta, selecione a guia **Permissões** para exibir uma lista de permissões editáveis.

   ![Permissões editáveis](assets/permissions-tab.png)

1. Selecione o link **Editar** de uma permissão para poder editá-lo.

1. A janela **Editar Permissão** é aberta.
   * A permissão selecionada na etapa anterior é selecionada na coluna à esquerda.
   * Os itens de permissão disponíveis para atribuição estão na coluna do meio rotulada **Itens de permissão disponíveis**.
   * Os itens de permissões atribuídos estão na coluna à direita rotulada **Itens de permissão incluídos**.

   ![Editar itens de permissão](assets/edit-permission-items.png)

1. Selecione o ícone de adição (`+`) ao lado do item de permissão para adicioná-lo à coluna **Itens de Permissão Incluídos**.

   * Selecione o ícone `i` ao lado de um item de permissão se quiser saber mais sobre ele.

1. Selecione o botão **Adicionar tudo** na parte superior da coluna **Permissões Disponíveis** para que você possa adicionar todas as permissões.

1. Selecione **Salvar** quando terminar de definir os itens de permissão para o novo perfil de produto.

O novo perfil de produto é salvo com as permissões personalizadas.

### Atribuir usuários às permissões personalizadas {#assign-users}

Agora é possível atribuir usuários ao novo perfil de produto criado com permissões personalizadas.

1. Na Admin Console, selecione o nome do [novo perfil de produto ao qual você atribuiu permissões personalizadas](#assign-permissions).

1. Na janela aberta, selecione a guia **Usuários**.

1. Selecione o botão **Adicionar usuários** e atribua usuários ao novo perfil de produto com permissões personalizadas.

Consulte a seção **Adicionar usuários e grupos de usuários a um perfil de produto** do documento [Gerenciar perfis de produto para usuários corporativos](https://helpx.adobe.com/br/enterprise/using/manage-product-profiles.html) para obter mais detalhes sobre como usar o Admin Console.

## Permissões configuráveis {#configurable-permissions}

As seguintes permissões estão disponíveis para criar perfis personalizados.

| Permissão | Descrição |
| --- | --- |
| Criação de programa | Permitir que os usuários criem um programa. |
| Acesso ao programa | Permitir que os usuários acessem programas. |
| Editar programa | Permitir que os usuários editem programas. |
| Criação de ambiente | Permitir que os usuários criem um ambiente. |
| Edição de ambiente | Permitir que os usuários atualizem e editem ambientes. |
| Leitura de logs de ambiente | Permitir que os usuários leiam os logs de ambientes. |
| Gerenciamento de variáveis de ambiente | Permitir que os usuários criem/editem/excluam configurações de ambiente. |
| Criação de restauração de ambiente | Permitir que os usuários criem uma restauração de ambiente. |
| Redefinição do ambiente de desenvolvimento rápido | Permita que os usuários redefinam o RDE (Rapid Development Environment, ambiente de desenvolvimento rápido). |
| Gerenciamento de cópias de conteúdo | Permitir que os usuários gerenciem operações de cópia de conteúdo. |
| Criação de pipeline | Permitir que os usuários criem pipelines. |
| Exclusão de pipeline | Permitir que os usuários excluam pipelines. |
| Edição de pipeline | Permitir que os usuários editem pipelines. |
| Aprovar e rejeitar implantações de produção | Permitir que os usuários aprovem ou rejeitem uma etapa de implantação de produção. |
| Cancelamento de execuções de pipeline | Permitir que os usuários cancelem as execuções de pipeline. |
| Iniciar execuções de pipeline | Permitir que os usuários iniciem uma nova execução de pipeline. |
| Ignorar e rejeitar falhas de métrica importantes | Permitir que os usuários substituam/rejeitem falhas de métricas importantes. |
| Programação de implantações de produção | Permitir que os usuários agendem uma etapa de implantação de produção. |
| Acesso às informações do repositório | Permitir que os usuários acessem as informações do repositório e gerem uma senha de acesso. |
| Criar repositório | Permitir que os usuários criem repositórios Git. |
| Exclusão de repositório | Permitir que os usuários excluam repositórios Git. |
| Edição de repositório | Permitir que os usuários editem repositórios Git. |
| Geração de códigos do repositório | Permitir que os usuários gerem um projeto do arquétipo. |
| Gerenciar nome de domínio | Permitir que os usuários criem/editem/excluam nomes de domínio. |
| Gerenciar Incluo na lista de permissões IP | Permitir que os usuários criem/editem/excluam o incluo na lista de permissões IP e a associação do incluo na lista de permissões IP. |
| Gerenciamento de infraestrutura de rede | Permitir que os usuários criem/editem/excluam a infraestrutura de rede. |
| Gerenciamento de certificados SSL | Permitir que os usuários criem/editem/excluam certificados SSL. |
| Gerenciamento de usuários da subconta do New Relic | Permitir que os usuários leiam/editem usuários de subcontas do New Relic. |

### Permissões no nível da organização {#organization-level}

As permissões no nível da organização se referem às permissões que são sempre fornecidas em todos os programas em uma organização.

Estas são permissões no nível da organização:

* **Criação de programa** - Essa permissão permite que os usuários criem um programa na organização.
* **Acesso às Informações do Repositório** Essa permissão de nível de locatário/organização permite que os usuários gerem um nome de usuário, uma senha e uma URL de repositório para acessar e contribuir com um projeto do cliente.
   * O nome de usuário e a senha para acesso ao repositório são comuns em todos os repositórios na organização. No entanto, o URL do repositório é exclusivo para cada programa.
   * Consulte [Acessando repositórios](/help/implementing/cloud-manager/managing-code/accessing-repos.md) para obter mais informações.

## Termos {#terms}

Os termos a seguir são usados na criação e no gerenciamento de permissões personalizadas e funções predefinidas.

| Termo | Descrição |
| --- | --- |
| Permissões predefinidas | Funções predefinidas como **Proprietário da empresa** e **Gerente de implantação** para controlar vários recursos do Cloud Manager. Para obter detalhes sobre funções predefinidas, consulte [Perfis de produto e de equipe do AEM as a Cloud Service](/help/onboarding/aem-cs-team-product-profiles.md). |
| Permissões personalizadas | Os recursos do Cloud Manager permitem que os usuários criem perfis de permissão para definir funções que controlem os recursos compatíveis do Cloud Manager. |
| Perfil do produto | Criado no Admin Console para gerenciar permissões configuráveis aplicáveis a usuários que fazem parte do perfil de permissão. |
| Permissão configurável | Permissões do Cloud Manager que você pode configurar no perfil de permissões. |
| Item de permissão | Um programa, ambiente ou recurso de pipeline no qual uma permissão pode ser aplicada. |

Os itens de permissão se referem ao escopo no qual a permissão é aplicada. Normalmente, é um dos seguintes.

| Tipo de item de permissão | Exemplo | Descrição |
| --- | --- | --- |
| Organização | organização:companyA | Todos os recursos aplicáveis de uma organização. Um recurso pode ser um programa, ambiente ou pipeline. Se o usuário adicionar uma organização para qualquer permissão, todos os novos recursos dessa organização também possuirão essa permissão. |
| Programa | Programa A | Todos os recursos aplicáveis de um programa. |
| Ambiente | Programa A : ambiente | Aplicável a um ambiente específico. |
| Pipeline | Programa A : pipeline | Aplicável a um pipeline específico. |

## Notas de uso {#usage-notes}

* Um perfil de permissões personalizadas também lista programas, ambientes e pipelines do AMS ao configurar permissões.
* Recursos como programa, ambiente e pipeline que foram criados no Cloud Manager podem levar até dois minutos para serem exibidos no Admin Console para configuração de permissão.
* Em situações raras nas quais o serviço de permissões personalizadas não responde, os perfis predefinidos ainda estarão disponíveis, e os usuários desses perfis ainda possuirão o acesso apropriado.

## Perguntas frequentes {#faq}

### Quais são os perfis de permissão predefinidos?

* Proprietário da empresa
* Gerenciador de programas
* Gerenciador de implantação
* Desenvolvedor

Para obter detalhes sobre funções predefinidas, consulte [Perfis de produto e de equipe do AEM as a Cloud Service](/help/onboarding/aem-cs-team-product-profiles.md).

### O que acontece com os perfis de permissão predefinidos com a introdução dos perfis personalizados?

Os perfis de produtos padrão e as funções do Cloud Manager continuarão funcionando como antes.

### Posso editar os perfis de permissão predefinidos?

Não, os perfis padrão não são editáveis. Não é possível adicionar nem remover permissões do perfil de permissão padrão. Você só pode adicionar ou remover usuários de perfis predefinidos.

### Devo excluir os perfis de permissão predefinidos, já que os perfis personalizados estão disponíveis?

Não exclua perfis de permissão predefinidos da Admin Console.

### Posso adicionar usuários a vários perfis de permissão?

Sim, um usuário pode fazer parte de vários perfis, incluindo perfis de permissão predefinidos e personalizados. Quando um usuário é atribuído a vários perfis, as permissões combinadas de todos os perfis de permissão atribuídos são disponibilizadas para esse usuário.

### O que acontece se um usuário possuir permissão para editar um ambiente ou pipeline, mas não possuir acesso ao programa que contenha o ambiente ou pipeline?

Nesse caso, o usuário não poderá acessar o ambiente ou pipeline se não tiver as permissões **Acesso ao programa** que contenham o ambiente ou pipeline.
