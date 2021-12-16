---
title: Como criar um portal do Forms em uma página do Experience Manager Sites?
description: Saiba como criar um Portal do Forms e usar componentes principais prontos para uso em uma página do AEM Sites.
source-git-commit: 4c42abfe2cc1b11aefb2b298e883406ca5c17fd2
workflow-type: tm+mt
source-wordcount: '1753'
ht-degree: 1%

---


# Listar Forms adaptável em um portal {#publish-forms-on-portal}

Em um cenário típico de implantação de portal centrado em formulários, o desenvolvimento de formulários e o desenvolvimento de portal são duas atividades disjuntas. Embora os designers de formulários criem e armazenem formulários em um repositório, os desenvolvedores da Web criam uma aplicação Web para listar formulários e lidar com o envio de formulários. Os Forms são copiados para a camada da Web, pois não há comunicação entre o repositório de formulários e o aplicativo da Web.

Tais cenários muitas vezes resultam em problemas de gerenciamento e atrasos de produção. Por exemplo, se houver uma versão mais recente de um formulário disponível no repositório, será necessário substituir o formulário na camada da Web, modificar a aplicação Web e reimplantar o formulário no site público. A reimplantação do aplicativo da Web pode causar algum tempo de inatividade do servidor. Normalmente, o tempo de inatividade do servidor é uma atividade planejada e, portanto, as alterações não podem ser enviadas para o site público instantaneamente.

A AEM Forms fornece componentes de portal que reduzem as despesas gerais de gerenciamento e os atrasos de produção. Os componentes fazem com que os desenvolvedores da Web criem e personalizem um portal do Forms em sites criados usando o Adobe Experience Manager (AEM).

Os componentes do Portal de formulários permitem adicionar a seguinte funcionalidade:

* Liste formulários em layouts personalizados. Pronto para uso, os layouts List view e Card view são fornecidos. Você pode criar seus próprios layouts personalizados.
* Permite que você exiba metadados personalizados e ações personalizadas ao listá-los.
* Formulários de lista publicados pela interface do usuário do AEM Forms na instância de publicação em que os componentes do Forms Portal estão sendo usados.
* Permitir que usuários finais renderizem formulários em formato HTML e PDF.
* Habilite a pesquisa de formulários com base no título e na descrição.
* Use o CSS personalizado para personalizar a aparência do portal.
* Criar links para formulários.
* Lista rascunhos e envios relacionados ao Adaptive Forms criado pelo usuário final.

## Componentes de uma página do Forms Portal {#forms-portal-components}

O AEM Forms fornece os seguintes componentes de portal prontos para uso:

* Pesquisar &amp; Lister: Esse componente permite listar formulários do repositório de formulários na página do portal e fornece opções de configuração para listar formulários com base em critérios especificados.

* Rascunhos e envios: Enquanto o componente Pesquisar e listar exibe formulários que são tornados públicos pelo autor do Forms, o componente Rascunhos e envios exibe formulários que são salvos como rascunho para preencher formulários posteriores e enviados. Esse componente fornece experiência personalizada para qualquer usuário conectado.

* Link: Esse componente permite criar um link para um formulário em qualquer lugar na página.

Você pode [importar os componentes prontos para uso do Forms Portal](#import-forms-portal-components-aem-archetype) do Arquétipo de projeto AEM. Após a importação, execute as seguintes configurações:
* [Configurar um armazenamento externo](#configure-azure-storage-adaptive-forms)
* [Ativar os componentes do Portal do Forms](#enable-forms-portal-components)
* [Configurar os componentes do Portal do Forms](#configure-forms-portal-components)

## Importar componentes do Forms Portal {#import-forms-portal-components-aem-archetype}

Para importar componentes prontos para uso do Forms Portal no AEM Forms as a Cloud Service, execute as seguintes etapas:

1. **Repositório Git do Clone Cloud Manager na instância de desenvolvimento local:**  O repositório Git do Cloud Manager contém um projeto de AEM padrão. É baseado em [Arquétipo de AEM](https://github.com/adobe/aem-project-archetype/). Clone seu Repositório Git do Cloud Manager usando o Gerenciamento de conta Git de autoatendimento da interface do usuário do Cloud Manager para trazer o projeto para o ambiente de desenvolvimento local. Para obter detalhes sobre como acessar o repositório, consulte [Acessar repositórios](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/accessing-repos.html).

1. **Criar [!DNL Experience Manager Forms] como [Cloud Service] projeto:** Criar [!DNL Experience Manager Forms] como [Cloud Service] projeto baseado em [Arquétipo de AEM 27](https://github.com/adobe/aem-project-archetype/releases/tag/aem-project-archetype-27) ou posterior. O arquétipo ajuda os desenvolvedores a começarem facilmente a desenvolver [!DNL AEM Forms] as a Cloud Service. Também inclui alguns temas e modelos de exemplo para ajudar você a começar rapidamente.

   Para criar [!DNL Experience Manager Forms] as a Cloud Service projeto, abra o prompt de comando e execute o comando abaixo. Para incluir [!DNL Forms] configurações, temas e modelos específicos, conjunto `includeForms=y`.

   ```shell
   mvn -B archetype:generate -DarchetypeGroupId=com.adobe.aem -DarchetypeArtifactId=aem-project-archetype -DarchetypeVersion=30 -DaemVersion="cloud" -DappTitle="My Site" -DappId="mysite" -DgroupId="com.mysite" -DincludeForms="y"
   ```

   Além disso, altere `appTitle`, `appId`e `groupId`, no comando acima para refletir seu ambiente.

1. **Implante o projeto no ambiente de desenvolvimento local:** Você pode usar o seguinte comando para implantar em seu ambiente de desenvolvimento local

   `mvn -PautoInstallPackage clean install`

   Para obter a lista completa de comandos, consulte [Criação e instalação](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/using.html?lang=en#building-and-installing)

1. [Incluir os artefatos do componente principal](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure.html#embeddeds) e a dependência como se segue:

   ```shell
   <dependency>
               <groupId>com.adobe.aem</groupId>
               <artifactId>{TBD}</artifactId>
               <type>content-package</type>
               <version>{TBD}</version>
   </dependency>
   ```

1. [Implante o código no [!DNL AEM Forms] Ambiente as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure.html#embeddeds).


## Configurar o Armazenamento do Azure para Forms adaptável {#configure-azure-storage-adaptive-forms}

[[!DNL Experience Manager Forms] Integração de dados](data-integration.md) forneça [!DNL Azure] configuração de armazenamento para integrar formulários com o [!DNL Azure] serviços de armazenamento. O Modelo de dados de formulário pode ser usado para criar um Forms adaptável que interage com o [!DNL Azure] para ativar workflows de negócios.

### Criar configuração de armazenamento do Azure {#create-azure-storage-configuration}

Antes de executar essas etapas, verifique se você tem uma [!DNL Azure] conta de armazenamento e uma chave de acesso para autorizar o acesso ao [!DNL Azure] conta de armazenamento.

1. Navegar para **[!UICONTROL Ferramentas]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Armazenamento do Azure]**.
1. Selecione uma pasta para criar a configuração e toque em **[!UICONTROL Criar]**.
1. Especifique um título para a configuração no **[!UICONTROL Título]** campo.
1. Especifique o nome da variável [!DNL Azure] conta de armazenamento na **[!UICONTROL Conta de Armazenamento do Azure]** campo.

### Configurar o Conector de Armazenamento Unificado para Forms Portal {#configure-usc-forms-portal}

Execute as seguintes etapas para configurar o Unified Storage Connector para AEM Workflows:

1. Navegar para **[!UICONTROL Ferramentas]** > **[!UICONTROL Forms]** > **[!UICONTROL Conector de armazenamento unificado]**.
1. No **[!UICONTROL Forms Portal]** seção , selecione **[!UICONTROL Azure]** do **[!UICONTROL Armazenamento]** lista suspensa.
1. Especifique a [caminho de configuração para a configuração de armazenamento do Azure](#create-azure-storage-configuration) no **[!UICONTROL Caminho de configuração de armazenamento]** campo.
1. Toque **[!UICONTROL Publicar]** em seguida, toque em **[!UICONTROL Salvar]** para salvar a configuração.

## Ativar componentes do Forms Portal {#enable-forms-portal-components}

Para usar qualquer componente principal (incluindo os componentes prontos para uso do portal) em um site do Adobe Experience Manager (AEM), você deve criar um componente proxy e ativá-lo para o site. Para criar um componente proxy e ativar componentes do portal, consulte [Uso dos componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/using.html?lang=en#create-proxy-components).

Depois que um componente de portal é ativado, você pode usá-lo na instância do autor da página de sites.

## Adicionar e configurar componentes do Forms Portal {#configure-forms-portal-components}

Você pode criar e personalizar o Forms Portal em sites criados usando AEM adicionando e configurando os componentes do portal. Certifique-se de que [componentes ativados](#enable-forms-portal-components) antes de usá-los no Portal do Forms.

Para adicionar um componente, arraste e solte o componente do painel Componentes no contêiner de layout da página ou toque no ícone adicionar no contêiner de layout e adicione o componente do [!UICONTROL Inserir novo componente] caixa de diálogo.

### Componente Configurar rascunhos e envios {#configure-drafts-submissions-component}

O componente Rascunhos e envios exibe formulários que são salvos como rascunho para preencher formulários posteriores e enviados. Para configurar, toque no componente e toque no ![Ícone Configurar](assets/configure_icon.png). No [!UICONTROL Rascunhos e envios] , especifique o título para indicar a listagem do formulário como rascunho ou formulários enviados. Selecione também se o componente deve listar formulários de rascunho ou formulários enviados no formato de cartão ou lista.

![Ícone Rascunhos](assets/drafts-component.png)

![Ícone Submissões](assets/submission-listing.png)

### Configurar Componente de Pesquisa e Lister {#configure-search-lister-component}

O componente Pesquisar e listar é usado para listar formulários adaptáveis em uma página e implementar a pesquisa nos formulários listados.

![Ícone Pesquisa e Lister](assets/search-and-lister-component.png)

Para configurar, toque no componente e toque no ![Ícone Configurar](assets/configure_icon.png). O [!UICONTROL Pesquisar e Lister] será aberta.

1. No [!UICONTROL Exibir] , configure o seguinte:
   * Em **[!UICONTROL Título]**, especifique o título do componente Pesquisar e listar . Um título indicativo permite que os usuários façam uma pesquisa rápida na lista de formulários.
   * No **[!UICONTROL Layout]** selecione o layout para representar os formulários no formato de cartão ou de lista.
   * Selecionar **[!UICONTROL Ocultar pesquisa]** e **[!UICONTROL Ocultar Classificação]** para ocultar a pesquisa e classificar por recursos.
   * Em **[!UICONTROL Dica de ferramenta]**, forneça a dica de ferramenta exibida ao passar o mouse sobre o componente.
1. No [!UICONTROL Pasta de ativos] , especifique o local de onde os formulários são extraídos e listados na página. Você pode configurar vários locais de pastas.
1. No [!UICONTROL Resultados] , configure o número máximo de formulários a serem exibidos por página. O padrão é oito formulários por página.

### Configurar componente de link {#configure-link-component}

O componente de link permite que você forneça links para um formulário adaptável na página. Para configurar, toque no componente e toque no ![Ícone Configurar](assets/configure_icon.png). O [!UICONTROL Editar componente de link] será aberta.

1. No [!UICONTROL Exibir] , forneça a legenda do link e a dica de ferramenta para facilitar a identificação dos formulários representados pelo link.
1. No [!UICONTROL Informações do ativo] , especifique o caminho do repositório onde o ativo está armazenado.
1. No [!UICONTROL Params de Consulta] , especifique os parâmetros adicionais no formato do par de valores chave. Quando o link é clicado, esses parâmetros adicionais e são transmitidos com o formulário.

## Configurar o envio assíncrono de formulário usando o Adobe Sign {#configure-asynchronous-form-submission-using-adobe-sign}

Você pode configurar para enviar um formulário adaptável somente quando todos os recipients tiverem concluído a cerimônia de assinatura. Siga as etapas abaixo para definir a configuração usando o Adobe Sign.

1. Na instância do autor, abra um Formulário adaptável no modo de edição.
1. No painel esquerdo, toque no ícone Propriedades e expanda o **[!UICONTROL ASSINATURA ELETRÔNICA]** opção.
1. Selecionar **[!UICONTROL Ativar o Adobe Sign]**. Várias opções de configuração são exibidas.
1. No [!UICONTROL Enviar o formulário] selecione a **[!UICONTROL depois que cada recipient concluir a cerimônia de assinatura]** para configurar a ação Enviar formulário, onde o formulário é enviado pela primeira vez para todos os destinatários para assinatura. Depois que todos os recipients assinarem o formulário, somente o formulário será enviado.

## Salvar Forms Adaptável Como Rascunhos {#save-adaptive-forms-as-drafts}

Você pode salvar formulários como rascunhos para completá-los posteriormente. Há duas maneiras de salvar um formulário como rascunho:
* Crie uma regra &quot;Salvar formulário&quot; em um componente de formulário, por exemplo, um botão. Ao clicar no botão , a regra é acionada e o formulário é salvo em um rascunho.
* Ative o recurso Salvar automaticamente, que salva o formulário de acordo com o evento especificado ou após um intervalo de tempo configurado.

### Criar regras para salvar um formulário adaptável como rascunho {#rule-to-save-adaptive-form-as-draft}

Para criar uma regra &quot;Salvar formulário&quot; em um componente de formulário, por exemplo, um botão, siga as etapas abaixo:

1. Na instância do autor, abra um Formulário adaptável no modo de edição.
1. No painel esquerdo, toque em ![Ícone Componentes](assets/components_icon.png) e arraste a [!UICONTROL Botão] ao formulário.
1. Toque no [!UICONTROL Botão] e toque no componente ![Ícone Configurar](assets/configure_icon.png).
1. Toque no [!UICONTROL Editar regras] para abrir o Editor de regras.
1. Toque **[!UICONTROL Criar]** para configurar e criar a regra.
1. No [!UICONTROL When] selecione &quot;is clicked&quot; e, na seção [!UICONTROL Então] selecione a opção &quot;Salvar formulário&quot;.
1. Toque **[!UICONTROL Concluído]** para salvar a regra.

### Ativar gravação automática {#enable-auto-save}

Você pode configurar o recurso de salvamento automático para um formulário adaptável da seguinte maneira:

1. Na instância do autor, abra um Formulário adaptável no modo de edição.
1. No painel esquerdo, toque no ![Ícone Propriedades](assets/configure_icon.png) e amplie o [!UICONTROL SALVAR AUTOMATICAMENTE] opção.
1. Selecione o **[!UICONTROL Habilitar]** para ativar o salvamento automático do formulário. É possível configurar os seguintes itens:
* Por padrão, a variável [!UICONTROL Evento de formulário adaptável] é definido como &quot;true&quot;, o que significa que o formulário é salvo automaticamente após cada evento.
* Em [!UICONTROL Acionador], configure para acionar o salvamento automático com base na ocorrência de um evento ou após um intervalo de tempo específico.
