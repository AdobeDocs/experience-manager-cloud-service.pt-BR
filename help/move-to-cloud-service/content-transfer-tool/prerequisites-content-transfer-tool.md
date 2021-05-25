---
title: Pré-requisitos para a ferramenta Transferência de conteúdo
description: Pré-requisitos para a ferramenta Transferência de conteúdo
source-git-commit: c760b97cdb565244cf20f5193de3e3ebab1579ad
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 1%

---

# Pré-requisitos para a ferramenta Transferência de conteúdo {#prerequisites}

A tabela a seguir resume os pré-requisitos antes de usar a ferramenta Transferência de conteúdo . Revise todas as considerações listadas abaixo:

| Considerações | O que é compatível no momento |
|--- |--- |
| Versão do AEM | A ferramenta Transferência de conteúdo pode ser executada somente no AEM 6.3 ou versões superiores. Para poder usar a ferramenta Transferência de conteúdo com AEM 6.2 ou versões mais antigas, é necessária uma atualização no local do repositório de conteúdo para AEM 6.5. Não é necessário atualizar o código para AEM 6.5 para isso. |
| Tamanho do armazenamento de segmentos | A ferramenta Transferência de conteúdo suporta atualmente até 83 GB em *Author* e 31 GB em *Publish*. |
| Tamanho total do repositório de conteúdo (armazenamento de conteúdo + armazenamento de dados) | A ferramenta Transferência de conteúdo foi criada para transferir conteúdo de até 10 TB. Qualquer coisa superior a 10 TB não é compatível no momento. Crie um tíquete de suporte com o Atendimento ao cliente do Adobe para discutir opções de conteúdo maior que 10 TB. |
| Conteúdo em caminhos imutáveis | A ferramenta Transferência de conteúdo não funciona para migrar o conteúdo em caminhos imutáveis, como `“/etc”`. Consulte [Restruturação de Repositório Comum](https://experienceleague.adobe.com/docs/experience-manager-64/deploying/restructuring/all-repository-restructuring-in-aem-6-4.html?lang=en#restructuring) para saber mais sobre a reestruturação de repositório e os modelos de fluxo de trabalho. |