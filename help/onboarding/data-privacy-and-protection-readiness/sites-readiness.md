---
title: Regulamentos de proteção de dados e privacidade de dados - a Adobe Experience Manager está pronta para o Cloud Service Sites
description: 'Saiba mais sobre a Adobe Experience Manager como um suporte de Cloud Service Sites para as várias regulamentações de proteção de dados e privacidade de dados; incluindo o Regulamento Geral da UE sobre Proteção de Dados (RGPD), a Lei da Privacidade do Consumidor da Califórnia e como cumprir ao implementar um novo AEM como um projeto Cloud Service. '
translation-type: tm+mt
source-git-commit: 7b5a427853075054d56bc7ea6569d5d839e282a1
workflow-type: tm+mt
source-wordcount: '1036'
ht-degree: 1%

---


# A Adobe Experience Manager como Cloud Service Sites Prontidão para Proteção de Dados e Regulamentos de Privacidade de Dados {#aem-sites-readiness-for-data-protection-and-data-privacy-regulations}

>[!WARNING]
>
>O conteúdo deste documento não constitui um aconselhamento jurídico e não substitui o aconselhamento jurídico.
>
>Consulte o departamento jurídico da sua empresa para obter informações sobre as regulamentações de Proteção de Dados e Privacidade de Dados.

