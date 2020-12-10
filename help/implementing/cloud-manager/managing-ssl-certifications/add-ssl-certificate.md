---
title: Adicionar um certificado SSL - Gerenciar certificados SSL
description: Adicionar um certificado SSL - Gerenciar certificados SSL
translation-type: tm+mt
source-git-commit: 88ef9265b40f64f2229e37e5f8ca02959e8d9ce2
workflow-type: tm+mt
source-wordcount: '512'
ht-degree: 0%

---


# Adicionando um certificado SSL {#adding-an-ssl-certificate}

>[!NOTE]
>AEM como Cloud Service só aceitará certificados OV(Organization Validation) ou EV(Extended Validation). Certificados DV(Domain Validation) não serão aceitos.

Um certificado demora alguns dias para ser provisionado e recomenda-se que o certificado seja provisionado com meses de antecedência. Consulte [Obtendo um Certificado SSL](/help/implementing/cloud-manager/managing-ssl-certifications/get-ssl-certificate.md) para obter mais detalhes.

## Formato de certificado {#certificate-format}

Os arquivos SSL devem estar no formato PEM para serem instalados no Cloud Manager. As extensões de arquivo comuns que estão no formato PEM incluem `.pem,`.`crt`,  `.cer`e  `.cert`.

Siga as etapas abaixo para converter o formato dos arquivos SSL em PEM:

1. Converter PFX em PEM

`openssl pkcs12 -in certificate.pfx -out certificate.cer -nodes`

1. Converter P7B em PEM

`openssl pkcs7 -print_certs -in certificate.p7b -out certificate.cer`

1. Converter DER em PEM

`openssl x509 -inform der -in certificate.cer -out certificate.pem`

## Adicionando seu Certificado {#adding-certificate}

>[!NOTE]
>* Um usuário deve estar na função Proprietário de Negócios ou Gerenciador de Implantação para instalar um certificado SSL no Cloud Manager.
>* A qualquer momento, o Cloud Manager permitirá um máximo de 10 certificados SSL que podem ser associados a um ou mais ambientes em seu Programa, mesmo se um certificado expirar. No entanto, a interface do usuário do Cloud Manager permitirá que até 50 certificados SSL sejam instalados no programa com essa restrição.


Siga as etapas abaixo para adicionar um certificado:

1. Faça logon no Cloud Manager.
1. Navegue até a tela **Ambientes** da página **Visão geral**.
1. Clique em **Certificados SSL** no menu de navegação esquerdo. Uma tabela com detalhes de quaisquer certificados SSL existentes será exibida nessa tela.

   ![](/help/implementing/cloud-manager/assets/ssl/ssl-cert-1.png)
1. Selecione o botão **Adicionar certificado** para abrir a caixa de diálogo **Adicionar certificado SSL**.

   ![](/help/implementing/cloud-manager/assets/ssl/ssl-cert-2.png)
   1. Insira um nome para o certificado em **Nome do Certificado**. Esse pode ser qualquer nome que o ajude a referenciar seu certificado facilmente.
   1. Cole o **Certificado**, **Chave privada** e **Cadeia de certificados** nos respectivos campos. Use o ícone colar à direita da caixa de entrada.

      >[!NOTE]
      >Os três campos não são opcionais e devem ser incluídos.
1. Clique em **Salvar** para enviar seu certificado. Será exibido como uma nova linha na tabela.
   >[!NOTE]
   >Quaisquer erros detectados serão exibidos. Você deve corrigir todos os erros antes que seu certificado possa ser salvo. Consulte [Erros de Certificado](#certificate-errors) para saber mais sobre como lidar com erros comuns.

## Erros de certificado {#certificate-errors}

### Ordem de certificado correta {#correct-certificate-order}

O motivo mais comum para uma implantação de certificado falhar é que os certificados intermediários ou de cadeia não estão na ordem correta. Especificamente, os arquivos de certificado intermediários devem terminar com o certificado raiz ou mais próximo à raiz e estar em ordem decrescente do certificado `main/server` até a raiz.

Você pode determinar a ordem dos arquivos intermediários usando o seguinte comando:

`openssl crl2pkcs7 -nocrl -certfile $CERT_FILE | openssl pkcs7 -print_certs -noout`

Você pode verificar se a chave privada e o certificado `main/server` correspondem usando os seguintes comandos:

`openssl x509 -noout -modulus -in certificate.pem | openssl md5`

`openssl rsa -noout -modulus -in ssl.key | openssl md5`

>[!NOTE]
>A saída desses dois comandos deve ser exatamente a mesma. Se não conseguir localizar uma chave privada correspondente ao seu certificado `main/server`, será necessário recodificar o certificado gerando um novo CSR e/ou solicitando um certificado atualizado do seu fornecedor SSL.

### Datas de validade do certificado {#certificate-validity-dates}

O Cloud Manager espera que o certificado SSL seja válido por pelo menos 90 dias no futuro

Verifique a validade da cadeia de certificados.
