---
title: De planilhas para Forms - Dominando validações de campo de bloco adaptáveis do Forms
description: Crie formulários poderosos mais rápido usando planilhas e campos de bloco adaptáveis do Forms! Este guia ajuda a criar validações personalizadas para campos de Bloqueio de EDS Forms.
feature: Edge Delivery Services
hide: true
hidefromtoc: true
exl-id: 16e1d42a-42d0-4335-ba81-feedea7ed7d7
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---

# Adicionar validações a campos de formulário

O bloco adaptável do Forms tem recursos de validação integrados. Essas validações são aplicadas automaticamente em navegadores modernos com base no tipo de campo escolhido e nas propriedades adicionais fornecidas.

## Noções básicas sobre tipos de campo e validação

O Bloco Forms Adaptável oferece suporte a vários [tipos de entrada HTML-5](https://developer.mozilla.org/pt-BR/docs/Web/HTML/Element/input#input_types), incluindo texto, email, número, data e muito mais. Também acomoda [textarea](https://developer.mozilla.org/pt-BR/docs/Web/HTML/Element/textarea), select e fieldset, juntamente com recursos abrangentes de validação de entrada inerentes ao HTML-5.

O usa tipos de campo do HTML para definir o tipo de dados que um usuário pode inserir. Tipos de campos diferentes têm regras de validação integradas diferentes:

Email: esse tipo de campo valida automaticamente a entrada do usuário em relação a um formato de endereço de email comum. Os usuários que inserirem um email inválido verão uma mensagem de erro.
Número: esse tipo de campo permite apenas entrada numérica. Os usuários que inserirem caracteres não numéricos receberão um erro.
Data: esse tipo de campo valida a entrada do usuário em relação a um formato de data padrão. Datas fora de um intervalo razoável também podem ser sinalizadas como inválidas.
URL: esse tipo de campo valida a entrada do usuário em relação a um formato de URL válido. Os usuários que inserirem um URL inválido verão uma mensagem de erro.
Telefone: esse tipo de campo foi projetado especificamente para números de telefone e pode acionar a validação com base em formatos específicos de país (não suportado universalmente).



