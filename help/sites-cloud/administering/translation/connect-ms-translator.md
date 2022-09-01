---
title: Conectar ao Microsoft Translator
description: Saiba como conectar o AEM ao Microsoft Translator pronto para uso para automatizar seu fluxo de trabalho de tradução.
feature: Language Copy
role: Admin
exl-id: ca3c50f9-005e-4871-8606-0cfd3ed21936
source-git-commit: 421ad8506435e8538be9c83df0b78ad8f222df0c
workflow-type: tm+mt
source-wordcount: '517'
ht-degree: 99%

---

# Conectar ao Microsoft Translator {#connecting-to-microsoft-translator}

Crie uma configuração para o serviço em nuvem [Microsoft Translator](https://www.microsoft.com/en-us/translator/business/) para usar sua conta do Microsoft Translation para traduzir conteúdos ou ativos de página no AEM.

>[!TIP]
>
>Se você é novo na tradução de conteúdo, consulte nossa [Jornada de tradução de sites,](/help/journey-sites/translation/overview.md) que fornece um caminho guiado para a tradução de conteúdo do AEM Sites usando as ferramentas de tradução avançadas do AEM, ideal para aqueles que não têm experiência com o AEM ou com tradução.

>[!NOTE]
>
>O AEM fornece uma conta de avaliação do Microsoft Translation, que permite no máximo 2 milhões de caracteres traduzidos gratuitamente por mês. Para obter uma assinatura de conta adequada para sistemas de produção, consulte [Atualização da configuração da licença de avaliação do Microsoft Translator](#upgrading-the-microsoft-translator-trial-license-configuration).

| Propriedade | Descrição |
|---|---|
| Rótulo da tradução | O nome de exibição do serviço de tradução |
| Atribuição da tradução | (Opcional) Para conteúdo gerado pelo usuário, a atribuição que aparece ao lado do texto traduzido, por exemplo `Translations by Microsoft` |
| ID do espaço de trabalho | (Opcional) A ID do mecanismo personalizado do Microsoft Translator a ser usado |
| Chave de inscrição | Sua chave de assinatura Microsoft para o Microsoft Translator |

Após criar a configuração, é necessário [ativá-la](#activating-the-translator-service-configurations).

O procedimento a seguir cria uma configuração do Microsoft Translator.

1. No [painel de navegação,](/help/sites-cloud/authoring/getting-started/basic-handling.md#first-steps) clique ou toque em **Ferramentas** -> **Serviços em nuvem** -> **Serviços de tradução em nuvem**.
1. Navegue até o local em que deseja criar a configuração. Normalmente, isso fica na raiz do site ou pode ser uma configuração global padrão.
1. Toque ou clique no botão **Criar**.
1. Defina sua configuração.
   1. Selecione **Microsoft Translator** no menu suspenso.
   1. Digite um título para sua configuração. O título identifica a configuração no console de Serviços em nuvem, bem como nas listas suspensas de propriedade da página.
   1. Opcionalmente, digite um nome a ser usado para o nó do repositório que armazena a configuração.

   ![Criar configuração de tradução](../assets/create-translation-config.png)

1. Clique em **Criar**.
1. Na janela **Editar configuração**, forneça os valores para o serviço de tradução descrito na tabela anterior.

   ![Editar configuração de tradução](../assets/edit-translation-config.png)

1. Toque ou clique em **Conectar** para verificar a conexão.
1. Toque ou clique em **Salvar e fechar**.

## Atualização da configuração da licença de avaliação do Microsoft Translator {#upgrading-the-microsoft-translator-trial-license-configuration}

As páginas de configuração do Microsoft Translation fornecem um link para o site da Microsoft, onde é possível obter uma assinatura de conta adequada para sistemas de produção.

1. No [painel de navegação,](/help/sites-cloud/authoring/getting-started/basic-handling.md#first-steps) toque ou clique em **Ferramentas** -> **Serviços em nuvem** -> **Serviços de tradução em nuvem**.
1. Toque ou clique na configuração existente do Microsoft Translator.
1. Toque ou clique em **Editar**.
1. Na janela **Editar configuração**, toque ou clique em **Atualizar assinatura**. Uma página web da Microsoft, com mais detalhes sobre o serviço, é aberta.

## Personalizar o mecanismo do Microsoft Translator {#customizing-your-microsoft-translator-engine}

As páginas de configuração do Microsoft Translation fornecem um link para o site da Microsoft, onde é possível personalizar o mecanismo do Microsoft Translator.

1. No [painel de navegação,](/help/sites-cloud/authoring/getting-started/basic-handling.md#first-steps) toque ou clique em **Ferramentas** -> **Serviços em nuvem** -> **Serviços de tradução em nuvem**.
1. Toque ou clique na configuração existente do Microsoft Translator.
1. Toque ou clique em **Editar**.
1. Na janela **Editar configuração**, toque ou clique em **Personalizar tradutor**. Use a página da web da Microsoft que é aberta para personalizar o serviço.

## Ativar as configurações do serviço de tradução {#activating-the-translator-service-configurations}

É necessário ativar as configurações do Cloud Service para oferecer compatibilidade com o conteúdo traduzido que é replicado para a instância de publicação. Use o método de [publicar uma árvore](/help/sites-cloud/authoring/fundamentals/publishing-pages.md#publishing-and-unpublishing-a-tree) para ativar os nós do repositório que armazenam as configurações do Microsoft Translator. Os nós estão localizados abaixo dos seguintes nós principais:

* `/libs/settings/cloudconfigs/translation/msft-translation`
