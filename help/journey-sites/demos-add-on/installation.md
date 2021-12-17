---
title: Entender a instalação do complemento de demonstração de referência
description: Saiba mais sobre o Cloud Manager e como ele é usado para instalar o complemento.
source-git-commit: 52d65251744ce0ae5cf7a7e0a45b39d8fe78f13a
workflow-type: tm+mt
source-wordcount: '983'
ht-degree: 0%

---


# Entender a instalação do complemento de demonstração de referência {#understand-installation}

Saiba mais sobre o Cloud Manager e como ele é usado para instalar o complemento.

>[!TIP]
>
>Se você já tiver experiência com o Cloud Manager ou quiser ir diretamente para a configuração e uso do complemento, ignore para [Criar um programa e um pipeline](create-program.md)
>
>Se quiser saber como o Cloud Manager e o AEM trabalham juntos para criar seus ambientes de demonstração, bem como como configurar e usar seus próprios, continue lendo o documento atual.

## Objetivo {#objective}

Este documento ajuda você a entender como funciona o processo de instalação do Suplemento de Demonstrações de Referência, ilustrando como as diferentes partes funcionam juntas. Depois de ler, você deve:

* Ter uma compreensão básica do Cloud Manager.
* Entenda como os pipelines entregam conteúdo e configuração ao AEM.
* Veja como os modelos podem criar novos sites pré-preenchidos com conteúdo de demonstração com apenas alguns cliques.

Este documento se concentra em entender essas partes fundamentais do complemento Demonstração de Referência do AEM antes de passar para a próxima etapa da jornada em que você inicia a instalação.

Embora seja recomendável prosseguir com essa jornada passo a passo, se você já tiver experiência com o Cloud Manager ou quiser ir diretamente para a configuração e uso do complemento, ignore para [Criar um programa e um pipeline](create-program.md)

## Função responsável {#responsible-role}

Essa jornada se aplica a um administrador do sistema que é membro do **Proprietário da empresa** no Cloud Manager para sua organização.

## Requisitos e pré-requisitos {#requirements-prerequisites}

Existem requisitos mínimos para saber mais sobre e começar a usar o Complemento de Demonstrações de Referência.

### Conhecimento {#knowledge}

* Conhecimento básico do Cloud Manager

### Ferramentas {#tools}

* Ser membro de **Proprietário da empresa** função no Cloud Manager para sua organização

## Noções básicas sobre o Cloud Manager {#cloud-manager}

O Cloud Manager é um componente essencial AEM as a Cloud Service e serve como ponto de entrada único para a plataforma.

O Cloud Manager é usado para administrar os recursos de nuvem que oferecem suporte aos projetos da AEM, incluindo os ambientes e as ferramentas necessárias. Para fins dessa jornada, não é necessário compreender completamente o Cloud Manager. No entanto, você precisa conhecer alguns conceitos básicos.

>[!TIP]
>
>Se quiser saber mais sobre o Cloud Manager , consulte a seção [Recursos adicionais](#additional-resources) para obter links para mais informações.

### Programas {#programs}

Ao entrar no Cloud Manager, você tem acesso a um ou mais **programas**. Um programa pode ser definido de várias maneiras diferentes, mas é mais fácil pensar nele como associado aos sites e experiências associados à identidade de uma marca.

Se você entrar no Cloud Manager representando **WKND Travel and Adventure Enterprises**, você pode criar um **WKND Nightlife** e um **Projetos de quintais WKND** programa. Ambos os programas teriam ambientes AEM para gerenciar seus sites associados.

### Sandboxes {#sandboxes}

Os programas podem ser programas de produção ou programas de sandbox.

* **Um programa de produção** é criado para eventualmente permitir o tráfego ao vivo quando o programa estiver pronto para entrar no ar.
* **Um programa sandbox** O é criado para treinamento, execução de demonstrações, ativação, POCs etc. e não se destina ao tráfego ao vivo.

Para instalar o Suplemento de Demonstrações de Referência de AEM, será necessário criar um novo programa sandbox.

>[!NOTE]
>
>O Suplemento de Demonstrações de Referência de AEM só está disponível em programas sandbox.

## Fluxo de instalação e uso {#installation-flow}

Agora que você entende alguns conceitos fundamentais do Cloud Manager, a instalação do Suplemento de Demonstrações de Referência de AEM é conceitualmente simples.

1. Faça logon no Cloud Manager.
1. Crie um novo programa de AEM sandbox, ativando o AEM Reference Demos Add-On como uma opção para o programa.
1. O conteúdo e a configuração da demonstração são implantados no programa. O conteúdo da demonstração contém:
   * Modelos de site usados para criar vários sites de AEM usando recursos de AEM, pré-preenchidos com exemplos de práticas recomendadas.
   * Ferramentas de configuração para gerenciar o conteúdo de demonstração.
1. Faça logon em AEM no novo programa sandbox e use a ferramenta de criação rápida de sites e crie sites de demonstração com base nos modelos.
1. Use as ferramentas de configuração para gerenciar esses sites de demonstração e modelos, incluindo a exclusão deles quando não forem mais necessários.

## Modelos de site AEM {#site-templates}

AEM Modelos de site são pacotes que contêm conteúdo e estrutura predefinidos para um site. Os modelos de site podem ser personalizados para atender às necessidades de projetos específicos para que, quando AEM administradores criem novos sites, possam escolher entre modelos que se aplicam a seus casos de negócios.

O Suplemento de Demonstrações de Referência de AEM inclui vários modelos para várias necessidades de teste e demonstração. Depois de criar seu programa e implantar o pipeline para instalar o complemento, você pode fazer logon no AEM e criar sites com base em vários modelos de demonstração

## O que vem a seguir {#what-is-next}

Agora que você concluiu esta parte da jornada AEM Referência do complemento Demonstrações, você deve:

* Ter uma compreensão básica do Cloud Manager.
* Entenda como os pipelines entregam conteúdo e configuração ao AEM.
* Veja como os modelos podem criar novos sites pré-preenchidos com conteúdo de demonstração com apenas alguns cliques.

Crie com base nesse conhecimento e prossiga sua jornada de Criação de Site Rápido de AEM revisando o documento [Criar um programa e um pipeline,](create-program.md) onde você aprenderá a configurar um novo programa e pipeline para implantar o complemento.

## Recursos adicionais {#additional-resources}

Embora seja recomendável seguir para a próxima parte da jornada de Criação Rápida de Site revisando o documento [Criar um programa e um pipeline,](create-program.md) a seguir estão alguns recursos adicionais e opcionais que aprofundam alguns conceitos mencionados neste documento, mas não é necessário que eles continuem na jornada.

* [Noções básicas sobre programas e tipos de programas](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/understand-program-types.html) - Comece aqui para entender as diferenças entre os programas live e sandbox.
* [Modelos de site](/help/sites-cloud/administering/site-creation/site-templates.md) - Se você quiser saber mais sobre a estrutura dos modelos de site e como eles são usados para criar sites, consulte este documento.
* [Documentação do Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/cloud-manager-introduction.html) - Se quiser obter mais detalhes sobre os recursos do Cloud Manager, consulte diretamente os documentos técnicos detalhados.
