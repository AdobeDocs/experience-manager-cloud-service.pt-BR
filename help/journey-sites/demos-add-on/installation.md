---
title: Entender a instalação do complemento de demonstração de referência
description: Saiba mais sobre o Cloud Manager e como ele é usado para instalar o complemento.
exl-id: 9418aac6-a8c4-43f7-b329-b02149fe2d53
feature: Onboarding
role: Admin, User, Developer
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '941'
ht-degree: 93%

---

# Entender a instalação do complemento de demonstração de referência {#understand-installation}

Saiba mais sobre o Cloud Manager e como ele é usado para instalar o complemento.

>[!TIP]
>
>Se já tiver experiência com o Cloud Manager ou quiser ir diretamente para a configuração e uso do complemento, pode pular para [Criar um programa e um pipeline](create-program.md)
>
>Se quiser saber como o Cloud Manager e o AEM trabalham juntos para criar os ambientes de demonstração, bem como configurar e usar os seus próprios, continue lendo o presente documento.

## Objetivo {#objective}

Este documento ajuda a entender como funciona o processo de instalação do Complemento de demonstrações de referência, ilustrando como as diferentes partes funcionam juntas. Depois de ler, você deverá:

* Ter uma compreensão básica do Cloud Manager.
* Entender como os pipelines entregam conteúdo e configuração ao AEM.
* Veja como os modelos podem criar novos sites pré-preenchidos com conteúdo de demonstração com apenas alguns cliques.

Este documento se concentra em entender essas partes fundamentais do Complemento de demonstrações de referência do AEM antes de passar para a próxima etapa da jornada, onde você inicia a instalação.

Embora seja recomendável prosseguir nessa jornada, se já tiver experiência com o Cloud Manager ou quiser ir diretamente para a configuração e uso do complemento, pode pular para [Criar um programa e um pipeline](create-program.md).

## Função de responsabilidade {#responsible-role}

Essa jornada se aplica a administradores de sistemas que são membros da função **Proprietário da empresa** no Cloud Manager de sua organização.

## Requisitos e pré-requisitos {#requirements-prerequisites}

Existem alguns requisitos mínimos cujo o aprendizado é necessário antes de começar a usar o Complemento de demonstrações de referência.

### Conhecimento {#knowledge}

* Conhecimento básico do Cloud Manager

### Ferramentas {#tools}

* Ser membro da função **Proprietário da empresa** no Cloud Manager de sua organização

## Noções básicas sobre o Cloud Manager {#cloud-manager}

O Cloud Manager é um componente essencial do AEM as a Cloud Service e serve como ponto de entrada único para a plataforma.

O Cloud Manager é usado para administrar os recursos de nuvem que dão suporte aos Projetos do AEM, incluindo os ambientes e as ferramentas necessárias. Para os fins dessa jornada, não é necessário compreender completamente o Cloud Manager. No entanto, ainda é necessário conhecer alguns conceitos básicos.

>[!TIP]
>
>Se quiser conhecer o Cloud Manager em detalhes, consulte a seção [Recursos adicionais](#additional-resources) deste artigo e obtenha links para mais informações.

### Programas {#programs}

Ao fazer logon no Cloud Manager, você terá acesso a um ou mais **programas**. Um programa pode ser definido de várias maneiras diferentes, mas é mais fácil pensar nele como associado aos sites e experiências vinculados à identidade de uma marca.

Se você fizer logon no Cloud Manager representando a **WKND Travel and Adventure Enterprises**, pode criar um programa **WKND Nightlife** e um programa **WKND Backyard Projects**. Ambos os programas teriam ambientes do AEM para gerenciar seus sites associados.

### Sandboxes {#sandboxes}

Os programas podem ser de produção ou de sandbox.

* **Um programa de produção** é criado para eventualmente permitir o tráfego ativo quando o programa estiver pronto para entrar no ar.
* **Um programa de sandbox** é criado para treinamento, execução de demonstrações, capacitação, POCs e outros, e não se destina à tráfego ativo.

Para instalar o Complemento de demonstrações de referência do AEM, crie um programa de sandbox.

>[!NOTE]
>
>O Complemento de demonstrações de referência do AEM só está disponível em programas de sandbox.

## Fluxo de instalação e uso {#installation-flow}

Agora que você compreende alguns conceitos fundamentais sobre o Cloud Manager, a instalação do Complemento de demonstrações de referência do AEM é conceitualmente simples.

1. Faça logon no Cloud Manager.
1. Crie um novo programa de sandbox do AEM, ativando o Complemento de demonstrações de referência do AEM como uma opção para esse programa.
1. O conteúdo e a configuração da demonstração são implantados no programa. O conteúdo da demonstração contém:
   * Modelos de site usados para criar vários AEM Sites usando recursos do AEM, pré-preenchidos com exemplos de práticas recomendadas.
   * Ferramentas de configuração para gerenciar o conteúdo de demonstração.
1. Faça logon no AEM no novo programa sandbox e use a ferramenta de criação rápida de sites para criar sites de demonstração com base nos modelos.
1. Use as ferramentas de configuração para gerenciar esses sites de demonstração e modelos, incluindo a exclusão deles quando não forem mais necessários.

## Modelos de site do AEM {#site-templates}

Os Modelos de site do AEM são pacotes que contêm conteúdo e estrutura predefinidos para um site. Os modelos de site podem ser personalizados para atender às necessidades de projetos específicos para que, quando administradores do AEM criarem novos sites, possam escolher entre modelos que se aplicam a seus casos de negócios.

O Complemento de demonstrações de referência do AEM inclui vários modelos para atender diversas necessidades de teste e demonstração. Depois de criar seu programa e implantar o pipeline para instalar o complemento, é possível fazer logon no AEM e criar sites com base em vários modelos de demonstração

## O que vem a seguir {#what-is-next}

Agora que concluiu esta parte da jornada do complemento de demonstrações de referência do AEM, você deve:

* Ter uma compreensão básica do Cloud Manager.
* Entender como os pipelines entregam conteúdo e configuração ao AEM.
* Veja como os modelos podem criar novos sites pré-preenchidos com conteúdo de demonstração com apenas alguns cliques.

Desenvolva esse conhecimento e prossiga com sua jornada de Criação rápida de sites de AEM revisando [Criar um Programa e um Pipeline](create-program.md), onde você aprenderá a configurar um novo programa e pipeline para implantar o complemento.

## Recursos adicionais {#additional-resources}

Embora seja recomendável seguir para a próxima parte da jornada de criação rápida de sites revisando [Criar um Programa e um Pipeline](create-program.md), a seguir estão alguns recursos adicionais e opcionais. Esses recursos aprofundam os conceitos mencionados neste documento. No entanto, eles não são necessários para continuar a jornada.

* [Noções básicas sobre programas e tipos de programas](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/programs/program-types.html?lang=pt-BR) - Comece aqui para entender as diferenças entre os programas live e sandbox.
* [Modelos de site](/help/sites-cloud/administering/site-creation/site-templates.md) - Se quiser saber mais sobre a estrutura dos modelos de site e como eles são usados para criar sites, consulte este documento.
* [Documentação do Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/onboarding-concepts/cloud-manager-introduction.html?lang=pt_BR) - Se quiser obter mais detalhes sobre os recursos do Cloud Manager, consulte diretamente os documentos técnicos detalhados.
