---
title: Saiba mais sobre as noções básicas de criação
description: Saiba mais sobre os conceitos e os mecanismos de criação de conteúdo para seu CMS headless usando Fragmentos de conteúdo.
exl-id: 3eca973f-b210-41bb-98da-ecbd2bae9803
source-git-commit: 60ddcb3f2fd2219b0b1672791703582920825e81
workflow-type: ht
source-wordcount: '1668'
ht-degree: 100%

---

# Noções básicas de criação para headless com AEM {#author-headless-basics}

## A história até agora {#story-so-far}

No início da [Jornada do autor de conteúdo headless do AEM](overview.md), a [Introdução](introduction.md) abordou os conceitos básicos e a terminologia relevante para a criação de conteúdo headless.

Este artigo se baseia nessas noções para que você entenda como criar seu próprio conteúdo para o seu projeto headless do AEM.

## Objetivo {#objective}

* **Público-alvo**: iniciante
* **Objetivo**: apresentar as noções básicas da criação de CMS headless:
   * Introdução à criação com o AEMaaCS
   * Introdução aos Fragmentos de conteúdo

## Manuseio básico {#basic-handling}

Antes de lidar com os Fragmentos de conteúdo, veja uma introdução (muito) rápida ao uso do AEM....mas nada substitui a experiência de entrar e tentar usar o sistema.

### Criação e publicação {#author-preview-publish}

Uma instalação do AEM geralmente consiste em pelo menos dois ambientes:

* Autor
* Publicação

Você faz logon e usa o ambiente de criação para gerar o seu conteúdo. Quando estiver pronto, publique seu conteúdo para que ele fique disponível. Para headless, isso seria para outros aplicativos, para páginas da Web, isso seria para os leitores na Web.

Para obter mais detalhes, consulte os Conceitos de criação.

### Fazer logon {#signing-in}

Assim como na maioria dos sistemas, você precisará fazer logon. Como autor, você receberá:

* Nome do usuário (conta)
* Senha
* Link para acessar a tela de logon

Sua conta já terá sido configurada com os privilégios necessários. Em caso de problemas, recomendamos que você entre em contato com a equipe interna de suporte a projetos.

### Navegação {#navigation}

A primeira vez que você efetuar o logon, um pequeno tutorial online destacará alguns dos principais recursos da interface.

Em seguida, você pode usar o Painel de navegação para acessar as áreas-chave do AEM. Para Fragmentos de conteúdo, você usará o console de **Fragmentos de conteúdo** (para algumas ações, você também usará o console **Ativos**).

O Painel de navegação pode ser aberto selecionando o ícone da Adobe na parte superior esquerda, seguido pelo ícone de uma pequena bússola.

<!--
The Navigation Panel can be opened by selecting Adobe icon at the top left, followed by the small compass icon:

![Navigation panel](/help/journey-headless/author/assets/headless-journey-author-navigation-01.png)
-->

>[!NOTE]
>Embora os Fragmentos de conteúdo sejam um recurso do AEM **Sites**, eles são salvos como **Ativos**. Este é um detalhe técnico que não deve afetar você, mas que pode ser útil.

No console, é possível selecionar pastas no painel esquerdo para navegar até o seu Fragmento de conteúdo. Também é possível filtrar e/ou pesquisar.

![Console de Fragmentos de conteúdo](/help/sites-cloud/administering/content-fragments/assets/cfc-console-filter.png)

### Ações, Seleção, Exibição {#actions-selecting-viewing}

No console de **Fragmentos de conteúdo**, várias ações estão disponíveis para seus fragmentos de conteúdo na barra de ferramentas:

<!-- ![Console actions](assets/cfm-managing-cf-console-01.png) -->

* **Abrir no Assets**
* **Criar**
* A coluna **Referenciado por** também fornece um link direto para mostrar todas as referências principais desse fragmento, incluindo a referência a fragmentos de conteúdo, fragmentos de experiência e páginas.
* Passar o mouse sobre o nome da pasta mostrará o caminho JCR.

Após a seleção do fragmento, todas as ações apropriadas estarão disponíveis:

<!-- ![Console actions - fragment selected](assets/cfm-managing-cf-console-selected-01.png) -->

* **Abrir**
* **Publicar** (e **Desfazer publicação**)
* **Copiar**
* **Mover**
* **Renomeie**
* **Excluir**

