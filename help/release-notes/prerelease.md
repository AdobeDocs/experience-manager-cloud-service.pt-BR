---
title: Canal de pré-lançamento do Adobe Experience Manager as a Cloud Service
description: Saiba como usar o canal de pré-lançamento para pré-visualizar os recursos futuros para AEM as a Cloud Service.
exl-id: cfc91699-0087-40fa-a76c-0e5e1e03a5bd
source-git-commit: 5b38e7d0ad97cdf8b7d0d5da79cf3d6721fa618a
workflow-type: tm+mt
source-wordcount: '1306'
ht-degree: 25%

---


# Canal de pré-lançamento do Adobe Experience Manager as a Cloud Service {#prerelease-channel}

Saiba como usar o canal de pré-lançamento para pré-visualizar os recursos futuros para AEM as a Cloud Service.

## Introdução {#introduction}

A Adobe Experience Manager as a Cloud Service fornece novos recursos mensalmente, de acordo com a [O Experience Manager lança o roteiro.](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=pt-BR#aem-as-cloud-service)

Para se familiarizar com os recursos agendados para serem ativados no mês seguinte, você pode assinar o canal de pré-lançamento, que pode ser acessado ao configurar os ambientes de desenvolvimento ou quaisquer ambientes sandbox. Você pode visualizar as alterações acessíveis pela interface do usuário do AEM, bem como criar o código em relação a quaisquer novas APIs de pré-lançamento.

A lista de recursos de pré-lançamento de um determinado mês é publicada no [notas de versão mensais.](/help/release-notes/release-notes-cloud/release-notes-current.md)

## AEM lançamentos as a Cloud Service {#releases}

AEM as a Cloud Service tem dois tipos de lançamentos.

* **Versões mensais** adicione recursos e recursos ao AEM as a Cloud Service
* **Atualizações críticas** adicione atualizações de segurança, aprimoramentos de desempenho e correções de erros e sejam aplicadas diariamente.

Esse padrão garante versões contínuas sem interrupção do serviço.

O canal de pré-lançamento permite que você visualize os recursos agendados para a versão mensal futura para avaliar a funcionalidade futura e planejar sua possível implementação para seus próprios projetos. Ele permite que você se planeje com antecedência para a próxima versão mensal.

Por exemplo, se for maio e você estiver inscrito no canal de pré-lançamento, será possível avaliar os recursos na próxima versão de junho.

![Gráfico de cadência de pré-lançamento](assets/prerelease-cadence.png)

O pré-lançamento oferece uma janela rolante de um mês para os recursos futuros do AEMaaCS, dando tempo para avaliar o impacto de quaisquer novos recursos em seus projetos e personalizações, bem como planejar a implantação desses recursos, testes e treinamento do usuário.

Aproveitar efetivamente o canal de pré-lançamento requer quatro etapas.

1. [Marcar seus calendários](#mark-calendars)
1. [Revise as notas de versão](#release-notes)
1. [Acesse e experimente os novos recursos](#new-features)
1. [Treinar seus usuários](#train-users)

## Marcar seus calendários {#mark-calendars}

As versões mensais são programadas com bastante antecedência e as datas de lançamento são publicadas em [Adobe Experience League.](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html#aem-as-cloud-service)

Anote as datas de lançamento para que você possa planejar tempo para revisar e testar os recursos futuros.

## Revise as notas de versão {#release-notes}

Depois de marcar as datas de lançamento no seu calendário, verifique a [Adobe Experience League](/help/release-notes/release-notes-cloud/release-notes-current.md) no dia da versão para obter as notas de versão mais recentes.

Cada versão é acompanhada de notas de versão que documentam não apenas as novidades dessa versão, mas também os recursos disponíveis para avaliação de pré-lançamento. Conheça com antecedência e planeje aproveitar os recursos mais recentes do AEMaaCS!

Você também pode [verifique os problemas conhecidos](/help/release-notes/known-issues.md) que são publicados junto com todas as versões para que você também possa estar ciente de quaisquer problemas técnicos que possam representar um desafio para sua avaliação ou eventual adoção de novos recursos.

## Ative o Canal de pré-lançamento para acessar e experimente novos recursos {#new-features}

O canal de pré-lançamento pode ser ativado em qualquer ambiente de desenvolvimento ou sandbox. O pré-lançamento não pode ser ativado em ambientes de preparação ou produção.

Os recursos de pré-lançamento podem ser vistos de diferentes maneiras:

* [Ambientes na nuvem](#cloud-environments)
* [SDK local](#local-sdk)

### Ambientes em nuvem {#cloud-environments}

Para atualizar um ambiente de nuvem para usar o pré-lançamento, você deve adicionar uma nova variável de ambiente. Você pode fazer isso usando a interface do usuário do Cloud Manager ou pela CLI.

#### Adicionar variável de ambiente usando a interface do usuário {#add-with-ui}

1. Faça logon no Cloud Manager, em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/), e selecione a organização apropriada.

1. Navegue até o programa em que deseja ativar o pré-lançamento.

1. Selecione o ambiente em que deseja habilitar o pré-lançamento e acessar sua configuração por meio de **Programa** > **Ambiente** > **Configuração do ambiente**.

1. Adicione uma nova [variável de ambiente:](../implementing/cloud-manager/environment-variables.md)

   | Nome | Valor | Serviço aplicado | Tipo |
   |------|-------|-----------------|------|
   | `AEM_RELEASE_CHANNEL` | `prerelease` | Todos | Variável |

1. Salve as alterações e o ambiente será atualizado com as opções do recurso de pré-lançamento ativadas.

   ![Nova variável de ambiente](assets/env-configuration-prerelease.png)

#### Adicionar variável de ambiente usando a CLI {#add-with-cli}

Você também pode usar a API e a CLI do Cloud Manager para atualizar as variáveis de ambiente.

* Usando [endpoint de variáveis de ambiente da API do Cloud Manager,](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/patchEnvironmentVariables) defina as `AEM_RELEASE_CHANNEL` variável de ambiente para o valor `prerelease`.

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
   aio cloudmanager:environment:set-variables <ENVIRONMENT_ID> --programId=<PROGRAM_ID> --variable AEM_RELEASE_CHANNEL “prerelease
   ```

A variável pode ser excluída ou retornada a um valor diferente se você desejar que o ambiente seja restaurado ao comportamento do canal padrão (que não seja o de pré-lançamento)

### SDK local {#local-sdk}

Você pode ver novos recursos no console Sites no SDK do Quickstart local e código em relação às novas APIs no pré-lançamento configurando seu projeto Maven para fazer referência ao pré-lançamento `API Jar` localizada em Maven Central. Você também pode ver esses recursos de pré-lançamento no ambiente de desenvolvimento local, iniciando o SDK Quickstart normal no modo de pré-lançamento.

#### Iniciar o SDK do Quickstart no modo de pré-lançamento {#prerelease-mode}

1. Baixe o SDK no portal de distribuição de softwares e instale como descrito em [Acesso ao SDK do AEM as a Cloud Service.](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md)
1. Ao iniciar o Quickstart do SDK, inclua o argumento `-r prerelease`.

O valor é aderente, assim, ele só pode ser selecionado na primeira inicialização. Reinstale o SDK para alterar a opção de linha de comando.

Como pode haver várias versões de manutenção do AEM entre as versões de recursos mensais, você pode baixar esses novos SDKs e fazer referência às novas versões do Jar da API do SDK em projetos maven. As versões de manutenção não incluirão recursos adicionais de pré-lançamento, mas poderão incluir outras alterações menores, como correções de erros, correções de segurança e aprimoramentos de desempenho.
Javadocs são publicados no Maven Central.

#### Criar em relação ao SDK de pré-lançamento {#build-sdk}

1. Modifique os `pom.xml` para fazer referência a um jar de API do SDK de pré-lançamento distinto, que é publicado no Maven Central. Ele contém qualquer nova API Java para os recursos de pré-lançamento e tem uma dependência no jar da API do SDK. Ele usa a mesma versão.

   Como exemplo, aqui está um trecho da seção de gerenciamento de dependência do pom pai que faz referência ao jar da API regular:

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

1. Se ele funcionar conforme esperado localmente, confirme o código em uma ramificação de desenvolvimento e use um pipeline de não produção do Cloud Manager para implantar em um ambiente que assine o canal de pré-lançamento.

>[!CAUTION]
> 
> O `aem-prerelease-sdk-api` artifactId nunca deve ser usada ao implantar em estágio ou produção. Sempre use o `aem-sdk-api` ao implantar por meio do pipeline de produção. Da mesma forma, o código que faz referência às APIs de pré-lançamento não deve ser implantado por meio do pipeline de produção.

O [AEM CS SDK build do Analyzer maven plugin v1.0 e superior](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html#developing) O detectará se a API de pré-lançamento é usada em um projeto, inspecionando as dependências. Se o analisador o encontrar, ele usará a API do SDK de pré-lançamento para analisar o projeto.

## Treinar seus usuários {#train-users}

Depois de testar os novos recursos no canal de pré-lançamento e decidir aproveitá-los em seus projetos, você precisa treinar os usuários.

A Adobe Experience League oferece muitos recursos para aprender o AEMaaCS.

* [A documentação do AEMaaCS](https://experienceleague.adobe.com/docs/experience-manager-cloud-service.html?lang=pt-BR)
* [Tutoriais](https://experienceleague.adobe.com/docs/experience-manager-learn/aem-tutorials/overview.html)
* [Vídeo de visão geral da versão mensal](/help/release-notes/release-notes-cloud/release-notes-current.md#release-video) nas notas de versão

## Considerações {#considerations}

Há alguns itens a serem observados ao usar o canal de pré-lançamento.

* O canal de pré-lançamento não contém necessariamente todos os novos recursos a serem implementados na versão a seguir.
* Os recursos no pré-lançamento são submetidos a uma garantia de qualidade rigorosa e se destinam a ser completos em recursos, e não de qualidade beta. Caso detecte problemas, reporte-os, como faria se suspeitasse de erros em recursos em uma versão comum do AEM.
* Para determinar se um ambiente está configurado para o canal de pré-lançamento, vá para o console AEM **Sobre** e verifique se o número da versão AEM inclui um *pré-lançamento* sufixo como ```Adobe Experience Manager 2021.4.5226.20210427T070726Z-210429-PRERELEASE```.

![Sobre](/help/release-notes/assets/about.png)
