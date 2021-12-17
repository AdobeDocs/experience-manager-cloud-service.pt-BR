---
title: Entender o Cloud Manager e o fluxo de trabalho de criação rápida de sites
description: Saiba mais sobre o Cloud Manager e como ele se vincula ao novo processo de Criação rápida de sites.
source-git-commit: 5e1a89743c5ac36635a139ada690849507813c30
workflow-type: tm+mt
source-wordcount: '1102'
ht-degree: 1%

---


# Entender o Cloud Manager e o fluxo de trabalho de criação rápida de sites {#understand-cloud-manager}

Saiba mais sobre o Cloud Manager e como ele se vincula ao novo processo de Criação rápida de sites.

>[!TIP]
>
>Se sua função for exclusivamente desenvolvimento front-end, você poderá ignorar o artigo [Recuperar informações de acesso do repositório Git](retrieve-access.md) nesta jornada.
>
>Se você for um administrador de AEM, um administrador do Cloud Manager, for responsável pelas tarefas de desenvolvimento front-end e de administrador, ou quiser simplesmente entender o processo end-to-end em AEM para desenvolvimento front-end, continue lendo o documento atual e continue nessa jornada.

## Objetivo {#objective}

Este documento ajuda você a entender como a ferramenta Criação de site AEM funciona e fornece uma visão geral do fluxo completo. Depois de ler, você deve:

* Entenda como o AEM Sites e o Cloud Manager trabalham juntos para facilitar o desenvolvimento de front-end
* Veja como a etapa de personalização de front-end é totalmente dissociada do AEM e não requer conhecimento AEM.

Este documento se concentra em entender essas partes fundamentais da solução de criação do Site Rápido antes de passar para a próxima etapa da jornada em que a configuração é iniciada.

Embora seja recomendável prosseguir com essa jornada passo a passo, se você já entender que o AEM Sites e o Cloud Manager trabalham juntos e quiser começar diretamente com a configuração, poderá [pule para a próxima etapa da jornada.](create-site.md)

## Função responsável {#responsible-role}

Essa parte da jornada se aplica ao administrador do AEM e ao administrador do Cloud Manager.

## Requisitos e pré-requisitos {#requirements-prerequisites}

Há vários requisitos antes de começar a criar e personalizar sites usando a ferramenta de Criação rápida de sites.

Como essa jornada se destina a desenvolvedores front-end, administradores e combinações de todas as funções, os requisitos para ambas são listados aqui.

É importante entender que para o desenvolvedor de front-end não é necessário acesso ou conhecimento AEM.

### Conhecimento {#knowledge}

| Conhecimento | Função |
|---|---|
| Compreensão das ferramentas e processos padrão de desenvolvimento front-end | Desenvolvedor front-end |
| Conhecimento básico sobre como criar e gerenciar sites no AEM | Administrador do AEM |
| Conhecimento básico do Cloud Manager | Administrador do Cloud Manager |

Para o desenvolvedor front-end, não é necessário conhecimento AEM.

### Ferramentas {#tools}

| Ferramenta | Função |
|---|---|
| Ambiente de desenvolvimento front-end preferido | Desenvolvedor front-end |
| npm | Desenvolvedor front-end |
| webpack | Desenvolvedor front-end |
| Acesso ao Cloud Manager | Administrador do Cloud Manager |
| Ser membro de **Proprietário da empresa** função no Cloud Manager | Administrador do Cloud Manager |
| Seja um administrador do Sys no Cloud Manager | Administrador do Cloud Manager |
| Acesso ao Admin Console | Administrador do Cloud Manager |
| Ser membro do **Gerenciador de implantação** função no Cloud Manager | Administrador do Cloud Manager |
| Ser membro do **Gerenciador de implantação** função no Cloud Manager | Desenvolvedor front-end |

Para o desenvolvedor de front-end, não é necessário usar AEM.

