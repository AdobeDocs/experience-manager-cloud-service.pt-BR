---
title: SDK do AEM as a Cloud Service
description: Visão geral do AEM como um Kit de desenvolvimento de software para Cloud Service
translation-type: tm+mt
source-git-commit: 0b46cc8ce4229138df84c70193cf9068e1200f0a
workflow-type: tm+mt
source-wordcount: '1181'
ht-degree: 1%

---


# The AEM as a Cloud Service SDK {#aem-as-a-cloud-service-sdk}

O AEM como um SDK Cloud Service é composto pelos seguintes artefatos:

* **Jar** Quickstart - O tempo de execução AEM usado para desenvolvimento local
* **Java API Jar** - a Dependência Java Jar/Maven que expõe todas as APIs Java permitidas que podem ser usadas para desenvolvimento contra AEM como Cloud Service. Anteriormente conhecido como Uberjar
* **Jar** Javadoc - O javadocs para o Java API Jar
* **Ferramentas** do Dispatcher - o conjunto de ferramentas usado para desenvolver no Dispatcher localmente. Separe artefatos para unix e janelas

Além disso, alguns clientes que foram implantados anteriormente com AEM 6.5 ou versões anteriores usarão os artefatos abaixo. Se a compilação local não estiver funcionando com o jar Quickstart e você suspeitar que isso seja devido a interfaces que foram removidas de AEM implantadas como Cloud Service, entre em contato com o Suporte ao cliente para determinar se você precisa de acesso. Isso exigirá alterações no backend.

* **6.5 Java API Jar** obsoleto - um conjunto adicional de interfaces que foram removidas desde AEM 6.5
* **6.5 Javadoc Jar** obsoleto - os Javadocs para o conjunto adicional de interfaces

## Criação para o SDK {#building-for-the-sdk}

O AEM como um SDK Cloud Service é usado para criar e implantar código personalizado. Para obter mais detalhes, consulte a documentação do [AEM Project Archetype](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/using.html?lang=en). Em um nível alto, as seguintes etapas são executadas:

* **Compilar código**. Como esperado, o código-fonte é compilado, gerando os pacotes de conteúdo resultantes
* **Construa artefatos**. Os artefatos são construídos durante esse processo
* **Analisar pacotes**. Os pacotes são analisados usando o plug-in do analisador Maven, que procura problemas no projeto Maven, como dependências ausentes
* **Implante artefatos**. Os artefatos são implantados no servidor local.

As mesmas etapas são executadas pelo Gerenciador de nuvem ao implantar Ambientes da Cloud. A execução de builds localmente permite o desenvolvimento e o teste locais para que os desenvolvedores possam descobrir problemas estruturais ou de código com eficiência bem antes de se comprometer com o controle de origem e acionar as implantações do Cloud Manager, o que pode demorar mais.

## Accessing the AEM as a Cloud Service SDK {#accessing-the-aem-as-a-cloud-service-sdk}

* Você pode verificar o ícone AEM Admin Console **About Adobe Experience Manager** para descobrir a versão do AEM que está sendo executado na produção.
* As Ferramentas QuickStart jar e Dispatcher podem ser baixadas como um arquivo zip do portal [de Distribuição de](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)software. Observe que o acesso às listagens do SDK é limitado àquelas com AEM Managed Services ou AEM como ambientes Cloud Service.
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

>[!NOTE]
>
>A entrada da versão do SDK deve corresponder à versão do AEM como um Cloud Service. Você pode ver qual versão está usando fazendo logon no AEM, indo para o ponto de interrogação no canto superior direito da tela e selecionando **[!UICONTROL Sobre o Adobe Experience Manager]**


## Atualização de um projeto local com uma nova versão do SDK {#refreshing-a-local-project-with-a-new-skd-version}

Quando é recomendado atualizar o projeto local com um novo SDK?

É *recomendável* atualizá-la pelo menos após uma versão de manutenção mensal.

