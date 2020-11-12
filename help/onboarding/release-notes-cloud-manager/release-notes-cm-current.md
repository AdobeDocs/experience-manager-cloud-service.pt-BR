---
title: Notas de versão do Cloud Manager no AEM como Cloud Service versão 2020.11.0
description: Notas de versão do Cloud Manager no AEM como Cloud Service versão 2020.11.0
translation-type: tm+mt
source-git-commit: 65752c7c51538de27aa2b21695e8eb6c6695a5f5
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 4%

---


# Release Notes for Cloud Manager in Adobe Experience Manager as a Cloud Service 2020.11.0 {#release-notes}

Esta página descreve as Notas de versão do Cloud Manager em AEM como Cloud Service 2020.11.0.

## Data de lançamento {#release-date}

A data de lançamento do Cloud Manager no AEM como Cloud Service 2020.11.0 é 12 de novembro de 2020.

## Cloud Manager {#cloud-manager}

### Novidades {#what-is-new}

* Uma nova opção de menu **Logon localmente** agora está disponível para os usuários nas opções de menu ambientes nas páginas Cartão de Ambiente e Resumo de Ambientes.

* A guia **Aprendizagem** no Cloud Manager foi atualizada com novas imagens na interface do usuário

### Correções de erros {#bug-fixes-cloud-manager}

* O carregamento de dependências feitas antes da execução da compilação exigia o download de um plug-in Maven.
* O link do rodapé do Gerenciador de nuvem para selecionar um idioma agora navegará até o local correto.
* Às vezes, durante a digitalização do código, o processo SonarQube não era start. Isso será detectado automaticamente e uma tentativa de reinicialização será feita.
* Todos os pipelines de produção existentes serão ativados automaticamente com a etapa Auditoria de experiência.