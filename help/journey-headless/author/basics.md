---
title: Noções básicas sobre criação de aprendizado
description: Saiba mais sobre os conceitos e os mecanismos de criação de conteúdo para seu CMS sem cabeçalho usando Fragmentos de conteúdo.
index: false
hide: true
hidefromtoc: true
source-git-commit: 41ad9e8ee77ae4494d28026b5ad9da45c06eaeaf
workflow-type: tm+mt
source-wordcount: '1683'
ht-degree: 3%

---


# Noções básicas de criação para headless com AEM {#author-headless-basics}

## A história até agora {#story-so-far}

No início da [AEM Jornada do autor de conteúdo sem cabeçalho](overview.md) a [Introdução](introduction.md) cobria os conceitos básicos e a terminologia relevante para a criação sem cabeçalho.

Este artigo é baseado neles para que você entenda como criar seu próprio conteúdo para seu projeto sem periféricos de AEM.

## Objetivo {#objective}

* **Público-alvo**: Iniciante
* **Objetivo**: Apresente as noções básicas da criação de CMS sem cabeçalho:
   * Introdução à criação com o AEMaaCS
   * Introdução aos fragmentos de conteúdo

## Manuseio básico {#basic-handling}

Antes de lidar com Fragmentos de conteúdo, veja uma (muito) rápida introdução ao uso de AEM....mas nada substitui a experiência de entrar e tentar usar o sistema.

### Autor e publicação {#author-preview-publish}

Uma instalação do AEM geralmente consiste em pelo menos dois ambientes:

* Autor
* Publicação

Você faz logon e usa o ambiente de criação para gerar seu conteúdo. Quando estiver pronto, publique seu conteúdo para que ele fique disponível. Para ser impotente, isso seria para outros aplicativos, para páginas da Web isso seria para os leitores na Web.

Para obter mais detalhes, consulte os Conceitos de criação .

### Fazer logon {#signing-in}

Assim como na maioria dos sistemas, você precisará fazer logon. Como autor, você receberá:

* Nome do usuário (conta)
* Senha
* Link para acessar a tela de logon

Sua conta terá sido configurada com os privilégios necessários. Em caso de problemas, recomendamos que você entre em contato com a equipe interna de suporte a projetos.

### Navegação {#navigation}

A primeira vez que você efetuar o logon em um pequeno tutorial online destacará alguns dos principais recursos da interface do usuário do .

Em seguida, você pode usar o Painel de navegação para acessar áreas-chave de AEM. Para Fragmentos de conteúdo, você estará usando o **Console de ativos**.

O Painel de navegação pode ser aberto selecionando o ícone Adobe na parte superior esquerda, seguido pelo pequeno ícone de bússola:

![Painel Navegação](/help/journey-headless/author/assets/headless-journey-author-navigation-01.png)

>[!NOTE]
>Embora os Fragmentos de conteúdo sejam um recurso AEM **Sites**, eles são encontrados no console **Assets**. Este é um detalhe técnico que não deve afetá-lo, mas que pode ser útil saber.

No console, é possível selecionar pastas para navegar até o Fragmento do conteúdo ou a navegação estrutural (no cabeçalho) para navegar de volta para a árvore.

![Navegações estruturais](/help/journey-headless/author/assets/headless-journey-author-navigation-02.png)

### Ações, Seleção, Exibição {#actions-selecting-viewing}

O console **Assets** tem **Barras de ferramentas de ação** dedicadas e **Ações rápidas** que você pode usar após selecionar um recurso (por exemplo, uma pasta ou fragmento de conteúdo).

As Ações rápidas estão disponíveis para um único recurso:

![Ações rápidas](/help/journey-headless/author/assets/headless-journey-author-navigation-05.png)

A barra de ferramentas Ações fornece acesso a toda a gama de ações - aplicáveis ao cenário atual. As ações disponíveis podem mudar; por exemplo, dependendo da sua localização ou se você selecionou vários recursos:

