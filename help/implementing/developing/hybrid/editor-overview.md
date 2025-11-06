---
title: Visão geral do editor de SPA
description: Este artigo fornece uma visão geral abrangente do Editor de SPA e como ele funciona, incluindo fluxos de trabalho detalhados de interação do Editor de SPA no AEM.
exl-id: 9814d86e-8d87-4f7f-84ba-6943fe6da22f
feature: Developing
role: Admin, Developer
index: false
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1633'
ht-degree: 93%

---


# Visão geral do editor de SPA {#spa-editor-overview}

Aplicativos de página única (SPAs) podem oferecer experiências interessantes para usuários de sites. Os desenvolvedores desejam criar sites usando estruturas de SPA, e os autores desejam editar o conteúdo de um site criado usando essas estruturas diretamente no AEM.

O editor de SPA oferece uma solução abrangente para permitir o uso de SPAs no AEM. Esta página fornece uma visão geral de como o suporte do SPA é estruturado no AEM, como o Editor de SPA funciona e como a estrutura de SPA e AEM permanece sincronizada.

{{ue-over-spa}}

## Introdução {#introduction}

Sites criados usando estruturas de SPA comuns, como React e Angular, carregam seu conteúdo dinamicamente via JSON e não fornecem a estrutura de HTML necessária para que o editor de página do AEM possa estabelecer controles de edição.

Para habilitar a edição de SPAs no AEM, é necessário um mapeamento entre a saída JSON do SPA e o modelo de conteúdo no repositório do AEM para salvar as alterações no conteúdo.

A compatibilidade com SPA no AEM apresenta uma camada de JS sutil que interage com o código JS do SPA quando ele é carregado no editor de página através do qual os eventos podem ser enviados, sendo assim, o local dos controles de edição pode ser ativado para permitir a edição de acordo com o contexto. Esse recurso se baseia no conceito de endpoint da API de serviços de conteúdo, pois o conteúdo do SPA deve ser carregado por meio dos serviços de conteúdo.

Para obter mais detalhes sobre SPAs no AEM, consulte o seguinte:

* [Blueprint de SPA](blueprint.md) para os requisitos técnicos de um SPA.
* [Introdução a SPAs no AEM usando o React](getting-started-react.md) para um tour rápido de um SPA simples usando o React.
* [Introdução a SPAs no AEM usando o Angular](getting-started-angular.md) para obter um tour rápido de um SPA simples usando o Angular.

## Design {#design}

O componente de página para um SPA não fornece os elementos HTML de seus componentes filhos por meio do arquivo JSP ou HTL. Esta operação é delegada na estrutura de SPA. A representação de componentes ou modelos filhos é buscada como uma estrutura de dados JSON do JCR. Os componentes do SPA são adicionados à página de acordo com essa estrutura. Esse comportamento diferencia a composição do corpo inicial do componente de página de contrapartes não SPA.

### Gerenciamento do modelo de página {#page-model-management}

A resolução e o gerenciamento do modelo de página são delegados a uma biblioteca `PageModel`. O SPA deve usar a biblioteca de Modelos de página para ser inicializado e criado pelo Editor de SPA. A biblioteca de Modelos de página fornecida indiretamente ao componente Página de AEM por meio do npm `aem-react-editable-components`. O Modelo de página é um interpretador entre o AEM e o SPA e, portanto, sempre deve estar presente. Quando a página é criada, uma biblioteca adicional `cq.authoring.pagemodel.messaging` precisa ser adicionada para habilitar a comunicação com o editor de páginas.

Se o componente Página de SPA herda do componente principal da página, há duas opções para criar a categoria de biblioteca de clientes `cq.authoring.pagemodel.messaging` disponível:

* Se o modelo for editável, adicione-o à política de página.
* Ou adicione as categorias utilizando o `customfooterlibs.html`.

Para cada recurso no modelo exportado, o SPA mapeia um componente real que faz a
renderização. O modelo, representado como JSON, é renderizado utilizando os mapeamentos de componente em um container.

![Mapeamento de modelo e componente nos SPAs](assets/model-component-mapping.png)

>[!CAUTION]
>
>A inclusão da categoria `cq.authoring.pagemodel.messaging` deve ser limitada ao contexto do editor de SPA.

### Tipo de dados da comunicação {#communication-data-type}

Quando a categoria `cq.authoring.pagemodel.messaging` é adicionada à página, ela envia uma mensagem para o editor de páginas para estabelecer o tipo de dados de comunicação JSON. Quando o tipo de dados de comunicação é definido como JSON, as solicitações GET se comunicam com os end-points do modelo do Sling de um componente. Depois que uma atualização ocorre no editor de páginas, a representação JSON do componente atualizado é enviada para a biblioteca do Modelo de página. A biblioteca do Modelo de página informa ao SPA de atualizações.

![Comunicação SPA](assets/communication.png)

## Fluxo de trabalho {#workflow}

Você pode entender o fluxo da interação entre o SPA e o AEM pensando no editor de SPA como um mediador entre os dois.

* A comunicação entre o editor de páginas e o SPA é feita utilizando JSON em vez de HTML.
* O editor de páginas fornece a versão mais recente do modelo de página para o SPA por meio do iframe e da API de mensagens.
* O gerenciador de modelo de página notifica o editor de que está pronto para edição e passa o modelo de página como uma estrutura JSON.
* O editor não altera nem mesmo acessa a estrutura DOM da página que está sendo criada, mas fornece o modelo de página mais recente.

![Fluxo de trabalho SPA](assets/workflow.png)

### Fluxo de trabalho básico do editor de SPA {#basic-spa-editor-workflow}

Lembrando os elementos principais do editor de SPA, o fluxo de trabalho de alto nível da edição de um SPA no AEM é exibido ao autor da seguinte maneira.

![Fluxo de trabalho de SPA animado](assets/workflow.gif)

1. Editor de SPA é carregado.
1. O SPA é carregado em um quadro separado.
1. O SPA solicita conteúdo JSON e renderiza componentes do lado do cliente.
1. O Editor de SPA detecta componentes renderizados e gera sobreposições.
1. O autor clica em sobrepor, exibindo a barra de ferramentas de edição do componente.
1. O Editor de SPA mantém as edições com uma solicitação POST para o servidor.
1. As solicitações do Editor de SPA atualizaram o JSON para o Editor de SPA, que é enviado ao SPA com um evento DOM.
1. O SPA renderiza novamente o componente relacionado, atualizando seu DOM.

>[!NOTE]
>
>Lembre-se:
>
>* O SPA é sempre encarregado de sua exibição.
>* O Editor de SPA é isolado do próprio SPA.
>* Na produção (publicação), o editor de SPA nunca é carregado.

### Fluxo de trabalho de edição de página do cliente-servidor {#client-server-page-editing-workflow}

É uma visão geral mais detalhada da interação cliente-servidor ao editar um SPA.

![Fluxo de trabalho de edição do cliente-servidor](assets/client-server-editing.png)

1. O SPA é inicializado e solicita o modelo de página do Exportador de modelo do Sling.
1. O Exportador de modelo do Sling solicita os recursos que compõem a página do repositório.
1. O repositório retorna os recursos.
1. O Exportador de modelo do Sling retorna o modelo da página.
1. O SPA instancia seus componentes com base no modelo da página.
1. **6a** O conteúdo informa ao editor que está pronto para criação.

   **6b** O editor de páginas solicita as configurações de criação do componente.

   **6c** O editor de páginas recebe as configurações do componente.
1. Quando o autor edita um componente, o editor de páginas posta uma solicitação de modificação no servlet POST padrão.
1. O recurso é atualizado no repositório.
1. O recurso atualizado é fornecido ao servlet POST.
1. O servlet POST padrão informa ao editor de páginas que o recurso foi atualizado.
1. O editor de páginas solicita o novo modelo de página.
1. Os recursos que compõem a página são solicitados do repositório.
1. Os recursos que compõem a página são fornecidos pelo repositório ao Exportador de modelo do Sling.
1. O modelo de página atualizado é retornado ao editor.
1. O editor de páginas atualiza a referência do modelo de página do SPA.
1. O SPA atualiza seus componentes com base na nova referência do modelo de página.
1. As configurações de componentes dos editores de página são atualizadas.

   **17a** O SPA sinaliza ao editor de páginas que o conteúdo está pronto.

   **17b** O editor de páginas fornece o SPA com configurações de componentes.

   **17c** O SPA fornece configurações atualizadas do componente.

