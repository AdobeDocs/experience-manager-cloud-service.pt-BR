---
title: Notas de versão do Cloud Manager 2023.8.0 no Adobe Experience Manager as a Cloud Service
description: Estas são as notas de versão do Cloud Manager 2023.8.0 no AEM as a Cloud Service.
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: d1640c14c796d7b7b6a7b236b38077e360559966
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 27%

---


# Notas de versão do Cloud Manager 2023.8.0 no Adobe Experience Manager as a Cloud Service {#release-notes}

Esta página documenta as notas de versão do Cloud Manager 2023.8.0 no AEM as a Cloud Service.

>[!NOTE]
>
>Consulte [esta página](/help/release-notes/release-notes-cloud/release-notes-current.md) para obter as notas de versão atuais do Adobe Experience Manager as a Cloud Service.

## Data de lançamento {#release-date}

A data de lançamento do Cloud Manager 2023.8.0 no AEM as a Cloud Service é 10 de agosto de 2023. A próxima versão está planejada para 7 de setembro de 2023.

## Novidades {#what-is-new}

* Ao configurar um conjunto de conteúdo para [copiar conteúdo,](/help/implementing/developing/tools/content-copy.md) [configurações sensíveis ao contexto](/help/implementing/developing/introduction/configurations.md) agora são permitidos em conjuntos de conteúdo na interface do usuário.
* Foram feitos aprimoramentos para melhorar a compreensão e a detecção de mensagens de erro na interface do usuário do Cloud Manager.

## Programa de restauração antecipada de conteúdo por autoatendimento {#early-adoption}

[Um novo recurso de restauração de conteúdo de autoatendimento](/help/operations/restore.md) O agora oferece restauração de backup por até sete dias e está disponível para usuários iniciais para fins de avaliação, apresentando:

* Restauração de backup point-in-time nas últimas 24 horas
* Restaurações por tempo fixo de até sete dias

Se você estiver interessado em testar esse novo recurso e compartilhar seu feedback, envie um email para `aemcs-restorefrombackup-adopter@adobe.com` do email associado à Adobe ID. Observação:

* O programa de adoção antecipada está limitado apenas a ambientes de desenvolvimento.
* A disponibilidade do programa de adoção antecipada é limitada.
* Esse recurso é para recuperação de conteúdo excluído acidentalmente e não se destina à recuperação de desastres.

## Correções de erros {#bug-fixes}

* A variável **Ambientes** O menu agora fecha depois de acionar o **[Copiar conteúdo](/help/implementing/developing/tools/content-copy.md)** modal.
* [Uma reexecução de pipeline](/help/implementing/cloud-manager/deploy-code.md#reexecute-deployment) não é mais permitida se a execução anterior não tiver uma `commitId` definido no estado da fase de compilação.
* Uma mensagem mais compreensível agora é exibida para erros raros quando um usuário clica em um pipeline na **Atividade** ou **Pipeline** telas.
* A variável `contentSetName` não estiver mais ausente nos logs e agora for fornecido nas entradas ao iniciar um [cópia de conteúdo](/help/implementing/developing/tools/content-copy.md) operação.
* Em determinadas circunstâncias raras, não é mais possível iniciar duas execuções a partir do mesmo pipeline, levando a um estado de &quot;paralisação&quot;.
* Quando um certificado expirar, os nomes de domínio e as listas de permissões de IP associados ao certificado não serão mais removidos do CDN.
   * Nesses casos, o site continuará acessível.
   * [](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md)A interface do Cloud Manager fornecerá avisos antecipados mais visíveis de que o certificado SSL está prestes a expirar.
* Um problema com o AEM perdendo o acesso a um endpoint de publicação foi corrigido em situações em que o Sites é adicionado como uma solução para um programa somente Assets.
