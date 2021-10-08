---
title: SDK do AEM as a Cloud Service
description: Uma visão geral do AEM Kit de desenvolvimento de software as a Cloud Service
exl-id: 06f3d5ee-440e-4cc5-877a-5038f9bd44c6
source-git-commit: c08e442e58a4ff36e89a213aa7b297b538ae3bab
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# O SDK AEM as a Cloud Service {#aem-as-a-cloud-service-sdk}

O SDK as a Cloud Service AEM é composto pelos seguintes artefatos:

* **Quickstart Jar**  - O tempo de execução do AEM usado para desenvolvimento local
* **Java API Jar**  - A dependência Java Jar/Maven que expõe todas as APIs Java permitidas que podem ser usadas para desenvolver em relação ao AEM como Cloud Service. Anteriormente conhecido como Uberjar
* **Jar Javadoc**  - Os javadocs para o Java API Jar
* **Ferramentas do Dispatcher**  - O conjunto de ferramentas usadas para ser desenvolvido no Dispatcher localmente. Artefatos separados para unix e janelas

Além disso, alguns clientes que foram implantados anteriormente com AEM 6.5 ou versões anteriores usarão os artefatos abaixo. Se a compilação local não estiver funcionando com o jar do Quickstart e você suspeitar que isso se deve a interfaces que foram removidas de AEM implantadas as a Cloud Service, entre em contato com o Suporte ao cliente para determinar se você precisa de acesso. Isso exigirá alterações no back-end.

* **6.5 Jar da API do Java obsoleto**  - um conjunto adicional de interfaces que foram removidas desde a AEM 6.5
* **6.5 Javadoc obsoleto**  - o Javadocs para o conjunto adicional de interfaces

## Criação para o SDK {#building-for-the-sdk}

O SDK as a Cloud Service AEM é usado para criar e implantar código personalizado. Para obter mais detalhes, consulte a [AEM documentação do Arquétipo de projeto](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/using.html?lang=en). Em um alto nível, as seguintes etapas são executadas:

* **Compilar código**. Como esperado, o código-fonte é compilado, gerando os pacotes de conteúdo resultantes
* **Construir artefatos**. Os artefatos são construídos durante esse processo
* **Analisar pacotes**. Os pacotes são analisados usando o plug-in do analisador Maven, que procura problemas no projeto Maven, como dependências ausentes
* **Implantar artefatos**. Os artefatos são implantados no servidor local.

As mesmas etapas são executadas pelo Cloud Manager ao implantar em ambientes do Cloud. A execução de builds localmente permite o desenvolvimento e o teste locais, de modo que os desenvolvedores possam descobrir problemas de código ou estruturais com eficiência, bem antes de se comprometer com o controle de origem e acionar as implantações do Cloud Manager, o que pode demorar mais.

## Acesso ao SDK as a Cloud Service do AEM {#accessing-the-aem-as-a-cloud-service-sdk}

* Você pode verificar o ícone **Sobre o Adobe Experience Manager** para descobrir a versão do AEM que está sendo executado na produção.
* É possível baixar o jar de início rápido e as Ferramentas do Dispatcher como um arquivo zip do [Portal de distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html). Observe que o acesso às listagens do SDK está limitado àqueles com AEM Managed Services ou ambientes as a Cloud Service AEM.
* O Java API Jar e o Javadoc Jar podem ser baixados por meio de ferramentas de maven, linha de comando ou com o IDE preferido.
* Os poms do projeto maven devem fazer referência ao seguinte pacote Jar da API. Essa dependência também deve ser referenciada em quaisquer poms de subpacote.

