---
title: Notas de versão do Cloud Manager no AEM as a Cloud Service versão 2020.11.0
description: Notas de versão do Cloud Manager no AEM as a Cloud Service versão 2020.11.0
feature: Release Information
translation-type: tm+mt
source-git-commit: 0f2b7176b44bb79bdcd1cecf6debf05bd652a1a1
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 5%

---


# Notas de versão do Cloud Manager no Adobe Experience Manager as a Cloud Service 2020.11.0 {#release-notes}

Esta página descreve as Notas de versão do Cloud Manager no AEM as a Cloud Service 2020.11.0.

## Data de lançamento {#release-date}

A data de lançamento do Cloud Manager no AEM as a Cloud Service 2020.11.0 é 12 de novembro de 2020.

## Cloud Manager {#cloud-manager}

### Novidades {#what-is-new}

* Uma nova opção de menu **Logon local** agora está disponível para os usuários nas opções do menu Ambiente nas páginas Cartão do ambiente e Resumo dos ambientes .
Consulte [Gerenciamento de ambientes](/help/implementing/cloud-manager/manage-environments.md#login-locally) para obter mais detalhes.

* A guia **Aprendizagem** no Cloud Manager foi atualizada com novas imagens na interface do usuário.

### Correções de erros {#bug-fixes-cloud-manager}

* O carregamento de dependências feitas antes da execução da build requer o download de um plug-in Maven.
* O link do rodapé do Cloud Manager para selecionar um idioma agora irá navegar até o local correto.
* Às vezes, durante a verificação do código, o processo SonarQube não era iniciado. Isso será detectado automaticamente e uma reinicialização tentada.
* Todos os pipelines de produção existentes serão ativados automaticamente com a etapa Auditoria de experiência.
