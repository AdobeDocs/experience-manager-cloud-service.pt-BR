---
title: SDK do AEM as a Cloud Service
description: 'A completar '
translation-type: tm+mt
source-git-commit: a7dc007230632bf8343004794b2bc4c5baaf4e05

---


# The AEM as a Cloud Service SDK {#aem-as-a-cloud-service-sdk}

O AEM como um SDK de serviço em nuvem é composto pelos seguintes artefatos:

* **Jar** de início rápido - O tempo de execução do AEM usado para desenvolvimento local
* **Java API Jar** - a Dependência Java Jar/Maven que expõe todas as APIs Java permitidas que podem ser usadas para desenvolvimento em relação ao AEM como serviço de nuvem. Anteriormente conhecido como Uberjar
* **Jar** Javadoc - O javadocs para o Java API Jar
* **Ferramentas** do Dispatcher - o conjunto de ferramentas usado para desenvolver no Dispatcher localmente. Separe artefatos para unix e janelas

Além disso, alguns clientes que foram implantados anteriormente com o AEM 6.5 ou versões anteriores usarão os artefatos abaixo. Se a compilação local não estiver funcionando com o jar do Quickstart e você suspeitar que isso seja devido a interfaces que foram removidas do AEM implantadas como um serviço em nuvem, entre em contato com o Suporte ao cliente para determinar se você precisa de acesso. Isso exigirá alterações no backend.

* **6.5 Java API Jar** obsoleto - um conjunto adicional de interfaces que foram removidas desde o AEM 6.5
* **6.5 Javadoc Jar** obsoleto - os Javadocs para o conjunto adicional de interfaces

## Acessar o AEM como um SDK de serviço em nuvem {#accessing-the-aem-as-a-cloud-service-sdk}

* Você pode verificar o ícone **Sobre o Adobe Experience Manager** do Admin Console do AEM para descobrir a versão do AEM que você está executando na produção.
* As Ferramentas QuickStart jar e Dispatcher podem ser baixadas como um arquivo zip do portal [de Distribuição de](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/aemcloud.html)software. Observe que o acesso às listagens do SDK é limitado àquelas com os serviços gerenciados do AEM ou o AEM como ambientes de serviço em nuvem.
* O Java API Jar e o Javadoc Jar podem ser baixados por meio da ferramenta maven, linha de comando ou com seu IDE preferencial.
* Os poms do projeto maven devem fazer referência ao seguinte pacote de API Jar. Essa dependência também deve ser referenciada em quaisquer salas de subpacotes.

```
<dependency>
  <groupId>com.adobe.aem</groupId>
  <artifactId>aem-sdk-api</artifactId>
  <version>2019.11.3006.20191108T223635Z-191201</version> 
  <scope>provided</scope>
</dependency>
```

> [!NOTE] A entrada da versão do SDK deve corresponder à versão do AEM como um serviço em nuvem. Você pode ver qual versão está usando fazendo logon no AEM, indo para o ponto de interrogação no canto superior direito da tela e selecionando **[!UICONTROL Sobre o Adobe Experience Manager]**

* A coordenada remota para o repositório maven onde o pacote está hospedado deve ser incluída no arquivo pom.

```
<repository>
    <id>adobe-aem-releases</id>
    <name>Adobe AEM Repository</name>
    <url>https://downloads.experiencecloud.adobe.com/content/maven/public</url>
    <releases>
        <enabled>true</enabled>
        <updatePolicy>never</updatePolicy>
    </releases>
    <snapshots>
        <enabled>false</enabled>
    </snapshots>
</repository>
```

## Atualização de um projeto local com uma nova versão do SDK {#refreshing-a-local-prokect-with-a-new-skd-version}

Quando é recomendado atualizar o projeto local com um novo SDK?

É *recomendável* atualizá-la pelo menos após uma versão de manutenção mensal.

