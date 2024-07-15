---
title: Notas de versão do Universal Editor 2024.06.28
description: Estas são as notas de versão do Universal Editor de 2024.06.28.
feature: Release Information
role: Admin
source-git-commit: cc94ad2ba42707bb7541217f0225b995f64ad84f
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 1%

---


# Notas de versão do Universal Editor 2024.06.28 {#release-notes}

Estas são as notas de versão do Universal Editor de 28 de junho de 2024.

>[!TIP]
>
>Para obter as notas de versão atuais do Adobe Experience Manager as a Cloud Service, consulte [esta página.](/help/release-notes/release-notes-cloud/release-notes-current.md)

## Novidades {#what-is-new}

* **Página inicial**: as páginas recentes são exibidas como uma lista, sem imagens de visualização.
* **Barra de Localização**: a validação de URL aprimorada foi adicionada, impondo URLs HTTPS e hashes de suporte em URLs para conta de aplicativos roteados por hash.
* **Navegação pelo teclado**: a seleção de sobreposição de página foi dissociada do foco do painel de propriedades para melhorar a navegação pelo teclado na página sem perder o foco.
* **Rótulos de Item**: o valor de fallback dos rótulos agora usa `data-aue-prop` em vez de `data-aue-type` para uma identificação mais clara nas sobreposições e na árvore de conteúdo.
* **Modal de RTE**: um botão **Cancelar** foi adicionado ao modal do editor de rich text ao abri-lo no painel de propriedades.
* **UE Service no Nó**: o suporte HTTP para o Universal Editor Service foi reintroduzido, pois todas as conexões HTTPS são encerradas no nível do Dispatcher.
* **API de Cópia Interna**: uma API para o Serviço do Universal Editor para copiar componentes foi adicionada, permitindo a introdução futura de opções da barra de ferramentas para copiar e duplicar conteúdo.

## Correções de erros {#bug-fixes}

* **Navegação estrutural no Painel de Propriedades**: o menu de navegação estrutural no painel de propriedades para itens profundamente aninhados, que não permaneceram abertos, foi corrigido.
* **Seletor de fragmentos de conteúdo**: o seletor de fragmentos de conteúdo foi aprimorado para garantir que respeite as regras definidas no modelo de fragmento de conteúdo ou no `data-aue-filter`.
* **Inserção de componente**: a lista para inserir novos componentes que não foram atualizados com precisão após navegar para outra página foi corrigida.
* **Status da publicação**: o tratamento dos status de publicação foi aprimorado para funcionar de forma mais consistente.
* **Várias correções**: esta versão também contém várias correções secundárias, limpeza de débito técnico, aprimoramentos de segurança e testes consolidados para estabilidade e desempenho gerais.
