---
title: Conectar ao Microsoft Translator
description: Saiba como conectar o AEM ao Microsoft Translator pronto para uso para automatizar seu fluxo de trabalho de tradução.
feature: Language Copy
role: Admin
exl-id: ca3c50f9-005e-4871-8606-0cfd3ed21936
solution: Experience Manager Sites
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 52%

---

# Conectar ao Microsoft Translator {#connecting-to-microsoft-translator}

O AEM fornece um conector integrado para o [Microsoft Translator](https://www.microsoft.com/pt-br/translator/business/) para traduzir conteúdo ou ativos da página. Após obter uma licença do Microsoft para usar o Microsoft Translator, configure o conector seguindo as instruções nesta página.

>[!TIP]
>
>Se você é novo na tradução de conteúdo, consulte a [Jornada de tradução de sites](/help/journey-sites/translation/overview.md), que é um caminho guiado pela tradução de conteúdo do AEM Sites usando as ferramentas de tradução avançadas do AEM AEM, ideais para aqueles sem experiência com o ou com a tradução.

| Propriedade | Descrição |
|---|---|
| Rótulo da tradução | O nome de exibição do serviço de tradução |
| Atribuição da tradução | (Opcional) Para conteúdo gerado pelo usuário, a atribuição que aparece ao lado do texto traduzido, por exemplo, `Translations by Microsoft` |
| ID do espaço de trabalho | (Opcional) A ID do mecanismo personalizado do Microsoft Translator a ser usado |
| Chave de inscrição | Sua chave de assinatura Microsoft para o Microsoft Translator |

O procedimento a seguir cria uma configuração do Microsoft Translator.

1. No [painel de navegação](/help/sites-cloud/authoring/basic-handling.md#first-steps), selecione **Ferramentas** > **Cloud Service** > **Cloud Service de tradução**.
1. Navegue até o local em que deseja criar a configuração. Normalmente, isso fica na raiz do site ou pode ser uma configuração global padrão.
1. Selecione o botão **Criar**.
1. Defina sua configuração.
   1. Selecione **Microsoft Translator** no menu suspenso.
   1. Digite um título para sua configuração. O título identifica a configuração no console do Cloud Services bem como nas listas suspensas de propriedades da página.
   1. Opcionalmente, digite um nome a ser usado para o nó do repositório que armazena a configuração.

   ![Criar configuração de tradução](../assets/create-translation-config.png)

1. Clique em **Criar**.
1. Na janela **Editar configuração**, forneça os valores para o serviço de tradução descrito na tabela anterior.

   ![Editar configuração de tradução](../assets/msft-config-ui.png)

1. Selecione **Conectar** para verificar a conexão.
1. Selecione **Salvar e fechar**.

## Publicar as configurações do serviço de tradução {#publishing-the-translator-service-configurations}

Como etapa final, publique as configurações do Microsoft Translator para oferecer suporte ao conteúdo traduzido publicado, usando a ação [publicar uma árvore](/help/sites-cloud/authoring/sites-console/publishing-pages.md#publishing-and-unpublishing-a-tree).
