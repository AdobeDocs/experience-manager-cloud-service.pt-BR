---
title: Ativação de recursos progressivos do aplicativo web
description: O AEM Sites permite que o autor de conteúdo ative recursos progressivos do aplicativo da Web para qualquer site por meio de uma configuração simples, em vez de codificação.
translation-type: tm+mt
source-git-commit: f130fe34e5c57b9fc78697374a5a9772da3c4c17
workflow-type: tm+mt
source-wordcount: '2032'
ht-degree: 0%

---


# Ativar recursos progressivos do aplicativo web {#enabling-pwa}

Por meio de uma configuração simples, um autor de conteúdo agora pode ativar recursos progressivos do aplicativo da Web (PWA) para experiências criadas no AEM Sites.

>[!CAUTION]
>
>Este é um recurso avançado que requer:
>
>* Conhecimento do PWA
>* Conhecimento do seu site e estrutura de conteúdo
>* Noções básicas sobre estratégias de armazenamento em cache
>* Suporte da sua equipe de desenvolvimento

>
>
Antes de usar esse recurso, é recomendável discutir isso com a equipe de desenvolvimento para definir a melhor maneira de aproveitá-lo para o seu projeto.

>[!NOTE]
>
>Os recursos descritos neste documento estão planejados para serem disponibilizados com a [versão de março de 2021 do AEM como Cloud Service.](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html)

## Introdução {#introduction}

