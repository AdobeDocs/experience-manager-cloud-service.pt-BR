---
title: Saiba mais sobre as noções básicas de criação
description: Saiba mais sobre os conceitos e os mecanismos de criação de conteúdo para seu CMS headless usando Fragmentos de conteúdo.
exl-id: 3eca973f-b210-41bb-98da-ecbd2bae9803
solution: Experience Manager
feature: Headless, Content Fragments,GraphQL API
role: Admin, Architect, Developer
source-git-commit: 18c997a5644288e870c109a8d745b196349b923d
workflow-type: tm+mt
source-wordcount: '1733'
ht-degree: 81%

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

### Autor, visualização e publicação {#author-preview-publish}

Uma instalação do AEM geralmente conta com três ambientes:

* Autor
* Publicação
* Visualização

Você faz logon e usa o ambiente de criação para gerar o seu conteúdo. Quando estiver pronto, publique seu conteúdo para que ele fique disponível. Para headless, isso seria para outros aplicativos, para páginas da Web, isso seria para os leitores na Web.

Para obter mais detalhes, consulte os Conceitos de criação.

Usando o console de **fragmentos de conteúdo**, você também pode publicar no **serviço de visualização** para testar e visualizar antes de publicar. Consulte Publicar e visualizar um fragmento.

### Logon {#signing-in}

Como na maioria dos sistemas, é necessário fazer logon. Como autor, você receberá:

* Nome do usuário (conta)
* Senha
* Link para acessar a tela de logon

Sua conta já terá sido configurada com os privilégios necessários. Se você tiver algum problema, a Adobe recomenda que você entre em contato com a equipe interna de suporte ao projeto.

### Navegação {#navigation}

A primeira vez que você efetuar o logon, um pequeno tutorial online destacará alguns dos principais recursos da interface.

Em seguida, você pode usar o Painel de navegação para acessar as áreas-chave do AEM. Para Fragmentos de conteúdo, você usará o console **Fragmentos de Conteúdo** (para algumas ações, você também usará o console **Ativos**).

O Painel de navegação pode ser aberto selecionando o ícone da Adobe na parte superior esquerda, seguido pelo ícone de uma pequena bússola.

>[!NOTE]
>Embora os Fragmentos de conteúdo sejam um recurso do AEM **Sites**, eles são salvos como **Ativos**. Este é um detalhe técnico que não deve afetar você, mas que pode ser útil.

No console de Fragmentos de conteúdo, é possível selecionar pastas no painel esquerdo para navegar até o Fragmento de conteúdo. Também é possível filtrar e/ou pesquisar.

![Console de Fragmentos de conteúdo](/help/sites-cloud/administering/content-fragments/assets/cf-managing-console-filter.png)

### Ações, Seleção, Exibição {#actions-selecting-viewing}

No console de **Fragmentos de conteúdo**, várias ações estão disponíveis para seus fragmentos de conteúdo na barra de ferramentas:

* **Abrir no Assets**
* **Criar**
* A coluna **Referenciado por** também fornece um link direto para mostrar todas as referências principais desse fragmento, incluindo a referência a fragmentos de conteúdo, fragmentos de experiência e páginas.
* Passar o mouse sobre o nome da pasta mostrará o caminho JCR.

Após a seleção do fragmento, outras ações estarão disponíveis (conforme apropriado):

* **Abrir**
* **Publicar** (e **Desfazer publicação**)
* **Gerenciar Marcas**
* **Copiar**
* **Substituir**
* **Mover**
* **Renomeie**
* **Excluir**

>[!NOTE]
>
>Ações como Publicar, Desfazer publicação, Excluir, Mover, Renomear e Copiar acionam um processo assíncrono. O progresso desse processo pode ser monitorado por meio da interface de processos assíncronos do AEM.

## Criação de fragmentos de conteúdo {#authoring-content-fragments}

Essa foi uma introdução bem rápida à interface do AEM, mas espero que você tenha tido uma chance de experimentá-lo. Agora, chegamos ao seu verdadeiro interesse: Fragmentos de conteúdo para headless.

Teremos que passar pelas coisas do início ao fim, mas sua instância já pode ter pastas e/ou fragmentos criados, e eles podem estar em locais diferentes. Os princípios são os mesmos.

### Organização e navegação {#organizing-and-navigating}

A menos que tenha pouquíssimos Fragmentos de conteúdo, você vai querer organizá-los - para que você (e outros) possam encontrá-los novamente.

