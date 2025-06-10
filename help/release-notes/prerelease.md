---
title: Canal de pré-lançamento do Adobe Experience Manager as a Cloud Service
description: Saiba como usar o canal de pré-lançamento para visualizar os recursos futuros do AEM as a Cloud Service.
exl-id: cfc91699-0087-40fa-a76c-0e5e1e03a5bd
feature: Release Information
role: Admin
source-git-commit: 36da09746f02daad82875329b0aa53ee4eb7c074
workflow-type: tm+mt
source-wordcount: '889'
ht-degree: 55%

---


# Canal de pré-lançamento do Adobe Experience Manager as a Cloud Service {#prerelease-channel}

Saiba como usar o canal de pré-lançamento para visualizar os recursos futuros do AEM as a Cloud Service.

## Introdução {#introduction}

O Adobe Experience Manager as a Cloud Service fornece novos recursos regularmente. A lista de recursos novos e futuros para uma determinada versão de recurso está publicada nas [notas de versão.](/help/release-notes/release-notes-cloud/release-notes-current.md)

Os recursos futuros geralmente são disponibilizados de uma das duas formas a seguir:

* Como parte de um programa de primeiros usuários
* Como parte do canal de pré-lançamento

Este documento descreve como ativar o canal de pré-lançamento. O canal de pré-lançamento fornece acesso aos recursos anteriores que serão introduzidos em uma versão futura do AEM. Isso dá a você a chance de validar novos recursos e planejar sua adoção antes da versão futura. Consulte o documento [Notas de versão do Adobe Experience Manager (AEM) as a Cloud Service](/help/release-notes/home.md) para obter detalhes sobre o cronograma de lançamento do AEM.

## Ative o canal de pré-lançamento para acessar e tentar os recursos futuros {#enable-prerelease}

O canal de pré-lançamento pode ser ativado em qualquer ambiente de desenvolvimento ou sandbox. O canal de pré-lançamento não pode ser habilitado em ambientes de preparo ou produção.

O canal de pré-lançamento pode ser acessado de duas maneiras diferentes:

