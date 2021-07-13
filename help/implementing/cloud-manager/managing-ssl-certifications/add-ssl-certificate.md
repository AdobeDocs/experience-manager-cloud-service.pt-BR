---
title: Adicionar um certificado SSL - Gerenciar certificados SSL
description: Adicionar um certificado SSL - Gerenciar certificados SSL
exl-id: 104b5119-4a8b-4c13-99c6-f866b3c173b2
source-git-commit: 3b4a9d7c04a5f4feecad0f34c27a894c187152e7
workflow-type: tm+mt
source-wordcount: '578'
ht-degree: 0%

---

# Adicionar um certificado SSL {#adding-an-ssl-certificate}

>[!NOTE]
>AEM como Cloud Service só aceitará certificados OV (Validação da Organização) ou EV (Validação Estendida). Certificados DV (Validação de Domínio) não serão aceitos. Além disso, qualquer certificado deve ser um certificado TLS X.509 de uma autoridade de certificação (CA) confiável com uma chave privada RSA de 2048 bits correspondente. AEM como Cloud Service aceitará certificados SSL curinga para um domínio.

Um certificado leva alguns dias para ser provisionado e é recomendável que ele seja provisionado com meses de antecedência. Consulte [Obter um certificado SSL](/help/implementing/cloud-manager/managing-ssl-certifications/get-ssl-certificate.md) para obter mais detalhes.

## Formato do certificado {#certificate-format}

Os arquivos SSL devem estar no formato PEM para serem instalados no Cloud Manager. Extensões de arquivo comuns que estão no formato PEM incluem `.pem,` .`crt`,  `.cer`, e  `.cert`.

Siga as etapas abaixo para converter o formato de seus arquivos SSL em PEM:

* Converter PFX em PEM

   `openssl pkcs12 -in certificate.pfx -out certificate.cer -nodes`

* Converter P7B em PEM

   `openssl pkcs7 -print_certs -in certificate.p7b -out certificate.cer`

* Converter DER em PEM

   `openssl x509 -inform der -in certificate.cer -out certificate.pem`

## Considerações importantes {#important-considerations}

* Um usuário deve estar na função Proprietário comercial ou Gerente de implantação para instalar um certificado SSL no Cloud Manager.

* A qualquer momento, o Cloud Manager permitirá no máximo 10 certificados SSL que podem ser associados a um ou mais ambientes em todo o Programa, mesmo que um certificado tenha expirado. No entanto, a interface do usuário do Cloud Manager permitirá que até 50 certificados SSL sejam instalados no programa com essa restrição. Normalmente, um certificado pode abranger vários domínios (até 100 SANs), portanto, considere agrupar vários domínios no mesmo certificado para permanecer dentro desse limite.


## Adicionar um certificado {#adding-a-cert}

Siga as etapas abaixo para adicionar um certificado:

1. Faça logon no Cloud Manager.
1. Navegue até a tela **Ambientes** a partir da página **Visão geral**.
1. Clique em **Certificados SSL** no menu de navegação esquerdo. Uma tabela com detalhes de quaisquer certificados SSL existentes será exibida nessa tela.

   ![](/help/implementing/cloud-manager/assets/ssl/ssl-cert-1.png)

1. Clique em **Adicionar certificado SSL** para abrir a caixa de diálogo **Adicionar certificado SSL**.

   * Insira um nome para o certificado em **Nome do certificado**. Pode ser qualquer nome que ajude você a fazer referência ao certificado facilmente.
   * Cole o **Certificado**, **Chave privada** e **Cadeia de certificados** nos respectivos campos. Use o ícone de colar à direita da caixa de entrada.
Todos os três campos não são opcionais e devem ser incluídos.

      ![](/help/implementing/cloud-manager/assets/ssl/ssl-cert-02.png)


      >[!NOTE]
      >Quaisquer erros detectados serão exibidos. Você deve corrigir todos os erros antes que o certificado possa ser salvo. Consulte [Erros de certificado](#certificate-errors) para saber mais sobre como lidar com erros comuns.

1. Clique em **Save** para enviar seu certificado. Você o verá como uma nova linha na tabela.

   ![](/help/implementing/cloud-manager/assets/ssl/ssl-cert-3.png)

## Erros de certificado {#certificate-errors}

### Corrija a ordem do certificado {#correct-certificate-order}

O motivo mais comum para uma implantação de certificado falhar é que os certificados intermediários ou em cadeia não estão na ordem correta. Especificamente, os arquivos de certificado intermediários devem terminar com o certificado raiz ou o certificado mais próximo da raiz e estar em uma ordem decrescente do certificado `main/server` para a raiz.

Você pode determinar a ordem dos arquivos intermediários usando o seguinte comando:

`openssl crl2pkcs7 -nocrl -certfile $CERT_FILE | openssl pkcs7 -print_certs -noout`

Você pode verificar se a chave privada e o certificado `main/server` correspondem usando os seguintes comandos:

`openssl x509 -noout -modulus -in certificate.pem | openssl md5`

`openssl rsa -noout -modulus -in ssl.key | openssl md5`

>[!NOTE]
>A saída desses dois comandos deve ser exatamente a mesma. Se não for possível localizar uma chave privada correspondente ao seu certificado `main/server`, será necessário rechavear o certificado gerando uma nova CSR e/ou solicitando um certificado atualizado de seu fornecedor SSL.

### Datas de validade do certificado {#certificate-validity-dates}

O Cloud Manager espera que o certificado SSL seja válido por, pelo menos, 90 dias no futuro. Você deve verificar a validade da cadeia de certificados.