#### Criação de pastas {#creating-folder}

Você pode fazer isso criando uma série de pastas na seção **Arquivos** do console **Ativos**. Selecione a opção **Criar** (parte superior direita), seguido por **Pasta**:

![Opção Criar pasta](/help/journey-headless/author/assets/headless-journey-author-folder-01.png)

Uma caixa de diálogo é aberta, onde você pode inserir os detalhes e confirmar com **Criar**:

![Caixa de diálogo Criar pasta](/help/journey-headless/author/assets/headless-journey-author-folder-02.png)

#### Uso de caminhos e tags para limitar os Modelos de fragmentos de conteúdo disponíveis na pasta {#tags-paths-for-models-in-folder}

Esta seção é um pouco mais avançada. Você realmente não precisa dela se estiver apenas começando e testando as coisas, mas é *muito* útil quando há muitos fragmentos. Por isso é bom saber sobre ela mesmo que ainda não a utilize.

Seu Arquiteto de conteúdo terá criado todos os Modelos de fragmentos de conteúdo necessários para seu projeto atual e talvez alguns outros projetos também. Para ajudar a simplificar as coisas para você mesmo e para outros autores, você pode limitar a lista de modelos disponíveis para uma pasta específica.

Depois de criar a pasta, você pode abrir suas **Propriedades**. Aqui estão várias guias com informações e detalhes de configuração sobre a pasta. Especificamente para Fragmentos de conteúdo, você pode usar a guia **Políticas** para definir caminhos e/ou tags específicas para a pasta. Isso limita os Modelos de fragmentos do conteúdo disponíveis para uso na pasta, pois significa que eles devem atender a esses critérios antes que possam ser usados para gerar fragmentos nessa pasta.

![Criar propriedades de pasta - Políticas](/help/journey-headless/author/assets/headless-journey-author-folder-04.png)

>[!NOTE]
>
>Você pode ler mais detalhes em Modelos de fragmentos do conteúdo - Permitir Modelos de fragmentos do conteúdo na pasta de ativos.

Em seguida, navegue por essas pastas para criar e editar os Fragmentos de conteúdo.

#### Por segurança - Configuração dos serviços de pasta na nuvem {#cloud-services-folder}

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

### Edição de um fragmento {#editing-fragment}

É possível abrir um fragmento imediatamente depois de criá-lo ou selecionando-o no console Fragmentos de conteúdo (também no console Ativos).

>[!NOTE]
>
>Os Fragmentos de conteúdo são um recurso do Sites, mas são armazenados como **Assets**.
>
>Existem dois editores para a criação de fragmentos de conteúdo.
>
>* O novo editor, acessado principalmente pelo console **Fragmentos de conteúdo**.
>* O editor original, acessado principalmente pelo console **Assets**.

Quando o editor for aberto pela primeira vez, você verá:

* barra de ferramentas superior: para informações principais e ações
   * um link para o Console de fragmentos de conteúdo (ícone Início)
   * informações sobre o modelo e a pasta
   * links para Visualização; se o Padrão de URL de Visualização Padrão estiver configurado para o modelo
   * Publicar e Desfazer publicação de ações
   * uma opção para mostrar todas as **Referências principais** (ícone de link)
   * o fragmento **Status** e as últimas informações salvas
   * um botão para alternar para o editor original (baseado no Assets)
* painel esquerdo: mostra as **Variações** do fragmento de conteúdo e seus **Campos**:
   * esses links podem ser usados para navegar pela estrutura do fragmento de conteúdo
* painel direito: apresenta guias mostrando as propriedades (metadados) e tags, informações sobre o histórico de versões e informações relacionadas a quaisquer cópias de idioma
   * na guia **Propriedades**, é possível atualizar o **Título** e a **Descrição** do fragmento ou a **Variação**
* painel central: mostra os campos reais e o conteúdo da variação selecionada
   * permite editar o conteúdo
   * se os campos **Espaço Reservado para Guia** forem definidos no modelo, eles serão mostrados aqui e poderão ser usados para navegação

Por exemplo, um fragmento pode:

* Exigir várias informações, algumas com um tipo específico. Para conteúdo headless, as referências são fundamentais (você aprenderá sobre elas mais tarde na jornada).

* Permite escrever uma longa seção de texto. Aqui há opções adicionais para gerenciar e formatar o texto. Você pode até mesmo abrir os campos de texto individuais em um editor de tela cheia (usando o ícone de tela pequena à direita)

