---
title: Adicionar um certificado SSL
description: Saiba como adicionar seu próprio certificado SSL ou certificado DV (Validação de domínio) usando as ferramentas de autoatendimento do Cloud Manager.
exl-id: 104b5119-4a8b-4c13-99c6-f866b3c173b2
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: fcde1f323392362d826f9b4a775e468de9550716
workflow-type: tm+mt
source-wordcount: '966'
ht-degree: 21%

---


# Adicionar um certificado SSL

Saiba como adicionar um certificado SSL gerenciado pelo cliente ou um certificado DV (Validação de domínio) gerado e gerenciado por Adobe usando as ferramentas de autoatendimento da Cloud Manager.


## Adicionar um certificado SSL ou DV {#adding-an-ssl-certificate}

Um certificado pode levar alguns dias para ser provisionado. Assim, a Adobe recomenda que o certificado seja provisionado bem antes de qualquer prazo ou data de ativação.

Certifique-se de revisar os **Requisitos do certificado** em [Introdução ao Gerenciamento de Certificados SSL](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md#requirements) para verificar se a AEM as a Cloud Service oferece suporte ao certificado que você deseja adicionar.

O usuário deve ser membro da função **Proprietário da empresa** ou **Gerente de implantação** para concluir esta tarefa.

>[!NOTE]
>
>Os clientes não têm permissão para carregar certificados DV (Validação de domínio).

**Para adicionar um certificado SSL ou DV:**

1. Faça logon no Cloud Manager, em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/), e selecione a organização apropriada.

