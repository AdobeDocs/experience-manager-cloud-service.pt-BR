---
title: Introdução à tradução do AEM Sites
description: Saiba como organizar o conteúdo do AEM Sites e como funcionam AEM ferramentas de tradução.
index: true
hide: false
hidefromtoc: false
exl-id: 9bfc3995-ac8e-488e-b68f-9e1b5b4a3176
source-git-commit: 96a0dacf69f6f9c5744f224d1a48b2afa11fb09e
workflow-type: tm+mt
source-wordcount: '1412'
ht-degree: 0%

---

# Introdução à tradução do AEM Sites {#getting-started}

Saiba como organizar o conteúdo do AEM Sites e como funcionam AEM ferramentas de tradução.

## A História Até Agora {#story-so-far}

No documento anterior da jornada de tradução do AEM Sites, [Saiba mais sobre o conteúdo do AEM Sites e como traduzir no AEM](learn-about.md) você aprendeu a teoria básica do AEM Sites e agora deve:

* Entenda os conceitos básicos da criação de conteúdo do AEM Sites.
* Familiarize-se com o suporte AEM tradução.

Este artigo se baseia nesses fundamentos para que você entenda como o AEM armazena e gerencia o conteúdo e como você pode usar AEM ferramentas de tradução para traduzir esse conteúdo.

## Objetivo {#objective}

Este documento ajuda você a entender como começar a traduzir conteúdo de sites no AEM. Depois de ler, você deve:

* Entenda a importância da estrutura de conteúdo para a tradução.
* Entenda como o AEM armazena conteúdo.
* Familiarize-se com AEM ferramentas de tradução.

## Requisitos e pré-requisitos {#requirements-prerequisites}

Há vários requisitos antes de começar a traduzir o conteúdo AEM.

### Conhecimento {#knowledge}

* Experiência de tradução de conteúdo em um CMS
* Experiência usando os recursos básicos de um CMS em larga escala
* Possuir um conhecimento prático AEM tratamento básico
* Noções básicas do serviço de tradução que você está usando
* Ter uma compreensão básica do conteúdo que você está traduzindo

>[!TIP]
>
>Se você não estiver familiarizado com o uso de um CMS em larga escala como o AEM, considere revisar a [Manuseio básico](/help/sites-cloud/authoring/getting-started/basic-handling.md) documentação antes de continuar. A documentação de Manuseio básico não faz parte da jornada, portanto, retorne a esta página quando terminar.

### Ferramentas {#tools}

* Acesso à sandbox para testes de tradução do conteúdo
* Credenciais para se conectar ao serviço de tradução preferencial
* Ser membro do `project-administrators` grupo em AEM

## Como o AEM armazena conteúdo {#content-in-aem}

Para o especialista em tradução, não é importante entender em detalhes como o AEM gerencia o conteúdo. Entretanto, familiarizar-se com os conceitos e a terminologia básicos será útil, pois você poderá usar as ferramentas de tradução AEM mais tarde. O mais importante é que você precisa entender seu próprio conteúdo e como ele é estruturado para traduzi-lo efetivamente.

### Console de sites {#sites-console}

O console Sites fornece uma visão geral da estrutura do seu conteúdo, facilitando a navegação pelo seu conteúdo, além de gerenciá-lo criando novas páginas, movendo e copiando páginas, bem como publicando conteúdo.

Para acessar o console de sites:

1. No menu de navegação global, clique ou toque em **Navegação** -> **Sites**.
1. O console Sites é aberto no nível superior do seu conteúdo.
1. Certifique-se de que a variável **Exibição de coluna** é selecionado usando o seletor de exibições na parte superior direita da janela.

   ![Seleção da exibição de coluna](assets/selecting-column-view.png)

1. Ao tocar ou clicar em um item em uma coluna, ele mostra o conteúdo abaixo na hierarquia na coluna à direita.

   ![Hierarquia de conteúdo](assets/sites-console-hierarchy.png)

1. Ao tocar ou clicar na caixa de seleção de um item em uma coluna, ele seleciona esse item e mostra os detalhes do item selecionado na coluna à direita, bem como revela várias ações disponíveis para o item selecionado na barra de ferramentas acima.

   ![Seleção de conteúdo](assets/sites-console-selection.png)

1. Ao tocar ou clicar no seletor do painel na parte superior esquerda, também é possível mostrar a variável **Árvore de conteúdo** para obter uma visão geral em árvore do seu conteúdo.

   ![Exibição da árvore de conteúdo](assets/sites-console-content-tree.png)

Com essas ferramentas simples, você pode navegar intuitivamente pela sua estrutura de conteúdo.

>[!NOTE]
>
>O arquiteto de conteúdo normalmente define a estrutura do conteúdo, enquanto os autores de conteúdo criam o conteúdo dentro dessa estrutura.
>
>Como especialista em tradução, é importante simplesmente entender como navegar por essa estrutura e entender onde o conteúdo está localizado.

### Editor de página {#page-editor}

O console Sites permite navegar pelo seu conteúdo e fornece uma visão geral de sua estrutura. Para ver os detalhes de uma página individual, é necessário usar o editor de sites.

Para editar uma página:

1. Use o console Sites para localizar e selecionar uma página. Lembre-se de que é necessário tocar ou clicar na caixa de seleção de uma página individual para selecioná-la.

   ![Selecionar uma página para editar](assets/sites-editor-select-page.png)

1. Toque no **Editar** na barra de ferramentas.
1. O editor de sites é aberto com a página selecionada carregada para edição em uma nova guia do navegador.
1. Passar o mouse sobre o conteúdo ou tocar nele revela seletores de componentes individuais. Os componentes são os blocos que formam a página.

   ![Edição de uma página](assets/sites-editor-title.png)