![Editor de Fragmentos de conteúdo - Alaska Spirits](/help/sites-cloud/administering/content-fragments/assets/cf-authoring-overview.png)

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

  Você pode ver o nome do Modelo de fragmento de conteúdo no painel direito do editor. Este também é um link que leva você ao editor de modelo.
Os Modelos de fragmentos de conteúdo são essenciais para os Fragmentos de conteúdo, pois definem a estrutura usada. No entanto, criá-los e editá-los é (geralmente) responsabilidade de outro perfil, o Arquiteto de conteúdo.

  >[!NOTE]
  >
  >Se quiser saber mais, leia a Jornada do arquiteto de conteúdo do AEM Headless.

### Publicação {#publishing}

<!-- needs more details -->

Após concluir o fragmento, é possível **Publicar** para que esteja disponível para os aplicativos headless.

As ações de publicação estão disponíveis no editor:

![Editor de fragmento de conteúdo - Meu fragmento](/help/journey-headless/author/assets/headless-journey-author-content-fragment-06.png)

>[!NOTE]
>
>Você também pode publicar seu fragmento usando o console de **Ativos** ou **Fragmentos de conteúdo**.

## O que vem a seguir {#whats-next}

Agora que você aprendeu o básico, o próximo passo é [Saiba mais sobre referências](references.md). Isso introduzirá e discutirá as várias referências disponíveis e como criar níveis de estrutura com as Referências de fragmento - uma parte essencial da criação para o headless.

## Recursos adicionais {#additional-resources}

* [Conceitos de criação](/help/sites-cloud/authoring/author-publish.md)

* [Manuseio básico](/help/sites-cloud/authoring/basic-handling.md) - esta página se baseia principalmente no console **Sites**, mas muitos/a maioria dos recursos também são relevantes para a criação **Fragmentos de conteúdo** no console **Ativos**.

   * [Painel Navegação](/help/sites-cloud/authoring/basic-handling.md#navigation-panel)

   * [O Cabeçalho](/help/sites-cloud/authoring/basic-handling.md#the-header)

   * [Barra de ferramentas de ação](/help/sites-cloud/authoring/basic-handling.md#actions-toolbar)

   * [Ações rápidas](/help/sites-cloud/authoring/basic-handling.md#quick-actions)

   * [Visualização e seleção de recursos](/help/sites-cloud/authoring/basic-handling.md#viewing-and-selecting-resources)

   * [Seletor de painéis](/help/sites-cloud/authoring/basic-handling.md#rail-selector)

* [Trabalho com Fragmentos de conteúdo](/help/sites-cloud/administering/content-fragments/overview.md)

   * [Gerenciamento dos Fragmentos de conteúdo](/help/sites-cloud/administering/content-fragments/managing.md)

   * [Aplique a configuração à sua pasta de ativos](/help/sites-cloud/administering/content-fragments/setup.md#apply-the-configuration-to-your-folder)

   * [Criação de um Fragmento de conteúdo](/help/sites-cloud/administering/content-fragments/managing.md#creating-a-content-fragment)

   * [Criação de fragmentos de conteúdo](/help/sites-cloud/administering/content-fragments/authoring.md)

   * Publicação

      * No editor ou no console de **Ativos**

         * [Publicação rápida](/help/assets/manage-publication.md#quick-publish)

         * [Gerenciar publicação](/help/assets/manage-publication.md#manage-publication)

      * No console de **Fragmentos de conteúdo**

         * [Publicar e visualizar um fragmento de conteúdo](/help/sites-cloud/administering/content-fragments/managing.md#publishing-and-previewing-a-fragment)

   * [Modelos de fragmentos do conteúdo](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md)

      * [Modelos de fragmento de conteúdo - Tipos de dados](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#data-types)

      * [Modelos de fragmento de conteúdo: propriedades](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#properties)

      * [Modelos de fragmentos de conteúdo: permitir modelos de fragmento de conteúdo na pasta Ativos](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md#allowing-content-fragment-models-assets-folder)

* [Fragmentos de conteúdo - editor original, no console do Assets](/help/assets/content-fragments/content-fragments-variations.md)

* Guias de introdução
   * [Criação de uma Pasta de ativos Configuração do Headless](/help/headless/setup/create-assets-folder.md)

* Jornada do arquiteto de conteúdo do AEM Headless

* Jornada de tradução headless do AEM
