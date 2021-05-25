---
title: Pré-requisitos para a ferramenta Transferência de conteúdo
description: Pré-requisitos para a ferramenta Transferência de conteúdo
source-git-commit: f70959efd9d0382c083ac05b9ccd63cf79947bc2
workflow-type: tm+mt
source-wordcount: '222'
ht-degree: 0%

---

# Pré-requisitos para a ferramenta Transferência de conteúdo {#prerequisites}

A tabela a seguir resume os pré-requisitos para usar a ferramenta Transferência de conteúdo .

Revise todas as considerações listadas abaixo:

| Considerações | O que é compatível no momento |
|--- |--- |
| Versão do AEM | A ferramenta Transferência de conteúdo pode ser executada somente no AEM 6.3 ou versões superiores. Para poder usar a ferramenta Transferência de conteúdo com AEM 6.2 ou versões mais antigas, é necessária uma atualização no local do repositório de conteúdo para AEM 6.5. Não é necessário atualizar o código para AEM 6.5 para isso. |
| Tamanho do armazenamento de segmentos | A ferramenta Transferência de conteúdo suporta atualmente até 83 GB em *Author* e 31 GB em *Publish*. |
| Tamanho total do repositório de conteúdo <br>*(armazenamento de conteúdo + armazenamento de dados)* | A ferramenta Transferência de conteúdo foi criada para transferir conteúdo de até 10 TB. Qualquer coisa superior a 10 TB não é compatível no momento. Crie um tíquete de suporte com o Atendimento ao cliente do Adobe para discutir opções de conteúdo maior que 10 TB. |
| Conteúdo em caminhos imutáveis | A ferramenta Transferência de conteúdo não funciona para migrar o conteúdo em caminhos imutáveis, como `“/etc”`. <br>Consulte  [Reestruturação ](https://experienceleague.adobe.com/docs/experience-manager-64/deploying/restructuring/all-repository-restructuring-in-aem-6-4.html?lang=en#restructuring) comum de repositório para saber mais sobre a reestruturação de repositório e os modelos de fluxo de trabalho. |

## O que vem a seguir {#whats-next}

Depois de revisar os pré-requisitos, você pode aprender a executar a ferramenta Transferência de conteúdo. Consulte [Usar a ferramenta Transferência de conteúdo](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md) para obter mais detalhes.