>[!NOTE]
>
>Ações como Publicar, Desfazer publicação, Excluir, Mover, Renomear e Copiar acionam um processo assíncrono. O progresso desse processo pode ser monitorado por meio da interface de processos assíncronos do AEM.

<!--
The **Assets** console has dedicated **Action Toolbars**, and **Quick Actions** that you can use after selecting a resource (for example, a folder or content fragment).

The Quick Actions are available for a single resource, see **Basel** in the example below:

![Quick Actions](/help/journey-headless/author/assets/headless-journey-author-navigation-05.png)

The Actions Toolbar provides access to the full range of actions - applicable for the current scenario. The actions available can change; for example, dependent on your location, or whether you have selected multiple resources:

![Action Toolbar](/help/journey-headless/author/assets/headless-journey-author-navigation-06.png)

You can select the format for viewing your resources with the View Selector:

![View Selector](/help/journey-headless/author/assets/headless-journey-author-navigation-03.png)

You can view additional information about items using the Rail Selector. This also gives access to additional actions.

![Left Rail](/help/journey-headless/author/assets/headless-journey-author-navigation-04.png)
-->

## Criação de fragmentos de conteúdo {#authoring-content-fragments}

Então, essa foi uma introdução bem rápida à interface do AEM, mas espero que você tenha tido uma chance de experimentá-la. Agora, chegamos ao seu verdadeiro interesse: Fragmentos de conteúdo para headless.

Teremos que passar pelas coisas do início ao fim, mas sua instância já pode ter pastas e/ou fragmentos criados, e eles podem estar em locais diferentes. Os princípios são os mesmos.

### Organização e navegação {#organizing-and-navigating}

A menos que tenha pouquíssimos Fragmentos de conteúdo, você vai querer organizá-los - para que você (e outros) possam encontrá-los novamente.

#### Criação de pastas {#creating-folder}

Você pode fazer isso criando uma série de pastas na seção **Arquivos** do console **Ativos**. Selecione a opção **Criar** (parte superior direita), seguido por **Pasta**:

![Opção Criar pasta](/help/journey-headless/author/assets/headless-journey-author-folder-01.png)

Uma caixa de diálogo será aberta em que você pode inserir os detalhes e, em seguida, confirmar clicando em **Criar**:

![Caixa de diálogo Criar pasta](/help/journey-headless/author/assets/headless-journey-author-folder-02.png)

#### Uso de caminhos e tags para limitar os Modelos de fragmentos de conteúdo disponíveis na pasta {#tags-paths-for-models-in-folder}

Esta seção é um pouco mais avançada. Você realmente não precisa dela se você está começando e apenas testando as coisas, mas é *muito* útil quando você tem muitos fragmentos. Por isso é bom saber - mesmo que ainda não o utilize.

Seu Arquiteto de conteúdo terá criado todos os Modelos de fragmentos de conteúdo necessários para seu projeto atual e talvez alguns outros projetos também. Para ajudar a simplificar as coisas para você mesmo e para outros autores, você pode limitar a lista de modelos disponíveis para uma pasta específica.

Depois de criar a pasta, você pode abrir suas **Propriedades**. Aqui estão várias guias com informações e detalhes de configuração sobre a pasta. Especificamente para Fragmentos de conteúdo, você pode usar a guia **Políticas** para definir caminhos e/ou tags específicas para a pasta. Isso limita os Modelos de fragmentos do conteúdo disponíveis para uso na pasta, pois significa que eles devem atender a esses critérios antes que possam ser usados para gerar fragmentos nessa pasta.

![Criar propriedades de pasta - Políticas](/help/journey-headless/author/assets/headless-journey-author-folder-04.png)

>[!NOTE]
>
>Você pode ler mais detalhes em Modelos de fragmentos do conteúdo - Permitir Modelos de fragmentos do conteúdo na pasta de ativos.

Em seguida, navegue por essas pastas para criar e editar os Fragmentos de conteúdo.

#### Por segurança - Configuração dos serviços de pasta na nuvem  {#cloud-services-folder}

Por segurança...

Você provavelmente receberá uma pasta inicial em que poderá criar suas pastas. Isso ocorre porque alguns detalhes de configuração devem ser aplicados (geralmente por um Desenvolvedor ou Administrador do Sistema) à pasta raiz. Isso provavelmente não lhe interessará, mas, se necessário, você poderá verificar a **Configuração** nos **Serviços na nuvem** da pasta **Propriedades**:

