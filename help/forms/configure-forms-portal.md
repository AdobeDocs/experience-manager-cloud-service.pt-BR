---
title: Como criar um Portal do Forms em uma página do Experience Manager Sites?
description: Saiba como criar um Portal do Forms e usar componentes principais prontos para uso em uma página do AEM Sites.
exl-id: 13cfe3ba-2e85-46bf-a029-2673de69c626
source-git-commit: 2d4ffd5518d671a55e45a1ab6f1fc41ac021fd80
workflow-type: tm+mt
source-wordcount: '1785'
ht-degree: 1%

---

# Adicionar o Forms Portal a uma página do AEM Sites {#publish-forms-on-portal}

<span class="preview"> O Adobe recomenda o uso da captura de dados moderna e extensível [Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=pt-BR) para [criação de um novo Forms adaptável](/help/forms/creating-adaptive-form-core-components.md) ou [adição de Forms adaptável às páginas do AEM Sites](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md). Esses componentes representam um avanço significativo na criação do Forms adaptável, garantindo experiências de usuário impressionantes. Este artigo descreve a abordagem mais antiga para criar o Forms adaptável usando componentes de base. </span>

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/publish-process-aem-forms/introduction-publishing-forms.html) |
| AEM as a Cloud Service | Este artigo |

Em um cenário típico de implantação de portal centrada em formulários, o desenvolvimento de formulários e o desenvolvimento de portal são duas atividades distintas. Enquanto os designers de formulários criam e armazenam formulários em um repositório, os desenvolvedores da Web criam um aplicativo da Web para listar formulários e manipular o envio de formulários. Os Forms são copiados para o nível da Web, pois não há comunicação entre o repositório de formulários e o aplicativo web.

Esses cenários geralmente resultam em problemas de gerenciamento e atrasos de produção. Por exemplo, se houver uma versão mais recente de um formulário disponível no repositório, você precisará substituir o formulário no nível da Web, modificar o aplicativo da Web e reimplantar o formulário no site público. A reimplantação do aplicativo Web pode causar algum tempo de inatividade do servidor. Normalmente, o tempo de inatividade do servidor é uma atividade planejada e, portanto, as alterações não podem ser enviadas para o site público instantaneamente.

A AEM Forms fornece componentes de portal que reduzem as despesas gerais de gerenciamento e os atrasos de produção. Os componentes equipam os desenvolvedores da Web para criar e personalizar um Forms Portal em sites criados usando o Adobe Experience Manager (AEM).

Os componentes do Portal de formulários permitem adicionar a seguinte funcionalidade:

* Listar formulários em layouts personalizados. Pronto para uso, são fornecidos a Exibição de lista e os Layouts de exibição de cartão. Você pode criar seus próprios layouts personalizados.
* Permite exibir metadados personalizados e ações personalizadas ao listá-los.
* Listar formulários publicados pela interface do usuário do AEM Forms na instância de publicação em que os componentes do Forms Portal estão sendo usados.
* Permitir que os usuários finais renderizem formulários no formato HTML e PDF.
* Habilitar a pesquisa de formulários com base no título e na descrição.
* Use o CSS personalizado para personalizar a aparência do portal.
* Criar links para formulários.
* Lista rascunhos e envios relacionados ao Adaptive Forms criados pelo usuário.

## Componentes de uma página do Forms Portal {#forms-portal-components}

A AEM Forms fornece os seguintes componentes do portal prontos para uso:

* Pesquisar e listar: este componente permite listar formulários do repositório de formulários na página do portal e fornece opções de configuração para listar formulários com base em critérios especificados.

* Rascunhos e envios: enquanto o componente Pesquisa e listagem exibe formulários que são tornados públicos pelo autor do Forms, o componente Rascunhos e envios exibe formulários que são salvos como rascunho para concluir e enviar formulários posteriormente. Este componente fornece experiência personalizada para qualquer usuário conectado.

* Link: este componente permite criar um link para um formulário em qualquer lugar da página.

Você pode [importar os componentes prontos para uso do Forms Portal](#import-forms-portal-components-aem-archetype) do Arquétipo de projeto AEM. Após a importação, execute as seguintes configurações:

* [Configurar um armazenamento externo](#configure-azure-storage-adaptive-forms)

* [Habilitar os componentes do Portal do Forms](#enable-forms-portal-components)

* [Configurar os componentes do Forms Portal](#configure-forms-portal-components)

## Importar componentes do portal do Forms {#import-forms-portal-components-aem-archetype}

Para importar componentes prontos para uso do Forms Portal no AEM Forms as a Cloud Service, execute as seguintes etapas:

1. **Clonar o repositório Git do Cloud Manager na instância de desenvolvimento local:**  Seu repositório Git do Cloud Manager contém um projeto AEM padrão. Baseia-se no [Arquétipo AEM](https://github.com/adobe/aem-project-archetype/). Clonar o Repositório Git do Cloud Manager usando o Gerenciamento de conta Git por autoatendimento da interface do usuário do Cloud Manager para trazer o projeto para o ambiente de desenvolvimento local. Para obter detalhes sobre o acesso ao repositório, consulte [Acessar repositórios](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/accessing-repos.html).

1. **Criar [!DNL Experience Manager Forms] as a [Cloud Service] projeto:** Criar [!DNL Experience Manager Forms] as a [Cloud Service] projeto baseado em [Arquétipo AEM 27](https://github.com/adobe/aem-project-archetype/releases/tag/aem-project-archetype-27) ou posteriormente. O arquétipo ajuda os desenvolvedores a iniciar o desenvolvimento facilmente para [!DNL AEM Forms] as a Cloud Service. Ele também inclui alguns exemplos de temas e modelos para ajudá-lo a começar rapidamente.

   Para criar [!DNL Experience Manager Forms] as a Cloud Service projeto, abra o prompt de comando e execute o comando abaixo. Para incluir [!DNL Forms] configurações, temas e modelos específicos, definir `includeForms=y`.

   ```shell
   mvn -B archetype:generate -DarchetypeGroupId=com.adobe.aem -DarchetypeArtifactId=aem-project-archetype -DarchetypeVersion=30 -DaemVersion="cloud" -DappTitle="My Site" -DappId="mysite" -DgroupId="com.mysite" -DincludeForms="y"
   ```

   Além disso, altere `appTitle`, `appId`, e `groupId`, no comando acima para refletir o ambiente.

   Quando o projeto estiver pronto, atualize o `<core.forms.components.version>x.y.z</core.forms.components.version>` propriedade no nível superior `pom.xml` do projeto Arquétipo para refletir a versão mais recente do [core-forms-components](https://github.com/adobe/aem-core-forms-components) no seu `AEM Archetype` projeto.

1. **Implante o projeto no seu ambiente de desenvolvimento local:** Você pode usar o comando a seguir para implantar no ambiente de desenvolvimento local

   `mvn -PautoInstallPackage clean install`

   Para obter a lista completa de comandos, consulte [Criação e instalação](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/using.html?lang=en#building-and-installing)

1. [Implante o código no seu [!DNL AEM Forms] ambiente as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure.html#embeddeds).


## Configurar o armazenamento do Azure para o Adaptive Forms {#configure-azure-storage-adaptive-forms}

[[!DNL Experience Manager Forms] Integração de dados](data-integration.md) fornece [!DNL Azure] configuração de armazenamento para integrar formulários com o [!DNL Azure] serviços de armazenamento. O modelo de dados de formulário pode ser usado para criar o Forms adaptável que interage com o [!DNL Azure] servidor para habilitar workflows de negócios.

### Criar configuração de armazenamento do Azure {#create-azure-storage-configuration}

Antes de executar essas etapas, verifique se você tem uma conta de armazenamento do Azure e uma chave de acesso para autorizar o acesso ao [!DNL Azure] conta de armazenamento.

1. Navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Armazenamento do Azure]**.
1. Selecione uma pasta para criar a configuração e selecione **[!UICONTROL Criar]**.
1. Especifique um título para a configuração no campo **[!UICONTROL Título]** campo.
1. Especifique o nome do [!DNL Azure] conta de armazenamento na **[!UICONTROL Conta de armazenamento do Azure]** campo.

### Configurar o Conector de armazenamento unificado para o Forms Portal {#configure-usc-forms-portal}

Execute as seguintes etapas para configurar o Conector de armazenamento unificado para fluxos de trabalho AEM:

1. Navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Forms]** > **[!UICONTROL Conector de armazenamento unificado]**.
1. No **[!UICONTROL Portal Forms]** , selecione **[!UICONTROL Azure]** do **[!UICONTROL Armazenamento]** lista suspensa.
1. Especifique a [caminho de configuração para a configuração de armazenamento do Azure](#create-azure-storage-configuration) no **[!UICONTROL Caminho de configuração de armazenamento]** campo.
1. Selecionar **[!UICONTROL Publish]** e selecione **[!UICONTROL Salvar]** para salvar a configuração.

## Habilitar Componentes do Portal Forms {#enable-forms-portal-components}

Para usar qualquer componente principal (incluindo os componentes de portal prontos para uso) em um site do Adobe Experience Manager (AEM), você deve criar um componente proxy e habilitá-lo para o seu site. Para criar um componente proxy e ativar componentes do portal, consulte [Uso de Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/using.html?lang=en#create-proxy-components).

Depois que um componente de portal é ativado, você pode usá-lo na instância de autor da página de sites.

## Adicionar e configurar componentes do portal do Forms {#configure-forms-portal-components}

Você pode criar e personalizar o Forms Portal em sites criados usando AEM adicionando e configurando os componentes do portal. Certifique-se de que o [os componentes estão ativados](#enable-forms-portal-components) antes de usá-los no Forms Portal.

Para adicionar um componente, arraste e solte o componente do painel Componentes no contêiner de layout da página ou selecione o ícone adicionar no contêiner de layout e adicione o componente da [!UICONTROL Inserir novo componente] diálogo.

### Configurar o componente de rascunhos e envios {#configure-drafts-submissions-component}

O componente Rascunhos e envios exibe formulários que são salvos como rascunho para preencher formulários posteriormente e enviados. Para configurar, selecione o componente e selecione a variável ![Ícone Configurar](assets/configure_icon.png). No [!UICONTROL Rascunhos e envios] especifique o título para indicar a lista de formulários como rascunho ou formulários enviados. Selecione também se o componente deve listar formulários de rascunho ou formulários enviados no formato de cartão ou lista.

![Ícone Rascunhos](assets/drafts-component.png)

![Ícone Envios](assets/submission-listing.png)

### Configurar o componente de pesquisa e listagem {#configure-search-lister-component}

O componente de Pesquisa e listagem é usado para listar formulários adaptáveis em uma página e implementar a pesquisa nos formulários listados.

![Ícone Pesquisar e Lister](assets/search-and-lister-component.png)

Para configurar, selecione o componente e selecione a variável ![Ícone Configurar](assets/configure_icon.png). A variável [!UICONTROL Pesquisa e Lister] será aberta.

1. No [!UICONTROL Exibir] , configure o seguinte:
   * Entrada **[!UICONTROL Título]**, especifique o título para o componente de Pesquisa e Lister. Um título indicativo permite que os usuários executem uma pesquisa rápida na lista de formulários.
   * No **[!UICONTROL Layout]** selecione o layout para representar os formulários no formato de cartão ou lista.
   * Selecionar **[!UICONTROL Ocultar pesquisa]** e **[!UICONTROL Ocultar classificação]** para ocultar a pesquisa e classificar por recursos.
   * Entrada **[!UICONTROL Dica de ferramenta]**, fornecem a dica de ferramenta que aparece quando você passa o mouse sobre o componente.
1. No [!UICONTROL Pasta de ativos] especifique o local de onde os formulários são extraídos e listados na página. Você pode configurar vários locais de pastas.
1. No [!UICONTROL Resultados] , configure o número máximo de formulários a serem exibidos por página. O padrão é oito formulários por página.

### Configurar o componente de link {#configure-link-component}

O componente Link permite fornecer links para um formulário adaptável na página. Para configurar, selecione o componente e selecione a variável ![Ícone Configurar](assets/configure_icon.png). A variável [!UICONTROL Editar componente do link] será aberta.

1. No [!UICONTROL Exibir] , forneça a legenda do link e a dica de ferramenta para facilitar a identificação dos formulários representados pelo link.
1. No [!UICONTROL Informações do ativo] especifique o caminho do repositório onde o ativo está armazenado.
1. No [!UICONTROL Parâmetros de consulta] especifique os parâmetros adicionais no formato do par de valores chave. Quando o link for clicado, esses parâmetros adicionais serão transmitidos junto com o formulário.

## Configurar o envio assíncrono de formulários usando o Adobe Sign {#configure-asynchronous-form-submission-using-adobe-sign}

Você pode configurar o para enviar um formulário adaptável somente quando todos os recipients tiverem concluído a cerimônia de assinatura. Siga as etapas abaixo para definir a configuração usando o Adobe Sign.

1. Na instância do autor, abra um Formulário adaptável no modo de edição.
1. No painel esquerdo, selecione o ícone Propriedades e expanda a janela **[!UICONTROL ASSINATURA ELETRÔNICA]** opção.
1. Selecionar **[!UICONTROL Ativar o Adobe Sign]**. Várias opções de configuração são exibidas.
1. No [!UICONTROL Enviar o formulário] , selecione a **[!UICONTROL depois que cada recipient concluir a cerimônia de assinatura]** opção para configurar a ação Enviar formulário, onde o formulário é enviado pela primeira vez a todos os recipients para assinatura. Depois que todos os recipients tiverem assinado o formulário, somente então o formulário será enviado.

## Salvar Forms Adaptável Como Rascunhos {#save-adaptive-forms-as-drafts}

Você pode salvar formulários como rascunhos para preenchê-los posteriormente. Há duas maneiras pelas quais um formulário é salvo como rascunho:

* Crie uma regra &quot;Salvar formulário&quot; em um componente de formulário, por exemplo, um botão. Ao clicar no botão, os acionadores da regra e o formulário são salvos como rascunho.
* Habilite o recurso de Salvamento automático, que salva o formulário de acordo com o evento especificado ou após um intervalo configurado de tempo.

### Criar regras para salvar um formulário adaptável como rascunho {#rule-to-save-adaptive-form-as-draft}

Para criar uma regra &quot;Salvar formulário&quot; em um componente de formulário, por exemplo, um botão, siga as etapas abaixo:

1. Na instância do autor, abra um Formulário adaptável no modo de edição.
1. No painel esquerdo, selecione ![Ícone Componentes](assets/components_icon.png) e arraste o [!UICONTROL Botão] componente ao formulário.
1. Selecione o [!UICONTROL Botão] e selecione o ![Ícone Configurar](assets/configure_icon.png).
1. Selecione o [!UICONTROL Editar regras] ícone para abrir o Editor de regras.
1. Selecionar **[!UICONTROL Criar]** para configurar e criar a regra.
1. No [!UICONTROL Quando] selecione &quot;está clicado&quot; e na caixa [!UICONTROL Depois] selecione as opções &quot;Salvar formulário&quot;.
1. Selecionar **[!UICONTROL Concluído]** para salvar a regra.

### Ativar salvamento automático {#enable-auto-save}

Você pode configurar o recurso de salvamento automático para um formulário adaptável da seguinte maneira:

1. Na instância do autor, abra um Formulário adaptável no modo de edição.
1. No painel esquerdo, selecione a ![Ícone Propriedades](assets/configure_icon.png) e expanda a variável [!UICONTROL SALVAMENTO AUTOMÁTICO] opção.
1. Selecione o **[!UICONTROL Ativar]** para ativar o salvamento automático do formulário. Você pode configurar o seguinte:
* Por padrão, a variável [!UICONTROL Evento de formulário adaptável] está definido como &quot;true&quot;, o que implica que o formulário é salvo automaticamente após cada evento.
* Entrada [!UICONTROL Acionador], configure o para acionar o salvamento automático com base na ocorrência de um evento ou após um intervalo de tempo específico.

## Consulte também {#see-also}

{{see-also}}



<!--

>[!MORELIKETHIS]
>
>* [Configure data sources for AEM Forms](/help/forms/configure-data-sources.md)
>* [Configure Azure storage for AEM Forms](/help/forms/configure-azure-storage.md)
>* [Integrate Microsoft Dynamics 365 and Salesforce with Adaptive Forms](/help/forms/configure-msdynamics-salesforce.md)

-->