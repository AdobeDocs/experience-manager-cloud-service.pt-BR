---
title: Remover dependências externas de instalações existentes
description: Remover dependências externas de instalações existentes
feature: Integrations
exl-id: 5b28ce97-2719-47b8-a386-77d4aaddbe81
source-git-commit: b71a78696d4b347c97b077d84b455f53a1747a07
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 17%

---

# Remover dependências externas de instalações existentes {#remove-external-depedencies}

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
