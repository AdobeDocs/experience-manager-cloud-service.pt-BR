---
title: Notas de versão do Cloud Manager no AEM como Cloud Service versão 2021.2.0
description: Notas de versão do Cloud Manager no AEM como Cloud Service versão 2021.2.0
translation-type: tm+mt
source-git-commit: bca0519b3f27ee21df41b2292d19e330c4aa5f7d
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 2%

---


# Notas de versão do Cloud Manager no Adobe Experience Manager como Cloud Service 2021.2.0 {#release-notes}

Esta página descreve as Notas de versão do Cloud Manager em AEM como Cloud Service 2021.2.0.

## Data de lançamento {#release-date}

A data de lançamento do Cloud Manager no AEM como Cloud Service 2021.2.0 é 11 de fevereiro de 2021.

## Cloud Manager {#cloud-manager}

### Novidades {#what-is-new}

* O pipeline de produção do Cloud Manager agora inclui o recurso de teste de interface personalizada.

* Os clientes do Assets agora poderão escolher quando e onde implantar sua instância do Brand Portal de forma automática por meio da interface do usuário do Cloud Manager. Para um programa regular (não caixa de proteção) com a solução Assets, o Portal de marcas agora pode ser provisionado no ambiente Production. O provisionamento pode ser feito somente uma vez no Production ambiente.

* O AEM Project Archetype usado em Projeto e criação de caixa de proteção foi atualizado para a versão 25.

* A lista de APIs obsoletas identificadas durante a digitalização de código foi refinada para incluir classes e métodos adicionais obsoletos nas versões mais recentes do Cloud Service SDK.

* O perfil SonarQube para o Gerenciador de nuvem foi atualizado para remover o Lula de regra Sonar:S2142. Isso não entrará em conflito com as verificações de Interrupção de Thread.

* A interface do usuário do Gerenciador de nuvem informará o usuário que pode não ser capaz de adicionar/atualizar temporariamente o nome do domínio porque o ambiente associado tem um pipeline em execução conectado a ele ou que está aguardando a etapa de aprovação.

* As propriedades definidas nos arquivos `pom.xml` do cliente prefixados com o sonar agora serão removidas dinamicamente para evitar falhas de compilação e verificação de qualidade.

* A interface do usuário do Gerenciador de nuvem informará o usuário que não pode selecionar temporariamente um certificado SSL se ele estiver sendo usado por um nome de Domínio que está sendo implantado no momento.


### Correções de erros {#bug-fixes}

* A correspondência do certificado SSL com um nome de domínio não faz mais distinção entre maiúsculas e minúsculas.

* A interface do usuário do Cloud Manager agora informará um usuário se as chaves privadas do certificado não atenderem ao limite de 2048 bits com uma mensagem de erro apropriada.

* A interface do usuário do Gerenciador de nuvem informará o usuário que não pode selecionar temporariamente um certificado SSL se ele estiver sendo usado por um nome de Domínio que está sendo implantado no momento.

* Em alguns casos, um problema interno pode fazer com que a exclusão de ambientes fique travada.

* Algumas falhas de pipeline foram relatadas incorretamente como erros de pipeline.