![Barra de ferramentas de ação](/help/journey-headless/author/assets/headless-journey-author-navigation-06.png)

Você pode selecionar o formato para visualizar seus recursos com o Seletor de exibições:

![Exibir seletor](/help/journey-headless/author/assets/headless-journey-author-navigation-03.png)

Você pode exibir informações adicionais sobre itens usando o Seletor de painéis. Isso também dá acesso a ações adicionais.

![Painel esquerdo](/help/journey-headless/author/assets/headless-journey-author-navigation-04.png)

## Criação de fragmentos de conteúdo {#authoring-content-fragments}

Então, essa foi uma introdução muito rápida à interface do usuário do AEM, mas espero que você tenha tido a chance de experimentá-la. Agora, mostramos seu interesse real - Fragmentos de conteúdo para headless.

Teremos que passar pelas coisas do início ao fim, mas sua instância já pode ter pastas e/ou fragmentos criados, e eles podem estar em locais diferentes. Os princípios são os mesmos.

### Organização e navegação {#organizing-and-navigating}

A menos que tenha pouquíssimos Fragmentos de conteúdo, você desejará organizá-los - para que você (e outros) os encontre novamente.

#### Criação de uma pasta {#creating-folder}

Você pode fazer isso criando uma série de pastas na seção **Files** do console Assets. Selecione a opção **Criar** (canto superior direito), seguida de **Criar pasta**:

![Opção Criar pasta](/help/journey-headless/author/assets/headless-journey-author-folder-01.png)

Uma caixa de diálogo será aberta onde você pode inserir os detalhes e, em seguida, confirmar com **Criar**:

![Caixa de diálogo Criar pasta](/help/journey-headless/author/assets/headless-journey-author-folder-02.png)

#### Uso de caminhos e tags para limitar os modelos de fragmentos de conteúdo disponíveis na pasta {#tags-paths-for-models-in-folder}

Esta seção está um pouco mais avançada. Você não precisa realmente dele se estiver apenas começando e tentando coisas, mas ele é *very* útil quando você tem muitos fragmentos. Por isso é bom saber - mesmo que ainda não o utilize.

Seu Arquiteto de conteúdo terá criado todos os Modelos de fragmento de conteúdo necessários para seu projeto atual e talvez alguns outros projetos também. Para ajudar a simplificar as coisas para seus autores, você pode limitar a lista de modelos disponíveis para uma pasta específica.

Depois de criar a pasta, você pode abrir a pasta **Propriedades**. Aqui estão várias guias com informações e detalhes de configuração sobre a pasta. Particularmente para Fragmentos de conteúdo, você pode usar a guia **Policies** para definir caminhos e/ou tags específicos para essa pasta. Isso limita os Modelos de fragmento de conteúdo disponíveis para uso na pasta, pois significa que os Modelos de fragmento de conteúdo devem atender a esses requisitos antes que possam ser usados para gerar fragmentos nessa pasta.

![Criar propriedades de pasta - Políticas](/help/journey-headless/author/assets/headless-journey-author-folder-04.png)

>[!NOTE]
>
>Você pode ler mais detalhes em Modelos de fragmentos de conteúdo - Permitir modelos de fragmentos de conteúdo na pasta Ativos.

Em seguida, navegue por essas pastas para criar e editar os Fragmentos de conteúdo.

#### Por acaso - Configuração de Cloud Services de pasta {#cloud-services-folder}

Só para o caso...

Você provavelmente receberá uma pasta inicial onde poderá criar suas pastas. Isso ocorre porque alguns detalhes de configuração devem ser aplicados (geralmente por um Desenvolvedor ou Administrador do Sistema) à pasta raiz. Isso provavelmente não lhe interessará, mas se necessário, você poderá verificar a **Configuração** no **Cloud Services** da pasta **Propriedades**:

![Criar propriedades de pasta - Configuração](/help/journey-headless/author/assets/headless-journey-author-folder-03.png)

>[!NOTE]
>
>Você pode ler mais em Aplicar a configuração à pasta Ativos .

