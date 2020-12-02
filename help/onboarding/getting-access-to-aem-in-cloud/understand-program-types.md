---
title: Como entender os tipos de Programas e Programas
description: Como entender os tipos de Programas e Programas - Cloud Services
translation-type: tm+mt
source-git-commit: 14da491cf09ed46ea425a8d65670d8b851aef388
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 3%

---


# Noções básicas sobre programas e tipos de programas {#understanding-programs}

No Cloud Manager, você tem a entidade Inquilino na parte superior, que pode ter vários Programas dentro dela.  Cada Programa não pode conter mais de um ambiente de produção e vários ambientes que não sejam de produção.

O diagrama a seguir mostra a hierarquia de entidades no Gerenciador de nuvem.

![imagem](assets/program-types1.png)

## Tipos de programas {#program-types}

Um usuário pode criar um programa **Sandbox** ou **Regular**.

Uma *caixa de proteção* é normalmente criada para servir os propósitos de treinamento, execução de demonstração, ativação, POC&#39;s ou documentação. Não se trata de transportar tráfego em direto e de ter restrições que um programa regular não irá impor. Ele incluirá Sites e Ativos e será entregue automaticamente preenchido com uma ramificação Git que inclui código de amostra, um ambiente Dev e um pipeline de não produção.

Um *programa regular* é criado para ativar o tráfego ao vivo no momento apropriado no futuro.