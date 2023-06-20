---
title: Configurar o conector de tradução (AEM Sites)
description: Saiba como conectar o AEM a um serviço de tradução.
index: true
hide: false
hidefromtoc: false
exl-id: d1a3eb42-e9e4-4118-9ff7-7aab5519cf0d
source-git-commit: bceec9ea6858b1c4c042ecd96f13ae5cac1bbee5
workflow-type: tm+mt
source-wordcount: '1166'
ht-degree: 96%

---

# Configurar o conector de tradução {#configure-connector}

Saiba como conectar o AEM a um serviço de tradução.

## A história até agora {#story-so-far}

No documento anterior da jornada de tradução do AEM Sites, [Introdução à tradução no AEM Sites](learn-about.md), você aprendeu a organizar seu conteúdo e descobriu como funcionam as ferramentas de tradução do AEM. Agora, você deverá:

* Compreender a importância da estrutura de conteúdo para a tradução.
* Compreender como o AEM armazena conteúdo.
* Se familiarizar com as ferramentas de tradução do AEM.

Este artigo se baseia nesses fundamentos para que você possa realizar a primeira etapa e configurar um serviço de tradução, que será usado posteriormente na jornada para traduzir o conteúdo.

## Objetivo {#objective}

Este documento ajuda você a entender como configurar um conector do AEM para o serviço de tradução escolhido. Depois de ler esse documento, você deverá:

* Compreender os parâmetros fundamentais da estrutura de integração de tradução no AEM.
* Ser capaz de configurar sua própria conexão com o serviço de tradução.

## A estrutura de integração de tradução {#tif}

A estrutura de integração de tradução (TIF) do AEM integra-se a serviços de tradução de terceiros para orquestrar a tradução de conteúdo do AEM. Isso envolve três etapas básicas.

1. Conectar ao provedor de serviços de tradução.
1. Criar uma configuração da estrutura de integração de tradução.
1. Associar a configuração ao seu conteúdo.

As seções a seguir descrevem essas etapas com mais detalhes.

## Conexão com um provedor de serviços de tradução {#connect-translation-provider}