### Criação de um fragmento de conteúdo {#creating-fragment}

A criação de um Fragmento de conteúdo é muito semelhante - em vez disso, use a opção **Fragmento de conteúdo** :

![Opção Criar fragmento de conteúdo](/help/journey-headless/author/assets/headless-journey-author-content-fragment-01.png)

Desta vez, um assistente será aberto. A primeira etapa é selecionar o Modelo do fragmento de conteúdo no qual o fragmento será baseado:

![Criar fragmento de conteúdo - selecione Modelo](/help/journey-headless/author/assets/headless-journey-author-content-fragment-02.png)

Depois de continuar com **Next**, você pode fornecer os detalhes do fragmento:

![Criar fragmento do conteúdo - fornecer nome](/help/journey-headless/author/assets/headless-journey-author-content-fragment-03.png)

Confirme com **Criar** e você poderá **Abrir** seu fragmento no editor.

### Edição de um fragmento {#editing-fragment}

Você pode abrir um fragmento imediatamente após criá-lo ou selecionando-o no console Assets.

Quando o editor for aberto pela primeira vez, você verá:

* Uma lista de ícones no lado esquerdo - isso dá acesso a várias áreas de funcionalidade. O editor é aberto na guia **Variations**, é aqui que a maior parte da edição acontece. Você também pode estar interessado nas guias **Anotações** e **Metadados**.

* Um cabeçalho com informações sobre o fragmento e acesso a várias ações.

* A área de edição principal - depende do modelo usado para criar o fragmento.

Como exemplos:

* Um fragmento que requer apenas várias informações, algumas com um tipo específico. Para conteúdo sem cabeçalho, referências são fundamentais, você aprenderá sobre isso mais tarde na sua jornada.

   ![Editor de fragmento de conteúdo - Meu fragmento](/help/journey-headless/author/assets/headless-journey-author-content-fragment-04.png)

* Um fragmento que permite escrever uma longa seção de texto. Aqui há opções adicionais para gerenciar e formatar o texto. Você pode até mesmo abrir os campos de texto individuais em um editor de tela cheia (usando o ícone de tela pequena à direita)

   ![Editor de fragmentos de conteúdo - Espirais do Alasca](/help/journey-headless/author/assets/headless-journey-author-content-fragment-05.png)

>[!NOTE]
>
>A documentação específica do projeto pode ser necessária para ajudar os autores com detalhes sobre como preencher alguns campos com êxito.
>
>Consulte Modelos de fragmentos de conteúdo - Tipos de dados e propriedades para obter detalhes genéricos.

Confirme suas atualizações com **Save** ou **Save &amp; close**.

>[!NOTE]
>
>Para obter mais detalhes, leia Variações - Criação de fragmentos de conteúdo .

#### O que você (provavelmente) não precisa se preocupar {#what-you-probably-do-not-need-to-worry-about}

OK, essa seção pode parecer um pouco estranha, mas depois de abrir o Editor de fragmento de conteúdo e começar a explorar, você verá várias opções que (provavelmente) não se aplicam à sua jornada sem cabeçalho como um Autor de conteúdo. Então isto é apenas uma breve visualização do que você deve ser capaz de ignorar no contexto sem cabeça:

* **Modelos de fragmentos do conteúdo**

   Você verá o nome do Modelo do fragmento de conteúdo na parte superior do editor - diretamente sob o nome do fragmento. Este também é um link que leva você ao editor de modelo.
Os Modelos de fragmentos de conteúdo são essenciais para os Fragmentos de conteúdo, pois definem a estrutura usada. No entanto, criá-los e editá-los é (geralmente) responsabilidade de outra pessoa, o Arquiteto de conteúdo.

   >[!NOTE]
   >
   >Se quiser saber mais, leia a Jornada do AEM Headless Content Architect.

