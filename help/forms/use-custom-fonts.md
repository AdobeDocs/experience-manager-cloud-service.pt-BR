---
title: Como podemos usar fontes personalizadas no AEM Forms?
description: Saiba como adicionar fontes personalizadas a um ambiente as a Cloud Service do Forms.
exl-id: 88214d36-fb97-4d46-a9fe-71dbc7826eb1
source-git-commit: 7a65aa82792500616f971df52b8ddb6d893ab89d
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 0%

---

# Usar fontes personalizadas

**A documentação de comunicações do Cloud Service está na versão beta**

Você pode usar as Comunicações as a Cloud Service da Forms para combinar um modelo XDP, um documento PDF baseado em XDP ou o Acrobat Form (AcroForm) com dados XML para gerar documentos PDF. Você também pode usar Comunicações para combinar, reorganizar e aumentar documentos PDF e XDP e obter informações sobre documentos PDF.

Juntamente com as operações mencionadas anteriormente, você pode usar fontes incluídas no Cloud Service ou fontes personalizadas (fontes aprovadas pela organização) para renderizar os documentos de PDF gerados. Você pode usar o projeto de desenvolvimento de Cloud Service para adicionar fontes personalizadas ao seu ambiente de Cloud Service.

## Comportamento dos documentos do PDF

Você pode [incorporar uma fonte](https://adobedocs.github.io/experience-manager-forms-cloud-service-developer-reference/references/output-sync/#tag/PrintedOutputOptions) para um documento PDF. Quando uma fonte é incorporada, o documento PDF aparece (parece) idêntico em todas as plataformas. Ele usa fontes incorporadas para garantir uma aparência consistente. Quando uma fonte não está incorporada, a renderização da fonte depende das configurações de renderização dos clientes do visualizador de PDF, como Acrobat ou Acrobat Reader. Se a fonte estiver disponível no computador cliente, o PDF usará a fonte especificada, caso contrário, o PDF será renderizado com uma fonte de fallback padrão.

## Adicionar fontes personalizadas ao seu ambiente as a Cloud Service do Forms {#custom-fonts-cloud-service}

Para adicionar fontes personalizadas ao ambiente de Cloud Service:

1. Configure e abra o [projeto de desenvolvimento local](setup-local-development-environment.md). Você pode usar qualquer IDE de sua escolha.
1. Na estrutura de pastas de nível superior do projeto, crie uma pasta (módulo) para salvar fontes personalizadas e adicionar fontes personalizadas à pasta. Por exemplo, fontes/src/main/resources
   ![Pasta Fonts](assets/fonts.png)

1. Abra o arquivo pom.xml do módulo de fontes do projeto de desenvolvimento.
1. Adicionar o plug-in jar ao arquivo pom:

   ```xml
   <plugin>
       <groupId>org.apache.maven.plugins</groupId>
       <artifactId>maven-jar-plugin</artifactId>
       <version>3.1.2</version>
       <configuration>
           <archive>
               <manifest>
                   <addDefaultEntries/>
                   <addDefaultImplementationEntries/>
               </manifest>
           </archive>
       </configuration>
   </plugin>
   ```

1. Adicione o `<Font-Archive-Version>` entrada manifest do arquivo .pom e definir valor da versão como 1:

   ```xml
   <plugin>
       <groupId>org.apache.maven.plugins</groupId>
       <artifactId>maven-jar-plugin</artifactId>
       <version>3.1.2</version>
       <configuration>
           <archive>
               <manifest>
                   <addDefaultEntries/>
                   <addDefaultImplementationEntries/>
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

   A pasta de fontes contém todas as fontes personalizadas.

1. Faça check-in do código atualizado e [executar o pipeline](/help/implementing/cloud-manager/deploy-code.md) para implantar as fontes no ambiente Cloud Service.

1. (Opcional) Abra o prompt de comando, navegue até a pasta do projeto local e execute o comando abaixo. O comando compacta as fontes em um arquivo .jar junto com informações relevantes. Você pode usar o arquivo .jar para adicionar fontes personalizadas a um ambiente de desenvolvimento local de Cloud Service Forms.

   ```shell
   mvn clean install
   ```

## Adicione fontes personalizadas ao ambiente de desenvolvimento do Forms Cloud Service local {#custom-fonts-cloud-service-sdk}

1. Inicie o ambiente de desenvolvimento local.
1. Navegue até `<aem install directory>/crx-quickstart/install` pasta.
1. Coloque o `<jar file contaning custom fonts and relevant deployment code>.jar` para a pasta de instalação. Se você não tiver o arquivo .jar, execute as etapas listadas em [Adicionar fontes personalizadas ao seu ambiente as a Cloud Service do Forms](#custom-fonts-cloud-service) seção para gerar o arquivo.
1. Execute o [ambiente de SDK baseado em docker](setup-local-development-environment.md#docker-microservices)


   >[!NOTE]
   >
   >Sempre que você implantar um arquivo .jar de fontes personalizadas atualizado no ambiente de desenvolvimento local, reinicie o ambiente do SDK baseado em docker.