A primeira etapa é escolher qual serviço de tradução usar. Há muitas opções de serviços de tradução humana e tradução automática disponíveis para o AEM. A maioria dos provedores oferece um pacote de tradutor para instalação. Consulte a seção [Recursos adicionais](#additional-resources) para obter uma seleção de opções disponíveis.

>[!NOTE]
>
>O especialista em tradução geralmente é responsável por escolher qual serviço de tradução usar, mas o administrador normalmente é responsável por instalar o pacote do conector de tradução necessário.

Para os propósitos desta jornada, usamos o Microsoft Translator, fornecido pelo AEM juntamente com uma licença de avaliação pronta para uso. Consulte a seção [Recursos adicionais](#additional-resources) para obter mais informações sobre esse provedor.

Se você escolher outro provedor, o administrador deverá instalar o pacote do conector de acordo com as instruções fornecidas pelo serviço de tradução.

>[!NOTE]
>
>O Microsoft Translator pronto para uso funciona bem no AEM sem necessidade de configurações adicionais. As configurações do conector também não precisam ser alteradas.
>
>Se você optar por usar o conector do Microsoft Translator para fins de teste, não será necessário executar as etapas das próximas duas seções: [Criar uma configuração de integração de tradução](#create-config) e [Associar a configuração ao seu conteúdo.](#associate) No entanto, é recomendável lê-las para que você esteja familiarizado com as etapas para quando precisar configurar seu conector de preferência.
>
>A licença de avaliação do conector do Microsoft Translator não se destina a fins de produção e, caso decida adquirir uma licença, o administrador do sistema deverá seguir as etapas detalhadas na [Recursos adicionais](#additional-resources) no final deste documento para configurar essa licença.

## Criar uma configuração de integração de tradução {#create-config}

Depois que o pacote do conector do seu serviço de tradução de preferência for instalado, você deverá criar uma configuração da estrutura de integração de tradução para esse serviço. A configuração inclui as seguintes informações:

* Qual provedor de serviços de tradução usar
* Se deve ser realizada tradução humana ou automática
* Se outros conteúdos associados às páginas, como tags, devem ou não ser traduzidos

Para criar uma nova configuração de tradução:

1. No menu de navegação global, clique ou toque em **Ferramentas** -> **Cloud Services** -> **Serviços de tradução em nuvem**.
1. Navegue até o local em que deseja criar a configuração na estrutura do conteúdo. Geralmente, ela é baseada em um projeto específico, mas também pode ser global.
   * Por exemplo, nesse caso, pode-se criar uma configuração global que se aplique a todo o conteúdo ou uma configuração específica para o projeto WKND.

   ![Local da configuração de tradução](assets/translation-configuration-location.png)

1. Clique ou toque em **Criar** na barra de ferramentas para criar a nova configuração.
1. Forneça as seguintes informações nos campos e, em seguida, clique ou toque em **Criar**.
   1. Selecione o **Tipo de configuração** no menu suspenso. Selecione **Integração de tradução** na lista.
   1. Insira um **Título** para sua configuração. O **Título** identifica a configuração no console do **Cloud Services**, bem como nas listas suspensas de propriedade da página.
   1. Opcionalmente, insira um **Nome** para o nó do repositório que armazena a configuração.

   ![Criar configuração de tradução](assets/create-translation-configuration.png)

1. Toque ou clique em **Criar** e a janela **Editar configuração** será exibida, onde você poderá definir as propriedades de configuração.

1. Visto que seu conteúdo é gerenciado como um site, toque ou clique na guia **Sites**.

![Propriedades de configuração de tradução](assets/translation-configuration.png)

1. Forneça as seguintes informações.

   1. **Método de tradução** - selecione **Tradução automática** ou **Tradução humana**, dependendo do seu provedor de tradução. Para os fins desta jornada, vamos pressupor o uso de tradução automática.
   1. **Provedores de tradução** - selecione na lista o conector instalado para o serviço de tradução.
   1. **Categoria de conteúdo** - selecione a categoria mais apropriada para direcionar melhor a tradução (somente para tradução automática).
   1. **Traduzir ativos da página** - selecione **Uso do fluxo de trabalho de tradução de sites** para traduzir os ativos associados às páginas dos sites.
   1. **Traduzir cadeias de caracteres do componente** - marque essa opção para traduzir informações do componente.
   1. **Traduzir tags** - marque essa opção para traduzir tags associadas à página.
   1. **Executar tradução automaticamente** - marque essa propriedade se desejar que as traduções sejam enviadas automaticamente para o serviço de tradução.

1. Toque ou clique em **Salvar e fechar**.

Você concluiu a configuração do conector para o serviço de tradução.

## Associar a configuração ao seu conteúdo {#associate}

O AEM é uma ferramenta flexível e eficiente que tem compatibilidade com diversos serviços de tradução simultâneos, por meio de vários conectores e configurações. A definição dessa configuração está fora do escopo desta jornada. No entanto, essa flexibilidade significa que você deve especificar quais conectores e configurações devem ser usados para traduzir o conteúdo, associando essa configuração ao seu conteúdo.

Para fazer isso, navegue até a raiz do idioma do conteúdo. Para os fins do nosso exemplo, isto é

```text
/content/<your-project>/en
```

1. Vá até a navegação global e acesse **Navegação** -> **Ativos** -> **Arquivos**.
1. No console de ativos, selecione a raiz do idioma a ser configurada e clique ou toque em **Propriedades**.
1. Toque ou clique na guia **Cloud Services**.
1. Em **Configurações do Cloud Service**, na lista suspensa **Adicionar configuração**, selecione o conector. Ele deve aparecer na lista suspensa quando você tiver instalado o pacote, conforme [descrito anteriormente.](#connect-translation-provider)
1. Em **Configurações do Cloud Service**, na lista suspensa **Adicionar configuração**, selecione também a configuração.
1. Toque ou clique em **Salvar e fechar**.

![Selecionar configurações do Cloud Service](assets/select-cloud-service-configurations.png)

## O que vem a seguir {#what-is-next}

Agora que concluiu esta parte da jornada de tradução do AEM Sites, você deve:

* Compreender os parâmetros fundamentais da estrutura de integração de tradução no AEM.
* Ser capaz de configurar sua própria conexão com o serviço de tradução.

Aplicar esse conhecimento e prosseguir com sua jornada de tradução no AEM Sites, revisando a seguir o documento [Configurar regras de tradução,](translation-rules.md) onde você aprenderá a definir qual conteúdo traduzir.

## Recursos adicionais {#additional-resources}

Embora seja recomendável seguir para a próxima parte da jornada de tradução revisando o documento [Configurar regras de tradução](translation-rules.md), os recursos opcionais a seguir fornecerão uma melhor explicação dos conceitos mencionados neste documento. Porém, eles não são obrigatórios para continuar na jornada.

*  [Configuração da estrutura de integração de tradução](/help/sites-cloud/administering/translation/integration-framework.md) - revise uma lista de conectores de tradução selecionados e saiba como configurar a estrutura de integração de tradução para integrar-se a serviços de tradução de terceiros.
* [Conexão com o Microsoft Translator](/help/sites-cloud/administering/translation/connect-ms-translator.md) - o AEM fornece uma conta de avaliação do Microsoft Translation para fins de teste.
