---
title: Configurar o conector de tradução
description: Saiba como conectar AEM a um serviço de tradução.
source-git-commit: bc56a739d8aa59d8474f47c9882662baacfdda84
workflow-type: tm+mt
source-wordcount: '1164'
ht-degree: 0%

---

# Configurar o conector de tradução {#configure-connector}

Saiba como conectar AEM a um serviço de tradução.

## A História Até Agora {#story-so-far}

No documento anterior da jornada de tradução AEM sem cabeçalho, [Comece com AEM tradução sem cabeçalho](learn-about.md) você aprendeu a organizar o conteúdo sem cabeçalho e como AEM as ferramentas de tradução funcionam e agora deve:

* Entenda a importância da estrutura de conteúdo para a tradução.
* Entenda como o AEM armazena conteúdo sem interface.
* Familiarize-se com AEM ferramentas de tradução.

Este artigo se baseia nesses fundamentos para que você possa realizar a primeira etapa de configuração e configurar um serviço de tradução, que será usado posteriormente na jornada para traduzir o conteúdo.

## Objetivo {#objective}

Este documento ajuda você a entender como configurar um conector de AEM para o serviço de tradução escolhido. Depois de ler, você deve:

* Entenda os parâmetros importantes da Estrutura de integração de tradução no AEM.
* Pode configurar sua própria conexão com o serviço de tradução.

## O Quadro de Integração de Tradução {#tif}

AEM TIF (Translation Integration Framework) integra-se a serviços de tradução de terceiros para orquestrar a tradução de conteúdo AEM. Envolve três etapas básicas.

1. Conecte-se ao seu provedor de serviços de tradução.
1. Crie uma configuração da Estrutura de integração de tradução.
1. Associe a configuração ao seu conteúdo.

As seções a seguir descrevem essas etapas com mais detalhes.

## Conexão com um provedor de serviços de tradução {#connect-translation-provider}

