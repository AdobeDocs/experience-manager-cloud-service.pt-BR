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
>Para obter as notas de versão atuais do Adobe Experience Manager as a Cloud Service, consulte [nesta página.](/help/release-notes/release-notes-cloud/release-notes-current.md)

## Novidades {#what-is-new}

* **Início**: as páginas recentes são exibidas como uma lista, sem imagens de pré-visualização.
* **Barra de localização**: a validação aprimorada do URL foi adicionada, impondo URLs HTTPS e hashes de suporte em URLs para contabilizar aplicativos roteados por hash.
* **Navegação do teclado**: a seleção de sobreposição de página foi dissociada do foco do painel de propriedades para melhorar a navegação do teclado na página sem perder o foco.
* **Rótulos de item**: o valor de fallback dos rótulos agora usa `data-aue-prop` em vez de `data-aue-type` para obter uma identificação mais clara nas sobreposições e na árvore de conteúdo.
* **Modal RTE**: A **Cancelar** Foi adicionado um botão ao modal do editor de rich text ao abri-lo no painel de propriedades.
* **Serviço UE no nó**: o suporte HTTP para o Universal Editor Service foi reintroduzido, pois todas as conexões HTTPS são encerradas no nível do Dispatcher.
* **API de cópia interna**: uma API ao Serviço do editor universal para copiar componentes foi adicionada, permitindo a introdução futura de opções da barra de ferramentas para copiar e duplicar conteúdo.

## Correções de erros {#bug-fixes}

* **Navegação estrutural no painel Propriedades**: o menu de navegação estrutural no painel de propriedades para itens aninhados profundamente, que não permaneciam abertos, foi corrigido.
* **Seletor de fragmentos de conteúdo**: o seletor de Fragmento de conteúdo foi aprimorado para garantir que respeite as regras definidas no modelo de Fragmento de conteúdo ou na `data-aue-filter`.
* **Inserção de componente**: a lista para inserir novos componentes que não foram atualizados com precisão após navegar para outra página foi corrigida.
* **Status da publicação**: o manuseio dos status de publicação foi aprimorado para funcionar de forma mais consistente.
* **Correções diversas**: esta versão também contém várias correções secundárias, limpeza de débito de tecnologia, aprimoramentos de segurança e testes consolidados para estabilidade e desempenho gerais.
