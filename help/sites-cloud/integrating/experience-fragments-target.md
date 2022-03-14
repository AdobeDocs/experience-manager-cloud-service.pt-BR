---
title: Exportar fragmentos de experiência para o Adobe Target
description: Exportar fragmentos de experiência para o Adobe Target
exl-id: 752d91f9-13a6-40c2-9425-7d18dafe9205
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '1118'
ht-degree: 2%

---

# Exportar fragmentos de experiência para o Adobe Target{#exporting-experience-fragments-to-adobe-target}

>[!CAUTION]
>
>* Os Fragmentos de experiência AEM são exportados para o espaço de trabalho padrão do Adobe Target.
>* AEM deve ser integrado ao Adobe Target de acordo com as instruções em [Integração com o Adobe Target](/help/sites-cloud/integrating/integrating-adobe-target.md).


Você pode exportar [Fragmentos de experiência](/help/sites-cloud/authoring/fundamentals/experience-fragments.md), criado no Adobe Experience Manager as a Cloud Service (AEM), no Adobe Target (Target). Eles podem ser usados como ofertas em atividades do Target, para testar e personalizar experiências em escala.

Há três opções de formato disponíveis para exportar um Fragmento de experiência para o Adobe Target:

* HTML (padrão): Suporte para entrega de conteúdo da Web e híbrido
* JSON: Suporte para entrega de conteúdo sem periféricos
* HTML e JSON

Depois [Integração com o Adobe Target](/help/sites-cloud/integrating/integrating-adobe-target.md) AEM Fragmentos de experiência podem ser exportados para o espaço de trabalho padrão no Adobe Target ou para espaços de trabalho definidos pelo usuário no Adobe Target.

>[!NOTE]
>
>Os espaços de trabalho do Adobe Target não existem no próprio Adobe Target. Eles são definidos e gerenciados no Adobe IMS (Identity Management System) e, em seguida, selecionados para uso em soluções que usam integrações Adobe I/O.

>[!NOTE]
>
>Os espaços de trabalho do Adobe Target podem ser usados para permitir que membros de uma organização (grupo) criem e gerenciem ofertas e atividades somente para essa organização; sem conceder acesso a outros usuários. Por exemplo, organizações específicas de cada país dentro de uma preocupação global.

