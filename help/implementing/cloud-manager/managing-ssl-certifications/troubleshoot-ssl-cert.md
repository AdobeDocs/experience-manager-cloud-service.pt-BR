---
title: Solução de problemas de erros de certificado SSL
description: Saiba como solucionar erros de certificado SSL identificando causas comuns para que você possa manter conexões seguras.
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: ff8c7fb21b4d8bcf395d28c194a7351281eef45b
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 46%

---


# Solução de problemas de erros de certificado SSL {#certificate-errors}

Alguns erros podem ocorrer se um certificado não for instalado corretamente ou não atender aos requisitos do Cloud Manager.

+++**Certificado inválido**

Esse erro ocorre porque o cliente adicionou uma chave privada criptografada e usou uma chave privada formatada com DER.

+++

+++**A chave privada precisa estar no formato PKCS 8**

Esse erro ocorre porque o cliente adicionou uma chave privada criptografada e usou uma chave privada formatada com DER.

+++

+++**Ordem correta dos certificados**

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

Ao adicionar um certificado, se você receber um erro semelhante ao seguinte:

```text
The Subject of an intermediate certificate must match the issuer in the previous certificate. The SKI of an intermediate certificate must match the AKI of the previous certificate.
```

Você provavelmente incluiu o certificado de cliente na cadeia de certificados. Verifique se a cadeia não inclui o certificado de cliente e tente novamente.

+++

+++**Política de certificado**

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

+++**Datas de validade do certificado**

O Cloud Manager espera que o certificado SSL seja válido por pelo menos 90 dias a partir da data atual. Verifique a validade da cadeia de certificados.

+++