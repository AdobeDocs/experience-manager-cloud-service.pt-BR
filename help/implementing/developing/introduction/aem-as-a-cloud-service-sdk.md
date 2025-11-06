---
title: SDK do AEM as a Cloud Service
description: Uma visão geral do Kit de desenvolvimento de software da AEM as a Cloud Service.
exl-id: 06f3d5ee-440e-4cc5-877a-5038f9bd44c6
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1246'
ht-degree: 1%

---

# O SDK do AEM as a Cloud Service {#aem-as-a-cloud-service-sdk}

O AEM as a Cloud Service SDK é composto pelos seguintes artefatos:

* **Quickstart Jar** - O tempo de execução do AEM usado para o desenvolvimento local.
* **Jar da API Java™** - A dependência Java™ Jar/Maven que expõe todas as APIs Java™ permitidas que podem ser usadas para desenvolvimento em relação ao AEM as a Cloud Service. Anteriormente conhecido como Uberjar.
* **Jar do Javadoc** - Os documentos Java do Jar da API Java™.
* **Ferramentas do Dispatcher** - O conjunto de ferramentas usadas para desenvolver localmente em relação ao Dispatcher. Separe os artefatos no UNIX® e no Windows.

Além disso, alguns clientes que foram implantados anteriormente com o AEM 6.5 ou versões anteriores usam os artefatos abaixo. Se a compilação local não estiver funcionando com o QuickStart Jar, e você suspeitar que isso ocorre devido à remoção de interfaces do as a Cloud Service implantado pela AEM, entre em contato com o Suporte ao cliente. Eles podem determinar se você precisa de acesso. Requer alterações no back-end.

* **6.5 Jar da API Java™ obsoleta** - Um conjunto extra de interfaces que foram removidas desde o AEM 6.5.
* **6.5 Jar Javadoc obsoleto** - Os documentos Java do conjunto adicional de interfaces.

>[!NOTE]
> 
> Há diferenças entre o AEM as a Cloud Service e a SDK em várias áreas diferentes. Para situações em que são necessárias alterações rápidas e iterativas, a Adobe introduziu os ambientes de desenvolvimento rápido. Consulte os [Ambientes de desenvolvimento rápido](/help/implementing/developing/introduction/rapid-development-environments.md) para obter mais informações.

## Criação para a SDK {#building-for-the-sdk}

