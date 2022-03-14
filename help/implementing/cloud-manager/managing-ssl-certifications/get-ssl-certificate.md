---
title: Obter um certificado SSL - Gerenciar certificados SSL
description: Obter um certificado SSL - Gerenciar certificados SSL
exl-id: a3a247e5-164a-4c9c-aeed-bde882635e6f
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 1%

---

# Obter um certificado SSL {#getting-an-ssl-certificate}

As empresas usam certificados SSL para proteger seus sites e permitir que seus clientes confiem neles. Para usar o protocolo SSL, um servidor da Web requer o uso de um certificado SSL. O Cloud Manager não fornece certificados SSL ou chaves privadas. Essas informações devem ser obtidas junto das Autoridades de Certificação.

Quando uma entidade solicita um certificado de uma autoridade de certificação, a autoridade de certificação conclui um processo de verificação. Isso pode variar desde verificar o controle do nome de domínio até coletar documentos de registro da empresa e contratos de assinante. Depois que as informações de uma entidade forem verificadas, a CA assinará sua chave pública usando a chave privada da CA. Como todas as principais autoridades de certificados têm certificados raiz em navegadores da Web, o certificado da entidade será vinculado por meio de um *cadeia de confiança* e o navegador da Web o reconhecerá como um certificado confiável.

>[!NOTE]
>AEM as a Cloud Service só aceitará certificados OV (Validação da Organização) ou EV (Validação Estendida). Certificados DV(Domain Validation) ou autoassinados não serão aceitos. Os certificados OV e EV fornecem aos usuários informações extras validadas por CA que eles podem usar para decidir se o proprietário de um site, remetente de um email ou signatário digital de código executável ou documentos PDF é confiável. Certificados DV são comuns e baratos. Contudo, não permitem a verificação da propriedade.
>Além disso, qualquer certificado deve ser um certificado TLS X.509 de uma autoridade de certificação (CA) confiável com uma chave privada RSA de 2048 bits correspondente.
