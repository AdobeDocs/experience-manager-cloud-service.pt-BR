---
title: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: d3cdc3d69c0002c5b124150050f905123457331c
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 29%

---


# Notas da versão de manutenção {#maintenance-release-notes}

A seção a seguir descreve as notas de versão técnicas para a versão de manutenção atual do Experience Manager as a Cloud Service.

## Versão 21193 {#21193}

Veja abaixo um resumo das melhorias contínuas da versão de manutenção 21193, lançada para o público em quarta-feira, 10 de junho de 2025. A versão de manutenção anterior era 21005.

A ativação de recursos do 2025.6.0 fornecerá o conjunto completo de recursos para esta versão de manutenção. Consulte o [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/pt-br/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obter mais informações.

### Aprimoramentos {#enhancements-21193}

* ASSETS-51245: desempenho aprimorado para listagens de pastas grandes na interface para toque.
* ASSETS-51686: melhorias no trabalho de operações em massa, incluindo cancelamento de trabalho mais fácil, registro aprimorado, downloads de auditoria para resultados grandes.
* CQ-4360131: resposta de erro aprimorada para endpoints OpenAPI, permitindo que os clientes da API recebam informações de erro estruturadas corretas.

### Problemas corrigidos {#fixed-issues-21193}

* ASSETS-41007: os ativos excluídos podem permanecer visíveis no Content Hub.
* ASSETS-50994: AemRequestEventFilter causando contenção excessiva de thread do Jetty.
* ASSETS-50155: eventos de alteração de metadados duplicados acionados.
* ASSETS-50716: A classificação por título na exibição de lista do Assets não funciona como esperado.
* ASSETS-50820: certifique-se de que solicitações inválidas da API de relações de ativos sejam rejeitadas corretamente com um erro 400.
* ASSETS-50562: a API de upload de ativos deve criar a versão por comportamento padrão em conflito de nomes.
* ASSETS-50992: O endpoint da API do Assets initiateUpload.json deve retornar o tipo de conteúdo de &quot;application/json&quot;.
* ASSETS-51322: Remoção e expiração automáticas de barricadas assíncronas que permanecem persistentes indefinidamente após uma falha de trabalho.
* ASSETS-51809: o editor de CSV não mostrou alterações salvas recentemente devido ao armazenamento em cache do navegador.
* SITES-31678: Fragmentos de experiência (XF) com referências sensíveis ao contexto não resolveram a raiz de idioma correta na API de publicação XF.


### Problemas conhecidos {#known-issues-21193}

Nenhum.

### Recursos e APIs obsoletos {#deprecated-21193}

Os recursos e APIs obsoletos e removidos do AEM as a Cloud Service estão detalhados no documento [Recursos e APIs obsoletos e removidos](/help/release-notes/deprecated-removed-features.md).

### Correções de segurança {#security-21193}

A AEM as a Cloud Service dedica-se a otimizar a segurança e o desempenho da sua plataforma. Esta versão de manutenção aborda duas vulnerabilidades identificadas, reforçando nosso compromisso com a proteção robusta do sistema.

### Tecnologias integradas {#embedded-tech-21193}

| Tecnologia | Versão | Link |
|---|---|---|
| AEM Oak | 1.80.0 | [API Oak API 1.80.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.80.0/index.html) |
| API DO SLING DO AEM | 2.27.6 | [API Apache Sling API 2.27.6](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| HTL do AEM | 1.4.28-1.4.0 | [Especificação da linguagem de modelo HTML](https://github.com/adobe/htl-spec) |
| Componentes principais do AEM | 2.29.0 | [Componentes principais de WCM do AEM](https://github.com/adobe/aem-core-wcm-components) |
