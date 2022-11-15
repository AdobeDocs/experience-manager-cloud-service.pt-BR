---
title: Notas de versão do Cloud Manager no AEM as a Cloud Service versão 2020.3.0
description: Notas de versão do Cloud Manager no AEM as a Cloud Service versão 2020.3.0
feature: Release Information
exl-id: 2ff62ba5-a657-4739-b646-1e948332bf79
source-git-commit: 09d5d125840abb6d6cc5443816f3b2fe6602459f
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 100%

---

# Notas de versão do Cloud Manager no Adobe Experience Manager as a Cloud Service 2020.3.0 {#release-notes}

Esta página descreve as notas de versão do Cloud Manager no AEM as a Cloud Service 2020.3.0.

## Data de lançamento {#release-date}

A data de lançamento do Cloud Manager no AEM as a Cloud Service 2020.3.0 é 5 de março de 2020.

### Novidades {#what-is-new}

* O registro da etapa de build já está disponível, enquanto a etapa de build está em execução.
* Algumas das mensagens na página de detalhes de execução do pipeline foram editadas para maior clareza.

### Correções de erros  {#bug-fixes}

* Não foi possível baixar os arquivos de log para as etapas de teste funcional personalizadas e do produto por meio da interface do usuário.
* Quando ocorria uma falha na criação do repositório de git de um programa do Cloud Service, às vezes os usuários na função do Gerente de implantação não conseguiam se recuperar dessa falha.
* Certas atividades do usuário durante a criação de um programa sandbox podem causar falha na criação do programa, antes da criação do pipeline não relacionado à produção.
* Ocasionalmente, ocorria uma falha na instância efêmera SonarQube usada na etapa de build, ao iniciar dentro do tempo limite configurado.
* A criação simultânea de ambientes de desenvolvimento no mesmo programa de Cloud Service pode encontrar uma condição em que apenas um pode ser criado com sucesso.
* As notificações da Experience Cloud para programas do Cloud Service não eram recebidas constantemente.
* Em projetos específicos, os objetos *ResourceResolver devem ser sempre fechados*, gerando uma Exceção de Null Pointer. No entanto, isso não teve impacto na execução do pipeline.
