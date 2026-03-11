---
title: Como reiniciar o AEM SDK?
description: Práticas recomendadas para reiniciar o AEM SDK
role: Admin, Developer, User
feature: Adaptive Forms
badgeSaas: label="AEM Forms" type="Positive" tooltip="Aplicável ao AEM Forms)."
exl-id: 5fec2a93-1dda-4240-8690-24a6afae5c2b
source-git-commit: 89b0f2a8ca9d2f60365a5c3962b0b4e826f79b3e
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 4%

---

# Reiniciar o AEM SDK

Se você reiniciar o AEM SDK interrompendo os processos do Java™, o poderá causar inconsistências no ambiente de desenvolvimento do AEM, e um erro ocorrerá:

`javax.jcr.RepositoryException: Applying repoinit operation failed despite retry; set loglevel to DEBUG to see all exceptions. Last exception message was: Failed to set ACL (javax.jcr.ValueFormatException: Invalid type: 0) AclLine ALLOW {principals=[forms-xfa-writers], privileges=[jcr:modifyProperties]} restrictions=[rep:glob=[*/jcr:content/*], rep:itemNames=[xfaForm], fd:condition=[xfaForm, 1]]`

![Reiniciar-aem-sdk-erro](/help/forms/assets/restart-sdk-error.png)

## Solução

Para reiniciar o AEM SDK, vá para a janela de comando ativa e pressione o comando `Ctrl + C` para reiniciar o SDK.

É recomendável usar o comando &#39;Ctrl + C&#39; para reiniciar o SDK. Reiniciar o AEM SDK usando métodos alternativos, por exemplo, parar processos Java™, pode levar a inconsistências no ambiente de desenvolvimento do AEM.

## Consulte também:

* [Configurar ambiente de desenvolvimento local para o AEM Forms](/help/forms/setup-local-development-environment.md)

