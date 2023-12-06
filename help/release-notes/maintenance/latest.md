---
title: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: 2677e8fbdf6b21ce2d1d848000401c826bc5f289
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 42%

---

# Notas da versão de manutenção {#maintenance-release-notes}

A seção a seguir descreve as notas de versão técnicas para a versão de manutenção atual do Experience Manager as a Cloud Service.

## Versão 14538 {#release-14538}

Veja abaixo um resumo das melhorias contínuas da versão de manutenção 14538, lançada publicamente em quinta-feira, 6 de dezembro de 2023. Esta versão de manutenção é uma atualização da versão de manutenção anterior: versão 14227.

A Ativação de recursos 2023.12.0 fornecerá o conjunto completo de recursos para esta versão de manutenção. Consulte o [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=pt-BR) para obter mais informações.

### Aprimoramentos {#enhancements-14538}

* GRANITE-46723: Sincronização de usuários - Migração de SAML da sincronização padrão para a sincronização baseada em IDP.
* OAK-10311: Replicação - Otimize a comparação de blob para reduzir o tempo de replicação de um grande lote de ativos no AEM.
* OAK-10511: Replicação - Reduza as viagens de ida e volta da rede para reduzir o tempo de replicação de grandes ativos no AEM.
* GRANITE-48334: Editores - O script de coleção está ausente para o RUM.

### Problemas corrigidos {#fixed-issues-14538}

* CQ-4354867: a referência ToggleCondition refere-se ao campo inexistente no InstanceActionServlet.
* CQ-4349948: Localização de strings &quot;Propriedades de perfil&quot; em Editar configurações do usuário em Ferramentas → Segurança → Usuários.
* GRANITE-44541: Localização de caixas de diálogo de Erro ao adicionar a tela Arquivo de chave privada de Editar usuário > Armazenamento de chaves em Ferramentas → Segurança → Usuários.
* GRANITE-45341: Localização de strings de sucesso/falha para ativar/desativar a ação do usuário em Ferramentas → Segurança → Usuários.
* GRANITE-46650: Localização da mensagem de erro &quot;UserId/Password mismatch&quot;. string em Ferramentas → Segurança → Caixa de diálogo Criar usuários.
* GRANITE-47764: Atualização da API de modelos do Sling 1.5.0: a injeção em uma variável estática em um modelo do Sling causará erros de compilação (SLING-11507).
* GRANITE-48452: Enviando clientlibs vazias com código de status 200.
* GRANITE-48410: ResourceResolver não está fechado.
* ASSETS-31297: impede a exclusão de ativos copiados da mídia dinâmica.
* ASSETS-30811: atualizações de referência para o serviço Blocktag.
* GRANITE-46418: atualização de eventos Sling no AEM: GaugeSupport tem recursão infinita em registerWithSuffix (SLING-11918).

### Problemas conhecidos {#known-issues-14538}

Nenhum.

### Tecnologias integradas {#embedded-tech-14538}

| Tecnologia | Versão | Link |
|---|---|---|
| AEM OAK | 1.58-T20231123092841-619e1bd | [API Oak API 1.58.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.58.0/index.html) |
| API DO SLING DO AEM | Versão 2.27.2 | [API Apache Sling API 2.27.2](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| HTL do AEM | Versão 1.4.20-1.4.0 | [Especificação da linguagem de modelo HTML](https://github.com/adobe/htl-spec) |
| Componentes principais do AEM | Versão 2.23.4 | [Componentes principais de WCM do AEM](https://github.com/adobe/aem-core-wcm-components) |
