---
title: Solução de problemas e perguntas frequentes do MSM
description: Descubra como solucionar os problemas mais comuns relacionados ao MSM e obter respostas para as perguntas mais comuns relacionadas ao MSM.
feature: Gerenciamento de vários sites
role: Admin
exl-id: 50f02f4f-a347-4619-ac90-b3136a7b1782
source-git-commit: 24a4a43cef9a579f9f2992a41c582f4a6c775bf3
workflow-type: tm+mt
source-wordcount: '761'
ht-degree: 0%

---

# Solução de problemas e perguntas frequentes do MSM {#troubleshooting-msm}

## Solução de problemas nas primeiras etapas {#first-steps}

Se você estiver experimentando o que acha que é um comportamento incorreto ou um erro no MSM, antes de começar e solucionar problemas detalhados, certifique-se de:

* Verifique as [Perguntas frequentes do MSM](#faq), pois seus problemas ou perguntas podem já ser resolvidos lá.
* Verifique o [artigo de práticas recomendadas do MSM](best-practices.md), pois várias dicas são oferecidas, juntamente com esclarecimentos de várias concepções erradas.

## Encontrar informações avançadas sobre seu blueprint e status da Live Copy {#advanced-info}

O MSM registra vários servlets que podem ser solicitados com seletores nos URLs do recurso. Eles são usados pela interface do usuário, mas também podem ser solicitados diretamente para ver diretamente status de MSM computado avançado adicionais para suas páginas:

1. `http://<host>:<port>/content/path/to/bluprint/page.blueprint.json?&maxSize=500&advancedStatus=true&returnRelationships=true&msm%3Atrigger=ROLLOUT`
   * Use-o em uma página de blueprint para recuperar a lista de todas as Live Copies vinculadas a ela, com informações adicionais sobre o status da Live Copy.
1. `http://<host>:<port>/content/path/to/livecopy/page.msm.json`
   * Use-o nas páginas de Live Copy para recuperar informações avançadas em sua conexão com suas páginas de blueprint. Se a página não for uma Live Copy, nada será retornado.

Esses servlets geram mensagens DEBUG Log por meio do logger `com.day.cq.wcm.msm` que também pode ser útil.

## Verificando informações específicas do MSM no repositório {#checking-repo}

Os servlets anteriores retornavam informações computadas com base nos nós e mixins específicos do MSM. As informações são armazenadas no repositório da seguinte maneira.

* `cq:LiveSync` tipo mixin
   * Isso é definido nos nós `jcr:content` e define as páginas raiz da Live Copy.
   * Essas páginas terão um nó filho `cq:LiveSyncConfig` do tipo `cq:LiveCopy` que conterá informações básicas e obrigatórias na Live Copy por meio das seguintes propriedades:
      * `cq:master` aponta para a página de blueprint do Live Copy.
      * `cq:rolloutConfigs` indica configurações de implementação ativas aplicadas à Live Copy.
      * `cq:isDeep` é verdadeiro se as páginas filhas desta página raiz da Live Copy estiverem incluídas na Live Copy.
* `cq:LiveRelationship` tipo mixin
   * Qualquer página da Live Copy tem esse tipo de mixin em seu nó `jcr:content`.
   * Caso contrário, a página foi desanexada ou criada manualmente por meio da interface de criação fora de uma ação de Live Copy (criar ou implantar).
* `cq:LiveSyncCancelled` tipo mixin
   * Adicionado aos nós `jcr:content` de páginas de Live Copy que foram suspensas.
   * Se a suspensão também for efetiva para páginas filhas, uma propriedade `cq:isCancelledForChildren` será definida como true no mesmo nó.

As informações presentes nessas propriedades devem ser refletidas na interface do usuário, no entanto, ao solucionar problemas, pode ser útil observar o comportamento do MSM diretamente no repositório, à medida que as ações do MSM ocorrem.

Conhecer essas propriedades também pode ser útil para consultar seu repositório e descobrir conjuntos de páginas que estão em estados específicos. Por exemplo:

* `select * from cq:LiveSync` retorna todas as páginas raiz da Live Copy.

## Perguntas frequentes {#faq}

Aqui estão algumas perguntas frequentes relacionadas ao MSM e Live Copy.

### Por que algumas propriedades (por exemplo, título, anotações) não são atualizadas durante uma implantação do MSM? {#missing-properties}

As ações de sincronização MSM são altamente configuráveis. Quais propriedades ou componentes são modificados durante as implantações dependem diretamente das propriedades dessas configurações.

Consulte [este artigo](best-practices.md) para obter mais informações sobre este tópico.

### Como posso remover as permissões de implantação de um grupo de autores? {#remove-rollout-permissions}

Não há privilégio **rollout** que possa ser definido ou removido para entidades principais AEM (usuários ou grupos).

Como alternativa, você pode:

* Personalize a interface do usuário do produto para ocultar as ações de Implantação de um determinado principal.
* Remova privilégios de gravação da árvore da Live Copy para autores que não têm permissão para implantar.

### Por que vejo páginas da Live Copy com o sufixo &quot;_msm_moved&quot;? {#moved-pages}

Se uma página de blueprint for implantada, ela atualizará sua página Live Copy ou criará uma nova página Live Copy se ainda não existir (por exemplo, quando ela for implantada pela primeira vez ou a página Live Copy for excluída manualmente).

Neste último caso, no entanto, se uma página sem uma propriedade `cq:LiveRelationship` existir com o mesmo nome, essa página será renomeada adequadamente, antes que a página Live Copy seja criada.

Por padrão, a implantação espera uma página vinculada da Live Copy, para a qual as atualizações dos blueprints serão implantadas ou nenhuma página em, quando uma página da Live Copy for criada.

Se uma página &quot;independente&quot; for encontrada, o MSM optará por renomear esta página e criar uma página separada e vinculada da Live Copy.

Essa página autônoma em uma subárvore do Live Copy geralmente é o resultado de uma operação **Desanexar**, ou a antiga página do Live Copy foi excluída manualmente por um autor e depois recriada com o mesmo nome.

Para evitar isso, use o recurso **Suspender** no lugar de **Desanexar**. Mais detalhes sobre a ação **Desanexar** em [este artigo.](creating-live-copies.md)
