---
title: Notas de versão do Cloud Manager AEM versão as a Cloud Service 2021.6.0
description: Notas de versão do Cloud Manager AEM versão as a Cloud Service 2021.5.0
feature: Release Information
exl-id: 9a0a53d3-31d4-493d-ba2e-b4bb22f60351
source-git-commit: 4b76fbbb1b58324065b39d6928027759b0897246
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 3%

---

# Notas de versão do Cloud Manager no Adobe Experience Manager as a Cloud Service 2021.6.0 {#release-notes}

Esta página descreve as Notas de versão do Cloud Manager AEM as a Cloud Service 2021.6.0.

>[!NOTE]
>Para ver as Notas de versão atuais do Adobe Experience Manager as a Cloud Service, clique em [here](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=pt-BR).

## Data de lançamento {#release-date}

A data de lançamento do Cloud Manager AEM as a Cloud Service 2021.6.0 é 10 de junho de 2021.

### Novidades {#what-is-new}

* O Serviço de Pré-visualização será implantado continuamente em todos os Programas. Os clientes serão notificados no produto quando o Programa estiver ativado para o Serviço de visualização. Consulte [Acesso ao serviço de visualização](/help/implementing/cloud-manager/manage-environments.md#access-preview-service) para obter mais detalhes.

* As Dependências de Maven baixadas durante a etapa de build agora serão armazenadas em cache entre as execuções de pipeline. Esse recurso será ativado para clientes nas próximas semanas.

* O nome do programa agora pode ser editado por meio da caixa de diálogo Editar programa .

* O nome da ramificação padrão usado durante a criação do projeto e no comando de push padrão por meio do gerenciamento de workflows do git foi alterado para `main`.

* A experiência de edição de programa na interface do usuário foi atualizada.

* A regra de qualidade `ImmutableMutableMixCheck` foi atualizada para classificar `/oak:index` como sendo imutáveis.

* Regras de qualidade `CQBP-84` e `CQBP-84--dependencies` foram consolidadas em uma única regra. Como parte dessa consolidação, a varredura de dependências identifica com mais precisão os problemas em dependências de terceiros que estão sendo implantados no tempo de execução AEM.

* Para evitar confusão, as linhas de segmento Publicar AEM e Publicar Dispatcher na página Detalhes do ambiente foram consolidadas.

   ![](/help/implementing/cloud-manager/release-notes-cloud-manager/assets/aem-dispatcher.png)

* Uma nova regra de qualidade de código foi adicionada para validar a estrutura de `damAssetLucene` índices. Consulte [Índices Oak do Ativo DAM Personalizado](/help/implementing/cloud-manager/custom-code-quality-rules.md#oakpal-damAssetLucene-sanity-check) para obter mais detalhes.

* A página Detalhes do ambiente agora exibe vários nomes de domínio para os serviços de Publicação e Visualização (conforme aplicável). Consulte [Detalhes do ambiente](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html?lang=en#viewing-environment) para obter mais detalhes.

### Correções de erros {#bug-fixes}

* Definições de nó JCR contendo uma nova linha após o nome do elemento raiz não foram analisadas corretamente.

* A API de repositórios de lista não filtra repositórios excluídos.

* Uma mensagem de erro incorreta era exibida quando um valor inválido era fornecido para a etapa de programação.

* Ocasionalmente, o usuário pode ver um verde *ative* status ao lado de uma Lista de permissões de IP, mesmo quando essa configuração não foi implantada.

* Algumas sequências de edição de programas podem resultar na incapacidade de criar ou editar o pipeline de produção.

* Algumas sequências de edição de programas podem resultar no **Visão geral** página exibindo uma mensagem enganosa para executar novamente a configuração do programa.
