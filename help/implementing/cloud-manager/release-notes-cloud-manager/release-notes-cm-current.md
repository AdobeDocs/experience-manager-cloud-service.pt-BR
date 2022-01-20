---
title: Notas de versão do Cloud Manager AEM versão as a Cloud Service 2022.01.0
description: Estas são as notas de versão do Cloud Manager AEM as a Cloud Service versão 2022.01.0.
feature: Release Information
source-git-commit: 8da3976250c94d5858d07a83b0eb395fab9a3eda
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 2%

---


# Notas de versão do Cloud Manager no Adobe Experience Manager as a Cloud Service 2022.01.0 {#release-notes}

Esta página descreve as notas de versão do Cloud Manager AEM as a Cloud Service 2022.01.0.

>[!NOTE]
>
>Consulte [esta página](/help/release-notes/release-notes-cloud/release-notes-current.md) para obter as notas de versão atuais do Adobe Experience Manager as a Cloud Service.

## Data de lançamento {#release-date}

A data de lançamento do Cloud Manager AEM as a Cloud Service 2022.01.0 é 20 de janeiro de 2022. A próxima versão está planejada para 10 de fevereiro de 2022.

## Novidades {#what-is-new}

* O Cloud Manager [evite reconstruir a base de código quando detecta que a mesma confirmação de git é usada](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/setting-up-project.md#build-artifact-reuse) em várias execuções de pipeline de pilha completa.
* Agora, para acessar o log de ambiente AEM é necessário **Gerenciador de implantação** perfil do produto. Os usuários sem esse perfil verão um botão desativado na interface do usuário.
* A interface do usuário não permitirá a configuração de pipeline de front-end para um programa em que o Sites não está habilitado como uma solução.
* Após gerar uma senha git, a data de expiração será exibida.

## Correções de erros {#bug-fixes}

* Exceções de ponteiro nulo encontradas por algumas implantações de pipeline front-end foram corrigidas.
* As variáveis de ambiente agora podem ser adicionadas, atualizadas e excluídas quando um ambiente estiver executando uma versão desatualizada do AEM.
* A etapa de criação de imagem não será mais marcada como ERRO para pipelines que usaram a etapa agendada em determinados casos raros.
* Para programas com apenas um repositório, a tela de execução do pipeline agora exibirá o nome do repositório.
