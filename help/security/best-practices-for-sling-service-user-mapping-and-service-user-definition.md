---
title: Práticas recomendadas para o mapeamento de usuário do serviço Sling e definição do usuário do serviço
description: Saiba mais sobre as práticas recomendadas para o mapeamento de usuários do serviço do sling e a definição de usuários do serviço
exl-id: 72f0dcbf-b4e6-4a73-8232-3574a212ac19
feature: Security
role: Admin
source-git-commit: f28f212574dda0ece2cedb56a714d381e5bd7d3c
workflow-type: tm+mt
source-wordcount: '1884'
ht-degree: 0%

---

# Práticas recomendadas para o mapeamento de usuário do serviço Sling e definição do usuário do serviço {#best-practices-for-sling-service-user-mapping-and-service-user-definition}

## Mapeamento de usuário de serviço {#service-user-mapping}

Para adicionar um mapeamento de seu serviço ao(s) usuário(s) do sistema correspondente(s), é necessário criar uma configuração de fábrica para o serviço `ServiceUserMapper`. Para manter essa modular, essas configurações podem ser fornecidas usando o mecanismo Sling &quot;mend&quot; (consulte [SLING-3578](https://issues.apache.org/jira/browse/SLING-3578) para obter mais detalhes). A maneira recomendada de instalar essas configurações com seu pacote é adicionando-o ao modelo de provisionamento Quickstart, conforme descrito no exemplo a seguir:

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
>O `userName` está obsoleto e não deve ser mais usado.

```
bundleId [:subserviceName] = userName | [principalNames]   
```

`bundleId` e `subserviceName` identificam o serviço, `userName/principalNames` identificam o usuário do serviço e `principalNames` é uma lista separada por vírgulas.

Além disso, observe que `principalNames` é a lista de nomes principais de usuários de serviço que, prontos para uso, são iguais à ID.


**Prática recomendada**

* Nomes de subserviços para tarefas diferentes - se os serviços do seu conjunto executam tarefas diferentes, é recomendável identificar `subserviceNames` para agrupá-los por tarefas
* Se um determinado serviço executar operações diferentes (por exemplo, ler o conteúdo do ativo e atualizar as informações abaixo de uma subárvore de `/var`), é recomendável refletir isso agregando entidades de serviço diferentes que refletem a operação individual, como agregar o `dam-reader-service` comum com o `assetreport-writer-service` específico do recurso
* Idealmente, cada serviço está vinculado a um conjunto muito específico e limitado de operações
* O novo formato com `[one,or,multiple,principalNames]` é a maneira recomendada de definir mapeamentos de usuários de serviço a partir do AEM 6.4.

Veja abaixo uma lista dos motivos para alterar o formato e por que o Adobe recomenda usá-lo em vez do mapeamento de versão apenas para uma única ID de usuário:

* A capacidade de reutilizar usuários de serviço combinando as necessidades especiais dos clientes com tarefas comuns
* Evitar duplicação da configuração de permissão
* Melhor compreensão das permissões (e tarefas) eficazes que um determinado serviço está realmente executando
* Não há necessidade de associação explícita de grupo de usuários de serviço. Isso pode ter efeitos colaterais problemáticos à medida que as permissões de grupo forem alteradas
* Melhorias de desempenho e escalabilidade

## Resolução de mapeamento e logon de serviço {#mapping-resolution-and-service-login}

### Resolução de mapeamento de serviço {#service-mapping-resolution}

A sequência de chamadas para resolver o mapeamento de serviço descrito abaixo:

1. Pesquisar mapeamento `principalNames` ativo para o `bundleId` e `subserviceName` especificados
1. `principalNames` mapeamento para `bundleId` e `subserviceName` nulo
1. Mapeamento de `userName` para `bundleId` e `subserviceName`
1. `userName` mapeamento para `bundleId` e `subserviceName` nulo
1. Mapeamento padrão
1. Usuário padrão

### SlingRepository - logon do serviço {#slingrepository-servicelogin}

A sequência para obter um serviço `Session/ResourceResolver` funciona da seguinte maneira:

1. Obtenha nomes principais de `ServiceUserMapper` => logon de repositório de pré-autenticação conforme descrito abaixo
1. Recuperar ID de usuário de `ServiceUserMapper`
1. Verificar 1ServiceUserConfiguration` obsoleto para a id do usuário atual
1. Logon padrão do serviço Sling com a ID de usuário (por exemplo, uma sequência de `createAdministrativeSession` e representação da ID de usuário do serviço)

O novo mapeamento com nomes principais resulta no seguinte logon de repositório simplificado:

* O conjunto de nomes de entidade é tratado como a(s) entidade(s) de segurança efetiva(s) a ser(em) usada(s) para preencher o `Subject`
* Consequentemente, o logon no repositório pode ser pré-autenticado
* Nenhuma resolução de associação de grupo

  >[!NOTE]
  >
  >Todas as permissões necessárias precisam ser declaradas para os usuários do serviço. &#39;todos&#39; e outras permissões do Grupo não serão mais herdadas.

* Nenhum login de administrador adicional para que o serviço-`Session/ResourceResolver` seja criado.

### ServiceUserConfiguration obsoleto {#deprecated-serviceUserConfiguration}

Observe que especificar um único nome de usuário no mapeamento é equivalente ao `ServiceUserConfiguration.simpleSubjectPopulation` existente. Com o novo formato, a solução alternativa fornecida pelo `ServiceUserConfiguration` pode ser refletida diretamente no mapeamento de usuário do serviço. O `ServiceUserConfiguration` foi, portanto, descontinuado para AEM e todos os usos existentes foram substituídos.

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

**Convenção de Nomenclatura**

A equipe de segurança do AEM definiu a seguinte convenção de nomenclatura para os usuários de serviço, a fim de adicionar consistência aos novos usuários de serviço e melhorar sua legibilidade e manutenção.

Um nome de usuário de serviço consiste em 3 elementos separados por um traço **&#39;-&#39;**:

1. A entidade/recurso lógico que é direcionado pelas operações de serviço (evite caminhos de elementos que podem ser alterados)
1. A tarefa que os serviços vão executar
1. **&#39;serviço&#39;** à direita para poder detectar facilmente, a partir da ID e do nome principal, que o usuário é um usuário de serviço

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

      * Um `content-foo-service` deve ser associado somente a operações no conteúdo. A concessão de permissões para operar em outras entidades, como configuração ou usuários, seria incorreta
      * Um serviço específico como o `personalization-foo-service` também deve ser fornecido com permissões específicas. Se você acabar concedendo permissões em todo o conteúdo, ele não será mais específico. Refletir isso no nome ou reutilizar um usuário comum na agregação
      * Um serviço específico de recurso como `msm-xyz-service` deve ter somente permissões relacionadas ao msm. Não expanda as permissões para recursos não relacionados, como gerenciar configurações de comunidades ou usuários do Screens.

   * A tarefa precisa corresponder às permissões:

      * Um `foo-reader-service` deve ser capaz de ler apenas itens regulares. Nunca conceder permissões de gravação
      * É esperado que `foo-writer-service` execute operações de gravação. No entanto, não deve receber permissões para ler/modificar o conteúdo do controle de acesso
      * Espera-se que `foo-replicator-service` tenha `crx:replicate` concedido.

**Exemplos**

Exemplos para `configuration-reader-service`:

* O nome indica que se refere às configurações em geral e não à configuração de um recurso específico, como a configuração da integração do DM. Um usuário de serviço especificamente direcionado para a leitura da configuração dessa integração preferiria ser nomeado como `dmconfig-reader-service` ou `s7config-reader-service`

  >[!NOTE]
  >
  >Nenhuma informação de caminho está incluída na nomeação. Configurações movidas de `/etc` para `/conf`.

* O elemento tarefa indica que os serviços vinculados a esse usuário só executarão operações de leitura.

Exemplos para `userproperties-copy-service`:

* Os serviços vinculados a este usuário de serviço operarão nas propriedades do usuário/grupo, como perfis ou preferências
* Ela é direcionada especificamente para apenas copiar essas informações, ao contrário de um nome como `userproperties-writer-service`, que incluiria qualquer tipo de operação de gravação. Portanto, seria possível que a configuração de permissão dessas tarefas de cópia só permitisse adicionar itens em um local e remover itens em outro local.

**Práticas recomendadas para a instalação de permissões**

* Sempre usar a configuração do controle de acesso baseado na entidade de segurança para usuários do serviço. Para obter mais detalhes, consulte os exemplos abaixo:

   * Permitir marcar usuários do serviço e suas permissões como conteúdo de aplicativo imutável no skyline
   * Não é necessário criar caminhos e estruturas de árvore

* Conceder somente permissões, nunca negar
* Limitar permissões

   * Conceda somente o conjunto mínimo de permissões necessárias
   * Para obter mais informações, consulte a documentação [Mapeando Privilégios para Itens](https://jackrabbit.apache.org/oak/docs/security/privilege/mappingtoitems.html) e [Mapeando Chamadas de API para Privilégios](https://jackrabbit.apache.org/oak/docs/security/privilege/mappingtoprivileges.html)
   * Não conceder permissão para `jcr:all`. Esse provavelmente não é o conjunto mínimo.

* Reduzir escopo

   * Colocar políticas de controle de acesso em subárvores específicas de recursos
   * No caso de itens distribuídos: use restrições para limitar o escopo (consulte [a documentação](https://jackrabbit.apache.org/oak/docs/security/authorization/restriction.html) para obter uma lista de restrições internas).

* Garantir a consistência

   * Tornar as permissões consistentes com a entidade e a tarefa usadas no nome de usuário do serviço
   * Evite adicionar permissões não relacionadas. Por exemplo, seria estranho ter um `workflow-administration-service` e conceder a ele permissões para executar operações de gerenciamento de usuário em `/home/users/screens` ou deixá-lo ler s7-config.

* Integralidade

   * Verifique se o serviço tem todas as permissões necessárias para executar as tarefas para as quais foi projetado. Seu serviço precisa funcionar imediatamente também em ambientes do cliente.
   * Nunca espere/peça aos clientes para expandir a configuração de permissão (por exemplo, abaixo de `/apps`)

* Evitar duplicação da configuração de permissão

   * Reutilizar usuários comuns de serviços
   * Agregue-os aos usuários de serviço específicos do seu recurso que fornecem a permissão específica necessária, além disso

* Não divida a configuração de permissão em diferentes recursos. A necessidade de fazer isso indica que o usuário do serviço não está bem definido ou faz muitas coisas diferentes
* Não coloque usuários de serviço em grupos, pois:

   * Ele combina detalhes de implementação de usuários de serviço com grupos &quot;públicos&quot;
   * Você não tem controle sobre as alterações de permissão (propenso a regressões e escalonamentos de privilégio)
   * Desempenho de logon e avaliação
   * Não funciona com a configuração AC baseada em entidade

* O acesso ao nó user-home (ou qualquer subárvore contida nele), que não tem um caminho previsível, é obtido na inicialização do repositório usando home(`userId`). Consulte a [documentação](https://sling.apache.org/documentation/bundles/repository-initialization.html) da inicialização do sling repo para obter detalhes.
* RTC: crie um problema de RTC dedicado se você alterar as permissões de um usuário de serviço existente e garantir que você o analise pela equipe de segurança.

**Criação com Inicialização de Repositório**

Sempre use o `repo-init` para definir usuários de serviço e suas permissões para configurar e colocar ambos na seção correta do modelo de recurso Quickstart:

**Práticas recomendadas**

* Sempre usar `repo-init` para criar o usuário do serviço
* Sempre especificar um caminho intermediário para a criação do usuário de serviço
* Todos os usuários do serviço interno para AEM devem estar localizados abaixo de `system/cq:services/internal`
* Além disso, anexe ao caminho relativo intermediário para agrupar usuários de serviço por recurso: `system/cq:services/internal/<your-feature>`
* Os usuários do serviço definido pelo cliente devem estar localizados abaixo de `system/cq:services/<customer-intermediate-rel-path>` e nunca abaixo da árvore interna
* Use **com o caminho forçado** em vez de **com o caminho** se um usuário já existir e precisar ser movido para o novo local que dá suporte à autorização baseada em entidade de segurança.

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

A biblioteca `com.adobe.granite.testing.clients` fornece vários utilitários que facilitam a gravação de SSTs para usuários de serviço.
