---
title: Desenvolver o AEM Commerce para o AEM as a Cloud Service
description: Saiba como gerar um projeto do AEM habilitado para comércio usando o arquétipo de projeto do AEM. Saiba como criar e implantar o projeto em um ambiente de desenvolvimento local usando o AEM as a Cloud Service SDK.
topics: Commerce, Development
feature: Commerce Integration Framework
version: Experience Manager as a Cloud Service
doc-type: tutorial
kt: 5826
thumbnail: 39476.jpg
exl-id: 6f28a52b-52f8-4b30-95cd-0f9cb521de62
role: Admin
index: false
source-git-commit: 173b70aa6f9ad848d0f80923407bf07540987071
workflow-type: tm+mt
source-wordcount: '908'
ht-degree: 41%

---

# Desenvolver o AEM Commerce para o AEM as a Cloud Service {#develop}

O desenvolvimento de projetos do AEM Commerce, com base no Commerce integration framework (CIF) for AEM as a Cloud Service, segue as mesmas regras e práticas recomendadas de outros projetos do AEM no AEM as a Cloud Service. Revise o seguinte primeiro:

- [Estrutura de projetos do AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure.html?lang=pt-BR)
- [SDK do AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=pt-BR)
- [Diretrizes de desenvolvimento do AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines.html?lang=pt-BR)

## Desenvolvimento local com o AEM as a Cloud Service SDK {#local}

>[!VIDEO](https://video.tv.adobe.com/v/39476/?quality=12&learn=on)

Um ambiente de desenvolvimento local é recomendado para trabalhar com projetos da CIF. O complemento do CIF fornecido para o AEM as a Cloud Service também está disponível para desenvolvimento local. Ele pode ser baixado no [Portal de distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html).

O complemento CIF é fornecido como um arquivo de recursos Sling. O arquivo zip disponível no Portal de distribuição de software inclui dois arquivos de recursos Sling, um para o autor no AEM e outro para instâncias de publicação do AEM.

**Novo no AEM as a Cloud Service?** Confira [um guia mais detalhado para configurar um ambiente de desenvolvimento local usando o AEM as a Cloud Service SDK](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html?lang=pt-BR).

### Software necessário

Devem ser instalados:

- [SDK do AEM as a Cloud Service](https://experienceleague.adobe.com/pt-br/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/aem-runtime#download-the-aem-as-a-cloud-service-sdk)
- [Java™ 11](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/general.html)
- [Apache Maven](https://maven.apache.org/) (3.3.9 ou mais recente)
- [Node.js v10+](https://nodejs.org/en)
- [npm 6+](https://www.npmjs.com/)
- [Git](https://git-scm.com/)

### Acesso ao complemento CIF

É possível baixar o complemento CIF como um arquivo zip no [Portal de distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html). O arquivo zip contém o complemento CIF como **arquivo de recursos Sling**, não é um pacote AEM. As listagens do SDK podem ser acessadas com uma licença do AEM as a Cloud Service.

>[!TIP]
>
>Use sempre a versão mais recente do complemento CIF.

### Configuração local

Para o desenvolvimento local do complemento CIF usando o AEM as a Cloud Service, siga estas etapas:

1. Obtenha o SDK do AEM as a Cloud Service mais recente
1. Descompacte o AEM .jar para que você possa criar a pasta `crx-quickstart` e execute:

   ```bash
   java -jar <jar name> -unpack
   ```

1. Crie uma pasta `crx-quickstart/install`
1. Copie o arquivo de recursos Sling correto do complemento CIF na pasta `crx-quickstart/install`.

   O arquivo zip do complemento CIF contém dois arquivos `.far` de recursos Sling. Use o arquivo correto para autor ou publicação no AEM, dependendo de como você planeja executar o SDK do AEM as a Cloud Service local.

1. Crie uma variável de ambiente do sistema operacional local com o nome `COMMERCE_ENDPOINT` que contenha o ponto de extremidade do Adobe Commerce GraphQL.

   Exemplo macOS X:

   ```bash
   export COMMERCE_ENDPOINT=https://<yourcommercesystem>/graphql
   ```

   Exemplo para Windows:

   ```bash
   set COMMERCE_ENDPOINT=https://<yourcommercesystem>/graphql
   ```

   Essa variável é usada pelo AEM para se conectar ao sistema de comércio. Além disso, o complemento CIF inclui um proxy reverso local para disponibilizar o endpoint do Commerce GraphQL localmente. Esse proxy é usado pelas ferramentas de criação do CIF (console do produto e seletores) e para os componentes do lado do cliente do CIF que fazem chamadas diretas de GraphQL.

   Essa variável também deve ser configurada para o ambiente do AEM as a Cloud Service. Para obter mais informações sobre variáveis, consulte [Configurar OSGi para AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/configuring-osgi.html?lang=pt-BR#local-development).

1. (Opcional) Para ativar recursos de catálogo em etapas, você deve criar um token de integração para sua instância do Adobe Commerce. Siga as etapas em [Introdução](./getting-started.md#staging) para criar o token.

   Defina um segredo OSGi com o nome `COMMERCE_AUTH_HEADER` com o seguinte valor:

   ```xml
   Authorization: Bearer <Access Token>
   ```

   Para obter mais informações sobre segredos, consulte [Configuração de OSGi para AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/configuring-osgi.html?lang=pt-BR#local-development).

1. Inicie o SDK do AEM as a Cloud Service

>[!NOTE]
>
>Inicie o AEM as a Cloud Service SDK na mesma janela de terminal em que a variável de ambiente foi definida na etapa 5. Se você iniciá-lo em uma janela de terminal separada ou clicando duas vezes no arquivo .jar, verifique se a variável de ambiente está visível.

Verifique a configuração por meio do console OSGI: `http://localhost:4502/system/console/osgi-installer`. A lista deve incluir os pacotes relacionados ao complemento CIF, o pacote de conteúdo e as configurações OSGI, conforme definido no arquivo de modelo de recurso.

## Configuração do projeto {#project}

Há duas maneiras de Bootstrap seu projeto do CIF para o AEM as a Cloud Service.

### Usar o Arquétipo de projeto do AEM

O [Arquétipo de projeto do AEM](https://github.com/adobe/aem-project-archetype) é a principal ferramenta para o Bootstrap, um projeto pré-configurado para começar a usar o CIF. Os Componentes principais da CIF e todas as configurações necessárias podem ser incluídos em um projeto gerado com uma opção adicional.

>[!TIP]
>
>Sempre use a versão mais recente do [Arquétipo de Projetos AEM](https://github.com/adobe/aem-project-archetype/releases) para gerar o projeto.

Consulte as [instruções de uso](https://github.com/adobe/aem-project-archetype#usage) do Arquétipo de projeto do AEM sobre como gerar um projeto do AEM. Para incluir CIF no projeto, use a opção `includeCommerce`.

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

Os Componentes principais do CIF podem ser usados em qualquer projeto incluindo o pacote `all` fornecido ou individualmente usando o pacote de conteúdo do CIF e os pacotes OSGI relacionados. Para adicionar manualmente os Componentes principais do CIF a um projeto, use as seguintes dependências:

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
>O projeto da loja de referência Venia contém dois perfis de construção para o AEM as a Cloud Service e o AEM 6.5. Verifique o [arquivo readme.md](https://github.com/adobe/aem-cif-guides-venia/blob/main/README.md) do projeto para ver como ele é usado.

## Recursos adicionais

- [Arquétipo de projeto do AEM](https://github.com/adobe/aem-project-archetype)
- [Loja de referência Venia](https://github.com/adobe/aem-cif-guides-venia)
- [Portal de distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)