>[!NOTE]
>
>Para obter mais informações sobre o que isso significa em relação a problemas de privacidade, consulte [Centro de Privacidade do Adobe](https://www.adobe.com/privacy.html)Adobe.

A Adobe Experience Manager como Cloud Service Sites está pronta para ajudar os clientes com suas obrigações de privacidade de dados e conformidade de proteção. Esta página orienta os clientes pelos procedimentos para lidar com essas solicitações no AEM Sites. Ela descreve a localização dos dados privados armazenados e como removê-los manualmente ou com código.

Para obter mais informações, consulte o [Centro de privacidade do Adobe](https://www.adobe.com/privacy.html).

>[!NOTE]
>
>Consulte [Adobe Experience Manager como Cloud Service para Prontidão para Proteção de Dados e Regulamentos de Privacidade de Dados](/help/onboarding/data-privacy-and-protection-readiness/aem-readiness.md) para obter mais detalhes.

## Nível de criação do AEM {#aem-author-tier}

As contas de usuário e o conteúdo UGC no servidor do autor são abordados na [AEM documentação do Foundation](/help/onboarding/data-privacy-and-protection-readiness/aem-readiness.md).

## Nível de publicação do AEM {#aem-publish-tier}

As contas de usuário usadas para autenticar visitantes no site e o conteúdo UGC no servidor de publicação são abordados na [documentação AEM Foundation](/help/onboarding/data-privacy-and-protection-readiness/aem-readiness.md).

Por padrão, os componentes da AEM Sites não armazenam dados de formulário inseridos por visitantes no servidor de publicação. É recomendável encaminhar os dados para um sistema de terceiros, ou para a Adobe Campaign, para processamento adicional.

## Inclusão/exclusão {#opt-in-opt-out}

<!--
AEM has a [cookie opt-out service](/help/sites-developing/cookie-optout.md ) that can be used for managing the opt-in/opt-out for users.
-->

A Adobe Experience Manager está sujeita a um serviço de opção de não participação de cookie usado para gerenciar a opção de participação/não participação dos usuários.

Para recusar:

1. Vá até:
   [Centro de privacidade do Adobe - Recusar](https://www.adobe.com/privacy/opt-out.html)

1. Role para baixo até **Services** - **dados de uso do serviço Experience Cloud**.

1. Selecione o link referenciado; atualmente denominado **here**.

1. Você receberá os seguintes detalhes, juntamente com as opções para opt out ou em:

   * Para excluir a agregação e a análise de dados sobre sua visita a este site, é necessário instalar um cookie no navegador. Este cookie identifica que você optou por não participar.

      Se você excluir o cookie de opção de não participação, ou se você alterar computadores ou navegadores da Web, precisará recusar novamente.

      Recusar - exclua-me da agregação e análise da sessão do visitante (instale o cookie de `amcglobal.sc.omtrdc.net` opção de não participação) - Clique aqui.

      Inclusão - Inclua-me na agregação e análise da sessão do visitante (não instale o `amcglobal.sc.omtrdc.net` cookie de opção de não participação) - Clique aqui.
   Siga as etapas acima para acessar os links reais.

   >[!NOTE]
   >
   > Há uma descrição adicional em **2. Privacidade.** dos Termos de uso [ gerais do ](https://www.adobe.com/legal/terms.html)Adobe.

## Analytics Foundation {#analytics-foundation}

A AEM Sites inclui uma integração opcional com a Analytics Foundation que usa funcionalidade no Adobe Analytics On-demand Service.

Para obter mais informações sobre como gerenciar solicitações de pessoas relacionadas ao Adobe Analytics, consulte [Adobe Analytics e Privacidade de dados](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/gdpr-view-settings.html).

## Fundação de personalização por Público alvo {#personalization-foundation-by-target}

A AEM Sites inclui uma integração opcional com a Personalization Foundation por Público alvo que usa funcionalidade no Adobe Target On-demand Service.

Para obter mais informações sobre como gerenciar solicitações de pessoas relacionadas à Adobe Target, consulte [Adobe Target - Privacy and General Data Protection Regulation](https://docs.adobe.com/content/help/en/target/using/implement-target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.html).

## ContextHub {#contexthub}

<!--
AEM provides an optional data layer with [ContextHub](/help/sites-developing/contexthub.md).
-->

AEM fornece uma camada de dados opcional com o ContextHub. Isso mantém os dados específicos do visitante no navegador, a serem usados para personalização baseada em regras.

Por padrão, esses dados de visitante não são armazenados em AEM; AEM envia regras para a camada de dados para tomar decisões de personalização no navegador.

### Implementação da aceitação/não participação {#implementing-opt-in-opt-out}

O proprietário do site precisa implementar um componente de opção de não participação de acordo com as diretrizes a seguir.

Essas diretrizes implementam o opt-in como padrão. Assim, um visitante do site deve concordar claramente, antes que quaisquer dados pessoais sejam armazenados na persistência do navegador (do lado do cliente).

* O componente de opção de não participação deve ser incluído toda vez que o componente ContextHub for incluído.
* Os termos e condições relacionados à proteção de dados e à privacidade do website devem ser exibidos no visitante do site, permitindo que eles:

   * accept
   * rejeição
   * alterar sua escolha anterior

* Se um visitante do site aceitar os termos e condições do site, o cookie de opção de não participação do ContextHub deverá ser removido:

   ```
   ContextHub.Utils.Cookie.removeItem('cq-opt-out');
   ```

* Se um visitante do site não aceitar os termos e condições do site, o cookie de opção de não participação do ContextHub deverá ser definido:

   ```
   ContextHub.Utils.Cookie.setItem('cq-opt-out', 1);
   ```

* Para verificar se o ContextHub está sendo executado no modo de não participação, a seguinte chamada deve ser feita no console do navegador:

   ```
   var isOptedOut = ContextHub.isOptedOut(true) === true;
   // if isOptedOut is true, ContextHub is running in opt-out mode
   ```

### Visualização da persistência do ContextHub {#previewing-persistence-of-contexthub}

Para que a persistência da pré-visualização seja usada pelo ContextHub, o usuário pode:

* Use o console do navegador; por exemplo:

   * Chrome:

      * Abra Ferramentas do desenvolvedor > Aplicativo > Armazenamento:

         * Armazenamento local > (site) > ContextHubPersistence
         * Armazenamento da sessão > (site) > ContextHubPersistence
         * Cookies > (site) > SessionPersistence
   * Firefox:

      * Abra Ferramentas do desenvolvedor > Armazenamento:

         * Armazenamento local > (site) > ContextHubPersistence
         * Armazenamento da sessão > (site) > ContextHubPersistence
         * Cookies > (site) > SessionPersistence
   * Safari:

      * Abrir Preferências > Avançado > Mostrar menu Revelação na barra de menus
      * Abrir Revelação > Mostrar JavaScript Console

         * Console > Armazenamento > Armazenamento local > (site) > ContextHubPersistence
         * Console > Armazenamento > Armazenamento da sessão > (site) > ContextHubPersistence
         * Console > Armazenamento > Cookies > (site) > ContextHubPersistence
   * Internet Explorer:

      * Abrir Ferramentas do Desenvolvedor > Console

         * `localStorage.getItem('ContextHubPersistence')`
         * `sessionStorage.getItem('ContextHubPersistence')`
         * `document.cookie`




* Use a API ContextHub, no console do navegador:

   * O ContextHub fornece as seguintes camadas de persistência de dados:

      * `ContextHub.Utils.Persistence.Modes.LOCAL` (default)
      * `ContextHub.Utils.Persistence.Modes.SESSION`
      * `ContextHub.Utils.Persistence.Modes.COOKIE`
      * `ContextHub.Utils.Persistence.Modes.WINDOW`

      O repositório do ContextHub define qual camada de persistência será usada, portanto, para visualização do estado atual da persistência, todas as camadas devem ser verificadas.


Por exemplo, para visualização de dados armazenados em localStorage:

Para que a persistência da pré-visualização seja usada pelo ContextHub, o usuário pode:

* Use o console do navegador:

   * Chrome - abra Ferramentas do desenvolvedor > Aplicativo > Armazenamento:

      * Armazenamento local > (site) > ContextHubPersistence
      * Armazenamento da sessão > (site) > ContextHubPersistence
      * Cookies > (site) > SessionPersistence
   * Firefox - abra Ferramentas do desenvolvedor > Armazenamento:

      * Armazenamento local > (site) > ContextHubPersistence
      * Armazenamento da sessão > (site) > ContextHubPersistence
      * Cookies > (site) > SessionPersistence


* Use a API ContextHub, no console do navegador:

   * O ContextHub fornece as seguintes camadas de persistência de dados:

      * `ContextHub.Utils.Persistence.Modes.LOCAL` (padrão)
      * `ContextHub.Utils.Persistence.Modes.SESSION`
      * `ContextHub.Utils.Persistence.Modes.COOKIE`
      * `ContextHub.Utils.Persistence.Modes.WINDOW`

      O repositório do ContextHub define qual camada de persistência será usada, portanto, para visualização do estado atual da persistência, todas as camadas devem ser verificadas.


Por exemplo, para visualização de dados armazenados em localStorage:

```
var storage = new ContextHub.Utils.Persistence({ mode: ContextHub.Utils.Persistence.Modes.LOCAL });
console.log(storage.getTree());
```

### Limpando a persistência do ContextHub {#clearing-persistence-of-contexthub}

Para limpar a persistência do ContextHub:

* Para eliminar a persistência dos armazenamentos atualmente carregados:

   ```
   // in order to be able to fully access persistence layer, Opt-Out must be turned off
   ContextHub.Utils.Cookie.removeItem('cq-opt-out');
   
   // following call asks all currently loaded stores to clear their data
   ContextHub.cleanAllStores();
   
   // following call asks all currently loaded stores to set back default values (provided in their configs)
   ContextHub.resetAllStores();
   ```

* Para limpar uma camada de persistência específica; por exemplo, sessionStorage:

   ```
   var storage = new ContextHub.Utils.Persistence({ mode: ContextHub.Utils.Persistence.Modes.SESSION });
   storage.setItem('/store', null);
   storage.setItem('/_', null);
   
   // to confirm that nothing is stored:
   console.log(storage.getTree());
   ```

* Para limpar todas as camadas de persistência do ContextHub, o código apropriado deve ser chamado para todas as camadas:

   * `ContextHub.Utils.Persistence.Modes.LOCAL` (padrão)
   * `ContextHub.Utils.Persistence.Modes.SESSION`
   * `ContextHub.Utils.Persistence.Modes.COOKIE`
   * `ContextHub.Utils.Persistence.Modes.WINDOW`
