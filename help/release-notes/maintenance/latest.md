---
title: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: 558babc0124a8ee8c1337b91c5ef016ed238c935
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 37%

---

# Notas da versão de manutenção {#maintenance-release-notes}

A seção a seguir descreve as notas de versão técnicas para a versão de manutenção atual do Experience Manager as a Cloud Service.

## Versão 16544 {#release-16544}

Veja abaixo um resumo das melhorias contínuas da versão de manutenção 16544, lançada para o público em quarta-feira, 4 de junho de 2024. A versão de manutenção anterior era a versão 16461.

A Ativação de recursos 2024.6.0 fornecerá o conjunto completo de recursos para esta versão de manutenção. Consulte o [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obter mais informações.

### Aprimoramentos {#enhancements-16544}

* GRANITE-41133: Suporte à API 5 do servlet Jakarta e à API do quadro de permissões do servlet OSGi.
* GRANITE-51355: obsoleto org.slf4j.event.
* GRANITE-51565: AEM perde o relacionamento do grupo local com o grupo externo quando o grupo local é publicado a partir do AEM.
* GRANITE-51707: Defina o cookie saml_request_path durante o redirecionamento http para autenticação.
* GRANITE-52010: atualize a versão Jackrabbit para 2.20.16.
* GRANITE-52057: atualização do Filevault para 3.7.3-T20240514105118-694f6aea, corrigindo JCRVLT-745.
* SKYOPS-35998: Atualizar dependências de &#39;Sling RepoInit&#39; : Analisador de Repoinit 1.9.0, JCR de Repoinit 1.1.46.

### Problemas corrigidos {#fixed-issues-16544}

* DXML-17171: Guias AEM: a operação de copiar e colar de tópicos que excedem 15 KB falha com um erro inesperado.
* DXML-17088: Guias AEM: a funcionalidade para alterar o estado do documento de **Propriedades do arquivo** O painel não está funcionando corretamente e as alterações na *Rascunho* estado.
* DXML-16931: Guias AEM: Imagens vinculadas dos tópicos não aparecem na linha de base após a criação da versão.
* DXML-16896: Guias AEM: painéis de conteúdo reutilizáveis não listam elementos quando a variável **Preferências do usuário** estão configurados para exibir arquivos por **Nome do arquivo**.
* GRANITE-51375: idp-sync lança NPE se nenhum caminho intermediário for especificado.

### Problemas conhecidos {#known-issues-16544}

Nenhum.

### Recursos e APIs obsoletos {#deprecated-16544}

Para saber o que está obsoleto ou foi removido no AEM as a Cloud Service, consulte [Recursos e APIs obsoletos e removidos](/help/release-notes/deprecated-removed-features.md).

### Tecnologias integradas {#embedded-tech-16544}

| Tecnologia | Versão | Link |
|---|---|---|
| AEM Oak | 1.64.0 | [API Oak API 1.64.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.64.0/index.html) |
| API DO SLING DO AEM | 2.27.2 | [API Apache Sling API 2.27.2](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| HTL do AEM | 1.4.22-1.4.0 | [Especificação da linguagem de modelo HTML](https://github.com/adobe/htl-spec) |
| Componentes principais do AEM | 2.25.4 | [Componentes principais de WCM do AEM](https://github.com/adobe/aem-core-wcm-components) |