>[!TIP]
>
>Se você não estiver familiarizado com as funções do Cloud Manager e o gerenciamento de funções, consulte o documento Permissões baseadas em funções no [Recursos adicionais](#additional-resources) seção.

## Cloud Manager {#cloud-manager}

O Cloud Manager é um componente essencial AEM as a Cloud Service e serve como ponto de entrada único para a plataforma.

Para oferecer suporte a clientes com configurações de desenvolvimento corporativo, o AEM integra-se totalmente ao Cloud Manager e seus pipelines de CI/CD criados especificamente. A ferramenta Quick Site Creation estende esses recursos para oferecer suporte a pipelines de desenvolvimento front-end dedicados.

Para fins dessa jornada, não é necessário compreender completamente o Cloud Manager. Em um alto nível, o Cloud Manager consiste em vários níveis de estrutura.

![Estrutura do Cloud Manager](assets/cloud-manager-structure.png)

* **CONTENTOR** - Todos os clientes são provisionados com um locatário. **WKND Travel and Adventure Enterprises** pode ser um inquilino.
* **PROGRAMAS** - Cada locatário tem um ou mais programas. O **WKND Travel and Adventure Enterprises** o inquilino pode ter um **WKND Nightlife** e **Projetos da tarde da WKND** programa.
* **AMBIENTES** - Cada programa tem vários ambientes, como produção para conteúdo ao vivo e armazenamento temporário e desenvolvimento para fins de desenvolvimento. **WKND Nightlife** e **Projetos da tarde da WKND** programas teriam ambientes de desenvolvimento, estágio e produção.
* **REPOSITÓRIO** - Os ambientes têm repositórios git, onde o aplicativo e o código front-end são mantidos.
* **FERRAMENTAS E FLUXOS DE TRABALHO** - Pipelines gerencia a implantação do código dos repositórios para os ambientes.

## O fluxo de desenvolvimento front-end para a criação rápida de sites {#flow}

O fluxo geral é simples e intuitivo, mesmo que você ainda não tenha uma experiência extensa com o Cloud Manager.

1. O administrador do AEM entra em um ambiente AEM e cria um novo site usando um modelo de site.
1. O administrador do Cloud Manager cria um pipeline de front-end no Cloud Manager. O pipeline orquestra a implantação de código de um repositório Git para um ambiente AEM.
1. O administrador do AEM exporta o tema do site da instância AEM do programa e o fornece ao desenvolvedor front-end.
1. O administrador do Cloud Manager concede ao desenvolvedor de front-end acesso ao repositório Git de AEM, onde as personalizações podem ser confirmadas.
1. O desenvolvedor front-end recupera credenciais de acesso para acessar o git e o pipeline.
1. O desenvolvedor de front-end personaliza o tema, testando-o usando conteúdo real do site usando um proxy e, em seguida, confirma as alterações no repositório Git.
1. O desenvolvedor de front-end executa o pipeline para implantar as personalizações de tema no ambiente de produção do programa.

![Fluxo de criação rápida de site](assets/qsc-flow.png)

A principal vantagem de usar a ferramenta de Criação rápida de site é que o desenvolvedor front-end puro é responsável apenas pela personalização real. O desenvolvedor de front-end não tem interação com AEM ou precisa de conhecimento de AEM.

## O que vem a seguir {#what-is-next}

Agora que você concluiu esta parte da jornada de Criação de Site Rápido de AEM, é necessário:

* Entenda como o AEM Sites e o Cloud Manager trabalham juntos para facilitar o desenvolvimento de front-end
* Veja como a etapa de personalização de front-end é totalmente dissociada do AEM e não requer conhecimento AEM.

Crie com base nesse conhecimento e prossiga sua jornada de Criação de Site Rápido de AEM revisando o documento [Criar Site a partir de Modelo,](create-site.md) onde você aprenderá a criar rapidamente um novo site de AEM usando um modelo.

## Recursos adicionais {#additional-resources}

Embora seja recomendável seguir para a próxima parte da jornada de Criação Rápida de Site revisando o documento [Criar Site a partir de Modelo,](create-site.md) a seguir estão alguns recursos adicionais e opcionais que aprofundam alguns conceitos mencionados neste documento, mas não é necessário que eles continuem na jornada.

* [Documentação do Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/cloud-manager-introduction.html) - Se quiser obter mais detalhes sobre os recursos do Cloud Manager, consulte diretamente os documentos técnicos detalhados.
* [Permissões baseadas em função](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/requirements/role-based-permissions.html) - O Cloud Manager tem funções pré-configuradas com permissões apropriadas. Consulte este documento para obter detalhes sobre essas funções e como administrá-las.
* [npm](https://www.npmjs.com) - AEM temas usados para criar sites rapidamente se baseiam em npm.
* [webpack](https://webpack.js.org) - AEM temas usados para criar sites rapidamente dependem do webpack.
