---
title: Notas de versão das Ferramentas de migração no AEM as a Cloud Service versão 2024.09
description: Notas de versão das Ferramentas de migração no AEM as a Cloud Service versão 2024.09.0
feature: Release Information
exl-id: 52709511-eab2-47a7-8bea-1b707cd568a1
role: Admin
source-git-commit: 0c16f264826a46907afc33c91a021e7696f5b7a8
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 7%

---

# Notas de versão das Ferramentas de migração no AEM as a Cloud Service versão 2024.09.0 {#release-notes}

Esta página descreve as Notas de versão das Ferramentas de migração no AEM as a Cloud Service 2024.09.0.

## Ferramenta Transferência de conteúdo {#ctt-release}

### Data de lançamento {#release-date-ctt}

A data de lançamento da ferramenta de Transferência de conteúdo v3.0.20 é 28 de agosto de 2024.

### Novidades {#what-is-new-ctt}

* Os usuários não serão mais assimilados com esta versão e, por esse motivo, o recurso opcional Mapeamento de usuário foi removido.
* Uma opção de configuração OSGI foi adicionada para desativar ou ativar a migração de entidades durante a extração e a assimilação (a configuração padrão é ativá-la)

### Correções de erros {#bug-fixes-ctt}

* A CTT foi aprimorada para evitar um erro ao desproteger uma chave secreta na configuração do azcopy
* A CTT agora lida normalmente com qualquer erro ao copiar logs do AzCopy na fase de validação
* Alterar o diretório de log do Azcopy criado durante o processo de extração

## Analisador de práticas recomendadas {#bpa-release}

### Data de lançamento {#release-date-bpa}

A data de lançamento do Analisador de práticas recomendadas v2.1.52 é 4 de setembro de 2024

### Novidades {#what-is-new-bpa}

* Um novo padrão foi introduzido para detectar eventos baseados em JCR no AEM

### Correções de erros {#bug-fixes-bpa}

* Correção de falsos positivos
* Robustez aprimorada para lidar com a resposta redirecionada do dispatcher
* Correção da não comunicação de descoberta NCC para todos os idiomas em /apps/wcm/core/resources/languages/
* adição de uma verificação para detectar se uma multipropriedade de um nó não tem valores

