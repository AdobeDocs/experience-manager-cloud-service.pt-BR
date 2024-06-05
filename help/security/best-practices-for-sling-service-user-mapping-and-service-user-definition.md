---
title: Práticas recomendadas para o mapeamento de usuário do serviço Sling e definição do usuário do serviço
description: Saiba mais sobre as práticas recomendadas para o mapeamento de usuários do serviço do sling e a definição de usuários do serviço
exl-id: 72f0dcbf-b4e6-4a73-8232-3574a212ac19
feature: Security
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '1884'
ht-degree: 0%

---

# Práticas recomendadas para o mapeamento de usuário do serviço Sling e definição do usuário do serviço {#best-practices-for-sling-service-user-mapping-and-service-user-definition}

## Mapeamento de usuário de serviço {#service-user-mapping}

Para adicionar um mapeamento de seu serviço ao(s) usuário(s) do sistema correspondente(s), é necessário criar uma configuração de fábrica para o `ServiceUserMapper` serviço. Para manter essa modular, essas configurações podem ser fornecidas usando o mecanismo Sling &quot;mend&quot; (consulte [SLING-3578](https://issues.apache.org/jira/browse/SLING-3578) para obter mais detalhes). A maneira recomendada de instalar essas configurações com seu pacote é adicionando-o ao modelo de provisionamento Quickstart, conforme descrito no exemplo a seguir:

```
org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.amended-my-mapping
    user.default=""
    user.mapping=[
        "com.adobe.cq.my-bundle:my-subservice\=[content-writer-service]",
        "com.adobe.cq.my-bundle:my-subservice-different-task\="[myfeature-configuration-writer-service,content-reader-service]"
    ]
```

### Formato de mapeamento {#mapping-format}

A partir do AEM 6.4, o formato de mapeamento é definido da seguinte maneira:

>[!NOTE]
>
>A variável `userName` está obsoleto e não deve mais ser usado.

```
bundleId [:subserviceName] = userName | [principalNames]   
```

`bundleId` e `subserviceName` identificar o serviço, `userName/principalNames` identificar o usuário do serviço e `principalNames` é uma lista separada por vírgulas.

Observe também que `principalNames` é a lista de nomes principais de usuários de serviço que são iguais à id e prontos para uso.


**Prática recomendada**

* Nomes de subserviços para tarefas diferentes - se os serviços do seu pacote executarem tarefas diferentes, é recomendável identificar `subserviceNames` para agrupá-los por tarefas
* Se um determinado serviço executar operações diferentes (por exemplo, ler o conteúdo do ativo e atualizar as informações abaixo de uma subárvore de `/var`), é recomendável refletir isso agregando diferentes entidades de serviço que refletem a operação individual, como agregando o `dam-reader-service` com seu recurso específico `assetreport-writer-service`
* Idealmente, cada serviço está vinculado a um conjunto muito específico e limitado de operações
* O novo formato com `[one,or,multiple,principalNames]` O é a maneira recomendada de definir os mapeamentos de usuário do serviço a partir do AEM 6.4.

Veja abaixo uma lista dos motivos para alterar o formato e por que o Adobe recomenda usá-lo em vez do mapeamento de versão apenas para uma única ID de usuário:

* A capacidade de reutilizar usuários de serviço combinando as necessidades especiais dos clientes com tarefas comuns
* Evitar duplicação da configuração de permissão
* Melhor compreensão das permissões (e tarefas) eficazes que um determinado serviço está realmente executando
* Não há necessidade de associação explícita de grupo de usuários de serviço. Isso pode ter efeitos colaterais problemáticos à medida que as permissões de grupo forem alteradas
* Melhorias de desempenho e escalabilidade

## Resolução de mapeamento e logon de serviço {#mapping-resolution-and-service-login}

### Resolução de mapeamento de serviço {#service-mapping-resolution}

A sequência de chamadas para resolver o mapeamento de serviço descrito abaixo:

1. Pesquisar por ativos `principalNames` mapeamento para o dado `bundleId` e `subserviceName`
1. `principalNames` mapeamento para o `bundleId` e nulo `subserviceName`
1. `userName` mapeamento para o `bundleId` e `subserviceName`
1. `userName` mapeamento para `bundleId` e nulo `subserviceName`
1. Mapeamento padrão
1. Usuário padrão

### SlingRepository - logon do serviço {#slingrepository-servicelogin}

A sequência para obter um serviço `Session/ResourceResolver` funciona da seguinte forma:

1. Obter nomes principais de `ServiceUserMapper` => logon de repositório de pré-autenticação conforme descrito abaixo
1. Recuperar ID de usuário de `ServiceUserMapper`
1. Verificar 1ServiceUserConfiguration` obsoleto para a id do usuário atual
1. Logon de serviço do Sling padrão com a ID do usuário (por exemplo, uma sequência de `createAdministrativeSession` e representar para a id de usuário do serviço)

O novo mapeamento com nomes principais resulta no seguinte logon de repositório simplificado:

* O conjunto de nomes principais é tratado como o principal ou principais efetivos a serem usados para preencher o `Subject`
* Consequentemente, o logon no repositório pode ser pré-autenticado
* Nenhuma resolução de associação de grupo

  >[!NOTE]
  >
  >Todas as permissões necessárias precisam ser declaradas para os usuários do serviço. &#39;todos&#39; e outras permissões do Grupo não serão mais herdadas.

* Não é necessário fazer logon administrativo adicional para que o serviço-`Session/ResourceResolver` são criados.

### ServiceUserConfiguration obsoleto {#deprecated-serviceUserConfiguration}

Observe que especificar um único nome de usuário no mapeamento é equivalente ao nome `ServiceUserConfiguration.simpleSubjectPopulation`. Com o novo formato, a solução alternativa fornecida pelo `ServiceUserConfiguration` pode ser refletido diretamente no mapeamento do usuário do serviço. A variável `ServiceUserConfiguration` foi, portanto, descontinuado para AEM e todos os usos existentes foram substituídos.

## Usuários de serviço {#service-users}

### Reutilizar Usuários de Serviços Existentes {#reusing-existing-service-users}

É recomendável reutilizar usuários de serviço existentes se as seguintes condições forem atendidas:

* Suas necessidades correspondem à intenção do usuário do serviço existente
* Seu serviço requer a execução de uma tarefa comum coberta por um usuário de serviço comum existente. Nesse caso, é recomendável reutilizar o usuário do serviço em vez de introduzir a duplicação
* Seu serviço requer uma tarefa específica coberta por um usuário de serviço existente. Se não tiver certeza sobre isso, pergunte à equipe de recursos proprietária.

Não reutilizar usuários de serviço existentes se:

* Você precisaria modificar a permissão de maneira não relacionada para que funcionasse
* Se você precisar apenas de um pequeno subconjunto da permissão fornecida e reutilizá-lo, pois isso faz com que o recurso funcione, não porque é uma correspondência real
* Se o nome indicar uma intenção totalmente diferente da que você precisa. Escolhê-lo porque funciona pode causar problemas no futuro, pois a equipe de recursos que possui um serviço específico pode alterar as permissões e interromper seu recurso.

### Criando um Usuário de Serviço {#creating-a-service-user}

Depois de verificar que nenhum usuário de serviço existente no AEM é aplicável ao seu caso de uso e que os problemas de RTC correspondentes foram aprovados, você pode adicionar o novo usuário ao conteúdo padrão. Idealmente, um membro da equipe de segurança estendida está envolvido na votação do RTC, portanto, certifique-se de envolver também as partes interessadas apropriadas.

**Convenção de nomeação**

A equipe de segurança do AEM definiu a seguinte convenção de nomenclatura para os usuários de serviço, a fim de adicionar consistência aos novos usuários de serviço e melhorar sua legibilidade e manutenção.

Um nome de usuário de serviço consiste em 3 elementos separados por um traço **&#39;-&#39;**:

1. A entidade/recurso lógico que é direcionado pelas operações de serviço (evite caminhos de elementos que podem ser alterados)
1. A tarefa que os serviços vão executar
1. À Direita **&#39;serviço&#39;** para poder detectar facilmente, a partir da id e do nome principal, que o usuário é um usuário de serviço

**Práticas recomendadas**

* Não misture entidades/recursos diferentes. Dividir para usuários de serviço individuais e agregá-los no mapeamento se o serviço tiver necessidades diferentes
* Limite-se a uma tarefa bem definida por usuário de serviço. Dividir se você acabar concedendo muitas permissões ou permissões não relacionadas
* Gaste tempo identificando a real necessidade do seu serviço
* Gaste tempo procurando um nome de usuário de serviço bom, significativo e autoexplicativo
* Peça feedback e revise: os desenvolvedores que não estiverem familiarizados com seu recurso devem ler e entender sua intenção. Eles podem, no futuro, ser incumbidos de corrigi-lo ou mantê-lo.

No final, o nome de usuário do serviço deve revelar:

* Como ele deve ser usado e se pode ser reutilizado:

   * Muito genérico: `content-writer-service`. É seguro reutilizar na agregação se os serviços também precisarem ler todo o conteúdo
   * Muito específico: `asset-linkshare-service`. Não é tão seguro reutilizar a menos que seu serviço realmente faça o compartilhamento de links de ativos também.

* Como deve ser o conjunto de recursos e a configuração de permissão:

   * A entidade lógica precisa corresponder à configuração de permissão:

      * A `content-foo-service` deve ser associado apenas a operações no conteúdo. A concessão de permissões para operar em outras entidades, como configuração ou usuários, seria incorreta
      * Um serviço específico como `personalization-foo-service` O também deve ser fornecido com permissões específicas. Se você acabar concedendo permissões em todo o conteúdo, ele não será mais específico. Refletir isso no nome ou reutilizar um usuário comum na agregação
      * Um serviço específico de recursos, como o `msm-xyz-service` deve ter somente permissões relacionadas ao msm. Não expanda as permissões para recursos não relacionados, como gerenciar configurações de comunidades ou usuários do Screens.

   * A tarefa precisa corresponder às permissões:

      * A `foo-reader-service` O só deve ser capaz de ler itens comuns. Nunca conceder permissões de gravação
      * A `foo-writer-service` executar operações de gravação. No entanto, não deve receber permissões para ler/modificar o conteúdo do controle de acesso
      * A `foo-replicator-service` espera-se que o `crx:replicate` concedido.

**Exemplos**

Exemplos para `configuration-reader-service`:

* O nome indica que se refere às configurações em geral e não à configuração de um recurso específico, como a configuração da integração do DM. Um usuário de serviço direcionado especificamente para a configuração de leitura dessa integração preferiria ser nomeado `dmconfig-reader-service` ou `s7config-reader-service`

  >[!NOTE]
  >
  >Nenhuma informação de caminho está incluída na nomeação. As configurações foram movidas de `/etc` para `/conf`.

* O elemento tarefa indica que os serviços vinculados a esse usuário só executarão operações de leitura.

Exemplos para `userproperties-copy-service`:

* Os serviços vinculados a este usuário de serviço operarão nas propriedades do usuário/grupo, como perfis ou preferências
* Ele é direcionado especificamente para apenas copiar essas informações, ao contrário de um nome como `userproperties-writer-service` que incluiria qualquer tipo de operação de gravação. Portanto, seria possível que a configuração de permissão dessas tarefas de cópia só permitisse adicionar itens em um local e remover itens em outro local.

**Práticas recomendadas para configuração de permissões**

* Sempre usar a configuração do controle de acesso baseado na entidade de segurança para usuários do serviço. Para obter mais detalhes, consulte os exemplos abaixo:

   * Permitir marcar usuários do serviço e suas permissões como conteúdo de aplicativo imutável no skyline
   * Não é necessário criar caminhos e estruturas de árvore

* Conceder somente permissões, nunca negar
* Limitar permissões

   * Conceda somente o conjunto mínimo de permissões necessárias
   * Para obter mais informações, consulte o [Mapeando Privilégios a Itens](https://jackrabbit.apache.org/oak/docs/security/privilege/mappingtoitems.html) e [Mapeamento de chamadas de API para privilégios](https://jackrabbit.apache.org/oak/docs/security/privilege/mappingtoprivileges.html) documentação
   * Não conceder permissão para `jcr:all`. Esse provavelmente não é o conjunto mínimo.

* Reduzir escopo

   * Colocar políticas de controle de acesso em subárvores específicas de recursos
   * No caso de itens distribuídos: use restrições para limitar o escopo (consulte [a documentação](http://jackrabbit.apache.org/oak/docs/security/authorization/restriction.html) para obter a lista de restrições incorporadas).

* Garantir a consistência

   * Tornar as permissões consistentes com a entidade e a tarefa usadas no nome de usuário do serviço
   * Evite adicionar permissões não relacionadas. Por exemplo, seria estranho ter uma variável `workflow-administration-service` e conceder permissões de ti para executar operações de gerenciamento de usuários em `/home/users/screens` ou deixe ler s7-config.

* Integralidade

   * Verifique se o serviço tem todas as permissões necessárias para executar as tarefas para as quais foi projetado. Seu serviço precisa funcionar imediatamente também em ambientes do cliente.
   * Nunca espere/peça aos clientes para expandir a configuração de permissão (por exemplo, abaixo `/apps`)

* Evitar duplicação da configuração de permissão

   * Reutilizar usuários comuns de serviços
   * Agregue-os aos usuários de serviço específicos do seu recurso que fornecem a permissão específica necessária, além disso

* Não divida a configuração de permissão em diferentes recursos. A necessidade de fazer isso indica que o usuário do serviço não está bem definido ou faz muitas coisas diferentes
* Não coloque usuários de serviço em grupos, pois:

   * Ele combina detalhes de implementação de usuários de serviço com grupos &quot;públicos&quot;
   * Você não tem controle sobre as alterações de permissão (propenso a regressões e escalonamentos de privilégio)
   * Desempenho de logon e avaliação
   * Não funciona com a configuração AC baseada em entidade

* O acesso ao nó user-home (ou qualquer subárvore contida nele), que não tem um caminho previsível, é obtido no repo init usando home(`userId`). Consulte a inicialização do sling repo [documentação](https://sling.apache.org/documentation/bundles/repository-initialization.html) para obter detalhes.
* RTC: crie um problema de RTC dedicado se você alterar as permissões de um usuário de serviço existente e garantir que você o analise pela equipe de segurança.

**Criação com inicialização de repositório**

Sempre usar `repo-init` para definir os usuários de serviço e a configuração de suas permissões, coloque ambos na seção correta do modelo de recurso Quickstart:

**Práticas recomendadas**

* Sempre usar `repo-init` para criar o usuário do serviço
* Sempre especificar um caminho intermediário para a criação do usuário de serviço
* Todos os usuários do serviço integrado para AEM devem estar localizados abaixo `system/cq:services/internal`
* Além disso, anexe ao caminho relativo intermediário para agrupar usuários de serviço por recurso: `system/cq:services/internal/<your-feature>`
* Os usuários do serviço definido pelo cliente devem estar localizados abaixo `system/cq:services/<customer-intermediate-rel-path>` e nunca abaixo da árvore interna
* Uso **com caminho forçado** em vez de **com caminho** se um usuário já existia e precisa ser movido para o novo local que suporta a autorização baseada em principal.

**Exemplos**

```
create service user my-new-feature-readcomment-service with path system/cq:services/internal/myfeature
set principal ACL for my-new-feature-readcomment-service
    allow rep:readProperties on /content/myFeature restriction(rep:itemNames,commentTitle,commentDate,commentTxt)
end
```

```
create service user my-existing-feature-addcomment-service with forced path system/cq:services/internal/myfeature
set principal ACL for my-existing-feature-addcomment-service
    allow jcr:addChildNodes,rep:addProperties on /content/myfeature restrictions(rep:glob,*/comments/*)
end
```

```
create service user myfeature-ims-service with path system/cq:services/internal/myfeature
set principal ACL for myfeature-ims-service
    allow jcr:read on home(myfeature-ims-service)
end
```

### Usuários e permissões do serviço de limpeza {#cleanup-service-users-and-permissions}

O seguinte comando repo init pode ser usado para limpar usuários de serviço não utilizados e suas permissões:

```
# Remove the principal-based access control policy for principal my-feature-service
delete principal ACL for my-feature-service

# Remove all resource-based access control entries (ACEs) for principal my-feature-service
delete ACL for my-feature-service

# Disable the service user
disable service user my-feature-service : "My feature is no longer used"

# Remove the service user
delete service my-feature-service 
```

### Usuários de Serviço de Teste {#testing-service-users}

É crucial gravar testes no lado do servidor para usuários de serviço e sua configuração de permissão. Isso não só verifica se a configuração realmente funciona, como também ajuda a detectar regressões e erros não intencionais ao alterar o controle de acesso de usuários de conteúdo ou serviço.

A variável `com.adobe.granite.testing.clients` A biblioteca do fornece vários utilitários que facilitam a gravação de SSTs para usuários de serviço.
