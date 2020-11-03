---
title: Obter um certificado SSL - Gerenciamento de certificados SSL
description: Obter um certificado SSL - Gerenciamento de certificados SSL
translation-type: tm+mt
source-git-commit: b0162640b6d85291aba9c926138f39a0433c0a6e
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 0%

---


# Obtendo um certificado SSL {#getting-an-ssl-certificate}

As empresas usam certificados SSL para proteger seus sites e permitir que seus clientes confiem neles. Para usar o protocolo SSL, um servidor Web requer o uso de um certificado SSL. O Cloud Manager não fornece certificados SSL nem chaves privadas. Estes devem ser obtidos junto das Autoridades de Certificação (AC).

Quando uma entidade solicita um certificado de uma autoridade de certificação (CA), a CA conclui um processo de verificação. Isso pode variar desde a verificação do controle de nome de domínio até a coleta de documentos de registro de empresa e contratos de assinante.

Depois que as informações de uma entidade forem verificadas, a CA assinará sua chave pública usando a chave privada da CA. Como todas as principais autoridades de certificados têm certificados raiz em navegadores da Web, o certificado da entidade será vinculado por uma *cadeia de confiança* e o navegador da Web o reconhecerá como um certificado confiável.

