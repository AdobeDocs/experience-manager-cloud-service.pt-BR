---
title: Problemas conhecidos
description: Notas de versão específicas dos problemas conhecidos do Adobe Experience Manager como um serviço em nuvem
translation-type: tm+mt
source-git-commit: 82dd9bd69fe994f74c7be8a571e386f0e902f6a1

---


# Problemas conhecidos {#known-issues}

Este artigo lista os problemas conhecidos do Adobe Experience Manager como uma oferta de serviço em nuvem. A lista é revisada e atualizada com cada versão contínua do Experience Manager.

[Entre em contato com o suporte](https://helpx.adobe.com/support/experience-manager.html) para obter mais informações sobre os problemas conhecidos.

<!-- 
## Platform {#platform}

## Sites {#sites}
-->

## Assets {#assets}

<!-- Jira label: assets-cloud-known-issues -->

Alguns problemas conhecidos são:

* **Esquema** de metadados: O widget de classificação de ativos pode causar erro de compilação JSP. Uma solução alternativa é remover o componente de classificação de ativos do esquema de metadados. <!-- CQ-4282865 -->

Algumas limitações da funcionalidade Ativos são:

* Com os ativos AEM como um serviço em nuvem, a funcionalidade dos ativos conectados funciona quando os sites do AEM 6.5 são implantados no AMS.

### Recursos dos ativos futuros {#upcoming-assets-capabilities}

Espera-se que alguns recursos dos ativos Adobe Experience Manager que dependem dos recursos básicos, que ainda não estão disponíveis no Experience Manager como uma arquitetura de implantação do serviço em nuvem, sejam ativados posteriormente:

* A publicação no Brand Portal não está ativada neste estágio. Você pode estender e implantar a implementação do [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/) para casos de uso da distribuição de ativos.
* A funcionalidade aprimorada de marcação inteligente que aproveita os serviços de IA da E/S da Adobe não está disponível por enquanto.
* Recursos não ativados neste estágio devido à dependência das APIs do Commerce Integration Framework:
   * Modelos de fluxo de trabalho de fotos.
   * A guia Informações do produto na interface do usuário das propriedades do ativo não é preenchida.
* Recursos não ativados neste estágio devido à dependência da integração do InDesign Server:
   * Modelos de ativos e Catálogos de ativos.
   * Visualização de várias páginas de arquivos do InDesign.

>[!MORELIKETHIS]
>
>* [Alterações importantes no AEM](aem-cloud-changes.md)
>* [Recursos obsoletos e removidos](deprecated-removed-features.md)
>* [Notas de versão](home.md)

