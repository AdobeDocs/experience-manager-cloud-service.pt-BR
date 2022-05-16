---
title: Notas de versão do Cloud Manager AEM versão as a Cloud Service 2021.11.0
description: Estas são as notas de versão do Cloud Manager AEM as a Cloud Service versão 2021.11.0
feature: Release Information
exl-id: 98fd6d8a-ddc2-4f53-9dfc-d8e21af0c14d
source-git-commit: 4505f703754fa46cd746ae4794a3cab65cb19976
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Notas de versão do Cloud Manager no Adobe Experience Manager as a Cloud Service 2021.11.0 {#release-notes}

Esta página descreve as Notas de versão do Cloud Manager AEM as a Cloud Service 2021.11.0.

>[!NOTE]
>
>Consulte [esta página](/help/release-notes/release-notes-cloud/release-notes-current.md) para obter as notas de versão atuais do Adobe Experience Manager as a Cloud Service.

## Data de lançamento {#release-date}

A data de lançamento do Cloud Manager AEM as a Cloud Service 2021.11.0 é 4 de novembro de 2021.
A próxima versão está planejada para 16 de dezembro de 2021.

## Novidades {#what-is-new}

* Os usuários agora podem aproveitar os novos pipelines de front-end para implantar exclusivamente o código de front-end de forma acelerada. Consulte [Pipelines de front-end do Cloud Manager](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end) para saber mais.

   >[!IMPORTANT]
   >Você deve estar AEM versão `2021.10.5933.20211012T154732Z` para utilizar novos pipelines Front-End.

* A duração do pipeline de qualidade de código é significativamente reduzida ao executar a análise de código de uma maneira mais eficiente, sem a necessidade de criar uma imagem completa do AEM. Esta alteração será gradual durante as semanas que se seguem ao lançamento.

* A Git Commit ID agora será exibida nos detalhes de execução do pipeline, facilitando o rastreamento do código que foi criado.

* A Criação de programas agora está disponível por meio da API exposta publicamente.

* A Criação de ambiente agora está disponível por meio da API exposta publicamente.

* O cabeçalho de resposta `x-request-id` agora está visível na API Playground em [www.adobe.io](https://www.adobe.io/). Esse cabeçalho é útil ao enviar problemas de atendimento ao cliente para solução de problemas.

* Como usuário, vejo que o pipeline card com zero pipelines me fornece a orientação apropriada.

* Uma nova Página de atividade agora está disponível, em que atividades como pipeline e execuções de código podem ser visualizadas junto a seus detalhes associados. Com o tempo, as atividades listadas nesta página se expandirão em escopo junto com os detalhes fornecidos.

* Uma nova página Pipelines, com um popover de status ao passar o mouse para facilitar a visualização do resumo dos detalhes, está disponível. As execuções de pipeline podem ser visualizadas junto com seus detalhes associados.

* A API Editar pipeline agora oferece suporte à alteração do ambiente usado nas fases de implantação.

* Uma otimização no processo de varredura do OakPal foi introduzida para pacotes grandes.

* O arquivo CSV de problemas de qualidade agora contém o carimbo de data e hora de cada problema de qualidade.

## Correções de erros {#bug-fixes}

* Certas configurações de build não ortodoxas resultaram no armazenamento de arquivos desnecessários no cache de artefatos do Maven no pipeline, o que resultou em I/O de rede irrelevantes ao iniciar e parar o contêiner de compilação.

* A API do PATCH de pipeline falha se a fase de implantação não existir.

* A regra de qualidade `ClientlibProxyResourceCheck` gerava problemas de falso positivo quando havia bibliotecas de clientes com caminhos de base comuns.

* A mensagem de erro quando o número máximo de repositórios era atingido não especificava o motivo do erro.

* Em casos raros, os pipelines estavam falhando devido ao manuseio de novas tentativas inadequado de determinados códigos de resposta.