* **Conteúdo associado**

   Esta é bastante óbvia, já que é uma guia no editor.

   Fragmentos de conteúdo foram disponibilizados no AEM para várias versões. Originalmente, eles eram disponibilizados para uso &quot;tradicional&quot; durante a criação de páginas....e ainda são usados nesse contexto. Isso pode envolver a associação de ativos (por exemplo, imagens) que, embora não estejam incorporados ao fragmento, precisam estar disponíveis para o autor ao criar uma página.

* **Visualizar**

   Esta é outra guia no editor e fornece uma visualização técnica, destinada principalmente aos desenvolvedores.

* **Atualizar referências de página**

   Esta ação está disponível no **...Lista suspensa** (elipses). Não é interessante para autores sem cabeçalho, pois se relaciona à criação de página.

### Publicação {#publishing}

<!-- needs more details -->

Após concluir o fragmento, você pode **Publicar** para que ele fique disponível para os aplicativos sem periféricos.

As ações de publicação estão disponíveis no editor (ou na barra de ferramentas do console **Assets**):

![Editor de fragmento de conteúdo - Meu fragmento](/help/journey-headless/author/assets/headless-journey-author-content-fragment-06.png)

## O que vem a seguir {#whats-next}

Agora que você aprendeu as noções básicas, o próximo passo é [Saiba como sobre Referências](references.md). Isso introduzirá e discutirá as várias referências disponíveis e como criar níveis de estrutura com as Referências de fragmento - uma parte essencial da criação para o headless.

## Recursos adicionais {#additional-resources}

* [Conceitos de criação](/help/sites-cloud/authoring/getting-started/concepts.md)

* [Manuseio básico](/help/sites-cloud/authoring/getting-started/basic-handling.md)  - esta página é baseada principalmente no console  **** Sites, mas muitos/a maioria dos recursos também são relevantes para a criação de  **Fragmentos** de conteúdo no console  **** Ativos.

   * [Painel Navegação  ](/help/sites-cloud/authoring/getting-started/basic-handling.md#navigation-panel)

   * [O Cabeçalho](/help/sites-cloud/authoring/getting-started/basic-handling.md#the-header)

   * [Barra de ferramentas de ação](/help/sites-cloud/authoring/getting-started/basic-handling.md#actions-toolbar)

   * [Ações rápidas](/help/sites-cloud/authoring/getting-started/basic-handling.md#quick-actions)

   * [Visualização e seleção de recursos](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources)

   * [Seletor de painéis](/help/sites-cloud/authoring/getting-started/basic-handling.md#rail-selector)

* [Trabalho com fragmentos de conteúdo](/help/assets/content-fragments/content-fragments.md)

   * [Gerenciamento dos fragmentos de conteúdo](/help/assets/content-fragments/content-fragments-managing.md)

      * [Aplicar a configuração à sua pasta de ativos](/help/assets/content-fragments/content-fragments-configuration-browser.md#apply-the-configuration-to-your-assets-folder)

      * [Criação de um fragmento de conteúdo](/help/assets/content-fragments/content-fragments-managing.md#creating-a-content-fragment)
   * [Variações - Criação de fragmentos de conteúdo](/help/assets/content-fragments/content-fragments-variations.md)

   * [Modelos de fragmentos do conteúdo](/help/assets/content-fragments/content-fragments-models.md)

      * [Modelos de fragmentos do conteúdo - Tipos de dados](/help/assets/content-fragments/content-fragments-models.md#data-types)

      * [Modelos de fragmentos do conteúdo - Propriedades](/help/assets/content-fragments/content-fragments-models.md#properties)

      * [Modelos de fragmentos do conteúdo - Permitir modelos de fragmentos do conteúdo na pasta Ativos](/help/assets/content-fragments/content-fragments-models.md#allowing-content-fragment-models-assets-folder)


* Guias de introdução
   * [Criação de uma pasta de ativos sem cabeçalho Guia de início rápido](/help/implementing/developing/headless/getting-started/create-assets-folder.md)

* jornada do AEM Headless Content Architect

* jornada de tradução sem cabeçalho AEM