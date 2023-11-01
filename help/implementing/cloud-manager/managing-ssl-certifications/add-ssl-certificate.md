---
title: Adicionar um certificado SSL
description: Saiba como adicionar seu próprio certificado SSL usando as ferramentas de autoatendimento do Cloud Manager.
exl-id: 104b5119-4a8b-4c13-99c6-f866b3c173b2
source-git-commit: 6db3565fefe4c826bb40695d0fa84368fd3f283b
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 88%

---

# Adicionar um certificado SSL {#adding-an-ssl-certificate}

Saiba como adicionar seu próprio certificado SSL usando as ferramentas de autoatendimento do Cloud Manager.

>[!TIP]
>
>Um certificado pode levar alguns dias para ser provisionado. A Adobe recomenda que o certificado seja provisionado com bastante antecedência.

## Requisitos de certificado {#certificate-requirements}

Revise a seção **Requisitos de certificado** do documento [Introdução ao gerenciamento de certificados SSL](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md#requirements) para garantir que o certificado que você deseja adicionar seja compatível com o AEM as a Cloud Service.

## Adição de um certificado {#adding-a-cert}

Siga estas etapas para adicionar um certificado usando o Cloud Manager.

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriado.

1. Acesse a tela **Ambientes** a partir da página **Visão geral**.

1. Clique em **Certificados SSL** no painel de navegação esquerdo. Uma tabela com detalhes de todos os certificados SSL existentes é exibida na tela principal.

   ![Adição de um certificado SSL](/help/implementing/cloud-manager/assets/ssl/ssl-cert-1.png)

1. Clique em **Adicionar certificado SSL** para abrir a caixa de diálogo **Adicionar certificado SSL**.

   * Insira um nome para o certificado em **Nome do certificado**.
      * Isso é apenas para fins de informação e pode ser qualquer nome que o ajude a identificar o certificado com facilidade.
   * Cole os valores de **Certificado**, **Chave privada** e **Cadeia de certificado** nos respectivos campos. Todos esses três campos são obrigatórios.

   ![Caixa de diálogo Adicionar certificado SSL](/help/implementing/cloud-manager/assets/ssl/ssl-cert-02.png)

   * Todos os erros detectados são exibidos.
      * É necessário corrigir todos eles para salvar o certificado.
      * Consulte a seção [Erros de certificado](#certificate-errors) para saber mais sobre como resolver erros comuns.

1. Clique em **Salvar** para salvar o certificado.

Depois de salvo, o certificado será exibido como uma nova linha na tabela.

![Certificado SSL salvo](/help/implementing/cloud-manager/assets/ssl/ssl-cert-3.png)

>[!NOTE]
>
>É necessário ser um membro com a função **Proprietário da empresa** ou **Gerente de implantação** para instalar um certificado SSL no Cloud Manager.

## Erros de certificado {#certificate-errors}

Certos erros podem ocorrer se um certificado não for instalado corretamente ou atender aos requisitos do Cloud Manager.

### Política de certificado {#certificate-policy}

Se o seguinte erro for exibido, verifique a política do seu certificado.

```text
Certificate policy must conform with EV or OV, and not DV policy.
```

Normalmente, as políticas de certificados são identificadas por valores OID incorporados. Extrair o texto de um certificado e pesquisar o OID revelarão a política do certificado.

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

### Ordem correta de certificados {#correct-certificate-order}

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
>A saída desses dois comandos deve ser exatamente a mesma. Se não conseguir localizar uma chave privada correspondente para seu `main/server` , você precisará rechavear o certificado gerando uma nova CSR e/ou solicitando um certificado atualizado de seu fornecedor de SSL.

### Datas de validade do certificado {#certificate-validity-dates}

O Cloud Manager espera que o certificado SSL seja válido por pelo menos 90 dias a partir da data atual. Você deve verificar a validade da cadeia de certificados.
