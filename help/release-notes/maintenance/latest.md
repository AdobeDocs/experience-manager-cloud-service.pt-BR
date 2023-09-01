---
title: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: a1686d7796bb1e310b776195bd19df98f6f10650
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 41%

---

# Notas da versão de manutenção {#maintenance-release-notes}

A seção a seguir descreve as notas de versão técnicas para a versão de manutenção atual do Experience Manager as a Cloud Service.

## Versão 13323 {#release-13323}

Veja abaixo um resumo das melhorias contínuas da versão de manutenção 13323, lançada publicamente em 1 de setembro de 2023. Esta versão de manutenção substitui a versão 13239.

A Ativação de recursos 2023.9.0 fornecerá o conjunto completo de recursos para esta versão de manutenção. Consulte o [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=pt-BR) para obter mais informações.

### Aprimoramentos {#enhancements-13323}

- GRANITE-46784: adicione a opção para desativar BearerAuthenticationHandler
- GRANITE-36205: atualize a versão interna de lançamento do oak para a mais recente
- ASSETS-26713: link externo da interface para toque para o novo painel da interface da experiência - integração de shell unificado e interface otimizada para ui-touch atualizada
- SKYOPS-63302: Atualização de com.adobe.granite:com.adobe.granite.auth.saml para v1.0.54
- GRANITE-46634: atualização para cliente de eventos 1.4.0
- GRANITE-46788: Atualização de bibliotecas para Apache Commons IO 2.13.0, Commons Lang 3.13.0, Commons Code 1.16.0 e Commons Compress 1.23.0
- GRANITE-46705: atualização para Apache Felix Http Jetty 4.1.14
- GRANITE-46631: atualização da versão Jackrabbit para 2.20.11
- SKYOPS-61895: Atualização para Jackrabbit Filevault 3.7.0

### Problemas corrigidos {#fixed-issues-13323}

- SKYOPS-63290: Correção da evolução incorreta de compartimentos
- SKYOPS-54607: Cálculo de carga de servidor Ratelimiter incorreto para a solicitação que falhou
- ASSETS-27648: ContentModelIT falha ao ler arquivos de exclusão de outros pacotes
- GRANITE-43744: o Sling Authenticator não funciona corretamente se houver uma configuração incorreta com requisito de autenticação e caminho personalizado
- GRANITE-46419: problema de integração do AEM com Auth0 Idp
- GRANITE-46292: A configuração SAML do Okta não está funcionando após a atualização do AEM Cloud
- GRANITE-47059: Remover o pacote SSL do Granite Jetty

### Problemas conhecidos {#known-issues-13323}

- SITES-15622: GraphQL - problema com consultas persistentes com parâmetros numéricos e booleanos.
- SITES-15654: GraphQL - problemas com uniões e propriedades de mesmo nome.

### Tecnologias integradas {#embedded-tech-13323}

| Tecnologia | Versão | Link |
|---|---|---|
| AEM OAK | 1.54-T20230817132355-3800a65 | [API Oak API 1.54.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.54.0/index.html) |
| API DO SLING DO AEM | Versão 2.27.2 | [API Apache Sling API 2.27.2](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| HTL do AEM | Versão 1.4.20-1.4.0 | [Especificação da linguagem de modelo HTML](https://github.com/adobe/htl-spec) |
| Componentes principais do AEM | Versão 2.23.2 | [Componentes principais de WCM do AEM](https://github.com/adobe/aem-core-wcm-components) |
