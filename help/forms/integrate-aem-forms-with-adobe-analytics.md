---
title: Como integrar o AEM Forms com o Adobe Analytics?
seo-title: Learn how to integrate AEM Forms with Adobe Analytics.
exl-id: 0730432e-75b8-4b35-a377-ae4a2bee6c9f
hidefromtoc: true
feature: Adaptive Forms, Acrobat Sign
role: User, Developer
source-git-commit: 64a8b363cff079aa0a6f56effd77830ac797deca
workflow-type: tm+mt
source-wordcount: '1709'
ht-degree: 1%

---

# Integrar o AEM Forms com o [!DNL Adobe Analytics] {#integrate-aem-forms-with-adobe-analytics}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/integrate-aem-forms-with-experience-cloud-solutions/configure-analytics-forms-documents.html) |
| AEM as a Cloud Service | Este artigo |

<span class="preview"> Este documento descreve o procedimento manual para habilitar o Adobe Analytics em um Formulário adaptável. No entanto, o Adobe recomenda usar o [Habilitar o Adobe Analytics para um Formulário Adaptável usando a Automação de Instalação do Experience Cloud](/help/forms/enable-adobe-analytics-adaptive-form-using-experience-cloud-setup-automation.md). </span>

O AEM Forms integra-se ao [Adobe Analytics](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/overview.html?lang=en) para permitir que você capture e rastreie métricas de desempenho para seus formulários publicados. O objetivo por trás da análise dessas métricas é permitir que os usuários empresariais obtenham insights sobre o comportamento do usuário final e otimizem a experiência de captura de dados. Você pode capturar e rastrear o comportamento de usuários conectados e não conectados (anônimos) por meio do Adobe Analytics para Forms adaptável.

Após executar as ações mencionadas neste artigo, você pode configurar e exibir relatórios no [!DNL Adobe Analytics], conforme demonstrado no vídeo a seguir:

>[!VIDEO](https://video.tv.adobe.com/v/337262)

Você pode usar o [!DNL Adobe Analytics] para descobrir padrões de interação e problemas que os usuários enfrentam ao usar formulários adaptáveis. Pronto para uso, [!DNL Adobe Analytics] rastreia e armazena informações sobre os seguintes eventos:

* **Renderização**: número de vezes que um formulário é aberto.

* **Enviar**: número de vezes que um formulário é enviado.

* **Abandonar**: número de vezes que os usuários saem sem preencher o formulário.

* **Erro**: Número de erros encontrados no painel e nos campos do painel.

* **Ajuda**: Número de vezes que um usuário abre a ajuda de um painel e os campos do painel.

* **Visita de campo**: número de vezes que um usuário visita um campo no formulário.

* **Salvar**: número de vezes que os usuários salvam um formulário no Portal do Forms.

Além desses eventos prontos para uso, você pode definir eventos personalizados em formulários adaptáveis usando um editor de regras e mapear esses eventos para eventos no [!DNL Adobe Analytics]

A figura a seguir ilustra as ações que você precisa executar antes de exibir relatórios em [!DNL Adobe Analytics]:

![Visão geral do Analytics](assets/analytics-workflow.png)

## 1. Configurar [!DNL Adobe Analytics] {#Configure-adobe-analytics}

Antes de configurar [!DNL Adobe Analytics], crie:

* Uma Adobe ID para fazer logon no [Adobe Experience Cloud](https://experience.adobe.com/#/home).
* Um [conjunto de relatórios](https://experienceleague.adobe.com/docs/analytics/admin/manage-report-suites/new-report-suite/t-create-a-report-suite.html).


### Instalar o AEM Forms e as extensões do [!DNL Adobe Analytics] {#install-extensions}

Execute as seguintes etapas para configurar o AEM Forms e as extensões do [Adobe Analytics](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/analytics/overview.html):

1. Faça logon no Adobe Experience Cloud e selecione um nome apropriado para a empresa.

1. Selecione **[!UICONTROL Iniciar/Coleção de Dados]** e **[!UICONTROL Ir para Iniciar/Coleção de Dados]**.

1. Selecione **[!UICONTROL Nova propriedade]** e especifique um nome para a configuração.

1. Especifique um nome de domínio e selecione **[!UICONTROL Salvar]** para salvar a propriedade.

1. Selecione o nome da configuração disponível na lista de Propriedades da tag.

1. Na seção **[!UICONTROL Criação]**, selecione **[!UICONTROL Extensões]**.

1. Selecione **[!UICONTROL Catálogo]** e **[!UICONTROL Instalar]** para a extensão **[!UICONTROL Adobe Experience Manager Forms]**. O **[!UICONTROL Adobe Experience Manager Forms]** é exibido na lista de extensões instaladas disponíveis na guia **Instalado**.

1. Selecione **[!UICONTROL Instalar]** para a extensão **[!UICONTROL Adobe Analytics]**.
1. Selecione o nome do conjunto de relatórios nas listas suspensas **[!UICONTROL Conjuntos de relatórios de desenvolvimento]**, **[!UICONTROL Conjuntos de relatórios de preparo]** e **[!UICONTROL Conjuntos de relatórios de produto]** e selecione **[!UICONTROL Salvar]** para salvar a extensão.

### Configurar elementos de dados {#configure-data-elements}

Você pode selecionar qualquer um dos elementos de dados configurados em uma regra criada para um evento. Quando ocorre um evento em um formulário adaptável, o AEM Forms envia esses elementos de dados para [!DNL Adobe Analytics].

Após instalar a extensão **[!UICONTROL Adobe Experience Manager Forms]**, você pode criar os seguintes elementos de dados:

<table>
 <tbody>
  <tr>
   <td>NomeCampo</th>
   <td>TítuloDoCampo</th>
   <td>FormInstance</th>
  </tr>
  <tr>
   <td>FormName<br /> </td>
   <td>TítuloFormulário<br /> </td>
   <td>PageName</td>
  </tr>
  <tr>
   <td>URLdaPágina<br /> </td>
   <td>PanelTitle<br /> </td>
   <td>Tempo gasto</td>
  </tr>
 </tbody>
</table>

Execute as seguintes etapas para configurar elementos de dados:

1. Na seção **[!UICONTROL Criação]**, selecione **[!UICONTROL Elementos de Dados]**.

1. Selecione **[!UICONTROL Criar Novo Elemento De Dados]**.

1. Especifique um nome para o Elemento de dados. Por exemplo, Título do formulário para o tipo de elemento de dados FormTitle.

1. Especifique **[!UICONTROL Adobe Experience Manager Forms]** como o nome da Extensão.

1. Selecione o **[!UICONTROL Tipo de Elemento de Dados]**.

1. Selecione **[!UICONTROL Salvar]** para salvar o elemento de dados.

>[!VIDEO](https://video.tv.adobe.com/v/337472)

### Configurar regras {#configure-rules}

Execute as seguintes etapas para criar regras com base na extensão **[!UICONTROL Adobe Experience Manager Forms]**:

1. Na seção **[!UICONTROL Criação]**, selecione **[!UICONTROL Regras]**.

1. Selecione **[!UICONTROL Criar Nova Regra]**.

1. Especifique um nome para a Regra. Por exemplo, Envio de formulário para registrar envios de formulário.

1. Na seção **[!UICONTROL Eventos]**, selecione **[!UICONTROL Adicionar]**.

1. Especifique **[!UICONTROL Adobe Experience Manager Forms]** como o nome da Extensão.

1. Selecione o tipo de evento. A entrada para o campo **[!UICONTROL Nome]** é preenchida automaticamente com base no tipo de evento selecionado.

1. Selecione **[!UICONTROL Manter alterações]** para salvar o evento.

1. Na seção **[!UICONTROL Actions]**, selecione **[!UICONTROL Add]**.

1. Especifique **[!UICONTROL Adobe Analytics]** como o nome da Extensão.

1. Selecione **[!UICONTROL Definir variáveis]** como o Tipo de ação. As opções disponíveis na lista suspensa incluem:

   * **[!UICONTROL Definir Variáveis]**: use este tipo de ação para definir o tipo de evento para o qual os elementos de dados selecionados são enviados do AEM Forms para [!DNL Adobe Analytics].

   * **[!UICONTROL Enviar sinal]**: use este tipo de ação para enviar dados do AEM Forms para [!DNL Adobe Analytics].

   * **[!UICONTROL Limpar Variáveis]**: use este tipo de ação para limpar a trilha de dados de forma que o evento seja registrado apenas uma vez em [!DNL Adobe Analytics].

     A abordagem recomendada é usar o tipo de ação **[!UICONTROL Definir Variáveis]** para configurar o evento e os elementos de dados, usar **[!UICONTROL Enviar Beacon]** para enviar dados e usar **[!UICONTROL Limpar Variáveis]** para limpar a trilha de dados.

1. Na seção **[!UICONTROL Props]**, mapeie as opções do conjunto de relatórios disponíveis na lista suspensa com os elementos de dados definidos com o uso de [Configurar elementos de dados](#configure-data-elements).

   Por exemplo, para enviar o elemento de dados **Título do formulário** do AEM Forms para [!DNL Adobe Analytics] quando você enviar um formulário:
   1. Na seção **[!UICONTROL Props]**, selecione uma prop para o Título do Formulário disponível no conjunto de relatórios e, em seguida, selecione ![Ícone do Banco de Dados](assets/database-icon.svg) para mapeá-lo para o Título do Formulário criado em [Configurar elementos de dados](#configure-data-elements).

      ![define-props](assets/define-props.png)

   1. Selecione **[!UICONTROL Adicionar Outro]** para adicionar mais elementos de dados à lista.

1. Na seção **[!UICONTROL Eventos]**, selecione um evento dentre as opções disponíveis no conjunto de relatórios e selecione **[!UICONTROL Manter alterações]**.

1. Na seção **[!UICONTROL Actions]**, selecione + e especifique **[!UICONTROL Adobe Analytics]** como o nome da Extensão.

1. Selecione **[!UICONTROL Enviar sinal]** como o Tipo de ação. No painel direito, selecione **[!UICONTROL s.t()]** para enviar dados a [!DNL Adobe Analytics] e tratá-los como um modo de exibição de página ou **[!UICONTROL s.tl()]** para enviar dados a [!DNL Adobe Analytics] e não tratá-los como um modo de exibição de página. Selecione **[!UICONTROL Manter alterações]**.

1. Na seção **[!UICONTROL Actions]**, selecione + e especifique **[!UICONTROL Adobe Analytics]** como o nome da Extensão.

1. Selecione **[!UICONTROL Limpar Variáveis]** como o Tipo de Ação. Selecione **[!UICONTROL Manter alterações]**. Depois de executar essas etapas, a seção **[!UICONTROL Ações]** é exibida como:
   ![Configuração de ações](assets/actions-config.png)

   Personalize a seção **[!UICONTROL Ações]** de acordo com suas necessidades. Por exemplo, você pode definir duas etapas **Enviar Beacon** em um Fluxo de ação para enviar dados para [!DNL Adobe Analytics] e tratá-los como uma exibição de página em uma etapa e enviar dados para [!DNL Adobe Analytics] e não tratá-los como uma exibição de página na segunda etapa.

   ![Configuração de ações](assets/actions-config-2.png)

1. Selecione **[!UICONTROL Salvar]** para salvar a regra.

   Você pode criar regras para todos os tipos de evento, como Abandonar, Erro, Visita de campo, Ajuda, Renderizar, Salvar e Enviar.

>[!VIDEO](https://video.tv.adobe.com/v/337425)


### Fluxos Publish {#publish-flow}

Depois de criar os elementos de dados e usá-los nas regras, publique a configuração para coletar dados de formulário no [!DNL Adobe Analytics].

Execute as seguintes etapas para publicar a configuração:

1. Na seção **[!UICONTROL Publicação]**, selecione **[!UICONTROL Fluxo de Publicação]**.

1. Selecione **[!UICONTROL Adicionar biblioteca]**, especifique um nome e selecione o ambiente para a biblioteca.

1. Selecione **[!UICONTROL Adicionar todos os recursos alterados]** e selecione **[!UICONTROL Salvar e criar no desenvolvimento]**.

1. Na seção **[!UICONTROL Desenvolvimento]**, selecione ![Mais opções](assets/more-options-icon.svg) e **[!UICONTROL Aprovar e Publish para produção]**.

1. Confirme se as alterações e o fluxo de publicação serão exibidos em breve na seção **[!UICONTROL Publicado]**.

![Fluxo do Publish](assets/publish-flow.png)

## 2. Configurar o AEM Forms {#configure-aem-forms}

Antes de criar uma configuração do Adobe Launch, crie uma [Configuração do Adobe IMS usando o Adobe Launch como a Solução da nuvem](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-launch/connect-aem-launch-adobe-io.html).

### Criar configuração do Adobe Launch {#create-adobe-launch-configuration}

Execute as seguintes etapas para criar uma configuração do Adobe Launch:

1. Na instância do Autor do AEM Forms, navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Configurações do Adobe Launch]**.

1. Selecione uma pasta para criar a configuração e selecione **[!UICONTROL Criar]**.

1. Especifique um título para a configuração no campo **[!UICONTROL Título]**.

1. Selecione a [configuração IMS da Adobe associada](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-launch/connect-aem-launch-adobe-io.html).

1. Selecione o nome da empresa usada durante a [configuração do Adobe Analytics](#Configure-adobe-analytics).

1. Selecione o nome da propriedade criada durante a [configuração do Adobe Analytics](#install-extensions).

1. Selecione **[!UICONTROL Salvar e fechar]**.

1. Publish da configuração.

### Habilitar [!DNL Adobe Analytics] para um formulário adaptável {#enable-analytics-adaptive-form}

Para usar a configuração [!DNL Adobe Launch] em um Formulário adaptável existente:

1. Na instância do Autor do AEM Forms, navegue até **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms e Documentos]**.
1. Selecione o Formulário adaptável e selecione **[!UICONTROL Propriedades]**.
1. Na guia **[!UICONTROL Básico]**, selecione o [contêiner de configuração](#create-adobe-launch-configuration) usado ao criar a configuração do Adobe Launch.
1. Selecione **[!UICONTROL Salvar e fechar]**. O Formulário adaptável está habilitado para [!DNL Adobe Analytics].
1. Publish o formulário.

Depois de habilitar [!DNL Adobe Analytics] para um formulário adaptável, você poderá [validar](https://experienceleague.adobe.com/docs/launch-learn/implementing-in-websites-with-launch/implement-solutions/analytics.html?lang=en#validate-the-page-view-beacon) se houver um fluxo de eventos de dados apropriado entre o AEM Forms e o [!DNL Adobe Analytics]. A integração do AEM Forms com o Adobe Analytics está concluída. Agora você pode [configurar e exibir relatórios no Adobe Analytics](#view-reports-adobe-analytics).

### Criar regras para capturar eventos personalizados (Opcional) {#capture-custom-events}

Crie regras em campos específicos de um formulário adaptável usando um editor de regras para enviar dados do Analytics de um formulário adaptável para [!DNL Adobe Analytics].

Em um processo de dois estágios, você define uma regra em um campo em um formulário adaptável. A regra despacha um evento. O nome do evento é mapeado para um evento de captura personalizado no Adobe Launch.

Para criar regras usando um editor de regras em um formulário adaptável:

1. Selecione o campo e selecione ![Editor de regras](assets/rule-editor-icon.svg) para abrir a página do editor de regras.
1. Defina uma condição na seção [!UICONTROL When] da regra.
1. Na seção [!UICONTROL Then] da regra, selecione **[!UICONTROL Evento de Despacho]** na lista suspensa **[!UICONTROL Selecionar Ação]**.
1. Especifique o nome do evento no campo **[!UICONTROL Digitar Nome do Evento]**.

Por exemplo, se a data de nascimento for anterior a uma determinada data, a AEM Forms enviará o evento **Segurança**.

![Evento de expedição](assets/security-event.png)

Para mapear o evento para um evento de captura personalizado em [!DNL Adobe Analytics]:

1. [Criar uma regra](#configure-rules).

1. Na seção **[!UICONTROL Eventos]**, selecione **[!UICONTROL Adicionar]**.

1. Especifique **[!UICONTROL Adobe Experience Manager Forms]** como o nome da Extensão.

1. Selecione **[!UICONTROL Capturar evento personalizado]** na lista suspensa **[!UICONTROL Tipo de evento]**.

1. Especifique o nome do evento especificado na etapa 4 ao criar uma regra usando o editor de regras.

1. Selecione **Manter Alterações** e execute o restante das ações especificadas em [Configurar Regras](#configure-rules).

## 3. Configurar e exibir relatórios em [!DNL Adobe Analytics] {#view-reports-adobe-analytics}

Depois de configurar um formulário adaptável para enviar dados do evento para o [!DNL Adobe Analytics], você pode começar a exibir relatórios em [!DNL Adobe Analytics]:

1. Selecione ![Selecionar Produto](assets/select-analytics.png) e **[!UICONTROL Analytics]**.

1. Selecione **[!UICONTROL Criar projeto]** e selecione **[!UICONTROL Projeto em branco]**.

1. Selecione o nome do conjunto de relatórios na lista suspensa na parte superior direita da forma livre.

1. Especifique o **Título do formulário** no texto dos **[!UICONTROL itens de dimensão de Pesquisa]** para exibir todos os títulos de formulário.

1. Solte o título do formulário adaptável para a caixa de texto **[!UICONTROL Solte um segmento aqui (ou qualquer outro componente)]**.

1. Na seção **[!UICONTROL Métricas]**, solte os eventos a serem rastreados na caixa de texto **[!UICONTROL Solte uma métrica aqui (ou qualquer outro componente)]**.

1. Selecione ![Visualizações](assets/visualization-icon.svg) e solte um tipo de gráfico na seção de Forma livre. Da mesma forma, você pode adicionar vários tipos de gráfico à seção Forma livre.

1. Selecione as teclas Ctrl + S e especifique um nome para salvar o projeto.

<!--

## Add AEM Forms and Adobe Analytics integration specific rules to Dispatcher {#forms-specific-rules-to-dispatcher}

Add AEM Forms and Adobe Analytics integration specific rules to filter the data traffic that is sent to the backend.

Perform the following steps to add AEM Forms and Adobe Analytics integration specific rules to Dispatcher for Experience Manager Forms as a Cloud Service:

1. Open your AEM Project and navigate to `\src\conf.dispatcher.d\filters`.
1. Open `filters.any` file for editing and add the following rule at the end of the file:

     ```json
     /00XX { /type "allow" /path "/content/forms/af/*" /method "POST" /selectors '(analyticsconfigparser)' /extension '(jsp|json)' }
     ```

1. Save and close the file.
1. Compile and deploy the project to your [!DNL AEM Forms] as a Cloud Service environment.



## Limitations {#limitations}

* Adobe Analytics can track form metrics only for authenticated users.

-->

>[!MORELIKETHIS]
>
>*[Habilitar o Adobe Analytics para um Formulário Adaptável](/help/forms/enable-adobe-analytics-adaptive-form-using-experience-cloud-setup-automation.md)