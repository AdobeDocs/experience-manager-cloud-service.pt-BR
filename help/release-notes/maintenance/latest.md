---
title: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: 22ed74b307b9eb4c6c2f72ac2a34e2ab6d30a85c
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 45%

---

# Notas da versão de manutenção {#maintenance-release-notes}

A seção a seguir descreve as notas de versão técnicas para a versão de manutenção atual do Experience Manager as a Cloud Service.

## Versão 13239 {#release-13239}

Veja abaixo um resumo das melhorias contínuas da versão de manutenção 13239, lançada publicamente em 29 de agosto de 2023. Esta versão de manutenção substitui a versão 13206.

A Ativação de recursos 2023.9.0 fornecerá o conjunto completo de recursos para esta versão de manutenção. Consulte o [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=pt-BR) para obter mais informações.

### Aprimoramentos {#enhancements-13239}

- GRANITE-46784: adicione a opção para desativar BearerAuthenticationHandler
- GRANITE-36205: atualize a versão interna de lançamento do oak para a mais recente
- GRANITE-47059: Remover o pacote SSL do Granite Jetty
- ASSETS-26713: link externo da interface para toque para o novo painel da interface da experiência - integração de shell unificado e interface otimizada para ui-touch atualizada
- SKYOPS-63302: Atualização de com.adobe.granite:com.adobe.granite.auth.saml para v1.0.54
- GRANITE-46634: atualização para cliente de eventos 1.4.0
- GRANITE-46788: atualização das bibliotecas do Apache Commons
- GRANITE-29211: Atualização da ferramenta para o modelo de recurso Sling 2.0
- GRANITE-46705: atualização para Apache Felix Http Jetty 4.1.14
- GRANITE-46631: atualização da versão Jackrabbit para 2.20.11
- SKYOPS-61895: Atualização para Jackrabbit Filevault 3.7.0

### Problemas corrigidos {#fixed-issues-13239}

- SKYOPS-63290: Correção da evolução incorreta de compartimentos
- SKYOPS-54607: Cálculo de carga de servidor Ratelimiter incorreto para a solicitação que falhou
- ASSETS-27648: ContentModelIT falha ao ler arquivos de exclusão de outros pacotes
- GRANITE-43744: o Sling Authenticator não funciona corretamente se houver uma configuração incorreta com requisito de autenticação e caminho personalizado
- GRANITE-46419: problema de integração do AEM com Auth0 Idp
- GRANITE-46292: A configuração SAML do Okta não está funcionando após a atualização do AEM Cloud

### Problemas conhecidos {#known-issues-13239}

Nenhum.

### Tecnologias integradas {#embedded-tech-13239}

| Tecnologia | Versão | Link |
|---|---|---|
| AEM OAK | 1.54-T20230817132355-3800a65 | [API Oak API 1.54.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.54.0/index.html) |
| API DO SLING DO AEM | Versão 2.27.2 | [API Apache Sling API 2.27.2](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| HTL do AEM | Versão 1.4.20-1.4.0 | [Especificação da linguagem de modelo HTML](https://github.com/adobe/htl-spec) |
| Componentes principais do AEM | Versão 2.23.2 | [Componentes principais de WCM do AEM](https://github.com/adobe/aem-core-wcm-components) |
