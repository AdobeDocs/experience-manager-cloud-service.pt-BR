---
title: AEM Terminologia as a Cloud Service
description: Antes de entrar no AEMaaCS, é útil entender a terminologia do sistema e sua estrutura básica.
exl-id: d02776a7-836a-4894-a5d5-ae88cc7e4e76
source-git-commit: 097c17b37cc308dc906cd4af7dc7c5d51862bdfa
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 18%

---

# AEM Terminologia as a Cloud Service {#terminology}

Nesta parte do [jornada de integração,](overview.md) você aprenderá a terminologia de AEM as a Cloud Service e sua estrutura básica.

## Objetivo {#objective}

Agora que você entende o que levou ao processo de integração lendo o documento [Preparação de integração,](preparation.md) é útil entender a terminologia do sistema e sua estrutura básica antes de fazer logon.

AEM as a Cloud Service é uma ferramenta poderosa e flexível e para usar qualquer ferramenta que você deveria conhecer em sua organização, bem como a terminologia e a linguagem usadas para descrevê-la. Este documento resume alguns termos-chave que você precisa entender antes de começar a usar o sistema.

Após a leitura deste documento, você entenderá:

* As diferentes camadas que compõem o AEMaaCS.
* O básico do que cada camada faz.

## Estrutura do AEMaaCS {#structure}

Para efeitos desta jornada de integração, não é necessário um entendimento completo da estrutura AEM as a Cloud Service. Mas a familiaridade com os seguintes conceitos facilitará o acompanhamento posterior na jornada.

![Estrutura do Cloud Manager](/help/journey-sites/quick-site/assets/cloud-manager-structure.png)

* **LOCATÁRIO** - cada cliente recebe um locatário. Um locatário também é conhecido como uma organização IMS (mais sobre IMS posteriormente nesta jornada)
* **PROGRAMAS** - cada locatário tem um ou mais programas, que geralmente refletem as soluções licenciadas do cliente.
* **AMBIENTES** - cada programa tem vários ambientes, um de produção para conteúdo dinâmico, um para preparo e outro para fins de desenvolvimento.
* **REPOSITÓRIO** - Os ambientes têm um ou mais repositórios git, onde o aplicativo e o código front-end são mantidos.
* **FERRAMENTAS E FLUXOS DE TRABALHO** - pipelines gerenciam a implantação do código dos repositórios para os ambientes.

Geralmente, um exemplo é útil na contextualização dessa hierarquia.

* A WKND Travel and Adventure Enterprises pode ser um **locatário** que se concentra em mídias relacionadas a viagens.
* O locatário da WKND Travel and Adventure Enterprises pode ter dois **programas**:
   * Programa One Sites para a divisão da revista WKND
   * Um programa de ativos para a divisão de mídia WKND
* Os programas WKND Magazine e WKND Media teriam desenvolvimento, armazenamento temporário e produção **ambientes**.
* **Repositórios** são usados para manter o código personalizado e os aplicativos da WKND Magazine e WKND Media.
* Vários **ferramentas e fluxos de trabalho** trabalhe nos acordos de recompra para implantar código usando pipelines de CI/CD, registros de acesso, AEM de acesso, etc.

## O que vem a seguir {#what-is-next}

Agora que você concluiu esta parte da jornada de integração de AEM, deve entender:

* As diferentes camadas que compõem o AEMaaCS.
* O básico do que cada camada faz.

Aproveite esse conhecimento e continue sua jornada de integração de AEM ao ler o documento [Acesso ao Admin Console](admin-console.md), onde você aprenderá como acessar o console e verificar seu status como administrador do sistema.
