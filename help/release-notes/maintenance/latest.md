---
title: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: 1dd2eae9201c86d2cdac78ff99634eff8ca57a05
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 50%

---

# Notas da versão de manutenção {#maintenance-release-notes}

A seção a seguir descreve as notas de versão técnicas para a versão de manutenção atual do Experience Manager as a Cloud Service.

## Versão 15860 {#release-15860}

Veja abaixo um resumo das melhorias contínuas da versão de manutenção 15860, lançada publicamente em quinta-feira, 10 de abril de 2024. A versão de manutenção anterior era a versão 15787.

A Ativação de recursos 2024.3.0 fornecerá o conjunto completo de recursos para esta versão de manutenção. Consulte o [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=pt-BR) para obter mais informações.

### Aprimoramentos {#enhancements-15860}

Nenhum.

### Problemas corrigidos {#fixed-issues-15860}

* Corrige a regressão para exibir o console Inicializações quando uma inicialização se refere a uma página excluída ou movida.

### Problemas conhecidos {#known-issues-15860}

Nenhum.

### Recursos e APIs obsoletos {#deprecated-15860}

* [Descontinuação de credenciais JWT no console do Adobe Developer](/help/security/jwt-credentials-deprecation-in-adobe-developer-console.md)

Veja [Recursos e APIs obsoletos e removidos](/help/release-notes/deprecated-removed-features.md) saber o que foi descontinuado ou removido no AEM as a Cloud Service.

### Aviso de mudança {#change-notice-15860}

**Ações necessárias**

#### Defina a versão do Java CM para 11 {#set-java-version-11}

A nova versão do aem-sdk-api contém classes compiladas com um destino Java 11, que não é compatível com a versão 1.8 do JDK padrão do ambiente de compilação do Cloud Manager. Esta atualização requer que o Maven seja executado usando o JDK 11.

Os clientes são aconselhados a adicionar um `.cloudmanager/java-version` para a raiz do repositório Git com o conteúdo: `11`. Consulte [Ambiente de compilação / Configuração da versão do JDK Maven](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#alternate-maven-jdk-version).


### Tecnologias integradas {#embedded-tech-15860}

| Tecnologia | Versão | Link |
|---|---|---|
| AEM OAK | 1.60-T20240131102219-0cde853 | [API Oak API 1.60.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.60.0/index.html) |
| API DO SLING DO AEM | Versão 2.27.2 | [API Apache Sling API 2.27.2](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| HTL do AEM | Versão 1.4.20-1.4.0 | [Especificação da linguagem de modelo HTML](https://github.com/adobe/htl-spec) |
| Componentes principais do AEM | Versão 2.24.4 | [Componentes principais de WCM do AEM](https://github.com/adobe/aem-core-wcm-components) |
