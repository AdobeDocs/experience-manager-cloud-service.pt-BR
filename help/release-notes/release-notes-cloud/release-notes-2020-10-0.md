---
title: Notas de versão do  [!DNL Adobe Experience Manager] as a Cloud Service 2020.10.0.
description: '[!DNL Adobe Experience Manager] como notas de versão de Cloud Service para 2020.10.0.'
translation-type: tm+mt
source-git-commit: eb4a567e7ae2aac7260aae28e2b91b088e42f945
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 55%

---


# Notas de versão do [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

The following section outlines the general Release Notes for [!DNL Experience Manager] as a Cloud Service 2020.10.0.

## Cloud Manager {#cloud-manager}

### Data de lançamento {#release-date-cm}

A data de lançamento do Cloud Manager no AEM como Cloud Service 2020.10.0 é 2 de outubro de 2020.

### What is new in [!DNL Cloud Manager] {#what-is-new-cm}

* A página Ambientes foi reprojetada.

* A página de ambientes hibernados agora mostra um status discreto no Cloud Manager.

* O container de compilação do Cloud Manager agora oferece suporte à compilação de projetos usando Java 8 ou Java 11. O suporte para Java 11 é fornecido pelo sistema de cadeias de ferramentas Maven.

* O número de variáveis por ambiente aumentou para 200.

* A placa de Ambiente na página Visão geral agora lista até três ambientes. Os usuários podem selecionar o botão **Mostrar tudo** para navegar até a página de resumo do Ambiente para visualização de uma tabela com uma lista completa de ambientes.
Consulte [Visualizando Ambiente](/help/implementing/cloud-manager/manage-environments.md#viewing-environment) para obter mais detalhes.

### Correções de erros {#bug-fixes-cloud-manager}

* Devido a um erro, o link do Cloud Manager para o Console do desenvolvedor estava ativo antes dos ambientes serem totalmente criados.

* O link direto do Cloud Manager para o Console do desenvolvedor não exibia a opção de desibernar/hibernar para ambientes do Programa de sandbox.

* Os botões Cancelar e Salvar na página Edição de Pipeline de Não Produção nem sempre estavam visíveis.

* Certas falhas no processo de qualidade do código podiam resultar na geração incorreta do arquivo de log.

* Às vezes, o nome sugerido na criação de um novo programa retornava um duplicado de um nome de programa existente.

* Grandes logs de etapas de pipeline não podiam ser baixados consistentemente pela interface do usuário.

* A validação de nomes de ambientes apresentava um erro off-by-one.

* A página Ambientes às vezes mostrava segmentos do Publish e do Dispatcher sem que estivessem presentes.
