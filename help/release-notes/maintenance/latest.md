---
title: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 33468de99a3e77539f4bdc9435324c9f52a45d9f
workflow-type: tm+mt
source-wordcount: '350'
ht-degree: 32%

---


# Notas da versão de manutenção {#maintenance-release-notes}

A seção a seguir descreve as notas de versão técnicas para a versão de manutenção atual do Experience Manager as a Cloud Service.

## Versão 22171 {#22171}

Veja abaixo um resumo das melhorias contínuas da versão de manutenção 22171, lançada publicamente em quarta-feira, 2 de setembro de 2025. A versão de manutenção anterior era 21994.

A ativação de recursos do 2025.9.0 fornecerá o conjunto completo de recursos para esta versão de manutenção. Consulte o [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/pt-br/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obter mais informações.

### Novos recursos  {#new-features-22171}

* ASSETS-53136: Suporte à ID personalizada no Dynamic Media com OpenAPI.

### Aprimoramentos {#enhancements-22171}

Nenhum.

### Problemas corrigidos {#fixed-issues-22171}

* ASSETS-52510: Falha na detecção de nome de arquivo duplicado para nomes de arquivo contendo Unicode `U+202F`.
* ASSETS-53489: A exclusão de pasta da interface do usuário do Assets View não cancela a aprovação de todos os ativos contidos.
* ASSETS-54821: &quot;Erro de servidor&quot; intermitente no Asset Link.
* ASSETS-55024: Imagem quebrada no modelo &quot;Download por email&quot; do AEM Assets.
* ASSETS-55325: os URLs estáticos do Dynamic Media omitem a extensão de arquivo após a renomeação do ativo.
* ASSETS-55334: a caixa de diálogo Compartilhamento de links pisca brevemente e desaparece ou nunca aparece.
* ASSETS-55382: os trabalhos de ativos assíncronos reiniciados criam uma pasta de destino duplicada.
* ASSETS-55472: Opção Gerenciar publicação &quot;Incluir somente páginas já publicadas&quot; ignorada.
* SITES-31600: Personalização de quebra de erro do Contexthub js.

Para obter mais informações sobre recursos e problemas novos e aprimorados corrigidos nessa versão, exiba o [roteiro de versão do Experience Manager Guides](https://experienceleague.adobe.com/pt-br/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap).

### Problemas conhecidos {#known-issues-22171}

Nenhum.

### Recursos e APIs obsoletos {#deprecated-22171}

Os recursos e APIs obsoletos e removidos do AEM as a Cloud Service estão detalhados no documento [Recursos e APIs obsoletos e removidos](/help/release-notes/deprecated-removed-features.md).

### Correções de segurança {#security-22171}

A AEM as a Cloud Service dedica-se a otimizar a segurança e o desempenho da sua plataforma. Esta versão de manutenção aborda sete vulnerabilidades identificadas, reforçando nosso compromisso com a proteção robusta do sistema.

### Tecnologias integradas {#embedded-tech-22171}

| Tecnologia | Versão | Link |
|---|---|---|
| AEM Oak | 1.84.0 | [API Oak API 1.84.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.84/index.html) |
| API DO SLING DO AEM | 2.27.6 | [API Apache Sling API 2.27.6](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| HTL do AEM | 1.4.28-1.4.0 | [Especificação da linguagem de modelo HTML](https://github.com/adobe/htl-spec) |
| Apache HTTP Server | 2.4.65 | [Apache Httpd 2.4.65](https://apache.googlesource.com/httpd/+/refs/tags/2.4.65/CHANGES) |
| Componentes principais do AEM | 2.29.0 | [Componentes principais de WCM do AEM](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14 (padrão) | [Versões Node.js com suporte](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |
