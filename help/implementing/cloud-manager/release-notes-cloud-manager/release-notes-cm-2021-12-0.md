---
title: Notas de versão do Cloud Manager AEM versão as a Cloud Service 2021.12.0
description: Estas são as notas de versão do Cloud Manager AEM as a Cloud Service versão 2021.12.0.
feature: Release Information
exl-id: ee920bc5-cad7-4fac-bf73-bc1178699f90
source-git-commit: 1b7183421b9acd30697f1dc228dd9e2728d24ba6
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 1%

---

# Notas de versão do Cloud Manager no Adobe Experience Manager as a Cloud Service 2021.12.0 {#release-notes}

Esta página descreve as notas de versão do Cloud Manager AEM as a Cloud Service 2021.12.0.

>[!NOTE]
>
>Consulte [esta página](/help/release-notes/release-notes-cloud/release-notes-current.md) para obter as notas de versão atuais do Adobe Experience Manager as a Cloud Service.

## Data de lançamento {#release-date}

A data de lançamento do Cloud Manager AEM as a Cloud Service 2021.12.0 é 16 de dezembro de 2021. A próxima versão está planejada para 20 de janeiro de 2022.

## Novidades {#what-is-new}

* O hash de confirmação, que já está visível na interface do usuário, agora também é fornecido na API.
* A página Atividade agora inclui um pop-up para a execução de pipelines que fornece um resumo dos detalhes do pipeline imediatamente.
* Foram adicionadas atualizações para incluir detalhes adicionais apresentados na página Atividades.
* A guia Aprendizagem no Cloud Manager agora inclui acesso rápido aos guias da API e aos recursos associados.
* Um usuário com a função Deployment Manager agora pode iniciar o assistente de criação de Projeto/Ramificação para um repositório sem ramificações no menu de ação na página Repositórios.
* O Gerenciador de implantação, que está no fluxo de trabalho de adicionar ou editar pipeline, agora é informado sobre como criar uma ramificação ou projeto se o repositório selecionado não tiver ramificações.
* Um novo recurso de autoatendimento do Cloud Manager foi adicionado para permitir [adicionar variáveis e segredos de forma livre no nível do ambiente.](/help/implementing/cloud-manager/environment-variables.md)
* Com o novo [Complemento de Demonstrações de Referência](/help/journey-sites/demos-add-on/overview.md) (disponível em 17 de dezembro de 2021), as bases de código de demonstração mais recentes para AEM produtos podem ser instaladas e estar prontas para serem implantadas através do novo [ferramenta de criação rápida de sites](/help/journey-sites/quick-site/overview.md) em Sites.
* Os pipelines de front-end agora oferecem suporte a variáveis de pipeline.
* As telas agora podem ser ativadas na caixa de diálogo Editar programa para todas as sandboxes.
* As orientações fornecidas pelo cartão de chamada para ação na página de visão geral foram atualizadas para refletir precisamente sua associação com o pipeline de pilha completa de produção.
* Aprimoramentos na página Atividade foram adicionados à superfície detalhes adicionais aplicáveis a pipelines, incluindo código-fonte, ID de confirmação, etc.
* Pequenas atualizações foram feitas na interface do usuário ao copiar entradas TXT (&quot;valor TXT&quot; em vez de &quot;registro TXT&quot;) para remover uma possível confusão.
* [A documentação relacionada aos erros de certificado](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md#certificate-errors) O foi atualizado para cobrir mais exemplos, juntamente com etapas de solução de problemas.
* Uma opção agora está disponível na execução do pipeline de front-end para rejeitar ou aprovar antes da implantação para produção.
* A versão do AEM Project Archetype usada pelo Cloud Manager foi atualizada para a versão 32.


## Correções de erros {#bug-fixes}

* Os artefatos de teste funcionais e de interface do usuário não foram incluídos no log de etapas da compilação.
* Os registros das etapas de teste do produto, funcional e interface do usuário não eram acessíveis por meio da API pública.
* Em casos raros, o link da página de detalhes do ambiente para o serviço de publicação ou visualização não funcionaria.
* Os pipelines de produção de pilha completa permanecem nomeados como &quot;Pipeline de produção&quot; mesmo quando o usuário insere um nome diferente no campo de nome.
