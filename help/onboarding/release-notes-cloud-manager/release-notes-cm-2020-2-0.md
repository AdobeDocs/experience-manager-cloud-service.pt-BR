---
title: Notas de versão para 2020.2.0
description: Notas de versão para 2020.2.0
translation-type: tm+mt
source-git-commit: 6c719411ffa7bd814a515e302024ac433f173207
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 77%

---


# Release Notes for Cloud Manager in Adobe Experience Manager as a Cloud Service 2020.2.0 {#release-notes}

Esta página descreve as Notas de versão do Cloud Manager em AEM como Cloud Service 2020.2.0.

## Data de lançamento {#release-date}

A data de lançamento do Cloud Manager no AEM como Cloud Service 2020.2.0 é 13 de fevereiro de 2020.

## Cloud Manager {#cloud-manager}

### Novidades {#what-is-new}

* A versão do arquétipo do Adobe Experience Manager foi atualizada para a versão 22.
* Os ambientes de Preparo e Produção nos programas Sandbox/Demo já podem ser atualizados por meio da interface do usuário do Cloud Manager.
* Os URLs usados nas notificações da Experience Cloud foram otimizados para evitar um redirecionamento extra.
* As etapas de execução do pipeline que expiraram agora indicam isso explicitamente.
* A etapa de Verificação de código agora tem um registro que pode ser baixado.
* A planilha que contém os problemas detectados durante a verificação de código agora tem uma coluna com um link para a documentação da regra específica.

### Correções de erros {#bug-fixes}

* Às vezes, as políticas de segurança do navegador impediam que determinados botões na tela de execução do pipeline funcionassem corretamente.
* Os links Visão geral, Ambientes e Atividade às vezes ficavam disponíveis na página de aterrissagem do Cloud Manager.
* Certas falhas na implantação poderiam impedir erroneamente a criação de novos pipelines.
