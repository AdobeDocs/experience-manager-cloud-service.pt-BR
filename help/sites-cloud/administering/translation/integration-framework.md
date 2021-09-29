---
title: Configuração da estrutura de integração de tradução
description: Saiba como configurar a Estrutura de integração de tradução para integrar com serviços de tradução de terceiros.
feature: Language Copy
role: Admin
exl-id: 6e74cdee-7965-4087-a733-e9d81c4aa7c2
source-git-commit: 917f5790fb36fd1560ba43c67f8072616b605894
workflow-type: tm+mt
source-wordcount: '1419'
ht-degree: 2%

---

# Configuração da estrutura de integração de tradução {#configuring-the-translation-integration-framework}

A Estrutura de integração de tradução integra-se aos serviços de tradução de terceiros para orquestrar a tradução de conteúdo AEM. Envolve três etapas básicas.

1. [Conecte-se ao seu provedor de serviços de tradução.](#connecting-to-a-translation-service-provider)
1. [Crie uma configuração da Estrutura de integração de tradução.](#creating-a-translation-integration-configuration)
1. [Associe as configurações de nuvem com suas páginas.](#configuring-pages-for-translation)

Para obter uma visão geral dos recursos de tradução de conteúdo no AEM, consulte [Tradução de conteúdo para sites multilíngues](overview.md).

>[!TIP]
>
>Se você não estiver familiarizado com a tradução de conteúdo, consulte nossa [Jornada de tradução de sites,](/help/journey-sites/translation/overview.md) que é o caminho orientado pela tradução do conteúdo do AEM Sites usando as ferramentas de tradução avançadas do AEM, ideal para aqueles sem AEM ou experiência de tradução.

## Conexão com um provedor de serviços de tradução {#connecting-to-a-translation-service-provider}

Crie uma configuração de nuvem que se conecta AEM seu provedor de serviços de tradução. AEM inclui a capacidade de [conectar ao Microsoft Translator](connect-ms-translator.md) por padrão.

Os seguintes fornecedores de tradução fornecem uma implementação da API de AEM para projetos de tradução.

* [Microsoft Translator](connect-ms-translator.md)
* [Translations.com](https://exchange.adobe.com/experiencecloud.details.90104.globallink-connect-plus-for-aem.html)  (Adobe Exchange Premier Partner)
* [Clay Tablet Technologies](https://exchange.adobe.com/experiencecloud.details.90064.clay-tablet-translation-for-experience-manager.html)
* [Lionbridge](https://exchange.adobe.com/experiencecloud.details.100064.lionbridge-connector-for-experience-manager-63.html)
* [Memória](https://exchange.adobe.com/experiencecloud.details.103166.memsource-connector-for-adobe-experience-manager.html)
* [Palavras-chave](https://exchange.adobe.com/experiencecloud.details.90019.html)
* [Cloud XTM](https://exchange.adobe.com/experiencecloud.details.105037.xtm-connect-for-adobe-experience-manager.html)
* [Lingotek](https://exchange.adobe.com/experiencecloud.details.90088.lingotek-collaborative-translation-platform.html)
* [Smartling](https://exchange.adobe.com/experiencecloud.details.90101.smartling-connector-for-adobe-experience-manager.html)
* [SDL](https://exchange.adobe.com/experiencecloud.details.100110.sdl-translation-management.html)
* [Systran](https://exchange.adobe.com/experiencecloud.details.90233.systran-for-adobe-experience-manager.html)

Depois de instalar um pacote de conectores, você pode criar uma configuração de nuvem para o conector. Normalmente, você precisa fornecer suas credenciais para autenticação com o serviço de tradução. Para obter informações sobre como adicionar uma configuração de nuvem para o conector do Microsoft Translator, consulte [Integração com o Microsoft Translator](connect-ms-translator.md).

Você pode criar várias configurações de nuvem para o mesmo conector, se necessário. Por exemplo, crie uma configuração para cada conta ou projeto que você tem com o mesmo fornecedor.

Após configurar uma conexão, você pode criar a configuração da estrutura de integração de tradução que a usa.

## Criar uma configuração de integração de tradução {#creating-a-translation-integration-configuration}

Crie uma configuração de estrutura de integração de tradução para especificar como traduzir o conteúdo. A configuração inclui as seguintes informações:

* Qual provedor de serviços de tradução usar
* Se a tradução humana ou de máquina deve ser realizada
* Traduzir outro conteúdo associado a uma página ou ativo, como tags

Após criar uma configuração de estrutura, associe a configuração de nuvem às páginas que deseja traduzir de acordo com a configuração. Quando o processo de tradução é iniciado, o fluxo de trabalho de tradução continua de acordo com a configuração de estrutura associada.

Quando diferentes seções do seu site tiverem diferentes requisitos de tradução, crie várias configurações de estrutura de acordo. Por exemplo, um site multilíngue pode incluir cópias em inglês, espanhol e japonês. O proprietário do site usa dois provedores de serviços de tradução diferentes para traduções em espanhol e japonês. Portanto, duas configurações da estrutura são configuradas. Cada configuração usa um provedor de serviço de tradução diferente.

Após configurar uma estrutura de integração de tradução, você pode [associá-la às páginas](preparation.md) que a utilizam.

>[!TIP]
>
>Para obter uma visão geral dos recursos de tradução de conteúdo no AEM, consulte [Tradução de conteúdo para sites multilíngues](overview.md).

Uma única configuração da estrutura controla como traduzir o conteúdo e os ativos da página.

![Configuração de tradução](../assets/translation-configuration.png)

Para criar uma nova configuração de tradução:

1. No menu de navegação global [clique ou toque em **Ferramentas -> Cloud Services - e Cloud Services de tradução**.](/help/sites-cloud/authoring/getting-started/basic-handling.md#global-navigation)
1. Navegue até o local em que deseja criar a configuração na estrutura do conteúdo. Geralmente, isso é baseado em um site específico ou pode ser global.
1. Forneça as seguintes informações nos campos e clique ou toque em **Create**:
   1. Selecione **Tipo de configuração** no menu suspenso.
   1. Insira um **Title** para sua configuração. O **Título** identifica a configuração no console **Cloud Services**, bem como nas listas suspensas de propriedade da página.
   1. Opcionalmente, digite um **Name** para usar no nó do repositório que armazena a configuração.
1. Na janela **Editar Configuração**, configure as propriedades nas guias **Sites** e **Assets** e clique ou toque em **Salvar e fechar**.

### Propriedades de configuração de sites {#sites-configuration-properties}

A guia **Sites** controla como a tradução do conteúdo da página é executada.

| Propriedade | Descrição |
|---|---|
| Fluxo de trabalho da conversão | Essa propriedade define o método de tradução executado pela estrutura para o conteúdo do site:<br> - Tradução do computador: O provedor de tradução executa a tradução usando a tradução automática em tempo real.<br>- Tradução Humana: O conteúdo é enviado ao provedor de tradução para ser traduzido por tradutores.<br>- Não Traduzir: O conteúdo não é enviado para tradução. Isso é para ignorar determinadas ramificações de conteúdo que não seriam traduzidas, mas poderiam ser atualizadas com o conteúdo mais recente. |
| Provedor de tradução | Essa propriedade define o provedor de tradução para executar a tradução. Um provedor é exibido na lista quando o conector correspondente é instalado. |
| Categoria de conteúdo | (Somente tradução automática) Essa propriedade é uma categoria que descreve o conteúdo que você está traduzindo. A categoria pode afetar a escolha da terminologia e da expressão na tradução do conteúdo. |
| Traduzir tags | Essa opção permite a tradução de tags associadas à página. |
| Traduzir ativos da página | Essa propriedade define como traduzir ativos que são adicionados a componentes do sistema de arquivos ou referenciados de ativos:<br>- Não traduzir: Os ativos da página não são traduzidos.<br>- Uso do fluxo de trabalho de tradução de sites: Os ativos são tratados de acordo com as propriedades de configuração da  **** Sitab.<br>- Uso do fluxo de trabalho de tradução de ativos: Os ativos são manipulados de acordo com as propriedades configuradas na  **** guia Ativos. |
| Executar tradução automaticamente | Ative essa propriedade para executar trabalhos de tradução automaticamente após a criação de projetos de tradução. Você não tem uma oportunidade de revisar e escoar o trabalho de tradução ao selecionar essa opção. |

### Propriedades de configuração de ativos {#assets-configuration-properties}

As propriedades de ativos controlam como configurar ativos. Para obter mais informações sobre a tradução de ativos, consulte [Criação de cópias de idioma para ativos](/help/assets/translate-assets.md).

| Propriedade | Descrição |
|---|---|
| Fluxo de trabalho da conversão | Esta propriedade seleciona o tipo de tradução que a estrutura executa para ativos:<br> - Tradução da Máquina: O provedor de tradução executa a tradução imediatamente usando a tradução automática.<br>- Tradução Humana: O conteúdo é enviado automaticamente para o provedor de tradução para ser traduzido manualmente.<br>-Não Traduzir: Os ativos não são enviados para tradução. |
| Provedor de tradução | Essa propriedade define o provedor de tradução para executar a tradução. Um provedor é exibido na lista quando o conector correspondente é instalado. |
| Categoria de conteúdo | (Somente tradução automática) Essa propriedade descreve o conteúdo que você está traduzindo. A categoria pode afetar a escolha da terminologia e da expressão na tradução do conteúdo. |
| Converter ativos | Ative essa propriedade para incluir ativos no projeto de tradução. |
| Traduzir metadados | Ative essa propriedade para traduzir metadados de ativos. |
| Traduzir tags | Ative essa propriedade para traduzir tags associadas ao ativo. |
| Executar tradução automaticamente | Selecione essa propriedade para executar trabalhos de tradução automaticamente após a criação de projetos de tradução. Você não tem uma oportunidade de revisar ou escoar o trabalho de tradução ao selecionar essa opção. |

## Configuração de páginas para tradução {#configuring-pages-for-translation}

Para configurar a tradução das páginas de origem em outros idiomas, associe as páginas às seguintes configurações de nuvem:

* A configuração da nuvem que se conecta AEM seu provedor de tradução.
* A estrutura de integração de tradução que configura os detalhes da tradução.

Observe que a configuração da nuvem da estrutura de integração de tradução identifica a configuração da nuvem a ser usada para conexão com o provedor de serviços. Quando você associa uma página de origem a uma configuração da nuvem de estrutura, a página deve ser associada à configuração da nuvem do provedor de serviços que a configuração da nuvem de estrutura usa.

Quando você associa uma página com uma configuração de nuvem, os descendentes da página herdam a associação. Por exemplo, se você associar a página `/content/wknd/language-masters/en/magazine` a uma Estrutura de integração de tradução, a página `magazine` e as páginas filhas abaixo dela serão traduzidas de acordo com a estrutura.

Quando necessário, é possível substituir a associação em uma página descendente. Por exemplo, o conteúdo de um site é principalmente sobre viagens e estilo de vida. No entanto, um ramo de páginas descreve a empresa. Nesse caso, a página raiz do site pode estar associada a uma Estrutura de integração de tradução que especifica a tradução automática usando a categoria Estilo de vida , enquanto a ramificação que descreve a empresa usaria uma estrutura que executa a tradução automática usando a categoria Geral .

### Associar uma página a um provedor de tradução {#associating-a-page-with-a-translation-provider}

Associe uma página ao provedor de tradução que você está usando para traduzir a página e as páginas descendentes.

1. No console de sites, selecione a página que será configurada e clique ou toque em **Propriedades da exibição**.
1. Clique ou toque na guia **Cloud Services**.
1. Na lista suspensa **Adicionar configuração**, selecione a configuração.
1. Clique ou toque em **Salvar e fechar**.

### Associar páginas a uma estrutura de integração de tradução {#associating-pages-with-a-translation-integration-framework}

Associe uma página à Estrutura de integração de tradução que define como você deseja executar a tradução da página e das páginas descendentes.

1. No console de sites, selecione a página que será configurada e clique ou toque em **Propriedades da exibição**.
1. Clique ou toque na guia **Cloud Services**.
1. Na lista suspensa **Adicionar configuração**, selecione a configuração.
1. Clique ou toque em **Salvar e fechar**.
