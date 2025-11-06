---
title: Regulamentos de proteção e privacidade de dados - Disponibilidade do AEM Sites
description: Saiba mais sobre o suporte do Experience Manager as a Cloud Service Sites a vários Regulamentos de Proteção e Privacidade de Dados, incluindo o Regulamento Geral sobre a Proteção de Dados da UE (GDPR), a Lei de Privacidade do Consumidor da Califórnia, e como estar em conformidade ao implementar um novo projeto do AEM as a Cloud Service.
exl-id: fdcad111-0cdd-46cc-964c-3f8669ca2030
feature: Compliance
role: Admin, Developer, Leader
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '989'
ht-degree: 90%

---

# Regulamentos de disponibilidade da Experience Manager Sites para proteção e privacidade de dados {#aem-sites-readiness-for-data-protection-and-data-privacy-regulations}

>[!WARNING]
>
>O conteúdo deste documento não constitui um aconselhamento jurídico e não se destina a substituir tal aconselhamento.
>
>Consulte o departamento jurídico da sua empresa para obter aconselhamento sobre os regulamentos de proteção e privacidade de dados.

>[!NOTE]
>
>Para obter mais informações sobre a resposta da Adobe a questões de privacidade, e o que isso significa para você como cliente da Adobe, consulte o [Centro de privacidade da Adobe](https://www.adobe.com/br/privacy.html).

O Adobe Experience Manager as a Cloud Service Sites está pronto para ajudar os clientes em suas obrigações de conformidade com a proteção e privacidade de dados. Esta página orienta os clientes por meio de procedimentos para lidar com essas solicitações no AEM Sites. Ele descreve a localização dos dados privados armazenados e como removê-los manualmente ou com um código.

Para obter mais informações, consulte o [Centro de privacidade da Adobe](https://www.adobe.com/br/privacy.html).

>[!NOTE]
>
>Consulte [Disponibilidade do Adobe Experience Manager as a Cloud Service para Regulamentos de proteção e privacidade de dados](/help/compliance/data-privacy-and-protection-readiness/aem-readiness.md) para mais detalhes.

## Nível de criação do AEM {#aem-author-tier}

As contas de usuário e o conteúdo UGC no servidor do autor são abordados na seção [Documentação do AEM Foundation](/help/compliance/data-privacy-and-protection-readiness/foundation-readiness.md).

## Nível de publicação do AEM {#aem-publish-tier}

As contas de usuário usadas para autenticar visitantes no site e o conteúdo UGC no servidor de publicação são abordados na [Documentação do AEM Foundation](/help/compliance/data-privacy-and-protection-readiness/aem-readiness.md).

Por padrão, os componentes dos AEM Sites não armazenam dados de formulário inseridos por visitantes no servidor de publicação. É recomendado encaminhar os dados para um sistema de terceiros ou para o Adobe Campaign para processamento adicional.

## Aceitar/Recusar {#opt-in-opt-out}

<!--
AEM has a [cookie opt-out service](/help/sites-developing/cookie-optout.md ) that can be used for managing the opt-in/opt-out for users.
-->

A Adobe Experience Manager está sujeito a um serviço de cookie de recusa para gerenciar a aceitação/recusa dos usuários.

Para recusar:

1. Vá até:
   [Central de privacidade da Adobe - Recusa](https://www.adobe.com/br/privacy/opt-out.html)

1. Role para baixo até **Serviços** - **Dados de uso de serviço da Experience Cloud**.

1. Selecione o link referenciado; atualmente denominado **aqui**.

1. Os detalhes a seguir são apresentados a você, juntamente com as opções de recusa ou aceitação:

   * Para recusar a agregação e a análise de dados sobre sua visita a este site, é necessário instalar um cookie em seu navegador. Este cookie identifica que você optou por não participar.

     Se você excluir o cookie de opção de recusa, ou se alterar os computadores ou navegadores da Web, será necessário recusar novamente.

     Recusar - Exclua-me da agregação e análise da sessão de visitante (instalar o `amcglobal.sc.omtrdc.net` cookie de opção) - Clique aqui.

     Aceitar - Inclua-me na agregação e análise da sessão do visitante (não instale o cookie `amcglobal.sc.omtrdc.net` de opção de recusa) - Clique aqui.

   Siga as etapas acima para acessar os links reais.

   >[!NOTE]
   >
   > Há uma descrição adicional no **2. Privacidade.seção** dos [Termos gerais de uso da Adobe](https://www.adobe.com/br/legal/terms.html).

## Analytics Foundation {#analytics-foundation}

O AEM Sites inclui uma integração opcional com o Analytics Foundation, que usa a funcionalidade no Adobe Analytics On-demand Service.

Para obter mais informações sobre como gerenciar solicitações de titulares de dados relacionadas ao Adobe Analytics, consulte [Adobe Analytics e privacidade de dados](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/gdpr-view-settings.html?lang=pt-BR).

## Personalization Foundation by Target {#personalization-foundation-by-target}

O AEM Sites inclui uma integração opcional com a Personalization Foundation by Target que usa a funcionalidade no Adobe Target On-Demand Service.

Para obter mais informações sobre como gerenciar solicitações de titulares de dados relacionadas ao Adobe Target, consulte [Adobe Target - Privacidade e Regulamento Geral sobre a Proteção de Dados](https://experienceleague.adobe.com/docs/target-dev/developer/implementation/privacy/cmp-privacy-and-general-data-protection-regulation.html).

## ContextHub {#contexthub}

<!--
AEM provides an optional data layer with [ContextHub](/help/sites-developing/contexthub.md).
-->

O AEM fornece uma camada de dados opcional com o ContextHub. Isto mantém os dados específicos do visitante no navegador, para serem usados para personalização baseada em regras.

Por padrão, esses dados do visitante não são armazenados no AEM; o AEM envia as regras para a camada de dados para tomar decisões de personalização no navegador.

### Implementação do Opt-in/Opt-out (Aceitar/Recusar) {#implementing-opt-in-opt-out}

O proprietário do site deve implementar um componente de opção de não participação, de acordo com as diretrizes a seguir.

Essas diretrizes implementam a opção de aceitação como padrão. Assim, um visitante do site deve concordar claramente, antes que quaisquer dados pessoais sejam armazenados na persistência do navegador (lado do cliente).

* O componente de opt out (recusar) deve ser incluído sempre que o componente ContextHub for incluído.
* Os termos e condições relacionados à proteção de dados e à privacidade do site devem ser exibidos para o visitante do site, para que eles possam:

   * Aceitar
   * Rejeitar
   * alterar a opção anterior

* Se um visitante aceitar os termos e condições do site, o cookie de opção de recusa do ContextHub deverá ser removido:

  ```
  ContextHub.Utils.Cookie.removeItem('cq-opt-out');
  ```

* Se um visitante não aceitar os termos e condições do site, o cookie de opção de recusa do ContextHub deverá ser definido:

  ```
  ContextHub.Utils.Cookie.setItem('cq-opt-out', 1);
  ```

* Para verificar se o ContextHub está sendo executado no modo de recusa, a seguinte chamada deve ser feita no console do navegador:

  ```
  var isOptedOut = ContextHub.isOptedOut(true) === true;
  // if isOptedOut is true, ContextHub is running in opt-out mode
  ```

### Visualização da persistência do ContextHub {#previewing-persistence-of-contexthub}

Para visualizar a persistência usada pelo ContextHub, um usuário pode:

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

      * Abra Preferências > Avançado > Mostrar menu Desenvolvedor na barra de menus
      * Abra Desenvolver > Mostrar console do JavaScript

         * Console > Armazenamento > Armazenamento local > (site) > ContextHubPersistence
         * Console > Armazenamento > Armazenamento de sessão > (site) > ContextHubPersistence
         * Console > Armazenamento > Cookies > (site) > ContextHubPersistence

   * Internet Explorer:

      * Abra Ferramentas do desenvolvedor > Console

         * `localStorage.getItem('ContextHubPersistence')`
         * `sessionStorage.getItem('ContextHubPersistence')`
         * `document.cookie`

* Use a API do ContextHub no console do navegador:

   * O ContextHub fornece as seguintes camadas de persistência de dados:

      * `ContextHub.Utils.Persistence.Modes.LOCAL` (default)
      * `ContextHub.Utils.Persistence.Modes.SESSION`
      * `ContextHub.Utils.Persistence.Modes.COOKIE`
      * `ContextHub.Utils.Persistence.Modes.WINDOW`

     O armazenamento do ContextHub define qual camada de persistência será usada, portanto, para exibir o estado atual da persistência, todas as camadas devem ser verificadas.

Por exemplo, para exibir dados armazenados em localStorage:

Para visualizar a persistência usada pelo ContextHub, um usuário pode:

* Use o console do navegador:

   * Chrome - abra Ferramentas do desenvolvedor > Aplicativo > Armazenamento:

      * Armazenamento local > (site) > ContextHubPersistence
      * Armazenamento de sessão > (site) > ContextHubPersistence
      * Cookies > (site) > SessionPersistence

   * Firefox - abra Ferramentas do desenvolvedor > Armazenamento:

      * Armazenamento local > (site) > ContextHubPersistence
      * Armazenamento de sessão > (site) > ContextHubPersistence
      * Cookies > (site) > SessionPersistence

* Use a API do ContextHub no console do navegador:

   * O ContextHub fornece as seguintes camadas de persistência de dados:

      * `ContextHub.Utils.Persistence.Modes.LOCAL` (default)
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

* Para eliminar a persistência de armazenamentos carregados no momento:

  ```
  // to be able to fully access persistence layer, Opt-Out must be turned off
  ContextHub.Utils.Cookie.removeItem('cq-opt-out');
  
  // following call asks all currently loaded stores to clear their data
  ContextHub.cleanAllStores();
  
  // following call asks all currently loaded stores to set back default values (provided in their configs)
  ContextHub.resetAllStores();
  ```

* Para eliminar uma camada de persistência específica; por exemplo, sessionStorage:

  ```
  var storage = new ContextHub.Utils.Persistence({ mode: ContextHub.Utils.Persistence.Modes.SESSION });
  storage.setItem('/store', null);
  storage.setItem('/_', null);
  
  // to confirm that nothing is stored:
  console.log(storage.getTree());
  ```

* Para eliminar todas as camadas de persistência do ContextHub, o código apropriado deve ser chamado para todas as camadas:

   * `ContextHub.Utils.Persistence.Modes.LOCAL` (default)
   * `ContextHub.Utils.Persistence.Modes.SESSION`
   * `ContextHub.Utils.Persistence.Modes.COOKIE`
   * `ContextHub.Utils.Persistence.Modes.WINDOW`
