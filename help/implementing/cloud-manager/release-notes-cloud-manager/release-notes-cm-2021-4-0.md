---
title: Notas de versão do Cloud Manager AEM versão as a Cloud Service 2021.4.0
description: Notas de versão do Cloud Manager AEM versão as a Cloud Service 2021.4.0
feature: Release Information
exl-id: a11ebe0e-2872-4fde-acc0-5babc6b01e1a
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 1%

---

# Notas de versão do Cloud Manager no Adobe Experience Manager as a Cloud Service 2021.4.0 {#release-notes}

Esta página descreve as Notas de versão do Cloud Manager AEM as a Cloud Service 2021.4.0.

## Data de lançamento {#release-date}

A Data de lançamento do Cloud Manager AEM as a Cloud Service 2021.4.0 é 8 de abril de 2021.
A próxima versão está planejada para 06 de maio de 2021.

### Novidades {#what-is-new-april}

* Atualizações da interface do usuário para os fluxos de trabalho Adicionar e editar programa para torná-lo mais intuitivo.

* Um usuário com as permissões necessárias agora pode enviar o ponto final de comércio por meio da interface do usuário do .

* Agora, as variáveis de ambiente podem ser enviadas para um serviço específico, seja de criação ou de publicação. Exige AEM versão `2021.03.5104.20210328T185548Z` ou superior.

* O **Gerenciar Git** é exibido no cartão Pipelines, mesmo quando nenhum pipeline foi configurado.

* A versão do arquétipo de projeto AEM usado pelo Cloud Manager foi atualizada para a versão 27.

* Os projetos no Console do desenvolvedor do Adobe I/O criados pelo Cloud Manager não podem mais ser editados ou excluídos involuntariamente.

* Quando um usuário adiciona um novo ambiente, ele é informado que, uma vez criado um ambiente, ele não pode ser movido para uma região diferente.

* Agora, as variáveis de ambiente podem ser enviadas para um serviço específico, seja de criação ou de publicação. Exige AEM versão 2021.03.5104.20210328T185548Z ou superior.

* A mensagem de erro ao iniciar um pipeline quando um ambiente foi excluído foi esclarecida.

* Pacotes OSGi fornecidos por projetos Eclipse agora são excluídos da regra `CQBP-84--dependencies`.

### Correções de erros {#bug-fixes-cm-april}

* Ao editar a página de auditoria da experiência de um pipeline, um caminho de entrada que começa com uma barra `( / )` O não resultará mais na interrupção da etapa no status pendente.

* Quando um novo pipeline de produção é criado, se nenhuma substituição de auditoria de conteúdo for adicionada pelo usuário, a página inicial padrão não foi auditada.

* Problemas para o `CloudServiceIncompatibleWorkflowProcess` tinha a severidade incorreta no arquivo CSV de problema baixável.

* O `Runmode` check estava produzindo falsos positivos em nós que não eram pastas.
