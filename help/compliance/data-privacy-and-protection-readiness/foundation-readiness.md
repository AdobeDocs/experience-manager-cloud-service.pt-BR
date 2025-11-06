---
title: Regulamentos de proteção e privacidade de dados - Disponibilidade do Adobe Experience Manager as a Cloud Service Foundation
description: Saiba mais sobre o suporte do Adobe Experience Manager as a Cloud Service Foundation a vários regulamentos de proteção e privacidade de dados. Este artigo inclui o Regulamento Geral sobre a Proteção de Dados da UE (RGPD), a Lei de Privacidade do Consumidor da Califórnia, e como estar em conformidade ao implementar um novo projeto do AEM as a Cloud Service.
exl-id: 3a4b9d00-297d-4b1d-ae57-e75fbd5c490c
feature: Compliance
role: Admin, Developer, Leader
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 100%

---

# Disponibilidade do Adobe Experience Manager as a Cloud Service Foundation para Regulamentos de proteção e privacidade de dados {#aem-foundation-readiness-for-data-protection-and-data-privacy-regulations}

>[!WARNING]
>
>O conteúdo deste documento não constitui um aconselhamento jurídico e não se destina a substituir tal aconselhamento.
>
>Consulte o departamento jurídico da sua empresa para obter aconselhamento sobre os regulamentos de proteção e privacidade de dados.

>[!NOTE]
>
>Para obter mais informações sobre a resposta da Adobe a questões de privacidade, e o que isso significa para você como cliente da Adobe, consulte o [Centro de privacidade da Adobe](https://www.adobe.com/br/privacy.html).

## Suporte do AEM Foundation à Proteção e privacidade de dados {#aem-foundation-data-privacy-and-protection-support}

No nível AEM Foundation, os dados pessoais armazenados são mantidos no perfil de usuário. Portanto, as informações neste artigo abordam principalmente como acessar e excluir perfis de usuário, atendendo às solicitações de acesso e exclusão respectivamente.

## Acessar um perfil de usuário {#accessing-a-user-profile}

### Etapas manuais {#manual-steps}

1. Abra o console Administração do usuário, navegando até **[!UICONTROL Ferramentas - Segurança - Usuários]** ou navegando diretamente até `https://<serveraddress>:<serverport>/security/users.html`

<!--
   ![useradmin2](assets/useradmin2.png)
-->

1. Em seguida, pesquise pelo usuário em questão digitando o nome na barra de pesquisa na parte superior da página:

   ![pesquisar pela conta](assets/dpp-foundation-01.png)

1. Por fim, clique para abrir o perfil do usuário, e verifique na guia **[!UICONTROL Detalhes]**.

   ![perfil do usuário](assets/dpp-foundation-02.png)

### API HTTP {#http-api}

Como mencionado, a Adobe fornece APIs para acessar dados do usuário, a fim de facilitar a automação. Há vários tipos de APIs que você pode usar:

**API UserProperties**

```shell
curl -u user:password http://localhost:4502/libs/granite/security/search/profile.userproperties.json\?authId\=cavery
```

**API Sling**

**Descobrir a página inicial do usuário:**

```xml
curl -g -u user:password 'http://localhost:4502/libs/granite/security/search/authorizables.json?query={"condition":[{"named":"cavery"}]}'
     {"authorizables":[{"type":"user","authorizableId_xss":"cavery","authorizableId":"cavery","name_xss":"Carlene Avery","name":"Carlene Avery","home":"/home/users/we-retail/DSCP-athB1NYLBXvdTuN"}],"total":1}
```

**Recuperar dados do usuário:**

Usando o caminho do nó da propriedade home da carga JSON retornada do comando acima:

```shell
curl -u user:password  'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN/profile.-1.json'
```

```shell
curl -u user:password  'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN/profiles.-1.json'
```

## Desativar um usuário e excluir os perfis associados {#disabling-a-user-and-deleting-the-associated-profiles}

### Desativar usuário {#disable-user}

1. Abra o console Administração do usuário e procure o usuário em questão, conforme descrito acima.
2. Passe o mouse sobre o usuário e clique no ícone de seleção. O perfil fica cinza, indicando que está selecionado.

3. No menu superior, clique em **Desabilitar** para desabilitar (desativar) o usuário:

   ![desativar conta](assets/dpp-foundation-03.png)

4. Por último, confirme a ação.

   A interface indicará que a conta do usuário foi desativada acinzentando e adicionando um cadeado ao cartão de perfil:

   ![conta desabilitada](assets/dpp-foundation-04.png)

### Excluir informações do perfil do usuário {#delete-user-profile-information}

>[!NOTE]
>
>Para o AEM as a Cloud Service, não há nenhum procedimento manual disponível na interface para a exclusão de um perfil de usuário, pois o CRXDE não está acessível.

### API HTTP {#http-api-1}

Os procedimentos a seguir usam a ferramenta de linha de comando `curl` para ilustrar como desabilitar o usuário com o **[!UICONTROL cavery]** `userId`e excluir seus perfis disponíveis no local padrão.

**Descobrir a página inicial do usuário:**

```shell
curl -g -u user:password 'http://localhost:4502/libs/granite/security/search/authorizables.json?query={"condition":[{"named":"cavery"}]}'
     {"authorizables":[{"type":"user","authorizableId_xss":"cavery","authorizableId":"cavery","name_xss":"Carlene Avery","name":"Carlene Avery","home":"/home/users/we-retail/DSCP-athB1NYLBXvdTuN"}],"total":1}
```

**Desabilitar o usuário:**

Usando o caminho do nó da propriedade home da carga JSON retornada do comando acima:

```shell
curl -X POST -u user:password -FdisableUser="describe the reasons for disabling this user (Data Privacy in this case)" 'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN.rw.userprops.html'
```

**Exclusão de perfis de usuário**

Usando o caminho do nó da propriedade página inicial do conteúdo JSON retornada a partir do comando de descoberta de conta e os locais de nós de perfil conhecidos e prontos para uso:

```shell
curl -X POST -u user:password -H "Accept: application/json,**/**;q=0.9" -d ':operation=delete' 'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN/profile'
```

```shell
curl -X POST -u user:password -H "Accept: application/json,**/**;q=0.9" -d ':operation=delete' 'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN/profile'
```
