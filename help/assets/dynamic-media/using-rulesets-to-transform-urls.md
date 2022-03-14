---
title: Usar conjuntos de regras para transformar URLs
description: Saiba como implantar conjuntos de regras no Dynamic Media para transformar URLs. Os conjuntos de regras são conjuntos de instruções escritas em uma linguagem de script (como JavaScript) que avalia dados XML e executa determinadas ações se esses dados atenderem a determinadas condições.
role: User
exl-id: f8010125-ba89-406a-bede-f6aa2f858c70
source-git-commit: d37193833d784f3f470780b8f28e53b473fd4e10
workflow-type: tm+mt
source-wordcount: '766'
ht-degree: 0%

---

# Usar conjuntos de regras para transformar URLs {#using-rulesets-to-transform-urls}

Você pode implantar conjuntos de regras no Dynamic Media para transformar URLs. Os conjuntos de regras são conjuntos de instruções escritas em uma linguagem de script (como JavaScript) que avalia dados XML e executa determinadas ações se esses dados atenderem a determinadas condições. Cada regra consiste em pelo menos uma condição e pelo menos uma ação. Uma regra avalia os dados XML em relação às condições e, se uma condição for atendida, tomará a ação apropriada. Exemplos de conjuntos de regras incluem:

* Adicionar um sufixo do tipo MIME. Muitos serviços e sites exigem sufixos de imagem, como a adição de `.jpg` para um URL.
* Criação de um caminho de pasta para o URL para fins de SEO (Otimização de Mecanismo de Pesquisa).

   Consulte [Como a Adobe Dynamic Media Classic suporta SEO](/help/assets/dynamic-media/assets/s7_seo.pdf).

* Adicionar metadados ao URL para fins de SEO (Otimização de mecanismo de pesquisa).

   Consulte [Como a Adobe Dynamic Media Classic suporta SEO](/help/assets/dynamic-media/assets/s7_seo.pdf).

* Definir a disposição do conteúdo para acionar um download.
* Simplifique os URLs de modelos do Image Serving para personalização. Por exemplo, virar `rgb{XX,YY,ZZ}` no modo pronto para RTF `\redXX\greenYY\blueZZ`

* Solicite determinados caracteres para serem codificados, como `$`, `{`e `}`e determinados caracteres a serem decodificados para o ImageServer. Por exemplo, o Facebook não funciona bem com URLs contendo caracteres especiais.

   Consulte [Remover caracteres especiais de URLs](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/remove-special-characters-urls.html).

No contexto do Dynamic Media, os sites que usam um sistema baseado em XML para gerenciar informações de ativos podem fazer upload de arquivos XML para o Dynamic Media. Você pode designar um desses arquivos como o arquivo de conjunto de regras de pré-processamento para servir ativos do Dynamic Media. Esse arquivo reestrutura o formato de protocolo URL padrão para atender à lógica da empresa de sistemas que estão sendo integrados ao Dynamic Media. Você especifica um arquivo XML a ser exibido como o caminho de arquivo das definições do conjunto de regras.

>[!CAUTION]
>
>Tenha cuidado ao usar conjuntos de regras; elas podem impedir que o conteúdo do Dynamic Media seja exibido no seu site.

Existem conjuntos de regras de amostra disponíveis que podem ajudar você a criar seu próprio conjunto de regras.
Consulte [Referência do conjunto de regras](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/rule-set-reference/c-rule-set-reference.html).

Como em toda a criação do conjunto de regras, certifique-se de que o arquivo XML seja válido antes de fazer upload usando um programa de validação XML, como xmlvalid.
Consulte também [Solucionar problemas de conjuntos de regras](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/scene7-ruleset-troubleshooting.html).

Além disso, certifique-se de testar primeiro seu conjunto de regras em um ambiente de preparo que não afete seu ambiente de produção ativo.
Ambientes de produção e ambientes de preparo normalmente exigem logons diferentes.

Consulte a [Aplicativo de desktop do Adobe Dynamic Media Classic para obter informações de logon](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#sign-in-dmc-app).

<!-- OBSOLETE CONTENT * **NA staging environment** login page: [https://s7sps1-staging.scene7.com/IpsWeb/](https://s7sps1-staging.scene7.com/IpsWeb/)
* **EMEA staging environment** login page: [https://s7sps3-staging.scene7.com/IpsWeb/](https://s7sps3-staging.scene7.com/IpsWeb/)
* **JAPAC staging environment** login page: [https://s7sps5-staging.scene7.com/IpsWeb/](https://s7sps5-staging.scene7.com/IpsWeb/) -->

Consulte também [Usar &#39;asset&#39; em vez de &#39;is&#39; imagem em um conjunto de regras](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/ruleset-asset-instead-image.html).

## Implantar conjuntos de regras XML {#deploy-xml-rule-sets}

1. Abra o [Aplicativo de desktop do Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), em seguida, faça logon em sua conta.

   Suas credenciais e detalhes de logon foram fornecidos pelo Adobe no momento do provisionamento. Caso não tenha essas informações, entre em contato com o Suporte ao cliente.

1. Faça upload do arquivo de conjunto de regras fazendo o seguinte:

   * Na barra Navegação global, selecione **[!UICONTROL Upload]**.
   * No **[!UICONTROL Upload]** , próximo ao canto superior esquerdo, selecione **[!UICONTROL Procurar]**.
   * No **[!UICONTROL Abrir]** , navegue até o arquivo do conjunto de regras (XML).
   * Selecione o arquivo e selecione **[!UICONTROL Abrir]**.
   * No lado direito do **[!UICONTROL Upload]** selecione uma pasta de destino para o arquivo de conjunto de regras.
   * Próximo à parte inferior da página, verifique se a opção Publicar após o upload está marcada.
   * No canto inferior direito da página, selecione **[!UICONTROL Enviar upload]**.
   * Na barra Navegação global, selecione **[!UICONTROL Tarefas]** para verificar o status do trabalho de upload. Quando a variável **[!UICONTROL Status]** na coluna **[!UICONTROL Tarefa]** diz Fazer upload concluído, continue para as próximas etapas.

1. Na barra de navegação próxima à parte superior da página, navegue até **[!UICONTROL Configuração]** > **[!UICONTROL Configuração do aplicativo]** > **[!UICONTROL Configuração de publicação]** > **[!UICONTROL Servidor de imagem]**.
1. No **[!UICONTROL Publicação do servidor de imagens]** na página **[!UICONTROL Gerenciamento de catálogo]** agrupar, localizar **[!UICONTROL Caminho do Arquivo de Definição do Conjunto de Regras]**, em seguida selecione **[!UICONTROL Selecionar]**.
1. No **[!UICONTROL Selecionar Arquivo de Definição de Conjunto de Regras (XML)]** navegue até o arquivo do conjunto de regras e, no canto inferior direito da página, selecione **[!UICONTROL Selecionar]**.
1. No canto inferior direito da página Configurar, selecione **[!UICONTROL Fechar]**.
1. Execute um trabalho de publicação do servidor de imagens.

   As condições do conjunto de regras são aplicadas nas solicitações dos Servidores de Imagem Dynamic Media ao vivo.

   Se você alterar o arquivo do conjunto de regras, as alterações serão aplicadas imediatamente quando você fizer upload e publicar novamente o arquivo do conjunto de regras atualizado.
