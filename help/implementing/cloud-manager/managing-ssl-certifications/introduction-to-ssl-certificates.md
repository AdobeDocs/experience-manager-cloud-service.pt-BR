---
title: Introdução aos certificados SSL
description: Saiba mais sobre as ferramentas de autoatendimento que a Cloud Manager fornece para instalar e gerenciar certificados SSL.
exl-id: 0d41723c-c096-4882-a3fd-050b7c9996d8
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: fa99656e0dd02bb97965e8629d5fa657fbae9424
workflow-type: tm+mt
source-wordcount: '928'
ht-degree: 21%

---


# Introdução aos certificados SSL{#introduction}

Saiba mais sobre as ferramentas de autoatendimento que a Cloud Manager fornece para instalar e gerenciar certificados SSL (Secure Socket Layer).

>[!CONTEXTUALHELP]
>id="aemcloud_golive_sslcert"
>title="Gerenciar certificados SSL"
>abstract="Saiba como o Cloud Manager fornece ferramentas de autoatendimento para instalar e gerenciar certificados SSL a fim de proteger seu site para os usuários. O Cloud Manager usa um serviço TLS para gerenciar certificados SSL e chaves privadas de propriedade de clientes e obtidas de autoridades de certificação terceirizadas."
>additional-url="https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-ssl-certificates/managing-certificates" text="Visualização, atualização e substituição de um certificado SSL"
>additional-url="https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-ssl-certificates/managing-certificates" text="Verificar o status de um certificado SSL"

## O que são certificados SSL? {#overview}

Empresas e organizações usam certificados SSL (Secure Socket Layer) para proteger seus sites e permitir que seus clientes confiem neles. Para usar o protocolo SSL, um servidor da Web exige um certificado SSL.

Quando uma entidade, como uma organização ou empresa, solicita um certificado de uma autoridade de certificação (CA), a CA conclui um processo de verificação. Esse processo pode variar desde a verificação do controle do nome de domínio até a coleta de documentos de registro da empresa e contratos de assinante. Depois que as informações de uma entidade são verificadas, a CA assina sua chave pública usando a chave privada da CA. Como todas as principais Autoridades de Certificação têm certificados raiz em navegadores da Web, o certificado da entidade é vinculado por meio de uma *cadeia de confiança*, e o navegador da Web a reconhece como um certificado confiável.

>[!IMPORTANT]
>
>O Cloud Manager não fornece certificados SSL ou chaves privadas. Essas peças devem ser obtidas de uma autoridade de certificação, uma organização terceirizada confiável. Algumas Autoridades de Certificação conhecidas incluem *DigiCert*, *Let&#39;s Encrypt*, *GlobalSign*, *Entrust* e *Verisign*.

## Gerenciar certificados com o Cloud Manager {#cloud-manager}

O Cloud Manager oferece ferramentas de autoatendimento para instalar e gerenciar certificados SSL, garantindo a segurança do site para seus usuários. A Cloud Manager oferece suporte a dois modelos para gerenciar certificados.

