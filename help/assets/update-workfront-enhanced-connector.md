---
title: Atualizar [!DNL Workfront for Experience Manager enhanced connector]
description: Atualizar [!DNL Workfront for Experience Manager enhanced connector]
source-git-commit: 34f3cf925a3ea58de176521be459a61f4317eec3
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 1%

---

# Atualizar [!DNL Workfront for Experience Manager enhanced connector] {#update-enhanced-connector-for-workfront}

[!UICONTROL Experience Manager Assets as a Cloud Service] permite atualizar o [!DNL Workfront for Experience Manager enhanced connector] de uma versão anterior para a versão mais recente.

>[!TIP]
>
>Você está procurando por [!DNL Workfront for Experience Manager enhanced connector] atualizar documentação do AEM 6.5? Clique em [here](https://experienceleague.adobe.com/docs/experience-manager-65/assets/integrations/workfront-connector-install.html?lang=en##update-enhanced-connector-for-workfront).


Para atualizar o [!DNL Workfront for Experience Manager enhanced connector] para a versão mais recente:

1. Baixe a versão mais recente do conector aprimorado em [Distribuição de software Adobe](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/workfront-tools.ui.apps.zip).

1. [Acesso](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/managing-code/accessing-repos.html?lang=en) e clonar seu repositório as a Cloud Service AEM do Cloud Manager.

1. Abra o repositório do Experience Manager as a Cloud Service clonado usando um IDE de sua escolha.

1. Coloque o arquivo zip do conector aprimorado baixado na Etapa 1 no seguinte caminho:

   ```TXT
      /ui.apps/src/main/resources/<zip file>
   ```

   >[!NOTE]
   >
   >Se a variável `resources` não existe, crie a pasta.

1. Atualizar a versão do conector aprimorado no pai `pom.xml`.

   ```XML
      <dependency>
         <groupId>digital.hoodoo</groupId>
         <artifactId>workfront-tools.ui.apps</artifactId>
         <type>zip</type>
         <version> updated enhanced connector version number</version>
         <scope>system</scope>
         <systemPath>${project.basedir}/ui.apps/src/main/resources/workfront-tools.ui.apps.zip</systemPath>
      </dependency>
   ```

1. Atualize a dependência em `all module pom.xml`.

   ```XML
      <dependency>
         <groupId>digital.hoodoo</groupId>
         <artifactId>workfront-tools.ui.apps</artifactId>
         <type>zip</type>
         <scope>system</scope>
         <systemPath>${project.basedir}/../ui.apps/src/main/resources/workfront-tools.ui.apps.zip</systemPath>
      </dependency>
   ```

   >[!NOTE]
   >
   >Certifique-se de adicionar `<scope>` e `<systemPath>` às dependências na etapa 5 e 6.

1. Atualizar `pom.xml` incorporados. Adicione o [!DNL Workfront for Experience Manager enhanced connector] pacotes para `embeddeds` da seção `pom.xml` de todo o seu subprojeto. Incorpore as atualizações em todos os módulos `pom.xml`.

   ```XML
   <!-- Workfront Tools -->
   <embedded>
      <groupId>digital.hoodoo</groupId>
      <artifactId>workfront-tools.ui.apps</artifactId>
      <type>zip</type>
      <target>/apps/<path-to-project-install-folder>/install</target>
   </embedded>
   ```

   O target da seção incorporada é definido como `/apps/<path-to-project-install-folder>/install`. Este caminho JCR `/apps/<path-to-project-install-folder>` deve ser incluído nas regras de filtro no `all/src/main/content/META-INF/vault/filter.xml` arquivo. As regras de filtro do repositório geralmente são derivadas do nome do programa. Use o nome da pasta como destino nas regras existentes.

1. [Remova as dependências nos pontos de distribuição do Hoodoo](remove-external-dependencies.md), se houver.

1. Encaminhe as alterações para o repositório.

1. Execute o pipeline para [implantar as alterações no Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html).
