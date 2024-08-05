---
title: Notas de versão das Ferramentas de migração no AEM as a Cloud Service versão 2024.07
description: Notas de versão das Ferramentas de migração no AEM as a Cloud Service versão 2024.07.0
feature: Release Information
exl-id: 52709511-eab2-47a7-8bea-1b707cd568a1
role: Admin
source-git-commit: 4f01ca0076248442fe93161bbc8b98bffb64551b
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 8%

---

# Notas de versão das Ferramentas de migração no AEM as a Cloud Service versão 2024.07.0 {#release-notes}

Esta página descreve as Notas de versão das Ferramentas de migração no AEM as a Cloud Service 2024.07.0.

## Ferramenta Transferência de conteúdo {#ctt-release}

### Data de lançamento {#release-date-ctt}

A data de lançamento da ferramenta de transferência de conteúdo v3.0.16 é julho de 2024.

### Novidades {#what-is-new-ctt}

* Upload automático de logs de extração da CTT em caso de falhas.
* Os usuários agora podem executar a assimilação com êxito após a renovação da chave de extração.
* Adição de suporte para executar extrações CTT usando uma chave de acesso e uma chave secreta do Azure com o AzureDataStore.
* Os usuários agora receberão a mensagem de erro correta quando uma chave inválida for usada para criar um conjunto de migração.

## Analisador de práticas recomendadas {#bpa-release}

### Data de lançamento {#release-date-bpa}

A data de lançamento do Analisador de práticas recomendadas v2.1.50 é maio de 2024.

### Correções de erros {#bug-fixes-bpa}

* O Analisador de práticas recomendadas agora detecta todos os nós maiores que 16 MB
* Condição de raça que causa ocorrências esporádicas de achados NCC corrigidos.
