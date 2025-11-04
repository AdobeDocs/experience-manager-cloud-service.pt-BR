---
title: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 89597ae0c54b1b2f42f597f556276700545ecd26
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 19%

---


# Notas da versão de manutenção {#maintenance-release-notes}

A seção a seguir descreve as notas de versão técnicas para a versão de manutenção atual do Experience Manager as a Cloud Service.

>[!NOTE]
>
>A versão 23122 foi tornada privada em 3 de novembro.

## Versão 22943 {#22943}

Veja abaixo um resumo das melhorias contínuas da versão de manutenção 22943, lançada publicamente em quarta-feira, 14 de outubro de 2025. A versão de manutenção anterior era 22758.

A ativação de recursos do 2025.10.0 fornece o conjunto completo de recursos para esta versão de manutenção. Consulte o [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obter mais informações.

### Aprimoramentos {#enhancements-22943}

* ASSETS-57809: Atualização da definição de índice para damAssetLucene-13.
* ASSETS-36521: fluxo de trabalho de recarregamento DM aprimorado para garantir pós-processamento consistente.
* ASSETS-56400: adição de uma nova representação PNG de zoom OOTB para ativos com transparência.
* ASSETS-55326: visualização de configuração da pasta de metadados de IA habilitada por meio de eventos HTTP.
* ASSETS-56905: suporte à conexão com o Indesign via proxy.
* ASSETS-48286: adicione propriedades CAI à Algolia para GenStudio.
* ASSETS-48653: aplique a marca d&#39;água invisível na fase de pré-processamento.
* ASSETS-55874: Migração da predefinição de imagem do scene7 para DMWithOpenapi.
* SITES-30452: Melhorias na API de conteúdo para ASO no endpoint /content/definition.

### Problemas corrigidos {#fixed-issues-22943}

* ASSETS-56301: Corrigida a exportação de metadados seletivos para incluir PredictedTags no CSV.
* ASSETS-55543: Lógica de processamento assíncrona refatorada em um pacote reutilizável.
* ASSETS-54789: NPE corrigido em ACLPermissionsValidator quando a ACL de DM está habilitada.
* ASSETS-55888: representação de malware corrigido que aparece no painel de representações da interface do usuário.
* GRANITE-62236: problema de localização de palavra-chave corrigido em pesquisas salvas de coleções inteligentes.
* GRANITE-61875: correção do problema de hotfix de &quot;avaliação de expressão inválida&quot; que impedia o salvamento de fragmentos de conteúdo e downloads de ativos.
* SITES-24074: navegação móvel oculta fixa recebendo foco durante a navegação da guia do teclado.
* SITES-33611: Corrigido o problema de visão geral da Live Copy para mercados de alto volume.

#### Guias do AEM {#guides-22943}

* GUIDES-31421: Quando vários mapas ou tópicos DITA são abertos e um dos tópicos é fechado, o botão **>>**, que mostra todas as guias abertas, é sobreposto às guias abertas restantes na barra de guias.
* GUIDES-33229: Ao gerar PDFs, as regras de filtragem em um arquivo DITAVAL serão ignoradas se qualquer nome de propriedade contiver um ponto.
* GUIDES-33720: Ao aplicar zoom na tela da interface de tradução, o botão Enviar para tradução se move sob as reticências e se torna habilitado mesmo sem que nenhum ativo seja selecionado.
* GUIDES-33590: Quando um revisor conclui uma tarefa de revisão ou o iniciador atualiza a tarefa de revisão sem inserir comentários, o email de notificação enviado exibe o comentário anterior mais recente.

Para obter mais informações sobre recursos e problemas novos e aprimorados corrigidos nessa versão, exiba o [roteiro de versão do Experience Manager Guides](https://experienceleague.adobe.com/en/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap).

### Recursos e APIs obsoletos {#deprecated-22943}

Os recursos e APIs obsoletos e removidos do AEM as a Cloud Service estão detalhados no documento [Recursos e APIs obsoletos e removidos](/help/release-notes/deprecated-removed-features.md).

### Correções de segurança {#security-22943}

A AEM as a Cloud Service dedica-se a otimizar a segurança e o desempenho da sua plataforma. Esta versão de manutenção aborda 14 vulnerabilidades identificadas, reforçando nosso compromisso com a proteção robusta do sistema.

### Aviso de mudança

* Esta versão inclui as seguintes novas versões do índice de produtos:
* **damAssetLucene-13**

### Tecnologias integradas {#embedded-tech-22943}

| Tecnologia | Versão | Link |
|---|---|---|
| AEM Oak | 1.86.0 | [API do Oak 1.86.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.86/index.html) |
| API DO SLING DO AEM | 2.27.6 | [API Apache Sling API 2.27.6](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| HTL do AEM | 1.4.28-1.4.0 | [Especificação da linguagem de modelo HTML](https://github.com/adobe/htl-spec) |
| Apache HTTP Server | 2.4.65 | [Apache Httpd 2.4.65](https://apache.googlesource.com/httpd/+/refs/tags/2.4.65/CHANGES) |
| Componentes principais do AEM | 2.30.2 | [Componentes principais de WCM do AEM](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14 (padrão) | [Versões Node.js com suporte](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |
