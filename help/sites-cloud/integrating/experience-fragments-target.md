---
title: Exportar fragmentos de experiência para o Adobe Target
description: Exportar fragmentos de experiência para o Adobe Target
exl-id: 752d91f9-13a6-40c2-9425-7d18dafe9205
source-git-commit: 8e13f671ada67e4e22b66094ad23bf5a0508ccba
workflow-type: tm+mt
source-wordcount: '2259'
ht-degree: 1%

---

# Exportar fragmentos de experiência para o Adobe Target{#exporting-experience-fragments-to-adobe-target}

>[!CAUTION]
>
>* Os Fragmentos de experiência AEM são exportados para o espaço de trabalho padrão do Adobe Target.
>* AEM deve ser integrado ao Adobe Target de acordo com as instruções em [Integração com o Adobe Target](/help/sites-cloud/integrating/integrating-adobe-target.md).


Você pode exportar [Fragmentos de experiência](/help/sites-cloud/authoring/fundamentals/experience-fragments.md), criado no Adobe Experience Manager as a Cloud Service (AEM), no Adobe Target (Target). Eles podem ser usados como ofertas em atividades do Target, para testar e personalizar experiências em escala.

Há três opções disponíveis para exportar um Fragmento de experiência para o Adobe Target:

* HTML (padrão): Suporte para entrega de conteúdo da Web e híbrido
* JSON: Suporte para entrega de conteúdo sem periféricos
* HTML e JSON

Para preparar sua instância para exportar AEM Fragmentos de experiência para o Adobe Target, é necessário:

