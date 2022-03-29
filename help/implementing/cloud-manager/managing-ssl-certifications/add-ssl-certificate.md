---
title: Adicionar um certificado SSL
description: Saiba como adicionar seu próprio certificado SSL usando as ferramentas de autoatendimento do Cloud Manager.
exl-id: 104b5119-4a8b-4c13-99c6-f866b3c173b2
source-git-commit: 2c87d5fb33b83ca77b97391e4b0baaf38f8dd026
workflow-type: tm+mt
source-wordcount: '592'
ht-degree: 2%

---

# Adicionar um certificado SSL {#adding-an-ssl-certificate}

Saiba como adicionar seu próprio certificado SSL usando as ferramentas de autoatendimento do Cloud Manager.

>[!TIP]
>
>Um certificado pode levar alguns dias para ser provisionado. O Adobe recomenda, portanto, que o certificado seja provisionado com bastante antecedência.

## Formato do certificado {#certificate-format}

Os arquivos de certificado SSL devem estar no formato PEM para serem instalados com o Cloud Manager. Extensões de arquivo comuns do formato PEM incluem `.pem,` .`crt`, `.cer`, e `.cert`.

O seguinte `openssl` comandos podem ser usados para converter certificados não PEM.

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

## Adicionar um certificado {#adding-a-cert}

Siga estas etapas para adicionar um certificado usando o Cloud Manager.

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriados.

1. Navegar para **Ambientes** da tela **Visão geral** página.

1. Clique em **Certificados SSL** no painel de navegação esquerdo. Uma tabela com detalhes de quaisquer certificados SSL existentes será exibida na tela principal.

   ![Adicionar um certificado SSL](/help/implementing/cloud-manager/assets/ssl/ssl-cert-1.png)

1. Clique em **Adicionar certificado SSL** para abrir **Adicionar certificado SSL** caixa de diálogo.

   * Insira um nome para o certificado em **Nome do certificado**.
      * Isso é apenas para fins informativos e pode ser qualquer nome que ajude você a fazer referência ao certificado facilmente.
   * Cole o **Certificado**, **Chave privada** e **Cadeia de certificados** nos respectivos campos.
      * Você pode usar o ícone de colar à direita da caixa de entrada.
      * Todos os três campos são obrigatórios.

   ![Caixa de diálogo Adicionar certificado SSL](/help/implementing/cloud-manager/assets/ssl/ssl-cert-02.png)

   * Quaisquer erros detectados serão exibidos.
      * Você deve corrigir todos os erros antes que o certificado possa ser salvo.
      * Consulte a [Erros de certificado](#certificate-errors) para saber mais sobre como lidar com erros comuns.


1. Clique em **Salvar** para salvar seu certificado.

Depois de salvo, você verá seu certificado exibido como uma nova linha na tabela.

![Certificado SSL salvo](/help/implementing/cloud-manager/assets/ssl/ssl-cert-3.png)

>[!NOTE]
>
>Um usuário deve ser membro do **Proprietário da empresa** ou **Gerenciador de implantação** para instalar um certificado SSL no Cloud Manager.

## Erros de certificado {#certificate-errors}

Certos erros podem surgir se um certificado não for instalado corretamente ou atender aos requisitos do Cloud Manager.

### Política de Certificado {#certificate-policy}

Se você vir o seguinte erro, verifique a política do seu certificado.

```text
Certificate policy must conform with EV or OV, and not DV policy.
```

Normalmente, as políticas de certificados são identificadas por valores OID incorporados. A saída de um certificado para o texto e a pesquisa do OID revelarão a política do certificado.

Você pode exibir seus detalhes do certificado como texto usando o exemplo a seguir como guia.

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

Por `grep`Ao fazer o ping dos padrões OID no texto do certificado de saída, é possível confirmar a política de certificados.

```shell
# "EV Policy"
openssl x509 -in certificate.pem -text grep "Policy: 2.23.140.1.1" -B5

# "OV Policy"
openssl x509 -in certificate.pem -text grep "Policy: 2.23.140.1.2.2" -B5

# "DV Policy - Not Accepted"
openssl x509 -in certificate.pem -text grep "Policy: 2.23.140.1.2.1" -B5
```

### Corrija a ordem do certificado {#correct-certificate-order}

O motivo mais comum para uma implantação de certificado falhar é que os certificados intermediários ou em cadeia não estão na ordem correta.

Os arquivos de certificado intermediários devem terminar com o certificado raiz ou o certificado mais próximo da raiz. Eles devem estar em ordem decrescente da variável `main/server` certificado para a raiz.

Você pode determinar a ordem dos arquivos intermediários usando o seguinte comando.

```shell
openssl crl2pkcs7 -nocrl -certfile $CERT_FILE | openssl pkcs7 -print_certs -noout
```

Você pode verificar se a chave privada e `main/server` a correspondência do certificado usando os seguintes comandos.

```shell
openssl x509 -noout -modulus -in certificate.pem | openssl md5
```

```shell
openssl rsa -noout -modulus -in ssl.key | openssl md5
```

>[!NOTE]
>
>A saída desses dois comandos deve ser exatamente a mesma. Se você não conseguir localizar uma chave privada correspondente para sua `main/server` certificado, você precisará rechavear o certificado gerando uma nova CSR e/ou solicitando um certificado atualizado de seu fornecedor SSL.

### Datas de validade do certificado {#certificate-validity-dates}

O Cloud Manager espera que o certificado SSL seja válido por pelo menos 90 dias a partir da data atual. Você deve verificar a validade da cadeia de certificados.
