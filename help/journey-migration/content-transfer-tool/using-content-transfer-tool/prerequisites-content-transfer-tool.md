---
title: Pré-requisitos para a ferramenta Transferência de conteúdo
description: Pré-requisitos para a ferramenta Transferência de conteúdo
exl-id: 41a9cff1-4d89-480c-b9fc-5e8efc2a0705
source-git-commit: eb633db8fe64a62661c094b88f0ce8d9950ed6d7
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 15%

---

# Pré-requisitos para a ferramenta Transferência de conteúdo {#prerequisites}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_prereqs"
>title="Considerações importantes sobre o uso do Content Transfer Tool"
>abstract="Revise considerações importantes para usar a ferramenta de Transferência de Conteúdo, incluindo versões do Java e AEM, tipos compatíveis de armazenamento de dados, considerações sobre grupos de usuários e mais."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html#pre-reqs" text="Considerações importantes sobre o uso da ferramenta Transferência de conteúdo"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html#best-practices" text="Práticas recomendadas e diretrizes"

A tabela a seguir resume os pré-requisitos para usar a Ferramenta de transferência de conteúdo.

Revise todas as considerações listadas abaixo:

| Considerações | O que é compatível no momento |
|---------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Versão do AEM | A ferramenta Transferência de conteúdo pode ser executada somente no AEM 6.3 ou em versões posteriores. |
| Tamanho do armazenamento de segmentos | Um repositório existente que tenha menos de 55 milhões de nós JCR e até 250 GB (tamanho compactado online) no *Autor* e 50 GB em *Publish* são compatíveis no momento. Crie um tíquete de suporte no Atendimento ao cliente do Adobe para discutir as opções de tamanho do armazenamento de segmento acima desses limites. |
| Tamanho total do repositório de conteúdo <br>*(armazenamento de segmentos + armazenamento de dados)* | A ferramenta Transferência de conteúdo foi projetada para transferir conteúdo de até 20 TB para o tipo de armazenamento de dados Armazenamento de dados de arquivo. Atualmente, não há suporte para itens com mais de 20 TB. Crie um tíquete de suporte com o Atendimento ao cliente do Adobe para discutir as opções de conteúdo maior que 20 TB. <br>Para acelerar significativamente o processo de transferência de conteúdo para repositórios grandes, um [pré-cópia](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html#setting-up-pre-copy-step) etapa pode ser usada. Isso se aplica aos tipos de armazenamento de dados File Data Store, Amazon S3 e Azure Data Store. Para o Amazon S3 e o Azure Data Store, há suporte para tamanhos de repositório maiores que 20 TB. |
| Tamanho total do índice Lucene | Tamanho total do índice Lucene de 25 GB, excluindo `/oak:index/lucene` e `/oak:index/damAssetLucene` O é compatível no momento. Crie um tíquete de suporte com o Atendimento ao cliente do Adobe para discutir as opções de tamanho de índice acima desse limite. |
| Comprimento do nome do nó | O comprimento do nome de um nó deve ser de 150 bytes ou menos quando o caminho pai do nó for >= (igual ou maior do que) 350 bytes. Esses nomes de nó devem ser encurtados para &lt;= 150 bytes para serem compatíveis com o armazenamento de nó do documento no AEM as a Cloud Service. As assimilações falharão se esses nomes de nó longos não forem corrigidos. |
| Conteúdo em caminhos imutáveis | A ferramenta Transferência de conteúdo não pode ser usada para migrar conteúdo em caminhos imutáveis. Para transferir o conteúdo de `/etc` apenas certas `/etc` é permitido selecionar caminhos, mas somente para dar suporte a [AEM Forms para AEM Forms as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/migrate-to-forms-as-a-cloud-service.html#paths-of-various-aem-forms-specific-assets). Para todos os outros casos de uso, consulte [Reestruturação do repositório comum](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/restructuring/all-repository-restructuring-in-aem-6-5.html) para saber mais sobre reestruturação de repositório. |
| Valor da propriedade do nó no MongoDB | Os valores de propriedade do nó armazenados no MongoDB não podem exceder 16MB. Isso é aplicado pelo MongoDB. As assimilações falharão se houver valores de propriedade maiores que esse limite. Antes de executar uma extração, execute este [oak-run](https://repo1.maven.org/maven2/org/apache/jackrabbit/oak-run/1.38.0/oak-run-1.38.0.jar) script. Revise todos os valores de propriedade grandes e valide se eles são necessários. Os que excederem 16MB precisarão ser convertidos em valores Binários. |

## O que vem a seguir {#whats-next}

Depois de analisar os pré-requisitos e determinar se você pode usar a ferramenta Transferência de conteúdo no projeto de migração, consulte [Diretrizes e práticas recomendadas para usar a ferramenta Transferência de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html).
