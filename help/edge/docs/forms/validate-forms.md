---
title: De planilhas para Forms - Dominando validações de campo de bloco do formulário adaptável
description: Crie formulários poderosos mais rápido usando planilhas e campos de bloco de formulário adaptável! Este guia ajuda a criar validações personalizadas para campos de Bloqueio de EDS Forms.
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: e8fbe3efae7368c940cc2ed99cc9a352bbafbc22
workflow-type: tm+mt
source-wordcount: '266'
ht-degree: 0%

---


# Adicionar validações a campos de formulário

O bloco de formulário adaptável tem recursos de validação integrados. Essas validações são aplicadas automaticamente em navegadores modernos com base no tipo de campo escolhido e nas propriedades adicionais fornecidas.

## Noções básicas sobre tipos de campo e validação

O bloco de formulário adaptável oferece suporte a uma variedade de [tipos de entrada HTML-5](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#input_types), incluindo texto, email, número, data e muito mais. Também acomoda [textarea](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/textarea), select e fieldset, juntamente com recursos abrangentes de validação de entrada inerentes ao HTML-5.

O usa tipos de campo HTML para definir o tipo de dados que um usuário pode inserir. Tipos de campos diferentes têm regras de validação integradas diferentes:

Email: esse tipo de campo valida automaticamente a entrada do usuário em relação a um formato de endereço de email comum. Os usuários que inserirem um email inválido verão uma mensagem de erro.
Número: esse tipo de campo permite apenas entrada numérica. Os usuários que inserirem caracteres não numéricos receberão um erro.
Data: esse tipo de campo valida a entrada do usuário em relação a um formato de data padrão. Datas fora de um intervalo razoável também podem ser sinalizadas como inválidas.
URL: esse tipo de campo valida a entrada do usuário em relação a um formato de URL válido. Os usuários que inserirem um URL inválido verão uma mensagem de erro.
Telefone: esse tipo de campo foi projetado especificamente para números de telefone e pode acionar a validação com base em formatos específicos de país (não suportado universalmente).


## Veja mais

* [Criar e visualizar um formulário](/help/edge/docs/forms/create-forms.md)
* [Ativar formulário para enviar dados](/help/edge/docs/forms/submit-forms.md)
* [Publicar um formulário na página de sites](/help/edge/docs/forms/publish-eds-forms.md)
* [Adicionar validações a campos de formulário](/help/edge/docs/forms/validate-forms.md)
* [Alterar temas e estilo de formulário](/help/edge/docs/forms/style-theme-forms.md)