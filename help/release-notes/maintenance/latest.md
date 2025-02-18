---
title: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 1d6a54f87d55179c11c7ccc7766eeeb475674f05
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 25%

---


# Notas da versão de manutenção {#maintenance-release-notes}

A seção a seguir descreve as notas de versão técnicas para a versão de manutenção atual do Experience Manager as a Cloud Service.

## Versão 19567 {#19567}

Veja abaixo um resumo das melhorias contínuas da versão de manutenção 19567, lançada publicamente em quarta-feira, 18 de fevereiro de 2025. A versão de manutenção anterior foi a de 19352.

A ativação de recursos do 2025.2.0 fornecerá o conjunto completo de recursos para esta versão de manutenção. Consulte o [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obter mais informações.

### Aprimoramentos {#enhancements-19567}

* GRANITE-56650: a distribuição de conteúdo só deve sinalizar fila bloqueada após algumas tentativas
* SKYOPS-89616: Permitir a Criação de até 40 Contas Técnicas no Adobe Developer Console

### Problemas corrigidos {#fixed-issues-19567}

* CNTBF-232: pacote profundo nt:nós de arquivo para incluir obrigatório jcr:content child
* CQ-4358930: problema de desempenho durante o carregamento das propriedades da página com vários campos
* GRANITE-55960: problema de desempenho com o campo Coral Select no AEM as Cloud Service
* GRANITE-56197: a nova etapa do fluxo de trabalho TreeActivation não agrupa ativos em lote em uma estrutura de pasta simples grande

#### Guias do AEM {#guides}

* GUIDES-23526: Ao atualizar condições do perfil da pasta, todos os grupos de condição são perdidos e as condições são niveladas.
* GUIDES-22574: Se um link externo contiver uma UUID, ele entrará no pós-processamento e converterá o link externo em link UUID, quebrando assim o link no editor e também nos sites de publicação.
* GUIDES-24983: Ao copiar uma imagem de qualquer produto externo (por exemplo, MS PowerPoint) e colá-la no Guides, a funcionalidade de fazer upload do ativo em tempo real para uso no arquivo do é interrompida.
* GUIDES-21772: Falha na geração de PDF nativo para conteúdo com **atributo de parte** definido como **para conteúdo**.
* GUIDES-23964: Ao escolher **Editar propriedades**, a caixa de diálogo da linha de base não mostra os critérios salvos anteriormente para a linha de base dinâmica.
* GUIDES-19067: Ao duplicar qualquer perfil de pasta, a lista de usuários administradores também é copiada do perfil da pasta original

Para obter mais informações sobre recursos e problemas novos e aprimorados corrigidos nessa versão, exiba o [roteiro de versão do Experience Manager Guides](https://experienceleague.adobe.com/en/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap).

### Problemas conhecidos {#known-issues-19567}

Nenhum.

### Recursos e APIs obsoletos {#deprecated-19567}

Os recursos e APIs obsoletos e removidos do AEM as a Cloud Service estão detalhados no documento [Recursos e APIs obsoletos e removidos](/help/release-notes/deprecated-removed-features.md).

### Correções de segurança {#security-19567}

A AEM as a Cloud Service dedica-se a otimizar a segurança e o desempenho da sua plataforma. Esta versão de manutenção aborda 21 vulnerabilidades identificadas, reforçando nosso compromisso com a proteção robusta do sistema.

### Tecnologias integradas {#embedded-tech-19567}

| Tecnologia | Versão | Link |
|---|--------------|-------------------------------------------------------------------------------------------------------------------|
| AEM Oak | 1.76.0 | [API Oak API 1.76.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.76.0/index.html) |
| API DO SLING DO AEM | 2.27.6 | [API Apache Sling API 2.27.6](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| HTL do AEM | 1.4.26-1.4.0 | [Especificação da linguagem de modelo HTML](https://github.com/adobe/htl-spec) |
| Componentes principais do AEM | 2.27.0 | [Componentes principais de WCM do AEM](https://github.com/adobe/aem-core-wcm-components) |
