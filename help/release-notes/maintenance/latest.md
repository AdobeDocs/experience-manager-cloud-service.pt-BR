---
title: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: b83d8736d47778ed133e0cc07207e02e581bbc69
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 17%

---


# Notas da versão de manutenção {#maintenance-release-notes}

A seção a seguir descreve as notas de versão técnicas para a versão de manutenção atual do Experience Manager as a Cloud Service.

## Versão 24893 {#release-24893}

Veja abaixo um resumo das melhorias contínuas da versão de manutenção 24893, lançada publicamente em quarta-feira, 17 de março de 2026. A versão de manutenção anterior era 24678.

A ativação de recursos do 2026.3.0 fornecerá o conjunto completo de recursos para esta versão de manutenção. Consulte o [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/pt-br/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obter mais informações.

### Aprimoramentos {#enhancements-24893}

* CNTBF-613: Acesso de correção negado (JCR-101) - falha ao registrar tipos de nó.
* GRANITE-53957: atualize o Azure SDK V8 para V12 para oak-blob-azure.
* GRANITE-57035: Use Bouncy Castle como provedor de segurança padrão.
* GRANITE-59249: Evite registrar um provedor de segurança na JVM.
* GRANITE-61564: Falha ao abrir configurações de exibição em `/security/users.html` para administradores.
* GRANITE-64748: OIDC: expiração do cookie `sling.oauth-request-key` configurável.
* SITES-39767: suporte ao valor nonce por meio do atributo de solicitação (CSP).
* SKYOPS-129301: Defina o nível de conformidade jar javadoc das APIs como 17.
* GRANITE-64962: atualize o Apache Jackrabbit Oak para 1.92.0.
* GRANITE-64963: atualização do Apache Jackrabbit Filevault para a versão 4.2.0.
* GRANITE-64764: Atualização do texto do Apache Commons para a versão 1.15.0.
* SKYOPS-131412: Atualização do Apache Commons Exec para 1.6.0.
* SKYOPS-131432: Atualização de Felix SCR para 2.2.14.
* SKYOPS-131907: Atualização da Região da API Sling para 1.1.10.
* SKYOPS-131938: Atualização do GSON para 2.13.2.
* SKYOPS-132173: Atualização do Apache Commons Codec para 1.21.0.
* SKYOPS-132182: Atualização do Locatário do Sling para 1.1.8.
* SKYOPS-132267: Atualização de org.osgi.service.component para 1.5.1.
* SKYOPS-132272: Atualização do Modelo de Recurso do Sling para 2.0.4.
* SKYOPS-133689: Atualize o Dispatcher para usar o Apache httpd 2.4.66.

### Problemas corrigidos {#fixed-issues-24893}

* GRANITE-64443: `workflow.core` remova as exportações obsoletas de `log4j`.
* GRANITE-64543: a resposta de restrições de permissão deve corresponder ao contrato da API.

#### Guias do AEM {#guides-24893}

* GUIDES-38412 : Ao editar um arquivo do Schematron `(*.sch)` e usar o recurso localizar e substituir, o painel localizar e substituir aparece parcialmente fora da tela na parte inferior, impedindo o acesso aos campos e controles de entrada.
* GUIDES-37806: Quando o mesmo tópico é reutilizado em vários mapas com diferentes predefinições condicionais, a publicação do mapa mais recente no Salesforce substitui o conteúdo do tópico, resultando na exibição de dados incorretos para os usuários de mapas publicados anteriormente.
* GUIDES-39394: Quando uma imagem gerenciada inicialmente como um ativo específico de idioma com uma versão específica (por exemplo, em `/en/`) é movida para uma pasta global com uma versão atualizada e a exportação da linha de base é executada, a nova linha de base continua a fazer referência a versões desatualizadas específicas do idioma dessa imagem, resultando em uma falha na exportação da linha de base.
* GUIDES-39054: Ao criar uma linha de base dinâmica, o Editor às vezes fica sem responder devido a várias solicitações de API simultâneas, fazendo com que todas as outras operações travem.
* GUIDES-37781: Ao atribuir um usuário a uma tarefa de revisão, a lista suspensa lista todos os usuários em vez de apenas aqueles associados aos projetos selecionados, resultando em opções de usuário inválidas.
* GUIDES-39385: Ao abrir um Relatório para um mapa, há um atraso no carregamento do painel Filtros.

Para obter mais informações sobre recursos e problemas novos e aprimorados corrigidos nessa versão, exiba o [roteiro de versão do Experience Manager Guides](https://experienceleague.adobe.com/pt-br/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap).

### Problemas conhecidos {#known-issues-24893}

Nenhum.

### Recursos e APIs obsoletos {#deprecated-24893}

Os recursos e APIs obsoletos e removidos do AEM as a Cloud Service estão detalhados no documento [Recursos e APIs obsoletos e removidos](/help/release-notes/deprecated-removed-features.md).

### Correções de segurança {#security-24893}

A AEM as a Cloud Service dedica-se a otimizar a segurança e o desempenho da sua plataforma. Esta versão de manutenção aborda 9 vulnerabilidades identificadas, reforçando nosso compromisso com a proteção robusta do sistema.

### Tecnologias integradas {#embedded-tech-24893}

| Tecnologia | Versão | Link |
|---|---|---|
| AEM Oak | 1.92.0 | [API do Oak 1.92.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.92.0/index.html) |
| API DO SLING DO AEM | 2.27.6 | [API Apache Sling API 2.27.6](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| HTL do AEM | 1.4.28-1.4.0 | [Especificação da linguagem de modelo HTML](https://github.com/adobe/htl-spec) |
| Apache HTTP Server | 2.4.66 | [Apache Httpd 2.4.66](https://apache.googlesource.com/httpd/+/refs/tags/2.4.66/CHANGES) |
| Componentes principais do AEM | 2.30.4 | [Componentes principais de WCM do AEM](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14 (padrão) | [Versões Node.js com suporte](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |
