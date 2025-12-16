---
title: Solução de problemas de certificado SSL
description: Saiba como solucionar problemas de certificado SSL identificando causas comuns para que você possa manter conexões seguras.
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
exl-id: 8fb8f708-51a5-46d0-8317-6ce118a70fab
source-git-commit: 7d86ec9cd7cc283082da44111ad897a5aa548f58
workflow-type: tm+mt
source-wordcount: '557'
ht-degree: 31%

---

# Solução de problemas de certificado SSL {#certificate-problems}

Saiba como solucionar problemas de certificado SSL identificando causas comuns para que você possa manter conexões seguras.

+++**Certificado inválido**

## Certificado inválido {#invalid-certificate}

Esse erro ocorre porque o cliente usou uma chave privada criptografada e forneceu a chave no formato DER.

+++

+++**A chave privada precisa estar no formato PKCS 8**

## A chave privada precisa estar no formato PKCS 8 {#pkcs-8}

Esse erro ocorre porque o cliente usou uma chave privada criptografada e forneceu a chave no formato DER.

+++

+++**Ordem correta dos certificados**

## Ordem correta dos certificados {#certificate-order}

O motivo mais comum para uma falha na implantação de um certificado é os certificados intermediários ou em cadeia não estarem na ordem correta.

Os arquivos de certificado intermediários devem terminar com o certificado raiz ou o certificado mais próximo da raiz. Eles devem estar em ordem decrescente, do `main/server` certificado à raiz.

Você pode determinar a ordem dos arquivos intermediários usando o comando a seguir.

```shell
openssl crl2pkcs7 -nocrl -certfile $CERT_FILE | openssl pkcs7 -print_certs -noout
```

Você pode verificar se a chave privada e o certificado `main/server` correspondem usando os comandos a seguir.

```shell
openssl x509 -noout -modulus -in certificate.pem | openssl md5
```

```shell
openssl rsa -noout -modulus -in ssl.key | openssl md5
```

>[!NOTE]
>
>A saída desses dois comandos deve ser exatamente a mesma. Se você não conseguir localizar uma chave privada correspondente ao seu certificado `main/server`, será necessário rechavear o certificado gerando uma nova CSR e/ou solicitando um certificado atualizado do seu fornecedor de SSL.

+++ 

+++**Remover certificados de cliente**

## Remover certificados de cliente {#client-certificates}

Ao adicionar um certificado, se você receber um erro semelhante ao seguinte:

```text
The Subject of an intermediate certificate must match the issuer in the previous certificate. The SKI of an intermediate certificate must match the AKI of the previous certificate.
```

Você provavelmente incluiu o certificado de cliente na cadeia de certificados. Verifique se a cadeia não inclui o certificado de cliente e tente novamente.

+++

+++**Política de certificado**

## Política de certificado {#policy}

Se o seguinte erro for exibido, verifique a política do seu certificado.

```text
Certificate policy must conform with EV or OV, and not DV policy.
```

Os valores de OID incorporados normalmente identificam as políticas de certificados. Extrair o texto de um certificado e pesquisar o OID revela a política do certificado.

Você pode exibir os detalhes do certificado como texto usando o exemplo a seguir como guia.

```text
openssl x509 -in 9178c0f58cb8fccc.pem -text
certificate:
    Data:
        Version: 3 (0x2)
        Serial Number:
            91:78:c0:f5:8c:b8:fc:cc
        Signature Algorithm: sha256WithRSAEncryption
        Issuer: C = US, ST = Arizona, L = Scottsdale, O = "GoDaddy.com, Inc.", OU = http://certs.godaddy.com/repository/, CN = Go Daddy Secure Certificate Authority - G2
        Validity
            Not Before: Nov 10 22:55:36 2021 GMT
            Not After : Dec  6 15:35:06 2022 GMT
        Subject: C = US, ST = Colorado, L = Denver, O = Alexandra Alwin, CN = adobedigitalimpact.com
        Subject Public Key Info:
...
```

O padrão OID no texto define o tipo de política do certificado.

| Padrão | Política | Aceitável no Cloud Manager |
|---|---|---|
| `2.23.140.1.1` | EV | Sim |
| `2.23.140.1.2.2` | OV | Sim |
| `2.23.140.1.2.1` | DV | Não |

Ao `grep` fazer ping nos padrões OID no texto extraído do certificado, é possível confirmar a política do certificado.

```shell
# "EV Policy"
openssl x509 -in certificate.pem -text grep "Policy: 2.23.140.1.1" -B5

# "OV Policy"
openssl x509 -in certificate.pem -text grep "Policy: 2.23.140.1.2.2" -B5

# "DV Policy - Not Accepted"
openssl x509 -in certificate.pem -text grep "Policy: 2.23.140.1.2.1" -B5
```

+++

+++Validade do certificado

## Validade do certificado {#validity}

O Cloud Manager espera que o certificado SSL seja válido por pelo menos 90 dias a partir da data atual. Verifique a validade da cadeia de certificados.

+++

+++Certificado SAN incorreto aplicado ao meu domínio

## Certificado SAN incorreto aplicado ao meu domínio {#wrong-san-cert}

Digamos que você queira vincular `dev.yoursite.com` e `stage.yoursite.com` ao seu ambiente de não produção e `prod.yoursite.com` ao seu ambiente de produção.

Para configurar a CDN para esses domínios, você precisa de um certificado instalado para cada um, para instalar um certificado que cubra o `*.yoursite.com` para seus domínios de não produção e outro que também cubra o `*.yoursite.com` para seus domínios de produção.

Essa configuração é válida. No entanto, quando você atualiza um dos certificados, ambos ainda abrangem a mesma entrada SAN. Como resultado, a CDN instala o certificado mais recente em todos os domínios aplicáveis, o que pode parecer inesperado.

Embora esse cenário possa ser inesperado, não é um erro e é o comportamento padrão do CDN subjacente. Se você tiver dois ou mais certificados SAN que abranjam a mesma entrada de domínio SAN, a CDN instalará o certificado atualizado mais recentemente para esse domínio. Essa situação acontece mesmo quando outro certificado já cobre a mesma entrada de domínio.

+++
