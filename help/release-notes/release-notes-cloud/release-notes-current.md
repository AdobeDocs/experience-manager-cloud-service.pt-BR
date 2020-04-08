---
title: Notas de versão para 2020.4.0
description: Notas de versão para 2020.4.0
translation-type: tm+mt
source-git-commit: 77163877bea36f854ac8ea6fbc78cbcf4d58ccc0

---


# Notas de versão para AEM as a Cloud Service 2020.4.0{#release-notes}

A seção a seguir descreve as Notas de versão gerais para Experience Manager as a Cloud Service 2020.4.0.

## Ativos {#assets}

Siga esta seção para saber mais sobre as novidades e as atualizações dos ativos Experience Manager e do Dynamic Media no AEM como uma versão 2020.4.0 do serviço de nuvem.

### Novidades {#assets-what-is-new}

* [O Brand Portal](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/home.html) está disponível para o AEM como ativos de serviço em nuvem, suportando casos de uso de distribuição de ativos. O Brand Portal auxilia as organizações a atender às suas necessidades de marketing, distribuindo com segurança os ativos de marca e produto aprovados a agências externas, parceiros, equipes internas e revendedores para download.
   * A configuração do Brand Portal é feita por meio do console de E/S da Adobe
   * A origem de ativos no Brand Portal ainda não é compatível com o AEM como um serviço em nuvem
* A nova versão do [Adobe Asset Link](https://helpx.adobe.com/br/enterprise/using/adobe-asset-link.html) 2.0 é compatível com o AEM como um serviço em nuvem. O Adobe Asset Link simplifica a colaboração entre criadores e comerciantes no processo de criação de conteúdo ao conectar os ativos AEM com aplicativos de desktop da Creative Cloud Photoshop, Illustrator e InDesign por meio do painel Link de ativos no aplicativo.
   * O AEM como um serviço em nuvem é pré-configurado para o Adobe Asset Link, o que resulta em configuração [](https://helpx.adobe.com/enterprise/using/configure-aem-assets-for-asset-link.html)simplificada.
   * O Link de ativos agora é compatível com um alternador [de ambientes](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html#UseAdobeAssetLink)AEM, permitindo que usuários criativos se conectem a diferentes ambientes AEM mais facilmente (por exemplo, no caso de designers de agências que trabalham com vários clientes com ativos AEM)
* O start automático para fluxos de trabalho de [pós-processamento](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows) pode ser configurado na interface do usuário de Propriedades da pasta para hierarquias de pastas específicas.
   * A interface do usuário de Propriedades da pasta foi simplificada, com a nova guia Processamento de ativos contendo Perfil de metadados, Perfil de processamento e a nova configuração de Fluxo de trabalho de Start automático
* A caixa de diálogo de reprocessamento de ativos permite selecionar um perfil de processamento específico e decidir reprocessar em subpastas
* Mídia dinâmica: Adicionada a configuração Publicação seletiva, o que significa que os ativos são publicados automaticamente apenas para pré-visualização segura e podem ser publicados explicitamente no AEM sem publicação no DMS7 para delivery no domínio público.

### Correções de erros {#assets-bug-fixes}

* Correções no processamento de ativos
* Correções na configuração do Dynamic Media e ativos de publicação no serviço delivery do Dynamic Media
