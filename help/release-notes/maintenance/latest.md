---
title: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 9323464610b804ff407f5eedf404ab2cca93a8da
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 19%

---


# Notas da versão de manutenção {#maintenance-release-notes}

A seção a seguir descreve as notas de versão técnicas para a versão de manutenção atual do Experience Manager as a Cloud Service.

## Versão 17689 {#release-17689}

Veja abaixo um resumo das melhorias contínuas da versão de manutenção 17689, lançada publicamente em quarta-feira, 10 de setembro de 2024. A versão de manutenção anterior era a versão 17569.

A ativação de recursos do 2024.9.0 fornecerá o conjunto completo de recursos para esta versão de manutenção. Consulte o [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obter mais informações.

### Aprimoramentos {#enhancements-17689}

* ASSETS-41404: alterações para suportar melhorias de DRM.
* ASSETS-41621: trabalho de cópia de ativo assíncrono atualizado.
* ASSETS-32166: trabalho de movimentação de ativo assíncrono atualizado.
* ASSETS-41429: Suporte a predefinições de imagem no DM OpenAPI.
* ASSETS-38968: melhore a representação de referências de fragmentos de conteúdo.
* ASSETS-41787, ASSETS-41183: melhorias na estrutura de operações em massa do Assets.
* GRANITE-52917: otimizações para melhorar os tempos de instalação do pacote de cópia de conteúdo.
* SCRNS-3980: Detecta a tela cinza em jogadores que têm subsequências sem ativos programados.

### Problemas corrigidos {#fixed-issues-17689}

* ASSETS-40875: NPE artificial registrado pelo AssetDeleteHandler.
* ASSETS-42422: Evite acionar o trabalho assíncrono para uma única movimentação de ativo.
* ASSETS-41234: Shell unificado - A navegação global pode não funcionar se aberta quando a barra de pesquisa está aberta.
* ASSETS-42256: shell unificado - Tag/selo indicando o ambiente que só funciona intermitentemente.
* ASSETS-41271: impede a republicação desnecessária do Assets durante as operações de movimentação.
* ASSETS-38894: Limitar tentativas processando o watchdog.
* ASSETS-40815: Use a representação do PDF de visualização para mostrar o arquivo PPT na interface do usuário de compartilhamento de link.
* ASSETS-37123: não é possível carregar a visualização do ativo na caixa de diálogo de compartilhamento de link.
* CQ-4358156: atualizar backlinks da tag que está sendo excluída.
* SCRNS-4495: O botão Colar fixo não está funcionando corretamente para diferentes grupos de usuários.
* SCRNS-4512: remova componentes relacionados ao dispositivo das telas do AEMaaCS.
* SCRNS-4466: No painel do canal, ocultar - exibir manifesto, gerar conteúdo offline, atualizar cache de manifesto, painel de exibição.
* SCRNS-4513: Adicionar cabeçalhos de coluna para a página de resultados da pesquisa na exibição de lista.

### Problemas conhecidos {#known-issues-17689}

* FORMS-14340: erro na instanciação de FormsAndDocumentOmniSearchHandler e CloudStorageSubmitActionInserter. Estas são instruções de registro inofensivas.
* FORMS-15818: Entrada do descritor do componente &quot;OSGI-INF/com.adobe.aemfd.docmanager.impl.*.xml’ não encontrou instruções nos logs do servidor. Estas são instruções de registro inofensivas.
* SITES-23662: o usuário que aciona uma publicação não pode ser extraído de instruções de log JCR em logs do servidor. Isso é para um recurso em desenvolvimento que pode causar erros intermitentes e inofensivos &quot;Não é possível encontrar uma ID de usuário válida no lote de eventos OSGI&quot; no log.

### Aviso de mudança {#change-notice-17689}

* A partir de setembro de 2024, a AEM as a Cloud Service desativará a serialização de Resource Resolvers por meio da estrutura do Exportador de modelo do Sling. Consulte [a documentação](/help/implementing/developing/hybrid/disallow-the-serialization-of-resourceresolvers-via-sling-model-exporter.md) para obter mais detalhes.

### Recursos e APIs obsoletos {#deprecated-17689}

Observe que estamos no processo de atualização do `com.day.cq.wcm.api` e, com a versão atual, marcamos como `@Deprecated` alguns de seus métodos e classes. Eles serão removidos em versões futuras. Portanto, considere mudar para as alternativas sugeridas se estiver usando alguma delas.

Os recursos e APIs obsoletos e removidos do AEM as a Cloud Service estão detalhados no documento [Recursos e APIs obsoletos e removidos](/help/release-notes/deprecated-removed-features.md).

### Correções de segurança {#security-17689}

A AEM as a Cloud Service dedica-se a otimizar a segurança e o desempenho da sua plataforma. Esta versão de manutenção aborda quatro vulnerabilidades identificadas, reforçando nosso compromisso com a proteção robusta do sistema.

### Tecnologias integradas {#embedded-tech-17689}

| Tecnologia | Versão | Link |
|---|---|---|
| AEM Oak | 1.68.0 | [API Oak API 1.68.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.68.0/index.html) |
| API DO SLING DO AEM | 2.27.6 | [API Apache Sling API 2.27.6](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| HTL do AEM | 1.4.24-1.4.0 | [Especificação da linguagem de modelo HTML](https://github.com/adobe/htl-spec) |
| Componentes principais do AEM | 2.26.0 | [Componentes principais de WCM do AEM](https://github.com/adobe/aem-core-wcm-components) |
