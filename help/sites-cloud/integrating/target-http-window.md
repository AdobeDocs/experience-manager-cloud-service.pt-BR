---
title: Janela HTTP do Adobe AEM Target
description: Janela HTTP do Adobe AEM Target
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 89%

---


# Introdução {#introduction}

Esta página descreve os parâmetros configuráveis presentes na janela HTTP do Adobe AEM Target.

## Parâmetros {#parameters}

![Janela HTTP do Target](assets/httpwindow.png "Janela HTTP do Target")

A janela contém os seguintes parâmetros configuráveis:

| Parâmetro | Descrição |
|---|---|
| URL da API do Adobe Target | O URL da API do Adobe Target. |
| Ativar URL absoluto | Determina se a parte do host do URL ou o URL completo é usado. Ative a caixa de seleção se desejar usar o URL completo (não abreviado). Por padrão, a caixa de seleção está desativada. |
| Tempo de espera limite da conexão | O tempo limite (em milissegundos) para que uma conexão seja estabelecida. O valor padrão é 60.000 milissegundos. Um valor de 0 é interpretado como um tempo limite infinito. |
| Tempo limite do soquete | O tempo limite (em milissegundos) para aguardar por dados ou um período máximo de inatividade entre dois pacotes de dados consecutivos. O valor padrão é 30.000 milissegundos. |
| Token regex de substituição de URL do Adobe Target Recommendations | Controla o token no URL do endpoint do Adobe Target que deve ser substituído para apontar para o URL da API do Target Recommendations. |
| Token de substituição de URL do Adobe Target Recommendations | Substituição do regex descrito no parâmetro acima para que o URL resultante aponte para a API do Target Recommendations. |