![Criar propriedades de pasta - Configuração](/help/journey-headless/author/assets/headless-journey-author-folder-03.png)

>[!NOTE]
>
>Você pode ler mais em Aplicar a configuração à sua pasta de Ativos.

### Criação de um Fragmento de conteúdo {#creating-fragment}

No console de **Fragmentos de conteúdo**, você pode usar **Criar** para abrir a caixa de diálogo **Novo fragmento de conteúdo**:

![Console de Fragmentos de conteúdo - Criar um novo fragmento](/help/sites-cloud/administering/content-fragments/assets/cfc-console-create.png)

Especifique o:

* **Local**
* **Modelo de Fragmentos do conteúdo**
* **Título**
* **Nome**
* **Descrição**

Em seguida, confirme com **Criar** ou **Criar e abrir**.

<!--
Creating a Content Fragment is very similar - you just use the **Content Fragment** option instead:

![Create Content Fragment option](/help/journey-headless/author/assets/headless-journey-author-content-fragment-01.png)

This time a wizard opens. The first step is to select the Content Fragment Model that your fragment will be based on:

![Create Content Fragment - select Model](/help/journey-headless/author/assets/headless-journey-author-content-fragment-02.png)

After continuing with **Next** you can supply the details (**Basic** and **Advanced**) for your fragment:

![Create Content Fragment - provide Name](/help/journey-headless/author/assets/headless-journey-author-content-fragment-03.png)

Confirm with **Create** and you can then **Open** your fragment in the editor.
-->

### Edição de um fragmento {#editing-fragment}

É possível abrir um fragmento imediatamente depois de criá-lo ou selecionando-o no console Fragmentos de conteúdo (também no console Ativos).

Quando o editor for aberto pela primeira vez, você verá:

* Uma lista de ícones no lado esquerdo - isso lhe dá acesso a várias áreas de funcionalidade. O editor é aberto na guia **Variações**, em que ocorre a maioria das edições. Você também pode estar interessado nas guias **Anotações** e **Metadados**.

* Um cabeçalho com as informações sobre o fragmento e acesso a várias ações.

* A área de edição principal - isso depende do modelo usado para criar o fragmento.

Como exemplos:

* Um fragmento que apenas requer várias informações, algumas com um tipo específico. Para conteúdo headless, as referências são fundamentais. Você aprenderá sobre isso mais tarde na sua jornada.

   ![Editor de fragmento de conteúdo - Meu fragmento](/help/journey-headless/author/assets/headless-journey-author-content-fragment-04.png)

* Um fragmento que permite escrever uma longa seção de texto. Aqui há opções adicionais para gerenciar e formatar o texto. Você pode até mesmo abrir os campos de texto individuais em um editor de tela cheia (usando o ícone de tela pequena à direita)

   ![Editor de Fragmentos de conteúdo - Alaska Spirits](/help/journey-headless/author/assets/headless-journey-author-content-fragment-05.png)

>[!NOTE]
>
>A documentação específica do projeto pode ser necessária para ajudar os autores com detalhes sobre como preencher alguns campos com êxito.
>
>Consulte Modelos de fragmentos de conteúdo - Tipos de dados e propriedades para detalhes genéricos.

Confirme suas atualizações com **Salvar** ou **Salvar e fechar**.

>[!NOTE]
>
>Para obter mais detalhes, leia Variações - Criação de Fragmentos de conteúdo.

#### Com o que você (provavelmente) não precisa se preocupar {#what-you-probably-do-not-need-to-worry-about}

Essa seção pode parecer um pouco estranha, mas após abrir o Editor de Fragmento de conteúdo e começar a explorar, você verá várias opções que (provavelmente) não se aplicam à sua jornada headless como um Autor de conteúdo. Então, isto é apenas um rápido aviso do que você deve ser capaz de ignorar no contexto headless:

* **Modelos de fragmentos de conteúdo**

   Você verá o nome do Modelo do Fragmento de Conteúdo na parte superior do editor - diretamente sob o nome do fragmento. Este também é um link que leva você ao editor de modelo.
Os Modelos de fragmentos de conteúdo são essenciais para os Fragmentos de conteúdo, pois definem a estrutura usada. No entanto, criá-los e editá-los é (geralmente) responsabilidade de outro perfil, o Arquiteto de conteúdo.

   >[!NOTE]
   >
   >Se quiser saber mais, leia a Jornada do arquiteto de conteúdo do AEM Headless.

