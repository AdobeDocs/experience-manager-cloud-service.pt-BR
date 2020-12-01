---
title: Renderização do servidor e do SPA
description: O uso da renderização do lado do servidor (SSR) em seu SPA pode acelerar a carga inicial da página e passar a renderização para o cliente.
translation-type: tm+mt
source-git-commit: cdd92032c627740c66de7b2f3836fa1dcd2ee2ca
workflow-type: tm+mt
source-wordcount: '1436'
ht-degree: 0%

---


# Renderização do SPA e do servidor{#spa-and-server-side-rendering}

Aplicativos de página única (SPA) podem oferta ao usuário uma experiência rica e dinâmica que reage e se comporta de maneiras familiares, normalmente como um aplicativo nativo. [Isso é feito contando com o cliente para carregar o conteúdo antecipadamente e, em seguida, fazer um pesado levantamento da manipulação da ](introduction.md#how-does-a-spa-work) interação do usuário, minimizando assim a quantidade de comunicação necessária entre o cliente e o servidor, tornando o aplicativo mais reativo.

No entanto, isso pode levar a tempos de carregamento iniciais mais longos, especialmente se o SPA for grande e rico em seu conteúdo. Para otimizar o tempo de carregamento, parte do conteúdo pode ser renderizada no lado do servidor. O uso da renderização no lado do servidor (SSR) pode acelerar a carga inicial da página e passar a renderização para o cliente.

## Quando usar o SSR {#when-to-use-ssr}

A SSR não é necessária em todos os projetos. Embora AEM suporte total ao JS SSR para SPA, o Adobe não recomenda implementá-lo sistematicamente para cada projeto.

Ao decidir implementar a SSR, você deve primeiro estimar o que a complexidade adicional, o esforço e a adição de custo representa realisticamente para o projeto, incluindo a manutenção de longo prazo. Uma arquitetura de SSR só deve ser escolhida se o valor acrescentado exceder claramente os custos estimados.

A SSR geralmente fornece algum valor quando há um claro &quot;sim&quot; a qualquer uma das seguintes perguntas:

* **SEO:** a SSR ainda é necessária para que seu site seja indexado corretamente pelos mecanismos de pesquisa que trazem tráfego? Lembre-se de que os principais rastreadores de mecanismo de pesquisa agora avaliam o JS.
* **Velocidade da página:** a SSR fornece uma melhoria mensurável da velocidade em ambientes reais e adiciona à experiência geral do usuário?

Somente quando pelo menos uma dessas duas perguntas for respondida com um claro &quot;sim&quot; para o seu projeto é que o Adobe recomenda a implementação da SSR. As seções a seguir descrevem como fazer isso usando o Adobe I/O Runtime.

## Adobe I/O Runtime {#adobe-i-o-runtime}

Se você [estiver confiante de que seu projeto requer a implementação do SSR](#when-to-use-ssr), a solução Adobe recomendada é usar o Adobe I/O Runtime

Para obter mais informações sobre o Adobe I/O Runtime, consulte

* [https://www.adobe.io/apis/experienceplatform/runtime.html](https://www.adobe.io/apis/experienceplatform/runtime.html) - para obter uma visão geral do serviço
* [https://www.adobe.io/apis/experienceplatform/runtime/docs.html](https://www.adobe.io/apis/experienceplatform/runtime/docs.html)  - para obter a documentação detalhada sobre a plataforma

As seções a seguir detalham como a Adobe I/O Runtime pode ser usada para implementar a SSR para seu SPA em dois modelos diferentes:

* [Fluxo de comunicação orientado por AEM](#aem-driven-communication-flow)
* [Fluxo de comunicação orientado pela Adobe I/O Runtime](#adobe-i-o-runtime-driven-communication-flow)

>[!NOTE]
>
>O Adobe recomenda uma instância do Adobe I/O Runtime separada para cada ambiente AEM (autor, publicação, estágio etc.).

## Configuração remota do renderizador {#remote-content-renderer-configuration}

AEM deve saber onde o conteúdo renderizado remotamente pode ser recuperado. Independentemente de [qual modelo você escolher implementar para SSR,](#adobe-i-o-runtime) você precisará especificar para AEM como acessar esse serviço de renderização remota.

Isso é feito por meio do **RemoteContentRenderer - serviço OSGi de fábrica de configuração**. Procure a string &quot;RemoteContentRenderer&quot; no console Configuração do console da Web em `http://<host>:<port>/system/console/configMgr`.

![Configuração do renderizador](assets/renderer-configuration.png)

Os seguintes campos estão disponíveis para a configuração:

* **Padrão**  do caminho do conteúdo - expressão regular para corresponder a uma parte do conteúdo, se necessário
* **URL**  de ponto de extremidade remoto - URL do ponto de extremidade responsável pela geração do conteúdo
   * Use o protocolo HTTPS protegido se não estiver na rede local.
* **Cabeçalhos**  de solicitação adicionais - Cabeçalhos adicionais a serem adicionados à solicitação enviada ao terminal remoto
   * Padrão: `key=value`
* **Tempo limite**  da solicitação - Tempo limite da solicitação de host remoto em milissegundos

>[!NOTE]
>
>Independentemente de você optar por implementar o [fluxo de comunicação orientado por AEM](#aem-driven-communication-flow) ou o [fluxo controlado pela Adobe I/O Runtime,](#adobe-i-o-runtime-driven-communication-flow) você deve definir uma configuração de renderizador de conteúdo remoto.

>[!NOTE]
>
>Essa configuração aproveita o [Remote Content Renderer,](#remote-content-renderer) que tem opções adicionais de extensão e personalização disponíveis.

## Fluxo de comunicação orientado por AEM {#aem-driven-communication-flow}

Ao usar o SSR, o [fluxo de trabalho de interação do componente](introduction.md#interaction-with-the-spa-editor) do SPA no AEM inclui uma fase na qual o conteúdo inicial do aplicativo é gerado no Adobe I/O Runtime.

1. O navegador solicita o conteúdo SSR da AEM.
1. AEM publica o modelo no Adobe I/O Runtime.
1. A Adobe I/O Runtime retorna o conteúdo gerado.
1. AEM serve o HTML retornado pela Adobe I/O Runtime por meio do modelo HTL do componente de página de backend.

![Adobe I/O AEM controlado por SSE CMS](assets/ssr-cms-drivenaemnode-adobeio.png)

## Fluxo de comunicação orientado pela Adobe I/O Runtime {#adobe-i-o-runtime-driven-communication-flow}

A seção anterior descreve a implementação padrão e recomendada da renderização do lado do servidor no que diz respeito ao SPA no AEM, onde o AEM executa o carregamento automático e a disponibilização de conteúdo.

Como alternativa, a SSR pode ser implementada para que a Adobe I/O Runtime seja responsável pela inicialização, revertendo efetivamente o fluxo de comunicação.

Ambos os modelos são válidos e suportados pela AEM. No entanto, é preciso considerar as vantagens e desvantagens de cada um antes de implementar um modelo específico.

<table>
 <tbody>
  <tr>
   <th><strong>Bootstrapping</strong></th>
   <th><strong>Vantagens</strong></th>
   <th><strong>Desvantagens</strong></th>
  </tr>
  <tr>
   <th><strong>via AEM</strong><br /> </th>
   <td>
    <ul>
     <li>AEM gerencia bibliotecas injetáveis quando necessário</li>
     <li>Os recursos só precisam ser mantidos em AEM<br /> </li>
    </ul> </td>
   <td>
    <ul>
     <li>Possivelmente estranho para SPA desenvolvedor<br /> </li>
    </ul> </td>
  </tr>
  <tr>
   <th><strong>via Adobe I/O Runtime<br /> </strong></th>
   <td>
    <ul>
     <li>Mais familiar aos desenvolvedores SPA<br /> </li>
    </ul> </td>
   <td>
    <ul>
     <li>Os recursos clientlib exigidos pelo aplicativo, como CSS e JavaScript, precisarão ser disponibilizados pelo desenvolvedor AEM por meio da propriedade <code><a href="/help/implementing/developing/introduction/clientlibs.md">allowProxy</a></code><br /> </li>
     <li>Os recursos devem ser sincronizados entre AEM e Adobe I/O Runtime<br /> </li>
     <li>Para habilitar a criação do SPA, pode ser necessário um servidor proxy para Adobe I/O Runtime</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## Planejamento para SSR {#planning-for-ssr}

Geralmente, apenas parte de um aplicativo precisa ser renderizada no lado do servidor. O exemplo comum é o conteúdo que será exibido acima da dobra na carga inicial da página que é renderizada no lado do servidor. Isso economiza tempo fornecendo ao cliente conteúdo já renderizado. Conforme o usuário interage com o SPA, o conteúdo adicional é renderizado pelo cliente.

Ao considerar a implementação da renderização do lado do servidor para seu SPA, é necessário verificar quais partes do aplicativo serão necessárias.

## Desenvolvimento de um SPA usando o SSR {#developing-an-spa-using-ssr}

SPA componentes podem ser renderizados pelo cliente (no navegador) ou pelo servidor. Quando o servidor renderizado, as propriedades do navegador, como tamanho e localização da janela, não estão presentes. Por conseguinte, os componentes SPA devem ser isomórficos, não assumindo qualquer hipótese quanto ao local em que serão apresentados.

Para aproveitar o SSR, será necessário implantar seu código no AEM e no Adobe I/O Runtime, que é responsável pela renderização no servidor. A maioria do código será o mesmo, no entanto, tarefas específicas do servidor serão diferentes.

## SSR para SPA em AEM {#ssr-for-spas-in-aem}

A SSR para SPA em AEM exige a Adobe I/O Runtime, que é chamada para a renderização do lado do servidor de conteúdo do aplicativo. No HTL do aplicativo, um recurso no Adobe I/O Runtime é chamado para renderizar o conteúdo.

Da mesma forma que o AEM suporta as estruturas Angular e React SPA predefinidas, a renderização do lado do servidor também é suportada para aplicativos Angular e React. Consulte a documentação do NPM para obter mais detalhes sobre ambas as estruturas.

## Renderizador de conteúdo remoto {#remote-content-renderer}

A [Configuração do Remote Content Renderer](#remote-content-renderer-configuration) necessária para usar o SSR com seu SPA em AEM se encaixa em um serviço de renderização mais generalizado que pode ser estendido e personalizado para atender às suas necessidades.

### RemoteContentRenderingService {#remotecontentrenderingservice}

`RemoteContentRenderingService` é um serviço OSGi para recuperar conteúdo renderizado em um servidor remoto, como da Adobe I/O. O conteúdo enviado para o servidor remoto é baseado no parâmetro de solicitação passado.

`RemoteContentRenderingService` pode ser inserido por inversão de dependência em um modelo Sling personalizado ou servlet quando for necessária manipulação de conteúdo adicional.

Este serviço é usado internamente pelo [RemoteContentRendererRequestHandlerServlet](#remotecontentrendererrequesthandlerservlet).

### RemoteContentRendererRequestHandlerServlet {#remotecontentrendererrequesthandlerservlet}

O `RemoteContentRendererRequestHandlerServlet` pode ser usado para definir programaticamente a configuração da solicitação. `DefaultRemoteContentRendererRequestHandlerImpl`, a implementação do manipulador de solicitações padrão fornecido permite que você crie várias configurações OSGi para mapear um local na estrutura do conteúdo para um terminal remoto.

Para adicionar um Manipulador de solicitações personalizado, implemente a interface `RemoteContentRendererRequestHandler`. Certifique-se de definir a propriedade do componente `Constants.SERVICE_RANKING` como um número inteiro maior que 100, que é a classificação de `DefaultRemoteContentRendererRequestHandlerImpl`.

```javascript
@Component(immediate = true,
        service = RemoteContentRendererRequestHandler.class,
        property={
            Constants.SERVICE_RANKING +":Integer=1000"
        })
public class CustomRemoteContentRendererRequestHandlerImpl implements RemoteContentRendererRequestHandler {}
```

### Configurar a configuração OSGi do manipulador padrão {#configure-default-handler}

A configuração do manipulador padrão deve ser configurada conforme descrito na seção [Configuração do Remote Content Renderer](#remote-content-renderer-configuration).

### Uso do Renderizador de Conteúdo Remoto {#usage}

Para obter um servlet e retornar algum conteúdo que possa ser inserido na página:

1. Verifique se o servidor remoto está acessível.
1. Adicione um dos seguintes trechos ao modelo HTL de um componente AEM.
1. Como opção, crie ou modifique as configurações do OSGi.
1. Procurar o conteúdo do site

Normalmente, o modelo HTL de um componente de página é o recipient principal desse recurso.

```html
<sly data-sly-resource="${resource @ resourceType='cq/remote/content/renderer/request/handler'}" />
```

### Requisitos {#requirements}

Os servlets aproveitam o Exportador do Modelo Sling para serializar os dados do componente. Por padrão, os adaptadores `com.adobe.cq.export.json.ContainerExporter` e `com.adobe.cq.export.json.ComponentExporter` são suportados como Sling Model. Se necessário, você pode adicionar classes para as quais a solicitação deve ser adaptada usando `RemoteContentRendererServlet` e implementando `RemoteContentRendererRequestHandler#getSlingModelAdapterClasses`. As classes adicionais devem estender `ComponentExporter`.
