---
title: Considerações de segurança do AEM as a Cloud Service
description: Saiba mais sobre as considerações importantes de segurança ao usar o AEM as a Cloud Service
hidefromtoc: true
hide: true
exl-id: d2dfde05-ce02-478e-8697-b939fb8740c3
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: ht
source-wordcount: '229'
ht-degree: 100%

---

# Considerações de segurança do AEM as a Cloud Service {#security-considerations}

## Armazenamento confiável do AEM {#aem-trust-store}

Para permitir operações assimétricas e criptográficas, o AEM armazena certificados no repositório de conteúdo, em um armazenamento global confiável. O conteúdo é público e, por padrão, é acessível anonimamente por todos nas instâncias do editor.

### Características do armazenamento confiável {#truststore-characteristics}

* O armazenamento confiável está localizado abaixo de `/etc/truststore` e consiste em um arquivo de armazenamento de chave Java, a senha do armazenamento de chaves e os metadados do repositório. Observe que a senha e o próprio armazenamento de chaves são criptografados por motivos técnicos, mesmo que os certificados contidos sejam acessíveis a todos por padrão por meio da API
* Prontos para uso, os certificados são usados somente para suporte HTTPS e SAML e o armazenamento deve ser criado manualmente primeiro
* Os clientes podem usá-lo em seu próprio código por meio da [API de armazenamento de chaves](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/granite/keystore/KeyStoreService.html#getTrustStore-org.apache.sling.api.resource.ResourceResolver-)
* O armazenamento confiável pode ser gerenciado por meio da interface em **Ferramentas** - **Segurança** - **Armazenamento confiável** ou acessando *`https://serveraddress:serverport/libs/granite/security/content/truststore.html`*, conforme mostrado abaixo:

  ![Gerenciamento de armazenamento confiável](/help/security/assets/global-trust-store-modified.png)

* O acesso ao armazenamento confiável pode ser ainda mais restrito pelo controle de acesso ao repositório, dependendo do caso de uso.

>[!NOTE]
>
>O Adobe recomenda que os controles de acesso padrão sejam usados para o Armazenamento confiável, o que significa que ele permanece acessível publicamente. Para a configuração mais segura, você pode usar uma política de recusar jcr:all para todos.

<!--
Commenting out section for now as requested by Lars

## Anonymous Permission Hardening Package {#anonymous-permission-hardening-package}

For more information on the Anonymous Hardening Package, see [Security Checklist](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security-checklist.html#anonymous-permission-hardening-package).
-->
