---
title: Lista suspensa em cascata
description: Use expressões adaptáveis do Forms para adicionar validação automática, cálculo e ativar ou desativar a visibilidade de uma seção.
feature: Adaptive Forms, Foundation Components
role: User
hide: true
hidefromtoc: true
source-git-commit: cc3cd74ad87f4213a200f36745ab3d335edca02d
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 2%

---

# Descrição do caso de uso

Ao criar formulários ou aplicativos, geralmente é útil guiar os usuários pela seleção de local de maneira estruturada. Uma lista suspensa em cascata torna isso simples e fácil de usar — o usuário primeiro seleciona um país, que filtra a lista de estados/províncias disponíveis e, em seguida, uma escolha final de cidades com base no estado. Essa abordagem não só mantém os formulários mais limpos, como também impede combinações inválidas (como escolher uma cidade que não existe em um estado escolhido).

As etapas a seguir são necessárias para realizar esse caso de uso

- Criar integração com a API
- Criar formulário com campos para capturar país/estado/cidade
- Criar regra para preencher as listas suspensas usando a integração de API