---
title: Ativação de recursos progressivos do aplicativo da Web
description: A AEM Sites permite que o autor do conteúdo ative recursos progressivos do aplicativo da Web para qualquer site por meio de uma configuração simples em vez de codificação.
translation-type: tm+mt
source-git-commit: ba014bb90b1cb08630455b3ac72895272ae8ed5b
workflow-type: tm+mt
source-wordcount: '1725'
ht-degree: 0%

---


# Ativando recursos progressivos do aplicativo da Web {#enabling-pwa}

Por meio de uma configuração simples, um autor de conteúdo agora pode habilitar os recursos progressivos do aplicativo da Web (PWA) para experiências criadas no AEM Sites.

>[!CAUTION]
>
>Este é um recurso avançado que requer:
>
>* Conhecimento dos PWA
>* Conhecimento do seu site e estrutura de conteúdo
>* Compreensão das estratégias de armazenamento em cache
>* Suporte da sua equipe de desenvolvimento

>
>
Antes de usar esse recurso, é recomendável discutir isso com sua equipe de desenvolvimento para definir a melhor maneira de aproveitá-lo para o seu projeto.

## Introdução {#introduction}

[Aplicativos da Web progressivos (PWA)](https://developer.mozilla.org/en-US/docs/Web/Progressive_web_apps) permitem experiências imersivas semelhantes a aplicativos para sites AEM permitindo que eles sejam armazenados localmente na máquina do usuário e sejam acessíveis offline. Um usuário pode navegar em um site enquanto estiver em trânsito, mesmo se perder uma conexão com a Internet. Os PWA permitem experiências ininterruptas mesmo se a rede for perdida ou instável.

Em vez de exigir qualquer recodificação do site, um autor de conteúdo pode configurar as propriedades do PWA como uma guia adicional nas [propriedades da página](/help/sites-cloud/authoring/fundamentals/page-properties.md) de um site.

* Quando salva ou publicada, essa configuração aciona um manipulador de eventos que grava os [arquivos manifest](https://developer.mozilla.org/en-US/docs/Web/Manifest) e [service worker](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API) que ativam os recursos do PWA no site.
* O manifesto e o trabalhador do serviço são armazenados em [configuração sensível ao contexto](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/context-aware-configs.html) aplicável ao site. Os mapeamentos de sling também são mantidos para garantir que o funcionário de serviço seja servido da raiz do aplicativo para ativar o conteúdo de proxy, permitindo recursos offline no aplicativo.

Com o PWA, o usuário tem uma cópia local do site, oferecendo uma experiência semelhante ao aplicativo mesmo sem uma conexão com a Internet.

>[!NOTE]
>
>Aplicativos da Web progressivos são uma tecnologia em evolução e suporte para instalação de aplicativos locais e outros recursos [dependem de qual navegador você usa.](https://developer.mozilla.org/en-US/docs/Web/Progressive_web_apps/Installable_PWAs#Summary)

## Pré-requisitos {#prerequisites}

Para poder usar os recursos do PWA para o seu site, há dois requisitos para o ambiente do seu projeto:

1. [Ajuste seus ](#adjust-components) componentes para ativar este recurso
1. [Ajuste as regras do ](#adjust-dispatcher) dispatcherrules para expor os arquivos necessários

Essas são etapas técnicas que o autor precisará coordenar com a equipe de desenvolvimento. Essas etapas são necessárias apenas uma vez por site.

### Ajuste seus componentes {#adjust-components}

Seus componentes precisam incluir os [arquivos manifest](https://developer.mozilla.org/en-US/docs/Web/Manifest) e [funcionários de serviço,](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API) que oferecem suporte aos recursos do PWA.

Para fazer isso, o desenvolvedor precisará adicionar o seguinte link ao arquivo `customheaderlibs.html` do componente de sua página.

```xml
<link rel="manifest" href="/content/<projectName>/manifest.webmanifest" crossorigin="use-credentials"/>
```

O desenvolvedor também precisará adicionar o seguinte link ao arquivo `customfooterlibs.html` do componente de sua página.

```xml
<script>
        // Check that service workers are supported
        if ('serviceWorker' in navigator) {
            // Use the window load event to make sure the page load performs well
            window.addEventListener('load', () => {
                let serviceWorker = '/<projectName>sw.js';
                navigator.serviceWorker.register(serviceWorker);
            });
        }
</script>
```

>[!NOTE]
>
>As versões futuras dos [Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) incluirão esses recursos automaticamente. No entanto, se você usar componentes personalizados em vez dos Componentes principais, esses ajustes sempre serão necessários.

### Ajustar o Dispatcher {#adjust-dispatcher}

O recurso PWA gera e usa arquivos `/content/<sitename>/manifest.webmanifest`. Por padrão, [o dispatcher](/help/implementing/dispatcher/overview.md) não expõe esses arquivos. Para expor esses arquivos, o desenvolvedor deve adicionar a seguinte configuração ao projeto do site.

```text
File location: [project directory]/dispatcher/src/conf.dispatcher.d/filters/filters.any >

# Allow webmanifest files
/0102 { /type "allow" /extension "webmanifest" /path "/content/*/manifest" }
```

>[!NOTE]
>
>As versões futuras do [AEM Project Archetype](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=en#developing) incluirão esta configuração.

## Habilitando o PWA para seu site {#enabling-pwa-for-your-site}

Com [os pré-requisitos](#prerequisites) atendidos, é muito fácil para um autor de conteúdo habilitar os recursos do PWA para um site. A seguir está um esboço básico de como fazer isso. As opções individuais estão detalhadas na seção [Opções detalhadas.](#detailed-options)

1. Efetue login no AEM.
1. No menu principal, toque ou clique em **Navegação** -> **Sites**.
1. Selecione o projeto do seu site e toque ou clique em [**Propriedades**](/help/sites-cloud/authoring/fundamentals/page-properties.md) ou utilize a tecla de atalho `p`.
1. Selecione a guia **Aplicativo Web progressivo** e configure as propriedades aplicáveis. No mínimo, você desejará:
   1. Selecione a opção **Ativar PWA**.
   1. Defina o **URL de inicialização**.

      ![Ativar PWA](../assets/pwa-enable.png)

   1. Carregue um ícone de png de 512x512 no DAM e faça referência a ele como o ícone do aplicativo.

      ![Definir ícone PWA](../assets/pwa-icon.png)

   1. Configure os caminhos que deseja que o trabalhador do serviço fique offline. Os caminhos típicos são:
      * `/content/<sitename>`
      * `/content/experiencefragements/<sitename>`
      * `/content/dam/<sitename>`
      * Quaisquer referências de fontes de terceiros
      * `/etc/clientlibs/<sitename>`

      ![Definir caminhos offline PWA](../assets/pwa-offline.png)


1. Toque ou clique em **Salvar e fechar**.

Seu site agora está configurado e você pode [instalá-lo como um aplicativo local.](#using-pwa-enabled-site)

## Usando seu site habilitado para PWA {#using-pwa-enabled-site}

Agora que [configurou o site para suportar o PWA,](#enabling-pwa-for-your-site) pode experimentá-lo por conta própria.

1. Acesse o site em um [navegador suportado.](https://developer.mozilla.org/en-US/docs/Web/Progressive_web_apps/Installable_PWAs#Summary)
1. Você verá um ícone `+` na barra de endereços do navegador, indicando que o site pode ser instalado como um aplicativo local.
   * Dependendo do navegador, também pode exibir uma notificação (como um banner ou uma caixa de diálogo) indicando que é possível instalar como um aplicativo local.
1. Instale o aplicativo.
1. O aplicativo será instalado na tela inicial do seu dispositivo.
1. Abra o aplicativo, navegue um pouco e veja se as páginas estão disponíveis offline.

## Opções detalhadas {#detailed-options}

A seção a seguir fornece mais detalhes sobre as opções disponíveis quando [configurar seu site para o PWA.](#enabling-pwa-for-your-site)

### Configurar experiência instalável {#configure-installable-experience}

Essas configurações permitem que seu site se comporte como um aplicativo nativo, tornando-o instalável na tela inicial do visitante e disponível offline.

* **Ativar PWA**  - Esta é a opção principal para ativar o PWA para o site.
* **URL**  de inicialização - este é o  [URL ](https://developer.mozilla.org/en-US/docs/Web/Manifest/start_url) de start preferencial que o aplicativo abrirá quando o usuário carregar o aplicativo instalado localmente.
   * Isso pode ser qualquer caminho na sua estrutura de conteúdo.
   * Essa não precisa ser a raiz e, muitas vezes, é uma página de boas-vindas dedicada ao aplicativo.
   * Se esse URL for relativo, o URL manifest será usado como o URL base para resolvê-lo.
   * Quando deixado em branco, o recurso usa o endereço da página da Web da qual o aplicativo Web foi instalado.
   * É recomendável definir um valor.
* **Modo**  de exibição - Um aplicativo habilitado para PWA ainda é um site AEM fornecido por um navegador. [Essas ](https://developer.mozilla.org/en-US/docs/Web/Manifest/display) opções de exibição definem como o navegador deve ser oculto ou apresentado de outra forma ao usuário no dispositivo local.
   * **Autônomo** : o navegador está completamente oculto do usuário e é exibido como um aplicativo nativo. Esse é o valor padrão.
      * Com essa opção, a navegação do aplicativo deve ser possível por todo o conteúdo usando links e componentes nas páginas do site sem usar os controles de navegação do navegador.
   * **Navegador**  - o navegador é exibido como normalmente seria ao visitar o site.
   * **IU**  mínima - O navegador está oculto, como um aplicativo nativo, mas os controles básicos de navegação são expostos.
   * **Tela**  cheia - o navegador está completamente oculto, como um aplicativo nativo, mas é renderizado no modo de tela cheia.
      * Com essa opção, a navegação do aplicativo deve ser possível por todo o conteúdo usando links e componentes nas páginas do site sem usar os controles de navegação do navegador.
* **Orientação**  da tela: como um aplicativo local, o PWA precisa saber como lidar com as orientações  [do dispositivo.](https://developer.mozilla.org/en-US/docs/Web/Manifest/orientation)
   * **Qualquer**  um - O aplicativo se ajusta à orientação do dispositivo do usuário. Esse é o valor padrão.
   * **Retrato** : isso força o aplicativo a ser aberto no layout retrato, independentemente da orientação do dispositivo do usuário.
   * **Paisagem** : isso força o aplicativo a ser aberto no layout paisagem, independentemente da orientação do dispositivo do usuário.
* **Cor**  do tema: define a  [cor do ](https://developer.mozilla.org/en-US/docs/Web/Manifest/theme_color) aplicativo que afeta como o sistema operacional do usuário local exibe a barra de ferramentas da interface nativa e os controles de navegação. Dependendo do navegador, pode afetar outros elementos de apresentação do aplicativo.
   * Use o pop-up do poço de cores para selecionar uma cor.
   * A cor também pode ser definida por valor hexadecimal ou RGB.
* **Cor**  do plano de fundo: define a cor do  [plano de fundo do aplicativo, ](https://developer.mozilla.org/en-US/docs/Web/Manifest/background_color) que é exibida à medida que o aplicativo é carregado.
   * Use o pop-up do poço de cores para selecionar uma cor.
   * A cor também pode ser definida por valor hexadecimal ou RGB.
   * Determinados navegadores [criam uma tela de apresentação automaticamente](https://developer.mozilla.org/en-US/docs/Web/Manifest#Splash_screens) a partir do nome do aplicativo, da cor do plano de fundo e do ícone.
* **Ícone** : define  [o ](https://developer.mozilla.org/en-US/docs/Web/Manifest/icons) ícone que representa o aplicativo no dispositivo do usuário.
   * O ícone deve ser um arquivo png de tamanho 512x512 pixels.
   * O ícone deve ser [armazenado em DAM.](/help/assets/overview.md)

### Gerenciamento de cache (avançado) {#offline-configuration}

Essas configurações disponibilizam partes deste site offline e localmente no dispositivo do visitante. Isso permite controlar o cache do aplicativo da Web para otimizar as solicitações de rede e suportar experiências offline.

* **Estratégia de cache e frequência de atualização**  de conteúdo - Essa configuração define o modelo de cache para seu PWA.
   * **Moderadamente**  -  [Essa ](https://web.dev/stale-while-revalidate/) configuração é o caso da maioria dos sites e é o valor padrão.
      * Com essa configuração, o conteúdo visualizado pela primeira vez pelo usuário será carregado do cache e, enquanto o usuário estiver consumindo esse conteúdo, o restante do conteúdo no cache será revalidado.
   * **Frequentemente**  - Esse é o caso de sites que precisam de atualizações para serem muito rápidos, como leiloeiros.
      * Com essa configuração, o aplicativo procurará o conteúdo mais recente pela rede primeiro e, se não estiver disponível, voltará para o cache local.
   * **Raramente**  - Esse é o caso para sites que são quase estáticos, como páginas de referência.
      * Com essa configuração, o aplicativo procurará o conteúdo no cache primeiro e, se não estiver disponível, voltará para a rede para recuperá-lo.
* **Pré-cache**  de arquivos - esses arquivos hospedados em AEM serão salvos no cache local do navegador quando o trabalhador do serviço estiver instalando e antes de ser usado. Isso garante que o aplicativo da Web esteja totalmente funcional quando estiver offline.
* **Inclusões**  de caminhos - As solicitações de rede para os caminhos definidos são interceptadas e o conteúdo em cache é retornado de acordo com a estratégia de  **cache configurada e a frequência de atualização** do conteúdo.
* **Exclusões**  de cache - esses arquivos nunca serão armazenados em cache, independentemente das configurações em  **Arquivo pré-** cache e inclusões **de** Caminho.

>[!TIP]
>
>Sua equipe de desenvolvedores provavelmente tem informações importantes sobre como sua configuração offline deve ser configurada.

## Limitações           {#limitations}

Nem todos os recursos do PWA estão disponíveis para o AEM Sites. Estas são algumas limitações notáveis.

* Um usuário deve navegar na página pelo menos uma vez antes de ser armazenada em cache offline.
* As páginas não são sincronizadas ou atualizadas automaticamente se o usuário não estiver usando o aplicativo.
