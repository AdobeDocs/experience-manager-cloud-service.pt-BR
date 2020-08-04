---
title: Desenvolver comércio AEM para AEM como Cloud Service
description: Desenvolver comércio AEM para AEM como Cloud Service
translation-type: tm+mt
source-git-commit: e30086c546d9efcc1da07ac5862c012a0db02c09
workflow-type: tm+mt
source-wordcount: '808'
ht-degree: 10%

---


# Desenvolver comércio AEM para AEM como Cloud Service {#develop}

O desenvolvimento de projetos de comércio AEM baseados no Commerce Integration Framework (CIF) para AEM como Cloud Service segue as mesmas regras e práticas recomendadas, como outros projetos AEM em AEM também como Cloud Service. Leia primeiro estes itens:

- [Estrutura de projetos do AEM](https://docs.adobe.com/content/help/pt-BR/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.translate.html)
- [SDK do AEM as a Cloud Service](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/aem-as-a-cloud-service-sdk.html)
- [Diretrizes de desenvolvimento do AEM as a Cloud Service](https://docs.adobe.com/content/help/pt-BR/experience-manager-cloud-service/implementing/developing/development-guidelines.translate.html)

## Desenvolvimento local com AEM como SDK Cloud Service {#local}

Recomenda-se um ambiente de desenvolvimento local para trabalhar com projetos CIF. O suplemento CIF fornecido para AEM como ambientes Cloud Service também está disponível para desenvolvimento local. Ele pode ser baixado do portal [de distribuição de](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)software.

O suplemento CIF é fornecido como um arquivo de recursos Sling. O arquivo zip disponível no portal de Distribuição de software inclui dois arquivos de arquivamento de recursos Sling, um para AEM autor e outro para AEM instâncias de publicação.

**Novo para AEM como Cloud Service?** Consulte o guia a [seguir para configurar um ambiente de desenvolvimento local usando o AEM como um SDK](https://docs.adobe.com/content/help/en/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html)Cloud Service.

### Software necessário

O seguinte deve ser instalado localmente:

- [SDK do AEM as a Cloud Service](https://docs.adobe.com/content/help/en/*experience-manager-learn/cloud-service/local-development-environment-set-up/aem-runtime.html#download-the-aem-as-a-cloud-service-sdk)
- [Java 11](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/general.html)
- [Apache Maven](https://maven.apache.org/) (3.3.9 ou mais recente)
- [Node.js v10+](https://nodejs.org/en/)
- [npm 6+](https://www.npmjs.com/)
- [Git](https://git-scm.com/)

### Acesso ao suplemento CIF

The CIF add-on can be downloaded as a zip file from the [Software Distribution portal](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html). O arquivo zip contém o suplemento CIF como arquivo de recursos Sling, ele não é um pacote AEM. Observe que o acesso às listagens do SDK está limitado àquelas com AEM como uma licença de Cloud Service.

>[!TIP]
>
>Certifique-se de usar sempre a versão mais recente do suplemento CIF.

### Configuração local

Para o desenvolvimento local CIF Add-on usando o AEM como SDK de Cloud Service:

1. Obtenha a AEM mais recente como um SDK para Cloud Service
2. Descompacte o AEM .jar para criar a `crx-quickstart` pasta, execute:

   ```bash
   java -jar <jar name> -unpack
   ```

3. Create a `crx-quickstart/install` folder
4. Copie o arquivo de arquivo do Sling Feature correto do complemento CIF na `crx-quickstart/install` pasta.

   O arquivo zip do complemento CIF contém dois `.far` arquivos de arquivamento do recurso Sling. Certifique-se de usar o correto para AEM Author ou AEM Publish, dependendo de como você planeja executar o AEM local como um SDK Cloud Service.

5. Crie uma variável de ambiente do SO local com o nome `COMMERCE_ENDPOINT` mantendo o ponto de extremidade Magento GraphQL.

   Exemplo de Mac OSX:

   ```bash
   export COMMERCE_ENDPOINT=https://demo.magentosite.cloud/graphql
   ```

   Janelas de exemplo:

   ```bash
   set COMMERCE_ENDPOINT=https://demo.magentosite.cloud/graphql
   ```

   Essa variável também deve ser configurada para o AEM como um ambiente Cloud Service.

6. Start do AEM como um SDK Cloud Service

Verifique a configuração por meio do console OSGI:`http://localhost:4502/system/console/osgi-installer`. A lista deve incluir os pacotes relacionados ao suplemento CIF, o pacote de conteúdo e as configurações OSGI, conforme definido no arquivo de modelo de recurso.

## Configuração do projeto {#project}

Há duas maneiras de inicializar seu projeto CIF para AEM como um Cloud Service.

### Usar AEM Tipo de Arquivo do Projeto

O [AEM Project Archetype](https://github.com/adobe/aem-project-archetype) é a principal ferramenta para inicializar um projeto pré-configurado para começar com CIF. CIF Componentes principais e todas as configurações necessárias podem ser incluídas em um projeto gerado com uma opção adicional.

>[!TIP]
>
>Use [AEM Project Archetype 24 ou posterior](https://github.com/adobe/aem-project-archetype/releases) para gerar o projeto.

Consulte AEM instruções [de](https://github.com/adobe/aem-project-archetype#usage) uso do Project Archetype sobre como gerar um projeto AEM. Para incluir CIF no projeto, use a `includeCommerce` opção.

Por exemplo:

```bash
mvn -B archetype:generate \
 -D archetypeGroupId=com.adobe.granite.archetypes \
 -D archetypeArtifactId=aem-project-archetype \
 -D archetypeVersion=24 \
 -D aemVersion=cloud \
 -D appTitle="My Site" \
 -D appId="mysite" \
 -D groupId="com.mysite" \
 -D frontendModule=general \
 -D includeExamples=n \
 -D includeCommerce=y
```

CIF Componentes Principais podem ser utilizados em qualquer projeto, incluindo a embalagem fornecida `all` ou individualmente, utilizando a embalagem do conteúdo CIF e os pacotes OSGI relacionados. Para adicionar manualmente os componentes principais CIF a um projeto, use as seguintes dependências:

```java
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>core-cif-components-apps</artifactId>
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

### Usar AEM Venia Reference Store

Uma segunda opção para start de um projeto CIF é clonar e usar a Loja [de Referência de Venia](https://github.com/adobe/aem-cif-guides-venia)AEM. O AEM Venia Reference Store é um exemplo de aplicativo de referência storefront que demonstra o uso de CIF Core Components para AEM. Ela serve como um conjunto de exemplos de práticas recomendadas, bem como um ponto de partida potencial para desenvolver sua própria funcionalidade.

Para começar a usar a Venia Reference Store, basta clonar o repositório Git e o start personalizar o projeto de acordo com suas necessidades.

>[!NOTE]
>
>O projeto Venia Reference Store contém dois perfis de construção para AEM como Cloud Service e AEM 6.5. Verifique o arquivo readme.md [do](https://github.com/adobe/aem-cif-guides-venia/blob/main/README.md) projeto para ver como eles são usados.

## Recursos adicionais

- [AEM Project Archetype](https://github.com/adobe/aem-project-archetype)
- [AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia)
- [Portal de distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)