É *opcional* atualizá-lo após qualquer versão de manutenção diária. Os clientes serão informados quando sua instância de produção for atualizada com êxito para uma nova versão do AEM. Para as versões de manutenção diárias, não é de se esperar que o novo SDK tenha mudado significativamente, se é que isso aconteceu. No entanto, é recomendável atualizar ocasionalmente o ambiente de desenvolvedor do AEM local com o SDK mais recente, em seguida, recriar e testar o aplicativo personalizado. A versão de manutenção mensal normalmente inclui alterações mais impactantes e, portanto, os desenvolvedores devem atualizar, reconstruir e testar imediatamente.

Abaixo está o procedimento recomendado para atualizar um ambiente local:

1. Certifique-se de que qualquer conteúdo útil seja enviado para o projeto no controle de origem ou esteja disponível em um pacote de conteúdo mutável para importação posterior
1. O conteúdo do teste de desenvolvimento local precisa ser armazenado separadamente para que não seja implantado como parte da compilação do pipeline do Gerenciador de nuvem. Isso porque só precisa ser usado para o desenvolvimento local
1. Parar o início rápido atualmente em execução
1. Mova a `crx-quickstart` pasta para uma pasta diferente para manter a segurança
1. Observe a nova versão do AEM, que é anotada no Gerenciador de nuvem (isso será usado para identificar a nova versão do QuickStart Jar para fazer download mais adiante)
1. Baixe o JAR QuickStart cuja versão corresponda à versão do Production AEM do Portal de distribuição de software
1. Crie uma nova pasta e insira o novo QuickStart Jar dentro
1. Start o novo QuickStart com os modos de execução desejados (renomeando o arquivo ou transmitindo os modos de execução via `-r`).
   * Certifique-se de que não há vestígios do arranque rápido antigo na pasta.
1. Criar seu aplicativo AEM
1. Implantar seu aplicativo AEM no AEM local via PackageManager
1. Instale todos os pacotes de conteúdo mutável necessários para teste de ambiente local via PackageManager
1. Continuar o desenvolvimento e implantar as alterações conforme necessário

Se houver conteúdo que deva ser instalado com cada nova versão de início rápido do AEM, inclua-o em um pacote de conteúdo e no controle de origem do projeto. Em seguida, instale-o sempre.

A recomendação é atualizar o SDK frequentemente (por exemplo, bisemanalmente) e descartar o estado local completo diariamente para não depender acidentalmente dos dados de estado no aplicativo.

Caso você dependa do CryptoSupport ([pela configuração das credenciais do Cloudservices ou do serviço de Email SMTP no AEM ou pelo uso da API CryptoSupport no aplicativo](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/crypto/CryptoSupport.html)), as propriedades criptografadas serão criptografadas por uma chave gerada automaticamente no primeiro start de um ambiente AEM. Enquanto a configuração de nuvem cuida da reutilização automática da CryptoKey específica do ambiente, é necessário injetar a chave de criptografia no ambiente de desenvolvimento local.

Por padrão, o AEM está configurado para armazenar os dados principais na pasta de dados de uma pasta, mas para facilitar a reutilização no desenvolvimento, o processo do AEM pode ser inicializado na primeira inicialização com &quot;`-Dcom.adobe.granite.crypto.file.disable=true`&quot;. Isso gerará os dados de criptografia em &quot;`/etc/key`&quot;.

Para poder reutilizar pacotes de conteúdo contendo os valores criptografados, siga estas etapas:

* Ao start inicial do quickstart.jar local, adicione o parâmetro abaixo: &quot;`-Dcom.adobe.granite.crypto.file.disable=true`&quot;. É recomendável, mas opcional, sempre adicioná-lo.
* A primeira vez que você iniciou uma instância cria um pacote que contém um filtro para a raiz &quot;`/etc/key`&quot;. Isso manterá o segredo a ser reutilizado em todos os ambientes para os quais você gostaria que fossem reutilizados
* Exporte qualquer conteúdo silencioso que contenha segredos ou procure os valores criptografados por meio `/crx/de` do para adicioná-lo ao pacote que será reutilizado em instalações
* Sempre que você gira uma nova instância (para substituir por uma nova versão ou como vários ambientes dev devem compartilhar as credenciais para teste), instale o pacote produzido nas etapas 2 e 3 para poder reutilizar o conteúdo sem a necessidade de reconfigurar manualmente. Isso porque agora a chave de criptografia está sincronizada.