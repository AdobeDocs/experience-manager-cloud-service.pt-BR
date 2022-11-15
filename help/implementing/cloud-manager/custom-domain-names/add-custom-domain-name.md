---
title: Adicionar um nome de domínio personalizado
description: Saiba como adicionar um nome de domínio personalizado usando o Cloud Manager.
exl-id: 0fc427b9-560f-4f6e-ac57-32cdf09ec623
source-git-commit: 0febf4b4a59617e6cc4f8414963c4a91fcf8765e
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 100%

---

# Adicionar um nome de domínio personalizado {#adding-cdn}

Você pode adicionar um nome de domínio personalizado a partir de dois locais no Cloud Manager:

* [Na página Configurações do domínio](#adding-cdn-settings)
* [Na página Ambientes](#adding-cdn-environments)

>[!NOTE]
>
>O usuário deve ter uma função de **Proprietário da empresa** ou **Gerente de implantação** para adicionar um nome de domínio personalizado no Cloud Manager

## Adição de um nome de domínio personalizado na página Configurações do domínio {#adding-cdn-settings}

Siga estas etapas para adicionar um nome de domínio personalizado na página **Configurações do domínio**.

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriado.

1. Acesse a tela **Ambientes** a partir da página **Visão geral**.

1. Clique em **Configurações do domínio** no painel de navegação esquerdo.

   ![A janela Configurações do domínio](/help/implementing/cloud-manager/assets/cdn/cdn-create.png)

1. Clique no botão **Adicionar domínio** no canto superior direito para abrir a caixa de diálogo **Adicionar nome de domínio**.

   ![Caixa de diálogo Adicionar domínio](/help/implementing/cloud-manager/assets/cdn/add-cdn1.png)

1. Insira o nome de domínio personalizado no campo **Nome do domínio**.

   >[!NOTE]
   >
   >Não inclua `http://`, `https://` ou espaços ao inserir seu domínio.

1. Selecione o **Ambiente** cujo serviço será associado ao nome de domínio.

1. Selecione **Publicar** ou **Visualizar** serviço.

1. Selecione o **Certificado SSL do domínio** associado ao nome de domínio no menu suspenso e clique em **Continuar**.

1. A caixa de diálogo **Adicionar nome de domínio** será exibida e direcionará você ao processo de verificação do nome de domínio. Siga as instruções fornecidas para comprovar a propriedade do domínio para o seu ambiente. Clique em **Criar**.

   ![Verificação do nome de domínio](/help/implementing/cloud-manager/assets/cdn/cdn-create6.png)

A implantação do CDN requer um certificado SSL válido e uma verificação TXT bem-sucedida. Isso é indicado pelo status **Verificado e implantado**.

Consulte o documento [Verificação de status do nome de domínio personalizado](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) para saber mais sobre diferentes status e como resolver com possíveis problemas.

>[!NOTE]
>
>A verificação de DNS pode levar algumas horas para ser processada devido a atrasos de propagação de DNS.
>
>O Cloud Manager verificará a propriedade e atualizará o status que pode ser visto na Tabela de configurações do domínio. Consulte o documento [Verificação de status do nome de domínio personalizado](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) para obter mais detalhes.

>[!TIP]
>
>Consulte [Adição de um registro TXT](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md) para saber mais sobre registros TXT.

## Adição de um nome de domínio personalizado na página Ambientes {#adding-cdn-environments}

Siga estas etapas para adicionar um nome de domínio personalizado na página **Ambientes**.

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriado.

1. Acesse a página **Detalhes do ambiente** do ambiente em que está interessado.

   ![Inserção do nome de domínio na página Detalhes do ambiente](/help/implementing/cloud-manager/assets/cdn/cdn-create4.png)

1. Use a tabela **Nomes de domínio** para enviar o nome de domínio personalizado.

   1. Insira o nome de domínio personalizado.
   1. Selecione o certificado SSL associado a esse nome na lista suspensa.
   1. Clique em **+Adicionar**.

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create3.png)

1. Verifique os valores selecionados na caixa de diálogo **Adicionar nome de domínio** e clique em **Continuar**.

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create5.png)

   >[!NOTE]
   >
   >Não inclua `http://`, `https://` ou espaços ao inserir o nome do domínio.

1. A caixa de diálogo **Adicionar nome de domínio** será exibida e direcionará você ao processo de verificação do nome de domínio. Siga as instruções fornecidas para comprovar a propriedade do domínio para o seu ambiente. Clique em **Criar**.

   ![Verificação do nome de domínio](/help/implementing/cloud-manager/assets/cdn/cdn-create6.png)

A implantação do CDN requer um certificado SSL válido e uma verificação TXT bem-sucedida. Isso é indicado pelo status **Verificado e implantado**.

Consulte o documento [Verificação de status do nome de domínio personalizado](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) para saber mais sobre diferentes status e como resolver com possíveis problemas.

>[!NOTE]
>
>A verificação de DNS pode levar algumas horas para ser processada devido a atrasos de propagação de DNS.
>
>O Cloud Manager verificará a propriedade e atualizará o status que pode ser visto na Tabela de configurações do domínio. Consulte o documento [Verificação de status do nome de domínio personalizado](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) para obter mais detalhes.

>[!TIP]
>
>Consulte [Adição de um registro TXT](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md) para saber mais sobre registros TXT.