[Os aplicativos web progressivos (PWA)](https://developer.mozilla.org/en-US/docs/Web/Progressive_web_apps) permitem experiências semelhantes a aplicativos imersivos para sites de AEM, permitindo que eles sejam armazenados localmente na máquina do usuário e sejam acessíveis offline. Um usuário pode navegar em um site em qualquer lugar, mesmo perdendo uma conexão com a Internet. O PWA permite experiências ininterruptas, mesmo que a rede seja perdida ou instável.

Em vez de exigir qualquer recodificação do site, um autor de conteúdo pode configurar as propriedades do PWA como uma guia adicional nas [propriedades da página](/help/sites-cloud/authoring/fundamentals/page-properties.md) de um site.

* Quando salva ou publicada, essa configuração aciona um manipulador de eventos que grava os [arquivos manifest](https://developer.mozilla.org/en-US/docs/Web/Manifest) e [service worker](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API) que ativam os recursos do PWA no site.
* Os mapeamentos Sling também são mantidos para garantir que o trabalhador de serviço seja disponibilizado a partir da raiz do aplicativo para ativar o conteúdo de proxy, permitindo recursos offline no aplicativo.

Com o PWA, o usuário tem uma cópia local do site, dando uma experiência semelhante ao aplicativo mesmo sem uma conexão com a Internet.

>[!NOTE]
>
>Aplicativos da Web progressivos são uma tecnologia em evolução e suporte para instalação de aplicativos locais e outros recursos [dependem de qual navegador você usa.](https://developer.mozilla.org/en-US/docs/Web/Progressive_web_apps/Installable_PWAs#Summary)

## Pré-requisitos {#prerequisites}

Para poder usar os recursos do PWA para o seu site, há dois requisitos para o ambiente do projeto:

1. [Use ](#adjust-components) os Componentes principais para aproveitar esse recurso
1. [Ajuste as regras do ](#adjust-dispatcher) dispatcher para expor os arquivos necessários

Essas são etapas técnicas que o autor precisará coordenar com a equipe de desenvolvimento. Essas etapas são necessárias apenas uma vez por site.

### Usar componentes principais {#adjust-components}

Os Componentes principais versão 2.15.0 e posteriores são compatíveis com os recursos do PWA dos sites de AEM. Como o AEMaaCS sempre inclui a versão mais recente dos Componentes principais, você pode aproveitar os recursos do PWA prontos para uso. Seu projeto AEMaaCS atende automaticamente a esse requisito.

>[!NOTE]
>
>O Adobe não recomenda usar os recursos do PWA em componentes personalizados ou componentes não [estendidos dos Componentes principais.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html)
<!--
Your components need to include the [manifest files](https://developer.mozilla.org/en-US/docs/Web/Manifest) and [service worker,](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API) which supports the PWA features.

 To do this, the developer will need to add the following link to the `customheaderlibs.html` file of your page component.

```xml
<link rel="manifest" href="/content/<projectName>/manifest.webmanifest" crossorigin="use-credentials"/>
```

The developer will also need to add the following link to the `customfooterlibs.html` file of your page component.

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
-->

### Ajuste seu Dispatcher {#adjust-dispatcher}

O recurso PWA gera e usa arquivos `/content/<sitename>/manifest.webmanifest`. Por padrão, [o dispatcher](/help/implementing/dispatcher/overview.md) não expõe esses arquivos. Para expor esses arquivos, o desenvolvedor deve adicionar a seguinte configuração ao projeto do site.

```text
File location: [project directory]/dispatcher/src/conf.dispatcher.d/filters/filters.any >

# Allow webmanifest files
/0102 { /type "allow" /extension "webmanifest" /path "/content/*/manifest" }
```

Dependendo do seu projeto, talvez você queira incluir diferentes tipos de extensões para as regras de regravação. A extensão `webmanifest` pode ser útil para incluir nas condições de regravação quando você introduz uma regra que oculta e redireciona solicitações para `/content/<projectName>`.

```text
RewriteCond %{REQUEST_URI} (.html|.jpe?g|.png|.svg|.webmanifest)$
```

## Ativar o PWA para seu site {#enabling-pwa-for-your-site}

Com [os pré-requisitos](#prerequisites) atendidos, é muito fácil para um autor de conteúdo habilitar os recursos do PWA para um site. Veja a seguir um esboço básico de como fazer isso. As opções individuais são detalhadas na seção [Opções detalhadas.](#detailed-options)

1. Faça logon no AEM.
1. No menu principal, toque ou clique em **Navegação** -> **Sites**.
1. Selecione o projeto do site e toque ou clique em [**Propriedades**](/help/sites-cloud/authoring/fundamentals/page-properties.md) ou use a tecla de atalho `p`.
1. Selecione a guia **Progressive Web App** e configure as propriedades aplicáveis. No mínimo, você desejará:
   1. Selecione a opção **Ativar PWA**.
   1. Defina o **URL de inicialização**.

      ![Ativar PWA](../assets/pwa-enable.png)

   1. Carregue um ícone de png de 512x512 no DAM e faça referência a ele como o ícone do aplicativo.

      ![Ícone PWA](../assets/pwa-icon.png)

   1. Configure os caminhos que deseja que o trabalhador do serviço fique offline. Os caminhos típicos são:
      * `/content/<sitename>`
      * `/content/experiencefragements/<sitename>`
      * `/content/dam/<sitename>`
      * Qualquer referência de fonte de terceiros
      * `/etc/clientlibs/<sitename>`

      ![Definir caminhos de PWA offline](../assets/pwa-offline.png)


1. Toque ou clique em **Salvar e fechar**.

Seu site agora está configurado e você pode [instalá-lo como um aplicativo local.](#using-pwa-enabled-site)

## Usando seu site habilitado para PWA {#using-pwa-enabled-site}

Agora que você configurou [o site para oferecer suporte ao PWA,](#enabling-pwa-for-your-site) você pode experimentá-lo por conta própria.

1. Acesse o site em um navegador compatível [.](https://developer.mozilla.org/en-US/docs/Web/Progressive_web_apps/Installable_PWAs#Summary)
1. Você verá um novo ícone na barra de endereços do navegador, indicando que o site pode ser instalado como um aplicativo local.
   * Dependendo do navegador, o ícone pode variar e o navegador também pode exibir uma notificação (como um banner ou caixa de diálogo) indicando que é possível instalar como um aplicativo local.
1. Instale o aplicativo.
1. O aplicativo será instalado na tela inicial do dispositivo.
1. Abra o aplicativo, navegue um pouco e veja se as páginas estão disponíveis offline.

## Opções detalhadas {#detailed-options}

A seção a seguir fornece mais detalhes sobre as opções disponíveis ao [configurar seu site para PWA.](#enabling-pwa-for-your-site)

### Configurar experiência instalável {#configure-installable-experience}

Essas configurações permitem que o site se comporte como um aplicativo nativo, tornando-o instalável na tela inicial do visitante e disponível offline.

* **Ativar PWA**  - Este é o botão principal para ativar o PWA para o site.
* **URL de inicialização**  - esse é o  [URL de início preferido ](https://developer.mozilla.org/en-US/docs/Web/Manifest/start_url) que o aplicativo abrirá quando o usuário carregar o aplicativo instalado localmente.
   * Pode ser qualquer caminho na estrutura do conteúdo.
   * Essa não precisa ser a raiz e geralmente é uma página de boas-vindas dedicada ao aplicativo.
   * Se esse URL for relativo, o URL de manifesto será usado como URL base para resolvê-lo.
   * Quando deixado em branco, o recurso usa o endereço da página da Web da qual o aplicativo Web foi instalado.
   * É recomendável definir um valor.
* **Modo de exibição**  - Um aplicativo habilitado para PWA ainda é um site AEM fornecido por um navegador. [Essas opções de exibição ](https://developer.mozilla.org/en-US/docs/Web/Manifest/display) definem como o navegador deve ser oculto ou apresentado de outra forma ao usuário no dispositivo local.
   * **Independente**  - O navegador é completamente oculto do usuário e parece ser um aplicativo nativo. Este é o valor padrão.
      * Com essa opção, a navegação do aplicativo deve ser totalmente possível por meio do conteúdo, usando links e componentes nas páginas do site, sem usar os controles de navegação do navegador.
   * **Navegador**  - O navegador é exibido como normalmente seria ao visitar o site.
   * **Interface do usuário mínima** : o navegador é oculto, como um aplicativo nativo, mas os controles básicos de navegação são expostos.
   * **Tela cheia**  - o navegador é completamente oculto, como um aplicativo nativo, mas é renderizado no modo de tela cheia.
      * Com essa opção, a navegação do aplicativo deve ser totalmente possível por meio do conteúdo, usando links e componentes nas páginas do site, sem usar os controles de navegação do navegador.
* **Orientação da tela**  - Como um aplicativo local, o PWA precisa saber como lidar com as orientações  [do dispositivo.](https://developer.mozilla.org/en-US/docs/Web/Manifest/orientation)
   * **Qualquer**  - O aplicativo se ajusta à orientação do dispositivo do usuário. Este é o valor padrão.
   * **Retrato**  - força o aplicativo a ser aberto no layout de retrato, independentemente da orientação do dispositivo do usuário.
   * **Paisagem**  - Isso força o aplicativo a ser aberto no layout de paisagem, independentemente da orientação do dispositivo do usuário.
* **Cor do tema**  - Define a  [cor do ](https://developer.mozilla.org/en-US/docs/Web/Manifest/theme_color) aplicativo que afeta a forma como o sistema operacional do usuário local exibe a barra de ferramentas da interface do usuário nativa e os controles de navegação. Dependendo do navegador, pode afetar outros elementos de apresentação do aplicativo.
   * Use o pop-up de poço de cores para selecionar uma cor.
   * A cor também pode ser definida por valor hexadecimal ou RGB.
* **Cor do plano de fundo**  - Define a cor do  [plano de fundo do aplicativo, ](https://developer.mozilla.org/en-US/docs/Web/Manifest/background_color) que é exibida quando o aplicativo é carregado.
   * Use o pop-up de poço de cores para selecionar uma cor.
   * A cor também pode ser definida por valor hexadecimal ou RGB.
   * Determinados navegadores [criam uma tela inicial automaticamente](https://developer.mozilla.org/en-US/docs/Web/Manifest#Splash_screens) a partir do nome do aplicativo, da cor de fundo e do ícone.
* **Ícone**  - Isso define  [o ](https://developer.mozilla.org/en-US/docs/Web/Manifest/icons) ícone que representa o aplicativo no dispositivo do usuário.
   * O ícone deve ser um arquivo png de tamanho 512x512 pixels.
   * O ícone deve ser [armazenado no DAM.](/help/assets/overview.md)

### Gerenciamento de cache (avançado) {#offline-configuration}

Essas configurações disponibilizam partes deste site offline e localmente no dispositivo do visitante. Isso permite controlar o cache do aplicativo da Web para otimizar as solicitações de rede e oferecer suporte a experiências offline.

* **Estratégia de armazenamento em cache e frequência de atualização de conteúdo**  - Essa configuração define o modelo de armazenamento em cache para o seu PWA.
   * **Moderadamente**  -  [essa ](https://web.dev/stale-while-revalidate/) configuração é o caso da maioria dos sites e é o valor padrão.
      * Com essa configuração, o conteúdo visualizado pela primeira vez pelo usuário será carregado do cache e, enquanto o usuário estiver consumindo esse conteúdo, o restante do conteúdo no cache será revalidado.
   * **Frequentemente**  - Esse é o caso de sites que precisam de atualizações para serem muito rápidos, como leiloeiros.
      * Com essa configuração, o aplicativo buscará primeiro o conteúdo mais recente por meio da rede e, se não estiver disponível, retornará ao cache local.
   * **Raramente**  - Esse é o caso para sites que são quase estáticos, como páginas de referência.
      * Com essa configuração, o aplicativo procurará primeiro o conteúdo no cache e, se não estiver disponível, recorrerá à rede para recuperá-lo.
* **Pré-armazenamento em cache de arquivos**  - Esses arquivos hospedados em AEM serão salvos no cache do navegador local quando o trabalhador do serviço estiver instalando e antes de serem usados. Isso garante que o aplicativo Web esteja totalmente funcional quando estiver offline.
* **Inclusões de caminhos**  - As solicitações de rede para os caminhos definidos são interceptadas e o conteúdo em cache é retornado de acordo com a estratégia de  **Cache configurada e a frequência de atualização** do conteúdo.
* **Exclusões de cache**  - Esses arquivos nunca serão armazenados em cache, independentemente das configurações em Pré- **armazenamento em cache do** arquivo e Inclusões de  **caminho**.

>[!TIP]
>
>Sua equipe de desenvolvedores provavelmente tem informações importantes sobre como a configuração offline deve ser configurada.

## Limitações e Recommendations {#limitations-recommendations}

Nem todos os recursos do PWA estão disponíveis para o AEM Sites. Essas são algumas limitações notáveis.

* As páginas não são sincronizadas ou atualizadas automaticamente se o usuário não estiver usando o aplicativo.

O Adobe também faz as seguintes recomendações ao implementar o PWA.

### Minimize o número de recursos para pré-armazenar em cache. {#minimize-precache}

O Adobe aconselha a limitar o número de páginas a serem pré-armazenadas em cache.

* Incorpore bibliotecas para reduzir o número de entradas para gerenciar ao pré-armazenar em cache.
* Limite o número de variações de imagem para pré-cache.

### Ative o PWA depois que os scripts do projeto e as folhas de estilos estiverem estabilizados. {#pwa-stabilized}

As bibliotecas de clientes são entregues com a adição de um seletor de cache observando o seguinte padrão `lc-<checksumHash>-lc`. Toda vez que um dos arquivos (e dependências) que compõe uma alteração de biblioteca, esse seletor é alterado. Se você listou uma biblioteca do cliente para ser pré-armazenada em cache pelo trabalhador do serviço e deseja fazer referência a uma nova versão, recupere e atualize manualmente a entrada. Como resultado, recomendamos que você configure o site para ser um PWA depois que os scripts do projeto e as folhas de estilos estiverem estabilizados.

### Minimize o número de variações de imagem. {#minimize-variations}

O Componente de imagem dos Componentes principais do AEM determina em um dos front-end a melhor representação para buscar. Esse mecanismo também inclui um carimbo de data e hora que corresponde à hora da última modificação desse recurso. Esse mecanismo complica a configuração do pré-cache do PWA.

Ao configurar o pré-cache, o usuário precisa listar todas as variações de caminho que podem ser buscadas. Essas variações são compostas de parâmetros como qualidade e largura. É fortemente aconselhável reduzir o número destas variações para um máximo de três - pequenas, médias e grandes. Você pode fazer isso através da caixa de diálogo da política de conteúdo do [Componente de imagem.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/image.html)

Se não for configurado com cuidado, o consumo de memória e de rede pode afetar seriamente o desempenho do seu PWA. Além disso, se você pretende realizar o pré-cache, digamos, 50 imagens, e tiver 3 larguras por imagem, o usuário que mantém o site terá que manter uma lista de até 150 entradas na seção pré-cache do PWA das propriedades da página.

O Adobe também aconselha você a configurar seu site como um PWA após a estabilização do uso de imagens do projeto.
