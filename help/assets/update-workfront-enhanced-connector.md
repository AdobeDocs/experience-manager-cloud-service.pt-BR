---
title: Atualizar o [!DNL Workfront for Experience Manager enhanced connector]
description: Atualizar o [!DNL Workfront for Experience Manager enhanced connector]
exl-id: 09276b4d-a7c8-4927-8c0a-40eda48e55a7
feature: Workfront Integrations and Apps
role: Admin
source-git-commit: 257930bc2633a0d31ad3bd28305b8159597befa5
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---

# Atualizar [!DNL Workfront for Experience Manager enhanced connector] {#update-enhanced-connector-for-workfront}

[!UICONTROL Experience Manager Assets as a Cloud Service] permite atualizar o [!DNL Workfront for Experience Manager enhanced connector] de uma versão anterior para a versão mais recente.

>[!TIP]
>
>Você está procurando por [!DNL Workfront for Experience Manager enhanced connector] atualizar a documentação do AEM 6.5? Clique em [aqui](https://experienceleague.adobe.com/docs/experience-manager-65/assets/integrations/workfront-connector-install.html?lang=en##update-enhanced-connector-for-workfront).


Para atualizar o [!DNL Workfront for Experience Manager enhanced connector] para a versão mais recente:

1. Baixe a versão mais recente do conector aprimorado em [Distribuição de software Adobe](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/workfront-tools.ui.apps.zip).

1. [Access](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/managing-code/accessing-repos.html?lang=en) e clonar seu repositório do AEM as a Cloud Service no Cloud Manager.

1. Abra o repositório as a Cloud Service Experience Manager clonado usando um IDE de sua escolha.

1. Coloque o arquivo zip do conector aprimorado baixado na Etapa 1 no seguinte caminho:

   ```TXT
      /ui.apps/src/main/resources/<zip file>
   ```

   >[!NOTE]
   >
   >Se a variável `resources` pasta não existe, crie a pasta.

1. Atualizar a versão aprimorada do conector no pai `pom.xml`.

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

1. Atualizar a dependência no `all module pom.xml`.

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
   >Adicione `<scope>` e `<systemPath>` às dependências nas etapas 5 e 6.

1. Atualizar `pom.xml` incorpora. Adicione o [!DNL Workfront for Experience Manager enhanced connector] pacotes para `embeddeds` seção do `pom.xml` de todo o subprojeto. Incorporar as atualizações em todos os módulos `pom.xml`.

   ```XML
   <!-- Workfront Tools -->
   <embedded>
      <groupId>digital.hoodoo</groupId>
      <artifactId>workfront-tools.ui.apps</artifactId>
      <type>zip</type>
      <target>/apps/<path-to-project-install-folder>/install</target>
   </embedded>
   ```

   O target da seção incorporada é definido como `/apps/<path-to-project-install-folder>/install`. Este caminho JCR `/apps/<path-to-project-install-folder>` deve ser incluído nas regras de filtro na `all/src/main/content/META-INF/vault/filter.xml` arquivo. As regras de filtro do repositório geralmente são derivadas do nome do programa. Use o nome da pasta como destino nas regras existentes.

1. [Remover as dependências nos pontos de distribuição Hoodoo](remove-external-dependencies.md), se houver.

1. Enviar as alterações para o repositório.

1. Executar o pipeline para [implantar as alterações no Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html).
