---
title: Envio de um conector do AEM
description: Saiba como implantar conectores usando o Cloud Manager.
exl-id: 9be1f00e-3666-411c-9001-c047e90b6ee5
source-git-commit: f7ffe727ecc7f1331c1c72229a5d7f940070c011
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 97%

---

Envio de um conector do AEM
===========================

As informações fornecidas abaixo são úteis para o envio de Conectores do AEM e devem ser lidas em conjunto com artigos sobre a [implementação](implement.md) e [manutenção](maintain.md) de conectores.

Os Conectores do AEM estão listados no [Adobe Exchange](https://partners.adobe.com/exchangeprogram/experiencecloud).

Em soluções anteriores do AEM, o [Gerenciador de pacotes](/help/implementing/developing/tools/package-manager.md) era usado para instalar conectores em várias instâncias do AEM. No entanto, com AEM as a Cloud Service, os conectores são implantados durante o processo de CI/CD no Cloud Manager. Para que os conectores sejam implantados, os conectores precisam ser referenciados no arquivo pom.xml do projeto do Maven.

Há várias opções de como os pacotes podem ser incluídos em um projeto:

1. Repositório público do parceiro — um parceiro hospedaria o pacote de conteúdo em um repositório do Maven acessível publicamente
1. Repositório protegido por senha do parceiro — um parceiro hospedaria o pacote de conteúdo em um repositório do Maven protegido por senha. Consulte [repositórios do Maven protegidos por senha](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/create-application-project/setting-up-project.html?lang=pt-BR#password-protected-maven-repositories) para obter instruções.
1. Artefato embutido — nesse caso, o pacote do conector é incluído localmente no projeto do Maven do cliente.

Independentemente de onde eles estejam hospedados, os pacotes precisam ser referenciados como dependências no arquivo pom.xml, conforme fornecido pelo fornecedor.

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

Se o parceiro ISV hospeda o conector em um repositório do Maven acessível pela Internet (acessível como o Cloud Manager), o ISV deve fornecer a configuração do repositório, onde o arquivo pom.xml pode ser colocado, para que as dependências do conector (acima) possam ser resolvidas no momento da criação (tanto localmente quanto pelo Cloud Manager).

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

Se o parceiro ISV optar por distribuir o conector como arquivos para download, o ISV deve fornecer instruções sobre como os arquivos podem ser implantados em um repositório do Maven de sistema de arquivos local que precisa ser enviado ao Git como parte do projeto do AEM, para que o Cloud Manager possa resolver essas dependências.
