---
title: Pré-requisitos para a ferramenta Transferência de conteúdo
description: Pré-requisitos para a ferramenta Transferência de conteúdo
source-git-commit: 0d664997a66d790d5662e10ac0afd0dca7cc7fac
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 2%

---

# Pré-requisitos para a ferramenta Transferência de conteúdo {#prerequisites}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_prereqs"
>title="Considerações importantes sobre o uso da ferramenta Transferência de conteúdo"
>abstract="Analise considerações importantes para usar a ferramenta Transferência de conteúdo , incluindo versões de Java e AEM, tipos compatíveis de armazenamento de dados, considerações sobre grupos de usuários e muito mais."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#pre-reqs" text="Considerações importantes sobre o uso da ferramenta Transferência de conteúdo"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?lang=en#best-practices" text="Práticas recomendadas e diretrizes"

A tabela a seguir resume os pré-requisitos para usar a ferramenta Transferência de conteúdo .

Revise todas as considerações listadas abaixo:

| Considerações | O que é compatível no momento |
|--- |--- |
| Versão do AEM | A ferramenta Transferência de conteúdo pode ser executada somente no AEM 6.3 ou versões superiores. Para poder usar a ferramenta Transferência de conteúdo com AEM 6.2 ou versões mais antigas, é necessária uma atualização no local do repositório de conteúdo para AEM 6.5. Não é necessário atualizar o código para AEM 6.5 para isso. |
| Tamanho do armazenamento de segmentos | A ferramenta Transferência de conteúdo suporta atualmente até 83 GB em *Author* e 31 GB em *Publish*. |
| Tamanho total do repositório de conteúdo <br>*(armazenamento de segmentos + armazenamento de dados)* | A ferramenta Transferência de conteúdo foi criada para transferir conteúdo de até 10 TB. Qualquer coisa superior a 10 TB não é compatível no momento. Crie um tíquete de suporte com o Atendimento ao cliente do Adobe para discutir opções de conteúdo maior que 10 TB. |
| Conteúdo em caminhos imutáveis | A ferramenta Transferência de conteúdo não pode ser usada para migrar o conteúdo em caminhos imutáveis, como `“/etc”`. Há determinados caminhos `"/etc"` permitidos a serem selecionados, mas somente para suportar [AEM Forms para AEM Forms como Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/migrate-to-forms-as-a-cloud-service.html?lang=en#paths-of-various-aem-forms-specific-assets). Para todos os outros casos de uso, consulte [Restruturação de Repositório Comum](https://experienceleague.adobe.com/docs/experience-manager-64/deploying/restructuring/all-repository-restructuring-in-aem-6-4.html?lang=en#restructuring) para saber mais sobre a reestruturação de repositório. |

## O que vem a seguir {#whats-next}

Depois de revisar os pré-requisitos e determinar se você pode usar a ferramenta Transferência de conteúdo no projeto de migração, consulte [Práticas recomendadas e considerações adicionais](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md) ao usar a ferramenta Transferência de conteúdo.
