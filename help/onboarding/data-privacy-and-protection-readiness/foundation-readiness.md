---
title: Proteção de dados e regulamentos de privacidade de dados - Adobe Experience Manager como disponibilidade para a base de Cloud Service
description: 'Saiba mais sobre o Adobe Experience Manager como um suporte da Cloud Service Foundation para as várias regulamentações de proteção de dados e privacidade de dados; incluindo o Regulamento geral da UE sobre proteção de dados (RGPD), a Lei da Privacidade do Consumidor da Califórnia e como cumprir ao implementar um novo AEM como um projeto Cloud Service. '
translation-type: tm+mt
source-git-commit: 23349f3350631f61f80b54b69104e5a19841272f
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 5%

---


# Adobe Experience Manager como uma tecnologia Cloud Service Foundation Prontidão para Proteção de Dados e Regulamentos de Privacidade de Dados {#aem-foundation-readiness-for-data-protection-and-data-privacy-regulations}

>[!WARNING]
>
>O conteúdo deste documento não constitui um aconselhamento jurídico e não substitui o aconselhamento jurídico.
>
>Consulte o departamento jurídico da sua empresa para obter informações sobre as regulamentações de Proteção de Dados e Privacidade de Dados.

>[!NOTE]
>
>Para obter mais informações sobre a resposta da Adobe a problemas de privacidade e o que isso significa para você como cliente da Adobe, consulte o Centro [de privacidade da](https://www.adobe.com/privacy.html)Adobe.

## Suporte para proteção e privacidade de dados do AEM Foundation {#aem-foundation-data-privacy-and-protection-support}

No nível do AEM Foundation, os Dados pessoais armazenados são mantidos no Perfil Usuário. Portanto, as informações neste artigo tratam principalmente de como acessar e excluir perfis de usuários, para atender às solicitações de acesso e exclusão, respectivamente.

## Acessar um Perfil de usuário {#accessing-a-user-profile}

### Etapas manuais {#manual-steps}

1. Abra o console Administração do usuário, navegando até **[!UICONTROL Ferramentas - Segurança - Usuários]** ou navegando diretamente para `https://<serveraddress>:<serverport>/security/users.html`

<!--
   ![useradmin2](assets/useradmin2.png)
-->

1. Em seguida, procure o usuário em questão digitando o nome na barra de pesquisa na parte superior da página:

   ![procurar conta](assets/dpp-foundation-01.png)

1. Por fim, abra o perfil do usuário clicando nele e, em seguida, marque na guia **[!UICONTROL Detalhes]** .

   ![perfil do usuário](assets/dpp-foundation-02.png)

### API HTTP {#http-api}

Conforme mencionado, a Adobe fornece APIs para acessar dados do usuário, a fim de facilitar a automação. Existem vários tipos de APIs que você pode usar:

**API UserProperties**

```shell
curl -u user:password http://localhost:4502/libs/granite/security/search/profile.userproperties.json\?authId\=cavery
```

**API Sling**

**Descobrindo a página inicial do usuário:**

```xml
curl -g -u user:password 'http://localhost:4502/libs/granite/security/search/authorizables.json?query={"condition":[{"named":"cavery"}]}'
     {"authorizables":[{"type":"user","authorizableId_xss":"cavery","authorizableId":"cavery","name_xss":"Carlene Avery","name":"Carlene Avery","home":"/home/users/we-retail/DSCP-athB1NYLBXvdTuN"}],"total":1}
```

**Recuperando dados do usuário:**

Usando o caminho do nó da propriedade home da carga JSON retornada do comando acima:

```shell
curl -u user:password  'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN/profile.-1.json'
```

```shell
curl -u user:password  'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN/profiles.-1.json'
```

## Desabilitar um usuário e Excluir os Perfis associados {#disabling-a-user-and-deleting-the-associated-profiles}

### Desativar usuário {#disable-user}

1. Abra o console Administração do usuário e procure o usuário em questão, conforme descrito acima.
2. Passe o mouse sobre o usuário e clique no ícone de seleção. O perfil ficará cinza, indicando que está selecionado.

3. Pressione o botão **Desativar** no menu superior para desativar o usuário:

   ![desativar conta](assets/dpp-foundation-03.png)

4. Por último, confirme a ação.

   A interface do usuário indicará que a conta de usuário foi desativada ao ficar acinzentada e adicionar um bloqueio à placa de perfil:

   ![conta desativada](assets/dpp-foundation-04.png)

### Excluir informações do Perfil do usuário {#delete-user-profile-information}

>[!NOTE]
>
>Para o AEM como Cloud Service, não há nenhum procedimento manual disponível na interface do usuário para a exclusão de um perfil do usuário, pois o CRXDE não está acessível.

### API HTTP {#http-api-1}

Os procedimentos a seguir usam a ferramenta de linha de comando `curl` para ilustrar como desativar o usuário com a **[!UICONTROL cavery]** `userId` e excluir seus perfis disponíveis no local padrão.

**Descobrindo a página inicial do usuário:**

```shell
curl -g -u user:password 'http://localhost:4502/libs/granite/security/search/authorizables.json?query={"condition":[{"named":"cavery"}]}'
     {"authorizables":[{"type":"user","authorizableId_xss":"cavery","authorizableId":"cavery","name_xss":"Carlene Avery","name":"Carlene Avery","home":"/home/users/we-retail/DSCP-athB1NYLBXvdTuN"}],"total":1}
```

**Desabilitando o usuário:**

Usando o caminho do nó da propriedade home da carga JSON retornada do comando acima:

```shell
curl -X POST -u user:password -FdisableUser="describe the reasons for disabling this user (Data Privacy in this case)" 'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN.rw.userprops.html'
```

**Excluindo perfis de usuário**

Usando o caminho do nó da propriedade home da carga JSON retornada do comando descoberta de conta e os locais conhecidos do nó do perfil out da caixa:

```shell
curl -X POST -u user:password -H "Accept: application/json,**/**;q=0.9" -d ':operation=delete' 'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN/profile'
```

```shell
curl -X POST -u user:password -H "Accept: application/json,**/**;q=0.9" -d ':operation=delete' 'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN/profile'
```
