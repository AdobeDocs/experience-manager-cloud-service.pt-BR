---
title: Renderização do SPA e do servidor
description: Usar a renderização do lado do servidor (SSR) no SPA pode acelerar o carregamento inicial da página e, em seguida, passar a renderização adicional para o cliente.
exl-id: be409559-c7ce-4bc2-87cf-77132d7c2da1
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '1492'
ht-degree: 0%

---

# Renderização do SPA e do servidor{#spa-and-server-side-rendering}

Os aplicativos de página única (SPA) podem oferecer ao usuário uma experiência avançada e dinâmica que reage e se comporta de maneiras familiares, geralmente como um aplicativo nativo. [Essa funcionalidade é obtida confiando no cliente para carregar o conteúdo antecipadamente e, em seguida, fazer o trabalho pesado de manipulação da interação do usuário](introduction.md#how-does-a-spa-work). Esse processo minimiza a quantidade de comunicação necessária entre o cliente e o servidor, tornando o aplicativo mais reativo.

No entanto, esse processo pode levar a tempos de carregamento inicial mais longos, especialmente se o SPA for grande e rico em conteúdo. Para otimizar os tempos de carregamento, parte do conteúdo pode ser renderizado no lado do servidor. O uso da renderização do lado do servidor (SSR) pode acelerar a carga inicial da página e, em seguida, passar a renderização adicional para o cliente.

## Quando usar o SSR {#when-to-use-ssr}

O SSR não é necessário em todos os projetos. Embora AEM seja totalmente compatível com JS SSR para SPA, o Adobe não recomenda implementá-lo sistematicamente para cada projeto.

Ao decidir implementar o SSR, você deve primeiro estimar a complexidade, o esforço e o custo adicionais que a adição do SSR representa realisticamente para o projeto, incluindo a manutenção a longo prazo. Uma arquitetura SSR só deve ser escolhida quando o valor acrescentado exceder claramente os custos estimados.

O SSR geralmente fornece algum valor quando há um claro &quot;sim&quot; para qualquer uma das seguintes perguntas:

* **SEO:** O SSR ainda é necessário para que seu site seja indexado corretamente pelos mecanismos de pesquisa que trazem tráfego? Lembre-se de que os principais rastreadores de mecanismo de pesquisa agora avaliam o JS.
* **Velocidade da página:** o SSR oferece uma melhoria mensurável na velocidade de ambientes reais e adiciona à experiência geral do usuário?

Somente quando pelo menos uma dessas duas perguntas for respondida com um claro &quot;sim&quot; para o seu projeto, o Adobe recomenda a implementação do SSR. As seções a seguir descrevem como fazer isso usando o Adobe I/O Runtime, parte da [App Builder](https://developer.adobe.com/app-builder).

## Adobe I/O Runtime {#adobe-i-o-runtime}

Se você [estiver confiante de que seu projeto requer a implementação do SSR](#when-to-use-ssr), a solução recomendada do Adobe é usar o Adobe I/O Runtime.

Para obter mais informações sobre o Adobe I/O Runtime, consulte o seguinte:

* [https://developer.adobe.com/runtime](https://developer.adobe.com/runtime) - para obter uma visão geral do recurso Tempo de Execução do App Builder
* [https://developer.adobe.com/app-builder](https://developer.adobe.com/app-builder) - para obter detalhes sobre o produto App Builder completo
* [https://developer.adobe.com/runtime/docs/](https://developer.adobe.com/runtime/docs) - para obter a documentação detalhada

As seções a seguir detalham como o Adobe I/O Runtime pode ser usado para implementar o SSR para o SPA em dois modelos diferentes:

* [Fluxo de comunicação orientado por AEM](#aem-driven-communication-flow)
* [Fluxo de comunicação orientado pela Adobe I/O Runtime](#adobe-i-o-runtime-driven-communication-flow)

>[!NOTE]
>
>A Adobe recomenda um espaço de trabalho do Adobe I/O Runtime separado por ambiente (preparo, produção, teste e assim por diante). Isso permite padrões típicos de SDLC (Systems Development Life Cycle, ciclo de vida de desenvolvimento de sistemas) com diferentes versões de um único aplicativo implantado em diferentes ambientes. Consulte [CI/CD para aplicativos App Builder](https://developer.adobe.com/app-builder/docs/guides/deployment/ci_cd_for_firefly_apps/) para obter mais informações.
>
>Um espaço de trabalho separado não é necessário por instância (autor, publicação), a menos que haja diferenças na implementação em tempo de execução por tipo de instância.

>[!NOTE]
>
>A Cloud Manager não oferece suporte à implantação do Adobe I/O Runtime. Como resultado, sua própria infraestrutura deve ser configurada para implantar o código SSR na Adobe I/O Runtime.

## Configuração do renderizador remoto {#remote-content-renderer-configuration}

O AEM deve saber onde o conteúdo renderizado remotamente pode ser recuperado. Independentemente do [modelo que você escolher implementar para SSR,](#adobe-i-o-runtime) você deve especificar ao AEM como acessar esse serviço de renderização remota.

Este serviço é feito por meio do **RemoteContentRenderer - serviço OSGi da Fábrica de Configurações**. Procure a cadeia de caracteres &quot;RemoteContentRenderer&quot; no console Configuração do Console da Web em `http://<host>:<port>/system/console/configMgr`.

![Configuração do processador](assets/renderer-configuration.png)

Os seguintes campos estão disponíveis para a configuração:

* **Padrão de caminho de conteúdo** - Expressão regular para corresponder a uma parte do conteúdo, se necessário
* **URL do ponto de extremidade remoto** - URL do ponto de extremidade responsável pela geração do conteúdo
   * Use o protocolo HTTPS seguro se não estiver na rede local.
* **Cabeçalhos de solicitação adicionais** - Cabeçalhos adicionais a serem adicionados à solicitação enviada ao ponto de extremidade remoto
   * Padrão: `key=value`
* **Tempo limite de solicitação** - Tempo limite de solicitação de host remoto em milissegundos

>[!NOTE]
>
>Independentemente de você optar por implementar o [fluxo de comunicação orientado por AEM](#aem-driven-communication-flow) ou o [fluxo orientado por Adobe I/O Runtime](#adobe-i-o-runtime-driven-communication-flow), será necessário definir uma configuração de renderizador de conteúdo remoto.

>[!NOTE]
>
>Esta configuração usa o [Renderizador de Conteúdo Remoto](#remote-content-renderer), que tem opções adicionais de extensão e personalização disponíveis.

## Fluxo de comunicação orientado por AEM {#aem-driven-communication-flow}

Ao usar o SSR, o [fluxo de trabalho de interação de componente](introduction.md#interaction-with-the-spa-editor) do SPA no AEM inclui uma fase em que o conteúdo inicial do aplicativo é gerado no Adobe I/O Runtime.

1. O navegador solicita o conteúdo SSR do AEM.
1. AEM posta o modelo no Adobe I/O Runtime.
1. O Adobe I/O Runtime retorna o conteúdo gerado.
1. O AEM serve o HTML retornado pelo Adobe I/O Runtime por meio do modelo HTL do componente de página de back-end.

![Adobe I/O de AEM orientado por CMS do SSE](assets/ssr-cms-drivenaemnode-adobeio.png)

## Fluxo de comunicação orientado pela Adobe I/O Runtime {#adobe-i-o-runtime-driven-communication-flow}

A seção anterior descreve a implementação padrão e recomendada da renderização no lado do servidor em relação ao SPA AEM, onde o AEM executa o bootstrapping e a veiculação de conteúdo.

Como alternativa, o SSR pode ser implementado para que o Adobe I/O Runtime seja responsável pela inicialização, revertendo efetivamente o fluxo de comunicação.

Ambos os modelos são válidos e suportados pelo AEM. No entanto, deve-se considerar as vantagens e desvantagens de cada um antes de implementar um modelo específico.

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
     <li>AEM gerencia a a injeção de bibliotecas onde necessário</li>
     <li>Manter recursos somente no AEM<br /> </li>
    </ul> </td>
   <td>
    <ul>
     <li>Possivelmente desconhecido do desenvolvedor de SPA<br /> </li>
    </ul> </td>
  </tr>
  <tr>
   <th><strong>via Adobe I/O Runtime<br /> </strong></th>
   <td>
    <ul>
     <li>Mais familiarizado com desenvolvedores de SPA<br /> </li>
    </ul> </td>
   <td>
    <ul>
     <li>Os recursos de clientlib necessários para o aplicativo, como CSS e JavaScript, devem ser disponibilizados pelo desenvolvedor AEM por meio da propriedade <code><a href="/help/implementing/developing/introduction/clientlibs.md">allowProxy</a></code> <br /> </li>
     <li>Os recursos devem ser sincronizados entre AEM e Adobe I/O Runtime<br /> </li>
     <li>Para habilitar a criação do SPA, pode ser necessário um servidor proxy para o Adobe I/O Runtime</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## Planejamento para SSR {#planning-for-ssr}

Geralmente, somente parte de um aplicativo deve ser renderizada no lado do servidor. O exemplo comum é o conteúdo exibido acima da dobra no carregamento inicial da página que é renderizado no lado do servidor. Esse processo economiza tempo, fornecendo ao cliente conteúdo já renderizado. Conforme o usuário interage com o SPA, o conteúdo adicional é renderizado pelo cliente.

Ao considerar implementar a renderização do lado do servidor para o seu SPA, analise quais partes do aplicativo são necessárias.

## Desenvolvimento de um SPA usando SSR {#developing-an-spa-using-ssr}

Os componentes do SPA podem ser renderizados pelo cliente (no navegador) ou pelo servidor. Quando renderizadas no lado do servidor, as propriedades do navegador, como tamanho e localização da janela, não estão presentes. Portanto, os componentes do SPA devem ser isomorfos, não fazendo suposições sobre onde são renderizados.

Para usar o SSR, você deve implantar seu código no AEM e no Adobe I/O Runtime, que é responsável pela renderização do lado do servidor. A maioria do código é o mesmo, no entanto, as tarefas específicas do servidor diferem.

## RSS para AEM no SPA {#ssr-for-spas-in-aem}

O SSR para AEM no SPA requer o Adobe I/O Runtime, que é chamado para a renderização do lado do servidor de conteúdo do aplicativo. No HTL do aplicativo, um recurso no Adobe I/O Runtime é chamado para renderizar o conteúdo.

Assim como o AEM suporta as estruturas SPA do Angular e do React prontas para uso, a renderização no lado do servidor também é compatível com os aplicativos Angular e React. Consulte a documentação do NPM para ambas as estruturas para obter mais detalhes.

## Renderizador remoto de conteúdo {#remote-content-renderer}

A [Configuração do Renderizador de Conteúdo Remoto](#remote-content-renderer-configuration), necessária para usar o SSR com seu SPA no AEM, utiliza um serviço de renderização mais generalizado, que pode ser estendido e personalizado para atender às suas necessidades.

### ServiçoDeRenderizaçãoDeConteúdoRemoto {#remotecontentrenderingservice}

`RemoteContentRenderingService` Um serviço OSGi para recuperar conteúdo renderizado em um servidor remoto, como do Adobe I/O. O conteúdo enviado para o servidor remoto se baseia no parâmetro de solicitação transmitido.

`RemoteContentRenderingService` Pode ser inserido por inversão de dependência em um modelo Sling personalizado ou servlet quando uma manipulação de conteúdo adicional é necessária.

Este serviço é usado internamente pelo [RemoteContentRendererRequestHandlerServlet](#remotecontentrendererrequesthandlerservlet).

### ServletManipuladordeSolicitaçãodeRenderizadorDeConteúdoRemoto {#remotecontentrendererrequesthandlerservlet}

O `RemoteContentRendererRequestHandlerServlet` é usado para definir programaticamente a configuração da solicitação. `DefaultRemoteContentRendererRequestHandlerImpl`, a implementação do manipulador de solicitações padrão fornecido, permite que você crie várias configurações OSGi para mapear um local na estrutura de conteúdo para um ponto de extremidade remoto.

Para adicionar um Manipulador de solicitação personalizado, implemente a interface `RemoteContentRendererRequestHandler`. Certifique-se de definir a propriedade do componente `Constants.SERVICE_RANKING` para um inteiro maior que 100, que é a classificação do `DefaultRemoteContentRendererRequestHandlerImpl`.

```javascript
@Component(immediate = true,
        service = RemoteContentRendererRequestHandler.class,
        property={
            Constants.SERVICE_RANKING +":Integer=1000"
        })
public class CustomRemoteContentRendererRequestHandlerImpl implements RemoteContentRendererRequestHandler {}
```

### Configurar o OSGi do manipulador padrão {#configure-default-handler}

A configuração do manipulador padrão deve ser definida conforme descrito na seção [Configuração do Renderizador de Conteúdo Remoto](#remote-content-renderer-configuration).

### Uso do renderizador de conteúdo remoto {#usage}

Faça uma busca de servlet e retorne algum conteúdo inserido na página:

1. Certifique-se de que o servidor remoto esteja acessível.
1. Adicione um dos seguintes trechos ao modelo HTL de um componente AEM.
1. Opcionalmente, crie ou modifique as configurações do OSGi.
1. Navegar pelo conteúdo do site

Normalmente, o modelo HTL de um componente de página é o principal destinatário desse recurso.

```html
<sly data-sly-resource="${resource @ resourceType='cq/remote/content/renderer/request/handler'}" />
```

### Requisitos {#requirements}

Os servlets usam o Exportador de modelo Sling para serializar os dados do componente. Por padrão, `com.adobe.cq.export.json.ContainerExporter` e `com.adobe.cq.export.json.ComponentExporter` são suportados como adaptadores do Modelo do Sling. Se necessário, você pode adicionar classes às quais a solicitação deve ser adaptada usando o `RemoteContentRendererServlet` e implementando o `RemoteContentRendererRequestHandler#getSlingModelAdapterClasses`. As classes adicionais devem estender o `ComponentExporter`.
