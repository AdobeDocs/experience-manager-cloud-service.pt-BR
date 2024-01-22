---
title: Adicionar um nome de domínio personalizado
description: Saiba como adicionar um nome de domínio personalizado usando o Cloud Manager.
exl-id: 0fc427b9-560f-4f6e-ac57-32cdf09ec623
source-git-commit: 52466e091cf6e0ab1ac620e15568c04881a3b63a
workflow-type: tm+mt
source-wordcount: '680'
ht-degree: 71%

---


# Adicionar um nome de domínio personalizado {#adding-cdn}

Você pode adicionar um nome de domínio personalizado a partir de dois locais no Cloud Manager:

* [Na página Configurações do domínio](#adding-cdn-settings)
* [Na página Ambientes](#adding-cdn-environments)

>[!NOTE]
>
>Um usuário deve ter o **Proprietário da empresa** ou **Gerente de implantação** para adicionar um nome de domínio personalizado no Cloud Manager, e você deve usar o Fastly CDN.

## Adição de um nome de domínio personalizado na página Configurações do domínio {#adding-cdn-settings}

Ao adicionar um nome de domínio personalizado, o domínio será distribuído usando o certificado mais específico e válido. Se vários certificados tiverem o mesmo domínio, o mais recente atualizado será escolhido. A Adobe recomenda que você gerencie certificados de forma que não haja domínios sobrepostos.

Siga estas etapas para adicionar um nome de domínio personalizado no **Configurações do domínio** página. Essas etapas são baseadas no Fastly. Se você usar um CDN diferente, deverá configurar seu domínio com o CDN que você escolheu usar.

1. Faça logon no Cloud Manager, em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/), e selecione a organização apropriada.

1. No **[Meus programas](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md#my-programs)** selecione o programa.

1. Acesse a tela **Ambientes** a partir da página **Visão geral**.

1. Clique em **Configurações do domínio** no painel de navegação esquerdo.

   ![A janela Configurações do domínio](/help/implementing/cloud-manager/assets/cdn/cdn-create.png)

1. Clique em **Adicionar domínio** botão na parte superior direita para abrir a **Adicionar nome de domínio** diálogo.

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

Consulte [Verificar o status do nome de domínio personalizado](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) para saber mais sobre diferentes status e como resolver possíveis problemas.

>[!TIP]
>
>Leia o seguinte artigo sobre a necessidade de [Adicionar um CNAME ou um registro em seguida](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md) para evitar o esforço duplo ao adicionar registros DNS ao domínio personalizado. A entrada TXT e o registro CNAME ou A podem ser definidos simultaneamente no servidor DNS regulador.

>[!TIP]
>
>Consulte [Adicionar um registro TXT](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md) para saber mais sobre registros TXT.

>[!NOTE]
>
>A verificação de DNS pode levar algumas horas para ser processada devido a atrasos de propagação de DNS.
>
>O Cloud Manager verificará a propriedade e atualizará o status que pode ser visto na Tabela de configurações do domínio. Consulte [Verificar o status do nome de domínio personalizado](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) para obter mais detalhes.

## Adicionar um nome de domínio personalizado na página Ambientes {#adding-cdn-environments}

Siga estas etapas para adicionar um nome de domínio personalizado na página **Ambientes**.

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriado.

1. Acesse a página **Detalhes do ambiente** do ambiente em que está interessado.

   ![Inserção do nome de domínio na página Detalhes do ambiente](/help/implementing/cloud-manager/assets/cdn/cdn-create4.png)

1. Use a tabela **Nomes de domínio** para enviar o nome de domínio personalizado.

   1. Insira o nome de domínio personalizado.
   1. Selecione o certificado SSL associado a esse nome na lista suspensa.
   1. Clique em **+Adicionar**.

   ![Adicionar nome de domínio personalizado](/help/implementing/cloud-manager/assets/cdn/cdn-create3.png)

1. Verifique os valores selecionados na caixa de diálogo **Adicionar nome de domínio** e clique em **Continuar**.

   ![Janela de nome de domínio](/help/implementing/cloud-manager/assets/cdn/cdn-create5.png)

   >[!NOTE]
   >
   >Não inclua `http://`, `https://` ou espaços ao inserir o nome do domínio.

1. A caixa de diálogo **Adicionar nome de domínio** será exibida e direcionará você ao processo de verificação do nome de domínio. Siga as instruções fornecidas para comprovar a propriedade do domínio para o seu ambiente. Clique em **Criar**.

   ![Verificação do nome de domínio](/help/implementing/cloud-manager/assets/cdn/cdn-create6.png)

A implantação do CDN requer um certificado SSL válido e uma verificação TXT bem-sucedida. Isso é indicado pelo status **Verificado e implantado**.

Consulte [Verificar o status do nome de domínio personalizado](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) para saber mais sobre diferentes status e como resolver possíveis problemas.

>[!NOTE]
>
>A verificação de DNS pode levar algumas horas para ser processada devido a atrasos de propagação de DNS.
>
>O Cloud Manager verificará a propriedade e atualizará o status que pode ser visto na Tabela de configurações do domínio. Consulte [Verificar o status do nome de domínio personalizado](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) para obter mais detalhes.

>[!TIP]
>
>Consulte [Adicionar um registro TXT](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md) para saber mais sobre registros TXT.
