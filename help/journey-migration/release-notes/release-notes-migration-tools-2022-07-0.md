---
title: Notas de versão das Ferramentas de migração no AEM as a Cloud Service versão 2022.7.0
description: Notas de versão das Ferramentas de migração no AEM as a Cloud Service versão 2022.7.0
feature: Release Information
exl-id: bc8f1a80-867e-423a-9c03-4a53b1ebc57c
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 9%

---

# Notas de versão das Ferramentas de migração no AEM as a Cloud Service versão 2022.7.0 {#release-notes}

Esta página descreve as Notas de versão das Ferramentas de migração no AEM as a Cloud Service 2022.7.0.

## Analisador de práticas recomendadas {#bpa-release}

### Data de lançamento {#release-date-bpa}

A data de lançamento do Analisador de práticas recomendadas v2.1.30 é 27 de julho de 2022.

### Novidades {#what-is-new-bpa}

* O BPA agora pode detectar e relatar o tamanho total do Índice Lucene migrável, que é o Índice Lucene Total excluindo `/oak:index/lucene` e `/oak:index/damAssetLucene`.
* Novo padrão adicionado no BPA para detectar e relatar o uso do dicionário i18n personalizado. O Translator.html não está disponível no AEM as a Cloud Service e o dicionário i18n personalizado deve ser implantado a partir do Git por meio do pipeline de CI/CD do Cloud Manager.

### Correções de erros {#bug-fixes-bpa}

* O BPA relatava a ausência de representações originais para Fragmentos de conteúdo. Como os Fragmentos de conteúdo não têm representações, essa verificação agora é ignorada para Fragmentos de conteúdo.
* A opção para filtrar achados ACS Commons estava ausente da interface do usuário do BPA. Isso foi corrigido.

## Ferramenta Transferência de conteúdo {#ctt-release}

### Data de lançamento {#release-date-ctt}

A data de lançamento da ferramenta de transferência de conteúdo v2.0.12 é 19 de julho de 2022.

### Novidades {#what-is-new-ctt}

* Os usuários conectados via LDAP agora podem executar os recursos Verificar Tamanho e Mapeamento de Usuários na CTT.
* Para ajudar a depurar problemas de conexão SSL/TLS durante as extrações, os usuários agora podem ativar o registro SSL.
* Para ajudar a depurar problemas de conectividade de origem, os nomes de subdomínio agora são impressos nos logs quando a conexão com o Azure falha.
* Para ajudar a depurar problemas durante a pré-cópia, os logs do AzCopy agora são anexados aos logs de extração quando a pré-cópia falha.
* Para evitar resultados obsoletos da verificação de tamanho, os usuários só podem executar a verificação de tamanho novamente após a conclusão de uma verificação de tamanho anterior.

### Correções de erros {#bug-fixes-ctt}

* Registros de extração anteriores apareciam após a exclusão e recriação de um conjunto de migração. Isso foi corrigido.
* O botão de ação Exibir andamento não estava disponível para conjuntos de migração com status PARADO. Isso foi corrigido.
* O botão Excluir ação não estava disponível para conjuntos de migração com uma chave de extração expirada. Isso foi corrigido.
* Correção de vários bugs na interface do usuário.

## Cloud Acceleration Manager {#cam-release}

### Data de lançamento {#release-date-cam}

A data de lançamento do Cloud Acceleration Manager é 15 de julho de 2022.

### Novidades {#what-is-new-cam}

* O Cloud Acceleration Manager agora fornece aos usuários a recuperação manual do token de migração para poder iniciar uma assimilação quando a recuperação automática falhar. A recuperação automática pode falhar se os clientes tiverem configurado uma lista de permissões de IP que bloqueia o CAM ou se um usuário não administrador tentar iniciar uma assimilação. Consulte [Solução de problemas](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#troubleshooting) para obter mais informações.
* Tabelas longas na página Complexidade de migração agora podem ser recolhidas para facilitar o uso.
