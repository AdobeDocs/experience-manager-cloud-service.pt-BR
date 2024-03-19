---
title: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: dbdc63db9a9ac954ce6359d3643231d6e195fd53
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 46%

---

# Notas da versão de manutenção {#maintenance-release-notes}

A seção a seguir descreve as notas de versão técnicas para a versão de manutenção atual do Experience Manager as a Cloud Service.

## Versão 15575 {#release-15575}

Veja abaixo um resumo das melhorias contínuas da versão de manutenção 15575, lançada publicamente em quarta-feira, 19 de março de 2024. A versão de manutenção anterior era a versão 15262.

A Ativação de recursos 2024.3.0 fornecerá o conjunto completo de recursos para esta versão de manutenção. Consulte o [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=pt-BR) para obter mais informações.

### Aprimoramentos {#enhancements-15575}

Nenhum.

### Problemas corrigidos {#fixed-issues-15575}

* ASSETS-36358: o relatório de uploads não pode ser renderizado.
* GRANITE-50774: GraniteContent deve usar a ordem determinística de valores de propriedade no momento da inicialização.

### Problemas conhecidos {#known-issues-15575}

Nenhum.

### Aviso de mudança {#change-notice-15575}

**Ações necessárias**

#### Defina a versão do Java CM para 11 {#set-java-version-11}

A nova versão do aem-sdk-api contém classes compiladas com um destino Java 11, que não é compatível com a versão 1.8 do JDK padrão do ambiente de compilação do Cloud Manager. Esta atualização requer que o Maven seja executado usando o JDK 11.

Os clientes são aconselhados a adicionar um `.cloudmanager/java-version` para a raiz do repositório Git com o conteúdo: `11`. Consulte [Ambiente de compilação / Configuração da versão do JDK Maven](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#alternate-maven-jdk-version).

#### Atualizar aem-cloud-testing-clients para 1.2.1 {#update-aem-cloud-testing-clients}

As próximas alterações exigirão a biblioteca [aem-cloud-testing-clients](https://github.com/adobe/aem-testing-clients) usado em seus testes funcionais personalizados para ser atualizado para pelo menos a versão **1.2.1**

Certifique-se de que sua dependência no `it.tests/pom.xml` foi atualizado.

```xml
<dependency>
   <groupId>com.adobe.cq</groupId>
   <artifactId>aem-cloud-testing-clients</artifactId>
   <version>1.2.1</version>
</dependency>
```

Essa alteração precisa ser executada antes de 6 de abril de 2024.

Falha ao atualizar a biblioteca de dependências resultará em falhas de pipeline na etapa &quot;Teste funcional personalizado&quot;.

### Tecnologias integradas {#embedded-tech-15575}

| Tecnologia | Versão | Link |
|---|---|---|
| AEM OAK | 1.60-T20240131102219-0cde853 | [API Oak API 1.60.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.60.0/index.html) |
| API DO SLING DO AEM | Versão 2.27.2 | [API Apache Sling API 2.27.2](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| HTL do AEM | Versão 1.4.20-1.4.0 | [Especificação da linguagem de modelo HTML](https://github.com/adobe/htl-spec) |
| Componentes principais do AEM | Versão 2.23.4 | [Componentes principais de WCM do AEM](https://github.com/adobe/aem-core-wcm-components) |
