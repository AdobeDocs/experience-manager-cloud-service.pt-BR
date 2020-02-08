---
title: Migrar para o serviço em nuvem do Adobe Experience Manager 6.x
description: Migrar para o serviço em nuvem do Adobe Experience Manager 6.x
contentOwner: AG
translation-type: tm+mt
source-git-commit: 991d4900862c92684ed92c1afc081f3e2d76c7ff

---


# Mover para os ativos Adobe Experience Manager como um serviço em nuvem {#move-to-assets-cloud-service}

<!-- About the need to move from previous AEM deployment to a cloud service deployment. And how does Adobe help do it OOTB?
-->

## Sobre a ferramenta de migração {#migration-tool}

<!-- 
Link back to information about the tool in the Experience Manager as a Cloud Service docs if the tool works the same for Sites and Assets. Document the Assets-specific information here.

* What is the migration tool called? Is there a branding term for it?
* How much do we want to elaborate about the Pattern Detector rules? Is there a branding term for it?
* Before migrating using the tool, is any prepping required?
* See CQ-4271901

-->

A ferramenta de migração ajuda você a obter o seguinte:

* Converta os modelos de fluxo de trabalho existentes em perfis de processamento que funcionam com o Assets Compute Service.
* Remova etapas não compatíveis dos modelos de fluxo de trabalho.
* Desabilitar iniciadores de fluxo de trabalho.
* Mesclar as configurações, após a confirmação/validação do usuário, no código-fonte existente.

A ferramenta de migração cria perfis de processamento em um módulo Maven que os usuários podem usar das duas maneiras a seguir:

* Mesclar em um dos projetos existentes.
* Adicione o módulo como novo submódulo.

A ferramenta de migração fornece um relatório das alterações feitas e informações sobre elas.

<!--  

What is the output of the tool, besides migrated content.

Give details about reports and logs of the tool. 

* How to access the report, including required permissions.
* How to read/interpret the report.
* Location of logs. How to read the logs.
* What common errors to look for. Troubleshooting for these errors.

-->

## Migrar conteúdo para uma nova implantação {#content-migration-across-deployments}
