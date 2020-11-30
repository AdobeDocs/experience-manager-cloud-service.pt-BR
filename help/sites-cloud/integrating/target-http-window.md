---
title: Janela HTTP do Público alvo AEM
description: 'Janela HTTP do Público alvo AEM '
translation-type: tm+mt
source-git-commit: c193b38718622cd2e960a8e8833c2d295822dc33
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 4%

---


# Introdução {#introduction}

Esta página descreve os parâmetros configuráveis presentes na janela HTTP do Público alvo AEM.

## Parâmetros {#parameters}

![Público alvo HTTP](assets/httpwindow.png "WindowTarget Janela HTTP")

A janela contém os seguintes parâmetros configuráveis:

| Parâmetro | Descrição |
|---|---|
| URL da API do Adobe Target | O URL da API do Adobe Target. |
| Ativar URL absoluto | Determina se a parte host do URL ou o URL completo é usado. Ative a caixa de seleção se desejar usar o URL completo (não abreviado). Por padrão, a caixa de seleção é desativada. |
| Tempo de espera limite da conexão | O tempo limite (em milissegundos) até que uma conexão seja estabelecida. O valor padrão é 60000 milissegundos. Um valor de 0 é interpretado como um tempo limite infinito. |
| Tempo limite do soquete | O tempo limite (em milissegundos) para aguardar os dados ou um período máximo de inatividade entre dois pacotes de dados consecutivos. O valor padrão é 30000 milissegundos. |
| Adobe Target Recommendations URL - Substituir Token Regex | Controla o token no URL do ponto final do Adobe Target que precisa ser substituído para apontar para o URL da API do Público alvo Recommendations. |
| Adobe Target Recommendations URL Replace com Token | A substituição do regex descrito no parâmetro acima, portanto, o URL resultante apontará para a API de recomendações do Público alvo. |
