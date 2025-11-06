---
title: Diagnósticos do ContextHub
description: O ContextHub fornece uma página de diagnóstico onde você pode ter uma visão geral da estrutura do ContextHub
exl-id: c8d4e160-ea02-49f3-9e31-119445ef5a68
feature: Developing, Personalization
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 1%

---

# Diagnósticos do ContextHub {#contexthub-diagnostics}

O ContextHub fornece uma página de diagnósticos na qual você pode ter uma visão geral da estrutura do ContextHub. Para abrir a página, vá para a página `contexthub.diagnostics.html` da instância do autor do AEM, por exemplo:

`http://<host>:<port>/conf/<site>/settings/cloudsettings/default/contexthub.diagnostics.html`

A página Diagnóstico do ContextHub fornece informações sobre os armazenamentos e módulos de interface do usuário criados, as pastas da biblioteca do cliente carregadas e os links para páginas úteis.

>[!NOTE]
>
>Para que as informações de diagnóstico sejam retornadas, o modo de depuração deve estar ativado, caso contrário, a página de diagnósticos estará em branco. Consulte [este documento](configuring-contexthub.md#debugging-contexthub) para obter detalhes sobre como habilitar o modo de depuração.

## Lojas {#stores}

A seção Lojas lista todos os armazenamentos do ContextHub que foram configurados. Cada item na lista consiste nas seguintes informações:

* **Título:** O [tipo de armazenamento](sample-stores.md) no qual o armazenamento se baseia.
* **caminho:** O caminho para o nó do repositório que contém a configuração.
* **resourceType:** o caminho do nó de repositório onde o tipo de repositório está definido.
* **clientlibs:** as categorias das bibliotecas de clientes carregadas que implementam o tipo de armazenamento.

## Módulos {#modules}

A seção Módulos lista todos os módulos de interface do usuário do ContextHub que foram configurados. Cada item na lista consiste nas seguintes informações:

* **Título:** O [tipo de Módulo de Interface do Usuário](sample-modules.md) no qual o módulo de interface do usuário se baseia.
* **caminho:** O caminho para o nó do repositório que contém a configuração.
* **resourceType:** o caminho do nó do repositório onde o tipo de módulo da interface do usuário é definido.
* **clientlibs:** as categorias das bibliotecas de clientes carregadas que implementam o tipo de módulo da interface do usuário.

## Clientlibs {#clientlibs}

A seção Clientlibs lista todas as t[pastas da biblioteca do cliente](/help/implementing/developing/introduction/clientlibs.md) carregadas pelo ContextHub. As bibliotecas de clientes são categorizadas da seguinte maneira:

* **kernel.js:** Bibliotecas de clientes que implementam a estrutura do ContextHub, o mecanismo de segmento e os tipos de armazenamento.
* **ui.js:** bibliotecas de clientes que implementam os tipos de módulo de interface e interface do usuário do ContextHub.
* **style.css:** arquivos CSS que são carregados das bibliotecas do cliente.

## URLs {#urls}

A seção URLs contém links para recursos do ContextHub:

* **Editor de configuração:** abre a [página Configuração do ContextHub](configuring-contexthub.md), onde você pode configurar lojas, modos de interface do usuário e módulos de interface do usuário.
* **Configuração dos módulos do ContextHub:** Abre o arquivo `/etc/cloudsettings/default/contexthub.config.kernel.js`, que contém a representação do objeto JavaScript das configurações de armazenamento do ContextHub.
* **Configuração da interface do usuário do ContextHub:** Abre o arquivo `/etc/cloudsettings/default/contexthub.config.ui.js`, que contém a representação do objeto JavaScript das configurações de modo da interface do usuário do ContextHub.
* **kernel.js:** abre o arquivo `/etc/cloudsettings/default/contexthub.kernel.js`, que contém o código-fonte das bibliotecas de clientes que implementam a estrutura do ContextHub, o mecanismo de segmento e os tipos de armazenamento.
* **ui.js:** abre o arquivo `/etc/cloudsettings/default/contexthub.ui.js`, que contém o código-fonte das bibliotecas de clientes que implementam os tipos de módulo da interface do usuário e da interface do usuário do ContextHub.
* **style.css:** Abre o arquivo `/etc/cloudsettings/default/contexthub.styles.css`, que contém os estilos CSS dos módulos de interface do usuário e da interface do ContextHub.
