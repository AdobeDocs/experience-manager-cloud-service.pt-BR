---
title: 'Usar fontes personalizadas '
description: 'Usar fontes personalizadas '
source-git-commit: 10fe582edc8ffc93ea3f8564a64259882bba1d6f
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 0%

---


# Usar fontes personalizadas

**A documentação de Comunicações do Cloud Service está em beta**

Você pode usar as Comunicações as a Cloud Service do Forms para combinar um modelo XDP, um documento PDF baseado em XDP ou um Formulário Acrobat (AcroForm) com dados XML para gerar documentos PDF. Você pode usar fontes incluídas no Cloud Service ou fontes personalizadas (fontes aprovadas pela organização) para renderizar os documentos PDF gerados. Você pode usar o projeto de desenvolvimento do Cloud Service para adicionar fontes personalizadas ao seu ambiente Cloud Service.

## Comportamento dos documentos do PDF

Você pode [incorporar uma fonte](https://adobedocs.github.io/experience-manager-forms-cloud-service-developer-reference/api/sync/#tag/PDFOutputOptions) para um documento PDF. Quando uma fonte é incorporada, o documento PDF aparece (Aparência) idêntico em todas as plataformas. Usava fonte incorporada para garantir uma aparência consistente. Quando uma fonte não é incorporada, a renderização da fonte depende das configurações de renderização do cliente do visualizador de PDF. Se a fonte estiver disponível na máquina cliente, o PDF usa a fonte especificada, caso contrário, o PDF é renderizado com uma fonte de fallback.

## Adicionar fontes personalizadas ao seu ambiente as a Cloud Service do Forms

Para adicionar fontes personalizadas ao seu ambiente Cloud Service:

1. Configure e abra o projeto de desenvolvimento local. Você pode usar qualquer IDE de sua escolha.
1. Na estrutura de pastas de nível superior do projeto, crie uma pasta para salvar fontes personalizadas e adicionar fontes personalizadas à pasta. Por exemplo, fonts/src/main/resources
   ![Pasta de fontes](assets/fonts.png)

1. Abra o arquivo pom.xml de nível superior do projeto de desenvolvimento.
1. Adicionar `<Font-Archive-Version>` entrada de manifesto no arquivo .pom e defina o valor da versão como 1:

   ```xml
   <plugin>
       <groupId>org.apache.maven.plugins</groupId>
       <artifactId>maven-jar-plugin</artifactId>
       <version>3.1.2</version>
       <configuration>
           <archive>
               <manifest>
                   </addDefaultEntries>
                   </addDefaultImplementationEntries>
               </manifest>
               <manifestEntries>
                   <Font-Archive-Version>1</Font-Archive-Version>
                   <Font-Archive-Contents>/</Font-Archive-Contents>
               </manifestEntries> 
           </archive>
       </configuration>
   </plugin>
   ```

1. Adicionar a pasta de fontes a `<modules>` listado no arquivo pom. Por exemplo:

   ```xml
   <modules>
       <module>all</module>
       <module>core</module>
       <module>ui.frontend</module>
       <module>ui.apps</module>
       <module>ui.apps.structure</module>
       <module>ui.config</module>
       <module>ui.content</module>
       <module>it.tests</module>
       <module>dispatcher</module>
       <module>dispatcher.ams</module>
       <module>dispatcher.cloud</module>
       <module>ui.tests</module>
       <module>fonts</module>
   </modules>
   ```

1. Verifique o código atualizado e [executar o pipeline](/help/implementing/cloud-manager/deploy-code.md) para implantar as fontes no seu ambiente Cloud Service.
