---
title: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 82b3b4bdcd09aa86974518f4f62e73c9f377c83f
workflow-type: tm+mt
source-wordcount: '777'
ht-degree: 14%

---


# Notas da versão de manutenção {#maintenance-release-notes}

A seção a seguir descreve as notas de versão técnicas para a versão de manutenção atual do Experience Manager as a Cloud Service.

## Versão 25821 {#release-25821}

Resumidos abaixo estão as melhorias contínuas da versão de manutenção 25821, que foi lançada publicamente em 5 de maio de 2026. A versão de manutenção anterior era 25520.

A ativação de recursos do 2026.5.0 fornecerá o conjunto completo de recursos para esta versão de manutenção. Consulte o [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obter mais informações.

### Aprimoramentos {#enhancements-25821}

* CQ-4362304: crie o front-end de diretrizes e atualize a interface de configuração do LLM.
* GRANITE-39546: atualize o Apache Tika para 3.x.
* GRANITE-53957: atualize o Azure SDK V8 para V12 para oak-blob-azure.
* GRANITE-61245: remova todo o uso de commons-lang (substitua por commons-lang3).
* GRANITE-64748: manipulador de autenticação Bump OIDC.
* GRANITE-64764: atualização do texto Apache Commons para 1.15.0.
* GRANITE-64963: atualização do Filevault para 4.2.0.
* GRANITE-66197: adicione o suporte por email da API Graph do Microsoft para locatários M365.
* GRANITE-66449: atualização dos plug-ins Maven para suporte à API Java 17.
* GRANITE-66473: adicione a biblioteca de cache do Caffeine ao base-granite.
* GRANITE-66836: atualize o Quickstart para o Oak 2.0.0.
* SKYOPS-129301: Defina o nível de conformidade jar Javadoc das APIs para Java 17.
* SKYOPS-129351: Atualize fluxos reativos e núcleo do reator para obter compatibilidade com o MCP SDK.
* SKYOPS-131412: Atualize o Apache Commons Exec para a versão mais recente.
* SKYOPS-131432: Atualização de Felix SCR para 2.2.14.
* SKYOPS-131907: Atualização das regiões da API Sling para 1.1.10.
* SKYOPS-131938: Atualize o GSON para a versão mais recente.
* SKYOPS-132173: Atualize o Apache Commons Codec para a versão mais recente.
* SKYOPS-132182: Atualizar conjunto de locatários do Sling.
* SKYOPS-132267: Atualização da anotação `org.osgi.service.component`.
* SKYOPS-132272: Atualização do pacote do Modelo de recurso do Sling.
* SKYOPS-132525: adicione o Quickstart analyzer para evitar novas remoções de API.
* SKYOPS-134408: Atualização `com.adobe.granite.asset.core` para 2.2.82.
* SKYOPS-137750: Atualização `com.adobe.granite.comments` para 1.0.40.
* SKYOPS-137759: Atualização `com.adobe.granite.jobs.async.ui.commons` para 3.2.4.
* SKYOPS-138356: Atualização `com.adobe.granite.oauth.server` para 1.1.36.
* SKYOPS-138739: Atualização do SnakeYAML para 2.6.

### Problemas corrigidos {#fixed-issues-25821}

* ASSETS-59546: remova as dependências da biblioteca commons-lang obsoleta.
* ASSETS-64831: a contagem de tentativas de redefinição de AssetProcessorProcess causa ativos travados.
* ASSETS-66683: Loop de aprovação causado pela falha de uploadBlob.
* CNTBF-613: Acesso de Correção Negado (JCR-101) ao registrar tipos de nó.
* GRANITE-44537: cadeia de caracteres em &quot;País/Região&quot; não localizada na AEM.
* GRANITE-61760: falha na ativação do AdminUserInitializer para correção.
* GRANITE-64543: a resposta de restrições de permissão não segue a estrutura da API.
* GRANITE-66692: carregador de classe interno não sensível a atualizações de pacote.
* GRANITE-66732: use ativadores em vez de componentes de serviço para pacotes de nível 1 iniciais.
* GRANITE-66846: a API de permissões do AEM não mostra a restrição `rep:ntNames`.
* SITES-39267: restaure pagePath em entradas da cadeia de relacionamento.
* SITES-43715: A validação de permissão falha ao ler o status do recurso.

#### Guias do AEM {#guides-25821}

* GUIDES-45110: Ao selecionar uma imagem no Editor usando a caixa de diálogo **Selecionar arquivo**, somente os formatos de varredura (como JPG, PNG e GIF) são exibidos. Arquivos de vetor (como `.ai` e `.eps`) não são exibidos e não podem ser selecionados.
* GUIDES-41938: A criação de um tópico em uma pasta com espaços em seu nome cria incorretamente uma pasta duplicada em que os espaços são substituídos por hifens e o tópico é salvo lá, em vez da pasta original.
* GUIDES-38377: Quando alterações em uma predefinição de saída em um perfil de Pasta são aplicadas a mapas existentes, o **Contexto de Publicação** salvo para a predefinição do AEM Sites é redefinido.
* GUIDES-43547: Quando tópicos ou mapas grandes são abertos, a instância do Autor fica sem resposta, exigindo uma reinicialização em alguns casos.
* GUIDES-32520: Quando o Backspace é usado em elementos, o Editor rola para a parte superior do tópico, independentemente da posição do cursor (Editor 2.0).

Para obter mais informações sobre recursos e problemas novos e aprimorados corrigidos nessa versão, exiba o [roteiro de versão do Experience Manager Guides](https://experienceleague.adobe.com/en/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap).

### Problemas conhecidos {#known-issues-25821}

Nenhum.

### Recursos e APIs obsoletos {#deprecated-25821}

Os recursos e APIs obsoletos e removidos do AEM as a Cloud Service estão detalhados no documento [Recursos e APIs obsoletos e removidos](/help/release-notes/deprecated-removed-features.md).

### Correções de segurança {#security-25821}

A AEM as a Cloud Service dedica-se a otimizar a segurança e o desempenho da sua plataforma. Esta versão de manutenção aborda 19 vulnerabilidades identificadas, reforçando nosso compromisso com a proteção robusta do sistema.

### Tecnologias integradas {#embedded-tech-25821}

| Tecnologia | Versão | Link |
|---|---|---|
| AEM Oak | 2.0.0 | [API do Oak 2.0.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/2.0.0/index.html) |
| API DO SLING DO AEM | 2.27.6 | [API Apache Sling API 2.27.6](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| HTL do AEM | 1.4.28-1.4.0 | [Especificação da linguagem de modelo HTML](https://github.com/adobe/htl-spec) |
| Apache HTTP Server | 2.4.65 | [Apache Httpd 2.4.65](https://apache.googlesource.com/httpd/+/refs/tags/2.4.65/CHANGES) |
| Componentes principais do AEM | 2.30.4 | [Componentes principais de WCM do AEM](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14 (padrão) | [Versões Node.js com suporte](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |
