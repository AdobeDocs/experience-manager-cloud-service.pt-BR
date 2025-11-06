---
title: Adicionar um certificado SSL
description: Saiba como adicionar seu próprio certificado SSL ou e o certificado DV (Validação de domínio) gerenciado pela Adobe usando as ferramentas de autoatendimento da Cloud Manager.
exl-id: 104b5119-4a8b-4c13-99c6-f866b3c173b2
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1021'
ht-degree: 2%

---


# Adicionar um certificado SSL {#add-ssl-cert}

Saiba como adicionar seu próprio certificado SSL ou e o certificado DV (Validação de domínio) gerenciado pela Adobe usando a nuvem

>[!NOTE]
>
>Se você usar um certificado SSL gerenciado pelo cliente (OV/EV) e um provedor CDN gerenciado pelo cliente, poderá ignorar a adição de um certificado SSL e ir diretamente para [Adicionar um Mapeamento de Domínio](/help/implementing/cloud-manager/domain-mappings/add-domain-mapping.md) quando estiver pronto.

O provisionamento de um certificado pode levar vários dias. Portanto, a Adobe aconselha provisionar seu próprio certificado com bastante antecedência em relação a qualquer prazo ou data de ativação para evitar atrasos.

Para saber mais sobre como atualizar e gerenciar certificados SSL no Cloud Manager, consulte [Gerenciar certificados SSL](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md).

Se tiver problemas ao adicionar ou gerenciar certificados, consulte [Solucionar erros de certificados SSL](/help/implementing/cloud-manager/managing-ssl-certifications/troubleshoot-ssl-cert.md).


## Pré-requisitos {#prerequisites}

* O usuário deve ser membro da função **Proprietário da empresa** ou **Gerente de implantação** para adicionar um certificado SSL.
* Se você estiver instalando seu próprio certificado, consulte **Requisitos de certificado** em [Introdução ao Gerenciamento de Certificados SSL](/help/implementing/cloud-manager/managing-ssl-certifications/introduction-to-ssl-certificates.md#requirements).

## Escolha de qual certificado SSL adicionar {#which-ssl-to-add}

Depois de [adicionar um nome de domínio personalizado](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) no AEM Cloud Manager, a próxima etapa dependerá se você optou por usar um certificado SSL gerenciado pela Adobe (DV) (recomendado) ou um certificado SSL gerenciado pelo cliente (OV/EV).

* **Para um certificado SSL gerenciado pela Adobe (DV):**
   * O processo de validação de domínio é feito depois que o domínio personalizado é adicionado e verificado no Cloud Manager.
   * Agora você deve [adicionar um certificado SSL gerenciado pela Adobe](#add-adobe-managed-ssl-cert).
Depois de adicionado ao Cloud Manager, aguarde que o Adobe emita e instale o certificado SSL DV em seu nome.
   * Quando o certificado estiver ativo, o domínio personalizado estará pronto para uso.

* **Para um certificado SSL gerenciado pelo cliente (OV/EV):**

   * Obtenha seu certificado SSL OV/EV de uma autoridade de certificação. Para obter mais detalhes, confira os [requisitos para certificados SSL OV/EV gerenciados pelo cliente](/help/implementing/cloud-manager/managing-ssl-certifications/introduction-to-ssl-certificates.md#requirements).
   * Depois de adquirir o certificado, [adicione os detalhes](#add-customer-managed-ssl-cert) do certificado SSL gerenciado pelo cliente (OV/EV) na Cloud Manager.
   * Depois de adicionado, o nome de domínio personalizado é marcado como verificado e o certificado SSL é aplicado.

Em ambos os casos, depois que o certificado é verificado e instalado, o domínio personalizado fica disponível para uso seguro em seu ambiente. Verifique o [status do domínio](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) na interface do Cloud Manager regularmente para confirmar se tudo está funcionando como esperado.

Consulte também [Introdução aos certificados SSL](/help/implementing/cloud-manager/managing-ssl-certifications/introduction-to-ssl-certificates.md).

## Adicionar um certificado SSL gerenciado pela Adobe (DV) {#add-adobe-managed-ssl-cert}

Precisa de ajuda para escolher se deseja usar um certificado SSL gerenciado pela Adobe (recomendado) ou um certificado SSL gerenciado pelo cliente com seu domínio? Consulte [Escolha de qual certificado SSL adicionar](#which-ssl-to-add)

**Para adicionar um certificado SSL gerenciado pela Adobe (DV):**

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione o programa apropriado.
1. No console **[Meus Programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, selecione o programa.
1. No canto superior esquerdo da página, clique em ![Mostrar ícone de menu](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) para exibir o menu lateral.

1. No cabeçalho **Serviços**, clique em ![Ícone Bloquear fechado](https://spectrum.adobe.com/static/icons/workflow_18/Smock_LockClosed_18_N.svg) **Certificados SSL**.

   ![Adicionando um certificado SSL](/help/implementing/cloud-manager/assets/ssl/ssl-cert-add.png)

1. Próximo ao canto superior direito da página Certificados SSL, clique em **Adicionar certificado SSL**.

1. Na caixa de diálogo **Adicionar certificado SSL**, com base em [seu caso de uso específico](#which-ssl-to-add), selecione **Adobe Managed (DV)**.

   ![Adicionar um certificado DV](/help/implementing/cloud-manager/assets/ssl/add-dv-certificate.png)

1. No campo **Nome do certificado**, digite um nome que você deseja associar ao certificado SSL DV.

1. Na lista suspensa **Selecionar domínios**, selecione um ou mais domínios verificados que deseja associar ao certificado SSL DV.
   * Nenhum domínio para selecionar? Em caso afirmativo, primeiro [adicione um nome de domínio personalizado](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) e verifique se ele foi verificado antes de adicionar um certificado SSL gerenciado pela Adobe.
   * Quando terminar de adicionar um nome de domínio personalizado, retorne a este tópico e comece na etapa 1 novamente.

1. No canto inferior direito da caixa de diálogo, clique em **Salvar**.

   Depois que o certificado SSL for emitido com êxito, ele será exibido com uma marca de seleção Válida verde na tabela **Certificados SSL**.

Agora você adicionou um certificado SSL DV gerenciado pela Adobe em funcionamento para o seu projeto. Essa etapa geralmente é a primeira a configurar um nome de domínio personalizado.

Agora você está pronto para adicionar uma [configuração de CDN](/help/implementing/cloud-manager/domain-mappings/add-domain-mapping.md).

## Adicionar um certificado SSL gerenciado pelo cliente (OV/ED) {#add-customer-managed-ssl-cert}

<!-- IF THIS TOPIC GET UPDATED, REMEMBER TO UPDATE THE STEPS ALSO IN THE "MANAGE SSL CERTIFICATES TOPIC TOO -->

Precisa de ajuda para escolher se deseja usar um certificado SSL gerenciado pela Adobe (recomendado) ou um certificado SSL gerenciado pelo cliente com seu domínio? Consulte [Escolha de qual certificado SSL adicionar](#which-ssl-to-add)

>[!IMPORTANT]
>
>Ao adicionar ou atualizar um certificado SSL, não inclua o novo certificado na cadeia de certificados. Incluí-lo impede que o upload seja concluído com sucesso.

**Para adicionar um certificado SSL gerenciado pelo cliente (OV/EV):**

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione o programa apropriado.

1. No console **[Meus Programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, selecione o programa.

1. No canto superior esquerdo da página, clique em ![Mostrar ícone de menu](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) para exibir o menu lateral.

1. No cabeçalho **Serviços**, clique em ![Ícone Bloquear fechado](https://spectrum.adobe.com/static/icons/workflow_18/Smock_LockClosed_18_N.svg) **Certificados SSL**.

   ![Adicionando um certificado SSL](/help/implementing/cloud-manager/assets/ssl/ssl-cert-add.png)

1. Próximo ao canto superior direito da página Certificados SSL, clique em **Adicionar certificado SSL**.

1. Na caixa de diálogo **Adicionar certificado SSL**, com base em [seu caso de uso específico](#which-ssl-to-add), selecione **OV/EV (Customer managed)**.

1. No campo **Nome do certificado**, digite um nome para o certificado.
Este campo é apenas para fins informativos e pode ser qualquer nome que o ajude a referenciar seu certificado SSL com facilidade.

1. Nos campos **Certificado**, **Chave privada** e **Cadeia de certificados**, copie os valores necessários do seu certificado SSL OV ou EV e cole-os nos respectivos campos na caixa de diálogo.

   Todos os erros detectados nos valores são exibidos. Antes de salvar o certificado, é necessário corrigir todos os erros. Consulte [Erros de Certificado](#certificate-errors) para saber mais sobre como solucionar erros comuns.

   ![Caixa de diálogo Adicionar certificado SSL](/help/implementing/cloud-manager/assets/ssl/ssl-cert-02.png)|

1. No canto inferior direito da caixa de diálogo, clique em **Salvar**.

   >[!NOTE]
   >
   >* Se você selecionou **Certificado gerenciado pelo cliente** enquanto [adicionou um nome de domínio personalizado](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md), o domínio será verificado ***após***, e o certificado SSL gerenciado pelo cliente (OV/EV) será adicionado e salvo. Consulte também [Verificar o status de um nome de domínio personalizado](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md#how-to).

   Depois que o certificado SSL for emitido com êxito, ele será exibido com uma marca de seleção verde verificada na tabela **Certificados SSL**.

Agora você adicionou um certificado SSL de trabalho ao projeto. Essa etapa geralmente é a primeira a configurar um nome de domínio personalizado.

Agora você está pronto para adicionar uma [configuração de CDN](/help/implementing/cloud-manager/domain-mappings/add-domain-mapping.md).























<!--
## Add an SSL certificate {#add-ssl-cert}

1. Log into Cloud Manager at [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) and select the appropriate program.
1. On the **[My Programs](/help/implementing/cloud-manager/navigation.md#my-programs)** console, select the program.
1. In the upper-left corner of the page, click ![Show menu icon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) to reveal the side menu. 
1. Under the **Services** heading, click ![Lock closed icon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_LockClosed_18_N.svg) **SSL Certificates**. 

   ![Adding an SSL certificate](/help/implementing/cloud-manager/assets/ssl/ssl-cert-add.png)

1. Near the upper-right corner of the SSL Certificates page, click **Add SSL Certificate**.

1. In the **Add SSL certificate** dialog box, based on [your particular use case](/help/implementing/cloud-manager/managing-ssl-certifications/introduction-to-ssl-certificates.md), do one of the following:

    | | Use case | Steps |
    | --- | --- | --- |
    | 1 | **Add an Adobe managed (DV) certificate** | **To add an Adobe managed (DV) SSL certificate:**<br>a. In the **Add SSL Certificate** dialog box, select the certificate type **Adobe managed (DV)**.<br>![Add a DV certificate](/help/implementing/cloud-manager/assets/ssl/add-dv-certificate.png)<br>b. In the **Certificate name** field, enter a name you want associated with the certificate.<br>c. In the **Select domains** drop-down list, select one or more domains that you want associated with the DV SSL certificate.<br>No domains to select? If so, it means that you must first add a custom domain name and ensure it is verified before you can add an SSL certificate. See [Add a custom domain name](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md). When you are finished adding a custom domain name, return to this topic and begin at step 1 again.<br>d. Continue to step 7. |
    | 2 | **Add a customer managed (OV/EV) certificate** | **To add a customer managed (OV/EV) SSL certificate:**<br>a. In the **Add SSL Certificate** dialog box, select the certificate type **Customer managed (OV/EV)**.<br>b. In the **Certificate name** field, enter a name for your certificate. This field is for informational purposes only and can be any name that helps you reference your SSL certificate easily.<br>c. In the **Certificate**, **Private key**, and **Certificate chain** fields, paste the required values into their respective fields.<br>![Add SSL certificate dialog box](/help/implementing/cloud-manager/assets/ssl/ssl-cert-02.png)<br>Any detected errors in values are displayed. Before you can save your certificate, you must address all errors. See [Certificate Errors](#certificate-errors) to learn more about troubleshooting common errors.<br>d. Continue to step 7. | 

1. In the lower-right corner of the dialog box, click **Save**.

    >[!NOTE]
    >
    >* If you selected **Adobe managed certificate** while [adding a custom domain name](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md), the domain is verified with the added certificate when the custom domain is added. 
    >
    >* If you selected **Customer managed certificate** while [adding a custom domain name](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md), the domain is verified ***after*** the customer managed (OV/EV) SSL certificate is added and saved. See also [Check the status of a custom domain name](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md#how-to).

    After the SSL certificate is successfully issued, it is displayed with a green verified check mark in the **SSL Certificates** table. 

    You now have added a working SSL certificate for your project. This step is often the first to set up a custom domain name. 
    

* To learn about updating and managing your SSL certificates in Cloud Manager, see [Manage SSL certificates](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md).

* If you are having issues adding or managing your certificates, see [Troubleshoot SSL certificate errors](/help/implementing/cloud-manager/managing-ssl-certifications/troubleshoot-ssl-cert.md). -->
