---
title: Considerações de segurança do AEM as a Cloud Service
description: Saiba mais sobre considerações importantes de segurança ao usar o AEM as a Cloud Service.
hidefromtoc: true
hide: true
exl-id: d2dfde05-ce02-478e-8697-b939fb8740c3
feature: Security
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 58%

---

# Considerações de segurança do AEM as a Cloud Service {#security-considerations}

## Armazenamento confiável do AEM {#aem-trust-store}

Para permitir operações assimétricas e criptográficas, o AEM armazena certificados no repositório de conteúdo, em um armazenamento global confiável. O conteúdo é público e, por padrão, é acessível anonimamente por todos nas instâncias do editor.

### Características do armazenamento confiável {#truststore-characteristics}

* O armazenamento de confiança está localizado abaixo de `/etc/truststore` e consiste em um arquivo de armazenamento de chaves Java™, a senha do armazenamento de chaves e os metadados do repositório. Tanto a senha quanto o keystore são criptografados por motivos técnicos, mesmo que os certificados contidos sejam acessíveis a todos por padrão por meio da API
* Prontos para uso, os certificados são usados somente para suporte HTTPS e SAML e o armazenamento deve ser criado manualmente primeiro
* Os clientes podem usá-lo em seu próprio código por meio da [API de armazenamento de chaves](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/granite/keystore/KeyStoreService.html#getTrustStore-org.apache.sling.api.resource.ResourceResolver-)
* O armazenamento confiável pode ser gerenciado por meio da interface em **Ferramentas** - **Segurança** - **Armazenamento confiável** ou acessando *`https://serveraddress:serverport/libs/granite/security/content/truststore.html`*, conforme mostrado abaixo:

  ![Gerenciamento de armazenamento confiável](/help/security/assets/global-trust-store-modified.png)

* O acesso ao armazenamento confiável pode ser ainda mais restrito pelo controle de acesso ao repositório, dependendo do caso de uso.

>[!NOTE]
>
>A Adobe recomenda que os controles de acesso padrão sejam usados para o Trust Store, o que significa que ele permanece acessível publicamente. Para obter a configuração mais segura, você pode usar uma política de negar `jcr:all` para todos.

<!--
Commenting out section for now as requested by Lars

## Anonymous Permission Hardening Package {#anonymous-permission-hardening-package}

For more information on the Anonymous Hardening Package, see [Security Checklist](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security-checklist.html#anonymous-permission-hardening-package).
-->
