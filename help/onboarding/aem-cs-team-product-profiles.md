---
title: Perfis de produto e de equipe do AEM as a Cloud Service
description: Descubra como os perfis de produto e de equipe do AEM as a Cloud Service podem conceder e limitar o acesso às suas soluções licenciadas da Adobe.
exl-id: 7b1474c9-aca0-4354-8798-1abdcda2f6dd
feature: Onboarding
role: Admin, User, Developer
source-git-commit: 0ff50aa77711d70d372a1f43ad7336c39ab1167c
workflow-type: tm+mt
source-wordcount: '1821'
ht-degree: 27%

---


# Perfis de produto e de equipe do AEM as a Cloud Service {#product-profiles}

Descubra como os perfis de produto e de equipe do AEM as a Cloud Service podem conceder e limitar o acesso às suas soluções licenciadas da Adobe.

## Perfis de produto {#profiles}

Ao conceder ao usuário acesso a uma solução específica da Adobe, você pode não pretender conceder acesso total a ele. Os perfis de produto permitem que cada solução tenha seu próprio conjunto de permissões do usuário. Eles estão disponíveis e podem ser acessados por meio do [Admin Console](/help/journey-onboarding/admin-console.md).

A Adobe Admin Console tem uma hierarquia estruturada de produtos, instâncias de produtos e perfis de produtos, à qual os usuários internos de uma organização podem ser atribuídos como membros, fornecendo a eles acesso às soluções e aos recursos que foram licenciados.

<!-- Alexandru: Drafting for now 

Your AEM as a Cloud Service team members are added and assigned to one or more of the following product profiles via the Admin Console during onboarding.

* **AEM Administrators**: An AEM administrator is typically assigned to developers, in particular developers who need access to, for example, the development environments. The AEM administrator's product profile is used to grant administrator privileges in the associated AEM instance.

* **AEM Users**: AEM users are the users in your organization who use AEM as a Cloud Service generally to create content. These users need to access AEM to do their tasks. The AEM users product profile is typically assigned to an AEM content author who creates and reviews the content. This content can be of many types such as pages, assets, publications, and so on. The AEM users product profile shown below is assigned to these members.

![Product profiles](/help/onboarding/assets/admin-console-profiles.png) -->

## Perfis de produto e de equipe do AEM as a Cloud Service {#aem-product-profiles}

O AEM as a Cloud Service é uma oferta em nuvem totalmente nativa que fornece o AEM como serviço. Ele fornece o AEM de maneira nativa em nuvem, com novos atributos como sempre ativo, sempre atual, sempre seguro e sempre em escala. Ao mesmo tempo, mantém a principal proposta de valor do AEM na forma de uma plataforma personalizável para os clientes e permite que equipes de nível empresarial se integrem em seus procedimentos de desenvolvimento e entrega. Consulte [Introdução ao Adobe Experience Manager as a Cloud Service](/help/overview/introduction.md) para saber mais sobre o AEM as a Cloud Service.

### Instâncias de Produto no Nível da Organização {#org-level-product-instances}

>[!NOTE]
>
> Algumas instâncias de produto e perfis de produto descritos neste artigo podem aparecer somente para ambientes recém-criados. Um mecanismo futuro também permitirá que os ambientes existentes sejam atualizados.

Quando o Adobe processar o licenciamento de uma solução AEM pela primeira vez, duas Instâncias do produto serão exibidas no Adobe Admin Console, sob o Produto Adobe Experience Manager as a Cloud Service:

* **Nível de Organização AEM** - contém um ou mais Perfis de Produto que representam o acesso a recursos com escopo para todos os ambientes AEM, em vez de apenas para um único ambiente
* **Cloud Manager** - contém Perfis de Produto correspondentes a diferentes níveis de acesso aos recursos do Cloud Manager.

<!--
>[!NOTE]
>
>For existing programs, the AEM Org-Level Product Instance is created upon selecting the **Update product** profiles action for a given environment.
-->

![Instâncias de Produto no Nível da Organização](/help/onboarding/assets/orglevel.png)

Dentro da Instância de Produto do Nível da Organização AEM há um Perfil de Produto chamado AEM Org-Level Reporters, que não é usado no momento, mas pode ser no futuro para representar o acesso à recuperação de informações sobre licenças de produto do AEM.

Quando uma Solução de comunicação da Forms for licenciada, um perfil de produto correspondente também aparecerá na Instância de produto do nível da organização AEM.

![Perfil de Produto dos Repórteres](/help/onboarding/assets/org-level-reporters.png)

### Instâncias de produto no nível do ambiente e da camada {#environment-and-tier-level-product-instances}

