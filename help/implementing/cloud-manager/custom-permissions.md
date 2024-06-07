---
title: Permissões personalizadas
description: Saiba como você pode usar permissões personalizadas para criar perfis de permissão personalizados com permissões configuráveis para restringir o acesso a programas, pipelines e ambientes para usuários do Cloud Managers.
exl-id: 167da985-7f19-45b3-90a3-884817907da2
solution: Experience Manager
feature: Security, Developing
role: Admin, Architect, Developer
source-git-commit: bc92ed7acefbbd906b0986ea0b6b96fa6d8422de
workflow-type: tm+mt
source-wordcount: '1515'
ht-degree: 41%

---


# Permissões personalizadas {#custom-permissions}

Saiba como você pode usar permissões personalizadas para criar perfis de permissão personalizados com permissões configuráveis para restringir o acesso a programas, pipelines e ambientes para usuários do Cloud Managers.

## Introdução {#introduction}

O Cloud Manager possui um conjunto de funções predefinidas que controlam o acesso a vários de seus recursos:

* Proprietário da empresa
* Gerenciador de programas
* Gerenciador de implantação
* Desenvolvedor

As permissões personalizadas permitem que os usuários criem perfis de permissão personalizados com permissões configuráveis para restringir o acesso dos usuários do Cloud Managers a programas, pipelines e ambientes.

>[!TIP]
>
>Para obter detalhes sobre funções predefinidas, consulte [Equipe as a Cloud Service do AEM e perfis de produto](/help/onboarding/aem-cs-team-product-profiles.md).

## Uso de permissões personalizadas {#using}

Para criar e usar suas próprias permissões personalizadas, são necessárias três etapas:

