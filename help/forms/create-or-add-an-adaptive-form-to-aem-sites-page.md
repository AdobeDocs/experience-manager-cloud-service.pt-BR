---
title: Criar ou adicionar um formulário adaptável à página do AEM Sites
description: Descubra como criar ou adicionar facilmente um formulário adaptável à sua página do AEM Sites. Conheça as técnicas passo a passo e as práticas recomendadas para integrar formulários dinâmicos e personalizáveis ao seu site, otimizando suas experiências digitais para obter o máximo impacto.
feature: Adaptive Forms
hide: true
hidefromtoc: true
source-git-commit: 7dc36220c1f12177037aaa79d864c1ec2209a301
workflow-type: tm+mt
source-wordcount: '1230'
ht-degree: 0%

---


# Criar ou adicionar um formulário adaptável à página do AEM Sites {#create-or-add-an-adaptive-form-to-aem-sites-page}

Com o AEM Forms, você pode incorporar facilmente formulários adaptáveis em suas páginas da Web. Isso permite que seus visitantes preencham e enviem formulários de maneira conveniente sem nunca sair da página em que estão. Ao fazer isso, eles podem se envolver facilmente com outros elementos do site enquanto interagem ativamente com o formulário.

Você pode aproveitar ao máximo esse recurso utilizando as seguintes opções:

* **Adicionar um formulário personalizado:** Crie um formulário totalmente novo do zero, adaptando-o especificamente às suas necessidades e preferências de design.

* **Aprimorar fragmentos de experiência:** Estenda o alcance de seus formulários adicionando-os aos Fragmentos de experiência de AEM, permitindo uma reutilização contínua em várias páginas ou sites.

* **Utilizar modelos aprovados:** Aproveite os modelos pré-aprovados para criar rapidamente formulários que se alinhem às diretrizes de marca e aos padrões de design de sua organização.

* **Adicionar formulários existentes:** Integre facilmente formulários que você já criou em seus sites, permitindo que os visitantes interajam diretamente com eles.

* **Adicionar vários formulários:**  Adicione vários formulários a uma página para fornecer várias opções aos usuários com base em suas preferências e requisitos. Eles podem combinar formulários totalmente novos do zero com formulários existentes.

Você pode usar o editor do AEM Sites para criar e adicionar rapidamente vários formulários às suas páginas do AEM Sites. Usar o editor do AEM Sites permite que os autores de conteúdo criem experiências de captura de dados perfeitas em uma página do Sites, usando o potencial dos componentes de formulários adaptáveis, incluindo comportamento dinâmico, validações, integração de dados e geração de documentos de registro e automação de processos comerciais. Ele também permite usar vários recursos de páginas do AEM Sites, como controle de versão, direcionamento, tradução e gerenciador de vários sites.

## Objetivo

* Saiba como criar um formulário adaptável usando o editor do AEM Sites e o fragmento de experiência
* Saiba como definir o layout e o tema de um Formulário adaptável adicionado a uma página do AEM Sites e
* Criar um formulário adaptável usando o editor do AEM Sites e o Fragmento de experiência


## Considerações {#consideration}

O AEM Forms fornece o Contêiner de formulário adaptável e os componentes Forms - Incorporar. Você pode usar o Contêiner de formulário adaptável para criar e adicionar um novo formulário em um Fragmento de experiência ou página do AEM Sites, enquanto o componente Adaptive Forms - Incorporar permite adicionar um formulário adaptável existente ou criar um novo formulário usando o editor Adaptive Forms.

Quando você usa o Contêiner de formulário adaptável para criar ou adicionar um formulário, os formulários são submetidos a tradução e localização por meio do fluxo de tradução do AEM Sites. Para cada idioma, uma cópia separada (cópia de idioma) da página de sites e os formulários correspondentes são gerados e, quando um autor de conteúdo modifica uma regra em um formulário na página principal, as mesmas alterações devem ser feitas em todas as cópias de idioma do formulário. O Contêiner de formulário adaptável também permite usar vários recursos das páginas do AEM Sites, como controle de versão, direcionamento, tradução e gerenciador de vários sites.

Ao criar ou adicionar um formulário usando o componente de incorporação do formulário adaptável, os formulários são submetidos a tradução e localização usando o fluxo de tradução do AEM Forms. Nesse caso, um único formulário é mantido e referenciado em todas as cópias de idioma das páginas do Sites. O componente de Formulário incorporado adaptável não fornece acesso a vários recursos de páginas do AEM Sites, como o, controle de versão, direcionamento, tradução e gerenciador de vários sites.


## Antes de você iniciar {#before-you-start}

+++  Ativar os Componentes principais adaptáveis do Forms para o seu ambiente

Certifique-se de que o [Os Componentes principais adaptáveis do Forms são ativados para o ambiente as a Cloud Service do AEM Forms](enable-adaptive-forms-core-components.md).

+++

+++ Ativar **[!UICONTROL Contêiner adaptável do Forms]

Para habilitar [!UICONTROL Contêiner adaptável do Forms] componente na política do modelo, execute as seguintes etapas:

1. Abra a página do AEM Sites para edição. Para abrir a página para edição, selecione a página e clique em Editar.
1. Abra o modelo da página Sites. Para abrir o template, vá para a [!UICONTROL Informações da página] ![Informações da página](/help/forms/assets/Smock_Properties_18_N.svg) > [!UICONTROL Editar modelo]. Ele abre o modelo correspondente no editor de modelos.
1. Na visualização Estrutura, clique no botão **[!UICONTROL Política]** ![Política](/help/forms/assets/Smock_FeedManagement_18_N.svg) ícone na barra de menus. No **[!UICONTROL Componentes permitidos]** e selecione o **[!UICONTROL Contêiner adaptável do Forms]**  na caixa de seleção **[Nome do projeto do arquétipo AEM] - Formulário adaptável**.
1. Clique em **[!UICONTROL Concluído]**.

