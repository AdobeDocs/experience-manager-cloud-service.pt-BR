---
title: Criar Site a partir de Modelo
description: Saiba como criar rapidamente um novo site de AEM usando um modelo de site.
source-git-commit: 73e9d1debe70aff7f53d658bbac074fc53d8f1ae
workflow-type: tm+mt
source-wordcount: '1518'
ht-degree: 0%

---


# Criar Site a partir de Modelo {#create-site-from-template}

Saiba como criar rapidamente um novo site de AEM usando um modelo de site.

>[!CAUTION]
>
>No momento, a ferramenta Criação rápida de site é uma visualização técnica. É disponibilizado para fins de ensaio e avaliação e não se destina à utilização da produção, a menos que acordado com o apoio ao Adobe.

## A História Até Agora {#story-so-far}

No documento anterior da jornada de Criação AEM de Site Rápido, [Entender o Cloud Manager e o fluxo de trabalho de criação rápida do site,](cloud-manager.md) você aprendeu sobre o Cloud Manager e como ele se vincula ao novo processo de Criação rápida de sites e agora deve:

* Entenda como o AEM Sites e o Cloud Manager trabalham juntos para facilitar o desenvolvimento de front-end
* Veja como a etapa de personalização de front-end é totalmente dissociada do AEM e não requer conhecimento AEM.

Este artigo se baseia nesses fundamentos para que você possa dar a primeira etapa de configuração e criar um novo site como um modelo, que pode ser personalizado posteriormente usando ferramentas de front-end.

## Objetivo {#objective}

Este documento ajuda você a entender como criar rapidamente um novo site AEM usando um modelo de site. Depois de ler, você deve:

* Saiba como obter modelos de site AEM.
* Saiba como criar um novo site usando um modelo.
* Veja como baixar o modelo do seu novo site para fornecer ao desenvolvedor de front-end.

## Função responsável {#responsible-role}

Essa parte da jornada se aplica ao administrador do AEM.

## Modelos de site {#site-templates}

Os modelos de site são uma maneira de combinar conteúdo básico do site em um pacote conveniente e reutilizável. Os modelos de site geralmente contêm conteúdo básico e estrutura do site, bem como informações de estilo do site para começar o novo site rapidamente. A estrutura real é a seguinte:

* `files`: Pasta com o kit de interface do usuário, XD arquivo e possivelmente outros arquivos
* `previews`: Pasta com capturas de tela do modelo de site
* `site`: Pacote de conteúdo do conteúdo que é copiado para cada site criado a partir deste modelo, como modelos de página, páginas, etc.
* `theme`: Fontes do tema de modelo para modificar a aparência do site, incluindo CSS, JavaScript, etc.

Os modelos são eficientes porque são reutilizáveis para que os autores de conteúdo possam criar um site rapidamente. E como você pode ter vários modelos disponíveis na sua instalação do AEM, você tem a flexibilidade para atender a várias necessidades comerciais.

>[!NOTE]
>
>O modelo de site não deve ser confundido com modelos de página. Os modelos de site descritos aqui definem a estrutura geral de um site. Um modelo de página define a estrutura e o conteúdo inicial de uma página individual.

## Obter um modelo de site {#obtaining-template}

