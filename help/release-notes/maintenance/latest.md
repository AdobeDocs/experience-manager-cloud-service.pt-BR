---
title: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: 97a6a7865f696f4d61a1fb4e25619caac7b68b51
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 39%

---

# Notas da versão de manutenção {#maintenance-release-notes}

A seção a seguir descreve as notas de versão técnicas para a versão de manutenção atual do Experience Manager as a Cloud Service.

## Versão 13420 {#release-13420}

Veja abaixo um resumo das melhorias contínuas da versão de manutenção 13420, lançada publicamente em 12 de setembro de 2023. Esta versão de manutenção substitui a versão 13323.

A Ativação de Recurso 2023.9.0 fornece o conjunto completo de recursos para esta versão de manutenção. Consulte o [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=pt-BR) para obter mais informações.

### Aprimoramentos {#enhancements-13420}

- ASSETS-19544: a última modificação de ativos por propriedade agora é definida como o usuário que solicita o processamento.

### Problemas corrigidos {#fixed-issues-13420}

- ASSETS-27628: nó incorreto &quot;canais&quot; sendo criado ao personalizar o painel de pesquisa Ativos
- ASSETS-27539: correspondência de expressão regular de restrições de upload.
- ASSETS-26530: o Unified Shell não traz os usuários de volta à página original.
- ATIVOS-22719: os colchetes no ponto de interrupção de corte inteligente quebram o recurso de edição de corte inteligente.
- ASSETS-27726: linkshare.html não deve ser indexado pelo Google.
- ASSETS-27791: A validação do esquema de metadados ocorre somente para o primeiro campo.
- ASSETS-25544: botão de invalidação de cache CDN desativado fixo.
- ASSETS-26575: correção do truncamento de nomes ao criar conjuntos de imagens.
- ASSETS-26705: corrigido o processamento desnecessário em ativos de pastas e fragmentos de conteúdo não-DM.
- ASSETS-25740: Correção de leitores de tela que não narravam o Nome e a função para controles de Edição/Corte na página &quot;Editar cortes inteligentes&quot; usando teclas de seta para baixo.
- CQ-4354266: não é possível abrir itens da caixa de entrada.
- CQ-4354347: atualizações das traduções do AEM.
- DISP-1009: O usuário-agente como cabeçalho não é removido pelo X-Forwarded-Host.
- Várias correções relacionadas a acessibilidade e segurança.

### Problemas conhecidos {#known-issues-13420}

Nenhum.

### Tecnologias integradas {#embedded-tech-13420}

| Tecnologia | Versão | Link |
|---|---|---|
| AEM Oak | 1.54-T20230817132355-3800a65 | [API Oak API 1.54.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.54.0/index.html) |
| API DO SLING DO AEM | Versão 2.27.2 | [API Apache Sling API 2.27.2](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| HTL do AEM | Versão 1.4.20-1.4.0 | [Especificação da linguagem de modelo HTML](https://github.com/adobe/htl-spec) |
| Componentes principais do AEM | Versão 2.23.2 | [Componentes principais de WCM do AEM](https://github.com/adobe/aem-core-wcm-components) |
