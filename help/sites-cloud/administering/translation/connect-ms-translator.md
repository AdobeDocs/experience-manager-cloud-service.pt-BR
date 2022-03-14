---
title: Conectar ao Microsoft Translator
description: Saiba como se conectar AEM ao Microsoft Translator pronto para uso para automatizar seu fluxo de trabalho de tradução.
feature: Language Copy
role: Admin
exl-id: ca3c50f9-005e-4871-8606-0cfd3ed21936
source-git-commit: 04054e04d24b5dde093ed3f14ca5987aa11f5b0e
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 4%

---

# Conectar ao Microsoft Translator {#connecting-to-microsoft-translator}

Crie uma configuração para o [Microsoft Translator](https://hub.microsofttranslator.com) serviço em nuvem para usar sua conta de Tradução da Microsoft para traduzir AEM conteúdo ou ativos da página.

>[!TIP]
>
>Se você é novo em traduzir conteúdo, consulte nosso [Jornada de tradução de sites,](/help/journey-sites/translation/overview.md) que é o caminho orientado pela tradução do conteúdo do AEM Sites usando as ferramentas de tradução avançadas do AEM, ideais para aqueles sem experiência de AEM ou tradução.

>[!NOTE]
>
>AEM fornece uma conta de tradução Microsoft de avaliação que permite no máximo 2 000 000 caracteres traduzidos gratuitos por mês. Para obter uma assinatura de conta adequada para sistemas de produção, consulte [Atualização Da Configuração Da Licença De Avaliação Do Microsoft Translator](#upgrading-the-microsoft-translator-trial-license-configuration).

| Propriedade | Descrição |
|---|---|
| Rótulo da tradução | O nome de exibição do serviço de tradução |
| Atribuição da tradução | (Opcional) Para conteúdo gerado pelo usuário, a atribuição que aparece ao lado do texto traduzido, por exemplo `Translations by Microsoft` |
| ID da área de trabalho | (Opcional) A ID do mecanismo personalizado do Microsoft Translator para usar |
| Chave de inscrição | Sua chave de assinatura Microsoft para o Microsoft Translator |

Após criar a configuração, é necessário [ative-a](#activating-the-translator-service-configurations).

O procedimento a seguir cria uma configuração do Microsoft Translator.

1. No [painel de navegação,](/help/sites-cloud/authoring/getting-started/basic-handling.md#first-steps) clicar ou tocar **Ferramentas** -> **Cloud Services** -> **Cloud Services de tradução**.
1. Navegue até o local em que deseja criar a configuração. Normalmente, está na raiz do site ou pode ser uma configuração global padrão.
1. Toque ou clique no botão **Criar** botão.
1. Defina sua configuração.
   1. Selecionar **Microsoft Translator** no menu suspenso .
   1. Digite um título para sua configuração. O título identifica a configuração no console Cloud Services, bem como nas listas suspensas de propriedade da página.
   1. Opcionalmente, digite um nome a ser usado para o nó do repositório que armazena a configuração.

   ![Criar configuração de tradução](../assets/create-translation-config.png)

1. Clique em **Criar**.
1. No **Editar configuração** , forneça os valores para o serviço de tradução descrito na tabela anterior.

   ![Editar configuração de tradução](../assets/edit-translation-config.png)

1. Toque ou clique **Connect** para verificar a conexão.
1. Toque ou clique em **Salvar e fechar**.

## Atualização Da Configuração Da Licença De Avaliação Do Microsoft Translator {#upgrading-the-microsoft-translator-trial-license-configuration}

As páginas de configuração do Microsoft Translation fornecem um link conveniente para o site da Microsoft na web, para obter uma assinatura de conta adequada para sistemas de produção.

1. No [painel de navegação,](/help/sites-cloud/authoring/getting-started/basic-handling.md#first-steps) toque ou clique **Ferramentas** -> **Cloud Services** -> **Cloud Services de tradução**.
1. Toque ou clique na configuração existente do Microsoft Translator.
1. Toque ou clique **Editar**.
1. No **Editar configuração** janela, toque ou clique **Atualizar assinatura**. Uma página da Web do Microsoft com mais detalhes sobre o serviço é aberta.

## Personalização Do Mecanismo Do Tradutor Da Microsoft {#customizing-your-microsoft-translator-engine}

As páginas de configuração da Tradução do Microsoft fornecem um link conveniente para o site da Microsoft na Web, para personalizar o mecanismo do Microsoft Translator.

1. No [painel de navegação,](/help/sites-cloud/authoring/getting-started/basic-handling.md#first-steps) toque ou clique **Ferramentas** -> **Cloud Services** -> **Cloud Services de tradução**.
1. Toque ou clique na configuração existente do Microsoft Translator.
1. Toque ou clique **Editar**.
1. No **Editar configuração** janela, toque ou clique **Personalizar tradutor**. Use a página da Web do Microsoft que é aberta para personalizar seu serviço.

## Ativar as configurações do serviço de tradução {#activating-the-translator-service-configurations}

É necessário ativar as configurações do serviço de nuvem para suportar o conteúdo traduzido que é replicado para a instância de publicação. Use o método de [publicação de uma árvore](/help/sites-cloud/authoring/fundamentals/publishing-pages.md#publishing-and-unpublishing-a-tree) para ativar os nós do repositório que armazenam as configurações do Microsoft Translator. Os nós estão localizados abaixo dos seguintes nós pai:

* `/libs/settings/cloudconfigs/translation/msft-translation`
