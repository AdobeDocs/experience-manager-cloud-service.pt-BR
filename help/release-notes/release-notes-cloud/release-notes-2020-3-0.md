---
title: Notas de versão para 2020.3.0
description: Notas de versão para 2020.3.0
translation-type: ht
source-git-commit: 27225bf4b918f39892ac9ab6f46deb97479f08e8

---


# Notas de versão para AEM as a Cloud Service 2020.3.0{#release-notes}

A seção a seguir descreve as Notas de versão gerais para Experience Manager as a Cloud Service 2020.3.0.


## Data de lançamento {#release-date}

A Data de lançamento do Experience Manager as a Cloud Service 2020.3.0 é 5 de março de 2020.

## Cloud Manager {#cloud-manager}

Siga esta seção para saber mais sobre as novidades e atualizações do Cloud Manager no AEM as a Cloud Service versão 2020.3.0.

### Novidades {#what-is-new}

* O registro da etapa de build já está disponível, enquanto a etapa de build está em execução.
* Algumas das mensagens na página de detalhes de execução do pipeline foram editadas para maior clareza.

### Correções de erros {#bug-fixes}

* Não foi possível baixar os arquivos de registro para as etapas de teste funcional personalizadas e do produto por meio da interface do usuário.
* Quando ocorria uma falha na criação do repositório de git de um programa do Cloud Service, às vezes os usuários na função do Gerenciador de implantação não conseguiam se recuperar dessa falha.
* Certas atividades do usuário durante a criação de um programa sandbox podem causar falha na criação do programa, antes da criação do pipeline não relacionado à produção.
* Ocasionalmente, ocorria uma falha na instância efêmera SonarQube usada na etapa de build, ao iniciar dentro do tempo limite configurado.
* A criação simultânea de ambientes de desenvolvimento no mesmo programa de Cloud Service pode encontrar uma condição em que apenas um pode ser criado com sucesso.
* As notificações da Experience Cloud para programas do Cloud Service não eram recebidas constantemente.
* Em projetos específicos, os objetos *ResourceResolver devem ser sempre fechados*, gerando uma Exceção de Null Pointer. No entanto, isso não teve impacto na execução do pipeline.

