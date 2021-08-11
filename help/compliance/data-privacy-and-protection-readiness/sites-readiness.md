---
title: Regulamentos de proteção e privacidade de dados - Disponibilidade do Adobe Experience Manager as a Cloud Service Sites
description: Saiba mais sobre o suporte do Adobe Experience Manager as a Cloud Service Sites para as várias regulamentações de proteção e privacidade de dados; incluindo o Regulamento Geral sobre a Proteção de Dados da UE (GDPR), a Lei de Privacidade do Consumidor da Califórnia e como fazer isso ao implementar um novo AEM como um projeto do Cloud Service.
exl-id: fdcad111-0cdd-46cc-964c-3f8669ca2030
source-git-commit: e9c1ec6807f86ab00f89ef292a89a0c8efdf802b
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Regulamentos de disponibilidade dos sites do Adobe Experience Manager as a Cloud Service para proteção e privacidade de dados {#aem-sites-readiness-for-data-protection-and-data-privacy-regulations}

>[!WARNING]
>
>O conteúdo deste documento não constitui um aconselhamento jurídico e não se destina a substituir tal aconselhamento.
>
>Consulte o departamento jurídico da sua empresa para obter aconselhamento sobre as regras de proteção e privacidade de dados.

>[!NOTE]
>
>Para obter mais informações sobre resposta do Adobe a problemas de privacidade e o que isso significa para você como cliente de Adobe, consulte [Central de Privacidade do Adobe](https://www.adobe.com/privacy.html).

O Adobe Experience Manager as a Cloud Service Sites está pronto para ajudar os clientes com suas obrigações de conformidade com a privacidade de dados e a proteção. Esta página orienta os clientes pelos procedimentos para lidar com essas solicitações no AEM Sites. Ele descreve a localização dos dados privados armazenados e como removê-los manualmente ou com código.

Para obter mais informações, consulte o [Centro de privacidade do Adobe](https://www.adobe.com/privacy.html).

>[!NOTE]
>
>Consulte [Adobe Experience Manager as a Cloud Service Readiness for Data Protection and Data Privacy Regulations](/help/compliance/data-privacy-and-protection-readiness/aem-readiness.md) para obter mais detalhes.

## Nível de criação do AEM {#aem-author-tier}

As contas de usuário e o conteúdo UGC no servidor do autor são abordados na [AEM documentação do Foundation](/help/compliance/data-privacy-and-protection-readiness/foundation-readiness.md).

## Nível de publicação do AEM {#aem-publish-tier}

As contas de usuário usadas para autenticar visitantes no site e o conteúdo UGC no servidor de publicação são abordados na [AEM documentação do Foundation](/help/compliance/data-privacy-and-protection-readiness/aem-readiness.md).

Por padrão, os componentes do AEM Sites não armazenam dados de formulário inseridos por visitantes no servidor de publicação. É recomendável encaminhar os dados para um sistema de terceiros ou para o Adobe Campaign para processamento adicional.

## Aceitação/Rejeição {#opt-in-opt-out}

<!--
AEM has a [cookie opt-out service](/help/sites-developing/cookie-optout.md ) that can be used for managing the opt-in/opt-out for users.
-->

A Adobe Experience Manager está sujeita a um serviço de opção de não participação de cookies usado para gerenciar a aceitação/não participação dos usuários.

Para recusar:

1. Vá até:
   [Central de privacidade do Adobe - Recusar](https://www.adobe.com/privacy/opt-out.html)

1. Role para baixo até **Services** - **Dados de uso do serviço Experience Cloud**.

1. Selecione o link referenciado; atualmente denominado **aqui**.

1. Os detalhes a seguir serão apresentados a você, juntamente com as opções de recusa ou aceitação:

   * Para recusar a agregação e a análise de dados sobre sua visita a este site, é necessário instalar um cookie em seu navegador. Este cookie identifica que você optou por não participar.

      Se você excluir o cookie de opção, ou se você alterar computadores ou navegadores da Web, será necessário rejeitar novamente.

      Recusar - Excluir-me da agregação e análise da sessão de visitante (instale o `amcglobal.sc.omtrdc.net` cookie de opção) - Clique aqui.

      Opt-in - Inclua-me na agregação e análise da sessão de visitante (não instale o `amcglobal.sc.omtrdc.net` cookie de opção) - Clique aqui.
   Siga as etapas acima para acessar os links reais.

   >[!NOTE]
   >
   > Há uma descrição adicional no **2. Privacidade.** da seção Termos de uso do  [Adobe General](https://www.adobe.com/br/legal/terms.html).

## Base do Analytics {#analytics-foundation}

O AEM Sites inclui uma integração opcional com a Analytics Foundation que usa funcionalidade no Adobe Analytics On-Demand Service.

Para obter mais informações sobre como gerenciar solicitações de titulares de dados relacionadas ao Adobe Analytics, consulte [Adobe Analytics e Privacidade de dados](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/gdpr-view-settings.html).

## Base de personalização por Target {#personalization-foundation-by-target}

O AEM Sites inclui uma integração opcional com a Fundação de personalização por Target que usa funcionalidade no Adobe Target On-Demand Service.

Para obter mais informações sobre como gerenciar solicitações de titulares de dados relacionadas ao Adobe Target, consulte [Adobe Target - Privacidade e Regulamento Geral sobre a Proteção de Dados](https://experienceleague.adobe.com/docs/target/using/implement-target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.html).

## ContextHub {#contexthub}

<!--
AEM provides an optional data layer with [ContextHub](/help/sites-developing/contexthub.md).
-->

O AEM fornece uma camada de dados opcional com o ContextHub. Isso mantém os dados específicos do visitante no navegador, a serem usados para personalização baseada em regras.

Por padrão, esses dados do visitante não são armazenados no AEM; AEM envia regras para a camada de dados para tomar decisões de personalização no navegador.

### Implementação do Opt-in/Opt-out {#implementing-opt-in-opt-out}

O proprietário do site precisa implementar um componente de opção de não participação, de acordo com as diretrizes a seguir.

Essas diretrizes implementam o opt-in como padrão. Assim, um visitante do site deve concordar claramente, antes que quaisquer dados pessoais sejam armazenados na persistência do navegador (lado do cliente).

* O componente de opt out deve ser incluído sempre que o componente ContextHub for incluído.
* Os termos e condições relacionados à proteção de dados e à privacidade do site devem ser exibidos para o visitante do site, permitindo que:

   * accept
   * rejeitar
   * alterar a opção anterior

* Se um visitante do site aceitar os termos e condições do site, o cookie de opção de não participação do ContextHub deverá ser removido:

   ```
   ContextHub.Utils.Cookie.removeItem('cq-opt-out');
   ```

* Se um visitante do site não aceitar os termos e condições do site, o cookie de opção do ContextHub deve ser definido:

   ```
   ContextHub.Utils.Cookie.setItem('cq-opt-out', 1);
   ```

* Para verificar se o ContextHub está sendo executado no modo de não participação, a seguinte chamada deve ser feita no console do navegador:

   ```
   var isOptedOut = ContextHub.isOptedOut(true) === true;
   // if isOptedOut is true, ContextHub is running in opt-out mode
   ```

### Visualização da persistência do ContextHub {#previewing-persistence-of-contexthub}

Para visualizar a persistência usada pelo ContextHub, o usuário pode:

* Use o console do navegador; por exemplo:

   * Chrome:

      * Abra Ferramentas do desenvolvedor > Aplicativo > Armazenamento:

         * Armazenamento local > (site) > ContextHubPersistence
         * Armazenamento de sessão > (site) > ContextHubPersistence
         * Cookies > (site) > SessionPersistence
   * Firefox:

      * Abra Ferramentas do desenvolvedor > Armazenamento:

         * Armazenamento local > (site) > ContextHubPersistence
         * Armazenamento de sessão > (site) > ContextHubPersistence
         * Cookies > (site) > SessionPersistence
   * Safari:

      * Abra Preferências > Avançado > Mostrar menu desenvolver na barra de menus
      * Abra Desenvolver > Mostrar console do JavaScript

         * Console > Armazenamento > Armazenamento local > (site) > ContextHubPersistence
         * Console > Armazenamento > Armazenamento de sessão > (site) > ContextHubPersistence
         * Console > Armazenamento > Cookies > (site) > ContextHubPersistence
   * Internet Explorer:

      * Abra Ferramentas do desenvolvedor > Console

         * `localStorage.getItem('ContextHubPersistence')`
         * `sessionStorage.getItem('ContextHubPersistence')`
         * `document.cookie`




* Use a API do ContextHub, no console do navegador:

   * O ContextHub fornece as seguintes camadas de persistência de dados:

      * `ContextHub.Utils.Persistence.Modes.LOCAL` (default)
      * `ContextHub.Utils.Persistence.Modes.SESSION`
      * `ContextHub.Utils.Persistence.Modes.COOKIE`
      * `ContextHub.Utils.Persistence.Modes.WINDOW`

      O armazenamento do ContextHub define qual camada de persistência será usada, portanto, para exibir o estado atual da persistência, todas as camadas devem ser verificadas.


Por exemplo, para exibir dados armazenados em localStorage:

Para visualizar a persistência usada pelo ContextHub, o usuário pode:

* Use o console do navegador:

   * Chrome - abra Ferramentas do desenvolvedor > Aplicativo > Armazenamento:

      * Armazenamento local > (site) > ContextHubPersistence
      * Armazenamento de sessão > (site) > ContextHubPersistence
      * Cookies > (site) > SessionPersistence
   * Firefox - abra Ferramentas do desenvolvedor > Armazenamento:

      * Armazenamento local > (site) > ContextHubPersistence
      * Armazenamento de sessão > (site) > ContextHubPersistence
      * Cookies > (site) > SessionPersistence


* Use a API do ContextHub, no console do navegador:

   * O ContextHub fornece as seguintes camadas de persistência de dados:

      * `ContextHub.Utils.Persistence.Modes.LOCAL` (padrão)
      * `ContextHub.Utils.Persistence.Modes.SESSION`
      * `ContextHub.Utils.Persistence.Modes.COOKIE`
      * `ContextHub.Utils.Persistence.Modes.WINDOW`

      O armazenamento do ContextHub define qual camada de persistência será usada, portanto, para exibir o estado atual da persistência, todas as camadas devem ser verificadas.


Por exemplo, para exibir dados armazenados em localStorage:

```
var storage = new ContextHub.Utils.Persistence({ mode: ContextHub.Utils.Persistence.Modes.LOCAL });
console.log(storage.getTree());
```

### Limpando a persistência do ContextHub {#clearing-persistence-of-contexthub}

Para limpar a persistência do ContextHub:

* Para limpar a persistência de armazenamentos carregados no momento:

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