>[!VIDEO](https://video.tv.adobe.com/v/3419370?quality=12&learn=on)

+++


+++  Adicionar bibliotecas de clientes Forms adaptáveis à sua página do AEM Sites

Para ativar a funcionalidade completa do componente de Contêiner adaptável do Forms, adicione as bibliotecas de clientes Customheaderlibs e Customfooterlibs à sua página do AEM Sites usando o pipeline de implantação. Para adicionar as bibliotecas:

1. Acesse e clone seu [Repositório Git do AEM Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/managing-code/repositories.html).
1. Abra a pasta Repositório Git da AEM Cloud Service em um editor de texto de plano. Por exemplo, Microsoft Visual Code.
1. Abra o `ui.apps/src/main/content/jcr_root/apps/[your-project]/components/page/.content.xml` para editar e anotar o valor de `sling:resourceSuperType`. Por exemplo, anote o valor `core/wcm/components/page/v3/page`.


   ![recurso sling](/help/forms/assets/slingresource.png)

1. Navegue até `  ui.apps\src\main\content\jcr_root\apps\[your-project]\components\page\` `ui.apps/src/main/content/jcr_root/apps` e crie uma estrutura de pastas idêntica ao valor anotado na etapa anterior. Por exemplo, se o valor for semelhante ao exemplo na etapa anterior, a estrutura do nó final será `ui.apps/src/main/content/jcr_root/apps/core/wcm/components/page/v3/page`

   ![estrutura de sobreposição](/help/forms/assets/overlaystructure.png)

1. Criar `customheaderlibs.html` e `customfooterlibs.html` Os arquivos na estrutura do nó criados na etapa anterior e adicione o seguinte conteúdo aos arquivos:

   ```
        //Customheaderlibs.html
        <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
        <sly data-sly-call="${clientlib.css @ categories='core.forms.components.runtime.all'}"/>
        </sly> 
   
        //customfooterlibs.html
        <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
        <sly data-sly-test="${!wcmmode.edit}" data-sly-call="${clientlib.js @ categories='core.forms.components.runtime.all', async=true}"/>
        </sly> 
   ```

1. [Executar o pipeline de implantação](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/site-creation/enable-front-end-pipeline.html) para implantar as bibliotecas de clientes no ambiente as a Cloud Service AEM.

+++

## Criar um Formulário adaptável {#create-an-adaptive-form-in-sites-editor-or-experience-fragment}

Você pode criar um formulário totalmente novo do zero, ajustando-o especificamente às suas necessidades e preferências de design, diretamente em uma página de sites AEM ou em um Fragmento de experiência. Para formulários de uso único, recomenda-se a criação direta em uma página de sites AEM, enquanto os Fragmentos de experiência são ideais para formulários que precisam ser reutilizados em várias páginas do site.

* [Criar um formulário em uma página do AEM Sites](#create-an-adaptive-form-in-sites-editor)
* [Criar um formulário em um Fragmento de experiência](#create-an-adaptive-form-in-experience-fragment)

### Criar um formulário em uma página do AEM Sites {#create-an-adaptive-form-in-sites-editor}

Você pode usar o componente de Contêiner de formulário adaptável no editor do AEM Sites para criar um formulário personalizado. O componente permite criar um formulário arrastando e soltando os componentes do formulário. Os componentes de formulário são baseados nos Componentes principais. Você pode personalizá-los facilmente de acordo com os requisitos de sua organização.

>[!VIDEO](https://video.tv.adobe.com/v/3419284?quality=12&learn=on)

Para criar um Formulário adaptável em uma página do Sites:

1. Abra a página do AEM Sites no modo de edição.
1. Arraste e solte a variável **[!UICONTROL Contêiner adaptável do Forms]** componente do Navegador de componentes para a página Sites. Ele cria um espaço na página para o formulário. Você pode usar o modo de layout para alterar o Tamanho do espaço do container.
1. Arraste e solte os Componentes principais do formulário adaptável no espaço do contêiner para criar o formulário.
1. Adicione o botão Submit.

Em seguida, defina a ação Enviar e as propriedades avançadas.

### Criar um formulário em um Fragmento de experiência {#create-an-adaptive-form-in-experience-fragment}

Você pode estender o alcance de seus formulários adicionando-os aos Fragmentos de experiência de AEM, permitindo uma reutilização contínua em várias páginas ou sites. Por exemplo, você pode incluir um formulário de inscrição de informativo em um Fragmento de experiência. Isso permite reutilizar convenientemente o fragmento em várias páginas do site, eliminando a necessidade de recriar o formulário repetidamente. Quaisquer atualizações ou modificações feitas no formulário de inscrição do boletim informativo no Fragmento de experiência são propagadas automaticamente para todas as páginas em que são utilizadas. Isso simplifica o processo e garante uma experiência perfeita para o usuário, simplificando o gerenciamento dos formulários de seu site.

Para criar um formulário adaptável em um fragmento de experiência:

## Alterar layout de um formulário adaptável {#change-layout-of-an-adaptive-form}

Na página AEM Sites, use o [Modo de layout](/help/sites-cloud/authoring/features/responsive-layout.md) para redimensionar um componente de Contêiner de formulário adaptável adicionado a uma página do AEM Sites.
