---
title: Notas de versão do Cloud Manager AEM versão as a Cloud Service 2021.11.0
description: Notas de versão do Cloud Manager AEM versão as a Cloud Service 2021.11.0
feature: Release Information
source-git-commit: 14042b45b14f2c5575fc96979579bb0aaffc9a17
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 2%

---

# Notas de versão do Cloud Manager no Adobe Experience Manager as a Cloud Service 2021.11.0 {#release-notes}

Esta página descreve as Notas de versão do Cloud Manager AEM as a Cloud Service 2021.11.0.

>[!NOTE]
>Para ver as Notas de versão atuais do Adobe Experience Manager as a Cloud Service, clique em [here](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=pt-BR).

## Data de lançamento {#release-date}

A data de lançamento do Cloud Manager AEM as a Cloud Service 2021.11.0 é 4 de novembro de 2021.
A próxima versão está planejada para 16 de dezembro de 2021.

### Novidades {#what-is-new}

* Os usuários agora podem aproveitar os novos pipelines do Front-End para implantar exclusivamente o código front-end de forma acelerada. Consulte [Pipelines de Front-End do Cloud Manager](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end) para saber mais.

   >[!IMPORTANT]
   >Você deve estar AEM versão `2021.10.5933.20211012T154732Z` para utilizar novos pipelines Front-End.

* A duração do pipeline de qualidade de código é significativamente reduzida ao executar a análise de código de uma maneira mais eficiente, sem a necessidade de criar uma imagem AEM inteira. Esta alteração será gradual durante as semanas que se seguem à libertação.

* A ID de confirmação de Git agora será exibida nos detalhes de execução do pipeline, facilitando o rastreamento do código que foi criado.

* A Criação de programas agora está disponível por meio da API exposta publicamente.

* A Criação de ambiente agora está disponível por meio da API exposta publicamente.

* O `x-request-id` o cabeçalho de resposta agora está visível no Reprodução da API em [www.adobe.io](https://www.adobe.io/). Esse cabeçalho é útil ao enviar problemas de atendimento ao cliente para solução de problemas.

* Como usuário, vejo que o pipeline card com zero pipelines me fornece a orientação apropriada.

* Uma nova Página de atividade agora está disponível, onde atividades como pipeline e execuções de código podem ser visualizadas junto com seus detalhes associados. Com o tempo, as atividades listadas nesta página se expanderão no escopo junto com os detalhes fornecidos.

* Uma nova página Pipelines com uma oferta de status on-hover para facilitar a visualização do resumo dos detalhes está disponível. As execuções de pipeline podem ser visualizadas junto com seus detalhes associados.

* A API Editar pipeline agora oferece suporte à alteração do ambiente usado nas fases de implantação.

* Uma otimização no processo de varredura do OakPal foi introduzida para pacotes grandes.

* O arquivo CSV do problema de qualidade agora contém o carimbo de data e hora de cada problema de qualidade.

### Correções de erros {#bug-fixes}

* Certas configurações de build não ortodoxas resultaram no armazenamento de arquivos desnecessários no cache de artefatos Maven do pipeline que resultaram em I/O de rede irrelevante ao iniciar e parar o contêiner de compilação.

* A API do PATCH de pipeline falha se a fase de implantação não existir.

* O `ClientlibProxyResourceCheck` a regra de qualidade gerava problemas de falso positivo quando havia bibliotecas de clientes com caminhos de base comuns.

* Mensagem de erro quando o número máximo de repositórios foi atingido não especificou o motivo do erro.

* Em casos raros, os pipelines estavam falhando devido ao tratamento inadequado de tentativas de determinados códigos de resposta.