O AEM as a Cloud Service SDK é usado para criar e implantar código personalizado. Consulte a [documentação do Arquétipo de Projetos AEM](https://experienceleague.adobe.com/pt-br/docs/experience-manager-core-components/using/developing/archetype/using). Em um nível superior, as seguintes etapas são executadas:

* **Código de compilação** - o código Source está compilado, gerando os pacotes de conteúdo resultantes.
* **Artefatos de compilação** - Os artefatos são compilados durante este processo.
* **Analisar pacotes** - Os pacotes são analisados usando o plug-in Maven Analyzer, que procura problemas no projeto Maven, como dependências ausentes.
* **Implantar artefatos** - Os artefatos são implantados no servidor local.

O Cloud Manager executa as mesmas etapas ao implantar em ambientes de nuvem. A execução de builds localmente permite o desenvolvimento e o teste locais. Os desenvolvedores podem identificar com eficiência problemas de código ou estruturais antes de confirmar no controle de origem. Esse processo ajuda a evitar atrasos causados pelo acionamento de implantações do Cloud Manager, que podem levar mais tempo.

>[!NOTE]
>
>O AEM as a Cloud Service SDK deve ser construído com uma distribuição e uma versão do Java suportadas pelo [ambiente de compilação do Cloud Manager](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md). Os clientes da AEM as a Cloud Service podem baixar o Oracle JDK no [Portal de distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html). Eles têm suporte estendido para o Java 11 até setembro de 2026 devido ao licenciamento da Adobe e aos termos de suporte para a tecnologia Oracle Java em projetos Adobe Experience Manager.

## Acesso ao AEM as a Cloud Service SDK {#accessing-the-aem-as-a-cloud-service-sdk}

* Você pode verificar o ícone **Sobre o Adobe Experience Manager** do AEM Admin Console para descobrir a versão do AEM que você está executando em produção.
* As Ferramentas do QuickStart Jar e do Dispatcher podem ser baixadas como um arquivo zip do [Portal de distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html). O acesso às listagens do SDK é limitado às pessoas que têm ambientes no AEM Managed Services ou AEM as a Cloud Service.
* O Jar da API Java™ e o Jar do Javadoc podem ser baixados por meio das ferramentas Maven, na linha de comando ou com o IDE de sua preferência.
* Os poms de projeto maven devem fazer referência ao seguinte pacote Jar de API. A dependência de poms de qualquer subpacote também deve ser referenciada.

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
>A entrada da versão do SDK deve corresponder à versão do AEM as a Cloud Service. Você pode ver qual versão está usando ao fazer logon no AEM. No canto superior direito da tela, vá para o ponto de interrogação e clique em **[!UICONTROL Sobre o Adobe Experience Manager]**.


## Atualizar um projeto local com uma nova versão do SDK {#refreshing-a-local-project-with-a-new-skd-version}

Quando é recomendado atualizar o projeto local com uma nova SDK?

A Adobe *recomenda* atualizá-la após uma versão de manutenção mensal.

É *opcional* atualizá-lo após qualquer versão de manutenção diária. Os clientes são informados quando a instância de produção é atualizada com êxito para uma nova versão do AEM. Para as versões de manutenção diárias, não é esperado que o novo SDK tenha mudado significativamente, se é que mudou. Ainda assim, a Adobe recomenda que você atualize ocasionalmente o ambiente de desenvolvedor local do AEM com a SDK mais recente e, em seguida, recrie e teste o aplicativo personalizado. A versão de manutenção mensal geralmente inclui alterações mais impactantes e, portanto, os desenvolvedores devem atualizar, reconstruir e testar imediatamente.

**Para atualizar um projeto local com uma nova versão do SDK:**

1. Certifique-se de que todo o conteúdo útil esteja comprometido com o controle de origem. Ou armazenado em um pacote de conteúdo mutável para importação posterior.
1. O conteúdo do teste de desenvolvimento local deve ser armazenado separadamente para que não seja implantado como parte da build do pipeline do Cloud Manager. O motivo é que ele é usado apenas para desenvolvimento local.
1. Interrompe a inicialização rápida em execução no momento.
1. Mova a pasta `crx-quickstart` para uma pasta diferente para manter a pasta segura.
1. Observe a nova versão do AEM, que é anotada no Cloud Manager (ela é usada para identificar a nova versão do QuickStart Jar para baixar mais).
1. Baixe o QuickStart Jar cuja versão corresponda à versão do AEM de produção no Portal de distribuição de software.
1. Crie uma pasta totalmente nova e coloque o novo QuickStart Jar dentro dela.
1. Inicie o novo QuickStart com os modos de execução desejados (renomeando o arquivo ou transmitindo os modos de execução por meio do `-r`).
Verifique se não há vestígios do início rápido antigo na pasta.
1. Crie seu aplicativo do AEM.
1. Implante o aplicativo AEM no AEM local por meio do Gerenciador de pacotes.
1. Instale todos os pacotes de conteúdo mutável necessários para o teste do ambiente local por meio do Gerenciador de pacotes.
1. Prossiga com o desenvolvimento e implante as alterações conforme necessário.

Se houver conteúdo que deve ser instalado com cada nova versão de início rápido do AEM, inclua-o em um pacote de conteúdo e no controle de origem do projeto. Em seguida, instale-o sempre.

A Adobe recomenda atualizar o SDK com frequência, por exemplo, duas vezes por semana. Além disso, descarte todo o estado local diariamente, de modo que você não dependa acidentalmente de dados com informações de estado no aplicativo.

Se você usar o CryptoSupport para serviços em nuvem, configuração do SMTP Mail ou a API CryptoSupport, as propriedades criptografadas serão protegidas com uma chave. Mais detalhes estão disponíveis na [Documentação da API CryptoSupport](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/granite/crypto/CryptoSupport.html). Essa chave é gerada automaticamente na primeira inicialização de um ambiente do AEM. Embora a configuração da nuvem trate da reutilização automática da CryptoKey específica do ambiente, é necessário injetar a cryptokey no ambiente de desenvolvimento local.

Por padrão, o AEM é configurado para armazenar os dados principais na pasta de dados de uma pasta, mas, para facilitar a reutilização no desenvolvimento, o processo do AEM pode ser inicializado na primeira inicialização com &quot;`-Dcom.adobe.granite.crypto.file.disable=true`.&quot; Este processo gera os dados de criptografia em &quot;`/etc/key`&quot;.

**Para reutilizar pacotes de conteúdo que contenham os valores criptografados:**

* Ao iniciar inicialmente o quickstart.jar local, adicione o parâmetro abaixo: &quot;`-Dcom.adobe.granite.crypto.file.disable=true`.&quot; Como opção, a Adobe recomenda que você sempre o adicione.
* Na primeira vez que você iniciou uma instância, crie um pacote que contenha um filtro para a raiz &quot;`/etc/key`&quot;. Esse pacote contém o segredo a ser reutilizado em todos os ambientes para os quais você deseja que eles sejam reutilizados.
* Exporte qualquer conteúdo mutável que contenha segredos. Ou procure os valores criptografados por meio de `/crx/de` para que você possa adicioná-los ao pacote que é reutilizado nas instalações.
* Sempre que você gerar uma nova instância (para substituir por uma nova versão ou como vários ambientes de desenvolvimento devem compartilhar as credenciais para teste), instale o pacote produzido nas etapas 2 e 3. Isso permite reutilizar o conteúdo sem a necessidade de reconfigurar manualmente. O motivo é porque agora a chave de criptografia está sincronizada.