| | Modelo | Descrição |
| --- | --- | --- |
| A | **[DV (certificado SSL gerenciado por Adobe)](#adobe-managed)** | O Cloud Manager permite que os usuários configurem os certificados DV (Validação de domínio) fornecidos pelo Adobe para configuração rápida do domínio. |
| B | **[Certificado SSL gerenciado pelo cliente (OV/EV)](#customer-managed)** | A Cloud Manager oferece um serviço TLS (Transport Layer Security) para permitir que você gerencie certificados SSL OV e EV que você possui e chaves privadas de Autoridades de Certificação de terceiros, como *Vamos Criptografar*. |

Ambos os modelos oferecem os seguintes recursos gerais para gerenciar seus certificados:

* Cada ambiente do Cloud Manager pode usar vários certificados.
* Uma chave privada pode emitir vários certificados SSL.
* O serviço TLS da plataforma encaminha solicitações para o serviço de CDN do cliente, com base no certificado SSL usado para encerramento, e para o serviço de CDN que hospeda esse domínio.

>[!IMPORTANT]
>
>[Para adicionar e associar um domínio personalizado a um ambiente](/help/implementing/cloud-manager/custom-domain-names/introduction.md), é necessário ter um certificado SSL válido que cubra o domínio.

### Certificados SSL gerenciados por Adobe (DV) {#adobe-managed}

Os certificados DV são o nível mais básico da certificação SSL e são frequentemente usados para fins de teste ou para proteger sites com criptografia básica. Os certificados DV estão disponíveis em [programas de produção e programas de sandbox](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md).

Após a criação do certificado DV, o Adobe o renova automaticamente a cada três meses, a menos que ele seja excluído.

### Certificados SSL OV/EV gerenciados pelo cliente {#customer-managed}

Os certificados OV e EV oferecem informações validadas pela CA. Essas informações ajudam os usuários a avaliar se o proprietário do site, remetente de email ou signatário digital de documentos de código ou PDF pode ser confiável. Os certificados DV não permitem essa verificação de propriedade.

OV e EV também oferecem esses recursos em relação aos certificados DV na Cloud Manager.

* Vários ambientes podem usar um certificado OV/EV. Ou seja, pode ser adicionado uma vez, mas usado várias vezes.
* Cada certificado OV/EV normalmente contém vários domínios.
* A Cloud Manager aceita certificados OV/EV curingas para um domínio.

>[!TIP]
>
>Se você tiver vários domínios personalizados, talvez não queira carregar um certificado sempre que adicionar um novo domínio. Nesse caso, você pode se beneficiar com a obtenção de um único certificado que abrange vários domínios.

>[!NOTE]
>
>Se dois certificados abrangerem o mesmo domínio estiverem instalados, o mais exato será aplicado.
>
>Por exemplo, se o seu domínio for `dev.adobe.com` e você tiver um certificado para `*.adobe.com` e outro para `dev.adobe.com`, o mais específico (`dev.adobe.com`) será usado.

#### Requisitos para certificados SSL OV/EV gerenciados pelo cliente {#requirements}

Se você optar por adicionar seu próprio certificado SSL OV/EV gerenciado pelo cliente, ele deverá atender aos seguintes requisitos:

* A AEM as a Cloud Service aceita certificados que estejam em conformidade com a política OV (Validação da organização) ou EV (Validação estendida).
   * A Cloud Manager não oferece suporte à adição de certificados DV (Validação de domínio).
* Qualquer certificado deve ser um certificado TLS X.509 de uma Autoridade de certificação confiável com uma chave privada RSA de 2048 bits correspondente.
* Certificados autoassinados não são aceitos.

#### Formato para certificados gerenciados pelo cliente {#certificate-format}

Os arquivos de certificado SSL devem estar no formato PEM para serem instalados com o Cloud Manager. Extensões de arquivo comuns no formato PEM incluem `.pem,`. .`crt`, `.cer`, e `.cert`.

Os seguintes comandos `openssl` podem ser usados para converter certificados não PEM.

* Converter PFX em PEM

  ```shell
  openssl pkcs12 -in certificate.pfx -out certificate.cer -nodes
  ```

* Converter P7B em PEM

  ```shell
  openssl pkcs7 -print_certs -in certificate.p7b -out certificate.cer
  ```

* Converter DER em PEM

  ```shell
  openssl x509 -inform der -in certificate.cer -out certificate.pem
  ```

>[!TIP]
>
>A Adobe recomenda que você valide a integridade do certificado localmente usando uma ferramenta como o `openssl verify -untrusted intermediate.pem certificate.pem` antes de tentar instalá-lo usando o Cloud Manager.

## Limitação do número de certificados SSL instalados {#limitations}

A qualquer momento, o Cloud Manager permite no máximo 50 certificados SSL instalados. Esses certificados podem ser associados a um ou mais ambientes em todo o programa e também incluir certificados expirados.

Se tiver atingido o limite, revise os certificados e considere excluir os certificados expirados. Ou agrupe vários domínios no mesmo certificado, pois um certificado pode abranger vários domínios (até 100 SANs).

## Saiba mais {#learn-more}

Um usuário com as permissões necessárias pode usar o Cloud Manager para gerenciar certificados SSL para um programa. Consulte os documentos a seguir para obter mais detalhes sobre a utilização desses recursos.

* [Adicionar um certificado SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) <!--CQDOC-21758, #4 -->
* [Gerenciar certificados SSL](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md) <!--CQDOC-21758, #4 -->

