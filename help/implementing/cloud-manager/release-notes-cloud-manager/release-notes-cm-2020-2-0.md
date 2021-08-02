---
title: Notas de versão do Cloud Manager no AEM as a Cloud Service versão 2020.2.0
description: Notas de versão do Cloud Manager no AEM as a Cloud Service versão 2020.2.0
feature: Informações da versão
exl-id: 3f3324d9-53db-458d-9523-2e0d5d6dc3f7
source-git-commit: 09d5d125840abb6d6cc5443816f3b2fe6602459f
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 67%

---

# Notas de versão do Cloud Manager no Adobe Experience Manager as a Cloud Service 2020.2.0 {#release-notes}

Esta página descreve as Notas de versão do Cloud Manager no AEM as a Cloud Service 2020.2.0.

## Data de lançamento {#release-date}

A Data de lançamento do Cloud Manager no AEM as a Cloud Service 2020.2.0 é 13 de fevereiro de 2020.

## Cloud Manager {#cloud-manager}

### Novidades {#what-is-new}

* A versão do arquétipo do Adobe Experience Manager foi atualizada para a versão 22.
* Os ambientes de Preparo e Produção nos programas Sandbox/Demo já podem ser atualizados por meio da interface do usuário do Cloud Manager.
* Os URLs usados nas notificações da Experience Cloud foram otimizados para evitar um redirecionamento extra.
* As etapas de execução do pipeline que expiraram agora indicam isso explicitamente.
* A etapa de Verificação de código agora tem um registro que pode ser baixado.
* A planilha que contém os problemas detectados durante a verificação de código agora tem uma coluna com um link para a documentação da regra específica.

### Correções de erros  {#bug-fixes}

* Às vezes, as políticas de segurança do navegador impediam que determinados botões na tela de execução do pipeline funcionassem corretamente.
* Os links Visão geral, Ambientes e Atividade às vezes ficavam disponíveis na página de aterrissagem do Cloud Manager.
* Certas falhas na implantação poderiam impedir erroneamente a criação de novos pipelines.