* [Faça a integração com o Adobe Target](/help/sites-cloud/integrating/integrating-adobe-target.md)
* [Adicionar a configuração da nuvem](#add-the-cloud-configuration)
* [Adicionar a configuração herdada](#add-the-legacy-configuration)

Depois disso, é possível:

* [Exportar um fragmento de experiência para o Adobe Target](#exporting-an-experience-fragment-to-adobe-target)
* [Usar seus Fragmentos de experiência no Adobe Target](#using-your-experience-fragments-in-adobe-target)
* E também [Excluir um fragmento de experiência já exportado para o Adobe Target](#deleting-an-experience-fragment-already-exported-to-adobe-target)

Os Fragmentos de experiência podem ser exportados para o espaço de trabalho padrão no Adobe Target ou para espaços de trabalho definidos pelo usuário no Adobe Target.

>[!NOTE]
>
>Os espaços de trabalho do Adobe Target não existem no próprio Adobe Target. Eles são definidos e gerenciados no Adobe IMS (Identity Management System) e, em seguida, selecionados para uso nas soluções usando o Adobe Developer Console.

>[!NOTE]
>
>Os espaços de trabalho do Adobe Target podem ser usados para permitir que membros de uma organização (grupo) criem e gerenciem ofertas e atividades somente para essa organização; sem conceder acesso a outros usuários. Por exemplo, organizações específicas de cada país dentro de uma preocupação global.

>[!NOTE]
>
>Para obter mais informações, consulte também:
>
>* [Desenvolvimento do Adobe Target](http://developers.adobetarget.com/)
>* [Componentes principais - Fragmentos de experiência](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=pt-BR)
>* [Adobe Target - Como uso os fragmentos de experiência do Adobe Experience Manager (AEM)?](https://experienceleague.adobe.com/docs/target/using/experiences/offers/aem-experience-fragments.html?lang=en)
>* [AEM 6.5 - Configuração manual da integração com o Adobe Target - Criação de uma configuração da nuvem do Target](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/target-configuring.html#creating-a-target-cloud-configuration)


## Pré-requisitos {#prerequisites}

Várias ações são necessárias:

1. Você tem que [integrar AEM com o Adobe Target](/help/sites-cloud/integrating/integrating-adobe-target.md).

1. Os Fragmentos de experiência são exportados da instância do autor do AEM, portanto, é necessário [Configurar o AEM Link Externalizer](/help/implementing/developing/extending/experience-fragments.md#configuring-the-aem-link-externalizer) na instância do autor para garantir que todas as referências no Fragmento de experiência sejam externalizadas para entrega na Web.

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
   >Se você adicionar a configuração da nuvem ao próprio Fragmento de experiência, a configuração será herdada por todas as variações.

1. Selecione o **Cloud Services** guia .

1. Em **Configuração Cloud Service**, selecione **Adobe Target** na lista suspensa.

   >[!NOTE]
   >
   >O formato JSON de uma oferta de Fragmento de experiência pode ser personalizado. Para fazer isso, defina um componente de Fragmento de experiência do cliente e anote como exportar suas propriedades no componente Modelo do Sling.
   >
   >Consulte o componente principal: [Componentes principais - Fragmentos de experiência](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/experience-fragment.html)

1. Em **Adobe Target** selecione:

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

   Por exemplo, para uma pasta:

   ![Pasta - Cloud Services](assets/xf-target-integration-01.png "Pasta - Cloud Services")

1. **Salvar e fechar**.

## Adicionar a configuração herdada {#add-the-legacy-configuration}

<!-- This is effectively the Manually Integrating with Adobe Target {#manually-integrating-with-adobe-target} section from 6.5 -->

>[!IMPORTANT]
>
>Adicionar uma nova configuração Herdada é um cenário de caso especial que só é suportado para exportar Fragmentos de experiência.

Depois [adicionar a configuração do Cloud](#add-the-cloud-configuration) para usar o Launch by Adobe, para integrar inicialmente o AEM com o Adobe Target, também é necessário integrar manualmente o com o Adobe Target usando uma configuração herdada.

### Criação de uma configuração da nuvem do Target {#creating-a-target-cloud-configuration}

Para permitir que o AEM interaja com o Adobe Target, crie uma configuração de nuvem do Target. Para criar a configuração, forneça o código de cliente do Adobe Target e as credenciais do usuário.

Você cria a configuração da nuvem do Target apenas uma vez, pois pode associar a configuração a várias campanhas AEM. Se você tiver vários códigos de cliente Adobe Target, crie uma configuração para cada código de cliente.

É possível configurar a configuração da nuvem para sincronizar segmentos do Adobe Target. Se você habilitar a sincronização, os segmentos serão importados do Target em segundo plano assim que a configuração da nuvem for salva.

Use o procedimento a seguir para criar uma configuração de nuvem do Target no AEM:

1. Navegar para **Cloud Services herdados** através da **Logotipo AEM** > **Ferramentas** > **Cloud Services** > **Cloud Services herdados**.
Por exemplo: ([http://localhost:4502/libs/cq/core/content/tools/cloudservices.html](http://localhost:4502/libs/cq/core/content/tools/cloudservices.html))

   O **Adobe Experience Cloud** a página de visão geral é aberta.

1. No **Adobe Target** seção , clique em **Configurar agora**.
1. No **Criar configuração** caixa de diálogo:

   1. Forneça uma configuração **Título**.
   1. Selecione o **Configuração do Adobe Target** modelo .
   1. Clique em **Criar**.

Agora é possível selecionar a nova configuração para edição.

1. A caixa de diálogo Editar é aberta.

   ![config-target-settings-dialog](assets/config-target-settings-dialog.png)

   <!-- Can this still occur?

   >[!NOTE]
   >
   >When configuring A4T with AEM, you may see a Configuration reference missing entry. To be able to select the analytics framework, do the following:
   >
   >1. Navigate to **Tools** &gt; **General** &gt; **CRXDE Lite**.
   >1. Navigate to **/libs/cq/analytics/components/testandtargetpage/dialog/items/tabs/items/tab1_general/items/a4tAnalyticsConfig**
   >1. Set the property **disable** to **false**.
   >1. Tap or click **Save All**.

   -->

1. No **Configurações do Adobe Target** , forneça valores para essas propriedades.

   * **Autenticação**: esse padrão é IMS (as credenciais do usuário estão obsoletas)

   * **Código do cliente**: o Código do cliente da conta do Target

   * **ID do locatário**: a ID do locatário

   * **Configuração IMS**: selecione a configuração necessária na lista suspensa

   * **Tipo de API**: o padrão é REST (o XML está obsoleto)

   * **Configuração do A4T Analytics Cloud**: Selecione a configuração de nuvem do Analytics usada para métricas e metas de atividade do Target. Isso é necessário se estiver usando o Adobe Analytics como fonte de relatórios ao direcionar conteúdo.

      <!-- Is this needed?
     If you do not see your cloud configuration, see note in [Configuring A4T Analytics Cloud Configuration](#configuring-a-t-analytics-cloud-configuration).
     -->

   * **Usar direcionamento preciso:** Por padrão, essa caixa de seleção está marcada. Se selecionada, a configuração do serviço de nuvem aguardará o contexto carregar antes de carregar o conteúdo. Veja a observação a seguir.

   * **Sincronizar segmentos do Adobe Target:** Selecione essa opção para baixar segmentos definidos no Target para usá-los em AEM. Você deve selecionar essa opção quando a propriedade Tipo de API for REST, pois os segmentos em linha não são compatíveis e você sempre precisa usar segmentos do Target. (Observe que o termo AEM de &quot;segmento&quot; equivale ao &quot;público-alvo&quot; do Target.)

   * **Biblioteca do cliente:** esse padrão é AT.js (mbox.js está obsoleta)

      >[!NOTE]
      >
      >O arquivo da Biblioteca do Target, [AT.JS](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/implement-target-for-client-side-web.html)O é uma nova biblioteca de implementação do Adobe Target, projetada para implementações típicas da Web e aplicativos de página única.
      >
      >A mbox.js foi descontinuada e será removida em um estágio posterior.
      >
      >O Adobe recomenda usar a AT.js em vez da mbox.js como a biblioteca do cliente.
      >
      >A AT.js oferece várias melhorias em relação à biblioteca mbox.js:
      >
      >* Tempos de carregamento de página aprimorados para implementações da Web
      >* Segurança aprimorada
      >* Melhores opções de implementação para aplicativos de página única
      >* A AT.js contém os componentes que foram incluídos na target.js, portanto, target.js não é mais chamada

      >
      >Você pode selecionar AT.js ou mbox.js no **Biblioteca do cliente** menu suspenso.

   * **Usar o Tag Management System para fornecer a biblioteca do cliente** - Selecione essa opção para usar a biblioteca do cliente no Adobe Launch ou outro sistema de gerenciamento de tags (ou DTM, que está obsoleto).

   * **AT.js personalizada**: Navegue para fazer upload de sua AT.js personalizada. Deixe em branco para usar a biblioteca padrão.

      >[!NOTE]
      >
      >Por padrão, quando você opta pelo assistente de configuração do Adobe Target, o Direcionamento preciso é ativado.
      >
      >Direcionamento preciso significa que a configuração do serviço de nuvem aguarda o contexto ser carregado antes de carregar o conteúdo. Como resultado, em termos de desempenho, o direcionamento preciso pode criar um atraso de alguns milissegundos antes de carregar o conteúdo.
      >
      >O direcionamento preciso é sempre ativado na instância do autor. No entanto, na instância de publicação, é possível desativar o direcionamento preciso globalmente, limpando a marca de seleção ao lado de Direcionamento preciso na configuração do serviço de nuvem (**http://localhost:4502/etc/cloudservices.html**). Você também pode ativar e desativar o direcionamento preciso para componentes individuais, independentemente da sua configuração na configuração do serviço de nuvem.
      >
      >Se tiver ***já*** componentes direcionados criados e você altera essa configuração, suas alterações não afetam esses componentes. Você deve fazer alterações diretamente nesses componentes.

1. Clique em **Conectar-se ao Adobe Target** para inicializar a conexão com o Target. Se a conexão for bem-sucedida, a mensagem **Conexão bem-sucedida** é exibida. Clique em **OK** na mensagem e depois **OK** na caixa de diálogo.

   Se não conseguir se conectar ao Target, consulte a [solução de problemas](#troubleshooting-target-connection-problems) seção.

### Adicionar uma estrutura do Target {#adding-a-target-framework}

<!-- Is this section needed? -->

Após configurar a configuração da nuvem do Target, adicione uma estrutura do Target. A estrutura identifica os parâmetros padrão enviados para o Adobe Target a partir do [ContextHub](/help/implementing/developing/personalization/configuring-contexthub.md) componentes. O Target usa os parâmetros para determinar os segmentos que se aplicam ao contexto atual.

Você pode criar várias estruturas para uma única configuração do Target. Várias estruturas são úteis quando você precisa enviar um conjunto diferente de parâmetros para o Target para diferentes seções do seu site. Crie uma estrutura para cada conjunto de parâmetros que você precisa enviar. Associe cada seção do seu site à estrutura apropriada. Observe que uma página da Web pode usar somente uma estrutura de cada vez.

1. Na página Configuração do Target , clique no botão **+** (sinal de mais) ao lado de Configurações disponíveis.

1. Na caixa de diálogo Criar estrutura , especifique um **Título**, selecione o **Adobe Target Framework** e clique em **Criar**.

   <!-- ![config-target-framework-dialog](assets/config-target-framework-dialog.png) -->

   A página da estrutura é aberta. O Sidekick fornece componentes que representam informações da [ContextHub](/help/implementing/developing/personalization/configuring-contexthub.md) que podem mapear.

   <!-- ![chlimage_1-162](assets/chlimage_1-162.png) -->

1. Arraste o componente Contexto do Cliente que representa os dados que você deseja usar para mapear para o destino de soltar. Como alternativa, arraste a **Armazenamento do ContextHub** para a estrutura.

   >[!NOTE]
   >
   >Ao mapear, os parâmetros são enviados para uma mbox por meio de strings simples. Não é possível mapear matrizes do ContextHub.

   Por exemplo, para usar **Dados do perfil** sobre os visitantes do seu site para controlar sua campanha do Target, arraste o **Dados do perfil** para a página. As variáveis de dados de perfil disponíveis para mapeamento para parâmetros do Target são exibidas.

   <!-- ![chlimage_1-163](assets/chlimage_1-163.png) -->

1. Selecione as variáveis que você deseja tornar visíveis para o sistema Adobe Target selecionando o **Compartilhar** caixa de seleção nas colunas apropriadas.

   <!-- ![chlimage_1-164](assets/chlimage_1-164.png) -->

   >[!NOTE]
   >
   >A sincronização de parâmetros é uma única maneira - do AEM ao Adobe Target.

Sua estrutura foi criada. Para replicar a estrutura para a instância de publicação, use o **Ativar estrutura** no sidekick.

<!--
### Associating Activities With the Target Cloud Configuration  {#associating-activities-with-the-target-cloud-configuration}

Associate your [AEM activities](/help/sites-cloud/authoring/personalization/activities.md) with your Target cloud configuration so that you can mirror the activities in [Adobe Target](https://experienceleague.adobe.com/docs/target/using/experiences/offers/manage-content.html).

>[!NOTE]
>
>What types of activities are available is determined by the following:
>
>* If the **xt_only** option is enabled on the Adobe Target tenant (clientcode) used on the AEM side to connect to Adobe Target, then you can create **only** XT activities in AEM.
>
>* If the **xt_only** options is **not** enabled on the Adobe Target tenant (clientcode), then you can create **both** XT and A/B activities in AEM.
>
>**Additional note:** **xt_only** options is a setting applied on a certain Target tenant (clientcode) and can only be modified directly in Adobe Target. You cannot enable or disable this option in AEM.
-->

<!--
### Associating the Target Framework With Your Site {#associating-the-target-framework-with-your-site}

After you create a Target framework in AEM, associate your web pages with the framework. The targeted components on the pages send the framework-defined data to Adobe Target for tracking. (See [Content Targeting](/help/sites-cloud/authoring/personalization/targeted-content.md).)

When you associate a page with the framework, the child pages inherit the association.

1. In the **Sites** console, navigate to the site that you want to configure.
1. Using either [quick actions](/help/sites-cloud/authoring/getting-started/basic-handling.md#quick-actions) or [selection mode](/help/sites-cloud/authoring/getting-started/basic-handling.md#selecting-resources), select **View Properties.**
1. Select the **Cloud Services** tab.
1. Tap/click **Edit**.
1. Tap/click **Add Configuration** under **Cloud Service Configurations** and select **Adobe Target**.

  ![chlimage_1-165](assets/chlimage_1-165.png)

1. Select the framework you want under **Configuration Reference**.

   >[!NOTE]
   >
   >Make sure that you select the specific **framework** that you created and not the Target cloud configuration under which it was created.

1. Tap/click **Done**.
1. Activate the root page of the website to replicate it to the publish server. (See [How To Publish Pages](/help/sites-cloud/authoring/fundamentals/publishing-pages.md).)

   >[!NOTE]
   >
   >If the framework you attached to the page was not activated yet, a wizard opens which allows you to publish it as well.
-->

<!--
### Troubleshooting Target Connection Problems {#troubleshooting-target-connection-problems}

Perform the following tasks to troubleshoot problems that occur when connecting to Target:

* Make sure that the user credentials that you provide are correct.
* Make sure that the AEM instance can connect to the Target server. For example, make sure that firewall rules are not blocking outbound AEM connections, or that AEM is configured to use necessary proxies.
* Look for helpful messages in the AEM error log. The error.log file is located in the **crx-quickstart/logs** directory where AEM is installed.
* When editing the activity in Adobe Target, the URL is pointing to localhost. Work around this by setting the AEM externalizer to the correct URL.
-->

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
