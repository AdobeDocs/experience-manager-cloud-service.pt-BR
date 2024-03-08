---
title: Os serviços de entrega de borda da AEM Forms geralmente usavam expressões regex para validar campos de formulário
description: Os serviços de entrega de borda da AEM Forms geralmente usavam expressões regex para validar campos de formulário
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: 53a66eac5ca49183221a1d61b825401d4645859e
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 4%

---


# Expressões regex geralmente usadas para validações

Estas são algumas expressões regulares que você pode usar para aprimorar a validação de formulários além do que os navegadores modernos oferecem:

## Senha forte

```regex
^(?=.*[a-z])(?=.*[A-Z])(?=.*\d)(?=.*[@$!%*?&])[A-Za-z\d@$!%*?&]{8,}$
```

Garante pelo menos 8 caracteres com:

* Letra minúscula (a-z)
* Letra maiúscula (A-Z)
* Dígito (0-9)
* Caractere especial (@$!%*?&amp;)


## Endereço de email


```regex
^[a-zA-Z0-9.!#$%&'*+/=?^_`{|}~-]+@[a-zA-Z0-9-]+(?:\.[a-zA-Z0-9-]+)*$
```

Permite letras, números e caracteres especiais no nome de usuário e nome de domínio.


## Número de telefone (formato dos EUA)

```regex
^\(?([0-9]{3})\)?[-. ]([0-9]{3})[-. ]([0-9]{4})$
```

Valida números de telefone no formato (XXX) XXX-XXXX.



## URL

```regex
^(http|https)://.*$
```

Garante um URL válido começando com http ou https.



## Data (AAAA-MM-DD)

```regex
^\d{4}-(0[1-9]|1[0-2])-(0[1-9]|[12][0-9]|3[01])$
```

Valida datas no formato AAAA-MM-DD.


## Hora (HH:MM)

```regex
^([01][0-9]|2[0-3]):[0-5][0-9]$
```

Valida horas no formato HH:MM (formato de 24 horas).


## CEP (formato EUA)

```regex
^\d{5}(?:[-\ ]\d{4})?$
```

Valida códigos postais dos EUA de 5 dígitos com hífen opcional e extensão de 4 dígitos.


## Nome de usuário (alfanumérico e sublinhado)

```regex
^[a-zA-Z0-9_]+$
```

Permite letras, números e sublinhados.


## Código hexadecimal de cor

```regex
^#[0-9a-fA-F]{6}$
```

Valida códigos de cor hexadecimais de 6 dígitos. Por exemplo, #FFFFFF.


## Endereço IP

```regex
^(25[0-5]|2[0-4][0-9]|1[0-9][0-9]|[0-9]{2,3})\.(25[0-5]|2[0-4][0-9]|1[0-9][0-9]|[0-9]{2,3})\.(25[0-5]|2[0-4][0-9]|1[0-9][0-9]|[0-9]{2,3})\.(25[0-5]|2[0-4][0-9]|1[0-9][0-9]|[0-9]{2,3})$
```

Valida endereços IPv4.



## Número do Seguro Social (formato dos EUA)

```regex
^\d{3}-\d{2}-\d{4}$
```



## Número do cartão de crédito

```regex
^(?:4[0-9]{12}(?:[0-9]{3})?|[25][1-7][0-9]{14}$
```

Valida números de telefone no formato (XXX) XXX-XXXX.



## Número de telefone (formato dos EUA):

```regex
^[a-zA-Z0-9.!#$%&'*+/=?^_`{|}~-]+@[a-zA-Z0-9-]+(?:\.[a-zA-Z0-9-]+)*$
```

Valida números de telefone no formato (XXX) XXX-XXXX.
