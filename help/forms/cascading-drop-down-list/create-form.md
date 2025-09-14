---
title: Criar formulário usando o editor universal
description: Use expressões adaptáveis do Forms para adicionar validação automática, cálculo e ativar ou desativar a visibilidade de uma seção.
feature: Adaptive Forms, Foundation Components
role: User
hide: true
hidefromtoc: true
source-git-commit: 53e476981874597bfb7f9293e67b2d135c72b318
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---

# Criar formulário usando o editor universal

Crie o formulário a seguir usando o editor universal. O formulário tem três listas suspensas, cujos valores serão preenchidos usando a integração da API
![formulário-adaptável](assets/address-form.png)

## País de residência

Na inicialização, o menu suspenso do país de residência será preenchido com os resultados da chamada à API.
![inicializar-evento](assets/initialize-event.png)

## Manipulador de sucesso

O manipulador de sucesso foi definido para definir o enum e enumNames da lista suspensa do país com os valores apropriados da matriz geonames. A matriz geonames está disponível na opção Carga do evento
![carga-evento](assets/event-payload.png)
![manipulador de sucesso](assets/success-handler.png)

## Buscar valores secundários

A lista suspensa de estado ou província é preenchida quando o usuário faz uma seleção na lista suspensa País de residência. O geonameId associado ao país selecionado é passado como parâmetro de entrada para a integração da API GetChildren

![obter-filhos](assets/invoke-service-get-children.png)

O manipulador de êxito foi definido para definir enum/enumNames do campo suspenso StateOrProvince
![get-children-success-handler](assets/child-success-handler.png)

Quando o estado ou província é selecionado, você pode preencher a lista suspensa cidade seguindo o padrão mencionado acima usado para preencher a lista suspensa estado ou província.