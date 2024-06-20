---
title: Desenvolver o AEM Commerce para o AEM as a Cloud Service
description: Saiba como gerar um projeto AEM habilitado para comércio usando o arquétipo de projeto AEM. Saiba como criar e implantar o projeto em um ambiente de desenvolvimento local usando o SDK as a Cloud Service do AEM.
topics: Commerce, Development
feature: Commerce Integration Framework
version: Cloud Service
doc-type: tutorial
kt: 5826
thumbnail: 39476.jpg
exl-id: 6f28a52b-52f8-4b30-95cd-0f9cb521de62
role: Admin
source-git-commit: 0e328d013f3c5b9b965010e4e410b6fda2de042e
workflow-type: tm+mt
source-wordcount: '908'
ht-degree: 41%

---

# Desenvolver o AEM Commerce para o AEM as a Cloud Service {#develop}

O desenvolvimento de projetos de Commerce de AEM, com base no Commerce integration framework (CIF AEM) para as a Cloud Service AEM AEM as a Cloud Service, segue as mesmas regras e práticas recomendadas, como outros projetos de em. Revise o seguinte primeiro:

- [Estrutura de projetos do AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure.html?lang=pt-BR)
- [SDK do AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=pt-BR)
- [Diretrizes de desenvolvimento do AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines.html)

## Desenvolvimento local com o SDK do AEM as a Cloud Service {#local}

