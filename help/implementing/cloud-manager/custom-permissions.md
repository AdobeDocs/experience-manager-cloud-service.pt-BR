---
title: Permissões personalizadas
description: Saiba como você pode usar permissões personalizadas para criar novos perfis de permissão personalizados com permissões configuráveis para restringir o acesso a programas, pipelines e ambientes para usuários do Cloud Managers.
exl-id: 167da985-7f19-45b3-90a3-884817907da2
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '1474'
ht-degree: 2%

---

# Permissões personalizadas {#custom-permissions}

Saiba como você pode usar permissões personalizadas para criar novos perfis de permissão personalizados com permissões configuráveis para restringir o acesso a programas, pipelines e ambientes para usuários do Cloud Managers.

>[!NOTE]
>
>Este recurso só está disponível para [programa de adoção antecipada.](/help/implementing/cloud-manager/release-notes/current.md#early-adoption)

## Introdução {#introduction}

O Cloud Manager tem um conjunto de funções predefinidas que controlam o acesso a vários recursos do Cloud Manager:

* Proprietário da empresa
* Gerenciador de programas
* Gerenciador de implantação
* Desenvolvedor

As permissões personalizadas permitem que os usuários criem novos perfis de permissão personalizados com permissões configuráveis para restringir o acesso de usuários do Cloud Managers a programas, pipelines e ambientes.

>[!TIP]
>
>Para obter detalhes sobre funções predefinidas, consulte o documento [Equipe as a Cloud Service e perfis de produto do AEM.](/help/onboarding/aem-cs-team-product-profiles.md)

## Uso de permissões personalizadas {#using}

Para criar e usar suas próprias permissões personalizadas, são necessárias três etapas:

1. [Crie um novo perfil de produto.](#create)
1. [Atribua permissões personalizadas ao novo perfil de produto.](#assign-permissions)
1. [Atribua usuários ao novo perfil de produto.](#assign-users)

Esta seção detalhará essas etapas. Talvez seja útil consultar a seção [Termos](#terms) e [Permissões configuráveis](#configurable-permissions) ao criar suas próprias permissões personalizadas.

>[!NOTE]
>
>Você deve ter direitos de administrador de produto no Admin Console para que o Adobe Experience Manager as a Cloud Service crie novos perfis e gerencie permissões para o Cloud Manager.

### Criar um novo perfil de produto {#create}

Você primeiro deve criar um perfil de produto antes de atribuir permissões personalizadas.

1. Faça logon no Cloud Manager, em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/)

1. Na página de aterrissagem do Cloud Manager, selecione a **Gerenciar acesso** botão

![Botão Gerenciar acesso](assets/manage-access.png)

1. Você será redirecionado para a **Produtos** guia do Admin Console, onde é possível gerenciar usuários e permissões do cloud manager. No Admin Console, selecione a variável **Novo perfil** botão.

![Botão Novo perfil](assets/admin-console-new-profile.png)

1. Forneça os detalhes gerais sobre o perfil.

   * **Nome do perfil do produto** - Um nome descritivo para o perfil
   * **Nome de exibição** - Um nome abreviado que será mostrado na interface do usuário (opções)
   * **Descrição** - Uma descrição informativa do perfil explicando sua finalidade (opcional)
   * **Notificar usuários por email** - Quando selecionado, os usuários serão notificados por email quando forem adicionados ou removidos deste perfil.

1. Selecionar **Salvar** quando concluído.

O novo perfil de produto é salvo e fica visível na lista de perfis de produto no Admin Console.

### Atribuir permissões personalizadas ao perfil {#assign-permissions}

Agora que você tem um novo perfil de produto, pode atribuir permissões personalizadas a ele.

1. Na Admin Console, selecione o nome da variável [novo perfil de produto recém-criado.](#create)

1. Na janela aberta, selecione a variável **Permissões** para exibir uma lista de permissões editáveis.

   ![Permissões editáveis](assets/permissions-tab.png)

1. Selecione o **Editar** link de uma permissão para editá-la.

1. A variável **Editar permissões** é aberta.
   * A permissão selecionada na etapa anterior é selecionada na coluna à esquerda.
   * Os itens de permissão disponíveis para atribuição para a permissão estão na coluna do meio rotulados **Permissão disponível** Itens.
   * Os itens de permissões atribuídas estão na coluna direita identificada **Itens de permissão incluídos**.

   ![Editar itens de permissão](assets/edit-permission-items.png)

1. Selecione o sinal de mais (`+`) ao lado do item de permissão para adicioná-lo à coluna **Itens de permissão incluídos**.

   * Selecione o `i` ícone ao lado de um item de permissão para saber mais sobre ele.

1. Selecione o **Adicionar tudo** na parte superior do **Permissões disponíveis** para adicionar todas as permissões.

1. Se o perfil tiver sempre todos os itens de permissões, considere usar o **Incluir automaticamente** opção.

   * **Ligado** - Todos os itens de permissões atuais e futuros itens de permissão serão movidos para Itens de permissão incluídos e, ao salvar, serão aplicáveis adequadamente.
   * **Desligado** - Todos os itens de permissão serão movidos de volta para os itens de permissão disponíveis e, ao salvar, serão aplicáveis adequadamente.

1. Selecionar **Salvar** quando terminar de definir os itens de permissão para o novo perfil de produto.

O novo perfil de produto foi salvo com as permissões personalizadas.

### Atribuir usuários às permissões personalizadas {#assign-users}

Agora é possível atribuir usuários ao novo perfil de produto criado com permissões personalizadas.

1. Na Admin Console, selecione o nome da variável [novo perfil de produto ao qual você acabou de atribuir permissões personalizadas.](#assign-permissions)

1. Na janela aberta, selecione a variável **Usuários** guia.

1. Selecione o **Adicionar usuários** e atribua os usuários ao novo perfil de produto com permissões personalizadas.

Consulte a seção **Adicionar usuários e grupos de usuários a um perfil de produto** do documento [Gerenciar perfis de produto para usuários corporativos](https://helpx.adobe.com/enterprise/using/manage-product-profiles.html) para obter mais detalhes sobre como usar o Admin Console.

## Permissões configuráveis {#configurable-permissions}

As seguintes permissões estão disponíveis para criar perfis personalizados.

| Permissão | Descrição |
|---|---|
| Criação de programa | Permitir que os usuários criem um programa |
| Acesso ao programa | Permitir que os usuários acessem programas |
| Editar programa | Permitir que os usuários editem programas |
| Criação de ambiente | Permitir que os usuários criem um ambiente |
| Edição de ambiente | Permitir que os usuários atualizem e editem ambientes |
| Leitura de logs de ambiente | Permitir que os usuários leiam os logs de ambiente |
| Criação de pipeline | Permitir que os usuários criem novos pipelines |
| Exclusão de pipeline | Permitir que os usuários excluam pipelines |
| Edição de pipeline | Permitir que os usuários editem pipelines |
| Aprovar/Rejeitar Implantações de Produção | Permitir que os usuários aprovem ou rejeitem uma etapa de implantação de produção |
| Cancelamento de execuções de pipeline | Permitir que os usuários cancelem execuções de pipeline |
| Início das execuções de pipeline | Permitir que os usuários iniciem novas execuções de pipeline |
| Substituir/Rejeitar Falhas de Métricas Importantes | Permitir que os usuários substituam/rejeitem falhas de métricas importantes |
| Programação de implantações de produção | Permitir que os usuários agendem uma etapa de implantação de produção |
| Acesso às informações do repositório | Permitir que os usuários acessem as informações do repositório e gerem a senha de acesso |

### Permissões no nível da organização {#organization-level}

As permissões no nível da organização se referem às permissões que são sempre fornecidas em todos os programas em uma organização.

As seguintes permissões são no nível da organização:

* **Criação de programa** - Essa permissão permite que os usuários criem um programa na organização.
* **Acesso às informações do repositório** Essa permissão de nível de locatário/organização permite que os usuários gerem nome de usuário, senha e URL do repositório para acessar e contribuir com o projeto do cliente.
   * O nome de usuário e a senha para acesso ao repositório serão comuns em todos os repositórios na organização, no entanto, o URL do repositório será exclusivo para cada programa.
   * Consulte [Acessar repositórios](/help/implementing/cloud-manager/managing-code/accessing-repos.md) para obter mais informações.

## Termos {#terms}

Os termos a seguir são usados na criação e no gerenciamento de permissões personalizadas e funções predefinidas.

| Termo | Descrição |
|---|---|
| Permissões predefinidas | Funções predefinidas como **Proprietário da empresa**, **Gerente de implantação** e assim por diante para controlar vários recursos do Cloud Manager. Para obter detalhes sobre funções predefinidas, consulte o documento [Equipe as a Cloud Service e perfis de produto do AEM.](/help/onboarding/aem-cs-team-product-profiles.md) |
| Permissões personalizadas | Recursos do Cloud Manager que permitem aos usuários criar perfis de permissão para definir funções para controlar os recursos compatíveis do Cloud Manager |
| Perfil de produto | Criado no Admin Console para gerenciar permissões configuráveis que serão aplicáveis a usuários que fazem parte do perfil de permissão |
| Permissão configurável | Permissões do Cloud Manager que podem ser configuradas no perfil de permissões |
| Item de permissão | Um recurso de programa, ambiente ou pipeline no qual uma permissão pode ser aplicada |

Os itens de permissão se referem ao escopo no qual a permissão será aplicada. Normalmente, será um dos seguintes.

| Tipo de item de permissão | Exemplo | Descrição |
|---|---|---|
| Organização | organização:companyA | Todos os recursos aplicáveis de uma organização. Um recurso pode ser um programa, ambiente ou pipeline. Se o usuário adicionar uma organização para qualquer permissão, todos os novos recursos nessa organização também terão essa permissão. |
| Programa | Programa A | Todos os recursos aplicáveis de um programa |
| Ambiente | Programa A : ambiente | Aplicável em um ambiente específico |
| Pipeline | Programa A : Pipeline | Aplicável em um pipeline específico |

## Limitações {#limitations}

Lembre-se das limitações a seguir ao usar permissões personalizadas.

* O perfil de permissões personalizadas também listará programas, ambientes e pipelines do AMS ao configurar as permissões.
* Recursos como programa, ambiente, pipeline e assim por diante, criados no Cloud Manager podem levar até dois minutos para serem exibidos no Admin Console para configuração de permissão.
* Em raros cenários em que o serviço de permissões personalizadas não responde, os perfis predefinidos ainda estão disponíveis e os usuários em perfis predefinidos ainda têm acesso apropriado.

## Perguntas frequentes {#faq}

### Quais perfis de permissão são perfis de permissão predefinidos?

* Proprietário da empresa
* Gerenciador de programas
* Gerenciador de implantação
* Desenvolvedor

Para obter detalhes sobre funções predefinidas, consulte [Equipe as a Cloud Service e perfis de produto do AEM.](/help/onboarding/aem-cs-team-product-profiles.md)

### O que acontece com os perfis de permissão predefinidos com a introdução a perfis personalizados?

Os perfis de produto padrão e as funções do Cloud Manager continuam a funcionar da mesma forma que antes.

### Posso editar perfis de permissão predefinidos?

Não, os perfis padrão não são editáveis. Não é possível adicionar ou remover permissões do perfil de permissão padrão. Você só pode adicionar ou remover usuários de perfis predefinidos.

### Devo excluir perfis de permissão predefinidos, já que os perfis personalizados estão disponíveis?

Os perfis de permissão predefinidos não devem ser excluídos do Admin Console.

### Posso adicionar usuários a vários perfis de permissão?

Sim, um usuário pode fazer parte de vários perfis, incluindo perfis de permissão predefinidos e personalizados. Quando um usuário é atribuído a vários perfis, as permissões combinadas de todos os perfis de permissão atribuídos ficam disponíveis para esse usuário.

### O que acontece se um usuário tiver permissão para editar um ambiente/pipeline, mas não tiver acesso a um programa que contenha o ambiente/pipeline?

Nesse caso, o usuário não poderá acessar o ambiente ou o pipeline se não tiver o **Acesso ao programa** permissões que contêm o ambiente ou pipeline.