É *opcional* atualizá-lo após qualquer versão de manutenção diária. Os clientes serão informados quando sua instância de produção for atualizada com êxito para uma nova versão AEM. Para as versões de manutenção diárias, não é de se esperar que o novo SDK tenha mudado significativamente, se é que isso aconteceu. Ainda assim, é recomendável atualizar ocasionalmente o ambiente local AEM desenvolvedor com o SDK mais recente, em seguida, recriar e testar o aplicativo personalizado. A versão de manutenção mensal normalmente inclui alterações mais impactantes e, portanto, os desenvolvedores devem atualizar, reconstruir e testar imediatamente.

Abaixo está o procedimento recomendado para atualizar um ambiente local:

1. Certifique-se de que qualquer conteúdo útil seja enviado para o projeto no controle de origem ou esteja disponível em um pacote de conteúdo mutável para importação posterior
1. O conteúdo do teste de desenvolvimento local precisa ser armazenado separadamente para que não seja implantado como parte da compilação do pipeline do Gerenciador de nuvem. Isso porque só precisa ser usado para o desenvolvimento local
1. Parar o início rápido atualmente em execução
1. Mova a `crx-quickstart` pasta para uma pasta diferente para manter a segurança
1. Observe a nova versão do AEM, que é anotada no Cloud Manager (ela será usada para identificar a nova versão do QuickStart Jar para fazer o download mais adiante)
1. Baixe o JAR QuickStart cuja versão corresponda à versão AEM Produção do Portal de Distribuição de Software
1. Crie uma nova pasta e insira o novo QuickStart Jar dentro
1. Start o novo QuickStart com os modos de execução desejados (renomeando o arquivo ou transmitindo os modos de execução via `-r`).
   * Certifique-se de que não há vestígios do arranque rápido antigo na pasta.
1. Crie seu aplicativo AEM
1. Implantar seu aplicativo AEM para AEM local via PackageManager
1. Instale todos os pacotes de conteúdo mutável necessários para teste de ambiente local via PackageManager
1. Continuar o desenvolvimento e implantar as alterações conforme necessário

Se houver conteúdo que deve ser instalado com cada nova versão de início rápido AEM, inclua-o em um pacote de conteúdo e no controle de origem do projeto. Em seguida, instale-o sempre.

A recomendação é atualizar o SDK frequentemente (por exemplo, bisemanalmente) e descartar o estado local completo diariamente para não depender acidentalmente dos dados de estado no aplicativo.

Caso você dependa do CryptoSupport ([pela configuração das credenciais do Cloudservices ou do serviço de Email SMTP no AEM ou pelo uso da API CryptoSupport no aplicativo](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/crypto/CryptoSupport.html)), as propriedades criptografadas serão criptografadas por uma chave gerada automaticamente no primeiro start de um ambiente AEM. Enquanto a configuração de nuvem cuida da reutilização automática da CryptoKey específica do ambiente, é necessário injetar a chave de criptografia no ambiente de desenvolvimento local.

Por padrão, o AEM é configurado para armazenar os dados principais dentro da pasta de dados de uma pasta, mas para facilitar a reutilização no desenvolvimento, o processo de AEM pode ser inicializado na primeira inicialização com &quot;`-Dcom.adobe.granite.crypto.file.disable=true`&quot;. Isso gerará os dados de criptografia em &quot;`/etc/key`&quot;.

Para poder reutilizar pacotes de conteúdo contendo os valores criptografados, siga estas etapas:

* Ao start inicial do quickstart.jar local, adicione o parâmetro abaixo: &quot;`-Dcom.adobe.granite.crypto.file.disable=true`&quot;. É recomendável, mas opcional, sempre adicioná-lo.
* A primeira vez que você iniciou uma instância cria um pacote que contém um filtro para a raiz &quot;`/etc/key`&quot;. Isso manterá o segredo a ser reutilizado em todos os ambientes para os quais você gostaria que fossem reutilizados
* Exporte qualquer conteúdo silencioso que contenha segredos ou procure os valores criptografados por meio `/crx/de` do para adicioná-lo ao pacote que será reutilizado em instalações
* Sempre que você gira uma nova instância (para substituir por uma nova versão ou como vários ambientes dev devem compartilhar as credenciais para teste), instale o pacote produzido nas etapas 2 e 3 para poder reutilizar o conteúdo sem a necessidade de reconfigurar manualmente. Isso porque agora a chave de criptografia está sincronizada.