1. [Criar um perfil de produto.](#create)
1. [Atribua permissões personalizadas ao perfil do produto.](#assign-permissions)
1. [Atribuir usuários ao perfil de produto.](#assign-users)

Esta seção detalha essas etapas. Talvez seja útil ver [Termos](#terms) e [Permissões configuráveis](#configurable-permissions) ao criar suas próprias permissões personalizadas.

>[!NOTE]
>
>Você deve ter direitos de administrador de produto no Admin Console para que o Adobe Experience Manager as a Cloud Service crie perfis e gerencie permissões para o Cloud Manager.

### Crie um novo perfil de produto {#create}

Primeiro, crie um perfil de produto, antes de atribuir permissões personalizadas.

1. Faça logon no Cloud Manager, em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/).

1. Na página de aterrissagem do Cloud Manager, selecione a **Gerenciar acesso** botão.

![Botão Gerenciar acesso](assets/manage-access.png)

1. Você será redirecionado(a) para a guia **Produtos** do Admin Console, onde é possível gerenciar usuários e permissões do Cloud Manager. No Admin Console, selecione a variável **Novo perfil** botão.

![Botão Novo perfil](assets/admin-console-new-profile.png)

1. Forneça os detalhes gerais sobre o perfil.

   * **Nome do perfil de produto**: um nome descritivo para o perfil
   * **Nome de exibição** - Um nome abreviado que é mostrado na interface (opções)
   * **Descrição**: uma descrição informativa do perfil que explique sua finalidade (opcional)
   * **Notificar usuários por email** - Quando selecionada, os usuários são notificados por email quando são adicionados ou removidos deste perfil.

1. Selecionar **Salvar** quando concluído.

O novo perfil de produto é salvo e torna-se visível na lista de perfis de produto no Admin Console.

### Atribuir permissões personalizadas ao perfil {#assign-permissions}

Agora que você tem um novo perfil de produto, é possível atribuir permissões personalizadas.

1. Na Admin Console, selecione o nome da variável [novo perfil de produto que você criou](#create).

1. Na janela aberta, selecione a guia **Permissões** para exibir uma lista de permissões editáveis.

   ![Permissões editáveis](assets/permissions-tab.png)

1. Selecione o **Editar** link de uma permissão para poder editá-la.

1. A variável **Editar permissão** é aberta.
   * A permissão selecionada na etapa anterior é selecionada na coluna à esquerda.
   * Os itens de permissão disponíveis para atribuição estão na coluna do meio rotulada **Itens de permissão disponíveis**.
   * Os itens de permissões atribuídos estão na coluna à direita rotulada **Itens de permissão incluídos**.

   ![Editar itens de permissão](assets/edit-permission-items.png)

1. Selecione o sinal de mais (`+`) ao lado do item de permissão para que você possa adicioná-lo à coluna **Itens de permissão incluídos**.

   * Selecione o `i` ícone ao lado de um item de permissão se quiser saber mais sobre ele.

1. Selecione o **Adicionar tudo** na parte superior do **Permissões disponíveis** para que você possa adicionar todas as permissões.

1. Selecionar **Salvar** quando terminar de definir os itens de permissão para o novo perfil de produto.

O novo perfil de produto é salvo com as permissões personalizadas.

### Atribuir usuários às permissões personalizadas {#assign-users}

Agora é possível atribuir usuários ao novo perfil de produto criado com permissões personalizadas.

1. Na Admin Console, selecione o nome da variável [novo perfil de produto ao qual você atribuiu permissões personalizadas.](#assign-permissions)

1. Na janela aberta, selecione a guia **Usuários**.

1. Selecione o **Adicionar usuários** e atribua os usuários ao novo perfil de produto com permissões personalizadas.

Consulte a seção **Adicionar usuários e grupos de usuários a um perfil de produto** do documento [Gerenciar perfis de produto para usuários corporativos](https://helpx.adobe.com/br/enterprise/using/manage-product-profiles.html) para obter mais detalhes sobre como usar o Admin Console.

## Permissões configuráveis {#configurable-permissions}

As seguintes permissões estão disponíveis para criar perfis personalizados.

| Permissão | Descrição |
|---|---|
| Criação de programa | Permitir que os usuários criem um programa |
| Acesso ao programa | Permitir que usuários acessem programas |
| Editar programa | Permitir que usuários editem programas |
| Criação de ambiente | Permitir que os usuários criem um ambiente |
| Edição de ambiente | Permitir que os usuários atualizem e editem ambientes |
| Leitura de logs de ambiente | Permitir que os usuários leiam os logs de ambiente |
| Gerenciamento de variáveis de ambiente | Permitir que os usuários criem/editem/excluam configurações de ambiente |
| Criação de restauração de ambiente | Permitir que os usuários criem restauração de ambiente |
| Redefinição do ambiente de desenvolvimento rápido | Permitir que os usuários redefinam o ambiente de desenvolvimento rápido |
| Gerenciamento de cópias de conteúdo | Permitir que usuários gerenciem operações de cópia do conteúdo |
| Criação de pipeline | Permitir que os usuários criem pipelines |
| Exclusão de pipeline | Permitir que usuários excluam pipelines |
| Edição de pipeline | Permitir que usuários editem pipelines |
| Aprovar e rejeitar implantações de produção | Permitir que usuários aprovem ou rejeitem uma etapa de implantação de produção |
| Cancelamento de execuções de pipeline | Permitir que usuários cancelem execuções de pipeline |
| Iniciar execuções de pipeline | Permitir que os usuários iniciem uma nova execução de pipeline |
| Ignorar e rejeitar falhas de métrica importantes | Permitir que usuários ignorem ou rejeitem falhas de métrica importantes |
| Programação de implantações de produção | Permitir que usuários programem uma etapa de implantação de produção |
| Acesso às informações do repositório | Permitir que usuários acessem as informações do repositório e gerem a senha de acesso |
| Criar repositório | Permitir que os usuários criem repositórios Git |
| Exclusão de repositório | Permitir que usuários excluam repositórios Git |
| Edição de repositório | Permitir que usuários editem repositórios Git |
| Geração de códigos do repositório | Permitir que usuários gerem projetos a partir do arquétipo |
| Gerenciar nome de domínio | Permitir que os usuários criem/editem/excluam nomes de domínio |
| Gerenciar Inclui na lista de permissões IP | Permitir que os usuários criem/editem/excluam a vinculação de incluir na lista de permissões inclui na lista de permissões de IP e de IP |
| Gerenciamento de infraestrutura de rede | Permitir que os usuários criem/editem/excluam a infraestrutura de rede |
| Gerenciamento de certificados SSL | Permitir que os usuários criem/editem/excluam certificados SSL |
| Gerenciamento de usuários da subconta do New Relic | Permitir que os usuários leiam/editem usuários de subcontas do New Relic |

### Permissões no nível da organização {#organization-level}

As permissões no nível da organização se referem às permissões que são sempre fornecidas em todos os programas em uma organização.

Estas são permissões no nível da organização:

* **Criação de programa** - Essa permissão permite que os usuários criem um programa na organização.
* **Acesso às informações do repositório** Essa permissão de nível de locatário/organização permite que os usuários gerem nome de usuário, senha e URL do repositório para acessar e contribuir com o projeto do cliente.
   * O nome de usuário e a senha para acesso ao repositório são comuns em todos os repositórios na organização, no entanto, o URL do repositório é exclusivo para cada programa.
   * Consulte [Acessar repositórios](/help/implementing/cloud-manager/managing-code/accessing-repos.md) para obter mais informações.

## Termos {#terms}

Os termos a seguir são usados na criação e no gerenciamento de permissões personalizadas e funções predefinidas.

| Termo | Descrição |
|---|---|
| Permissões predefinidas | Funções predefinidas como **Proprietário da empresa** e **Gerente de implantação** para controlar vários recursos do Cloud Manager. Para obter detalhes sobre funções predefinidas, consulte [Equipe as a Cloud Service e perfis de produto do AEM.](/help/onboarding/aem-cs-team-product-profiles.md) |
| Permissões personalizadas | Os recursos do Cloud Manager permitem que os usuários criem perfis de permissão para definir funções que controlem os recursos compatíveis do Cloud Manager |
| Perfil do produto | Criado no Admin Console para gerenciar permissões configuráveis aplicáveis a usuários que fazem parte do perfil de permissão |
| Permissão configurável | Permissões do Cloud Manager que podem ser configuradas no perfil de permissão |
| Item de permissão | Um programa, ambiente ou recurso de pipeline no qual uma permissão pode ser aplicada |

Os itens de permissão se referem ao escopo no qual a permissão é aplicada. Normalmente, é uma das opções a seguir.

| Tipo de item de permissão | Exemplo | Descrição |
|---|---|---|
| Organização | organização:empresaA | Todos os recursos aplicáveis de uma organização. Um recurso pode ser um programa, ambiente ou pipeline. Se o usuário adicionar uma organização para qualquer permissão, todos os novos recursos nessa organização também terão essa permissão. |
| Programa | Programa A | Todos os recursos aplicáveis de um programa |
| Ambiente | Programa A : ambiente | Aplicável em um ambiente específico |
| Pipeline | Programa A : pipeline | Aplicável em um pipeline específico |

## Limitações {#limitations}

Lembre-se das limitações a seguir ao usar permissões personalizadas.

* O perfil de permissões personalizadas também lista programas, ambientes e pipelines do AMS ao configurar permissões.
* Recursos como programa, ambiente e pipeline que foram criados no Cloud Manager podem levar até dois minutos para serem exibidos no Admin Console para configuração de permissão.
* Em situações raras nas quais o serviço de permissões personalizadas não responde, os perfis predefinidos ainda estarão disponíveis e usuários desses perfis ainda possuirão o acesso apropriado.

## Perguntas frequentes {#faq}

### Quais são os perfis de permissão predefinidos?

* Proprietário da empresa
* Gerenciador de programas
* Gerenciador de implantação
* Desenvolvedor

Para obter detalhes sobre funções predefinidas, consulte [Equipe as a Cloud Service e perfis de produto do AEM.](/help/onboarding/aem-cs-team-product-profiles.md)

### O que acontece com os perfis de permissão predefinidos com a introdução dos perfis personalizados?

Os perfis de produto padrão e as funções do Cloud Manager continuarão funcionando da mesma forma que antes.

### Posso editar os perfis de permissão predefinidos?

Não, os perfis padrão não são editáveis. Não é possível adicionar ou remover permissões do perfil de permissões padrão. Você só pode adicionar ou remover usuários de perfis predefinidos.

### Devo excluir os perfis de permissão predefinidos, já que os perfis personalizados estão disponíveis?

Não exclua perfis de permissão predefinidos do Admin Console.

### Posso adicionar usuários a vários perfis de permissão?

Sim, um usuário pode fazer parte de vários perfis, incluindo perfis de permissão predefinidos e personalizados. Quando um usuário é atribuído a vários perfis, as permissões combinadas de todos os perfis de permissão atribuídos ficam disponíveis para esse usuário.

### O que acontece se um usuário possuir permissão para editar um ambiente ou pipeline, mas não possuir acesso ao programa que contenha o ambiente ou pipeline?

Nesse caso, o usuário não poderá acessar o ambiente ou o pipeline se não tiver o **Acesso ao programa** permissões que contêm o ambiente ou pipeline.
