---
title: Usar conjuntos de regras para transformar URLs
description: Saiba como implantar conjuntos de regras no Dynamic Media para transformar URLs. Os conjuntos de regras são conjuntos de instruções escritos em uma linguagem de script (como JavaScript) que avaliam dados XML e executam determinadas ações se esses dados atenderem a determinadas condições.
contentOwner: Rick Brough
feature: Rulesets,Troubleshooting,Upload,Best Practices
role: User
exl-id: f8010125-ba89-406a-bede-f6aa2f858c70
source-git-commit: 35f31c95e92148ff5f3472f26ea9c40fa5a17947
workflow-type: tm+mt
source-wordcount: '720'
ht-degree: 0%

---

# Usar conjuntos de regras para transformar URLs {#using-rulesets-to-transform-urls}

É possível implantar conjuntos de regras no Dynamic Media para transformar URLs. Os conjuntos de regras são conjuntos de instruções escritos em uma linguagem de script (como JavaScript) que avaliam dados XML e executam determinadas ações se esses dados atenderem a determinadas condições. Cada regra consiste em pelo menos uma condição e uma ação. Uma regra avalia os dados XML em relação às condições e, se uma condição for atendida, a ação apropriada será executada. Exemplos de conjuntos de regras incluem o seguinte:

* Adição de um sufixo de tipo MIME. Muitos serviços e sites exigem sufixos de imagem, como adicionar `.jpg` a uma URL.
* Criar um caminho de pasta para o URL para fins de SEO (Otimização do mecanismo de pesquisa).

  Consulte [Como a Adobe Dynamic Media Classic oferece suporte para SEO](/help/assets/dynamic-media/assets/s7_seo.pdf).

* Adicionar metadados ao URL para fins de SEO (Otimização do mecanismo de pesquisa).

  Consulte [Como a Adobe Dynamic Media Classic oferece suporte para SEO](/help/assets/dynamic-media/assets/s7_seo.pdf).

* Definir a disposição do conteúdo para acionar um download.
* Simplifique os URLs de modelo do Servidor de imagens para personalização. Por exemplo, transforme `rgb{XX,YY,ZZ}` no `\redXX\greenYY\blueZZ` pronto para RTF

* Solicite que determinados caracteres sejam codificados, como `$`, `{` e `}`, e que determinados caracteres sejam decodificados em ImageServer. Por exemplo, o Facebook não funciona bem com URLs que contêm caracteres especiais.

  Consulte [Remover caracteres especiais de URLs](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/remove-special-characters-urls.html).

No contexto do Dynamic Media, os sites que usam um sistema baseado em XML para gerenciar informações de ativos podem fazer upload de arquivos XML para o Dynamic Media. Você pode designar um desses arquivos como o arquivo de conjunto de regras de pré-processamento para servir o ativo do Dynamic Media. Esse arquivo reestrutura o formato de protocolo de URL padrão para atender à lógica da empresa de sistemas que estão sendo integrados com o Dynamic Media. Especifique um arquivo XML para servir como o caminho do arquivo de definições do conjunto de regras.

>[!CAUTION]
>
>Tenha cuidado ao usar conjuntos de regras; eles podem impedir que o conteúdo do Dynamic Media seja exibido no seu site.

Há exemplos de conjuntos de regras disponíveis que podem ajudar você a criar seu próprio conjunto de regras.
Consulte [Referência do conjunto de regras](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/rule-set-reference/c-rule-set-reference.html).

Assim como em toda a criação de conjunto de regras, verifique se o arquivo XML é válido antes de fazer upload usando um programa de validação XML, como xmlvalid.
Consulte também [Solucionar problemas dos conjuntos de regras](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/scene7-ruleset-troubleshooting.html).

Além disso, primeiro teste seu conjunto de regras em um ambiente de preparo que não afete seu ambiente de produção em tempo real.
Os ambientes de produção e de preparo normalmente exigem logons diferentes.

Consulte o [aplicativo de desktop do Adobe Dynamic Media Classic para obter informações de entrada](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#sign-in-dmc-app).

<!-- OBSOLETE CONTENT * **NA staging environment** login page: [https://s7sps1-staging.scene7.com/IpsWeb/](https://s7sps1-staging.scene7.com/IpsWeb/)
* **EMEA staging environment** login page: [https://s7sps3-staging.scene7.com/IpsWeb/](https://s7sps3-staging.scene7.com/IpsWeb/)
* **JAPAC staging environment** login page: [https://s7sps5-staging.scene7.com/IpsWeb/](https://s7sps5-staging.scene7.com/IpsWeb/) -->

Consulte também [Usar &#39;asset&#39; em vez da imagem &#39;is&#39; em um conjunto de regras](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/ruleset-asset-instead-image.html).

## Implantar conjuntos de regras XML {#deploy-xml-rule-sets}

1. Abra o [aplicativo de desktop do Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started) e entre na sua conta.

   Suas credenciais e detalhes de logon foram fornecidos pelo Adobe no momento do provisionamento. Se você não tiver essas informações, entre em contato com o Suporte ao cliente.

1. Faça upload do arquivo de conjunto de regras fazendo o seguinte:

   * Na barra Navegação global, selecione **[!UICONTROL Carregar]**.
   * Na página **[!UICONTROL Carregar]**, próximo ao canto superior esquerdo, selecione **[!UICONTROL Procurar]**.
   * Na caixa de diálogo **[!UICONTROL Abrir]**, navegue até o arquivo de conjunto de regras (XML).
   * Selecione o arquivo e, em seguida, **[!UICONTROL Abrir]**.
   * No lado direito da página **[!UICONTROL Carregar]**, selecione uma pasta de destino para o arquivo de conjunto de regras.
   * Próximo à parte inferior da página, verifique se a opção Publish After Upload está marcada.
   * No canto inferior direito da página, selecione **[!UICONTROL Enviar Upload]**.
   * Na barra Navegação global, selecione **[!UICONTROL Trabalhos]** para verificar o status do trabalho de carregamento. Quando a coluna **[!UICONTROL Status]** na página **[!UICONTROL Trabalho]** indicar Carregamento concluído, continue com as próximas etapas.

1. Na barra de navegação próxima à parte superior da página, navegue até **[!UICONTROL Configuração]** > **[!UICONTROL Configuração do Aplicativo]** > **[!UICONTROL Configuração do Publish]** > **[!UICONTROL Servidor de Imagens]**.
1. Na página **[!UICONTROL Publish do Servidor de Imagens]**, no grupo **[!UICONTROL Gerenciamento de Catálogo]**, localize o **[!UICONTROL Caminho do Arquivo de Definição de Conjunto de Regras]** e selecione **[!UICONTROL Selecionar]**.
1. Na página **[!UICONTROL Selecionar Arquivo de Definição do Conjunto de Regras (XML)]**, navegue até o arquivo de conjunto de regras e, no canto inferior direito da página, selecione **[!UICONTROL Selecionar]**.
1. No canto inferior direito da página Instalação, selecione **[!UICONTROL Fechar]**.
1. Execute um trabalho do Publish do Servidor de imagens.

   As condições do conjunto de regras são aplicadas às solicitações para os Servidores de imagem ativos da Dynamic Media.

   Se você alterar o arquivo de conjunto de regras, as alterações serão aplicadas imediatamente quando você fizer upload novamente e publicar novamente o arquivo de conjunto de regras atualizado.
