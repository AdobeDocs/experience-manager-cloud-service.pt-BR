---
title: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 3067e88f8adea50f6b6b05e0466974bc57bc4a4e
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 18%

---


# Notas da versão de manutenção {#maintenance-release-notes}

A seção a seguir descreve as notas de versão técnicas para a versão de manutenção atual do Experience Manager as a Cloud Service.

## Versão 21994 {#21994}

Veja abaixo um resumo das melhorias contínuas da versão de manutenção 21994, lançada publicamente em quarta-feira, 19 de agosto de 2025. A versão de manutenção anterior era 21772.

A ativação de recursos do 2025.8.0 fornecerá o conjunto completo de recursos para esta versão de manutenção. Consulte o [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obter mais informações.

### Novos recursos  {#new-features-21994}

Nenhum.

### Aprimoramentos {#enhancements-21994}

* GRANITE-53488: Melhore a manipulação de erros do ponto de extremidade deleteconf.json.
* GRANITE-59968: permissão para configurar REPLICATION_FORCE_READY_MILLIES.
* GRANITE-60183: Apache commons-fileupload 1.6.0.
* GRANITE-60306: Apache commons-lang para 3.18.0.
* GRANITE-60637: Apache commons-codec para 1.19.0.
* GRANITE-60645: Apache commons-io 2.20.0.
* GRANITE-60663: Apache commons-text 1.14.0.
* GRANITE-60714: Driver Java Mongo 5.2.
* GRANITE-60778: Filevault 4.0.0.
* GRANITE-60823: Jackrabbit 2.22.2.
* GRANITE-60967: crie métricas para rastrear o tempo de compilação da clientlib.
* SKYOPS-105469: Adição de suporte para acsredirectMgr na api de correção automática.
* SKYOPS-113929: Adicionar métricas para verificação de replicação pronta.
* SKYOPS-84821: Mecanismo Sling 2.16.6.
* SKYOPS-114322: aumente o nível da linguagem do compilador de fechamento para `ECMASCRIPT_2018`.

### Problemas corrigidos {#fixed-issues-21994}

* GRANITE-60167: a atualização de índice assíncrono no Skyline não oferece suporte a dados CSV.
* GRANITE-60532: a modificação de alternadores de valor não é recebida.
* SITES-34277: corrija o erro de bloqueio em fluxos de trabalho de tradução para páginas.
* SKYOPS-105471: Dambaseredirect fix de suporte para autofix de aso.
* SKYOPS-109532: adição de link de recurso removido como comentário atrás da alternância.

#### Guias do AEM {#guides-21994}

* GUIDES-26688: Os arquivos CSS e de layout de página nos modelos nativos do PDF exibem um comportamento de bloqueio de arquivos inconsistente, permitindo edições mesmo quando os arquivos estão bloqueados.
* GUIDES-30900: Copiar uma pasta com um grande número de ativos da interface do Assets leva a um tempo limite da API. A operação continua a ser executada no backend e é concluída após algum tempo, mas nenhuma mensagem de sucesso ou falha, ou notificação é mostrada na interface do usuário.
* GUIDES-29090: Na saída do PDF nativo, a Lista de índice (LOI) é exibida em uma ordem não alfabética e os termos de índice aninhados não são agrupados corretamente, dificultando a navegação do índice.
* GUIDES-11227: Copiar um mapa DITA da interface do usuário do Assets também copia sua linha de base anexada para o novo mapa.
* GUIDES-31506: A página inicial fica em branco quando um dos arquivos listados no widget Arquivos recentes é baseado em um modelo cujo modelo de origem não inclui uma miniatura.

Para obter mais informações sobre recursos e problemas novos e aprimorados corrigidos nessa versão, exiba o [roteiro de versão do Experience Manager Guides](https://experienceleague.adobe.com/en/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap).

### Problemas conhecidos {#known-issues-21994}

* O Apache HTTPD versão 2.4.65 apresenta alterações que podem afetar determinadas configurações devido a novas restrições implementadas como parte das correções de segurança. Essas correções resolvem as vulnerabilidades, garantindo que diretivas como `RequestHeader set`, `edit` e `edit_r` usadas para modificar o cabeçalho Content-Type agora sejam limitadas corretamente aos cabeçalhos de solicitação. Essa alteração impede modificações não intencionais nos cabeçalhos de resposta, especialmente para conteúdo estático.

### Recursos e APIs obsoletos {#deprecated-21994}

Os recursos e APIs obsoletos e removidos do AEM as a Cloud Service estão detalhados no documento [Recursos e APIs obsoletos e removidos](/help/release-notes/deprecated-removed-features.md).

### Correções de segurança {#security-21994}

A AEM as a Cloud Service dedica-se a otimizar a segurança e o desempenho da sua plataforma. Esta versão de manutenção aborda duas vulnerabilidades identificadas, reforçando nosso compromisso com a proteção robusta do sistema.

### Tecnologias integradas {#embedded-tech-21994}

| Tecnologia | Versão | Link |
|---|---|---|
| AEM Oak | 1.84.0 | [API Oak API 1.84.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.84/index.html) |
| API DO SLING DO AEM | 2.27.6 | [API Apache Sling API 2.27.6](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| HTL do AEM | 1.4.28-1.4.0 | [Especificação da linguagem de modelo HTML](https://github.com/adobe/htl-spec) |
| Apache HTTP Server | 2.4.65 | [Apache Httpd 2.4.65](https://apache.googlesource.com/httpd/+/refs/tags/2.4.65/CHANGES) |
| Componentes principais do AEM | 2.29.0 | [Componentes principais de WCM do AEM](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14 (padrão) | [Versões Node.js com suporte](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |
