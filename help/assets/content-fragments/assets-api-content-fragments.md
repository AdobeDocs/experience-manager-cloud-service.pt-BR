---
title: Suporte a fragmentos de conteúdo do Adobe Experience Manager as a Cloud Service na API HTTP do Assets
description: Saiba mais sobre o suporte a fragmentos de conteúdo na API HTTP de ativos, uma parte importante do recurso de entrega headless do Adobe Experience Manager.
feature: Content Fragments,Assets HTTP API
exl-id: d72cc0c0-0641-4fd6-9f87-745af5f2c232
source-git-commit: 38cb2605e2133e858c60644084cf515a03b54f60
workflow-type: tm+mt
source-wordcount: '1747'
ht-degree: 11%

---

# Suporte a fragmentos de conteúdo na API HTTP do AEM Assets {#content-fragments-support-in-aem-assets-http-api}

## Visão geral {#overview}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-65/assets/extending/assets-api-content-fragments.html?lang=en) |
| AEM as a Cloud Service | Este artigo |

Saiba mais sobre o suporte a Fragmentos de conteúdo na API HTTP do Assets, uma parte importante do recurso de entrega headless do Adobe Experience Manager (AEM).

>[!NOTE]
>
>A variável [API HTTP de ativos](/help/assets/mac-api-assets.md) abrange:
>
>* API REST de ativos
>* incluindo suporte para fragmentos de conteúdo
>
>A implementação atual da API HTTP do Assets baseia-se na [REST](https://en.wikipedia.org/wiki/Representational_state_transfer) estilo arquitetônico.

>[!NOTE]
>
>Para obter as informações mais recentes sobre as APIs do Experience Manager, visite também [APIs do Adobe Experience Manager as a Cloud Service](https://developer.adobe.com/experience-cloud/experience-manager-apis/).

A variável [API REST de ativos](/help/assets/mac-api-assets.md) O permite que os desenvolvedores do Adobe Experience Manager as a Cloud Service acessem o conteúdo (armazenado em AEM) diretamente pela API HTTP, por meio de operações CRUD (Create, Read, Update, Delete, Criar, Ler, Atualizar, Excluir).

A API permite operar o Adobe Experience Manager as a Cloud Service como um CMS (Content Management System, Sistema de gerenciamento de conteúdo) headless, fornecendo Serviços de conteúdo a um aplicativo front-end JavaScript. Ou qualquer outro aplicativo que possa executar solicitações HTTP e manipular respostas JSON.

Por exemplo, [Aplicativos de página única (SPA)](/help/implementing/developing/hybrid/introduction.md), baseado em estrutura ou personalizado, exigem conteúdo fornecido pela API HTTP, geralmente no formato JSON.

Enquanto [Componentes principais do AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=pt-BR) A fornecer uma API personalizável que pode atender às operações de Leitura necessárias para essa finalidade e cuja saída JSON pode ser personalizada, eles exigem o know-how AEM WCM (Web Content Management, Gerenciamento de conteúdo da Web) para implementação. Isso ocorre porque eles devem ser hospedados em páginas baseadas em modelos de AEM dedicados. Nem todas as organizações de desenvolvimento de SPA têm acesso direto a esse conhecimento.

É quando a API REST do Assets pode ser usada. Ele permite que os desenvolvedores acessem ativos (por exemplo, imagens e fragmentos de conteúdo) diretamente, sem a necessidade de primeiro incorporá-los em uma página e entregar seu conteúdo no formato JSON serializado.

>[!NOTE]
>
>Não é possível personalizar a saída JSON da API REST do Assets.

A API REST do Assets também permite que os desenvolvedores modifiquem o conteúdo criando novos ativos, atualizando ou excluindo ativos, fragmentos de conteúdo e pastas existentes.

A API REST do Assets:

* segue o [Princípio do HATEOAS](https://en.wikipedia.org/wiki/HATEOAS)

* implementa o [Formato SIREN](https://github.com/kevinswiber/siren)

## Pré-requisitos {#prerequisites}

A API REST de ativos está disponível em cada instalação pronta para uso de versões recentes do Adobe Experience Manager as a Cloud Service.

## Principais conceitos {#key-concepts}

As ofertas da API REST do Assets [REST](https://en.wikipedia.org/wiki/Representational_state_transfer)Acesso com estilo do aos ativos armazenados em uma instância do AEM.

Ele usa o `/api/assets` ponto de extremidade e exige o caminho do ativo para acessá-lo (sem o ponto de extremidade `/content/dam`).

* Isso significa que para acessar o ativo em:
   * `/content/dam/path/to/asset`
* Solicitação:
   * `/api/assets/path/to/asset`

Por exemplo, para acessar `/content/dam/wknd/en/adventures/cycling-tuscany`, solicite `/api/assets/wknd/en/adventures/cycling-tuscany.json`

>[!NOTE]
>O acesso por:
>
>* `/api/assets` **não** precisa da utilização do seletor `.model`.
>* `/content/path/to/page` **precisa** da utilização do seletor `.model`.

O método HTTP determina a operação a ser executada:

* **GET**: para recuperar uma representação JSON de um ativo ou uma pasta
* **POST** - para criar ativos ou pastas
* **PUT**: para atualizar as propriedades de um ativo ou pasta
* **DELETE**: para excluir um ativo ou pasta

>[!NOTE]
>
>O corpo da solicitação e/ou os parâmetros de URL podem ser usados para configurar algumas dessas operações; por exemplo, definir que uma pasta ou um ativo deve ser criado por uma solicitação **POST**.

O formato exato das solicitações compatíveis é definido no [Referência da API](/help/assets/content-fragments/assets-api-content-fragments.md#api-reference) documentação.

### Comportamento transacional {#transactional-behavior}

Todas as solicitações são atômicas.

Isso significa que os subsequentes (`write`) solicitações não podem ser combinadas em uma única transação que poderia ter êxito ou falhar como uma única entidade.

### API REST do AEM (Assets) versus Componentes do AEM {#aem-assets-rest-api-versus-aem-components}

<table>
 <thead>
  <tr>
   <td>Aspecto</td>
   <td>API REST de ativos<br/> </td>
   <td>Componente AEM<br/> (componentes que usam Modelos Sling)</td>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td>Casos de uso compatíveis</td>
   <td>Finalidade geral.</td>
   <td><p>Otimizado para consumo em um Aplicativo de página única (SPA) ou em qualquer outro contexto (que consome conteúdo).</p> <p>Ele também pode conter informações de layout.</p> </td>
  </tr>
  <tr>
   <td>Operações suportadas</td>
   <td><p>Criar, ler, atualizar, excluir.</p> <p>Com operações adicionais, dependendo do tipo de entidade.</p> </td>
   <td>Somente leitura.</td>
  </tr>
  <tr>
   <td>Acesso</td>
   <td><p>Ele pode ser acessado diretamente.</p> <p>Usa o <code>/api/assets </code>endpoint, mapeado para <code>/content/dam</code> (no repositório).</p> 
   <p>Um caminho de exemplo seria semelhante a: <code>/api/assets/wknd/en/adventures/cycling-tuscany.json</code></p>
   </td>
    <td><p>Ele deve ser referenciado por meio de um componente AEM em uma página AEM.</p> <p>Usa o <code>.model</code> para criar a representação JSON.</p> <p>Um caminho de exemplo seria semelhante a:<br/> <code>/content/wknd/language-masters/en/adventures/cycling-tuscany.model.json</code></p> 
   </td>
  </tr>
  <tr>
   <td>Segurança</td>
   <td><p>Várias opções são possíveis.</p> <p>O OAuth é proposto; pode ser configurado separadamente da configuração padrão.</p> </td>
   <td>Usa a configuração padrão do AEM.</td>
  </tr>
  <tr>
   <td>Observações arquitetônicas</td>
   <td><p>O acesso de gravação normalmente aborda uma instância de Autor.</p> <p>A leitura também pode ser direcionada a uma instância de publicação.</p> </td>
   <td>Como essa abordagem é somente leitura, ela geralmente é usada para instâncias de Publicação.</td>
  </tr>
  <tr>
   <td>Saída</td>
   <td>Saída do SIREN baseada em JSON: detalhada, mas poderosa. Ela permite navegar dentro do conteúdo.</td>
   <td>Saída proprietária baseada em JSON; configurável por meio de Modelos Sling. Navegar pela estrutura de conteúdo é difícil de implementar (mas não necessariamente impossível).</td>
  </tr>
 </tbody>
</table>

### Segurança {#security}

Se a API REST do Assets for usada em um ambiente sem requisitos de autenticação específicos, o filtro CORS do AEM deverá ser configurado corretamente.

>[!NOTE]
>
>Para obter mais informações, consulte:
>
>* [Explicação sobre o CORS/AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html?lang=en)
>* [Vídeo - Desenvolvimento do CORS com AEM (04:06)](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/develop-for-cross-origin-resource-sharing.html?lang=en)
>

Em ambientes com requisitos de autenticação específicos, o OAuth é recomendado.

## Recursos disponíveis {#available-features}

Fragmentos de conteúdo são um tipo específico de ativo, consulte [Trabalhar com fragmentos de conteúdo](/help/assets/content-fragments/content-fragments.md).

Para obter mais informações sobre os recursos disponíveis por meio da API, consulte:

* A variável [API REST de ativos](/help/assets/mac-api-assets.md)
* [Tipos de entidade](/help/assets/content-fragments/assets-api-content-fragments.md#entity-types), em que os recursos específicos de cada tipo suportado (conforme relevante para os Fragmentos de conteúdo) são explicados

### Paginação {#paging}

A API REST do Assets oferece suporte à paginação (para solicitações GET) por meio dos parâmetros de URL:

* `offset` - o número da primeira entidade (secundária) a ser recuperada
* `limit` - o número máximo de entidades retornadas

A resposta contém informações de paginação como parte da variável `properties` seção da saída SIREN. Este `srn:paging` contém o número total de entidades (filhas) ( `total`), o deslocamento e o limite ( `offset`, `limit`) conforme especificado na solicitação.

>[!NOTE]
>
>A paginação normalmente é aplicada em entidades de contêiner (ou seja, pastas ou ativos com representações), pois está relacionada aos filhos da entidade solicitada.

#### Exemplo: Paginação {#example-paging}

`GET /api/assets.json?offset=2&limit=3`

```json
...
"properties": {
    ...
    "srn:paging": {
        "total": 7,
        "offset": 2,
        "limit": 3
    }
    ...
}
...
```

## Tipos de entidade {#entity-types}

### Pastas {#folders}

As pastas atuam como containers para ativos e outras pastas. Elas refletem a estrutura do repositório de conteúdo do AEM.

A API REST do Assets expõe o acesso às propriedades de uma pasta. Por exemplo, seu nome e título. Os ativos são expostos como entidades filhas de pastas e subpastas.

>[!NOTE]
>
>Dependendo do tipo de ativo dos ativos e pastas secundários, a lista de entidades secundárias pode já conter o conjunto completo de propriedades que define a respectiva entidade secundária. Como alternativa, somente um conjunto reduzido de propriedades pode ser exposto para uma entidade nesta lista de entidades filhas.

### Assets {#assets}

Se um ativo for solicitado, a resposta retornará seus metadados; como título, nome e outras informações conforme definido pelo respectivo esquema de ativo.

Os dados binários de um ativo são expostos como um link SIREN do tipo `content`.

Os ativos podem ter várias representações. Normalmente, elas são expostas como entidades filhas, com uma exceção sendo uma representação em miniatura, que é exposta como um link do tipo `thumbnail` ( `rel="thumbnail"`).

### Fragmentos de conteúdo {#content-fragments}

A [fragmento de conteúdo](/help/assets/content-fragments/content-fragments.md) O é um tipo especial de ativo. Eles podem ser usados para acessar dados estruturados, como textos, números, datas, entre outros.

Uma vez que existem várias diferenças em *padrão* ativos (como imagens ou áudio), algumas regras adicionais se aplicam à sua manipulação.

#### Representação {#representation}

Fragmentos de conteúdo:

* Não exponha dados binários.
* Estão contidos na saída JSON (dentro da variável `properties` propriedade).

* Eles também são considerados atômicos. Ou seja, os elementos e as variações são expostos como parte das propriedades do fragmento em vez de como links ou entidades filhas. Isso permite acesso eficiente à carga útil de um fragmento.

#### Modelos de conteúdo e fragmentos de conteúdo {#content-models-and-content-fragments}

Atualmente, os modelos que definem a estrutura de um fragmento de conteúdo não são expostos por meio de uma API HTTP. Por conseguinte, a *consumidor* O deve saber sobre o modelo de um fragmento (pelo menos um mínimo) - embora a maioria das informações possa ser inferida da carga; como os tipos de dados, e assim por diante, fazem parte da definição.

Para criar um fragmento de conteúdo, o caminho (repositório interno) do modelo deve ser fornecido.

#### Conteúdo associado {#associated-content}

O conteúdo associado não é exposto.

## Usar {#using}

O uso pode variar dependendo se você está usando um ambiente de Autor ou Publicação de AEM, juntamente com seu caso de uso específico.

* Recomenda-se que a criação seja vinculada a uma instância de Autor ([e, no momento, não há como replicar um fragmento para publicar usando essa API](/help/assets/content-fragments/assets-api-content-fragments.md#limitations)).
* A entrega é possível de ambos os ambientes, pois o AEM apresenta o conteúdo solicitado somente no formato JSON.

   * O armazenamento e a entrega de uma instância de autor do AEM devem ser suficientes para aplicativos de biblioteca de mídia com firewall.

   * Para entrega ao vivo pela Web, recomenda-se uma instância de publicação do AEM.

>[!CAUTION]
>
>A configuração do Dispatcher em instâncias de nuvem AEM pode bloquear o acesso a `/api`.

>[!NOTE]
>
>Consulte a [Referência da API](/help/assets/content-fragments/assets-api-content-fragments.md#api-reference). Em especial, a seção [API do Adobe Experience Manager Assets - Fragmentos de conteúdo](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/assets-api-content-fragments/index.html).

## Limitações {#limitations}

Existem algumas limitações:

* **Os modelos de fragmento de conteúdo não são compatíveis no momento**: elas não podem ser lidas ou criadas. Para criar ou atualizar um fragmento de conteúdo existente, os desenvolvedores precisam saber o caminho correto para o modelo do fragmento de conteúdo. Atualmente, o único método para obter uma visão geral é por meio da interface de administração.
* **As referências são ignoradas**. Atualmente, não há verificações sobre se um fragmento de conteúdo existente é referenciado. Portanto, por exemplo, excluir um fragmento de conteúdo pode resultar em problemas em uma página que contém uma referência ao fragmento de conteúdo excluído.
* **Tipo de dados JSON** A saída da API REST do *Tipo de dados JSON* é *saída baseada em sequência*.

## Códigos de status e mensagens de erro {#status-codes-and-error-messages}

Os seguintes códigos de status podem ser vistos nas circunstâncias relevantes:

* **200** (OK)

  Retornado quando:

   * solicitar um fragmento de conteúdo por meio de `GET`
   * atualização bem-sucedida de um fragmento de conteúdo por meio de `PUT`

* **201** (Criado)

  Retornado quando:

   * criar um fragmento de conteúdo com sucesso por meio de `POST`

* **404** (Não encontrado)

  Retornado quando:

   * o fragmento de conteúdo solicitado não existe

* **500** (Erro interno do servidor)

  >[!NOTE]
  >
  >Esse erro é retornado:
  >
  >* quando ocorreu um erro que não pode ser identificado com um código específico
  >* quando a carga fornecida não era válida

  A seguir, há uma lista de cenários comuns em que esse status de erro é retornado, juntamente com a mensagem de erro (monospace) gerada:

   * A pasta primária não existe (ao criar um fragmento de conteúdo por meio de `POST`)
   * Nenhum modelo de fragmento de conteúdo foi fornecido (cq:model está ausente), não pode ser lido (devido a um caminho inválido ou um problema de permissão) ou não há um modelo de fragmento válido:

      * `No content fragment model specified`
      * `Cannot create a resource of given model '/foo/bar/qux'`

   * Não foi possível criar o fragmento de conteúdo (possivelmente um problema de permissão):

      * `Could not create content fragment`

   * Não foi possível atualizar o título e/ou a descrição:

      * `Could not set value on content fragment`

   * Não foi possível definir os metadados:

      * `Could not set metadata on content fragment`

   * O elemento de conteúdo não pôde ser encontrado ou atualizado

      * `Could not update content element`
      * `Could not update fragment data of element`

  As mensagens de erro detalhadas são retornadas da seguinte maneira:

  ```xml
  {
    "class": "core/response",
    "properties": {
      "path": "/api/assets/foo/bar/qux",
      "location": "/api/assets/foo/bar/qux.json",
      "parentLocation": "/api/assets/foo/bar.json",
      "status.code": 500,
      "status.message": "...{error message}.."
    }
  }
  ```

## Referência da API  {#api-reference}

Consulte esta página para obter referências detalhadas de API:

* [API do Adobe Experience Manager Assets - Fragmentos de conteúdo](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/assets-api-content-fragments/index.html)

* [API HTTP de ativos](/help/assets/mac-api-assets.md)

   * [Recursos disponíveis](/help/assets/mac-api-assets.md#available-features)

## Recursos adicionais {#additional-resources}

Para obter mais informações, consulte:

* [Documentação da API HTTP do Assets](/help/assets/mac-api-assets.md)
* [Sessão Gem AEM: OAuth](https://experienceleague.adobe.com/docs/events/experience-manager-gems-recordings/gems2014/aem-oauth-server-functionality-in-aem.html?lang=en)
