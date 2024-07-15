---
title: Como reiniciar o SDK do AEM?
description: Práticas recomendadas para reiniciar o SDK do AEM
role: Admin, Developer, User
feature: Adaptive Forms
exl-id: 5fec2a93-1dda-4240-8690-24a6afae5c2b
source-git-commit: 62be3c6e98df9002cdfbeef50dd5475c4daa1576
workflow-type: tm+mt
source-wordcount: '107'
ht-degree: 7%

---

# Reiniciar o SDK do AEM

Se você reiniciar o SDK do AEM interrompendo os processos do Java™, o poderá causar inconsistências no ambiente de desenvolvimento do AEM. Um erro ocorrerá:

`javax.jcr.RepositoryException: Applying repoinit operation failed despite retry; set loglevel to DEBUG to see all exceptions. Last exception message was: Failed to set ACL (javax.jcr.ValueFormatException: Invalid type: 0) AclLine ALLOW {principals=[forms-xfa-writers], privileges=[jcr:modifyProperties]} restrictions=[rep:glob=[*/jcr:content/*], rep:itemNames=[xfaForm], fd:condition=[xfaForm, 1]]`

![Reiniciar-aem-sdk-erro](/help/forms/assets/restart-sdk-error.png)

## Solução

Para reiniciar o SDK do AEM, vá para a janela de comando ativa e pressione o comando `Ctrl + C` para reiniciar o SDK.

É recomendável usar o comando &quot;Ctrl + C&quot; para reiniciar o SDK. Reiniciar o SDK do AEM usando métodos alternativos, por exemplo, parar processos do Java™, pode levar a inconsistências no ambiente de desenvolvimento do AEM.

## Consulte também:

* [Configurar ambiente de desenvolvimento local para o AEM Forms](/help/forms/setup-local-development-environment.md)
* [Habilitar os componentes principais dos formulários adaptáveis](/help/forms/enable-adaptive-forms-core-components.md)
