---
title: Notas de versão do Cloud Manager AEM versão as a Cloud Service 2021.10.0
description: Notas de versão do Cloud Manager AEM versão as a Cloud Service 2021.10.0
feature: Release Information
exl-id: null
source-git-commit: a519b5bd774506f50f49c8309b14d4a62c7e7ba5
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 3%

---

# Notas de versão do Cloud Manager no Adobe Experience Manager as a Cloud Service 2021.10.0 {#release-notes}

Esta página descreve as Notas de versão do Cloud Manager AEM as a Cloud Service 2021.10.0.

>[!NOTE]
>Para ver as Notas de versão atuais do Adobe Experience Manager as a Cloud Service, clique [aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=pt-BR).

## Data de lançamento {#release-date}

A Data de lançamento do Cloud Manager AEM as a Cloud Service 2021.10.0 é 14 de outubro de 2021.
A próxima versão está planejada para 04 de novembro de 2021.

### Novidades {#what-is-new}

* Em preparação para algumas alterações futuras, os pipelines de implantação existentes agora serão referenciados e rotulados na interface do usuário como **Pilha completa** pipelines.

* O cartão de pipeline foi atualizado para exibir agora uma única face integrada que mostra os pipelines de produção e não de produção, e o usuário pode selecionar Executar/Pausar/Retomar diretamente do menu de ação associado a cada pipeline.

* Um usuário na função Gerenciador de implantação agora pode excluir o pipeline de Produção de maneira automatizada por meio da interface do usuário.

* Adicionar e editar experiências de pipeline foi atualizado para agora usar modais modernos e familiares.

* Os usuários do Cloud Manager agora podem enviar feedback diretamente da interface do usuário por meio do botão **Feedback** no canto superior direito da página de aterrissagem.

* Os gráficos de SLA anuais agora podem ser baixados na interface do usuário do Cloud Manager.

* As execuções de pipeline de não produção e qualidade de código agora usam um processo de clonagem superficial mais eficiente durante a etapa de compilação, resultando em um tempo de compilação mais rápido para clientes com repositórios Git especialmente grandes.

* O assistente Adicionar Lista de permissões de IP agora informará o usuário se o número máximo permitido de Listas de permissões de IP tiver sido atingido.

* A documentação da API do Cloud Manager agora inclui um playground interativo que permite que os usuários conectados façam experiências com a API a partir de seu navegador. Consulte [Espaço de reprodução da API do Cloud Manager](https://www.adobe.io/experience-cloud/cloud-manager/reference/playground/) para obter mais detalhes.

* A dica de ferramenta no cartão Programa será mais descritiva se uma opção de seleção em &quot;Navegar para&quot; estiver desativada. Agora, ele exibe &quot;Um ambiente de produção não existe&quot;.

### Correções de erros {#bug-fixes}

* Em raras situações, quando uma equipe de Adobe restaurava o ambiente de um cliente, a restauração era considerada concluída antes que o ambiente estivesse totalmente operacional.

* Certas solicitações internas feitas durante a criação do ambiente não foram repetidas.

