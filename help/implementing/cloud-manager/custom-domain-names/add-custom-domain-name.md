---
title: Adicionar um nome de domínio personalizado
description: Saiba como adicionar um nome de domínio personalizado usando o Cloud Manager.
exl-id: 0fc427b9-560f-4f6e-ac57-32cdf09ec623
source-git-commit: 0febf4b4a59617e6cc4f8414963c4a91fcf8765e
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 2%

---

# Adicionar um nome de domínio personalizado {#adding-cdn}

Você pode adicionar um nome de domínio personalizado a partir de dois locais no Cloud Manager:

* [Na página Configurações de domínio](#adding-cdn-settings)
* [Na página Ambientes](#adding-cdn-environments)

>[!NOTE]
>
>Um usuário deve ter a variável **Proprietário da empresa** ou **Gerenciador de implantação** para adicionar um nome de domínio personalizado no Cloud Manager

## Adicionar um nome de domínio personalizado na página Configurações de domínio {#adding-cdn-settings}

Siga estas etapas para adicionar um nome de domínio personalizado da **Configurações de domínio** página.

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriados.

1. Navegue até o **Ambientes** da tela **Visão geral** página.

1. Clique em **Configurações de domínio** no painel de navegação esquerdo.

   ![A janela Configurações de domínio](/help/implementing/cloud-manager/assets/cdn/cdn-create.png)

1. Clique no botão **Adicionar domínio** no canto superior direito para abrir o **Adicionar Nome de Domínio** caixa de diálogo.

   ![Caixa de diálogo Adicionar domínio](/help/implementing/cloud-manager/assets/cdn/add-cdn1.png)

1. Insira o nome de domínio personalizado no **Nome do domínio** campo.

   >[!NOTE]
   >
   >Não incluir `http://`, `https://`ou espaços ao inserir no seu domínio.

1. Selecione o **Ambiente** cujo serviço será associado ao nome de domínio.

1. Selecione uma das opções **Publicar** ou **Visualizar** serviço.

1. Selecione o **Certificado SSL de domínio** associado ao nome de domínio no menu suspenso e selecione **Continuar**.

1. O **Adicionar Nome de Domínio** será exibida e levará você ao processo de verificação do nome de domínio. Siga as instruções fornecidas para provar a propriedade do domínio para seu ambiente. Clique em **Criar**.

   ![Verificação do nome de domínio](/help/implementing/cloud-manager/assets/cdn/cdn-create6.png)

A implantação de CDN requer um certificado SSL válido e uma verificação TXT bem-sucedida. Isso é indicado pelo status **Verificado e implantado**.

Consulte o documento [Verificando o status do nome de domínio personalizado](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) para saber mais sobre vários status e como lidar com possíveis problemas.

>[!NOTE]
>
>A verificação de DNS pode levar algumas horas para ser processada devido a atrasos de propagação de DNS.
>
>O Cloud Manager verificará a propriedade e atualizará o status que pode ser visto na Tabela de configurações do domínio. Consulte o documento [Verificando o status do nome de domínio personalizado](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) para obter mais detalhes.

>[!TIP]
>
>Consulte [Adicionar um registro TXT](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md) para saber mais sobre registros TXT.

## Adicionar um nome de domínio personalizado na página Ambientes {#adding-cdn-environments}

Siga estas etapas para adicionar um nome de domínio personalizado da **Ambientes** página.

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriados.

1. Navegar para **Detalhes dos ambientes** página do ambiente de interesse.

   ![Inserir nome de domínio na página Detalhes do ambiente](/help/implementing/cloud-manager/assets/cdn/cdn-create4.png)

1. Use o **Nomes de Domínio** para enviar o nome de domínio personalizado.

   1. Insira o nome de domínio personalizado.
   1. Selecione o certificado SSL associado a esse nome na lista suspensa.
   1. Clique em **+Adicionar**.

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create3.png)

1. Verifique os valores selecionados na **Adicionar Nome de Domínio** e clique em **Continuar**.

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create5.png)

   >[!NOTE]
   >
   >Não incluir `http://`, `https://`ou espaços ao inserir o nome de domínio.

1. O **Adicionar Nome de Domínio** será exibida e levará você ao processo de verificação do nome de domínio. Siga as instruções fornecidas para provar a propriedade do domínio para seu ambiente. Clique em **Criar**.

   ![Verificação do nome de domínio](/help/implementing/cloud-manager/assets/cdn/cdn-create6.png)

A implantação de CDN requer um certificado SSL válido e uma verificação TXT bem-sucedida. Isso é indicado pelo status **Verificado e implantado**.

Consulte o documento [Verificando o status do nome de domínio personalizado](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) para saber mais sobre vários status e como lidar com possíveis problemas.

>[!NOTE]
>
>A verificação de DNS pode levar algumas horas para ser processada devido a atrasos de propagação de DNS.
>
>O Cloud Manager verificará a propriedade e atualizará o status que pode ser visto na Tabela de configurações do domínio. Consulte o documento [Verificando o status do nome de domínio personalizado](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) para obter mais detalhes.

>[!TIP]
>
>Consulte [Adicionar um registro TXT](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md) para saber mais sobre registros TXT.
