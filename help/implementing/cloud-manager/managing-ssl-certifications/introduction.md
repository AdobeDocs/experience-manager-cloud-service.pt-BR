---
title: Introdução aos certificados SSL
description: Saiba como o Cloud Manager fornece ferramentas de autoatendimento para instalar certificados SSL.
exl-id: 0d41723c-c096-4882-a3fd-050b7c9996d8
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: d2f05915c0bf0af073db7f070b83f13aeae55252
workflow-type: tm+mt
source-wordcount: '765'
ht-degree: 33%

---


# Introdução aos certificados SSL{#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_sslcert"
>title="Gerenciar certificados SSL"
>abstract="Saiba como o Cloud Manager fornece ferramentas de autoatendimento para instalar e gerenciar certificados SSL a fim de proteger seu site para os usuários. O Cloud Manager usa um serviço TLS para gerenciar certificados SSL e chaves privadas de propriedade de clientes e obtidas de autoridades de certificação terceirizadas."
>additional-url="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-ssl-certificates/managing-certificates" text="Visualização, atualização e substituição de um certificado SSL"
>additional-url="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-ssl-certificates/managing-certificates" text="Verificar o status de um certificado SSL"


A Cloud Manager oferece ferramentas de autoatendimento para instalar e gerenciar certificados SSL (Secure Socket Layer), garantindo a segurança do site para seus usuários. Os dois casos de uso a seguir são compatíveis:

<!-- CQDOC-21758, #1 -->

| | Caso de uso | Descrição |
| --- | --- | --- |
| 1 | **DV (certificado gerenciado por Adobe)** | O Cloud Manager permite que os usuários configurem um certificado DV (Validação de domínio) proveniente do Adobe para configuração rápida do domínio. Os certificados DV são o nível mais básico da certificação SSL e são frequentemente usados para fins de teste ou para proteger sites com criptografia básica. Os certificados DV estão disponíveis em [programas de produção e programas de sandbox](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md). Após a criação do certificado DV, o Adobe o renova automaticamente a cada três meses, a menos que ele seja excluído. |
| 2 | **Certificado gerenciado pelo cliente (OV/EV)** | A Cloud Manager usa um serviço TLS (Transport Layer Security) para gerenciar certificados SSL de propriedade do cliente e chaves privadas de Autoridades de Certificação de terceiros, como *Vamos Criptografar*. |

>[!NOTE]
>
>Os clientes não têm permissão para carregar certificados DV (Validação de domínio).


## Introdução aos certificados SSL {#certificates}

Empresas e organizações usam certificados SSL para proteger seus sites e permitir que os clientes confiem neles. Para usar o protocolo SSL, um servidor da Web exige o uso de um certificado SSL.

Quando uma entidade, como uma organização ou empresa, solicita um certificado de uma autoridade de certificação (CA), a CA conclui um processo de verificação. Esse processo pode variar desde a verificação do controle do nome de domínio até a coleta de documentos de registro da empresa e contratos de assinante. Depois que as informações de uma entidade são verificadas, a CA assina sua chave pública usando a chave privada da CA. Como todas as principais Autoridades de Certificação têm certificados raiz em navegadores da Web, o certificado da entidade é vinculado por meio de uma *cadeia de confiança*, e o navegador da Web a reconhece como um certificado confiável.

>[!IMPORTANT]
>
>O Cloud Manager não fornece certificados SSL ou chaves privadas. Essas coisas devem ser obtidas de uma autoridade de certificação, uma organização de terceiros confiável. Algumas Autoridades de Certificação conhecidas incluem *DigiCert*, *Let&#39;s Encrypt*, *GlobalSign*, *Entrust* e *Verisign*.

O Cloud Manager oferece suporte às opções de uso do certificado SSL do cliente descritas a seguir.

* Vários ambientes podem usar um certificado SSL. Ou seja, pode ser adicionado uma vez, mas usado várias vezes.
* Cada ambiente do Cloud Manager pode usar vários certificados.
* Uma chave privada pode emitir vários certificados SSL.
* Cada certificado normalmente contém vários domínios.
* O serviço TLS da plataforma encaminha solicitações para o serviço de CDN do cliente, com base no certificado SSL usado para encerramento, e para o serviço de CDN que hospeda esse domínio.
* O AEM as a Cloud Service aceita certificados SSL curinga para um domínio.

O AEM as a Cloud Service só oferece suporte seguro a sites `https`. Os clientes com vários domínios personalizados não desejam fazer upload de um certificado sempre que adicionam um domínio. Esses clientes se beneficiam de um certificado com vários domínios.

## Requisitos de certificado SSL {#requirements}

* A AEM as a Cloud Service aceita certificados que estejam em conformidade com a política OV (Validação da organização), EV (Validação estendida) ou DV (Validação de domínio). <!-- CQDOC-21758, #2 -->
* Qualquer certificado deve ser um certificado TLS X.509 de uma Autoridade de certificação confiável com uma chave privada RSA de 2048 bits correspondente.
* Certificados autoassinados não são aceitos.

Os certificados OV e EV oferecem informações validadas pela CA. Essas informações ajudam os usuários a avaliar se o proprietário do site, remetente de email ou signatário digital de documentos de código ou PDF pode ser confiável. Os certificados DV não permitem essa verificação de propriedade.

### Formato de certificado SSL gerenciado pelo cliente {#certificate-format}

<!-- CQDOC-21758, #3 -->

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

## Limitação do número de certificados SSL instalados {#limitations}

A qualquer momento, o Cloud Manager permite no máximo 50 certificados SSL instalados. Esses certificados podem ser associados a um ou mais ambientes em todo o programa e também incluir certificados expirados.

Se tiver atingido o limite, revise os certificados e considere excluir os certificados expirados. Ou agrupe vários domínios no mesmo certificado, pois um certificado pode abranger vários domínios (até 100 SANs).

## Saiba mais {#learn-more}

Um usuário com as permissões necessárias pode usar o Cloud Manager para gerenciar certificados SSL para um programa. Consulte os documentos a seguir para obter mais detalhes sobre a utilização desses recursos.

* [Adicionar um certificado SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) <!--CQDOC-21758, #4 -->
* [Gerenciar certificados SSL](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md) <!--CQDOC-21758, #4 -->