* **Conteúdo associado**

   Esta é bastante óbvia, já que é uma guia no editor.

   Fragmentos de conteúdo foram disponibilizados no AEM há algumas versões. Originalmente, eles eram disponibilizados para uso “tradicional” durante a criação de páginas....e ainda são usados nesse contexto. Isso pode envolver a associação de ativos (por exemplo, imagens) que, embora não estejam incorporados ao fragmento, precisam estar disponíveis para o autor ao criar uma página.

* **Visualização**

   Esta é outra guia no editor e fornece uma visualização técnica, destinada principalmente aos desenvolvedores.

* **Atualizar referências de página**

   Essa ação está disponível no menu suspenso **...** (reticências). Não é interessante para autores headless, pois se relaciona à criação de página.

### Publicação {#publishing}

<!-- needs more details -->

Após concluir o fragmento, é possível **Publicar** para que esteja disponível para os aplicativos headless.

As ações de publicação estão disponíveis no editor (ou na barra de ferramentas dos consoles **Fragmentos de conteúdo** ou **Ativos**):

![Editor de fragmento de conteúdo - Meu fragmento](/help/journey-headless/author/assets/headless-journey-author-content-fragment-06.png)

## O que vem a seguir {#whats-next}

Agora que você aprendeu o básico, o próximo passo é [Saiba mais sobre referências](references.md). Isso introduzirá e discutirá as várias referências disponíveis e como criar níveis de estrutura com as Referências de fragmento - uma parte essencial da criação para o headless.

## Recursos adicionais {#additional-resources}

* [Conceitos de criação](/help/sites-cloud/authoring/getting-started/concepts.md)

* [Manuseio básico](/help/sites-cloud/authoring/getting-started/basic-handling.md) - esta página se baseia principalmente no console **Sites**, mas muitos/a maioria dos recursos também são relevantes para a criação **Fragmentos de conteúdo** no console **Ativos**.

   * [Painel Navegação  ](/help/sites-cloud/authoring/getting-started/basic-handling.md#navigation-panel)

   * [O Cabeçalho](/help/sites-cloud/authoring/getting-started/basic-handling.md#the-header)

   * [Barra de ferramentas de ação](/help/sites-cloud/authoring/getting-started/basic-handling.md#actions-toolbar)

   * [Ações rápidas](/help/sites-cloud/authoring/getting-started/basic-handling.md#quick-actions)

   * [Visualização e seleção de recursos](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources)

   * [Seletor de painéis](/help/sites-cloud/authoring/getting-started/basic-handling.md#rail-selector)

   * Publicação

      * [Publicação rápida   ](/help/assets/manage-publication.md#quick-publish)

      * [Gerenciar publicação](/help/assets/manage-publication.md#manage-publication)

* [Trabalho com fragmentos de conteúdo](/help/sites-cloud/administering/content-fragments/content-fragments.md)

   * [Gerenciamento dos fragmentos de conteúdo](/help/sites-cloud/administering/content-fragments/content-fragments-managing.md)

      * [Aplique a configuração à sua pasta de ativos](/help/sites-cloud/administering/content-fragments/content-fragments-configuration-browser.md#apply-the-configuration-to-your-assets-folder)

      * [Criação de um fragmento de conteúdo](/help/sites-cloud/administering/content-fragments/content-fragments-managing.md#creating-a-content-fragment)
   * [Variações: criação de Fragmentos de conteúdo](/help/sites-cloud/administering/content-fragments/content-fragments-variations.md)

   * [Modelos de fragmentos do conteúdo](/help/sites-cloud/administering/content-fragments/content-fragments-models.md)

      * [Modelos de fragmento de conteúdo - Tipos de dados](/help/sites-cloud/administering/content-fragments/content-fragments-models.md#data-types)

      * [Modelos de fragmento de conteúdo: propriedades](/help/sites-cloud/administering/content-fragments/content-fragments-models.md#properties)

      * [Modelos de fragmentos de conteúdo: permitir modelos de fragmento de conteúdo na pasta Ativos](/help/sites-cloud/administering/content-fragments/content-fragments-models.md#allowing-content-fragment-models-assets-folder)


* Guias de introdução
   * [Criação de uma Pasta de ativos Configuração do Headless](/help/headless/setup/create-assets-folder.md)

* Jornada do arquiteto de conteúdo do AEM Headless

* Jornada de tradução headless do AEM
