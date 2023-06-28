---
title: Notas de versão das Ferramentas de migração no AEM as a Cloud Service versão 2021.10.0
description: Notas de versão das Ferramentas de migração no AEM as a Cloud Service versão 2021.11.0
feature: Release Information
exl-id: 6b1caa63-dcb0-4c48-ab2c-fd72617abf13
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 14%

---

# Notas de versão das Ferramentas de migração no AEM as a Cloud Service versão 2021.10.0 {#release-notes}

Esta página descreve as notas de versão das ferramentas de migração no AEM as a Cloud Service 2021.10.0.

>[!NOTE]
>Para ver as notas de versão atuais do Adobe Experience Manager as a Cloud Service, clique [aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/release-notes/release-notes-current.html?lang=pt-BR).

## Cloud Acceleration Manager {#cam-release}

### Data de lançamento {#release-date-cam}

A data de lançamento do Cloud Acceleration Manager é 25 de outubro de 2021.

### Novidades {#what-is-new-cam}

O Cloud Acceleration Manager agora oferece aos usuários a capacidade de visualizar relatórios históricos do BPA em um relatório de linha de tendências. Com esse relatório, os usuários podem visualizar o progresso que estão fazendo em uma representação gráfica fácil de consumir. Consulte [Usando Exibir Linha de Tendência](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-acceleration-manager/using-cam/cam-readiness-phase.html?lang=en#trendline-view-cam) para obter mais detalhes.

### Data de lançamento {#release-date-october-cam}

A data de lançamento do Cloud Acceleration Manager é 4 de outubro de 2021.

### Novidades {#what-is-new-cam-oct}

O Cloud Acceleration Manager agora oferece aos usuários a capacidade de visualizar os relatórios do BPA em uma impressão simples ou impressão em PDF para facilitar o compartilhamento. Consulte as Etapas 6 e 7 em [Usando o cartão de análise de práticas recomendadas](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-acceleration-manager/using-cam/cam-readiness-phase.html?lang=en#best-practices-analysis).


## Ferramenta Transferência de conteúdo {#ctt-release}

### Data de lançamento {#release-date-ctt-latest}

A data de lançamento da ferramenta de Transferência de conteúdo v1.6.0 é 4 de outubro de 2021.

### Novidades {#what-is-new-ctt-oct}

* Ferramenta de Mapeamento de usuário aprimorada com uma experiência do usuário simplificada, incluindo os seguintes recursos listados abaixo. Para obter mais detalhes, consulte [Utilização da ferramenta Mapeamento de usuários](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/legacy-user-mapping-tool/using-user-mapping-tool-legacy.html?lang=en).
   * Testar conexão com a API de gerenciamento de usuários antes de executar o mapeamento de usuários
   * Ignorar erros normalmente e continuar com a atividade Mapeamento de usuário
   * O mapeamento de usuários não falha mais se **Token de acesso** expira após 24 horas. O Mapeamento de usuário pode ser executado novamente de onde parou pela última vez.

* Para aumentar a robustez da Ferramenta de transferência de conteúdo, o conteúdo pode ser assimilado na instância do Autor ou na instância de Publicação de cada vez. Consulte [Introdução à ferramenta Transferência de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=pt-BR) para obter mais detalhes.

* Quando as versões são incluídas, o caminho `/var/audit` é incluído automaticamente para migrar eventos de auditoria.

## Analisador de práticas recomendadas {#best-practices-analyzer}

### Data de lançamento {#release-date-bpa-latest}

A data de lançamento do Analisador de práticas recomendadas v2.1.20 é 5 de outubro de 2021.

### Novidades {#what-is-new-bpa-oct}

* Capacidade de detectar e relatar o comprimento do nome do nó.

* Capacidade de detectar e relatar o tamanho total do índice.

* Capacidade de detectar e relatar ativos sem a representação original.
