---
title: Entendendo os tipos de programas e programas
description: Entendendo os tipos de programas e programas - Serviços em nuvem
translation-type: tm+mt
source-git-commit: 1129188c06d893bbeb8f8861b6fae25052605f12

---


# Noções básicas sobre programas e tipos de programas {#understanding-programs}

No Cloud Manager, você tem a entidade Inquilino na parte superior, que pode ter vários Programas dentro dela.  Cada programa não pode conter mais de um ambiente de produção e vários ambientes que não sejam de produção.

## Tipos de programas {#program-types}

Um usuário pode criar um **Sandbox** ou um programa **Regular** .

Geralmente, uma *caixa de proteção* é criada para servir aos propósitos de treinamento, execução de demonstração, ativação, POC ou documentação. Não se trata de transportar tráfego em direto e de ter restrições que um programa regular não fará. Ela incluirá Sites e Ativos e será fornecida automaticamente com uma ramificação Git que inclui código de amostra, um ambiente de Desenvolvimento e um pipeline de não-produção.

Um programa ** regular é criado para ativar o tráfego ao vivo no momento apropriado no futuro.