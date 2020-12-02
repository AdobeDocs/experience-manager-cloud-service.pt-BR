---
title: Adicionar um certificado SSL - Gerenciar certificados SSL
description: Adicionar um certificado SSL - Gerenciar certificados SSL
translation-type: tm+mt
source-git-commit: e27e5302802e68dce2a5713626950896bb35420a
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 0%

---


# Adicionando um certificado SSL {#adding-an-ssl-certificate}

>[!NOTE]
>Um certificado demora alguns dias para ser provisionado e recomenda-se que o certificado seja provisionado com meses de antecedência. Ir para Como obter um certificado SSL para saber mais.INSERT LINK

## Formato de certificado {#certificate-format}

Os arquivos SSL devem estar no formato PEM para serem instalados no Cloud Manager. As extensões de arquivo comuns que estão no formato PEM incluem .pem, .crt, .cer e .cert.

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
>* A qualquer momento, o Cloud Manager permitirá um máximo de 5 certificados SSL que podem ser associados a um ou mais ambientes em seu Programa, mesmo se um certificado expirar. No entanto, a interface do usuário do Cloud Manager permitirá que até 50 certificados SSL sejam instalados no programa com essa restrição.


1. Faça logon no Cloud Manager.
1. Navegue até a tela Ambientes na página Visão geral.
1. Navegue até a tela Certificados SSL no menu de navegação esquerdo. Uma tabela com detalhes de quaisquer certificados SSL existentes será exibida nesta tela.INSERIR IMAGEM
1. Selecione o botão **Adicionar certificado** para iniciar um assistente.
1. Digite um nome para o seu certificado. Esse pode ser qualquer nome que o ajude a referenciar seu certificado facilmente.
1. Cole o conteúdo Certificado, Chave privada e Cadeia em seus respectivos campos. Use o ícone colar à direita da caixa de entrada.
1. Selecione **Salvar**.

   >[!NOTE]
   >Quaisquer erros detectados serão exibidos. Você deve corrigir todos os erros antes que seu certificado possa ser salvo. Consulte Erros de link INSERT de certificado para saber mais sobre como lidar com erros comuns.

   Depois de enviar seu certificado, ele será exibido como uma nova linha na tabela.

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
