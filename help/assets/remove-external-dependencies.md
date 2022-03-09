---
title: Remover dependências externas para instalações existentes
description: Instalar [!DNL Workfront for Experience Manager enhanced connector]
feature: Integrations
source-git-commit: b61915a27968b11472ae458d7be3d73f3449fbbe
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 1%

---


# Remover dependências externas para instalações existentes {#remove-external-depedencies}

O Adobe recomenda que você execute as etapas de configuração para instalações de conector aprimorado existentes para o Workfront a fim de remover as dependências dos pontos de distribuição do Hoodoo.

>[!NOTE]
>
>Execute as etapas de configuração somente se tiver instalado o conector aprimorado para Workfront antes de março de 2022. Não há dependências nos pontos de distribuição do Hoodoo para novas instalações aprimoradas de conectores para o Workfront a partir de março de 2022.

Para remover as dependências externas:

1. Remova a seguinte configuração do repositório Hoodoo do pai `pom.xml`:

   ```XML
     <repository>
        <id>hoodoo-maven</id>
        <name>Hoodoo Repository</name>
        <url>https://gitlab.com/api/v4/projects/12715200/packages/maven</url>
     </repository>
   ```

1. Remova a seguinte configuração de servidor do `settings.xml` , disponível em `./cloudmanager/maven/settings.xml`:

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

1. Execute o [novas etapas de instalação](workfront-connector-install.md).

