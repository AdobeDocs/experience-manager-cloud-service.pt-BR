---
title: Configuração da estrutura de integração de tradução
description: Saiba como configurar a estrutura de integração de tradução para integrar aos serviços de tradução de terceiros.
feature: Language Copy
role: Admin
exl-id: 6e74cdee-7965-4087-a733-e9d81c4aa7c2
source-git-commit: 6be7cc7678162c355c39bc3000716fdaf421884d
workflow-type: tm+mt
source-wordcount: '1522'
ht-degree: 97%

---

# Configuração da estrutura de integração de tradução {#configuring-the-translation-integration-framework}

A estrutura de integração de tradução integra-se aos serviços de tradução de terceiros para orquestrar a tradução de conteúdo do AEM. Isso envolve três etapas básicas.

1. [Conectar-se ao provedor de serviços de tradução.](#connecting-to-a-translation-service-provider)
1. [Criar uma configuração da estrutura de integração de tradução.](#creating-a-translation-integration-configuration)
1. [Associar as configurações de nuvem as suas páginas.](#configuring-pages-for-translation)

Para obter uma visão geral dos recursos de tradução de conteúdo no AEM, consulte [Tradução de conteúdo para sites multilíngues](overview.md).

>[!TIP]
>
>Se você é novo na tradução de conteúdo, consulte nossa [Jornada de tradução de sites](/help/journey-sites/translation/overview.md), que oferece um guia para a tradução de conteúdo do AEM Sites usando as ferramentas de tradução avançadas do AEM, ideais para aqueles sem experiência com o AEM ou com a tradução.

## Conexão com um provedor de serviços de tradução {#connecting-to-a-translation-service-provider}

Crie uma configuração de nuvem que conecta o AEM ao seu provedor de serviços de tradução. O AEM inclui a capacidade de [conectar-se ao Microsoft Translator](connect-ms-translator.md) por padrão.

Os seguintes provedores de tradução fornecem uma implementação da API do AEM para projetos de tradução.

* [Microsoft Translator](connect-ms-translator.md)
* [Translations.com](https://exchange.adobe.com/experiencecloud.details.90104.globallink-connect-plus-for-aem.html) (parceiro importante do Adobe Exchange)
* [Clay Tablet Technologies](https://exchange.adobe.com/experiencecloud.details.90064.clay-tablet-translation-for-experience-manager.html)
* [Lionbridge](https://exchange.adobe.com/experiencecloud.details.100064.lionbridge-connector-for-experience-manager-63.html)
* [Memsource](https://exchange.adobe.com/experiencecloud.details.103166.memsource-connector-for-adobe-experience-manager.html)
* [Cloudwords](https://exchange.adobe.com/experiencecloud.details.90019.html)
* [XTM Cloud](https://exchange.adobe.com/experiencecloud.details.105037.xtm-connect-for-adobe-experience-manager.html)
* [Lingotek](https://exchange.adobe.com/experiencecloud.details.90088.lingotek-collaborative-translation-platform.html)
* [RWS](https://partners.adobe.com/exchangeprogram/experiencecloud/exchange.details.108277.html)
* [Smartling](https://exchange.adobe.com/experiencecloud.details.90101.smartling-connector-for-adobe-experience-manager.html)
* [Systran](https://exchange.adobe.com/experiencecloud.details.90233.systran-for-adobe-experience-manager.html)

Depois de instalar um pacote de conector, você pode criar uma configuração de nuvem para o conector. Normalmente, é preciso fornecer suas credenciais para realizar a autenticação com o serviço de tradução. Para obter informações sobre como adicionar uma configuração de nuvem para o conector do Microsoft Translator, consulte [Integração ao Microsoft Translator](connect-ms-translator.md).

Você pode criar várias configurações de nuvem para o mesmo conector, se necessário. Por exemplo, criar uma configuração para cada conta ou projeto que você tem com o mesmo provedor.

Após configurar uma conexão, você pode criar a configuração da estrutura de integração de tradução que a utilizará.

## Criar uma configuração de integração de tradução {#creating-a-translation-integration-configuration}

Crie uma configuração de estrutura de integração de tradução para especificar como traduzir o conteúdo. A configuração inclui as seguintes informações:

* Qual provedor de serviços de tradução usar
* Se deverá ser utilizada tradução humana ou automática
* Se outros conteúdos associados a uma página ou ativo, como tags, deverão ser traduzidos

Após criar uma configuração da estrutura, associe a configuração de nuvem às páginas que deseja traduzir de acordo com a configuração. Quando o processo de tradução é iniciado, o fluxo de trabalho de tradução continua de acordo com a configuração de estrutura associada.

Quando diferentes seções do seu site tiverem diferentes requisitos de tradução, crie várias configurações de estrutura de acordo com suas necessidades. Por exemplo, um site multilíngue pode incluir cópias em inglês, espanhol e japonês. O proprietário do site usa dois provedores de serviços de tradução diferentes para traduções em espanhol e japonês. Portanto, duas configurações da estrutura são configuradas. Cada configuração usa um provedor de serviço de tradução diferente.

Após configurar uma estrutura de integração de tradução, é possível [associá-la às páginas](preparation.md) que a usam.

>[!TIP]
>
>Para obter uma visão geral dos recursos de tradução de conteúdo no AEM, consulte [Tradução de conteúdo para sites multilíngues](overview.md).

Uma única configuração da estrutura controla como o conteúdo e os ativos da página são traduzidos. Para criar uma nova configuração de tradução:

1. No [menu de navegação global](/help/sites-cloud/authoring/getting-started/basic-handling.md#global-navigation), clique ou toque em **Ferramentas -> Serviços em nuvem -&amp; Serviços de tradução em nuvem**.
1. Navegue até o local em que deseja criar a configuração na estrutura do conteúdo. Isso normalmente é baseado em um site específico ou pode ser global.
1. Forneça as seguintes informações nos campos e, em seguida, clique ou toque em **Criar**.:
   1. Selecione **Tipo de configuração** no menu suspenso.
   1. Insira um **Título** para a sua configuração. O **Título** identifica a configuração no console dos **Serviços em nuvem**, bem como nas listas suspensas de propriedade da página.
   1. Opcionalmente, digite um **Nome** para usar no nó do repositório que armazena a configuração.
1. Na janela **Editar configuração**, configure as propriedades nas guias **Sites** e **Ativos** e, em seguida, clique ou toque em **Salvar e fechar**.

### Propriedades de configuração de sites {#sites-configuration-properties}

A guia **Sites** controla como a tradução do conteúdo da página é realizada.

![Configuração de tradução para sites](../assets/translation-configuration.png)

| Propriedade | Descrição |
|---|---|
| Método de tradução | Essa propriedade define o método de tradução utilizado pela estrutura para o conteúdo do site:<br>- Tradução automática: o provedor de tradução realiza a tradução usando a tradução automática em tempo real.<br>- Tradução humana: o conteúdo é enviado ao provedor de tradução para ser traduzido por tradutores.<br>- Não traduzir: o conteúdo não é enviado para tradução. Isso serve para ignorar determinadas ramificações de conteúdo que não seriam traduzidas, mas que poderiam ser atualizadas com o conteúdo mais recente. |
| Provedor de tradução | Essa propriedade define o provedor de tradução que realizará a tradução. Um provedor é exibido na lista quando seu conector correspondente é instalado. |
| Categoria de conteúdo | (Somente tradução automática) Essa propriedade é uma categoria que descreve o conteúdo que você está traduzindo. A categoria pode afetar a escolha de terminologia e estilo na tradução do conteúdo. |
| Traduzir tags | Essa opção permite a tradução de tags associadas à página. |
| Traduzir ativos da página | Essa propriedade define como traduzir ativos que são adicionados a componentes do sistema de arquivos ou referenciados de ativos:<br>- Não traduzir: os ativos da página não são traduzidos.<br>- Uso do fluxo de trabalho de tradução de sites: os ativos são manipulados de acordo com as propriedades de configuração na guia **Sites**.<br>- Uso do fluxo de trabalho de tradução de ativos: os ativos são manipulados de acordo com as propriedades configuradas na guia **Ativos**. |
| Executar a tradução automaticamente | Ative essa propriedade para executar trabalhos de tradução automaticamente após a criação de projetos de tradução. Você não tem a oportunidade de revisar e definir o escopo do trabalho de tradução ao selecionar essa opção. |
| Desativar tradução somente de atualização | Quando essa opção estiver marcada, a atualização do projeto de tradução enviará todos os campos traduzíveis para tradução, não apenas os campos alterados desde a última tradução. |

### Propriedades de configuração de ativos {#assets-configuration-properties}

As propriedades de ativos controlam como configurar ativos. Para obter mais informações sobre a tradução de ativos, consulte [Criação de cópias de idioma para ativos](/help/assets/translate-assets.md).

![Configuração de tradução para sites](../assets/translation-configuration-assets.png)

| Propriedade | Descrição |
|---|---|
| Método de tradução | Essa propriedade seleciona o tipo de tradução que a estrutura realiza para os ativos:<br>- Tradução automática: o provedor de tradução realiza a tradução imediatamente usando a tradução automática.<br>- Tradução humana: o conteúdo é enviado automaticamente para o provedor de tradução para ser traduzido manualmente.<br>-Não traduzir: os ativos não são enviados para tradução. |
| Provedor de tradução | Essa propriedade define o provedor de tradução que realizará a tradução. Um provedor é exibido na lista quando seu conector correspondente é instalado. |
| Categoria de conteúdo | (Somente tradução automática) Essa propriedade descreve o conteúdo que você está traduzindo. A categoria pode afetar a escolha de terminologia e estilo na tradução do conteúdo. |
| Traduzir ativos | Ative essa propriedade para incluir ativos no projeto de tradução. |
| Traduzir metadados | Ative essa propriedade para traduzir metadados de ativos. |
| Traduzir tags | Ative essa propriedade para traduzir tags associadas ao ativo. |
| Executar a tradução automaticamente | Selecione essa propriedade para executar trabalhos de tradução automaticamente após a criação de projetos de tradução. Você não terá a oportunidade de revisar ou definir o escopo do trabalho de tradução ao selecionar essa opção. |
| Desativar tradução somente de atualização | Quando essa opção estiver marcada, a atualização do projeto de tradução enviará todos os campos traduzíveis para tradução, não apenas os campos alterados desde a última tradução. |
| Ativar campos do modelo de conteúdo para tradução | Ativar essa opção usará o **Traduzível** no campo [Modelos de fragmentos do conteúdo](/help/sites-cloud/administering/content-fragments/content-fragments-models.md#properties) para determinar se o campo é traduzido e cria automaticamente [regras de tradução](rules.md) em conformidade. Essa opção substitui todas as regras de tradução criadas por você. |

## Configuração de páginas para tradução {#configuring-pages-for-translation}

Para configurar a tradução das páginas de origem para outros idiomas, associe as páginas às seguintes configurações de nuvem:

* A configuração da nuvem que conecta o AEM ao seu provedor de tradução.
* A estrutura de integração de tradução que configura os detalhes da tradução.

Observe que a configuração da nuvem da estrutura de integração de tradução identifica a configuração da nuvem a ser usada para a conexão com o provedor de serviços. Quando você associa uma página de origem a uma configuração da nuvem de estrutura, a página deve ser associada à configuração da nuvem do provedor de serviços que a configuração da nuvem de estrutura usa.

Quando você associa uma página com uma configuração de nuvem, os descendentes da página herdam a associação. Por exemplo, se você associar a página `/content/wknd/language-masters/en/magazine` a uma estrutura de integração de tradução, a página `magazine` e as páginas filho abaixo dela serão traduzidas de acordo com a estrutura.

Quando necessário, é possível substituir a associação em uma página descendente. Por exemplo, o conteúdo de um site é, em sua maior parte, sobre viagens e estilo de vida. No entanto, uma ramificação de páginas descreve a empresa. Nesse caso, a página raiz do site pode ser associada a uma estrutura de integração de tradução que especifica o uso da tradução automática utilizando a categoria Estilo de vida, enquanto a ramificação que descreve a empresa usaria uma estrutura que realiza a tradução automática utilizando a categoria Geral.

### Associar uma página a um provedor de tradução {#associating-a-page-with-a-translation-provider}

Associe uma página ao provedor de tradução que você está usando para traduzir a página e as páginas descendentes.

1. No console dos sites, selecione a página que deseja configurar e clique ou toque em **Propriedades de exibição**.
1. Clique ou toque na guia **Serviços em nuvem**.
1. Na lista suspensa **Adicionar configuração**, selecione a configuração.
1. Clique ou toque em **Salvar e fechar**.

### Associar páginas a uma estrutura de integração de tradução {#associating-pages-with-a-translation-integration-framework}

Associe uma página à estrutura de integração de tradução, a qual define como você deseja realizar a tradução da página e das páginas descendentes.

1. No console dos sites, selecione a página que deseja configurar e clique ou toque em **Propriedades de exibição**.
1. Clique ou toque na guia **Serviços em nuvem**.
1. Na lista suspensa **Adicionar configuração**, selecione a configuração.
1. Clique ou toque em **Salvar e fechar**.
