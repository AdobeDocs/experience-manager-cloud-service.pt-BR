---
title: AEM considerações de segurança as a Cloud Service
description: Saiba mais sobre considerações importantes de segurança ao usar AEM as a Cloud Service
hidefromtoc: true
hide: true
source-git-commit: 39ffd826f5d1e9cea2e6a03a74f39c16647b45fa
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 0%

---


# AEM considerações de segurança as a Cloud Service {#security-considerations}

## AEM Trust Store {#aem-trust-store}

Para oferecer suporte a operações assimétricas e criptográficas, o AEM armazena certificados dentro do repositório de conteúdo, em um armazenamento confiável global. Seu conteúdo é público e, por padrão, é acessível anonimamente por todos em instâncias do editor.

### Características do Armazenamento Fidedigno {#truststore-characteristics}

* O armazenamento de confiança está localizado abaixo `/etc/truststore` e consiste em um arquivo de repositório de chaves Java, a senha de armazenamento de chaves e os metadados do repositório. Observe que a senha e o próprio armazenamento de chaves são criptografados por motivos técnicos, mesmo que os certificados contidos sejam acessíveis a todos por padrão por meio da API
* Imediatamente, os certificados são usados somente para suporte HTTPS e SAML e o armazenamento deve ser criado manualmente primeiro
* Os clientes podem usá-lo em seu próprio código pelo [API do keystore](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/granite/keystore/KeyStoreService.html#getTrustStore-org.apache.sling.api.resource.ResourceResolver-)
* O armazenamento confiável pode ser gerenciado por meio da interface do usuário em **Ferramentas** - **Segurança** - **Armazenamento de confiança** ou acessando *`https://serveraddress:serverport/libs/granite/security/content/truststore.html`*, conforme mostrado abaixo:

   ![Gerenciamento de Armazenamento de Confiança](/help/security/assets/global-trust-store-modified.png)

* O acesso ao repositório de confiança pode ser restringido ainda mais pelo controle de acesso ao repositório, dependendo do caso de uso.

>[!NOTE]
>
>O Adobe recomenda que os controles de acesso padrão sejam usados para o Armazenamento de confiança, o que significa que ele permanece acessível publicamente. Para a configuração mais segura, você pode usar uma política de negar jcr:all para todos.

<!--
Commenting out section for now as requested by Lars

## Anonymous Permission Hardening Package {#anonymous-permission-hardening-package}

For more information on the Anonymous Hardening Package, please see the [Security Checklist](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security-checklist.html#anonymous-permission-hardening-package).
-->
