---
title: Remover dependências externas de instalações existentes
description: Remover dependências externas de instalações existentes
feature: Workfront Integrations and Apps
exl-id: 5b28ce97-2719-47b8-a386-77d4aaddbe81
role: Admin
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '104'
ht-degree: 17%

---

# Remover dependências externas de instalações existentes {#remove-external-depedencies}

A Adobe recomenda executar as etapas de configuração das instalações aprimoradas do conector existentes para Workfront, a fim de remover as dependências nos pontos de distribuição Hoodoo.

>[!NOTE]
>
>Execute as etapas de configuração somente se tiver instalado o conector aprimorado para Workfront antes de março de 2022. Não há dependências nos pontos de distribuição Hoodoo para novas instalações aprimoradas de conectores do Workfront a partir de março de 2022.

Para remover as dependências externas:

1. Remova a seguinte configuração de repositório Hoodoo do pai `pom.xml`:

   ```XML
     <repository>
        <id>hoodoo-maven</id>
        <name>Hoodoo Repository</name>
        <url>https://gitlab.com/api/v4/projects/12715200/packages/maven</url>
     </repository>
   ```

1. Remova a seguinte configuração de servidor do arquivo `settings.xml`, disponível em `./cloudmanager/maven/settings.xml`:

   ```XML
         <server>
            <id>hoodoo-maven</id>
            <configuration>
               <httpHeaders>
                     <property>
                        <name>Deploy-Token</name>
                        <value>xxxxxxxxxxxxxxxx</value>
                     </property>
               </httpHeaders>
            </configuration>
         </server>
   ```

1. Execute as [novas etapas de instalação](workfront-connector-install.md).
