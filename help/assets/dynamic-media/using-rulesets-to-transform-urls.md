---
title: Usar conjuntos de regras para transformar URLs
description: Saiba como implantar conjuntos de regras no Dynamic Media para transformar URLs. Os conjuntos de regras são conjuntos de instruções escritos em uma linguagem de script (como JavaScript) que avaliam dados XML e executam determinadas ações se esses dados atenderem a determinadas condições.
contentOwner: Rick Brough
feature: Rulesets,Troubleshooting,Upload
role: User
exl-id: f8010125-ba89-406a-bede-f6aa2f858c70
source-git-commit: ad2b36ffa178d787f50d33ce3393a76811467323
workflow-type: tm+mt
source-wordcount: '720'
ht-degree: 0%

---

# Usar conjuntos de regras para transformar URLs {#using-rulesets-to-transform-urls}

É possível implantar conjuntos de regras no Dynamic Media para transformar URLs. Os conjuntos de regras são conjuntos de instruções escritos em uma linguagem de script (como JavaScript) que avaliam dados XML e executam determinadas ações se esses dados atenderem a determinadas condições. Cada regra consiste em pelo menos uma condição e uma ação. Uma regra avalia os dados XML em relação às condições e, se uma condição for atendida, a ação apropriada será executada. Exemplos de conjuntos de regras incluem o seguinte:

* Adição de um sufixo de tipo MIME. Muitos serviços e sites exigem sufixos de imagem, como adicionar `.jpg` para um URL.
* Criar um caminho de pasta para o URL para fins de SEO (Otimização do mecanismo de pesquisa).

  Consulte [Como o Adobe Dynamic Media Classic oferece suporte a SEO](/help/assets/dynamic-media/assets/s7_seo.pdf).

* Adicionar metadados ao URL para fins de SEO (Otimização do mecanismo de pesquisa).

  Consulte [Como o Adobe Dynamic Media Classic oferece suporte a SEO](/help/assets/dynamic-media/assets/s7_seo.pdf).

* Definir a disposição do conteúdo para acionar um download.
* Simplifique os URLs de modelo do Servidor de imagens para personalização. Por exemplo, turn `rgb{XX,YY,ZZ}` no formato pronto para RTF `\redXX\greenYY\blueZZ`

* Solicitar que determinados caracteres sejam codificados, como `$`, `{`, e `}`e determinados caracteres a serem decodificados para ImageServer. Por exemplo, o Facebook não funciona bem com URLs que contêm caracteres especiais.

  Consulte [Remover caracteres especiais de URLs](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/remove-special-characters-urls.html).

No contexto do Dynamic Media, os sites que usam um sistema baseado em XML para gerenciar informações de ativos podem fazer upload de arquivos XML para o Dynamic Media. Você pode designar um desses arquivos como o arquivo de conjunto de regras de pré-processamento para servir o ativo do Dynamic Media. Esse arquivo reestrutura o formato de protocolo de URL padrão para atender à lógica da empresa de sistemas que estão sendo integrados com o Dynamic Media. Especifique um arquivo XML para servir como o caminho do arquivo de definições do conjunto de regras.

>[!CAUTION]
>
>Tenha cuidado ao usar conjuntos de regras; eles podem impedir que o conteúdo do Dynamic Media seja exibido no seu site.

Há exemplos de conjuntos de regras disponíveis que podem ajudar você a criar seu próprio conjunto de regras.
Consulte [Referência do conjunto de regras](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/rule-set-reference/c-rule-set-reference.html).

Assim como em toda a criação de conjunto de regras, verifique se o arquivo XML é válido antes de fazer upload usando um programa de validação XML, como xmlvalid.
Consulte também [Solução de problemas de conjuntos de regras](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/scene7-ruleset-troubleshooting.html).

Além disso, primeiro teste seu conjunto de regras em um ambiente de preparo que não afete seu ambiente de produção em tempo real.
Os ambientes de produção e de preparo normalmente exigem logons diferentes.

Consulte a [aplicativo de desktop do Adobe Dynamic Media Classic para informações de logon](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#sign-in-dmc-app).

<!-- OBSOLETE CONTENT * **NA staging environment** login page: [https://s7sps1-staging.scene7.com/IpsWeb/](https://s7sps1-staging.scene7.com/IpsWeb/)
* **EMEA staging environment** login page: [https://s7sps3-staging.scene7.com/IpsWeb/](https://s7sps3-staging.scene7.com/IpsWeb/)
* **JAPAC staging environment** login page: [https://s7sps5-staging.scene7.com/IpsWeb/](https://s7sps5-staging.scene7.com/IpsWeb/) -->

Consulte também [Usar a imagem &quot;asset&quot; em vez da imagem &quot;is&quot; em um conjunto de regras](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/ruleset-asset-instead-image.html).

## Implantar conjuntos de regras XML {#deploy-xml-rule-sets}

1. Abra o [aplicativo de desktop do Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), depois faça logon em sua conta.

   Suas credenciais e detalhes de logon foram fornecidos pelo Adobe no momento do provisionamento. Se você não tiver essas informações, entre em contato com o Suporte ao cliente.

1. Faça upload do arquivo de conjunto de regras fazendo o seguinte:

   * Na barra Navegação global, selecione **[!UICONTROL Carregar]**.
   * No **[!UICONTROL Carregar]** próximo ao canto superior esquerdo, selecione **[!UICONTROL Procurar]**.
   * No **[!UICONTROL Abertura]** , navegue até o arquivo de conjunto de regras (XML).
   * Selecione o arquivo e **[!UICONTROL Abertura]**.
   * No lado direito do **[!UICONTROL Carregar]** selecione uma pasta de destino para o arquivo de conjunto de regras.
   * Próximo à parte inferior da página, verifique se a opção Publicar após o upload está marcada.
   * No canto inferior direito da página, selecione **[!UICONTROL Enviar upload]**.
   * Na barra Navegação global, selecione **[!UICONTROL Tarefas]** para verificar o status do trabalho de upload. Quando a variável **[!UICONTROL Status]** coluna na **[!UICONTROL Trabalho]** diz Carregar concluído, continue com as próximas etapas.

1. Na barra de navegação próxima à parte superior da página, navegue até **[!UICONTROL Configuração]** > **[!UICONTROL Configuração do aplicativo]** > **[!UICONTROL Configuração de publicação]** > **[!UICONTROL Servidor de imagens]**.
1. No **[!UICONTROL Publicação de imagem do servidor]** página, sob o **[!UICONTROL Gerenciamento de catálogo]** grupo, localizar **[!UICONTROL Caminho do arquivo de definição do conjunto de regras]** e selecione **[!UICONTROL Selecionar]**.
1. No **[!UICONTROL Selecionar Arquivo de Definição do Conjunto de Regras (XML)]** navegue até o arquivo de conjunto de regras e, no canto inferior direito da página, selecione **[!UICONTROL Selecionar]**.
1. No canto inferior direito da página Configuração, selecione **[!UICONTROL Fechar]**.
1. Execute um trabalho de publicação do servidor de imagens.

   As condições do conjunto de regras são aplicadas às solicitações para os Servidores de imagem ativos da Dynamic Media.

   Se você alterar o arquivo de conjunto de regras, as alterações serão aplicadas imediatamente quando você fizer upload novamente e publicar novamente o arquivo de conjunto de regras atualizado.
