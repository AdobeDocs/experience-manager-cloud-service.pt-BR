---
title: '[!DNL Adobe Experience Manager] como um Canal de pré-lançamento do Cloud Service'
description: '[!DNL Adobe Experience Manager] como um Canal de pré-lançamento do Cloud Service'
source-git-commit: 4ee9a5744cdcec00dd497a00b0d8dbf288a5adcb
workflow-type: tm+mt
source-wordcount: '752'
ht-degree: 0%

---


# [!DNL Adobe Experience Manager] como um Canal de pré-lançamento do Cloud Service  {#prerelease-channel}


## Introdução {#introduction}

[!DNL Adobe Experience Manager] o as a Cloud Service fornece novos recursos mensalmente, de acordo com o agendamento do roteiro de versões do  [Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=en#aem-as-cloud-service). Para se familiarizar com os recursos agendados para serem ativados no mês seguinte, os clientes podem assinar o canal de pré-lançamento, que é acessível por meio da configuração apropriada em ambientes de desenvolvimento de programas padrão ou em quaisquer ambientes de programa sandbox. Os clientes podem visualizar as alterações no console Sites, bem como criar o código em relação a quaisquer novas APIs de pré-lançamento.

A lista de recursos de pré-lançamento de um determinado mês é publicada nas [notas de versão mensais](/help/release-notes/release-notes-cloud/release-notes-current.md).

>[!VÍDEO](/help/release-notes/assets/prerelease-overview.mp4)

## Como ativar o pré-lançamento {#enable-prerelease}

Os recursos de pré-lançamento podem ser vistos de diferentes maneiras:

* Ambientes em nuvem (ambientes padrão de desenvolvimento de programa ou qualquer tipo de ambiente de programa sandbox)
* SDK local

### Ambientes em nuvem {#cloud-environments}

Para ver novos recursos no console Sites em ambientes de desenvolvimento de nuvem, bem como o resultado de qualquer personalização de projeto:

* Usando o endpoint [Variáveis de ambiente da API do Cloud Manager](https://www.adobe.io/apis/experiencecloud/cloud-manager/api-reference.html#/Variables/patchEnvironmentVariables), defina a variável de ambiente **AEM_RELEASE_CHANNEL** para o valor **pré-lançamento**.

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

A CLI do Cloud Manager também pode ser usada, de acordo com as instruções em [https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid](https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid)
```aio cloudmanager:environment:set-variables <ENVIRONMENT_ID> --programId=<PROGRAM_ID> --variable AEM_RELEASE_CHANNEL “prerelease”```


A variável pode ser excluída ou retornada a um valor diferente se você quiser que o ambiente seja restaurado ao comportamento do canal regular (não pré-lançamento)

### SDK local {#local-sdk}

Você pode ver novos recursos no console Sites no SDK do Quickstart local e código em relação às novas APIs no pré-lançamento, fazendo com que seu projeto maven faça referência ao pré-lançamento `API Jar` localizado no Maven Central. Você também pode ver esses recursos de pré-lançamento em seu computador local, iniciando o SDK Quickstart normal no modo de pré-lançamento:

* Baixe o SDK no portal de distribuição de software e instale conforme descrito em [Acessando o AEM como um SDK do Cloud Service](/help/implementing/developing/aem-as-a-cloud-service-sdk.md#accessing-the-aem-as-a-cloud-service-sdk.)
* Ao iniciar o Início rápido do SDK, inclua o argumento `-r prerelease`.
* O valor é *sticky*, portanto, só pode ser selecionado na primeira inicialização. Reinstale o SDK para alterar a opção de linha de comando.

Como pode haver várias versões de manutenção de AEM entre as versões de recursos mensais, você pode baixar esses novos SDKs e fazer referência às novas versões do SDK API Jar em projetos maven. As versões de manutenção não adicionarão recursos adicionais de pré-lançamento, mas poderão incluir outras alterações menores, como correções de erros, correções de segurança e aprimoramentos de desempenho.
Javadocs são publicados no Maven Central.

Para build no SDK de pré-lançamento:

1. modifique o pom.xml do seu projeto maven para fazer referência a um jar de api sdk de pré-lançamento distinto, que é publicado no Maven central. Ele contém qualquer nova api Java para os recursos de pré-lançamento e tem uma dependência no jar da api do sdk. Ele usa a mesma versão.

   Como exemplo, aqui está um trecho da seção de gerenciamento de dependência do pom pai que faz referência ao Jar da API regular:

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

   E então o uso em um módulo:

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

1. Implantar no servidor local
1. Se ele funcionar conforme esperado localmente, confirme o código em uma ramificação de desenvolvimento e use um pipeline de não produção do Cloud Manager para implantar em um ambiente que assine o canal de pré-lançamento

>[!CAUTION]
O `aem-prerelease-sdk-api` artifactId nunca deve ser usado ao implantar em Preparo ou Produção. Sempre use o aem-sdk-api ao implantar via Pipeline de produção. Da mesma forma, o código que faz referência às APIs de pré-lançamento não deve ser implantado por meio do pipeline de produção.

O [AEM plug-in maven do Analyzer CS build v1.0 e superior](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html?lang=en#developing) detectará se a api de pré-lançamento é usada em um projeto inspecionando as dependências. Se o analisador o encontrar, ele usará a api de pré-lançamento do sdk para analisar o projeto.

## Considerações {#considerations}

Há algumas coisas a serem observadas no canal de pré-lançamento:

* Alguns recursos que serão implementados na versão do próximo mês podem não ser incluídos no canal de pré-lançamento.
* Os recursos no pré-lançamento são colocados por meio de garantia de qualidade rigorosa e destinam-se a ser concluídos em recursos em vez de beta. Caso detecte problemas, reporte-os, como faria se suspeitasse de erros em recursos em uma versão regular do AEM.
* Para determinar se um ambiente está configurado para o canal de pré-lançamento, vá para a página **About** do Console AEM e verifique se o número da versão AEM inclui um sufixo *prerelease* como ```Adobe Experience Manager 2021.4.5226.20210427T070726Z-210429-PRERELEASE```.

![about](/help/release-notes/assets/about.png)
