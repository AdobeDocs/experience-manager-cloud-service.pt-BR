---
title: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 6884e33a922a7147e3a6a3f3ddb3dd3b2da85fbf
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 20%

---


# Notas da versão de manutenção {#maintenance-release-notes}

A seção a seguir descreve as notas de versão técnicas para a versão de manutenção atual do Experience Manager as a Cloud Service.

## Versão 21005 {#21005}

Veja abaixo um resumo das melhorias contínuas da versão de manutenção 21005, lançada publicamente em quarta-feira, 27 de maio de 2025. A versão de manutenção anterior era 20626.

A ativação de recursos do 2025.5.0 fornecerá o conjunto completo de recursos para esta versão de manutenção. Consulte o [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obter mais informações.

### Aprimoramentos {#enhancements-21005}

* GRANITE-58927: melhorias no botão Pesquisa semântica.
* GRANITE-58800: Atualização das coleções do Apache Commons para a versão 4.5.0.
* GRANITE-58866: atualização do Oak para 1.80.0.
* SKYOPS-106509: Compatibilidade de GSON aprimorada por meio do acesso reflexivo no Java 21.
* SKYOPS-107761: Atualização do Exportador Sling Models Jackson para 1.1.6.
* SKYOPS-107813: Atualização para Sling ResourceResolver 1.12.8.

### Problemas corrigidos {#fixed-issues-21005}

* CNTBF-443: propriedade `EVENT_JOB_TOPIC` SearchSlingJob corrigida.
* GRANITE-57853: corrigidos problemas de alinhamento suspenso na interface do usuário.
* GRANITE-58107: correção de erros 404 na publicação ao desativar a afinidade de pod baseada em usuário no manipulador OAuth.
* GRANITE-58276, SLING-12755: correção dos ciclos de dependência OSGi que poderiam impedir que a fábrica do mecanismo de script HTL fosse iniciada corretamente, causando erros intermitentes de renderização do lado do servidor.
* SKYOPS-105151: NPE corrigido ao acessar a lista de pacotes.
* SKYOPS-83910, SKYOPS-82371 - Correção de problemas de simultaneidade de compilação JSP.

#### Guias do AEM {#guides}

* GUIDES-26919 : Ao abrir um mapa DITA com o Unified Shell ativado, o editor é atualizado intermitentemente.
* GUIDES-26282: Falha ao fechar conexões de sessão JCR ao atualizar ou criar tópicos resulta em vazamentos de memória e tempo de inatividade do serviço.
* GUIDES-26434: A publicação no PDF nativo continua indefinidamente, se o conteúdo DITA tiver um link da Web sem ter o escopo `external`.
* GUIDES-26516: A publicação de PDFs nativos e sites do AEM é interrompida e colocada em fila quando há erros no conteúdo.

Para obter mais informações sobre recursos e problemas novos e aprimorados corrigidos nessa versão, exiba o [roteiro de versão do Experience Manager Guides](https://experienceleague.adobe.com/en/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap).

### Problemas conhecidos {#known-issues-21005}

Nenhum.

### Recursos e APIs obsoletos {#deprecated-21005}

* GRANITE-54164: `org.apache.jackrabbit.oak.plugins.blob` removido da API pública.
* GRANITE-54280: `org.apache.jackrabbit.oak.cache` removido da API pública.
* GRANITE-58332: `org.apache.jackrabbit.oak.plugins.memory` obsoleto na API pública.
* O compactador YUI para javascript foi descontinuado.
* A funcionalidade [Automação de Instalação do Experience Cloud](/help/sites-cloud/integrating/adobe-analytics-exc-setup-automation.md) foi descontinuada.

Os recursos e APIs obsoletos e removidos do AEM as a Cloud Service estão detalhados no documento [Recursos e APIs obsoletos e removidos](/help/release-notes/deprecated-removed-features.md).

### Correções de segurança {#security-21005}

A AEM as a Cloud Service dedica-se a otimizar a segurança e o desempenho da sua plataforma. Esta versão de manutenção aborda cinco vulnerabilidades identificadas, reforçando nosso compromisso com a proteção robusta do sistema.

### Aviso de mudança {#change-notice-21005}

* Esta versão inclui as seguintes novas versões do índice de produtos:
   * **damAssetLucene-12**

As versões personalizadas das versões de índice anteriores serão mescladas automaticamente com a nova versão do índice do produto. Aplique mais atualizações personalizadas à versão mesclada.

#### Atualizar aem-cloud-testing-clients {#update-aem-cloud-testing-clients-21005}

As próximas alterações exigirão que a biblioteca [aem-cloud-testing-clients](https://github.com/adobe/aem-testing-clients) usada em seus testes funcionais personalizados seja atualizada para pelo menos a versão **1.2.1** (Recomendado: versão mais recente 1.2.9)

Verifique se sua dependência em `it.tests/pom.xml` foi atualizada.

```xml
<dependency>
   <groupId>com.adobe.cq</groupId>
   <artifactId>aem-cloud-testing-clients</artifactId>
   <version>1.2.9</version>
</dependency>
```

Essa alteração precisa ser executada antes de 15 de junho de 2025.
Falha ao atualizar a biblioteca de dependências resultará em falhas de pipeline na etapa &quot;Teste funcional personalizado&quot;.

### Tecnologias integradas {#embedded-tech-21005}

| Tecnologia | Versão | Link |
|---|---|---|
| AEM Oak | 1.80.0 | [API Oak API 1.80.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.80.0/index.html) |
| API DO SLING DO AEM | 2.27.6 | [API Apache Sling API 2.27.6](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| HTL do AEM | 1.4.28-1.4.0 | [Especificação da linguagem de modelo HTML](https://github.com/adobe/htl-spec) |
| Componentes principais do AEM | 2.29.0 | [Componentes principais de WCM do AEM](https://github.com/adobe/aem-core-wcm-components) |