### Fluxo de trabalho de criação {#authoring-workflow}

É uma visão geral mais detalhada que se concentra na experiência de criação.

![Fluxo de trabalho de criação de SPA](assets/authoring-workflow.png)

1. O SPA busca o modelo da página.
1. **2a** O modelo de página fornece ao editor os dados necessários para a criação.

   **2b** Quando notificado, o orquestrador de componentes atualiza a estrutura de conteúdo da página.
1. O orquestrador de componentes consulta o mapeamento entre um tipo de recurso do AEM e um componente do SPA.
1. O orquestrador de componentes instancia dinamicamente o componente do SPA com base no modelo de página e no mapeamento de componentes.
1. O editor de páginas atualiza o modelo de página.
1. **6a** O modelo de página fornece dados de criação atualizados para o editor de página.

   **6b** O modelo de página despacha alterações no orquestrador de componentes.
1. O orquestrador de componentes busca o mapeamento de componentes.
1. O orquestrador de componentes atualiza o conteúdo da página.
1. Quando o SPA conclui a atualização do conteúdo da página, o editor de páginas carrega o ambiente de criação.

## Requisitos e limitações {#requirements-limitations}

Para permitir que o autor use o editor de páginas para editar o conteúdo de um SPA, o aplicativo SPA deve ser implementado para interagir com o SDK do Editor de SPA do AEM. Consulte o documento [Introdução aos SPAs no AEM usando o React](getting-started-react.md) para saber o mínimo necessário para executar o seu.

### Estruturas compatíveis {#supported-frameworks}

O SDK do Editor de SPA é compatível com as seguintes versões mínimas:

* React 16.x e superior
* Angular 6.x e superior

As versões anteriores dessas estruturas podem funcionar com o SDK do Editor de SPA do AEM, mas não são compatíveis.

### Estruturas adicionais {#additional-frameworks}

Estruturas de SPA adicionais podem ser implementadas para funcionar com o SDK do Editor de SPA de AEM. Consulte o documento [Blueprint de SPA](blueprint.md) para obter os requisitos que uma estrutura deve atender para criar uma camada específica de estrutura composta por módulos, componentes e serviços para trabalhar com o Editor de SPA do AEM.

### Uso de vários seletores {#multiple-selectors}

Seletores personalizados adicionais podem ser definidos e usados como parte de um SPA desenvolvido para o SDK de SPA do AEM. No entanto, esse suporte exige que o seletor `model` seja o primeiro seletor e a extensão seja `.json`, conforme exigido pelo exportador JSON.

### Requisitos do editor de texto {#text-editor-requirements}

Se você quiser usar o editor local de um componente de texto criado no SPA, há uma configuração adicional necessária.

1. Defina um atributo (pode ser qualquer um), no elemento wrapper do container, que contém o HTML de texto. No caso do projeto SPA WKND, foi um elemento `<div>` e o seletor usado foi o `data-rte-editelement`.
1. Defina a configuração `editElementQuery` no `cq:InplaceEditingConfig` do componente de texto AEM correspondente que aponta para esse seletor, por exemplo, `data-rte-editelement`. Isso permite que o editor saiba qual elemento HTML envolve o texto HTML.

Para obter mais informações sobre a propriedade `editElementQuery` e a configuração do editor de rich text, consulte [Configuração do Editor de rich text](/help/implementing/developing/extending/rich-text-editor.md).

### Limitações {#limitations}

O SDK do Editor de SPA do AEM é totalmente compatível com a Adobe e continua sendo aprimorado e expandido. Os seguintes recursos do AEM ainda não são compatíveis com o Editor de SPA:

* Modo de Direcionamento
* ContextHub
* Edição de imagem integrada
* Editar configurações (por exemplo, listeners)
* Desfazer / Refazer
* Distorção temporal e Diferencial de páginas
* Recursos que executam regravação do HTML no lado do servidor, como [Verificador de Links,](/help/operations/link-checker.md) serviço de regravação CDN, redução de URL etc.
* Modo de desenvolvedor
* Inicializações do AEM