A maneira mais simples de começar é [baixe a versão mais recente do Modelo de site padrão do AEM de seu repositório GitHub.](https://github.com/adobe/aem-site-template-standard/releases)

Após o download, você pode carregá-lo no ambiente de AEM como faria com qualquer outro pacote. Consulte a [Seção Recursos adicionais](#additional-resources) para obter detalhes sobre como trabalhar com pacotes, se precisar de mais informações sobre este tópico.

>[!TIP]
>
>O modelo de site padrão do AEM pode ser personalizado para atender às necessidades do seu projeto e pode evitar a necessidade de mais personalização. No entanto, este tópico está fora do escopo dessa jornada. Consulte a documentação do GitHub do Modelo de site padrão para obter mais informações.

>[!TIP]
>
>Você também pode optar por criar o modelo da origem como parte do fluxo de trabalho do projeto. No entanto, este tópico está fora do escopo dessa jornada. Consulte a documentação do GitHub do Modelo de site padrão para obter mais informações.

## Instalar um modelo de site {#installing-template}

Usar um modelo para criar um novo site é muito fácil.

1. Faça logon no ambiente de criação do AEM e navegue até o console Sites

   * `https://<your-author-environment>.adobeaemcloud.com/sites.html/content`

1. Toque ou clique **Criar** no canto superior direito do ecrã e, no menu suspenso, selecione **Site a partir do modelo**.

   ![Criação de um novo site a partir de um modelo](assets/create-site-from-template.png)

1. No assistente Criar site , toque ou clique em **Importar** na parte superior da coluna à esquerda.

   ![Assistente de criação do site](assets/site-creation-wizard.png)

1. No navegador de arquivos, localize o modelo [você baixou anteriormente](#obtaining-template) e toque ou clique **Upload**.

1. Depois de carregado, ele aparece na lista de modelos disponíveis. Toque ou clique nele para selecioná-lo (o que também revela informações sobre o modelo na coluna direita) e toque ou clique **Próximo**.

   ![Selecione um modelo](assets/select-site-template.png)

1. Forneça um título para o seu site. Um nome de site pode ser fornecido ou será gerado a partir do título se omitido.

   * O título do site aparece na barra de título dos navegadores.
   * O nome do site se torna parte do URL.

1. Toque ou clique **Criar** e o novo site é criado a partir do modelo de site.

   ![Detalhes do novo site](assets/create-site-details.png)

1. Na caixa de diálogo de confirmação exibida, toque ou clique em **Concluído**.

   ![Caixa de diálogo de sucesso](assets/success.png)

1. No console de sites, os novos sites são visíveis e podem ser navegados para explorar sua estrutura básica, conforme definido pelo modelo.

   ![Nova estrutura de site](assets/new-site.png)

Os autores de conteúdo agora podem começar a criar.

## É Necessária Mais Personalização? {#customization-required}

Os modelos de site são muito eficientes e flexíveis e qualquer número pode ser criado para um projeto, permitindo variações de site de fácil criação. Dependendo do nível de personalização já executado no modelo de site que você usa, talvez você nem precise de personalização de front-end adicional.

* Se seu site não requer personalização adicional, parabéns! Sua jornada termina aqui!
* Se você ainda precisar de personalização de front-end adicional ou se simplesmente quiser entender o processo completo caso precise de personalização futura, continue lendo.

## Exemplo de página {#example-page}

Se você precisar de personalização de front-end adicional, lembre-se de que o desenvolvedor de front-end pode não estar familiarizado com os detalhes do seu conteúdo. Portanto, é uma boa ideia fornecer ao desenvolvedor um caminho para o conteúdo típico que possa ser usado como base de referência, à medida que o tema for personalizado. Um exemplo típico é a página inicial do idioma principal do site.

1. No navegador de sites, navegue até a página inicial do idioma principal do site e toque ou clique na página para selecioná-la e, em seguida, toque ou clique **Editar** na barra de menus.

   ![Página inicial típica](assets/home-page-in-console.png)

1. No editor, selecione o **Informações da página** na barra de ferramentas e **Exibir como publicado**.

   ![Edição da página inicial](assets/home-page-edit.png)

1. Na guia que é aberta, copie o caminho do conteúdo da barra de endereços. Será algo como `/content/<your-site>/en/home.html?wcmmode=disabled`.

   ![Página inicial](assets/home-page.png)

1. Salve o caminho para fornecer posteriormente ao desenvolvedor de front-end.

## Baixar o Tema {#download-theme}

Agora que o site foi criado, o tema do site como gerado pelo modelo pode ser baixado e fornecido ao desenvolvedor de front-end para personalização.

1. No console Sites, mostre o **Site** trilho.

   ![Mostrar painel de sites](assets/show-site-rail.png)

1. Toque ou clique na raiz do novo site e toque ou clique em **Baixar Fontes de Tema** no painel do site.

   ![Baixar fontes de tema](assets/download-theme-sources.png)

Agora você tem uma cópia dos arquivos de origem do tema nos arquivos de download.

## Configurar usuário proxy {#proxy-user}

Para que o desenvolvedor de front-end visualize as personalizações usando o conteúdo AEM real do site, é necessário configurar um usuário proxy.

1. Na AEM da navegação principal, acesse **Ferramentas** -> **Segurança** -> **Usuários**.
1. No console de gerenciamento de usuários, toque ou clique em **Criar**.

   ![Console de gerenciamento do usuário](assets/user-management-console.png)
1. No **Criar novo usuário** na janela você deve fornecer no mínimo:
   * **ID** - Anote esse valor, pois ele deve ser fornecido ao desenvolvedor front-end.
   * **Senha** - Salve esse valor com segurança em um cofre de senhas, pois ele deve ser fornecido ao desenvolvedor front-end.

   ![Detalhes do novo usuário](assets/new-user-details.png)

1. No **Grupos** , adicione o usuário proxy à guia `contributors` grupo.
   * Digitação no termo `contributors` dispara AEM recurso de autocompletar para facilitar a seleção do grupo.

   ![Adicionar ao grupo](assets/add-to-group.png)

1. Toque ou clique **Salvar e fechar**.

Agora você concluiu a configuração do . Os autores de conteúdo agora podem começar a criar conteúdo na preparação do site e começar a personalizar o front-end na próxima etapa da jornada.

## O que vem a seguir {#what-is-next}

Agora que você concluiu esta parte da jornada de Criação de Site Rápido de AEM, é necessário:

* Saiba como obter modelos de site AEM.
* Saiba como criar um novo site usando um modelo.
* Veja como baixar o modelo do seu novo site para fornecer ao desenvolvedor de front-end.

Crie com base nesse conhecimento e prossiga sua jornada de Criação de Site Rápido de AEM revisando o documento [Configurar o pipeline,](pipeline-setup.md) onde você criará um pipeline front-end para gerenciar a personalização do tema do site.

## Recursos adicionais {#additional-resources}

Embora seja recomendável seguir para a próxima parte da jornada de Criação Rápida de Site revisando o documento [Configurar o pipeline,](pipeline-setup.md) a seguir estão alguns recursos adicionais e opcionais que aprofundam alguns conceitos mencionados neste documento, mas não é necessário que eles continuem na jornada.

* [Modelo de Site Padrão AEM](https://github.com/adobe/aem-site-template-standard) - Este é o repositório GitHub do modelo de site padrão do AEM.
* [Criar e organizar páginas](/help/sites-cloud/authoring/fundamentals/organizing-pages.md) - Este guia detalha como gerenciar páginas do seu AEM Site se você quiser personalizá-lo ainda mais após criá-lo a partir do modelo.
* [Como trabalhar com o pacote](/help/implementing/developing/tools/package-manager.md) - Os pacotes permitem a importação e exportação de conteúdo do repositório. Este documento explica como trabalhar com pacotes no AEM 6.5, que também se aplica ao AEMaaCS.
* [Documentação de administração do site](/help/sites-cloud/administering/site-creation/create-site.md) - Consulte os documentos técnicos sobre a criação do site para obter mais detalhes sobre os recursos da ferramenta de Criação rápida de sites.
