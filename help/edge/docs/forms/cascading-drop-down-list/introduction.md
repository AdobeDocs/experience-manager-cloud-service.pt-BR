---
title: Lista suspensa em cascata
description: Use a Integração de API para preencher dinamicamente a lista suspensa
feature: Edge Delivery Services
role: User,Developer
source-git-commit: 53e476981874597bfb7f9293e67b2d135c72b318
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 2%

---

# Descrição do caso de uso

Ao criar formulários ou aplicativos, geralmente é útil guiar os usuários pela seleção de local de maneira estruturada. Uma lista suspensa em cascata torna isso simples e fácil de usar — o usuário primeiro seleciona um país, que filtra a lista de estados/províncias disponíveis e, em seguida, uma escolha final de cidades com base no estado. Essa abordagem não só mantém os formulários mais limpos, como também impede combinações inválidas (como escolher uma cidade que não existe em um estado escolhido).

As etapas a seguir são necessárias para realizar esse caso de uso

- Criar integração com a API
- Criar formulário com campos para capturar país/estado/cidade
- Criar regra para preencher as listas suspensas usando a integração de API