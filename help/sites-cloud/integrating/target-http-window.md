---
title: Janela HTTP do Adobe AEM Target
description: 'Janela HTTP do Adobe AEM Target '
source-git-commit: c193b38718622cd2e960a8e8833c2d295822dc33
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 4%

---


# Introdução {#introduction}

Esta página descreve os parâmetros configuráveis presentes no Adobe AEM da janela HTTP do Target.

## Parâmetros {#parameters}

![Janela HTTP do Target](assets/httpwindow.png "Janela HTTP do Target")

A janela contém os seguintes parâmetros configuráveis:

| Parâmetro | Descrição |
|---|---|
| URL da API do Adobe Target | O URL da API do Adobe Target. |
| Ativar URL absoluto | Determina se a parte do host do URL ou o URL completo é usado. Ative a caixa de seleção se desejar usar o URL completo (não abreviado). Por padrão, a caixa de seleção está desativada. |
| Tempo de espera limite da conexão | O tempo limite (em milissegundos) até que uma conexão seja estabelecida. O valor padrão é 60000 milissegundos. Um valor de 0 é interpretado como um tempo limite infinito. |
| Tempo limite do soquete | O tempo limite (em milissegundos) para aguardar os dados ou um período máximo de inatividade entre dois pacotes de dados consecutivos. O valor padrão é 30000 milissegundos. |
| Toque Regex de Substituição de URL do Adobe Target Recommendations | Controla o token no URL do ponto de extremidade do Adobe Target que precisa ser substituído para apontar para o URL da API do Target Recommendations. |
| Adobe Target Recommendations URL Replace with Token | Substituição do regex descrito no parâmetro acima, para que o URL resultante aponte para a API do Target Recommendations. |
