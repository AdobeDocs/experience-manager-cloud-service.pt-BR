---
title: Não permitir a serialização de ResourceResolvers por meio do Exportador de Modelo do Sling
description: Não permitir a serialização de ResourceResolvers por meio do Exportador de Modelo do Sling
source-git-commit: 4543a4646719f8433df7589b21344433c43ab432
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 0%

---


# Não permitir a serialização de ResourceResolvers por meio do Exportador de Modelo do Sling {#disallow-the-serialization-of-resourceresolvers-via-sling-model-exporter}

O recurso Exportador de modelo Sling permite serializar objetos Modelos Sling em um formato JSON. Esse recurso é amplamente usado, pois permite que o SPA (aplicativos de página única) acesse facilmente os dados do AEM. No lado da implementação, a biblioteca de ligação de dados Jacson é usada para serializar esses objetos.

A serialização é uma operação recursiva. Começando por um &quot;objeto raiz&quot;, ele repete recursivamente todos os objetos elegíveis e os serializa e seus filhos. Você pode encontrar uma descrição em quais campos são serializados [este artigo](https://www.baeldung.com/jackson-field-serializable-deserializable-or-not).

Essa abordagem serializa todos os tipos de objetos no JSON e, naturalmente, também pode serializar um Sling `ResourceResolver` objeto, se estiver coberto pelas regras de serialização. Isto é problemático, uma vez que a `ResourceResolver` O serviço (e, portanto, também o objeto de serviço que o representa) contém informações potencialmente sensíveis, que não devem ser divulgadas. Por exemplo:

* A ID do usuário
* Os caminhos de pesquisa para resolver caminhos relativos
* A variável `propertyMap`.

Especialmente sensível é a `propertyMap` (consulte a documentação da API do [`getPropertyMap`](https://sling.apache.org/apidocs/sling12/org/apache/sling/api/resource/ResourceResolver.html#getPropertyMap--)), pois é uma estrutura de dados interna, que pode ser usada para várias finalidades - por exemplo, armazenamento em cache de objetos que compartilham o mesmo ciclo de vida que a `ResourceResolver`. A serialização desses itens pode vazar detalhes de implementação e possivelmente ter um impacto na segurança, pois os dados são expostos e não devem ser legíveis e acessíveis para um usuário final. Por esse motivo `ResourceResolvers` não deve ser serializado no JSON.

O Adobe planeja desativar a serialização de `ResourceResolvers` em uma abordagem de duas etapas:

1. Começando com o AEM as a Cloud Service versão 14697, sempre que um `ResourceResolver` O AEM serializado registrará uma mensagem de aviso. Todos os clientes são incentivados a verificar seus logs de aplicativo para obter essas instruções de log e adaptar sua base de código de acordo.
1. Em um ponto posterior, o Adobe desativará a serialização de ResourceResolvers como JSON.

## Implementação {#implementation}

A mensagem de AVISO é registrada em instâncias de SDK do AEM as a Cloud Service e do AEM local, e tem a seguinte aparência:

```
[127.0.0.1 [1705061734620] GET /content/../page.model.json HTTP/1.1] org.apache.sling.models.jacksonexporter.impl.JacksonExporter A ResourceResolver is serialized with all its private fields containing implementation details you should not disclose. Please review your Sling Model implementation(s) and remove all public accessors to a ResourceResolver.
```

Esta mensagem de log significa que, durante o processo de serialização do `/content/…/page` no JSON a `ResourceResolver` já está serializado. Ao solicitar `/content/../page.model.json` é possível verificar onde exatamente os campos da `ResourceResolver` são exibidas e use-as para identificar a classe Modelo do Sling que está realmente acionando esse comportamento.


>[!NOTE]
>
>Os Componentes principais do AEM foram validados para não serem afetados por esse problema.

## Ação solicitada {#requested-action}

O Adobe solicita que todos os clientes verifiquem os logs do aplicativo e as bases de código para ver se são afetados por esse problema e altere o aplicativo personalizado onde for necessário, para que essa mensagem de AVISO não seja mais exibida.

Pressupõe-se que, na maioria dos casos, estas alterações necessárias sejam `ResourceResolver` Os objetos do não são necessários na saída JSON, pois as informações contidas neles normalmente não são exigidas pelos aplicativos de front-end. Isso significa que, na maioria dos casos, deve ser suficiente excluir a `ResourceResolver` objeto de ser considerado pela Jackson (consulte o [regras](https://www.baeldung.com/jackson-field-serializable-deserializable-or-not)).

No caso de um Modelo Sling ser afetado por esse problema, mas não alterado, a desativação explícita da serialização do `ResourceResolver` O objeto (executado pelo Adobe como a 2ª etapa) forçará uma alteração na saída JSON.



