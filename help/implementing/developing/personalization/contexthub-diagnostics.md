---
title: Diagnóstico do ContextHub
description: O ContextHub fornece uma página de diagnósticos na qual você pode ver uma visão geral da estrutura do ContextHub
translation-type: tm+mt
source-git-commit: 1c518830f0bc9d9c7e6b11bebd6c0abd668ce040
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 0%

---


# Diagnóstico do ContextHub {#contexthub-diagnostics}

O ContextHub fornece uma página de diagnósticos na qual você pode ver uma visão geral da estrutura do ContextHub. Para abrir a página, vá para a página `contexthub.diagnostics.html` da instância do autor AEM, por exemplo:

`http://<host>:<port>/conf/<site>/settings/cloudsettings/default/contexthub.diagnostics.html`

A página Diagnóstico do ContextHub fornece informações sobre os armazenamentos e os módulos de interface do usuário que foram criados, as pastas da biblioteca do cliente que foram carregadas e os links para páginas úteis.

>[!NOTE]
>
>Para que as informações de diagnóstico sejam retornadas, o modo de depuração deve estar ativado, caso contrário, a página de diagnósticos ficará em branco. Consulte [este documento](configuring-contexthub.md#debugging-contexthub) para obter detalhes sobre como ativar o modo de depuração.

## Armazena {#stores}

A seção Lojas lista todos os armazenamentos do ContextHub que foram configurados. Cada item da lista consiste nas seguintes informações:

* **Título:** O tipo de  [loja em que a ](sample-stores.md) loja se baseia.
* **path:** O caminho para o nó do repositório que armazena a configuração.
* **resourceType:** O caminho do nó do repositório no qual o tipo de armazenamento é definido.
* **clientlibs:** as categorias das bibliotecas clientes que são carregadas que implementam o tipo de armazenamento.

## Módulos {#modules}

A seção Módulos lista todos os módulos de interface do usuário do ContextHub que foram configurados. Cada item da lista consiste nas seguintes informações:

* **Título:** O tipo de módulo  [da interface ](sample-modules.md) em que o módulo da interface do usuário se baseia.
* **path:** O caminho para o nó do repositório que armazena a configuração.
* **resourceType:** O caminho do nó do repositório no qual o tipo de módulo da interface é definido.
* **clientlibs:** as categorias das bibliotecas clientes que são carregadas que implementam o tipo de módulo da interface do usuário.

## Clientlibs {#clientlibs}

A seção Clientlibs lista todas as [pastas da biblioteca do cliente](/help/implementing/developing/introduction/clientlibs.md) que o ContextHub carregou. As bibliotecas do cliente são categorizadas da seguinte forma:

* **kernel.js:bibliotecas** clientes que implementam a estrutura do ContextHub, o mecanismo de segmento e os tipos de armazenamento.
* **ui.js:bibliotecas** de clientes que implementam os tipos de módulos de interface do usuário e interface do ContextHub.
* **style.css:arquivos** CSS carregados das bibliotecas do cliente.

## URLs {#urls}

A seção URLs contém links para os recursos do ContextHub:

* **Editor de configuração:** abre a página Configuração do  [ContextHub, ](configuring-contexthub.md) onde você pode configurar lojas, modos de interface do usuário e módulos de interface do usuário.
* **Configuração dos módulos do ContextHub:** Abre o  `/etc/cloudsettings/default/contexthub.config.kernel.js` arquivo, que contém a representação de objeto do Javascript das configurações de armazenamento do ContextHub.
* **Configuração da interface do usuário do ContextHub:** Abre o  `/etc/cloudsettings/default/contexthub.config.ui.js` arquivo, que contém a representação do objeto Javascript das configurações do modo de interface do usuário do ContextHub.
* **kernel.js:** abre o  `/etc/cloudsettings/default/contexthub.kernel.js` arquivo, que contém o código-fonte das bibliotecas clientes que implementam a estrutura do ContextHub, o mecanismo de segmento e os tipos de armazenamento.
* **ui.js:** abre o  `/etc/cloudsettings/default/contexthub.ui.js` arquivo, que contém o código-fonte das bibliotecas do cliente que implementam os tipos de módulo de interface do usuário e do ContextHub.
* **style.css:** abre o  `/etc/cloudsettings/default/contexthub.styles.css` arquivo, que contém os estilos CSS para os módulos de interface do usuário e da interface do ContextHub.
