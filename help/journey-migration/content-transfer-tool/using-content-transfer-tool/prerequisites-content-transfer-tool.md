---
title: Pré-requisitos para a ferramenta Transferência de conteúdo
description: Pré-requisitos para a ferramenta Transferência de conteúdo
exl-id: 41a9cff1-4d89-480c-b9fc-5e8efc2a0705
source-git-commit: 5475f9995513d09e61bd8f52242b3e74b8d4694c
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 6%

---

# Pré-requisitos para a ferramenta Transferência de conteúdo {#prerequisites}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_prereqs"
>title="Considerações importantes sobre o uso da ferramenta Transferência de conteúdo"
>abstract="Analise considerações importantes para usar a ferramenta Transferência de conteúdo, incluindo versões Java e AEM, tipos compatíveis de armazenamento de dados, considerações sobre grupos de usuários e muito mais."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html#pre-reqs" text="Considerações importantes sobre o uso da ferramenta Transferência de conteúdo"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html#best-practices" text="Práticas recomendadas e diretrizes"

A tabela a seguir resume os pré-requisitos para usar a ferramenta Transferência de conteúdo .

Revise todas as considerações listadas abaixo:

| Considerações | O que é compatível no momento |
|---------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Versão do AEM | A ferramenta Transferência de conteúdo pode ser executada somente no AEM 6.3 ou versões superiores. |
| Tamanho do armazenamento de segmentos | Um repositório existente que tem menos de 55 milhões de nós JCR e até 250 GB (tamanho compactado online) em *Autor* e 50 GB em *Publicar* atualmente são compatíveis. Crie um tíquete de suporte com o Atendimento ao cliente do Adobe para discutir opções de tamanho de armazenamento de segmento acima desses limites. |
| Tamanho total do repositório de conteúdo <br>*(armazenamento de segmentos + armazenamento de dados)* | A ferramenta Transferência de conteúdo foi criada para transferir conteúdo de até 20 TB para o tipo de armazenamento de dados File Data Store. Qualquer coisa superior a 20 TB não é compatível no momento. Crie um tíquete de suporte com o Atendimento ao cliente do Adobe para discutir opções de conteúdo maior que 20 TB. <br>Para acelerar significativamente o processo de transferência de conteúdo para repositórios grandes, uma [pré-cópia](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=pt-BR#setting-up-pre-copy-step) pode ser usada. Isso se aplica aos tipos de armazenamento de dados do File Data Store, Amazon S3 e Azure Data Store. Para o Amazon S3 e o Azure Data Store, são suportados tamanhos de repositório maiores que 20 TB. |
| Tamanho total do índice de Lucene | Tamanho total do Índice Lucene de 25 GB no máximo, excluindo `/oak:index/lucene` e `/oak:index/damAssetLucene` atualmente é compatível. Crie um tíquete de suporte com o Atendimento ao cliente do Adobe para discutir opções de tamanho de índice acima desse limite. |
| Tamanho do nome do nó | O comprimento de um nome de nó deve ser de 150 bytes ou menos quando o caminho pai do nó for >= (igual ou maior que) 350 bytes. Esses nomes de nó devem ser encurtados para serem &lt;= 150 bytes para terem suporte no armazenamento de nó do documento em AEM as a Cloud Service. As sugestões falharão se esses nomes de nó longos não forem corrigidos. |
| Conteúdo em caminhos imutáveis | A ferramenta Transferência de conteúdo não pode ser usada para migrar o conteúdo em caminhos imutáveis. Para transferir conteúdo de `/etc` somente certos `/etc` os caminhos podem ser selecionados, mas somente para oferecer suporte [AEM Forms para AEM Forms as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/migrate-to-forms-as-a-cloud-service.html#paths-of-various-aem-forms-specific-assets). Para todos os outros casos de uso, consulte [Reestruturação comum de repositório](https://experienceleague.adobe.com/docs/experience-manager-64/deploying/restructuring/all-repository-restructuring-in-aem-6-4.html#restructuring) para saber mais sobre a reestruturação de repositório. |
| Valor da propriedade do nó no MongoDB | Os valores de propriedade de nó armazenados no MongoDB não podem exceder 16MB. Isso é empregado pelo MongoDB. As sugestões falharão se houver valores de propriedade maiores que esse limite. Antes de executar uma extração, execute isso [oak-run](https://repo1.maven.org/maven2/org/apache/jackrabbit/oak-run/1.38.0/oak-run-1.38.0.jar) script. Revise todos os valores de propriedades grandes e valide se eles forem necessários. Os que excederem 16MB precisarão ser convertidos em valores binários. |

## O que vem a seguir {#whats-next}

Depois de revisar os pré-requisitos e determinar se você pode usar a ferramenta Transferência de conteúdo no projeto de migração, consulte [Diretrizes e práticas recomendadas para usar a ferramenta Transferência de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html).
