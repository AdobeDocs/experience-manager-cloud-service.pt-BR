---
title: Pré-requisitos para a ferramenta de transferência de conteúdo
description: Familiarize-se com os pré-requisitos da Ferramenta de transferência de conteúdo
exl-id: 41a9cff1-4d89-480c-b9fc-5e8efc2a0705
feature: Migration
role: Admin
source-git-commit: 3e3d018dfd4babce9abef858e487bf1c116ed3a6
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 13%

---


# Pré-requisitos para a ferramenta de transferência de conteúdo {#prerequisites}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_prereqs"
>title="Considerações importantes sobre o uso da ferramenta de transferência de conteúdo"
>abstract="Revise considerações importantes para usar a Ferramenta de Transferência de Conteúdo, incluindo versões do Java™ e AEM, tipos compatíveis de armazenamento de dados, considerações sobre grupos de usuários e mais."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/prerequisites-content-transfer-tool.html?lang=pt-BR" text="Considerações importantes sobre o uso da ferramenta de transferência de conteúdo"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html?lang=pt-BR#best-practices" text="Práticas recomendadas e diretrizes"

A tabela a seguir resume os pré-requisitos para usar a Ferramenta de transferência de conteúdo.

Analise todas as considerações listadas abaixo:

| Considerações | O que é compatível no momento |
|--------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Versão do AEM | A Ferramenta de transferência de conteúdo pode ser executada somente no AEM 6.3 ou nas versões posteriores. |
| Tamanho do armazenamento de segmentos | Um repositório existente que tenha menos de 750 milhões de nós JCR e até 500 GB (tamanho compactado online) no *Author* e 50 GB no *Publish* tem suporte no momento. Crie um tíquete de suporte no Atendimento ao cliente da Adobe para discutir as opções de tamanho do armazenamento de segmento acima desses limites. |
| Tamanho Total do Repositório de Conteúdo <br>*(repositório de segmentos + repositório de dados)* | A ferramenta Transferência de conteúdo foi projetada para transferir conteúdo até 20 terabytes para o tipo de armazenamento de dados File Data Store. Não há suporte no momento para qualquer coisa com mais de 20 terabytes. Crie um tíquete de suporte no Atendimento ao cliente da Adobe para discutir as opções de conteúdo maior que 20 terabytes. <br>Para acelerar significativamente o processo de transferência de conteúdo para repositórios grandes, uma etapa [pré-cópia](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=pt-BR#setting-up-pre-copy-step) opcional pode ser usada. Esse processo se aplica aos tipos de armazenamento de dados File Data Store, Amazon S3 e Azure Data Store. Para o Amazon S3 e o Azure Data Store, há suporte para tamanhos de repositório superiores a 20 terabytes. |
| Tamanho total do índice Lucene | Tamanho total do Índice Lucene de 25 GB, no máximo, excluindo-se `/oak:index/lucene` e `/oak:index/damAssetLucene`. Crie um tíquete de suporte no Atendimento ao cliente da Adobe para discutir as opções de tamanho de índice acima desse limite. |
| Conteúdo em caminhos imutáveis | A ferramenta Transferência de conteúdo não pode ser usada para migrar conteúdo em caminhos imutáveis. Para transferir o conteúdo de `/etc`, você pode selecionar determinados caminhos de `/etc`, mas apenas para dar suporte ao [AEM Forms para o AEM Forms as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/setup-configure-migrate/migrate-to-forms-as-a-cloud-service.html?lang=pt-BR#paths-of-various-aem-forms-specific-assets). Para todos os outros casos de uso, consulte [Reestruturação do repositório comum](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/restructuring/all-repository-restructuring-in-aem-6-5.html?lang=pt-BR) para saber mais sobre a reestruturação do repositório. |
| Valor da propriedade do nó no MongoDB | Os valores de propriedade do nó armazenados no MongoDB não podem exceder 16 MB. Essa regra é aplicada pelo MongoDB. As assimilações falharão se houver valores de propriedade maiores que esse limite. Antes de executar uma extração, execute este script [oak-run](https://repo1.maven.org/maven2/org/apache/jackrabbit/oak-run/1.38.0/oak-run-1.38.0.jar). Revise todos os valores de propriedade grandes e valide se eles são necessários. Os que excedem 16 MB devem ser convertidos em valores Binários. |

## O que vem a seguir {#whats-next}

Depois de revisar os pré-requisitos e determinar se você pode usar a Ferramenta de transferência de conteúdo em seu projeto de migração, consulte [Diretrizes e práticas recomendadas para usar a Ferramenta de transferência de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html?lang=pt-BR).