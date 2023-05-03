---
title: Pré-requisitos para a ferramenta Transferência de conteúdo (herdado)
description: Pré-requisitos para a ferramenta Transferência de conteúdo
hide: true
hidefromtoc: true
exl-id: 6b2878cb-6882-452b-8cab-e590316633f6
source-git-commit: eb633db8fe64a62661c094b88f0ce8d9950ed6d7
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 2%

---

# Pré-requisitos para a ferramenta Transferência de conteúdo (herdado) {#prerequisites}

A tabela a seguir resume os pré-requisitos para usar a ferramenta Transferência de conteúdo .

Revise todas as considerações listadas abaixo:

| Considerações | O que é compatível no momento |
|--- |--- |
| Versão do AEM | A ferramenta Transferência de conteúdo pode ser executada somente no AEM 6.3 ou versões superiores. |
| Tamanho do armazenamento de segmentos | Um repositório existente que tem menos de 55 milhões de nós JCR e até 83 GB (tamanho compactado online) em *Autor* e 31 GB em *Publicar* atualmente são compatíveis. Crie um tíquete de suporte com o Atendimento ao cliente do Adobe para discutir opções de tamanho de armazenamento de segmento acima desses limites. |
| Tamanho total do repositório de conteúdo <br>*(armazenamento de segmentos + armazenamento de dados)* | A ferramenta Transferência de conteúdo foi criada para transferir conteúdo de até 20 TB para o tipo de armazenamento de dados File Data Store. Qualquer coisa superior a 20 TB não é compatível no momento. Crie um tíquete de suporte com o Atendimento ao cliente do Adobe para discutir opções de conteúdo maior que 20 TB. <br>Para acelerar significativamente o processo de transferência de conteúdo para repositórios grandes, uma [pré-cópia](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en#setting-up-pre-copy-step) pode ser usada. Isso se aplica aos tipos de armazenamento de dados do File Data Store, Amazon S3 e Azure Data Store. Para o Amazon S3 e o Azure Data Store, são suportados tamanhos de repositório maiores que 20 TB. |
| Tamanho total do índice de Lucene | Atualmente, há suporte para o tamanho total do Índice Lucene de no máximo 25 GB. Crie um tíquete de suporte com o Atendimento ao cliente do Adobe para discutir opções de tamanho de índice acima desse limite. |
| Tamanho do nome do nó | O comprimento de um nome de nó deve ser de 150 bytes ou menos. Nomes de nó com mais de 150 bytes devem ser encurtados para serem &lt;= 150 bytes para terem suporte no armazenamento de nó de documento em AEM as a Cloud Service. As sugestões falharão se esses nomes de nó longos não forem corrigidos. |
| Conteúdo em caminhos imutáveis | A ferramenta Transferência de conteúdo não pode ser usada para migrar o conteúdo em caminhos imutáveis. Para transferir conteúdo de `/etc` somente certos `/etc` os caminhos podem ser selecionados, mas somente para oferecer suporte [AEM Forms para AEM Forms as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/migrate-to-forms-as-a-cloud-service.html?lang=en#paths-of-various-aem-forms-specific-assets). Para todos os outros casos de uso, consulte [Reestruturação comum de repositório](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/restructuring/all-repository-restructuring-in-aem-6-5.html) para saber mais sobre a reestruturação de repositório. |
| Valor da propriedade do nó no MongoDB | Os valores de propriedade de nó armazenados no MongoDB não podem exceder 16MB. Isso é empregado pelo MongoDB. As sugestões falharão se houver valores de propriedade maiores que esse limite. Antes de executar uma extração, execute isso [oak-run](https://repo1.maven.org/maven2/org/apache/jackrabbit/oak-run/1.38.0/oak-run-1.38.0.jar) script. Revise todos os valores de propriedades grandes e valide se eles forem necessários. Os que excederem 16MB precisarão ser convertidos em valores binários. |

## O que vem a seguir {#whats-next}

Depois de revisar os pré-requisitos e determinar se você pode usar a ferramenta Transferência de conteúdo no projeto de migração, consulte [Diretrizes e práticas recomendadas para usar a ferramenta Transferência de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html?lang=en).
