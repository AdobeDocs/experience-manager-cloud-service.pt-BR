---
title: Terminologia do AEM as a Cloud Service
description: Antes de fazer logon no AEMaaCS, é útil compreender a terminologia do sistema e sua estrutura básica.
exl-id: d02776a7-836a-4894-a5d5-ae88cc7e4e76
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 81%

---

# Terminologia do AEM as a Cloud Service {#terminology}

Nesta parte do [integração do jornada,](overview.md) você aprende a terminologia do AEM as a Cloud Service e sua estrutura básica.

## Objetivo {#objective}

Agora que você entende o que precede o processo de integração lendo o documento [Preparação para a integração,](preparation.md) é útil compreender a terminologia do sistema e sua estrutura básica antes de fazer logon.

O AEM as a Cloud Service é uma ferramenta poderosa e flexível e, para usá-la, você precisa se familiarizar com a forma como ela está organizada, bem como com a terminologia e a linguagem usadas para descrevê-la. Este documento resume alguns termos-chave que você precisa compreender para começar a usar o sistema.

Depois de ler este documento, você deverá entender

* As diferentes camadas que compõem o AEMaaCS.
* As funções básicas de cada camada.

## Estrutura do AEMaaCS {#structure}

Para efeitos desta jornada de integração, não é necessário ter um entendimento completo da estrutura do AEM as a Cloud Service. Porém, estar familiarizado com os conceitos a seguir facilitará o acompanhamento da jornada.

![Estrutura do Cloud Manager](/help/journey-sites/quick-site/assets/cloud-manager-structure.png)

* **LOCATÁRIO** - cada cliente recebe um locatário. Um locatário também é conhecido como uma organização IMS (mais informações sobre IMS serão fornecidas posteriormente nesta jornada)
* **PROGRAMAS** - cada locatário tem um ou mais programas, que geralmente refletem as soluções licenciadas do cliente.
* **AMBIENTES** - cada programa tem vários ambientes, um de produção para conteúdo dinâmico, um para preparo e outro para fins de desenvolvimento.
* **REPOSITÓRIO** - Os ambientes têm um ou mais repositórios Git, nos quais o código do aplicativo e do front-end são mantidos.
* **FERRAMENTAS E FLUXOS DE TRABALHO** - pipelines gerenciam a implantação do código dos repositórios para os ambientes.

Geralmente, um exemplo é útil na contextualização dessa hierarquia.

* A WKND Travel and Adventure Enterprises pode ser um **locatário** que se concentra em mídias relacionadas a viagens.
* O locatário da WKND Travel and Adventure Enterprises pode ter dois **programas**:
   * Um programa do Sites para a divisão WKND Magazine
   * Um programa do Assets para a divisão WKND Media
* Os programas da WKND Magazine e WKND Media teriam **ambientes** de desenvolvimento, preparo e produção.
* **Repositórios** são usados para manter o código personalizado e os aplicativos da WKND Magazine e da WKND Media.
* Vários **ferramentas e fluxos de trabalho** trabalhe nos repositórios para implantar código usando pipelines de CI/CD, registros de acesso, acesso ao AEM e assim por diante.

## O que vem a seguir {#what-is-next}

Agora que concluiu esta parte da jornada de integração do AEM, você deve compreender:

* As diferentes camadas que compõem o AEMaaCS.
* As funções básicas de cada camada.

Desenvolva esse conhecimento e continue sua jornada de integração de AEM lendo o documento a seguir [Acessar o Admin Console](admin-console.md), onde você aprenderá a acessar o console e verificar seu status como administrador do sistema.
