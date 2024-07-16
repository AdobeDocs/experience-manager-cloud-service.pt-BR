---
title: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 573de431328650778b3ef0979a24190477382310
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 33%

---


# Notas da versão de manutenção {#maintenance-release-notes}

A seção a seguir descreve as notas de versão técnicas para a versão de manutenção atual do Experience Manager as a Cloud Service.

## Versão 17098 {#release-17098}

Veja abaixo um resumo das melhorias contínuas da versão de manutenção 17098, lançada publicamente em quarta-feira, 16 de julho de 2024. A versão de manutenção anterior foi a versão de 16971.

A ativação de recursos do 2024.7.0 fornecerá o conjunto completo de recursos para esta versão de manutenção. Consulte o [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obter mais informações.

### Aprimoramentos {#enhancements-17098}

- SKYOPS-79817: Ativar Tarefa do Analisador de Recursos do Sling para Mapeamentos de Usuário de Serviço

### Problemas corrigidos {#fixed-issues-17098}

- ASSETS-39665: a sincronização de cortes inteligentes não funciona após a migração da 6.5 para o AEMCS
- FORMS-14993: API do Forms que retorna 500 para o material adicional em funcionamento anteriormente
- GRANITE-52120: CRXDE retornando 500 ao mostrar dados de controle de acesso
- GRANITE-52573: solicitações que retornam 400 ao usar // em URLs regravadas
- GRANITE-52746: Todos os tipos de nó não carregados na caixa de diálogo Criar nó
- GRANITE-52777: Manipulação de 404s interrompida quando a solicitação é encapsulada
- GRANITE-52871: certifique-se de que o publish-worker esteja sincronizado com o golden-publish e seja concluído antes da compactação
- SKYOPS-79173: Replicador não replicando para vários agentes correspondentes a um determinado AgentIdFilter
- SKYOPS-80075: Problemas com Umlauts em nomes de ativos que causam o bloqueio da fila de publicação (Mac)
- SKYOPS-81032: Filtre os logs gerados pelas solicitações para obter logs ao usar o Log Aprimorado

### Problemas conhecidos {#known-issues-17098}

Nenhum

### Aviso de mudança {#change-notice-17098}

- A partir de setembro de 2024, a AEM as a Cloud Service desativará a serialização de Resource Resolvers por meio da estrutura do Exportador de modelo do Sling. Consulte [a documentação](/help/implementing/developing/hybrid/disallow-the-serialization-of-resourceresolvers-via-sling-model-exporter.md) para obter mais detalhes.

### Recursos e APIs obsoletos {#deprecated-17098}

Os recursos e APIs obsoletos e removidos do AEM as a Cloud Service estão detalhados no documento [Recursos e APIs obsoletos e removidos](/help/release-notes/deprecated-removed-features.md).

### Tecnologias integradas {#embedded-tech-17098}

| Tecnologia | Versão | Link |
|---|---|---|
| AEM Oak | 1.66.0 | [API Oak API 1.66.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.66.0/index.html) |
| API DO SLING DO AEM | 2.27.2 | [API Apache Sling API 2.27.2](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| HTL do AEM | 1.4.24-1.4.0 | [Especificação da linguagem de modelo HTML](https://github.com/adobe/htl-spec) |
| Componentes principais do AEM | 2.25.4 | [Componentes principais de WCM do AEM](https://github.com/adobe/aem-core-wcm-components) |