Ao provisionar novos programas com um ou mais ambientes AEM, duas instâncias de produto serão exibidas por ambiente, contendo perfis de produto para criação e publicação, respectivamente.

![Instâncias do Produto Ambiente](/help/onboarding/assets/env-productinstances.png)

Abaixo estão os Perfis de produto em uma Instância de produto de autor, para uma organização que provisionou um ambiente em um programa que contém o AEM Sites:

![Instâncias de Produto do Sites](/help/onboarding/assets/sites-product-instances.png)

A tabela a seguir descreve uma lista dos Perfis de produto possíveis abaixo de uma Instância de produto específica do nível do ambiente.

<table style="table-layout:auto">
    <tr>
        <th>Instância do produto</th>
        <th>Convenção de nomeação</th>
        <th>Serviço padrão</th>
        <th>Descrição</th>
    </tr>
    <tr>
        <td>Autor do AEM</td>
        <td>Gerenciadores de conteúdo do AEM Sites - autor - Programa <code>id</code> - Ambiente <code>id</code></td>
        <td>Gerenciadores de conteúdo do AEM Sites</td>
        <td>
            <ul>
                <li>Destina-se ao acesso controlado aos recursos de criação do AEM Sites neste ambiente. Os usuários neste Perfil de produto serão membros do grupo AEM, autor de conteúdo do AEM Sites, que é criado automaticamente no AEM. As permissões do grupo AEM devem ser configuradas no AEM com o nível de acesso desejado.</li><br>
                <li>Se o serviço padrão permanecer selecionado
                    <ul>
                        <li>os usuários neste perfil de produto também serão membros do grupo AEM "AEM Sites Content Managers - Service".</li>
                      <!--  <li>users in this product profile will have access to AEM Sites Content Management API.</li>
                        <li>an Adobe Developer Console API OAuth S2S project containing AEM Sites Content Management API can optionally be scoped to this environment.</li>-->
                    </ul>
                </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td></td>
        <td>Administradores de AEM - Autor - Programa <code>id</code> - Ambiente <code>id</code></td>
        <td>Administradores de AEM</td>
        <td>
            <ul>
                <li>Destinado a acesso irrestrito aos recursos de autor e ambiente de publicação do AEM. Os usuários neste perfil de produto serão membros do grupo AEM, autor de Administradores de AEM, criado automaticamente no AEM.</li><br>
                <li>Se o serviço padrão permanecer selecionado
                    <ul>
                        <li>os usuários neste perfil de produto também serão membros do grupo "Administradores AEM - Serviço" AEM</li>
                    </ul>
                </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td></td>
        <td>Usuários AEM - autor - Programa <code>id</code> - Ambiente <code>id</code></td>
        <td>Usuários do AEM</td>
        <td>
            <ul>
                <li>Destinado a acesso muito limitado aos recursos do ambiente de autor do AEM. Os usuários neste perfil de produto serão membros do grupo AEM "Contribuidores" criado automaticamente no AEM</li><br>
                <li>Se o serviço padrão permanecer selecionado
                    <ul>
                        <li>usuários neste perfil de produto também serão membros do grupo "Usuários AEM - Serviço" AEM</li>
                    </ul>
                </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td></td>
        <td>Repórteres AEM - autor - Programa <code>id</code> - Meio Ambiente <code>id</code></td>
        <td>Repórteres AEM</td>
        <td>
            <ul>
                <li>Não é usado no momento, mas pode fornecer acesso a informações de relatórios sobre o nível de criação deste ambiente no futuro.</li>
            </ul>
        </td>
    </tr>
    <tr>
        <td></td>
        <td>AEM Assets Collaborator - autor - Programa <code>id</code> - Ambiente <code>id</code></td>
        <td>Usuários do AEM Assets Collaborator</td>
        <td>
        <ul>
                <li>Destina-se ao acesso somente leitura ao DAM. Os usuários neste perfil de produto serão membros do grupo AEM "Contribuidores" criado automaticamente no AEM.
                </li>
                <li>
                Além disso, fornece os direitos de Adobe Express para criar variações de ativos.
                </li>
          <ul>
    </tr>
    <tr>
        <td></td>
        <td>Usuário Avançado do AEM Assets - autor - Programa <code>id</code> - Ambiente <code>id</code></td>
        <td>Usuários avançados do AEM Assets</td>
<td>
        <ul>
                <li>Destina-se ao acesso somente leitura ao DAM. Os usuários neste perfil de produto serão membros do grupo AEM "Contribuidores" criado automaticamente no AEM.
                </li>
                <li>
                Além disso, fornece os direitos de Adobe Express para criar variações de ativos.
                </li>
          <ul>
</td>
    </tr>
    <tr>
        <td></td>
        <td>Gerenciadores de conteúdo do AEM Forms - autor - Programa <code>id</code> - Ambiente <code>id</code></td>
        <td>Gerenciadores de conteúdo do AEM Forms</td>
        <td>
            <ul>
                <li>Destina-se ao acesso controlado aos recursos de criação do AEM Forms neste ambiente. Os usuários neste Perfil de produto serão membros do grupo AEM de usuários de formulários do AEM Forms, que é criado automaticamente no AEM.</li><br>
                <li>Se o serviço padrão permanecer selecionado
                    <ul>
                        <li>os usuários neste perfil de produto também serão membros do grupo AEM "AEM Forms Content Managers - Service".</li>
                    </ul>
                </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td></td>
        <td>Desenvolvedores do AEM Forms - autor - Programa <code>id</code> - Ambiente <code>id</code></td>
        <td>Desenvolvedores do AEM Forms</td>
        <td>
            <ul>
                <li>Destina-se ao acesso controlado aos recursos de criação do AEM Forms neste ambiente. Os usuários neste Perfil de produto serão membros do grupo AEM de usuários avançados do AEM Forms Forms, que é criado automaticamente no AEM. Esses usuários têm o direito de carregar XDPs e criar Modelos de dados de formulário, além de tarefas normais de criação de formulário.</li><br>
                <li>Se o serviço padrão permanecer selecionado
                    <ul>
                        <li>os usuários neste perfil de produto também serão membros do grupo AEM "Desenvolvedores do AEM Forms - Serviço".</li>
                    </ul>
                </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td></td>
        <td>Usuários do Serviço de Comunicações da AEM Forms - autor - Programa <code>id</code> - Ambiente <code>id</code></td>
        <td>Usuários do serviço de comunicações da AEM Forms</td>
        <td>
            <ul>
                <li>Destina-se ao acesso controlado aos recursos do AEM Forms Communications Services neste ambiente. Os usuários neste Perfil de produto serão membros do grupo AEM de usuários de formulários do AEM Forms, que é criado automaticamente no AEM.</li><br>
                <li>Se o serviço padrão permanecer selecionado
                    <ul>
                        <li>os usuários neste perfil de produto também serão membros do grupo AEM "Usuários do serviço de comunicações da AEM Forms - Serviço".</li>
                    </ul>
                </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td>Publicação no AEM</td>
        <td>Usuários AEM - publicar - Programa <code>id</code> - Ambiente <code>id</code></td>
        <td>Usuários do AEM</td>
        <td>
            <ul>
                <li>Destinado a acesso muito limitado aos recursos do ambiente de autor do AEM. Os usuários neste perfil de produto serão membros do grupo "contrib" AEM criado automaticamente no AEM</li><br>
                <li>Se o serviço padrão permanecer selecionado
                    <ul>
                        <li>os usuários neste perfil de produto também serão membros do grupo "Usuários AEM - Serviço" AEM.</li>
                    </ul>
                </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td></td>
        <td>Repórteres AEM - publicar - Programa <code>id</code> - Meio Ambiente <code>id</code></td>
        <td>Repórteres AEM</td>
        <td>
            <ul>
                <li>Não é usado no momento, mas pode fornecer acesso a informações de relatórios sobre o nível de publicação deste ambiente no futuro.</li>
            </ul>
        </td>
    </tr>
   <tr>
        <td></td>
        <td>Usuários do Serviço de Comunicações da AEM Forms - publicar - Programa <code>id</code> - Ambiente <code>id</code></td>
        <td>Usuários do serviço de comunicações da AEM Forms</td>
        <td>
            <ul>
                <li>Destina-se ao acesso controlado aos recursos do AEM Forms Communications Services neste ambiente. Os usuários neste Perfil de produto serão membros do grupo AEM de usuários de formulários do AEM Forms, que é criado automaticamente no AEM.</li><br>
                <li>Se o serviço padrão permanecer selecionado
                    <ul>
                        <li>os usuários neste perfil de produto também serão membros do grupo AEM "Usuários do serviço de comunicações da AEM Forms - Serviço".</li>
                    </ul>
                </li>
            </ul>
        </td>
    </tr>
</table>

Observe que cada Perfil de produto tem um Serviço de perfil de produto associado ativado por padrão. A menos que você tenha requisitos de acesso complexos, é recomendável manter apenas o Serviço padrão selecionado. Um grupo AEM correspondente será criado no AEM com a convenção de nomenclatura `<Product Profile Prefix> - Service` (por exemplo, **AEM Sites Content Managers - Service**) e os usuários nos perfis de produtos principais se tornarão automaticamente membros desse grupo AEM correspondente.

