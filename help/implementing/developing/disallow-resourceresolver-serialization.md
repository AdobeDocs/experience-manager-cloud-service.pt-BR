---
title: Não permitir a serialização de ResourceResolvers por meio do Exportador de Modelo do Sling
description: Não permitir a serialização de ResourceResolvers por meio do Exportador de Modelo do Sling
exl-id: 63972c1e-04bd-4eae-bb65-73361b676687
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 0%

---

# Não permitir a serialização de ResourceResolvers por meio do Exportador de Modelo do Sling {#disallow-the-serialization-of-resourceresolvers-via-sling-model-exporter}

O recurso Exportador de modelo Sling permite serializar objetos Modelo Sling no formato JSON. Esse recurso é amplamente usado, pois permite que os SPAs (aplicativos de página única) acessem dados facilmente do AEM. No lado da implementação, a biblioteca de ligação de dados Jackson é usada para serializar esses objetos.

A serialização é uma operação recursiva. Começando por um &quot;objeto raiz&quot;, ele repete recursivamente todos os objetos elegíveis e os serializa e seus filhos. Você pode encontrar uma descrição de quais campos são serializados no artigo [Jackson - Decidir quais campos são serializados/desserializados](https://www.baeldung.com/jackson-field-serializable-deserializable-or-not).

Essa abordagem serializa todos os tipos de objetos no JSON. Naturalmente, ele também pode serializar um objeto Sling `ResourceResolver`, se ele estiver coberto pelas regras de serialização. Isso é problemático, pois o serviço `ResourceResolver` (e, portanto, também o objeto de serviço que o representa) retém informações potencialmente confidenciais, que não devem ser divulgadas. Por exemplo:

* A ID do usuário
* Os caminhos de pesquisa para resolver caminhos relativos
* O `propertyMap`

Especialmente sensível é o `propertyMap` (consulte a documentação da API de [`getPropertyMap`](https://sling.apache.org/apidocs/sling12/org/apache/sling/api/resource/ResourceResolver.html#getPropertyMap--)), pois é uma estrutura de dados interna, que pode ser usada para muitos propósitos, por exemplo, armazenamento em cache de objetos que compartilham o mesmo ciclo de vida que o `ResourceResolver`. A serialização desses itens pode vazar detalhes de implementação e possivelmente ter um impacto na segurança, já que os dados são expostos e não devem ser legíveis e acessíveis para um usuário final. Por esse motivo, `ResourceResolvers` não deve ser serializado em JSON.

A Adobe planeja desabilitar a serialização de `ResourceResolvers` em uma abordagem de duas etapas:

1. A partir do AEM as a Cloud Service versão 14697, sempre que um `ResourceResolver` for serializado, a AEM registrará uma mensagem de aviso. Todos os clientes são incentivados a verificar seus logs de aplicativo para obter essas instruções de log e adaptar sua base de código de acordo.
1. Posteriormente, a Adobe desativará a serialização de `ResourceResolver`s como JSON.

## Implementação {#implementation}

A mensagem de AVISO é registrada em instâncias do AEM as a Cloud Service e do AEM SDK locais e tem a seguinte aparência:

```text
[127.0.0.1 [1705061734620] GET /content/../page.model.json HTTP/1.1] org.apache.sling.models.jacksonexporter.impl.JacksonExporter A ResourceResolver is serialized with all its private fields containing implementation details you should not disclose. Please review your Sling Model implementation(s) and remove all public accessors to a ResourceResolver.
```

Esta mensagem de log significa que, durante o processo de serialização de `/content/…/page` em JSON, `ResourceResolver` já está serializado. Ao solicitar `/content/../page.model.json`, você pode verificar onde exatamente os campos de `ResourceResolver` estão sendo exibidos e usá-los para identificar a classe do Modelo do Sling que está realmente acionando esse comportamento.


>[!NOTE]
>
>Os [Componentes principais do AEM](https://experienceleague.adobe.com/pt-br/docs/experience-manager-core-components/using/introduction) foram validados para não serem afetados por este problema.

## Ação solicitada {#requested-action}

A Adobe solicita que todos os clientes verifiquem seus logs de aplicativo e bases de código para ver se são afetados por esse problema e alterem o aplicativo personalizado quando necessário, para que essa mensagem de aviso não apareça mais nos logs.

Presume-se que, na maioria dos casos, essas alterações necessárias sejam diretas. Os objetos `ResourceResolver` não são necessários na saída JSON, pois as informações contidas neles normalmente não são exigidas pelos aplicativos de front-end, o que significa que, na maioria dos casos, deve ser suficiente excluir o objeto `ResourceResolver` de ser considerado por Jackson (consulte as [regras](https://www.baeldung.com/jackson-field-serializable-deserializable-or-not).)

Caso um Modelo do Sling seja afetado por esse problema, mas não alterado, a desabilitação explícita da serialização do objeto `ResourceResolver` (executada pelo Adobe como a segunda etapa) imporá uma alteração na saída JSON.
