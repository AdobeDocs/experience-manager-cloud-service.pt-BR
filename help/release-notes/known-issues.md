---
title: Problemas conhecidos
description: Notas de versão específicas para os problemas conhecidos do Adobe Experience Manager as a Cloud Service
translation-type: ht
source-git-commit: 82dd9bd69fe994f74c7be8a571e386f0e902f6a1

---


# Problemas conhecidos {#known-issues}

Este artigo lista os problemas conhecidos da oferta do Adobe Experience Manager as a Cloud Service. A lista é revisada e atualizada a cada versão contínua do Experience Manager.

[Entre em contato com o suporte](https://helpx.adobe.com/support/experience-manager.html) para obter mais informações sobre os problemas conhecidos.

<!-- 
## Platform {#platform}

## Sites {#sites}
-->

## Ativos {#assets}

<!-- Jira label: assets-cloud-known-issues -->

Alguns problemas conhecidos são:

* **Esquema de metadados**: o dispositivo de classificação de ativos pode causar erro de compilação de JSP. Uma solução alternativa é remover o componente de classificação de ativos do esquema de metadados. <!-- CQ-4282865 -->

Algumas limitações da funcionalidade do Assets são:

* Com o AEM Assets as a Cloud Service, a funcionalidade Connected Assets funciona quando o AEM 6.5 Sites é implantado no AMS.

### Futuros recursos do Assets {#upcoming-assets-capabilities}

Espera-se que alguns recursos do Adobe Experience Manager Assets que dependem dos recursos básicos, que ainda não estão disponíveis na arquitetura de implantação do Experience Manager as a Cloud Service, sejam ativados posteriormente:

* A publicação no Brand Portal não está ativada no momento. Você pode estender e implantar a implementação do [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/) para casos de uso de distribuição de ativos.
* A funcionalidade aprimorada de marcação inteligente que usa os serviços de IA de E/S da Adobe não está disponível por enquanto.
* Recursos não ativados no momento devido à dependência das APIs da Estrutura de integração do comércio:
   * Modelos de fluxo de trabalho da sessão de fotos.
   * A guia Informações do produto na interface do usuário das propriedades do ativo não foi preenchida.
* Recursos não ativados no momento devido à dependência da integração do InDesign Server:
   * Modelos de ativos e catálogos de ativos.
   * Visualização de várias páginas dos arquivos de InDesign.

>[!MORELIKETHIS]
>
>* [Alterações importantes no AEM](aem-cloud-changes.md)
>* [Recursos obsoletos e removidos](deprecated-removed-features.md)
>* [Notas de versão](home.md)