Você pode retornar ao console de sites, alternando de volta para essa guia no navegador a qualquer momento. Usando o editor de sites, você pode visualizar rapidamente o conteúdo da página, conforme os autores de conteúdo e seu público-alvo o verão.

>[!NOTE]
>
>Os autores de conteúdo criam o conteúdo do site usando o editor de sites.
>
>Como especialista em tradução, é importante simplesmente entender como visualizar os detalhes desse conteúdo usando o editor de sites.

## Estrutura é chave {#content-structure}

AEM conteúdo é orientado por sua estrutura. AEM impõe poucos requisitos à estrutura de conteúdo, mas uma consideração cuidadosa da hierarquia de conteúdo como parte do planejamento do projeto pode tornar a tradução muito mais simples.

>[!TIP]
>
>Planejar a tradução no início do projeto de AEM. Trabalhe em conjunto com o gerente do projeto e os arquitetos de conteúdo antecipadamente.
>
>Um Gerente de projeto de internacionalização pode ser necessário como uma pessoa separada, cuja responsabilidade é definir qual conteúdo deve ser traduzido e o que não, e qual conteúdo traduzido pode ser modificado pelos produtores de conteúdo regionais ou locais.

## Estrutura de conteúdo recomendada {#recommended-structure}

Conforme recomendado anteriormente, trabalhe com seu arquiteto de conteúdo para determinar a estrutura de conteúdo apropriada para seu próprio projeto. No entanto, a seguinte estrutura é comprovada, simples e intuitiva e é bastante eficaz.

Defina uma pasta base para o seu projeto em `/content`.

```text
/content/<your-project>
```

O idioma em que o conteúdo é criado é chamado de raiz de idioma. No nosso exemplo, é o inglês e deve estar abaixo deste caminho.

```text
/content/<your-project>/en
```

Todo o conteúdo do projeto que pode precisar ser localizado deve ser colocado na raiz do idioma.

```text
/content/<your-project>/en/<your-project-content>
```

As traduções devem ser criadas como pastas irmãs ao lado da raiz do idioma, com o nome da pasta representando o código de idioma ISO-2 do idioma. Por exemplo, alemão teria o seguinte caminho.

```text
/content/<your-project>/de
```

>[!NOTE]
>
>O arquiteto de conteúdo geralmente é responsável pela criação dessas pastas de idioma. Se não forem criadas, AEM não poderá criar trabalhos de tradução posteriormente.

A estrutura final pode ser parecida com a seguinte.

```text
/content
    |- your-project
        |- en
            |- some
            |- exciting
            |- sites
            |- content
        |- de
        |- fr
        |- it
        |- ...
    |- another-project
    |- ...
```

Você deve anotar o caminho específico do conteúdo, pois ele será necessário posteriormente para configurar a tradução.

>[!NOTE]
>
>Geralmente, é responsabilidade do arquiteto de conteúdo definir a estrutura de conteúdo, geralmente em colaboração com o especialista em tradução.
>
>Ela é detalhada aqui para ser completa.

## Ferramentas de tradução AEM {#translation-tools}

Agora que você entende o console e o editor de sites e a importância da estrutura de conteúdo, podemos observar como traduzir o conteúdo. As ferramentas de tradução em AEM são bastante poderosas, mas são simples de entender em alto nível.

* **Conector de tradução** - O conector é o link entre o AEM e o serviço de tradução usado.
* **Regras de tradução** - As regras definem qual conteúdo em caminhos específicos deve ser traduzido.
* **Projetos de tradução** - Os projetos de tradução reúnem conteúdo que deve ser abordado como um único esforço de tradução e rastreia o progresso da tradução, interagindo com o conector para transmitir o conteúdo a ser traduzido e recebê-lo de volta do serviço de tradução.

Geralmente, você só configura o conector uma vez para a instância e para as regras por projeto. Em seguida, você usa projetos de tradução para traduzir seu conteúdo e manter suas traduções atualizadas continuamente.

## O que vem a seguir {#what-is-next}

Agora que você concluiu esta parte da jornada de tradução do AEM Sites, deve:

* Entenda a importância da estrutura de conteúdo para a tradução.
* Entenda como o AEM armazena conteúdo.
* Familiarize-se com AEM ferramentas de tradução.

Aproveite esse conhecimento e continue sua jornada de tradução do AEM Sites revisando o documento [Configurar o conector de tradução](configure-connector.md) onde você aprenderá a se conectar AEM a um serviço de tradução.|

## Recursos adicionais {#additional-resources}

Embora seja recomendável seguir para a próxima parte da jornada de tradução revisando o documento [Configurar o conector de tradução](configure-connector.md) a seguir estão alguns recursos adicionais e opcionais que aprofundam alguns conceitos mencionados neste documento, mas não é necessário que eles continuem na jornada.

* [Manuseio básico de AEM](/help/sites-cloud/authoring/getting-started/basic-handling.md) - Saiba mais sobre as noções básicas da interface do usuário do AEM para navegar e executar tarefas essenciais com facilidade, como encontrar seu conteúdo.
* [Identificação de conteúdo a ser traduzido](/help/sites-cloud/administering/translation/rules.md) - Saiba como as regras de tradução identificam o conteúdo que precisa ser traduzido.
* [Configuração da estrutura de integração de tradução](/help/sites-cloud/administering/translation/integration-framework.md) - Saiba como configurar a Estrutura de integração de tradução para integrar com serviços de tradução de terceiros.
* [Gerenciamento de projetos de tradução](/help/sites-cloud/administering/translation/managing-projects.md) - Saiba como criar e gerenciar projetos de tradução automática e humana no AEM.
