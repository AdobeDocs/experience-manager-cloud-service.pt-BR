---
title: Introdução aos certificados SSL
description: Saiba mais sobre as ferramentas de autoatendimento que a Cloud Manager fornece para instalar e gerenciar certificados SSL.
exl-id: 0d41723c-c096-4882-a3fd-050b7c9996d8
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: fdd86b966f0480c00b7cd975d63a48b82fb1d027
workflow-type: tm+mt
source-wordcount: '1160'
ht-degree: 17%

---


# Introdução aos certificados SSL{#introduction}

Saiba mais sobre as ferramentas de autoatendimento que a Cloud Manager fornece para instalar e gerenciar certificados SSL (Secure Socket Layer).

>[!CONTEXTUALHELP]
>id="aemcloud_golive_sslcert"
>title="Gerenciar certificados SSL"
>abstract="Saiba como o Cloud Manager tem ferramentas de autoatendimento para instalar e gerenciar certificados SSL a fim de proteger o site para seus usuários. O Cloud Manager usa um serviço TLS para gerenciar certificados SSL e chaves privadas de propriedade de clientes e obtidas de autoridades de certificação terceirizadas."
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
| A | **[Certificado SSL gerenciado pela Adobe (DV)](#adobe-managed)** | O Cloud Manager permite que os usuários configurem os certificados DV (Validação de domínio) fornecidos pela Adobe para configuração rápida do domínio. |
| B | **[Certificado SSL gerenciado pelo cliente (OV/EV)](#customer-managed)** | A Cloud Manager oferece um serviço TLS (Transport Layer Security) para permitir que você gerencie certificados SSL OV e EV que você possui e chaves privadas de Autoridades de Certificação de terceiros, como *Vamos Criptografar*. |

Ambos os modelos oferecem os seguintes recursos gerais para gerenciar seus certificados:

* Cada ambiente do Cloud Manager pode usar vários certificados.
* Uma chave privada pode emitir vários certificados SSL.
* O serviço TLS da plataforma encaminha solicitações para o serviço de CDN do cliente, com base no certificado SSL usado para encerramento, e para o serviço de CDN que hospeda esse domínio.

>[!IMPORTANT]
>
>[Para adicionar e associar um domínio personalizado a um ambiente](/help/implementing/cloud-manager/custom-domain-names/introduction.md), é necessário ter um certificado SSL válido que cubra o domínio.

### Certificados SSL gerenciados pela Adobe (DV) {#adobe-managed}

Os certificados DV são o nível mais básico da certificação SSL e são frequentemente usados para fins de teste ou para proteger sites com criptografia básica. Os certificados DV estão disponíveis em [programas de produção e programas de sandbox](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md).

Após a criação do certificado DV, o Adobe o renova automaticamente a cada três meses, a menos que ele seja excluído.

>[!IMPORTANT]
>
>Se seu ambiente usar certificados SSL (DV) com uma validação baseada em CNAME, esteja ciente de que a remoção do registro CNAME antes da renovação automática do certificado pode causar falha na renovação. A remoção pode resultar na expiração do certificado e na interrupção do serviço. Para evitar esse problema, verifique se o registro CNAME permanece em vigor durante o processo de renovação completo. O processo de renovação depende da presença do registro CNAME para a validação da propriedade do domínio.

### Certificados SSL gerenciados pelo cliente (OV/EV) {#customer-managed}

Os certificados OV e EV oferecem informações validadas pela CA. Essas informações ajudam os usuários a avaliar se o proprietário do site, remetente de email ou signatário digital de código ou documentos do PDF podem ser confiáveis. Os certificados DV não permitem essa verificação de propriedade.

OV e EV também oferecem esses recursos em relação aos certificados DV na Cloud Manager.

* Vários ambientes podem usar um certificado OV/EV. Ou seja, pode ser adicionado uma vez, mas usado várias vezes.
* Cada certificado OV/EV normalmente contém vários domínios.
* A Cloud Manager aceita certificados OV/EV curingas para um domínio.

>[!TIP]
>
>Se você tiver vários domínios personalizados, talvez não queira carregar um certificado sempre que adicionar um novo domínio. Nesse caso, você pode se beneficiar com a obtenção de um único certificado que abrange vários domínios.

#### Requisitos para certificados SSL OV/EV gerenciados pelo cliente {#requirements}

Se você optar por adicionar seu próprio certificado SSL gerenciado pelo cliente, ele deverá atender aos seguintes requisitos atualizados:

* Os certificados de Validação de Domínio (DV) e os certificados autoassinados não são compatíveis.
* O certificado deve estar em conformidade com as políticas OV (Validação da organização) ou EV (Validação estendida).
* O certificado deve ser um certificado TLS X.509 emitido por uma CA confiável.
* Os tipos de chave criptográfica compatíveis incluem o seguinte:

   * Suporte padrão RSA de 2048 bits.
Chaves RSA maiores que 2048 bits (como chaves RSA de 3072 bits ou 4096 bits) não são suportadas no momento.
   * Chaves de Curva Elíptica (EC) `prime256v1` (`secp256r1`) e `secp384r1`
   * Certificados ECDSA (Elliptic Curve Digital Signature Algorithm). Esses certificados são recomendados pela Adobe em relação à RSA para melhorar o desempenho, a segurança e a eficiência.

* Os certificados devem estar formatados corretamente para serem aprovados na validação. As chaves privadas devem estar no formato `PKCS#8`.

>[!NOTE]
>Se sua organização exigir conformidade usando chaves RSA de 3072 bits, a alternativa recomendada pela Adobe é usar certificados ECDSA (`secp256r1` ou `secp384r1`).


#### Práticas recomendadas para gerenciamento de certificados

* **Evitar sobreposição de certificados:**

   * Para garantir um gerenciamento de certificados simples, evite implantar certificados sobrepostos que correspondam ao mesmo domínio. Por exemplo, ter um certificado curinga (*.example.com) ao lado de um certificado específico (dev.example.com) pode causar confusão.
   * A camada TLS prioriza o certificado mais específico e implantado recentemente.

  Exemplos de cenários:

   * &quot;Certificado de Desenvolvimento&quot; abrange `dev.example.com` e é implantado como um mapeamento de domínio para `dev.example.com`.
   * &quot;Certificado de Preparo&quot; abrange `stage.example.com` e é implantado como um mapeamento de domínio para `stage.example.com`.
   * Se o &quot;Certificado de Preparo&quot; for implantado/atualizado *após* o &quot;Certificado de Desenvolvimento&quot;, ele também servirá solicitações para `dev.example.com`.

     Para evitar esses conflitos, verifique se os certificados têm cuidadosamente o escopo de seus domínios pretendidos.

* **Certificados curinga:**

  Embora haja suporte a certificados curingas (por exemplo, `*.example.com`), eles só devem ser usados quando necessário. Em casos de sobreposição, o certificado mais específico tem prioridade. Por exemplo, o certificado específico serve `dev.example.com` em vez do curinga (`*.example.com`).

* **Validação e solução de problemas:**
Antes de tentar instalar um certificado com o Cloud Manager, a Adobe recomenda validar a integridade do certificado localmente usando ferramentas como o `openssl`. Por exemplo,

  `openssl verify -untrusted intermediate.pem certificate.pem`


<!--
>[!NOTE]
>
>If two certificates cover the same domain are installed, the one that is more exact is applied.
>
>For example, if your domain is `dev.adobe.com` and you have one certificate for `*.adobe.com` and another for `dev.adobe.com`, the more specific one (`dev.adobe.com`) is used.
-->

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

## Limitação do número de certificados SSL instalados {#limitations}

A qualquer momento, a Cloud Manager oferece suporte a até 50 certificados instalados. Esses certificados podem ser associados a um ou mais ambientes em todo o programa e também incluir certificados expirados.

Se tiver atingido o limite, revise os certificados e considere excluir os certificados expirados. Ou agrupe vários domínios no mesmo certificado, pois um certificado pode abranger vários domínios (até 100 SANs).

## Saiba mais {#learn-more}

Um usuário com as permissões necessárias pode usar o Cloud Manager para gerenciar certificados SSL para um programa. Consulte os documentos a seguir para obter mais detalhes sobre a utilização desses recursos.

* [Adicionar um certificado SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) <!--CQDOC-21758, #4 -->
* [Gerenciar certificados SSL](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md) <!--CQDOC-21758, #4 -->