* [Ambientes de nuvem](#cloud-environments)
* [SDK local](#local-sdk)

### Ambientes em nuvem {#cloud-environments}

Para atualizar um ambiente de nuvem para usar o canal de pré-lançamento, é necessário adicionar uma nova variável de ambiente. Você pode fazer isso usando a interface do Cloud Manager ou através da CLI.

#### Adicionar variável de ambiente usando a interface {#add-with-ui}

1. Faça logon no Cloud Manager, em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/), e selecione a organização apropriada.

1. Navegue até o programa em que deseja ativar o canal de pré-lançamento.

1. Selecione o ambiente em que deseja habilitar o canal de pré-lançamento e acessar sua configuração via **Programa** > **Ambiente** > **Configuração do Ambiente**.

1. Adicionar uma nova [variável de ambiente](/help/implementing/cloud-manager/environment-variables.md)

   | Nome | Valor | Serviço aplicado | Tipo |
   |------|-------|-----------------|------|
   | `AEM_RELEASE_CHANNEL` | `prerelease` | Todos | Variável |

1. Salve as alterações e o ambiente será atualizado com o canal de pré-lançamento ativado.

   ![Nova variável de ambiente](assets/env-configuration-prerelease.png)

#### Adicionar variável de ambiente usando a CLI {#add-with-cli}

Você também pode usar a API e a CLI do Cloud Manager para atualizar as variáveis de ambiente.

* Usando o [ponto de extremidade de variáveis de ambiente da API do Cloud Manager](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/patchEnvironmentVariables), defina a variável de ambiente `AEM_RELEASE_CHANNEL` com o valor `prerelease`.

  ```text
  PATCH /program/{programId}/environment/{environmentId}/variables
  [
          {
                  "name" : "AEM_RELEASE_CHANNEL",
                  "value" : "prerelease",
                  "type" : "string"
          }
  ]
  ```

* [A CLI do Cloud Manager](https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid) também pode ser usada

  ```shell
  aio cloudmanager:environment:set-variables <ENVIRONMENT_ID> --programId=<PROGRAM_ID> --variable AEM_RELEASE_CHANNEL "prerelease
  ```

A variável pode ser excluída se você quiser restaurar o ambiente para o comportamento padrão (canal de não pré-lançamento).

### SDK local {#local-sdk}

Você pode acessar recursos futuros no canal de pré-lançamento em sua SDK Quickstart local e codificar em relação às novas APIs, configurando seu projeto Maven para fazer referência ao canal de pré-lançamento `API Jar`, localizado na Maven Central. Você também pode ver o acesso ao canal de pré-lançamento em seu ambiente de desenvolvimento local, iniciando o Quickstart SDK normal no modo de pré-lançamento.

#### Iniciar o Quickstart do SDK no modo de pré-lançamento {#prerelease-mode}

1. Baixe o SDK da distribuição e instalação do software conforme descrito em [Acessando o AEM as a Cloud Service SDK.](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md)
1. Ao iniciar o Quickstart do SDK, inclua o argumento `-r prerelease`.

O valor é aderente, assim, ele só pode ser selecionado na primeira inicialização. Reinstale o SDK para alterar a opção de linha de comando.

Como pode haver várias versões de manutenção do AEM entre as versões de recursos mensais, você pode baixar esses novos SDKs e fazer referência às novas versões do Jar da API do SDK em projetos maven. As versões de manutenção não incluirão recursos adicionais de pré-lançamento, mas poderão incluir outras alterações menores, como correções de erros, correções de segurança e aprimoramentos de desempenho.
Javadocs são publicados no Maven Central.

#### Criar usando o SDK de pré-lançamento {#build-sdk}

1. Modifique o `pom.xml` do seu projeto Maven para fazer referência a um API.jar do SDK de pré-lançamento distinto, que será publicado na Maven Central. Ele contém qualquer nova API Java para recursos de pré-lançamento e é dependente do API.jar do SDK. Ele usa a mesma versão.

   Como exemplo, veja um trecho da seção de gerenciamento de dependência do POM principal que faz referência ao API.jar padrão:

   ```
   <dependencyManagement>
    <dependencies>
        <dependency>
            <groupId>com.adobe.aem</groupId>
            <artifactId>aem-sdk-api</artifactId>
            <version>${aem.sdk.api}</version>
            <scope>provided</scope>
        </dependency>
   ```

   E o uso em um módulo:

   ```
    <dependencies>
     <dependency>
         <groupId>com.adobe.aem</groupId>
         <artifactId>aem-sdk-api</artifactId>
     </dependency>
   ```

   Para alterar para o SDK de pré-lançamento, basta alterar a dependência de `com.adobe.aem:aem-sdk-api` para `com.adobe.aem:aem-prerelease-sdk-api`, conforme observado abaixo:

   ```
   <dependencyManagement>
    <dependencies>
      <dependency>
            <groupId>com.adobe.aem</groupId>
            <artifactId>aem-prerelease-sdk-api</artifactId>
            <version>${aem.sdk.api}</version>
            <scope>provided</scope>
      </dependency>
   <dependencies>
      <dependency>
         <groupId>com.adobe.aem</groupId>
         <artifactId>aem-prerelease-sdk-api</artifactId>
      </dependency>
   ```

   Como de costume, projetos individuais podem usar a dependência.

1. Implante no servidor local.

1. Se ele funcionar conforme esperado localmente, confirme o código em uma ramificação de desenvolvimento e use um pipeline de não produção do Cloud Manager para implantar em um ambiente [que tenha o canal de pré-lançamento habilitado.](#cloud-environments)

>[!CAUTION]
> 
> O artifactId `aem-prerelease-sdk-api` nunca deve ser usado ao implantar no ambiente de preparo ou produção. Sempre use `aem-sdk-api` ao implantar pelo pipeline de produção. Da mesma forma, o código que faz referência às APIs de pré-lançamento não deve ser implantado por meio do pipeline de produção.

O [plug-in Maven Build Analyzer do SDK do AEM CS v1.0 e superior](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html?lang=pt-BR#developing) detectará se a API de pré-lançamento é usada em um projeto inspecionando as dependências. Se o analisador a encontrar, ele usará a API de pré-lançamento do SDK para analisar o projeto.

## Considerações {#considerations}

Há alguns detalhes que devem ser observados ao usar o canal de pré-lançamento.

* O canal de pré-lançamento não contém necessariamente todos os novos recursos a serem implementados na próxima versão.
* Os recursos no pré-lançamento são submetidos a uma garantia de qualidade rigorosa e se destinam a ser completos em recursos, e não de qualidade beta. Caso detecte problemas, reporte-os, como faria se suspeitasse de erros em recursos em uma versão comum do AEM.
* Para determinar se um ambiente está configurado para o canal de pré-lançamento, vá até a página **Sobre** do console do AEM e verifique se o número de versão do AEM inclui um sufixo `PRERELEASE`, como `Adobe Experience Manager 2021.4.5226.20210427T070726Z-210429-PRERELEASE`.

![Sobre](/help/release-notes/assets/about.png)
