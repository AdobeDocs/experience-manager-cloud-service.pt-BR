---
title: Notas de versão do Cloud Manager no AEM as a Cloud Service versão 2021.4.0
description: Notas de versão do Cloud Manager no AEM as a Cloud Service versão 2021.4.0
feature: Informações da versão
exl-id: 456f945a-0320-4334-a407-ee2fcb1dbc0f
source-git-commit: 09d5d125840abb6d6cc5443816f3b2fe6602459f
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 2%

---

# Notas de versão do Cloud Manager no Adobe Experience Manager as a Cloud Service 2021.4.0 {#release-notes}

Esta página descreve as Notas de versão do Cloud Manager no AEM as a Cloud Service 2021.4.0.

## Data de lançamento {#release-date}

A Data de lançamento do Cloud Manager no AEM as a Cloud Service 2021.4.0 é 8 de abril de 2021.
A próxima versão está planejada para 06 de maio de 2021.

### Novidades {#what-is-new-april}

* Atualizações da interface do usuário para os fluxos de trabalho Adicionar e editar programa para torná-lo mais intuitivo.

* Um usuário com as permissões necessárias agora pode enviar o ponto final de comércio por meio da interface do usuário do .

* Agora, as variáveis de ambiente podem ser enviadas para um serviço específico, seja de criação ou de publicação. Exige AEM versão `2021.03.5104.20210328T185548Z` ou superior.

* O botão **Gerenciar Git** é exibido no cartão Pipelines mesmo quando nenhum pipeline foi configurado.

* A versão do arquétipo de projeto AEM usado pelo Cloud Manager foi atualizada para a versão 27.

* Os projetos no Console do desenvolvedor do Adobe I/O criados pelo Cloud Manager não podem mais ser editados ou excluídos involuntariamente.

* Quando um usuário adiciona um novo ambiente, ele é informado que, uma vez criado um ambiente, ele não pode ser movido para uma região diferente.

* Agora, as variáveis de ambiente podem ser enviadas para um serviço específico, seja de criação ou de publicação. Exige AEM versão 2021.03.5104.20210328T185548Z ou superior.

* A mensagem de erro ao iniciar um pipeline quando um ambiente foi excluído foi esclarecida.

* Pacotes OSGi fornecidos por projetos Eclipse agora são excluídos da regra `CQBP-84--dependencies`.

### Correções de erros {#bug-fixes-cm-april}

* Ao editar a página Auditoria de experiência de um pipeline, um caminho de entrada que começa com uma barra `( / )` não resultará mais na etapa presa no status pendente.

* Quando um novo pipeline de produção é criado, se nenhuma substituição de auditoria de conteúdo for adicionada pelo usuário, a página inicial padrão não foi auditada.

* Os problemas para `CloudServiceIncompatibleWorkflowProcess` tinham a severidade incorreta no arquivo CSV de problema baixável.

* A verificação `Runmode` estava produzindo falsos positivos em nós que não eram pastas.