```
<dependency>
  <groupId>com.adobe.aem</groupId>
  <artifactId>aem-sdk-api</artifactId>
  <version>2019.11.3006.20191108T223635Z-191201</version>
  <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>A entrada da versão do SDK deve corresponder à versão AEM as a Cloud Service. Você pode ver qual versão está usando fazendo logon no AEM, depois indo para o ponto de interrogação no canto superior direito da tela e selecionando **[!UICONTROL Sobre o Adobe Experience Manager]**


## Atualização de um projeto local com uma nova versão do SDK {#refreshing-a-local-project-with-a-new-skd-version}

Quando é recomendável atualizar o projeto local com um novo SDK?

É *recomendado* atualizá-lo pelo menos após uma versão de manutenção mensal.

É *opcional* para atualizá-lo após qualquer versão de manutenção diária. Os clientes serão informados quando a instância de produção for atualizada com êxito para uma nova versão de AEM. Para as versões de manutenção diárias, não se espera que o novo SDK tenha mudado significativamente, se é que mudará. Ainda assim, é recomendável atualizar ocasionalmente o ambiente de desenvolvedor do AEM local com o SDK mais recente, em seguida recriar e testar o aplicativo personalizado. A versão de manutenção mensal normalmente inclui alterações mais impactantes e, portanto, os desenvolvedores devem atualizar, reconstruir e testar imediatamente.

Abaixo está o procedimento recomendado para atualizar um ambiente local:

1. Certifique-se de que qualquer conteúdo útil esteja comprometido com o projeto no controle de origem ou disponível em um pacote de conteúdo mutável para importação posterior
1. O conteúdo do teste de desenvolvimento local precisa ser armazenado separadamente para que não seja implantado como parte da build do pipeline do Cloud Manager. Isso porque só precisa ser usado para desenvolvimento local
1. Parar o início rápido em execução no momento
1. Mova a pasta `crx-quickstart` para uma pasta diferente para manter a segurança
1. Observe a nova versão do AEM, anotada no Cloud Manager (será usada para identificar a nova versão do QuickStart Jar para fazer download mais adiante)
1. Baixe o QuickStart JAR cuja versão corresponde à versão do AEM de produção no Portal de distribuição de software
1. Crie uma nova pasta e coloque o novo QuickStart Jar dentro
1. Inicie o novo QuickStart com os modos de execução desejados (renomeando o arquivo ou transmitindo os modos de execução via `-r`).
   * Certifique-se de que não haja vestígios da inicialização rápida antiga na pasta .
1. Crie seu aplicativo AEM
1. Implante o aplicativo AEM no AEM local pelo PackageManager
1. Instale todos os pacotes de conteúdo mutável necessários para teste de ambiente local por meio do PackageManager
1. Continue desenvolvendo e implante as alterações conforme necessário

Se houver conteúdo que deve ser instalado com cada nova versão de início rápido de AEM, inclua-o em um pacote de conteúdo e no controle de origem do projeto. Em seguida, instale-o sempre.

A recomendação é atualizar o SDK com frequência (por exemplo, bisemanalmente) e descartar o estado local completo diariamente para não depender acidentalmente dos dados de estado no aplicativo.

Caso você dependa do CryptoSupport ([configurando as credenciais do Cloudservices ou do serviço SMTP Mail no AEM ou usando a API CryptoSupport no aplicativo](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/granite/crypto/CryptoSupport.html)), as propriedades criptografadas serão criptografadas por uma chave que é gerada automaticamente no primeiro início de um ambiente AEM. Embora a configuração de nuvem trate da reutilização automática da CryptoKey específica do ambiente, é necessário injetar a chave de criptografia no ambiente de desenvolvimento local.

Por padrão, o AEM é configurado para armazenar os dados principais dentro da pasta de dados de uma pasta, mas para facilitar a reutilização no desenvolvimento, o processo de AEM pode ser inicializado na primeira inicialização com &quot;`-Dcom.adobe.granite.crypto.file.disable=true`&quot;. Isso gerará os dados de criptografia em &quot;`/etc/key`&quot;.

Para poder reutilizar pacotes de conteúdo contendo os valores criptografados, siga estas etapas:

* Ao iniciar inicialmente o quickstart.jar local, adicione o parâmetro abaixo: &quot;`-Dcom.adobe.granite.crypto.file.disable=true`&quot;. É recomendável, mas opcional, sempre adicioná-lo.
* Na primeira vez que você iniciou uma instância, crie um pacote que contém um filtro para a raiz &quot;`/etc/key`&quot;. Isso manterá o segredo a ser reutilizado em todos os ambientes para os quais você deseja que eles sejam reutilizados
* Exportar qualquer conteúdo mutável que contenha segredos ou pesquisar os valores criptografados via `/crx/de` para adicioná-lo ao pacote que será reutilizado em instalações
* Sempre que você girar uma nova instância (para substituir por uma nova versão ou como vários ambientes de desenvolvimento devem compartilhar as credenciais para teste), instale o pacote produzido nas etapas 2 e 3 para poder reutilizar o conteúdo sem a necessidade de reconfigurar manualmente. Isso ocorre porque agora a chave de criptografia está sincronizada.