1. No console **[Meus Programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, selecione o programa.

1. Na página **Visão geral**, navegue até a tela **Ambientes**.

1. No painel de navegação esquerdo, em **Serviços**, clique em **Certificados SSL**. Se você não vir o painel de navegação esquerdo como visto na imagem a seguir, talvez seja necessário clicar no ícone de hambúrguer no canto superior esquerdo.

   ![Adicionando um certificado SSL](/help/implementing/cloud-manager/assets/ssl/ssl-cert-add.png)

1. Próximo ao canto superior direito da página, clique em **Adicionar certificado SSL**.

1. Na caixa de diálogo **Adicionar certificado SSL**, com base em seu caso de uso específico, execute um dos procedimentos a seguir:

   | Caso de uso | Etapas |
   | --- | --- |
   | **Adicionar um DV (certificado gerenciado por Adobe)** | **Para adicionar um DV (certificado gerenciado por Adobe):**<br> a. Selecione o tipo de certificado **Adobe gerenciado (DV)**.<br>![Adicionar um certificado DV](/help/implementing/cloud-manager/assets/ssl/add-dv-certificate.png)<br>b. Na lista suspensa **Selecionar domínios**, selecione um ou mais domínios que deseja associar ao certificado DV.<br>Nenhum domínio para selecionar? Em caso afirmativo, significa que você deve adicionar um domínio personalizado. Consulte [Adicionar um domínio personalizado](#add-custom-domain). Quando terminar de adicionar um nome de domínio personalizado, retorne a este tópico e comece na etapa 1 novamente.<br>d Continue com a etapa 7. |
   | **Adicionar um certificado gerenciado pelo cliente (OV/EV)** | **Para adicionar um certificado gerenciado pelo cliente (OV/EV):**<br> a. Selecione o tipo de certificado **Gerenciado pelo cliente (OV/EV)**.<br>b. No campo **Nome do certificado**, digite um nome para o certificado. Este campo é apenas para fins informativos e pode ser qualquer nome que o ajude a identificar o certificado com facilidade.<br>c Nos campos **Certificado**, **Chave privada** e **Cadeia de certificados**, cole os valores necessários nos respectivos campos.<br>![Caixa de diálogo Adicionar certificado SSL](/help/implementing/cloud-manager/assets/ssl/ssl-cert-02.png)<br>Todos os erros detectados nos valores são exibidos. Antes de salvar o certificado, é necessário corrigir todos os erros. Consulte [Erros de Certificado](#certificate-errors) para saber mais sobre como solucionar erros comuns.<br>d Continue com a etapa 7. |

<!--
    **Add an SSL certificate:**
    1. Select the certificate type **Customer managed (OV/EV)**.
    1. In **Certificate name** field, enter a name for your certificate. This field is for informational purposes only and can be any name that helps you reference your certificate easily.
    1. In the **Certificate**, **Private key**, and **Certificate chain** fields, paste the required values into their respective fields.

        ![Add SSL certificate dialog box](/help/implementing/cloud-manager/assets/ssl/ssl-cert-02.png)
  
    Any detected errors in values are displayed. Before you can save your certificate, you must address all errors. See [Certificate errors](#certificate-errors) to learn more about troubleshooting common errors.

    **Add a DV certificate:**
    1. Select the certificate type **Adobe managed (DV)**.

        ![Adding a DC certificate](/help/implementing/cloud-manager/assets/ssl/add-dv-certificate.png)

    1. In the **Select domains** drop-down list, select one or more domains that you want associated with the DV certificate.

        No domains to select? If so, it means that you must add a custom domain. See [Add a custom domain](#add-custom-domain). When you are finished, resume the steps from the beginning again. -->

1. No canto inferior direito da caixa de diálogo, clique em **Salvar**.

   Depois que o certificado for emitido com êxito, ele exibirá uma marca de seleção verde, como visto na imagem acima

   ![Certificado DV emitido](assets/issued-dv-certificate.png)

### Adicionar um domínio personalizado {#add-custom-domain}

Antes de adicionar um certificado de Domínio Validado (DV) gerado e gerenciado por Adobe, primeiro adicione um domínio personalizado. O processo para fazer isso é quase o mesmo detalhado em [Introdução a nomes de domínio personalizados](/help/implementing/cloud-manager/custom-domain-names/introduction.md) e [Adicionar um nome de domínio personalizado](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md). No entanto, essa funcionalidade agora está ligeiramente expandida, conforme descrito abaixo.

1. Ao adicionar um nome de domínio personalizado, na caixa de diálogo **Verificar domínio**, selecione um **certificado gerenciado de Adobe**.

   ![Escolher gerenciado por Adobe](assets/verify-domain-dialog.png)

1. Na caixa de diálogo **Verificar domínio**, adicione um registro de verificação CNAME ao DNS.

   ![Adicionar entrada CNAME](assets/verify-domain-dialog-adobe-managed.png)

1. Depois que o domínio for criado, clique no botão de reticências na lista de domínios e selecione **Verificar** para verificar o domínio.

   ![Verificar domínio](assets/verify-domain.png)

1. Retomar a tarefa [Adicionar um certificado DV](#adding-an-ssl-certificate).

### Solução de problemas de erros de certificado {#certificate-errors}

Alguns erros podem ocorrer se um certificado não for instalado corretamente ou não atender aos requisitos do Cloud Manager.

+++

* **Ordem correta dos certificados**

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

+++

* **Remover certificados de cliente**

  Ao adicionar um certificado, se você receber um erro semelhante ao seguinte:

  ```text
  The Subject of an intermediate certificate must match the issuer in the previous certificate. The SKI of an intermediate certificate must match the AKI of the previous certificate.
  ```

  Você provavelmente incluiu o certificado de cliente na cadeia de certificados. Verifique se a cadeia não inclui o certificado de cliente e tente novamente.

+++

+++

* **Política de certificado**

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

+++

* **Datas de validade do certificado**

  O Cloud Manager espera que o certificado SSL seja válido por pelo menos 90 dias a partir da data atual. Verifique a validade da cadeia de certificados.

+++

## Próximas etapas {#next-steps}

Agora você adicionou um certificado SSL de trabalho ao projeto. Essa etapa geralmente é a primeira a configurar um nome de domínio personalizado.

* Para configurar um nome de domínio personalizado, consulte [Adicionar um nome de domínio personalizado](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md).
* Para saber mais sobre como atualizar e gerenciar certificados SSL no Cloud Manager, consulte [Gerenciar certificados SSL](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md).
