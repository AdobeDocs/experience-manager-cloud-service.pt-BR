---
title: Notas de versão para Ferramentas de migração AEM versão as a Cloud Service 2022.7.0
description: Notas de versão para Ferramentas de migração AEM versão as a Cloud Service 2022.7.0
feature: Release Information
source-git-commit: f84327096951772e1bed8656334841e1292d6bcf
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 9%

---

# Notas de versão para Ferramentas de migração AEM versão as a Cloud Service 2022.7.0 {#release-notes}

Esta página descreve as Notas de versão para as Ferramentas de migração AEM as a Cloud Service 2022.7.0.

## Ferramenta Transferência de conteúdo {#ctt-release}

### Data de lançamento {#release-date-ctt}

A Data de lançamento da ferramenta Transferência de conteúdo v2.0.12 é 19 de julho de 2022.

### Novidades {#what-is-new-ctt}

* Os usuários conectados via LDAP agora podem executar os recursos Verificar tamanho e mapeamento do usuário no CTT.
* Para ajudar a depurar problemas de conexão SSL/TLS durante as extrações, os usuários agora podem ativar o registro em SSL.
* Para ajudar a depurar problemas de conectividade de origem, os nomes de subdomínio agora são impressos nos logs quando a conexão com o Azure falha.
* Para ajudar a depurar problemas durante a pré-cópia, os logs do AzCopy agora são anexados aos logs de extração quando a pré-cópia falha.
* Para evitar resultados obsoletos de Tamanho de Verificação, os usuários poderão executar novamente Tamanho de Verificação somente depois que um Tamanho de Verificação anterior for concluído.

### Correções de erros {#bug-fixes-ctt}

* Registros de extração anteriores apareciam após a exclusão e recriação de um conjunto de migração. Isso foi corrigido.
* O botão de ação Exibir progresso não estava disponível para conjuntos de migração com status PARADO. Isso foi corrigido.
* O botão de ação Excluir não estava disponível para conjuntos de migração com uma chave de extração expirada. Isso foi corrigido.
* Correção de vários bugs da interface do usuário.

## Cloud Acceleration Manager {#cam-release}

### Data de lançamento {#release-date-cam}

A data de lançamento do Cloud Acceleration Manager é 15 de julho de 2022.

### Novidades {#what-is-new-cam}

* O Cloud Acceleration Manager agora fornece aos usuários a recuperação manual do token de migração para poder iniciar uma assimilação quando a recuperação automática falhar. A recuperação automática pode falhar se os clientes tiverem configurado uma lista de permissões de IP que bloqueia a CAM ou se um usuário não administrador tentar iniciar uma assimilação. Consulte [Solução de problemas](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#troubleshooting) para obter mais informações.
* Tabelas longas na página Complexidade da migração agora podem ser recolhidas para facilitar o uso.

