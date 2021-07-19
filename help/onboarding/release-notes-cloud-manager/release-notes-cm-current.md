---
title: Notas de versão do Cloud Manager no AEM as a Cloud Service versão 2021.5.0
description: Notas de versão do Cloud Manager no AEM as a Cloud Service versão 2021.5.0
feature: Informações da versão
exl-id: 42cc9cab-6e66-4976-a3b1-ecb9dbaaabf4
source-git-commit: 00bea8b6a32bab358dae6a8c30aa807cf4586d84
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 3%

---

# Notas de versão do Cloud Manager no Adobe Experience Manager as a Cloud Service 2021.6.0 {#release-notes}

Esta página descreve as Notas de versão do Cloud Manager no AEM as a Cloud Service 2021.6.0.

>[!NOTE]
>Para ver as Notas de versão atuais do Adobe Experience Manager como um Cloud Service, clique [aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=pt-BR).

## Data de lançamento {#release-date}

A data de lançamento do Cloud Manager no AEM as a Cloud Service 2021.6.0 é 10 de junho de 2021.
A próxima versão está planejada para 15 de julho de 2021.

### Novidades {#what-is-new}

* O Serviço de Pré-visualização será implantado continuamente em todos os Programas. Os clientes serão notificados no produto quando o Programa estiver ativado para o Serviço de visualização. Consulte [Acessando o serviço de visualização](/help/implementing/cloud-manager/manage-environments.md#access-preview-service) para obter mais detalhes.

* As Dependências de Maven baixadas durante a etapa de build agora serão armazenadas em cache entre as execuções de pipeline. Esse recurso será ativado para clientes nas próximas semanas.

* O nome do programa agora pode ser editado por meio da caixa de diálogo Editar programa .

* O nome da ramificação padrão usado durante a criação do projeto e no comando push padrão por meio do gerenciamento de workflows git foi alterado para `main`.

* A experiência de edição de programa na interface do usuário foi atualizada.

* A regra de qualidade `ImmutableMutableMixCheck` foi atualizada para classificar os nós `/oak:index` como imutáveis.

* As regras de qualidade `CQBP-84` e `CQBP-84--dependencies` foram consolidadas em uma única regra. Como parte dessa consolidação, a varredura de dependências identifica com mais precisão os problemas em dependências de terceiros que estão sendo implantados no tempo de execução AEM.

* Para evitar confusão, as linhas de segmento Publicar AEM e Publicar Dispatcher na página Detalhes do ambiente foram consolidadas.

   ![](/help/onboarding/release-notes-cloud-manager/assets/aem-dispatcher.png)

* Uma nova regra de qualidade de código foi adicionada para validar a estrutura de índices `damAssetLucene`. Consulte [Índices de Oak do Ativo do DAM Personalizado](/help/implementing/cloud-manager/custom-code-quality-rules.md#oakpal-damAssetLucene-sanity-check) para obter mais detalhes.

* A página Detalhes do ambiente agora exibe vários nomes de domínio para os serviços de Publicação e Visualização (conforme aplicável). Consulte [Detalhes do ambiente](/help/implementing/cloud-manager/manage-environments.md#viewing-environment) para obter mais detalhes.

### Correções de erros {#bug-fixes}

* Definições de nó JCR contendo uma nova linha após o nome do elemento raiz não foram analisadas corretamente.

* A API de repositórios de lista não filtra repositórios excluídos.

* Uma mensagem de erro incorreta era exibida quando um valor inválido era fornecido para a etapa de programação.

* Ocasionalmente, o usuário pode ver um status verde *ativo* ao lado de uma Lista de permissões de IP, mesmo quando essa configuração não foi implantada.

* Algumas sequências de edição de programas podem resultar na incapacidade de criar ou editar o pipeline de produção.

* Algumas sequências de edição de programas podem resultar na página **Visão Geral** exibindo uma mensagem enganosa para executar novamente a configuração do programa.
