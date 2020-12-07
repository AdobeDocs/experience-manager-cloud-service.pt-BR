---
title: Obter um certificado SSL - Gerenciamento de certificados SSL
description: Obter um certificado SSL - Gerenciamento de certificados SSL
translation-type: tm+mt
source-git-commit: fecbd0b4d5cfd8aa970c235c79158bea44403c09
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 0%

---


# Obtendo um certificado SSL {#getting-an-ssl-certificate}

As empresas usam certificados SSL para proteger seus sites e permitir que seus clientes confiem neles. Para usar o protocolo SSL, um servidor Web requer o uso de um certificado SSL. O Cloud Manager não fornece certificados SSL nem chaves privadas. Estes devem ser obtidos junto das Autoridades de Certificação (AC).

Quando uma entidade solicita um certificado de uma autoridade de certificação, a autoridade de certificação conclui um processo de verificação. Isso pode variar desde a verificação do controle de nome de domínio até a coleta de documentos de registro de empresa e contratos de assinante. Depois que as informações de uma entidade forem verificadas, a CA assinará sua chave pública usando a chave privada da CA. Como todas as principais autoridades de certificados têm certificados raiz em navegadores da Web, o certificado da entidade será vinculado por meio de uma *cadeia de confiança* e o navegador da Web o reconhecerá como um certificado confiável.

>[!NOTE]
>AEM como Cloud Service só aceitará certificados OV(Organization Validation) ou EV(Extended Validation). Certificados DV(Domain Validation) ou autoassinados não serão aceitos. Os certificados OV e EV fornecem aos usuários informações extras validadas por CA que eles podem usar para decidir se o proprietário de um site, remetente de um email ou signatário digital de um código executável ou documentos PDF é confiável. Certificados DV são comuns e baratos. No entanto, não permitem a verificação da propriedade.

