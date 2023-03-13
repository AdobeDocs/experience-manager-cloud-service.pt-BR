---
title: Diagnósticos do ContextHub
description: O ContextHub fornece uma página de diagnóstico onde você pode ter uma visão geral da estrutura do ContextHub
exl-id: c8d4e160-ea02-49f3-9e31-119445ef5a68
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 1%

---

# Diagnósticos do ContextHub {#contexthub-diagnostics}

O ContextHub fornece uma página de diagnósticos na qual você pode ter uma visão geral da estrutura do ContextHub. Para abrir a página, vá para a `contexthub.diagnostics.html` página da instância do autor do AEM, por exemplo:

`http://<host>:<port>/conf/<site>/settings/cloudsettings/default/contexthub.diagnostics.html`

A página Diagnóstico do ContextHub fornece informações sobre os armazenamentos e módulos de interface do usuário criados, as pastas da biblioteca do cliente carregadas e os links para páginas úteis.

>[!NOTE]
>
>Para que as informações de diagnóstico sejam retornadas, o modo de depuração deve estar ativado; caso contrário, a página de diagnósticos ficará em branco. Consulte [este documento](configuring-contexthub.md#debugging-contexthub) para obter detalhes sobre como ativar o modo de depuração.

## Lojas {#stores}

A seção Lojas lista todos os armazenamentos do ContextHub que foram configurados. Cada item na lista consiste nas seguintes informações:

* **Título:** A variável [tipo de loja](sample-stores.md) em que o armazenamento se baseia.
* **caminho:** O caminho para o nó do repositório que contém a configuração.
* **resourceType:** O caminho do nó do repositório onde o tipo de armazenamento é definido.
* **clientlibs:** As categorias das bibliotecas de clientes que são carregadas que implementam o tipo de armazenamento.

## Módulos {#modules}

A seção Módulos lista todos os módulos de interface do usuário do ContextHub que foram configurados. Cada item na lista consiste nas seguintes informações:

* **Título:** A variável [Tipo de módulo da UI](sample-modules.md) em que o módulo de interface do usuário se baseia.
* **caminho:** O caminho para o nó do repositório que contém a configuração.
* **resourceType:** O caminho do nó do repositório onde o tipo de módulo da interface do usuário é definido.
* **clientlibs:** As categorias das bibliotecas de clientes que são carregadas que implementam o tipo de módulo de interface do usuário.

## Clientlibs {#clientlibs}

A seção Clientlibs lista todas as [pastas da biblioteca cliente](/help/implementing/developing/introduction/clientlibs.md) que o ContextHub carregou. As bibliotecas de clientes são categorizadas da seguinte maneira:

* **kernel.js:** Bibliotecas de clientes que implementam a estrutura do ContextHub, o mecanismo de segmento e os tipos de armazenamento.
* **ui.js:** Bibliotecas de clientes que implementam a interface do usuário do ContextHub e os tipos de módulo de interface do usuário.
* **style.css:** Arquivos CSS que são carregados das bibliotecas de clientes.

## URLs {#urls}

A seção URLs contém links para recursos do ContextHub:

* **Editor de configuração:** Abre a [Página Configuração do ContextHub](configuring-contexthub.md) onde você pode configurar lojas, modos de interface e módulos de interface do usuário.
* **Configuração de módulos do ContextHub:** Abre a `/etc/cloudsettings/default/contexthub.config.kernel.js` arquivo, que contém a representação do objeto JavaScript das configurações de armazenamento do ContextHub.
* **Configuração da interface do ContextHub:** Abre a `/etc/cloudsettings/default/contexthub.config.ui.js` arquivo, que contém a representação do objeto Javascript das configurações de modo da interface do usuário do ContextHub.
* **kernel.js:** Abre a `/etc/cloudsettings/default/contexthub.kernel.js` arquivo, que contém o código-fonte das bibliotecas de clientes que implementam a estrutura do ContextHub, o mecanismo de segmento e os tipos de armazenamento.
* **ui.js:** Abre a `/etc/cloudsettings/default/contexthub.ui.js` arquivo, que contém o código-fonte das bibliotecas de clientes que implementam os tipos de módulo da interface e da interface do usuário do ContextHub.
* **style.css:** Abre a `/etc/cloudsettings/default/contexthub.styles.css` arquivo, que contém os estilos CSS para a interface do usuário do ContextHub e os módulos de interface do usuário.
