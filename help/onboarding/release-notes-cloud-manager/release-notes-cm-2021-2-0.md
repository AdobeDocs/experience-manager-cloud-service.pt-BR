---
title: Notas de versão do Cloud Manager no AEM as a Cloud Service versão 2021.2.0
description: Notas de versão do Cloud Manager no AEM as a Cloud Service versão 2021.2.0
translation-type: tm+mt
source-git-commit: 32557b3f25e4d4f4cb652f19cff4dae58638e07b
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 2%

---


# Notas de versão do Cloud Manager no Adobe Experience Manager as a Cloud Service 2021.2.0 {#release-notes}

Esta página descreve as Notas de versão do Cloud Manager no AEM as a Cloud Service 2021.2.0.

## Data de lançamento {#release-date}

A Data de lançamento do Cloud Manager no AEM as a Cloud Service 2021.2.0 é 11 de fevereiro de 2021.

## Cloud Manager {#cloud-manager}

### Novidades {#what-is-new}

* Os clientes do Assets agora poderão escolher quando e onde implantar sua instância do Brand Portal de forma automatizada por meio da interface do usuário do Cloud Manager. Para um programa regular (não sandbox) com a solução Assets, o Brand Portal agora pode ser provisionado no ambiente de produção. O provisionamento pode ser feito apenas uma vez no ambiente de Produção.

* O Arquétipo de projeto AEM usado na Criação de projeto e sandbox foi atualizado para a versão 25.

* A lista de APIs obsoletas identificadas durante a verificação de código foi refinada para incluir classes e métodos adicionais obsoletos nas versões mais recentes do SDK do Cloud Service.

* O perfil do SonarQube para o Cloud Manager foi atualizado para remover a regra do Sonar squid:S2142. Isso não entrará mais em conflito com as verificações de Interrupção de encadeamento.

* A interface do usuário do Cloud Manager informará o usuário que pode não ser temporariamente capaz de adicionar/atualizar o nome de domínio porque o ambiente associado tem um pipeline em execução anexado a ele ou que está aguardando a etapa de aprovação.

* As propriedades definidas nos arquivos `pom.xml` do cliente prefixados com o sonar agora serão removidas dinamicamente para evitar falhas de verificação de qualidade e criação.

* A interface do usuário do Cloud Manager informará o usuário que pode não ser temporariamente capaz de selecionar um certificado SSL se ele estiver sendo usado por um nome de domínio que está sendo implantado no momento.

* Foram adicionadas Regras de qualidade de código adicionais para cobrir problemas de compatibilidade de Cloud Service.

### Correções de erros {#bug-fixes}

* A correspondência do certificado SSL com um nome de domínio não diferencia maiúsculas de minúsculas.

* A interface do usuário do Cloud Manager agora informará um usuário se as chaves privadas do certificado não atenderem ao limite de 2048 bits com uma mensagem de erro apropriada.

* A interface do usuário do Cloud Manager informará o usuário que pode não ser temporariamente capaz de selecionar um certificado SSL se ele estiver sendo usado por um nome de domínio que está sendo implantado no momento.

* Em alguns casos, um problema interno pode causar a interrupção da exclusão do ambiente.

* Algumas falhas de pipeline eram relatadas incorretamente como erros de pipeline.
