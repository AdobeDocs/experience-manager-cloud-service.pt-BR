---
title: '"Canal de pré-lançamento do [!DNL Adobe Experience Manager] as a Cloud Service"'
description: '"Canal de pré-lançamento do [!DNL Adobe Experience Manager] as a Cloud Service"'
exl-id: cfc91699-0087-40fa-a76c-0e5e1e03a5bd
source-git-commit: c2f0b9c904374b5e59ce2b2f268fdd73dfdbfd21
workflow-type: tm+mt
source-wordcount: '805'
ht-degree: 84%

---

# Canal de pré-lançamento do [!DNL Adobe Experience Manager] as a Cloud Service {#prerelease-channel}


## Introdução {#introduction}

O [!DNL Adobe Experience Manager] as a Cloud Service fornece novos recursos mensalmente, de acordo com a programação no [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=pt-BR#aem-as-cloud-service). Para se familiarizar com os recursos programados para serem ativados no mês seguinte, os clientes podem assinar o canal de pré-lançamento, que se torna acessível por meio da configuração apropriada em ambientes de desenvolvimento de programas padrão ou em quaisquer ambientes de programa sandbox. Os clientes podem visualizar as alterações no console do Sites, bem como criar código em relação a quaisquer novas APIs de pré-lançamento.

A lista de recursos de pré-lançamento de um determinado mês é publicada nas [notas de versão mensais](/help/release-notes/release-notes-cloud/release-notes-current.md).

>[!VIDEO](/help/release-notes/assets/prerelease-overview.mp4)

## Como ativar o pré-lançamento {#enable-prerelease}

Os recursos de pré-lançamento podem ser vistos de diferentes maneiras:

* Ambientes em nuvem (ambientes padrão de desenvolvimento de programas ou qualquer tipo de ambiente de programa sandbox)
* SDK local

### Ambientes em nuvem {#cloud-environments}

Para atualizar um ambiente do Cloud para usar o pré-lançamento, adicione um novo [variável de ambiente](../implementing/cloud-manager/environment-variables.md) usando a interface do usuário de configuração de ambiente no Cloud Manager:

1. Navegue até o **Programa** > **Ambiente** > **Configuração do ambiente** você deseja atualizar.
1. Adicione um novo [variável de ambiente](../implementing/cloud-manager/environment-variables.md):

   | Nome | Valor | Serviço Aplicado | Tipo |
   |------|-------|-----------------|------|
   | `AEM_RELEASE_CHANNEL` | `prerelease` | Todos os pacotes | Variável |

1. Salve as alterações e o ambiente será atualizado com as opções de recurso de pré-lançamento ativadas.

   ![Nova variável de ambiente](assets/env-configuration-prerelease.png)


**Alternativamente** você pode usar a API e a CLI do Cloud Manager para atualizar as variáveis de ambiente:

* Use [Ponto de extremidade das variáveis de ambiente da API do Cloud Manager](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/patchEnvironmentVariables), defina o **AEM_RELEASE_CHANNEL** variável de ambiente para o valor **pré-lançamento**.

   ```
   PATCH /program/{programId}/environment/{environmentId}/variables
   [
           {
                   "name" : "AEM_RELEASE_CHANNEL",
                   "value" : "prerelease",
                   "type" : "string"
           }
   ]
   ```

* A CLI do Cloud Manager também pode ser usada, de acordo com as instruções em [https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid](https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid)

   ```aio cloudmanager:environment:set-variables <ENVIRONMENT_ID> --programId=<PROGRAM_ID> --variable AEM_RELEASE_CHANNEL “prerelease”```


A variável pode ser excluída ou retornada a um valor diferente se você quiser que o ambiente seja restaurado ao comportamento do canal regular (não pré-lançamento).

### SDK local {#local-sdk}

Você pode ver novos recursos no console do Sites no SDK do Quickstart local e codificar em relação às novas APIs no pré-lançamento, fazendo com que seu projeto maven faça referência à `API Jar` de pré-lançamento, localizada na Maven Central. Você também pode ver esses recursos de pré-lançamento em seu computador local, iniciando o SDK do Quickstart padrão no modo de pré-lançamento:

* Baixe o SDK no portal de distribuição de softwares e instale como descrito em [Acesso ao SDK do AEM as a Cloud Service](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md).
* Ao iniciar o Quickstart do SDK, inclua o argumento `-r prerelease`.
* O valor é *aderente*, assim, ele só pode ser selecionado na primeira inicialização. Reinstale o SDK para alterar a opção de linha de comando.

Como pode haver várias versões de manutenção do AEM entre as versões de recursos mensais, você pode baixar esses novos SDKs e fazer referência às novas versões do Jar da API do SDK em projetos maven. As versões de manutenção não incluirão recursos adicionais de pré-lançamento, mas poderão incluir outras alterações menores, como correções de erros, correções de segurança e aprimoramentos de desempenho.
Javadocs são publicados no Maven Central.

Para criar usando o SDK de pré-lançamento:

1. modifique o pom.xml do seu projeto maven para fazer referência a um jar de api sdk de pré-lançamento distinto, que é publicado no Maven central. Ele contém qualquer nova API Java para os recursos de pré-lançamento e tem uma dependência no jar da API do SDK. Ele usa a mesma versão.

   Como exemplo, aqui está um trecho da seção de gerenciamento de dependência do pom pai que faz referência ao Jar da API padrão:

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

1. Implante no servidor local
1. Se ele funcionar conforme esperado localmente, confirme o código em uma ramificação de desenvolvimento e use um pipeline de não produção do Cloud Manager para implantar em um ambiente que assine o canal de pré-lançamento

>[!CAUTION]
> 
> O artifactId `aem-prerelease-sdk-api` nunca deve ser usado ao implantar em Preparo ou Produção. Sempre use o aem-sdk-api ao implantar pelo Pipeline de produção. Da mesma forma, o código que faz referência às APIs de pré-lançamento não deve ser implantado por meio do pipeline de produção.

O [Plug-in Maven Build Analyzer do SDK do AEM CS v1.0 e superior](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html?lang=pt-BR#developing) detectará se a api de pré-lançamento é usada em um projeto, inspecionando as dependências. Se o analisador o encontrar, ele usará a api de pré-lançamento do sdk para analisar o projeto.

## Considerações {#considerations}

Há algumas coisas a serem observadas sobre o canal de pré-lançamento:

* Alguns recursos que serão implementados na versão do próximo mês podem não ser incluídos no canal de pré-lançamento.
* Os recursos no pré-lançamento são submetidos a uma garantia de qualidade rigorosa e se destinam a ser completos em recursos, e não de qualidade beta. Caso detecte problemas, reporte-os, como faria se suspeitasse de erros em recursos em uma versão comum do AEM.
* Para determinar se um ambiente está configurado para o canal de pré-lançamento, vá até a página **Sobre** do console do AEM e verifique se o número da versão do AEM inclui um sufixo de *pré-lançamento*, como ```Adobe Experience Manager 2021.4.5226.20210427T070726Z-210429-PRERELEASE```.

![sobre](/help/release-notes/assets/about.png)