>[!VIDEO](https://video.tv.adobe.com/v/39476/?quality=12&learn=on)

Um ambiente de desenvolvimento local é recomendado para trabalhar com projetos da CIF. O complemento CIF fornecido para AEM as a Cloud Service também está disponível para desenvolvimento local. Ele pode ser baixado no [Portal de distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html).

O complemento CIF é fornecido como um arquivo de recursos Sling. O arquivo zip disponível no Portal de distribuição de software inclui dois arquivos de recursos Sling, um para o autor no AEM e outro para instâncias de publicação do AEM.

**Novo no AEM as a Cloud Service?** Confira [um guia mais detalhado para configurar um ambiente de desenvolvimento local usando o SDK as a Cloud Service do AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html?lang=pt-BR).

### Software necessário

Devem ser instalados:

- [SDK do AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/aem-runtime.html#download-the-aem-as-a-cloud-service-sdk)
- [Java™ 11](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/general.html)
- [Apache Maven](https://maven.apache.org/) (3.3.9 ou mais recente)
- [Node.js v10+](https://nodejs.org/en)
- [npm 6+](https://www.npmjs.com/)
- [Git](https://git-scm.com/)

### Acesso ao complemento CIF

É possível baixar o complemento CIF como um arquivo zip no [Portal de distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html). O arquivo zip contém o complemento CIF como **Arquivo de recursos do Sling**, não é um pacote de AEM. As listagens do SDK podem ser acessadas com uma licença do AEM as a Cloud Service.

>[!TIP]
>
>Use sempre a versão mais recente do complemento CIF.

### Configuração local

Para o desenvolvimento local do complemento CIF usando o AEM as a Cloud Service, siga estas etapas:

1. Obtenha o SDK do AEM as a Cloud Service mais recente
1. Descompacte o AEM .jar para que você possa criar o `crx-quickstart` pasta, execute:

   ```bash
   java -jar <jar name> -unpack
   ```

1. Crie uma pasta `crx-quickstart/install`
1. Copie o arquivo de recursos Sling correto do complemento CIF na pasta `crx-quickstart/install`.

   O arquivo zip do complemento CIF contém dois arquivos `.far` de recursos Sling. Use o arquivo correto para autor ou publicação no AEM, dependendo de como você planeja executar o SDK do AEM as a Cloud Service local.

1. Crie uma variável de ambiente do sistema operacional local chamada `COMMERCE_ENDPOINT` mantendo o endpoint do Adobe Commerce GraphQL.

   Exemplo macOS X:

   ```bash
   export COMMERCE_ENDPOINT=https://<yourcommercesystem>/graphql
   ```

   Exemplo para Windows:

   ```bash
   set COMMERCE_ENDPOINT=https://<yourcommercesystem>/graphql
   ```

   Essa variável é usada pelo AEM para se conectar ao sistema de comércio. Além disso, o complemento CIF inclui um proxy reverso local para disponibilizar o endpoint do Commerce GraphQL localmente. Esse proxy é usado pelas ferramentas de criação do CIF (console do produto e seletores) e para os componentes do lado do cliente CIF que fazem chamadas diretas de GraphQL.

   Essa variável também deve ser configurada para o ambiente as a Cloud Service do AEM. Para obter mais informações sobre variáveis, consulte [Configuração do OSGi para o AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/configuring-osgi.html#local-development).

1. (Opcional) Para ativar recursos de catálogo em etapas, você deve criar um token de integração para sua instância do Adobe Commerce. Siga as etapas em [Introdução](./getting-started.md#staging) para criar o token.

   Definir um segredo OSGi com o nome `COMMERCE_AUTH_HEADER` ao seguinte valor:

   ```xml
   Authorization: Bearer <Access Token>
   ```

   Para obter mais informações sobre segredos, consulte [Configuração do OSGi para o AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/configuring-osgi.html#local-development).

1. Inicie o SDK do AEM as a Cloud Service

>[!NOTE]
>
>Inicie o SDK as a Cloud Service do AEM na mesma janela de terminal em que a variável de ambiente foi definida na etapa 5. Se você iniciá-lo em uma janela de terminal separada ou clicando duas vezes no arquivo .jar, verifique se a variável de ambiente está visível.

Verifique a configuração por meio do console OSGI: `http://localhost:4502/system/console/osgi-installer`. A lista deve incluir os pacotes relacionados ao complemento CIF, o pacote de conteúdo e as configurações OSGI, conforme definido no arquivo de modelo de recurso.

## Configuração do projeto {#project}

Há duas maneiras de Bootstrap seu projeto CIF para o AEM as a Cloud Service.

### Usar o Arquétipo de projeto do AEM

A variável [Arquétipo de projeto AEM](https://github.com/adobe/aem-project-archetype) O é a principal ferramenta para Bootstrap um projeto pré-configurado e começar a usar o CIF. Os Componentes principais da CIF e todas as configurações necessárias podem ser incluídos em um projeto gerado com uma opção adicional.

>[!TIP]
>
>Sempre usar a versão mais recente do [Arquétipo de projeto AEM](https://github.com/adobe/aem-project-archetype/releases) então você pode gerar o projeto.

Consulte as [instruções de uso](https://github.com/adobe/aem-project-archetype#usage) do Arquétipo de projeto do AEM sobre como gerar um projeto do AEM. Para incluir o CIF no projeto, use o `includeCommerce` opção.

Por exemplo:

```bash
mvn -B org.apache.maven.plugins:maven-archetype-plugin:3.2.1:generate \
 -D archetypeGroupId=com.adobe.aem \
 -D archetypeArtifactId=aem-project-archetype \
 -D archetypeVersion=35 \
 -D appTitle="My Site" \
 -D appId="mysite" \
 -D groupId="com.mysite" \
 -D includeCommerce=y
```

Componentes principais do CIF podem ser usados em qualquer projeto, incluindo os `all` pacote ou individualmente usando o pacote de conteúdo CIF e os pacotes OSGI relacionados. Para adicionar manualmente os Componentes principais do CIF a um projeto, use as seguintes dependências:

```java
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>core-cif-components-apps</artifactId>
    <type>zip</type>
    <version>x.y.z</version>
</dependency>
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>core-cif-components-config</artifactId>
    <type>zip</type>
    <version>x.y.z</version>
</dependency>
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>core-cif-components-core</artifactId>
    <version>x.y.z</version>
</dependency>
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>graphql-client</artifactId>
    <version>x.y.z</version>
</dependency>
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>magento-graphql</artifactId>
    <version>x.y.z</version>
</dependency>
```

### Usar a loja de referência AEM Venia

Uma segunda opção para iniciar um projeto da CIF é clonar e usar a [loja de referência AEM Venia](https://github.com/adobe/aem-cif-guides-venia). A loja de referência AEM Venia é um exemplo de aplicativo de vitrine de referência que demonstra o uso dos Componentes principais da CIF para o AEM. Ela serve como um conjunto de exemplos de práticas recomendadas e um possível ponto de partida para desenvolver sua própria funcionalidade.

Para começar a usar a loja de referência Venia, clone o repositório Git e comece a personalizar o projeto de acordo com suas necessidades.

>[!NOTE]
>
>O projeto Loja de referência Venia contém dois perfis de construção para AEM as a Cloud Service e AEM 6.5. Marcar [readme.md do projeto](https://github.com/adobe/aem-cif-guides-venia/blob/main/README.md) para que você possa ver como eles são usados.

## Recursos adicionais

- [Arquétipo de projeto do AEM](https://github.com/adobe/aem-project-archetype)
- [Loja de referência Venia](https://github.com/adobe/aem-cif-guides-venia)
- [Portal de distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)
