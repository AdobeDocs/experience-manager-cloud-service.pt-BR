---
title: Envio de um conector do AEM
description: Envio de um conector do AEM
translation-type: tm+mt
source-git-commit: bffc335fdafe6bf12a66bcd2f7aacf029fce567e
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 12%

---


Envio de um conector do AEM
===========================

As informações fornecidas abaixo são úteis para o envio de Conectores do AEM e devem ser lidas em conjunto com artigos sobre a [implementação](implement.md) e [manutenção](maintain.md) de conectores.

Os Conectores AEM estão listados no [Adobe Exchange](https://partners.adobe.com/exchangeprogram/experiencecloud).

Nas soluções AEM anteriores, o Gerenciador de pacotes era usado para instalar conectores em várias instâncias do AEM. No entanto, com o AEM como Cloud Service, os conectores são implantados durante o processo de CI/CD no Cloud Manager. Para que os conectores sejam implantados, os conectores precisam ser referenciados no pom.xml do projeto maven.

Há várias opções de como os pacotes podem ser incluídos em um projeto:

1. Repositório público do parceiro - um parceiro hospedaria o pacote de conteúdo em um repositório maven acessível ao público
1. Artefato embutido - nesse caso, o pacote do conector é incluído localmente no projeto maven do cliente.

Independentemente de onde eles estejam hospedados, os pacotes precisam ser referenciados como dependências no pom.xml, conforme fornecido pelo fornecedor.

```xml
<!-- UberJAR Dependency to be added to the project's Reactor pom.xml -->
<dependency>
  <groupId>com.partnername</groupId>
  <artifactId>my-artifact</artifactId>
  <version>V123</version> <!-- use the latest! -->
  <scope>provided</scope>
  <classifier>my_classifier</classifier>
</dependency>
```

Se o parceiro ISV hospedar o conector em um repositório de mídia acessível à Internet (como o Cloud Manager acessível), o ISV deverá fornecer a configuração do repositório onde o pom.xml pode ser colocado, para que as dependências do conector (acima) possam ser resolvidas no momento da criação (tanto localmente quanto pelo Cloud Manager).

```xml
<repository>
    <id>the-repository</id>
    <name>The Repository Where the Connector is Hosted</name>
    <url>https://repo.partnername.com/repositories/aem_connector_repo</url>
    <releases>
        <enabled>true</enabled>
        <updatePolicy>never</updatePolicy>
    </releases>
    <snapshots>
        <enabled>false</enabled>
    </snapshots>
</repository>
```

Se o parceiro ISV optar por distribuir o Conector como arquivos baixáveis, o ISV deverá fornecer instruções sobre como os arquivos podem ser implantados em um repositório de servidor local do sistema de arquivos que precisa ser verificado no Git como parte do projeto AEM, para que o Cloud Manager possa resolver essas dependências.
