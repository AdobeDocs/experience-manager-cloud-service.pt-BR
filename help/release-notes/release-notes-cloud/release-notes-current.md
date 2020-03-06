---
title: Notas de versão da versão 2020.3.0
description: Notas de versão da versão 2020.3.0
translation-type: tm+mt
source-git-commit: bcbb50f467a0e3b3047e2bb872a8fe39a9f02a1a

---


# Release Notes for AEM as a Cloud Service 2020.3.0 {#release-notes}

A seção a seguir descreve as Notas de versão gerais do Experience Manager como um serviço da Cloud 2020.3.0.

## Cloud Manager {#cloud-manager}

A data de lançamento da versão 2020.3.0 do Cloud Manager é 5 de março de 2020.

Siga esta seção para saber mais sobre as novidades e as atualizações do Cloud Manager Versão 2020.3.0.

### Novidades {#what-is-new}

* O log da etapa de compilação agora está disponível enquanto a etapa de compilação está em execução.
* Algumas mensagens na página de detalhes de execução do pipeline foram editadas para maior clareza.

### Correções de erros {#bug-fixes}

* Não foi possível baixar os arquivos de log para as etapas de teste funcional personalizadas e do produto por meio da interface do usuário.
* Quando o repositório git de um programa do Serviço em nuvem não pôde ser criado, os usuários na função do Gerenciador de implantação às vezes não conseguiam se recuperar dessa falha.
* Certas atividades do usuário durante a criação de um programa sandbox podem causar falha na criação do programa antes da criação do pipeline de não-produção.
* A instância efêmera SonarQube usada na etapa de compilação falhou ocasionalmente ao iniciar dentro do tempo limite configurado.
* A criação simultânea de ambientes dev no mesmo programa do Cloud Service poderia encontrar uma condição em que apenas um pudesse ser criado com êxito.
* As notificações da Experience Cloud para programas do Cloud Service não foram recebidas de forma consistente.
* Em projetos específicos, os objetos *ResourceResolver devem ser sempre fechados* , gerando uma Exceção de Ponteiro Nulo; no entanto, tal não teve impacto na execução do gasoduto.