O grupo AEM no AEM associado ao serviço terá o conjunto agregado de usuários que existem em todos os Perfis de produto associados desse serviço para essa combinação de nível de ambiente.

![Serviços](/help/onboarding/assets/services.png)

A imagem a seguir representa os grupos AEM que refletem o perfil do produto e o serviço no nível do autor dos AEM Sites Content Managers.

![Mapeamento de Grupo para Serviço do AEM](/help/onboarding/assets/profile-to-service-mapping.png)

>[!NOTE]
>
>Todos os usuários atribuídos a um perfil de produto AEM as a Cloud Service têm acesso de somente leitura ao Cloud Manager por meio da função **Usuário do Cloud Manager**.
>
>Usuários com somente a função de **Usuário do Cloud Manager** pode fazer logon no Cloud Manager e navegar até os ambientes de autor do AEM (se existirem) usando as opções do menu **Programas**. A função de **Usuário do Cloud Manager** não é suficiente para acessar os detalhes do programa. Se tal acesso for necessário, os usuários devem receber funções adicionais pelo administrador do sistema.

>[!WARNING]
>
>O nome do perfil do produto **Administradores do AEM** não deve ser alterado. A alteração do perfil do produto **Administradores do AEM** removerá os direitos de administrador de todos os usuários atribuídos a esse perfil.

>[!TIP]
>
>* Para saber mais sobre perfis de produtos AEM, consulte [Atribuir perfis de produtos AEM](/help/journey-onboarding/assign-profiles-aem.md).
>* Para obter mais informações sobre o processo de integração, consulte a [jornada de integração](/help/journey-onboarding/overview.md).

## Perfis de produto do Cloud Manager {#cloud-manager-product-profiles}

O Cloud Manager tem perfis de produto pré-configurados que podem ser considerados permissões com base em função. O administrador do sistema é responsável pela configuração da sua equipe do Cloud Manager, atribuindo-a a esses perfis de produto.

>[!TIP]
>
>Consulte [Permissões com base em funções no Cloud Manager](/help/onboarding/cloud-manager-introduction.md#role-based-permissions) para obter mais detalhes.

Cada um dos perfis de produto tem permissões específicas associadas a eles.

* **Proprietário da empresa**
   * Nesta função, você tem permissão para adicionar um novo programa ou editar um programa, adicionar ou atualizar um ambiente, implantar código no ambiente AEM ou executar verificações de qualidade do código.
   * Esse usuário é responsável por definir KPIs, aprovar implantações de produção e neutralizar falhas de nível 3 importantes, quando necessário.
* **Gerente de implantação**
   * Nessa função, você tem permissão para adicionar ou atualizar um ambiente, executar pipelines e implantar código no ambiente AEM ou executar verificações de qualidade do código.
   * Esse usuário gerencia operações de implantação e usa o Cloud Manager para executar implantações de preparo/produção, editar os pipelines de CI/CD, aprovar falhas de nível 3 importantes quando necessário e acessar o repositório Git.
* **Desenvolvedor**
   * Nesta função, você tem permissão para gerar tokens de acesso pessoal para acessar o Git.
   * Esse usuário desenvolve e testa o código de aplicativo personalizado e usa principalmente o Cloud Manager para visualizar o status da implantação e acessar o repositório Git para confirmações de código.
* **Gerente de programas**
   * Nessa função, você tem permissão para agendar pipelines, substituir os quality gates (portais de qualidade) de três níveis e fornecer aprovação de produção.
   * Esse usuário usa o Cloud Manager para executar a configuração da equipe, revisar o status, visualizar KPIs e pode aprovar falhas de nível 3 importantes, quando necessário.

Um usuário pode ser atribuído a vários perfis de produto. Por exemplo, atribuir as funções **Proprietário da empresa** e **Gerente de implantação** a um usuário fornecerá a ele a soma dessas permissões.

A equipe do Cloud Manager incluirá pelo menos:

* Um **Proprietário da empresa**, que normalmente também é o administrador do sistema e deve ser a primeira pessoa a fazer logon e acessar o Cloud Manager
* Um **Gerente de implantação**
* Um **Desenvolvedor**

>[!NOTE]
>
>Para ter acesso ao AEM as a Cloud Service, os usuários devem pertencer a um de dois perfis de produto: `AEM Users` ou `AEM Administrators`. Não é suficiente ter permissões para administrar o Cloud Manager.

>[!TIP]
>
>* Para saber mais sobre perfis de produtos do Cloud Manager, consulte [Atribuição de membros da equipe aos perfis de produto do Cloud Manager](/help/journey-onboarding/assign-profiles-cloud-manager.md).
>* Para obter mais informações sobre o processo de integração, consulte a [jornada de integração](/help/journey-onboarding/overview.md).
