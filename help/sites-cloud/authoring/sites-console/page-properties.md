---
title: Propriedades da página
description: Saiba mais sobre as diferentes propriedades que uma página pode ter, como elas controlam o comportamento da página e como ela é gerenciada.
exl-id: 27521a6d-c6e9-4f43-9ddf-9165b0316084
solution: Experience Manager Sites
feature: Authoring
role: User
mini-toc-levels: 2
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '2138'
ht-degree: 33%

---


# Propriedades da página {#page-properties}

Saiba mais sobre as diferentes propriedades que uma página pode ter, como elas controlam o comportamento da página e como ela é gerenciada.

>[!TIP]
>
>Para obter detalhes sobre como editar e alterar as propriedades de uma página, consulte o documento [Editando Propriedades da Página.](/help/sites-cloud/authoring/sites-console/edit-page-properties.md)

## Visão geral e disponibilidade de propriedade {#overview}

As propriedades de página podem controlar muitos aspectos de uma página, desde o título e a identidade visual até suas permissões. As propriedades são distribuídas por várias guias, algumas podem estar ocultas, dependendo do tipo de página. Como a maioria das propriedades no AEM, as [propriedades de página podem ser herdadas.](/help/sites-cloud/authoring/sites-console/edit-page-properties.md#inheritance)

>[!NOTE]
>
>Este documento descreve todas as propriedades de página possíveis. Dependendo do tipo de página, nem todas as propriedades estarão disponíveis.

## Guia Básico {#basic}

### Título e tags {#title-tags}

* **Título** - Define o metatítulo da página para fins de SEO, bem como o título exibido no conteúdo da página (a menos que seja substituído)

   * O título da página é mostrado em vários locais na interface do usuário do AEM, incluindo as exibições de cartão/lista do **Sites** no [Console do Sites.](/help/sites-cloud/authoring/sites-console/introduction.md)
   * Este campo é obrigatório.

* **Marcas** - Define as metatags da página para fins de SEO

   * Você pode adicionar ou remover tags da página, atualizando a lista na caixa de seleção.
   * Use o menu suspenso para selecionar a partir de tags existentes.
   * Após selecionar uma tag, ela é listada abaixo da caixa de seleção. Você pode remover uma tag dessa lista usando o ícone “x”.
   * Uma tag totalmente nova pode ser inserida digitando o nome em uma caixa de seleção vazia.

      * A nova tag é criada ao pressionar Enter.
      * A nova tag será então exibida com uma pequena estrela à direita, indicando que é uma tag nova.

   * Um “x” é exibido ao passar o mouse sobre uma entrada de tag na caixa de seleção, e esse ícone pode ser usado para remover a tag desta página.
   * Para obter mais informações sobre marcas, consulte [Usando a Marca.](/help/sites-cloud/authoring/sites-console/tags.md)

* **Ocultar na Navegação** - Indica se a página está visível ou oculta na navegação de página do site resultante

### Identidade visual {#branding}

Aplique uma identidade de marca consistente em todas as páginas, anexando uma descrição da marca a cada título de página. Essa funcionalidade requer o uso do Componente de página da versão 2.14.0 ou posterior do [Componentes principais.](https://experienceleague.adobe.com/pt-br/docs/experience-manager-core-components/using/introduction)

* **Descrição da marca**

   * **Sobrepor**: marque essa opção para definir a descrição da marca nesta página.

      * O valor é herdado por todas as páginas filhas, a menos que elas também tenham seus valores de **Sobreposição** definidos.

   * **Substituir valor** - o texto da descrição da marca a ser anexado ao título da página.

      * O valor é anexado ao título da página após um caractere de barra vertical, como `Cycling Tuscany | Always ready for the WKND`

### ID HTML {#html-id}

* **ID** - a ID HTML a ser aplicada ao componente.

### Mais títulos e descrições {#more-titles}

* **Título da página** - Um título a ser usado na página

   * Normalmente, é usado por componentes de título.
   * Se estiver vazio, a variável **Título** é usada.

* **Título de Navegação** - Você pode especificar um título separado para usar na navegação (por exemplo, se desejar algo mais conciso).

   * Se estiver vazio, o **Título da página** será usado.

* **Subtítulo** - Uma subtítulo para usar na página
* **Descrição** - Sua descrição da página, a finalidade dela ou qualquer outro detalhe que desejar adicionar

### Horário ligado/desligado {#on-off-time}

O horário de ativação/desativação de uma página é uma maneira conveniente de ocultar temporariamente um conteúdo já publicado. O conteúdo permanece na instância de publicação quando está desativado. Desativar uma página não cancela a publicação do conteúdo.

* **Momento da ativação**: a data e a hora em que a página publicada ficará visível (renderizada) no ambiente de publicação. A página deve estar publicada, seja manualmente ou por replicação automática pré-configurada.

   * Se já [publicada](/help/sites-cloud/authoring/sites-console/publishing-pages.md), esta página estará disponível na instância de publicação, mas permanecerá inativa (oculta) até a renderização no horário especificado.
   * Se não for publicada e [estiver configurada para replicação automática](/help/operations/replication.md#on-and-off-times-trigger-configuratio), a página será publicada automaticamente e, em seguida, renderizada no horário especificado.
   * Se não for publicada e não estiver configurada para replicação automática, a página não será publicada automaticamente. Um 404 é exibido quando é feita uma tentativa de acessar a página.

* **Momento da desativação**: semelhante e frequentemente usado em combinação com o **Momento da ativação**, define o momento em que a página publicada fica oculta no ambiente de publicação.

Deixe esses campos (**Momento da ativação** e **Momento da desativação**) vazios para páginas que deseja publicar e que estão disponíveis imediatamente e no ambiente de publicação até que sejam desativadas (o cenário normal).

>[!NOTE]
>Se o **Momento da ativação** ou **Momento da desativação** estiverem no passado e a replicação automática estiver configurada, então a ação relevante será acionada imediatamente.

>[!TIP]
>
>Os tempos de ativação/desativação lidam estritamente com o conteúdo já publicado (manualmente ou por replicação automática). Por esse motivo, fluxos de trabalho de publicação, como aqueles para aprovação de conteúdo, não são acionados por horários de ativação/desativação e horários de ativação/desativação não afetam o status de publicação da página. Por esse motivo, os horários de ativação/desativação são mais apropriados para mostrar/ocultar temporariamente um conteúdo já aprovado e publicado.
>
>Se quiser publicar conteúdo novo com todos os fluxos de trabalho associados ou remover totalmente (cancelar a publicação do conteúdo) do site, considere [gerenciar sua publicação.](/help/sites-cloud/authoring/sites-console/publishing-pages.md#manage-publication)

### URL personalizado {#vanity-url}

Essa propriedade permite inserir um URL personalizado para esta página, o que pode permitir que você tenha um URL mais curto e/ou mais expressivo. Por exemplo, se o URL personalizado estiver definido como `welcome` para a página identificada pelo caminho`/v1.0/startpage` para o site `http://example.com`, em seguida, `http://example.com/welcome`será o URL personalizado de `http://example.com/content/v1.0/startpage`

>[!CAUTION]
>
>URLs personalizados:
>
>* Deve ser única.
>* Não é compatível com padrões de regex.
>* Não deve ser definido como uma página existente.

* **Adicionar** - Selecione para mostrar um campo e definir uma URL personalizada para a página.
   * Selecione novamente para adicionar vários.
   * Selecione o ícone **Remover** para excluir a URL personalizada.
* **Redirecionar URL personalizado** - Indica se você deseja que a página use a URL personalizado ou redirecione para a URL real da página

## Avançado {#advanced}

### Configurações {#settings}

* **Idioma** - o idioma da página
* **Raiz de idioma** - deve ser marcado se a página for a raiz de uma cópia no idioma de destino
* **Redirecionar** - Indica a página para a qual esta página deve ser redirecionada automaticamente com o status `302 Found` do HTML
   * **Redirecionamento permanente** — quando marcado, a página redireciona para o caminho de destino fornecido junto com um status HTML `301 Moved Permanently`.
* **Design**
* **Pseudônimo** - especifica um pseudônimo para ser usado com esta página
   * Por exemplo: se você definir um pseudônimo de `private` para a página `/content/wknd/us/en/magazine/members-only`, essa página poderá ser acessada por meio de `/content/wknd/us/en/magazine/private`
   * A criação de um pseudônimo define a propriedade de `sling:alias` no nó da página, que afeta apenas o recurso, não o caminho do repositório.
   * Páginas acessadas por pseudônimos no editor não podem ser publicadas. As [Opções de publicação](/help/sites-cloud/authoring/sites-console/publishing-pages.md) no editor só estão disponíveis para páginas acessadas por meio de seus caminhos de fato.
   * Consulte [Nomes de página localizados em SEO e Práticas recomendadas de gerenciamento de URL](/help/overview/seo-and-url-management.md#localized-page-names) para obter mais informações.

### Configuração {#configuration}

* **Herdado de &lt;caminho>** - Habilitar/desabilitar herança da **Configuração da Nuvem** para a página
   * Alterna a disponibilidade da **Configuração na Nuvem** para edição

* **Configuração da nuvem**: o caminho para a configuração selecionada

### Configurações do modelo {#template-settings}

* **Modelos permitidos**: [define a lista de modelos que estão disponíveis](/help/sites-cloud/authoring/page-editor/templates.md#enabling-and-allowing-a-template-template-author) dentro desta sub-ramificação
   * Cada valor deve ser um caminho absoluto para um modelo.
   * Use `/.*` para permitir todos os modelos abaixo deste caminho.
* **Usar Página como Modelo** - [Criar um novo modelo com base na página atual.](/help/sites-cloud/authoring/universal-editor/templates.md)
   * Aplica-se somente a páginas criadas para uso com o Editor universal que utiliza o Edge Delivery Services.

### Requisitos de autenticação {#authentication}

* **Habilitar** - Habilita o uso de autenticação para acessar a página

>[!NOTE]
>
>Os grupos de usuários fechados para a página são definidos na guia **[Permissões](#permissions)**.

* **Página de logon** - a página a ser usada para logon

### Exportar {#export}

* **Exportar configuração** - especifica uma configuração de exportação

## SEO {#seo}

* **URL canônica** - Usada para substituir a URL canônica da página
   * Se deixado em branco, o URL da página será o URL canônico.

* **Marcas de robôs** - Use a lista suspensa para selecionar as marcas de robôs e controlar o comportamento dos rastreadores do mecanismo de pesquisa
   * Algumas opções são conflitantes entre si, nesse caso, a opção mais permissiva tem precedência.

* **Gerar Mapa do Site** - Quando selecionado, um `sitemap.xml` é gerado para esta página e seus descendentes.

## Imagens {#images}

### Imagem em destaque {#featured-image}

Esta seção é usada para selecionar e configurar a imagem a ser apresentada. Isso é usado em componentes que fazem referência à página; por exemplo, teasers, listas de páginas etc.

* **Imagem** - Você pode **Escolher** um ativo ou procurar um arquivo para carregar e, em seguida, **Editar** ou **Limpar** a imagem selecionada.
* **Texto Alternativo** - Um texto usado para representar o significado e/ou função da imagem, normalmente usado por leitores de tela
* **Herdar - Valor retirado do ativo DAM** - Quando marcado, o texto alternativo é preenchido com o valor dos `dc:description`metadados no DAM.

### Miniatura  {#thumbnail}

Esta seção é usada para selecionar e configurar a miniatura da imagem para a página. Isso é usado em componentes que fazem referência à página; por exemplo, teasers, listas de páginas etc.

* **Gerar visualização** - gere uma visualização da página para usar como miniatura
* **Fazer upload da imagem** - faça upload de uma imagem para usar como miniatura
* **Selecionar imagem** - Selecione um ativo existente para usar como miniatura
* **Reverter** - esta opção fica disponível após você ter feito uma alteração na miniatura. Se você não quiser manter a alteração, poderá revertê-la antes de salvar.

## Cloud Services {#cloud-services}

* **Configurações do Cloud Service** - Define qual configuração é usada para os serviços em nuvem na página
* **Herdado de** - Para Live Copies e Cópias de idioma, as configurações de nuvem são herdadas por padrão do Blueprint.
   * Desmarcar para substituir a herança

## Personalização {#personalization}

### Configurações do ContextHub {#contexthub-config}

* **Caminho do ContextHub** - defina a [configuração do ContextHub](/help/sites-cloud/authoring/personalization/contexthub.md)
* **Caminho dos segmentos** - defina o [Caminho dos segmentos](/help/sites-cloud/authoring/personalization/contexthub-segmentation.md)

### Configuração de direcionamento {#targeting-config}

* **Marca** - Define uma [Marca para especificar um escopo para Direcionamento](/help/sites-cloud/authoring/personalization/targeted-content.md)
   * Esta opção requer que a conta de usuário esteja no grupo `Target Administrators`.

## Permissões {#permissions}

Use a guia **Permissões** para definir quais usuários, grupos ou [grupos de usuários fechados (CUGs)](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/advanced/closed-user-groups.html?lang=pt-BR) podem acessar e/ou modificar a página.

* **Adicionar permissões**
* **Editar grupo de usuários fechado**
* Exibir as **Permissões ativas**

## Blueprint {#blueprint}

Essa guia só fica visível para páginas que servem como blueprints. Os blueprints servem como base para as Live Copies que fazem parte do [Gerenciamento de vários sites.](/help/sites-cloud/administering/msm/overview.md)

* **Implantação** - Inicie uma implantação do conteúdo do blueprint nas Live Copies
* **Visão geral da Live Copy** - Abra uma janela para navegar pela estrutura da página da Live Copy
* **Live Copies atuais** - Uma lista de páginas baseadas na (ou seja, são Live Copies da) página de blueprint selecionada

## Live Copy {#live-copy}

Essa guia só fica visível para páginas configuradas como Live Copies. Assim como em [blueprints,](#blueprint) Live Copies fazem parte do [Gerenciamento de Vários Sites.](/help/sites-cloud/administering/msm/overview.md)

* **Sincronizar** - Sincronizar o Live Copy com o blueprint, mantendo as modificações locais
* **Redefinir** - Redefinir o Live Copy para o estado de blueprint, removendo as modificações locais
* **Suspender** - suspender modificações adicionais de implantação na Live Copy 
* **Desanexar** - Desanexar Live Copy do blueprint

### Origem {#source}

* Exibe o caminho do blueprint para esta Live Copy

### Status {#status}

* Lista o status atual da Live Copy da página

### Configuração {#live-copy-config}

* **Herança da Live Copy** - Se marcada, a configuração da Live Copy terá efeito em todas as páginas secundárias.
* **Herdar configurações de implantação da principal** - Se marcado, a configuração de implantação é herdada da página principal.
* **Escolher configuração de implantação**: define as circunstâncias em que as modificações são propagadas a partir do Blueprint e só estão disponíveis quando **Herdar configurações de implantação da página principal** não está selecionado
* **Lista de caminhos excluídos**

## Visualização {#preview}

Quando um [ambiente de visualização](/help/sites-cloud/authoring/sites-console/previewing-content.md) está habilitado, os seguintes detalhes ficam disponíveis:

* **URL de visualização** - A URL usada para acessar o conteúdo no ambiente de visualização

## Aplicativo web progressivo {#progressive-web-app}

Por meio de uma configuração simples, um autor de conteúdo pode ativar recursos do aplicativo web progressivo (PWA) para experiências criadas no AEM Sites. Seu site pode se comportar como um aplicativo nativo, tornando-o instalável na tela inicial do dispositivo dos visitantes e disponível offline.

{{pwa-deprecation}}

### Configurar experiência instalável {#config-pwa}

* **Habilitar PWA** - Quando habilitado, os visitantes da página podem instalar o site como um PWA.
* **URL de Inicialização** - URL que deve ser carregada quando o usuário inicia o aplicativo Web
   * Se o URL for relativo, o URL do manifest será usado como URL base para resolver
   * Quando vazio, o URL da página da qual o aplicativo foi instalado é usado.
   * É recomendável definir um valor.
* **Modo de Exibição** - Como o navegador deve ser oculto ou apresentado ao usuário no dispositivo local
* **Orientação da tela** - Como o PWA lidará com as orientações do dispositivo
* **Cor do tema** - A cor do aplicativo que afeta como o sistema operacional do usuário local exibe a barra de ferramentas da interface nativa e os controles de navegação
* **Cor do plano de fundo** - A cor do plano de fundo do aplicativo, mostrado quando o aplicativo é carregado
* **Ícone** - O ícone que representa o aplicativo no dispositivo do usuário quando o PWA é instalado

### Gerenciamento de cache (avançado) {#cache-management}

* **Estratégia de armazenamento em cache e frequência de atualização de conteúdo** - Define o modelo de armazenamento em cache da sua PWA.
* **Arquivos para armazenar em cache para uso offline**
   * **Pré-armazenamento em cache de arquivos (visualização técnica)** - Os arquivos hospedados no AEM são salvos no cache do navegador local quando o service worker está sendo instalado e antes de ser usado.
   * **Bibliotecas do lado do cliente** - Bibliotecas do lado do cliente para armazenar em cache para obter experiência offline
   * **Inclusões de caminho** - As solicitações de rede para os caminhos definidos são interceptadas e o conteúdo em cache é retornado de acordo com a Estratégia de cache e frequência de atualização de conteúdo configuradas
   * **Exclusões de caminho** - Esses arquivos nunca serão armazenados em cache, independentemente das configurações em Pré-armazenamento em cache de arquivos e Inclusões de caminho.

>[!NOTE]
>
>Consulte [Habilitar Recursos Progressivos do Aplicativo Web](/help/sites-cloud/authoring/sites-console/enable-pwa.md) para obter mais detalhes.