A primeira etapa é escolher qual serviço de tradução deseja usar. Há muitas opções para os serviços de tradução humana e de máquina disponíveis para AEM. A maioria dos provedores oferece um pacote de tradutor a ser instalado. Consulte a seção [Recursos adicionais](#additional-resources) para obter uma seleção de opções disponíveis.

>[!NOTE]
>
>O especialista em tradução geralmente é responsável por escolher qual serviço de tradução usar, mas o administrador normalmente é responsável por instalar o pacote de conector de tradução necessário.

Para os fins desta jornada, usamos o Microsoft Translator, que AEM fornece uma licença de avaliação pronta para uso. Consulte a seção [Additional Resources](#additional-resources) para obter mais informações sobre esse provedor.

Se você escolher outro provedor, o administrador deverá instalar o pacote de conectores de acordo com as instruções fornecidas pelo serviço de tradução.

>[!NOTE]
>
>Usar o Microsoft Translator pronto para uso no AEM não requer configuração adicional e funciona como está sem configuração de conector adicional.
>
>Se optar por usar o conector do Microsoft Translator para fins de teste, não será necessário executar as etapas nas próximas duas seções: [Criando uma Configuração de Integração de Tradução](#create-config) e [Associe a Configuração ao Seu Conteúdo.](#associate) No entanto, é recomendável lê-las para que você esteja familiarizado com as etapas para quando precisar configurar o conector preferencial.
>
>A licença de avaliação do conector do Microsoft Translator não se destina a fins de produção e, se você decidir licenciá-la, o administrador do sistema deverá seguir as etapas detalhadas na seção [Additional Resources](#additional-resources) no final deste documento para configurar essa licença.

## Criar uma configuração de integração de tradução {#create-config}

Depois que o pacote de conectores do seu serviço de tradução preferido for instalado, você deverá criar uma configuração de Estrutura de Integração de Tradução para esse serviço. A configuração inclui as seguintes informações:

* Qual provedor de serviços de tradução usar
* Se a tradução humana ou de máquina deve ser realizada
* Traduzir ou não outro conteúdo associado ao Fragmento do conteúdo, como tags

Para criar uma nova configuração de tradução:

1. No menu de navegação global, clique ou toque em **Ferramentas** -> **Cloud Services** -> **Cloud Services de tradução**.
1. Navegue até o local em que deseja criar a configuração na estrutura do conteúdo. Geralmente, isso se baseia em um projeto específico ou pode ser global.
   * Por exemplo, nesse caso, uma configuração pode ser feita globalmente para aplicar a todo o conteúdo ou apenas para o projeto WKND.

   ![Local de configuração de tradução](assets/translation-configuration-location.png)

1. Forneça as seguintes informações nos campos e clique ou toque em **Create**.
   1. Selecione **Tipo de configuração** no menu suspenso. Selecione **Integração de Tradução** na lista.
   1. Insira um **Title** para sua configuração. O **Título** identifica a configuração no console **Cloud Services**, bem como nas listas suspensas de propriedade da página.
   1. Opcionalmente, digite um **Name** para usar no nó do repositório que armazena a configuração.

   ![Criar configuração de tradução](assets/create-translation-configuration.png)

1. Toque ou clique em **Create** e a janela **Edit Configuration** é exibida, onde você pode configurar as propriedades de configuração.

1. Lembre-se de que os Fragmentos de conteúdo são armazenados como ativos no AEM. Toque ou clique na guia **Assets**.

![Propriedades de configuração de tradução](assets/translation-configuration.png)

1. Forneça as seguintes informações.

   1. **Método de tradução**  - Selecione  **Tradução de máquina ou** Tradução  **** humana, dependendo do seu provedor de tradução. Para os propósitos dessa jornada, supomos tradução automática.
   1. **Provedores de tradução**  - Selecione o conector instalado para o serviço de tradução na lista.
   1. **Categoria de conteúdo**  - Selecione a categoria mais apropriada para direcionar melhor a tradução (somente para tradução automática).
   1. **Traduzir ativos do fragmento de conteúdo**  - Verifique isso para traduzir ativos associados aos fragmentos de conteúdo.
   1. **Traduzir ativos**  - Marque essa opção para traduzir os ativos.
   1. **Traduzir metadados**  - Verifique isso para traduzir metadados de ativos.
   1. **Traduzir tags**  - Verifique isso para traduzir tags associadas ao ativo.
   1. **Tradução de execução automática**  - verifique essa propriedade se deseja que as traduções sejam enviadas automaticamente para o serviço de tradução.

1. Toque ou clique em **Salvar e fechar**.

Agora você configurou o conector para o serviço de tradução.

## Associar a configuração ao seu conteúdo {#associate}

AEM é uma ferramenta flexível e eficiente e oferece suporte a vários serviços de tradução simultâneos por meio de vários conectores e várias configurações. A configuração dessa configuração está além do escopo dessa jornada. No entanto, essa flexibilidade significa que você deve especificar quais conectores e configurações devem ser usados para traduzir o conteúdo, associando essa configuração ao seu conteúdo.

Para fazer isso, navegue até a raiz do idioma do conteúdo. Para nosso exemplo, isso é

```text
/content/dam/<your-project>/en
```

1. Vá para a navegação global e vá para **Navegação** -> **Ativos** -> **Arquivos**.
1. No console Assets, selecione a raiz de idioma para configurar e clique ou toque em **Properties**.
1. Toque ou clique na guia **Cloud Services**.
1. Em **Cloud Service Configurations**, na lista suspensa **Add Configuration**, selecione o conector. Ele deve aparecer na lista suspensa quando você tiver instalado seu pacote como [descrito anteriormente.](#connect-translation-provider)
1. Em **Cloud Service Configurations** na lista suspensa **Add Configuration**, selecione também a configuração.
1. Toque ou clique em **Salvar e fechar**.

![Selecionar configurações do serviço em nuvem](assets/select-cloud-service-configurations.png)

## O que vem a seguir {#what-is-next}

Agora que você concluiu esta parte da jornada de tradução sem cabeçalho, é necessário:

* Entenda os parâmetros importantes da Estrutura de integração de tradução no AEM.
* Pode configurar sua própria conexão com o serviço de tradução.

Aproveite esse conhecimento e prossiga com sua jornada de tradução sem periféricos AEM revisando o documento [Configure as regras de tradução,](translation-rules.md) onde você aprenderá a definir qual conteúdo traduzir.

## Recursos adicionais {#additional-resources}

Embora seja recomendável seguir para a próxima parte da jornada de tradução sem periféricos revisando o documento [Configurar regras de tradução](translation-rules.md), os seguintes são alguns recursos adicionais e opcionais que fazem um mergulho mais profundo em alguns conceitos mencionados neste documento, mas eles não são solicitados a continuar com a jornada sem periféricos.

* [Configuração da estrutura de integração de tradução](/help/sites-cloud/administering/translation/integration-framework.md)  - Revise uma lista de conectores de tradução selecionados e saiba como configurar a estrutura de integração de tradução para se integrar a serviços de tradução de terceiros.
* [Conexão com o Microsoft Translator](/help/sites-cloud/administering/translation/connect-ms-translator.md)  - O AEM fornece uma conta de avaliação do Microsoft Translation para fins de teste.
