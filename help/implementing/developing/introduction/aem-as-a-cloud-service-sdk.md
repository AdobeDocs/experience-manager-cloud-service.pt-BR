---
title: SDK do AEM as a Cloud Service
description: Uma visão geral do Kit de Desenvolvimento de Software as a Cloud Service AEM
exl-id: 06f3d5ee-440e-4cc5-877a-5038f9bd44c6
source-git-commit: c08e442e58a4ff36e89a213aa7b297b538ae3bab
workflow-type: tm+mt
source-wordcount: '1179'
ht-degree: 1%

---

# O SDK do AEM as a Cloud Service {#aem-as-a-cloud-service-sdk}

O SDK as a Cloud Service do AEM é composto pelos seguintes artefatos:

* **Quickstart Jar** - O tempo de execução do AEM usado para o desenvolvimento local
* **Jar da API Java** - A dependência Java Jar/Maven que expõe todas as APIs Java permitidas que podem ser usadas para desenvolver contra AEM como Cloud Service. Anteriormente conhecido como Uberjar
* **Jar do Javadoc** - Os javadocs do Jar da API Java
* **Ferramentas do Dispatcher** - O conjunto de ferramentas usadas para desenvolver localmente no Dispatcher. Artefatos separados para unix e windows

Além disso, alguns clientes que foram implantados anteriormente com AEM 6.5 ou versões anteriores usarão os artefatos abaixo. Se a compilação local não estiver funcionando com o Quickstart jar e você suspeitar que isso se deva às interfaces que foram removidas do AEM implantado as a Cloud Service, entre em contato com o Suporte ao cliente para determinar se você precisa de acesso. Isso exigirá alterações no back-end.

* **Jar da API Java obsoleta 6.5** - um conjunto adicional de interfaces que foram removidas desde o AEM 6.5
* **Jar Javadoc 6.5 obsoleto** - os Javadocs para o conjunto adicional de interfaces

## Criação para o SDK {#building-for-the-sdk}

O SDK as a Cloud Service do AEM é usado para criar e implantar código personalizado. Para obter mais detalhes, consulte [Documentação do Arquétipo de projeto do AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/using.html?lang=en). Em um nível superior, as seguintes etapas são executadas:

* **Compilar código**. Conforme esperado, o código-fonte é compilado, gerando os pacotes de conteúdo resultantes
* **Criar artefatos**. Os artefatos são criados durante esse processo
* **Analisar pacotes**. Os pacotes são analisados usando o plug-in Maven Analyzer, que procura problemas no projeto Maven, como dependências ausentes
* **Implantar artefatos**. Os artefatos são implantados no servidor local.

As mesmas etapas são executadas pelo Cloud Manager ao implantar em ambientes da nuvem. A execução de builds localmente permite o desenvolvimento e o teste locais para que os desenvolvedores possam descobrir problemas de código ou estruturais com eficiência, bem antes de se comprometerem com o controle de origem e acionarem as implantações do Cloud Manager, que podem levar mais tempo.

## Acesso ao SDK do AEM as a Cloud Service {#accessing-the-aem-as-a-cloud-service-sdk}

* Você pode verificar o Admin Console de AEM **Sobre o Adobe Experience Manager** ícone para descobrir a versão do AEM que você está executando na produção.
* As Ferramentas do quickstart jar e do Dispatcher podem ser baixadas como um arquivo zip no [Portal de distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html). Observe que o acesso às listagens do SDK está limitado aos ambientes com AEM Managed Services ou AEM as a Cloud Service.
* O Jar da API Java e o Jar do Javadoc podem ser baixados por meio das ferramentas maven, pela linha de comando ou com o IDE de sua preferência.
* Os poms de projeto maven devem fazer referência ao seguinte pacote Jar de API. Essa dependência também deve ser mencionada em todos os poms de subpacote.

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
>A entrada da versão do SDK deve corresponder à versão do AEM as a Cloud Service. Você pode ver qual versão está usando ao fazer logon no AEM, depois acessar o ponto de interrogação no canto superior direito da tela e selecionar **[!UICONTROL Sobre o Adobe Experience Manager]**


## Atualizar um projeto local com uma nova versão do SDK {#refreshing-a-local-project-with-a-new-skd-version}

Quando é recomendado atualizar o projeto local com um novo SDK?

É necessário *recomendado* para atualizá-lo pelo menos após uma versão de manutenção mensal.