>[!NOTE]
>
>Para obter mais informações, consulte também:
>
>* [Desenvolvimento do Adobe Target](https://www.adobe.io/apis/experiencecloud/target.html)
>* [Componentes principais - Fragmentos de experiência](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=pt-BR)
>* [Adobe Target - Como uso os fragmentos de experiência do Adobe Experience Manager (AEM)?](https://experienceleague.adobe.com/docs/target/using/experiences/offers/aem-experience-fragments.html?lang=en)


## Pré-requisitos {#prerequisites}


Várias ações são necessárias:

1. Você tem que [integrar AEM com o Adobe Target](/help/sites-cloud/integrating/integrating-adobe-target.md).
2. Os Fragmentos de experiência são exportados da instância do autor do AEM, portanto, é necessário [Configurar o AEM Link Externalizer](/help/implementing/developing/extending/experience-fragments.md#configuring-the-aem-link-externalizer) na instância do autor para garantir que todas as referências no Fragmento de experiência sejam externalizadas para entrega na Web.

   >[!NOTE]
   >
   >Para a reescrita de links não coberta pelo padrão, a variável [Provedor de regravação do link do fragmento de experiência](/help/implementing/developing/extending/experience-fragments.md#the-experience-fragment-link-rewriter-provider-html) está disponível. Com isso, regras personalizadas podem ser desenvolvidas para sua instância.

## Adicionar a configuração da nuvem {#add-the-cloud-configuration}

Antes de exportar um fragmento, é necessário adicionar o **Configuração na nuvem** para **Adobe Target** ao fragmento ou pasta. Isso também permite:

* especificar as opções de formato a serem usadas para exportar
* selecione um espaço de trabalho do Target como destino
* selecione um domínio externalizador para reescrever referências no Fragmento de experiência (opcional)

As opções necessárias podem ser selecionadas em **Propriedades da página** da pasta e/ou fragmento necessários; a especificação será herdada conforme necessário.

1. Navegue até o **Fragmentos de experiência** console.

1. Abrir **Propriedades da página** para a pasta ou fragmento apropriado.

   >[!NOTE]
   >
   >Se você adicionar a configuração de nuvem à pasta pai do Fragmento de experiência, a configuração será herdada por todos os filhos.
   >
   >
   >Se você adicionar a configuração da nuvem ao próprio Fragmento de experiência, a configuração será herdada por todas as variações.

1. Selecione o **Cloud Services** guia .

1. Em **Configuração Cloud Service**, selecione **Adobe Target** na lista suspensa.

   >[!NOTE]
   >
   >O formato JSON de uma oferta de Fragmento de experiência pode ser personalizado. Para fazer isso, defina um componente de Fragmento de experiência do cliente e anote como exportar suas propriedades no componente Modelo do Sling.
   >
   >Consulte o componente principal:
   >
   >[Componentes principais - Fragmentos de experiência](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/experience-fragment.html)

   Em **Adobe Target** selecione:

   * a configuração apropriada
   * a opção de formato necessária
   * um espaço de trabalho Adobe Target
   * se necessário - o domínio externalizador

   >[!CAUTION]
   >
   >O domínio externalizador é opcional.
   >
   > Um AEM externalizador é configurado quando você deseja que o conteúdo exportado aponte para um *publicar* domínio. Para obter mais detalhes, consulte [Configurar o AEM Link Externalizer](/help/implementing/developing/extending/experience-fragments.md#configuring-the-aem-link-externalizer).
   >
   > Observe também que os Domínios do Externalizador são relevantes somente para o conteúdo do Fragmento de experiência que é enviado ao Target, e não para metadados como Exibir conteúdo da oferta.

<!--
   For example, for a folder:

   ![Folder - Cloud Services](assets/xf-target-integration-01.png "Folder - Cloud Services")
-->

1. **Salvar e fechar**.

## Exportar um fragmento de experiência para o Adobe Target {#exporting-an-experience-fragment-to-adobe-target}

>[!CAUTION]
>
>Para ativos de mídia, como imagens, somente uma referência é exportada para o Target. O próprio ativo permanece armazenado no AEM Assets e é entregue a partir da instância de publicação do AEM.
>
>Devido a isso, o Fragmento de experiência, com todos os ativos relacionados, precisa ser publicado antes da exportação para o Target.

Para exportar um fragmento de experiência do AEM para o Target (depois de especificar a configuração da nuvem):

1. Navegue até o console Fragmento de experiência .
1. Selecione o Fragmento de experiência que deseja exportar para o target.

   >[!NOTE]
   >
   >Deve ser uma variação Web de Fragmento de experiência.

1. Toque/clique **Exportar para o Adobe Target**.

   >[!NOTE]
   >
   >Se o Fragmento de experiência já tiver sido exportado, selecione **Atualização no Adobe Target**.

1. Toque/clique **Exportar sem publicação** ou **Publicar** conforme necessário.

   >[!NOTE]
   >
   >Selecionar **Publicar** O publicará o fragmento de experiência imediatamente e o enviará para o Target.

1. Toque/clique **OK** na caixa de diálogo de confirmação.

   Seu fragmento de experiência agora deve estar no Target.

   >[!NOTE]
   >
   >[Vários detalhes](/help/sites-cloud/authoring/fundamentals/experience-fragments.md#details-of-your-experience-fragment) da exportação pode ser **Exibição de lista** do console e **Propriedades**.

   >[!NOTE]
   >
   >Ao visualizar um fragmento de experiência no Adobe Target, a variável *última modificação* data vista é a data em que o fragmento foi modificado pela última vez em AEM, não a data em que o fragmento foi exportado pela última vez para o Adobe Target.

>[!NOTE]
>
>Como alternativa, você pode executar a exportação do editor de páginas, usando comandos comparáveis no [Informações da página](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-information) menu.

## Uso dos Fragmentos de experiência no Adobe Target {#using-your-experience-fragments-in-adobe-target}

Depois de executar as tarefas anteriores, o fragmento de experiência é exibido na página Ofertas no Target. Dê uma olhada no [documentação específica do Target](https://experiencecloud.adobe.com/resources/help/en_US/target/target/aem-experience-fragments.html) para saber mais sobre o que você pode alcançar lá.

>[!NOTE]
>
>Ao visualizar um fragmento de experiência no Adobe Target, a variável *última modificação* data vista é a data em que o fragmento foi modificado pela última vez em AEM, não a data em que o fragmento foi exportado pela última vez para o Adobe Target.

## Excluir um fragmento de experiência já exportado para o Adobe Target {#deleting-an-experience-fragment-already-exported-to-adobe-target}

Excluir um fragmento de experiência que já foi exportado para o Target pode causar problemas se o fragmento já estiver sendo usado em uma oferta no Target. A exclusão do fragmento tornaria a oferta inutilizável, pois o conteúdo do fragmento está sendo entregue pelo AEM.

Para evitar essas situações:

* Se o Fragmento de experiência não estiver sendo usado atualmente em uma atividade, o AEM permite que o usuário exclua o fragmento sem uma mensagem de aviso.
* Se o Fragmento de experiência estiver sendo usado atualmente por uma atividade no Target, uma mensagem de erro avisará o usuário AEM sobre possíveis consequências que a exclusão do fragmento terá na atividade.

   A mensagem de erro no AEM não proíbe que o usuário (force-)exclua o Fragmento de experiência. Se o Fragmento de experiência for excluído:

   * A oferta do Target com AEM fragmento de experiência pode mostrar um comportamento indesejado

      * A oferta provavelmente ainda será renderizada, pois o HTML do Fragmento de experiência foi enviado para o Target
      * Qualquer referência no Fragmento de experiência pode não funcionar corretamente se os ativos referenciados também tiverem sido excluídos no AEM.
   * É claro que qualquer alteração adicional no Fragmento de experiência é impossível, pois o Fragmento de experiência não existe mais no AEM.
