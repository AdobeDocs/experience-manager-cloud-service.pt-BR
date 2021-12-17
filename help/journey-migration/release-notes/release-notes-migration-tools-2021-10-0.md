---
title: Notas de versão para Ferramentas de migração AEM versão as a Cloud Service 2021.10.0
description: Notas de versão para Ferramentas de migração AEM versão as a Cloud Service 2021.11.0
feature: Release Information
source-git-commit: a1c57a9d8165c9e67ce270a3f0c2ad80c75b7196
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 6%

---


# Notas de versão para Ferramentas de migração AEM versão as a Cloud Service 2021.10.0 {#release-notes}

Esta página descreve as Notas de versão para as Ferramentas de migração AEM as a Cloud Service 2021.10.0.

>[!NOTE]
>Para ver as Notas de versão atuais do Adobe Experience Manager as a Cloud Service, clique em [here](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=pt-BR).

## Cloud Acceleration Manager {#cam-release}

### Data de lançamento {#release-date-cam}

A data de lançamento do Cloud Acceleration Manager é 25 de outubro de 2021.

### Novidades {#what-is-new-cam}

O Cloud Acceleration Manager agora oferece aos usuários a capacidade de visualizar relatórios históricos de BPA em um Relatório de linha de tendência. Com este Relatório, os usuários podem visualizar o progresso que estão fazendo em uma representação gráfica fácil de consumir. Consulte [Usando a Linha de Tendência da Exibição](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/cam-readiness-phase.html?lang=en#trendline-view-cam) para obter mais detalhes.

### Data de lançamento {#release-date-october-cam}

A data de lançamento do Cloud Acceleration Manager é 4 de outubro de 2021.

### Novidades {#what-is-new-cam-oct}

O Cloud Acceleration Manager agora oferece aos usuários a capacidade de visualizar os relatórios de BPA em uma pré-visualização que pode ser impressa, permitindo que a impressão ou impressão simples sejam feitas no PDF para proporcionar fácil compartilhamento. Consulte as Etapas 6 e 7 em [Uso do cartão de análise de práticas recomendadas](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/cam-readiness-phase.html?lang=en#best-practices-analysis).


## Ferramenta Transferência de conteúdo {#ctt-release}

### Data de lançamento {#release-date-ctt-latest}

A Data de lançamento da ferramenta Transferência de conteúdo v1.6.0 é 4 de outubro de 2021.

### Novidades {#what-is-new-ctt-oct}

* Ferramenta de mapeamento de usuários aprimorada com uma experiência simplificada do usuário, incluindo os seguintes recursos listados abaixo. Para obter mais detalhes, consulte [Usar a ferramenta Mapeamento de usuários](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/user-mapping-tool/using-user-mapping-tool.html).
   * Testar conexão com a API de gerenciamento de usuários antes de executar o Mapeamento de usuários
   * Ignore erros com cuidado e continue com a atividade de Mapeamento de usuários
   * O mapeamento de usuário não falha mais se **Token de acesso** expira após 24 horas. O Mapeamento de Usuário pode ser executado novamente de onde parou pela última vez.

* Para aumentar a robustez da ferramenta Transferência de conteúdo, o conteúdo pode ser assimilado na instância de autor ou de publicação de cada vez. Consulte [Introdução à ferramenta Transferência de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=en) para obter mais detalhes.

* Quando as versões são incluídas, o caminho `/var/audit` é incluído automaticamente para migrar eventos de auditoria.

## Analisador de práticas recomendadas {#best-practices-analyzer}

### Data de lançamento {#release-date-bpa-latest}

A data de lançamento do Analisador de práticas recomendadas v2.1.20 é 5 de outubro de 2021.

### Novidades {#what-is-new-bpa-oct}

* Capacidade de detectar e relatar o comprimento do nome do nó.

* Capacidade de detectar e relatar o tamanho total do Índice.

* Capacidade de detectar e gerar relatórios sobre ativos que não possuem sua representação original.