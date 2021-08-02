---
title: Notas de versão do Cloud Manager no AEM as a Cloud Service versão 2020.10.0
description: Notas de versão do Cloud Manager no AEM as a Cloud Service versão 2020.10.0
feature: Informações da versão
exl-id: 129d0dd8-3d6e-4cf0-b42e-5526f5cf0836
source-git-commit: 09d5d125840abb6d6cc5443816f3b2fe6602459f
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 48%

---

# Notas de versão do Cloud Manager no Adobe Experience Manager as a Cloud Service 2020.10.0 {#release-notes}

Esta página descreve as Notas de versão do Cloud Manager no AEM as a Cloud Service 2020.10.0.

## Data de lançamento {#release-date}

A Data de lançamento do Cloud Manager no AEM as a Cloud Service 2020.10.0 é 1 de outubro de 2020.

## Cloud Manager {#cloud-manager}

### Novidades {#what-is-new}

* A página Ambientes foi reprojetada.

* A página de ambientes hibernados agora mostra um status discreto no Cloud Manager.

* O contêiner de build do Cloud Manager agora é compatível com a compilação de projetos usando o Java 8 ou o Java 11. O suporte para o Java 11 é fornecido pelo sistema de cadeias de ferramentas Maven.

* O número de variáveis por ambiente aumentou para 200.

* O cartão Environment na página Visão geral agora listará até três ambientes. Os usuários podem selecionar o botão **Mostrar tudo** para navegar até a página de resumo do ambiente para exibir uma tabela com uma lista completa de ambientes.
Consulte [Ambiente de visualização](/help/implementing/cloud-manager/manage-environments.md#viewing-environment) para obter mais detalhes.


### Correções de erros {#bug-fixes-cloud-manager}

* Devido a um erro, o link do Cloud Manager para o Console do desenvolvedor estava ativo antes dos ambientes serem totalmente criados.

* O link direto do Cloud Manager para o Console do desenvolvedor não exibia a opção de desibernar/hibernar para ambientes do Programa de sandbox.

* Os botões Cancelar e Salvar na página Editar pipeline de não produção nem sempre estavam visíveis.

* Certas falhas no processo de qualidade do código podiam resultar na geração incorreta do arquivo de log.

* Às vezes, o nome sugerido na criação de um novo programa retornava um duplicado de um nome de programa existente.

* Grandes logs de etapas de pipeline não podiam ser baixados consistentemente pela interface do usuário.

* A validação de nomes de ambientes apresentava um erro off-by-one.

* A página Ambientes às vezes mostrava segmentos do Publish e do Dispatcher sem que estivessem presentes.
