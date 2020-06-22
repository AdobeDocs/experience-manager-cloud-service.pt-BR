---
title: Adobe Experience Manager como suporte a fragmentos de conteúdo do Cloud Service na API HTTP Assets
description: Saiba mais sobre o Adobe Experience Manager como suporte a fragmentos de conteúdo do Cloud Service na API HTTP Assets.
translation-type: tm+mt
source-git-commit: efbd21aa7d8aa5b32d0af720466e4ffe92a012dd
workflow-type: tm+mt
source-wordcount: '1891'
ht-degree: 2%

---


# Suporte a Fragmentos de conteúdo na API HTTP do AEM Assets{#content-fragments-support-in-aem-assets-http-api}

## Visão geral {#overview}

>[!NOTE]
>
>A API [HTTP](/help/assets/mac-api-assets.md) Assets engloba:
>
>* API REST de ativos
>* incluindo suporte para fragmentos de conteúdo

>
>
A implementação atual da API HTTP Assets baseia-se no estilo de arquitetura [REST](https://en.wikipedia.org/wiki/Representational_state_transfer) .

A API [REST de](/help/assets/mac-api-assets.md) ativos permite que os desenvolvedores do Adobe Experience Manager como Cloud Service acessem o conteúdo (armazenado no AEM) diretamente pela API HTTP, por meio de operações CRUD (Criar, Ler, Atualizar, Excluir).

A API permite que você opere o Adobe Experience Manager como um Cloud Service como um CMS sem cabeçalho (Gestão de conteúdo System), fornecendo Serviços de conteúdo a um aplicativo front-end JavaScript. Ou qualquer outro aplicativo que possa executar solicitações HTTP e manipular respostas JSON.

Por exemplo, aplicativos de página única (SPA), baseados em estrutura ou personalizados, exigem conteúdo fornecido pela API HTTP, geralmente no formato JSON.

Embora os componentes [principais do](https://docs.adobe.com/content/help/br/experience-manager-core-components/using/introduction.html) AEM ofereçam uma API abrangente, flexível e personalizável que possa servir as operações de Leitura necessárias para essa finalidade, e cuja saída JSON possa ser personalizada, eles exigem o know-how WCM do AEM (Gestão de conteúdo da Web) para implementação, pois devem ser hospedados em páginas baseadas em modelos dedicados do AEM. Nem todas as organizações de desenvolvimento da ZPE têm acesso direto a esses conhecimentos.

É quando a API REST de ativos pode ser usada. Ela permite que os desenvolvedores acessem ativos (por exemplo, imagens e fragmentos de conteúdo) diretamente, sem a necessidade de primeiro incorporá-los em uma página e entregar seu conteúdo em formato JSON serializado.

>[!NOTE]
>
>Não é possível personalizar a saída JSON da API REST de ativos.

A API REST de ativos também permite que os desenvolvedores modifiquem o conteúdo - criando novos ativos, atualizando ou excluindo ativos, fragmentos de conteúdo e pastas existentes.

A API REST de ativos:

* segue o princípio [HATEOAS](https://en.wikipedia.org/wiki/HATEOAS)

* implementa o formato [SIREN](https://github.com/kevinswiber/siren)

## Pré-requisitos {#prerequisites}

A API REST de ativos está disponível em cada instalação predefinida de um Adobe Experience Manager recente como uma versão de Cloud Service.

## Principais conceitos {#key-concepts}

A API REST de ativos oferta o acesso ao estilo [REST](https://en.wikipedia.org/wiki/Representational_state_transfer)a ativos armazenados em uma instância do AEM.

Ele usa o `/api/assets` terminal e exige que o caminho do ativo acesse-o (sem o pontilhado `/content/dam`).

* Isso significa que para acessar o ativo em:
   * `/content/dam/path/to/asset`
* Você precisa solicitar:
   * `/api/assets/path/to/asset`

Por exemplo, para acessar `/content/dam/wknd/en/adventures/cycling-tuscany`, solicitar `/api/assets/wknd/en/adventures/cycling-tuscany.json`

>[!NOTE]
>Acesso através de:
>* `/api/assets` **não** necessita do uso do `.model` seletor.
>* `/content/assets` **não** requer o uso do `.model` seletor.


O método HTTP determina a operação a ser executada:

* **GET** - para recuperar uma representação JSON de um ativo ou pasta
* **POST** - para criar novos ativos ou pastas
* **PUT** - para atualizar as propriedades de um ativo ou pasta
* **DELETE** - para excluir um ativo ou pasta

>[!NOTE]
>
>Os parâmetros do corpo da solicitação e/ou URL podem ser usados para configurar algumas dessas operações; por exemplo, defina que uma pasta ou um ativo deve ser criado por uma solicitação **POST** .

<!--
The exact format of supported requests is defined in the [API Reference](/help/assets/assets-api-content-fragments.md#api-reference) documentation.
-->

### Comportamento transacional {#transactional-behavior}

Todas as solicitações são atômicas.

Isso significa que as solicitações subsequentes (`write`) não podem ser combinadas em uma única transação que pode ser bem-sucedida ou falhar como uma única entidade.

### API REST do AEM (Assets) versus componentes do AEM {#aem-assets-rest-api-versus-aem-components}

<table>
 <thead>
  <tr>
   <td>Aspecto</td>
   <td>API REST de ativos<br/> </td>
   <td>Componente<br/> AEM (componentes usando modelos Sling)</td>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td>Casos de uso suportados</td>
   <td>Finalidade geral.</td>
   <td><p>Otimizado para consumo em um aplicativo de página única (SPA) ou em qualquer outro contexto (que consome conteúdo).</p> <p>Também pode conter informações de layout.</p> </td>
  </tr>
  <tr>
   <td>Operações suportadas</td>
   <td><p>Criar, Ler, Atualizar, Excluir.</p> <p>Com operações adicionais, dependendo do tipo de entidade.</p> </td>
   <td>Somente leitura.</td>
  </tr>
  <tr>
   <td>Acesso</td>
   <td><p>Pode ser acessado diretamente.</p> <p>Usa o <code>/api/assets </code>terminal, mapeado para <code>/content/dam</code> (no repositório).</p> 
   <p>Um caminho de exemplo seria: <code>/api/assets/wknd/en/adventures/cycling-tuscany.json</code></p>
   </td>
    <td><p>Precisa ser referenciado por meio de um componente AEM em uma página do AEM.</p> <p>Usa o <code>.model</code> seletor para criar a representação JSON.</p> <p>Um caminho de exemplo seria:<br/> <code>/content/wknd/language-masters/en/adventures/cycling-tuscany.model.json</code></p> 
   </td>
  </tr>
  <tr>
   <td>Segurança</td>
   <td><p>Várias opções são possíveis.</p> <p>É proposta a OAuth; pode ser configurado separadamente da configuração padrão.</p> </td>
   <td>Usa a configuração padrão do AEM.</td>
  </tr>
  <tr>
   <td>Observações arquitetônicas</td>
   <td><p>O acesso de gravação normalmente endereçará uma instância do autor.</p> <p>A leitura também pode ser direcionada para uma instância de publicação.</p> </td>
   <td>Como essa abordagem é somente leitura, normalmente será usada para instâncias de publicação.</td>
  </tr>
  <tr>
   <td>Saída</td>
   <td>Saída SIREN baseada em JSON: profundo, mas poderoso. Permite navegar dentro do conteúdo.</td>
   <td>Saída proprietária baseada em JSON; configurável por meio de modelos Sling. É difícil implementar a navegação na estrutura de conteúdo (mas não é necessariamente impossível).</td>
  </tr>
 </tbody>
</table>

### Segurança {#security}

Se a API REST de ativos for usada dentro de um ambiente sem requisitos específicos de autenticação, o filtro CORS do AEM precisará ser configurado corretamente.

>[!NOTE]
>
>Para obter mais informações, consulte:
>
>* [Explicação do CORS/AEM](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/cors-security-article-understand.html)
>* [Vídeo - Desenvolvimento para CORS com AEM](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/cors-security-technical-video-develop.html)

>



Em ambientes com requisitos de autenticação específicos, o OAuth é recomendado.

## Recursos disponíveis {#available-features}

Fragmentos de conteúdo são um tipo específico de Ativo, consulte [Trabalhar com fragmentos](/help/assets/content-fragments/content-fragments.md)de conteúdo.

Para obter mais informações sobre os recursos disponíveis por meio da API, consulte:

* A API REST [do Assets](/help/assets/mac-api-assets.md)
* [Tipos](/help/assets/assets-api-content-fragments.md#entity-types)de entidade, onde os recursos específicos para cada tipo suportado (conforme relevante para Fragmentos de conteúdo) são explicados

### Paginação {#paging}

A API REST de ativos suporta paginação (para solicitações GET) pelos parâmetros de URL:

* `offset` - o número da primeira entidade (filho) a recuperar
* `limit` - o número máximo de entidades devolvidas

A resposta conterá informações de paginação como parte da `properties` seção da saída SIREN. Essa `srn:paging` propriedade contém o número total de entidades (filhas) ( `total`), o deslocamento e o limite ( `offset`, `limit`) conforme especificado na solicitação.

>[!NOTE]
>
>O paginação normalmente é aplicado em entidades de container (ou seja, pastas ou ativos com renderizações), pois está relacionado aos filhos da entidade solicitada.

#### Exemplo: Paginação {#example-paging}

`GET /api/assets.json?offset=2&limit=3`

```
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

As pastas atuam como container para ativos e outras pastas. Elas refletem a estrutura do repositório de conteúdo do AEM.

A API REST de ativos expõe o acesso às propriedades de uma pasta; por exemplo, seu nome, título etc. Os ativos são expostos como entidades filhas de pastas e subpastas.

>[!NOTE]
>
>Dependendo do tipo de ativo dos ativos e pastas filho, a lista de entidades filhas já pode conter o conjunto completo de propriedades que define a respectiva entidade-filho. Como alternativa, apenas um conjunto reduzido de propriedades pode ser exposto para uma entidade nesta lista de entidades-filho.

### Ativos {#assets}

Se um ativo for solicitado, a resposta retornará seus metadados; como título, nome e outras informações, conforme definido pelo respectivo schema de ativos.

Os dados binários de um ativo são expostos como um link SIREN do tipo `content` (também conhecido como o `rel attribute`).

Os ativos podem ter várias representações. Normalmente, são expostos como entidades filhas, uma exceção é uma execução em miniatura, que é exposta como um link do tipo `thumbnail` ( `rel="thumbnail"`).

### Fragmentos de conteúdo {#content-fragments}

Um fragmento [de](/help/assets/content-fragments/content-fragments.md) conteúdo é um tipo especial de ativo. Eles podem ser usados para acessar dados estruturados, como textos, números, datas, entre outros.

Como há várias diferenças nos ativos *padrão* (como imagens ou áudio), algumas regras adicionais se aplicam ao seu manuseio.

#### Representação {#representation}

Fragmentos de conteúdo:

* Não exponha quaisquer dados binários.
* Estão completamente contidos na saída JSON (dentro da `properties` propriedade).

* Também são considerados atômicos, ou seja, os elementos e variações são expostos como parte das propriedades do fragmento vs. como links ou entidades filhas. Isso permite um acesso eficiente à carga de um fragmento.

#### Modelos de conteúdo e fragmentos de conteúdo {#content-models-and-content-fragments}

Atualmente, os modelos que definem a estrutura de um fragmento de conteúdo não são expostos por meio de uma API HTTP. Por conseguinte, o *consumidor* precisa de conhecer o modelo de um fragmento (pelo menos um mínimo) - embora a maior parte das informações possa ser inferida a partir da carga útil; como tipos de dados, etc. fazem parte da definição.

Para criar um novo fragmento de conteúdo, o caminho (repositório interno) do modelo deve ser fornecido.

#### Conteúdo associado {#associated-content}

O conteúdo associado não está exposto no momento.

## Usar {#using}

O uso pode ser diferente se você estiver usando um autor ou ambiente de publicação do AEM, juntamente com seu caso de uso específico.

* A criação é estritamente vinculada a uma instância do autor ([e atualmente não há como replicar um fragmento para publicação usando essa API](/help/assets/assets-api-content-fragments.md#limitations)).
* O Delivery é possível de ambos, pois o AEM serve o conteúdo solicitado somente no formato JSON.

   * O Armazenamento e o delivery de uma instância de autor de AEM devem ser suficientes para aplicativos de biblioteca de mídia atrás do firewall.

   * Para o delivery online ao vivo, uma instância de publicação do AEM é recomendada.

>[!CAUTION]
>
>A configuração do dispatcher em instâncias da nuvem do AEM pode bloquear o acesso ao `/api`.

<!--
>[!NOTE]
>
>For further details, see the [API Reference](/help/assets/assets-api-content-fragments.md#api-reference). In particular, [Adobe Experience Manager Assets API - Content Fragments](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/assets-api-content-fragments/index.html). 
-->

### Leitura/Delivery {#read-delivery}

O uso é feito via:

`GET /{cfParentPath}/{cfName}.json`

Por exemplo:

`http://<host>/api/assets/wknd/en/adventures/cycling-tuscany.json`

A resposta é JSON serializado com o conteúdo estruturado como no fragmento de conteúdo. As referências são enviadas como URLs de referência.

Dois tipos de operações de leitura são possíveis:

* Ao ler um fragmento de conteúdo específico por caminho, isso retorna a representação JSON do fragmento de conteúdo.
* Leitura de uma pasta de fragmentos de conteúdo por caminho: isso retorna as representações JSON de todos os fragmentos de conteúdo dentro da pasta.

### Criar {#create}

O uso é feito via:

`POST /{cfParentPath}/{cfName}`

O corpo deve conter uma representação JSON do fragmento de conteúdo a ser criado, incluindo qualquer conteúdo inicial que deve ser definido nos elementos do fragmento de conteúdo. É obrigatório definir a `cq:model` propriedade e deve apontar para um modelo de fragmento de conteúdo válido. Se isso não for feito, ocorrerá um erro. Também é necessário adicionar um cabeçalho `Content-Type` definido como `application/json`.

### Atualizar {#update}

O uso é via

`PUT /{cfParentPath}/{cfName}`

O corpo deve conter uma representação JSON do que deve ser atualizado para o fragmento de conteúdo fornecido.

Pode ser simplesmente o título ou a descrição de um fragmento de conteúdo, um único elemento ou todos os valores de elementos e/ou metadados.

### Exclua {#delete}

O uso é feito via:

`DELETE /{cfParentPath}/{cfName}`

## Limitações          {#limitations}

Há algumas limitações:

* **As variações não podem ser gravadas e atualizadas.** Se essas variações forem adicionadas a uma carga (por exemplo, para atualizações), elas serão ignoradas. No entanto, a variação será servida através do delivery ( `GET`).

* **Os modelos de fragmento de conteúdo não são suportados** no momento: eles não podem ser lidos ou criados. Para poder criar um novo fragmento de conteúdo ou atualizar um existente, os desenvolvedores precisam saber o caminho correto para o modelo de fragmento de conteúdo. Atualmente, o único método para obter uma visão geral desses recursos é por meio da interface de usuário administrativa.
* **As referências são ignoradas**. Atualmente, não há verificações para determinar se um fragmento de conteúdo existente é referenciado. Portanto, por exemplo, excluir um fragmento de conteúdo pode resultar em problemas em uma página que contenha uma referência ao fragmento de conteúdo excluído.

## Códigos de status e mensagens de erro {#status-codes-and-error-messages}

Os seguintes códigos de status podem ser vistos nas circunstâncias relevantes:

* **200** (OK)

   Retornado quando:

   * solicitação de um fragmento de conteúdo via `GET`

   * atualização bem-sucedida de um fragmento de conteúdo por meio de `PUT`

* **201** (Criado)

   Retornado quando:

   * criação de um fragmento de conteúdo por meio de `POST`

* **404** (Não encontrado)

   Retornado quando:

   * o fragmento de conteúdo solicitado não existe

* **500** (erro de servidor interno)

   >[!NOTE]
   >
   >Este erro é retornado:
   >
   >    * quando um erro que não pode ser identificado com um código específico tiver ocorrido
   >    * quando a carga fornecida não era válida


   O seguinte lista cenários comuns quando esse status de erro é retornado, juntamente com a mensagem de erro (monospace) gerada:

   * A pasta pai não existe (ao criar um fragmento de conteúdo via `POST`)
   * Nenhum modelo de fragmento de conteúdo é fornecido (cq:model está ausente), não pode ser lido (devido a um caminho inválido ou a um problema de permissão) ou não há um modelo de fragmento válido:

      * `No content fragment model specified`
      * `Cannot create a resource of given model '/foo/bar/qux'`
   * Não foi possível criar o fragmento do conteúdo (possivelmente um problema de permissão):

      * `Could not create content fragment`
   * Não foi possível atualizar o título e/ou a descrição:

      * `Could not set value on content fragment`
   * Não foi possível definir metadados:

      * `Could not set metadata on content fragment`
   * O elemento de conteúdo não foi encontrado ou não pôde ser atualizado

      * `Could not update content element`
      * `Could not update fragment data of element`

   As mensagens de erro detalhadas normalmente são retornadas da seguinte maneira:

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

## API Reference {#api-reference}

Consulte aqui para obter referências detalhadas da API:
<!--
* [Adobe Experience Manager Assets API - Content Fragments](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/assets-api-content-fragments/index.html)
-->

* [API HTTP de ativos](/help/assets/mac-api-assets.md)

   * [Recursos disponíveis](/help/assets/mac-api-assets.md#available-features)

## Recursos adicionais {#additional-resources}

Para obter mais informações, consulte:

* [Documentação da API HTTP de ativos](/help/assets/mac-api-assets.md)
* [Sessão do AEM Gem: OAuth](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-oauth-server-functionality-in-aem.html)