É necessário *opcional* para atualizá-la após qualquer versão de manutenção diária. Os clientes serão informados quando a instância de produção for atualizada com êxito para uma nova versão do AEM. Para as versões de manutenção diárias, não é esperado que o novo SDK tenha mudado significativamente, se for o caso. Ainda assim, é recomendável atualizar ocasionalmente o ambiente de desenvolvedor do AEM local com o SDK mais recente e, em seguida, recriar e testar o aplicativo personalizado. A versão de manutenção mensal normalmente incluirá alterações mais impactantes e, portanto, os desenvolvedores devem atualizar, reconstruir e testar imediatamente.

Abaixo está o procedimento recomendado para atualizar um ambiente local:

1. Verifique se qualquer conteúdo útil está comprometido com o projeto no controle do código-fonte ou disponível em um pacote de conteúdo mutável para importação posterior
1. O conteúdo do teste de desenvolvimento local precisa ser armazenado separadamente para que não seja implantado como parte da build de pipeline do Cloud Manager. Isso ocorre porque ele só precisa ser usado para desenvolvimento local
1. Interrompe a inicialização rápida em execução no momento
1. Mova as `crx-quickstart` pasta para uma pasta diferente para manter segura
1. Observe a nova versão do AEM, que é anotada no Cloud Manager (isso será usado para identificar a nova versão do QuickStart Jar para baixar mais)
1. Baixe o QuickStart JAR cuja versão corresponda à versão do AEM de produção no Portal de distribuição de software
1. Crie uma pasta totalmente nova e coloque o novo QuickStart Jar dentro dela
1. Inicie o novo QuickStart com os modos de execução desejados (renomeando arquivos ou transmitindo-os por meio de `-r`).
   * Verifique se não há vestígios do início rápido antigo na pasta.
1. Crie seu aplicativo AEM
1. Implantar o aplicativo AEM no AEM local via PackageManager
1. Instale todos os pacotes de conteúdo mutável necessários para o teste do ambiente local via PackageManager
1. Continuar o desenvolvimento e implantar as alterações conforme necessário

Se houver conteúdo que deva ser instalado a cada nova versão de início rápido do AEM, inclua-o em um pacote de conteúdo e no controle de origem do projeto. Em seguida, instale-o sempre.

A recomendação é atualizar o SDK com frequência (por exemplo, duas vezes por semana) e descartar o estado local completo diariamente para não depender acidentalmente de dados com estado no aplicativo.

Caso você dependa de CryptoSupport ([configurando as credenciais do Cloud Services ou o serviço de email SMTP no AEM ou usando a API CryptoSupport no aplicativo](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/granite/crypto/CryptoSupport.html)), as propriedades criptografadas serão criptografadas por uma chave gerada automaticamente no primeiro início de um ambiente AEM. Embora o cloudsetup cuide da reutilização automática da CryptoKey específica do ambiente, é necessário injetar a cryptokey no ambiente de desenvolvimento local.

Por padrão, o AEM é configurado para armazenar os dados principais na pasta de dados de uma pasta, mas, para maior comodidade de reutilização no desenvolvimento, o processo AEM pode ser inicializado na primeira inicialização com &quot;`-Dcom.adobe.granite.crypto.file.disable=true`&quot;. Isso gerará os dados de criptografia em &quot;`/etc/key`&quot;.

Para poder reutilizar pacotes de conteúdo contendo os valores criptografados, é necessário seguir estas etapas:

* Ao iniciar inicialmente o quickstart.jar local, adicione o parâmetro abaixo: &quot;`-Dcom.adobe.granite.crypto.file.disable=true`&quot;. É recomendável, mas opcional, sempre adicioná-lo.
* Na primeira vez que você inicializou uma instância, crie um pacote que contenha um filtro para a raiz &quot;`/etc/key`&quot;. Isso manterá o segredo a ser reutilizado em todos os ambientes para os quais você deseja que eles sejam reutilizados
* Exporte qualquer conteúdo mutável que contenha segredos ou procure os valores criptografados via `/crx/de` para adicioná-lo ao pacote que será reutilizado nas instalações
* Sempre que você girar uma nova instância (para substituir por uma nova versão ou como vários ambientes de desenvolvimento devem compartilhar as credenciais para teste), instale o pacote produzido nas etapas 2 e 3 para poder reutilizar o conteúdo sem a necessidade de reconfigurar manualmente. Isso ocorre porque agora a chave de criptografia está sincronizada.
