---
title: Adicionar um nome de domínio personalizado
description: Saiba como adicionar um nome de domínio personalizado usando o Cloud Manager.
exl-id: 0fc427b9-560f-4f6e-ac57-32cdf09ec623
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 4a369104ea8394989149541ee1a7b956383c8f12
workflow-type: tm+mt
source-wordcount: '702'
ht-degree: 26%

---


# Adicionar um nome de domínio personalizado {#adding-cdn}

Saiba como adicionar um nome de domínio personalizado usando o Cloud Manager.

## Requisitos {#requirements}

Atenda a esses requisitos antes de adicionar um nome de domínio personalizado no Cloud Manager.

* Você deve ter adicionado um certificado SSL para o domínio que deseja adicionar antes de adicionar um nome de domínio personalizado, conforme descrito no documento [Adicionando um certificado SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md).
* Você deve ter a função de **Proprietário da empresa** ou **Gerente de implantação** para adicionar um nome de domínio personalizado no Cloud Manager.
* Estar usando o Fastly CDN.

## Onde adicionar nomes de domínio personalizados {#where}

Você pode adicionar um nome de domínio personalizado a partir de dois locais no Cloud Manager:

* [Na página Configurações do domínio](#adding-cdn-settings)
* [Na página Ambientes](#adding-cdn-environments)

Ao adicionar um nome de domínio personalizado, o domínio é distribuído usando o certificado mais específico e válido. Se vários certificados tiverem o mesmo domínio, o mais recente atualizado será escolhido. A Adobe recomenda que você gerencie certificados de forma que não haja domínios sobrepostos.

As etapas descritas neste documento são baseadas no Fastly. Se você usou um CDN diferente, configure seu domínio com o CDN que você escolheu usar.

## Adicionar um nome de domínio personalizado na página Configurações do domínio {#adding-cdn-settings}

Siga estas etapas para adicionar um nome de domínio personalizado na página **Configurações do domínio**.

1. Faça logon no Cloud Manager, em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/), e selecione a organização apropriada.

1. No console **[Meus Programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, selecione o programa.

1. Navegue até a guia **Configurações do domínio** selecionada no painel de navegação esquerdo.

   ![A janela Configurações do domínio](/help/implementing/cloud-manager/assets/cdn/cdn-create.png)

1. Clique no botão **Adicionar domínio** no canto superior direito para abrir a caixa de diálogo **Adicionar nome de domínio**.

   ![Caixa de diálogo Adicionar Domínio](/help/implementing/cloud-manager/assets/cdn/add-cdn1.png)

1. Na guia **Nome do Domínio**, digite o nome de domínio personalizado no campo **Nome do Domínio**.

   >[!NOTE]
   >
   >Não inclua `http://`, `https://` ou espaços ao inserir seu domínio.

1. Selecione o **Ambiente** cujo serviço será associado ao nome de domínio.

1. Selecione **Publicar** ou **Visualizar** serviço.

1. Selecione o **Certificado SSL do domínio** associado ao nome de domínio no menu suspenso e clique em **Continuar**.

1. A guia **Verificação** é exibida.

   ![Verificação do nome de domínio](/help/implementing/cloud-manager/assets/cdn/cdn-create6.png)

   * A guia **Verificação** descreve as próximas etapas para configurar o nome de domínio personalizado, que está criando um registro TXT necessário.
   * Você pode executar esta etapa imediatamente (antes de clicar em **Criar** na caixa de diálogo) ou depois de clicar em **Criar** na caixa de diálogo.
   * As opções e as próximas etapas são descritas abaixo.

1. Clique em **Criar** para salvar o nome de domínio personalizado no Cloud Manager.

Ao selecionar **Criar** no assistente **Adicionar domínio personalizado**, o Cloud Manager aciona uma verificação TXT. Crie o registro TXT ao configurar o nome de domínio personalizado no Cloud Manager. No entanto, essa etapa não é necessária. Para as verificações subsequentes, você deverá selecionar ativamente o ícone **Verificar novamente** ao lado do status.

O nome não estará ativo até que o Cloud Manager verifique se a entrada TXT foi adicionada e verificada. O status de **Verificado e implantado** indica uma verificação TXT bem-sucedida.

* Consulte [Adicionar um registro TXT](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md) para saber mais sobre registros TXT.
* Consulte [Verificar o status do nome de domínio](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) para obter mais detalhes sobre como a Cloud Manager verifica o nome de domínio personalizado e sua entrada TXT.

## Próximas etapas {#next-steps}

Depois de criar seu nome de domínio personalizado no Cloud Manager, adicione uma entrada TXT para verificar a propriedade do domínio. Prossiga para o documento [Adicionando um Registro TXT](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md) para continuar configurando seu nome de domínio personalizado.

## Adicione um nome de domínio personalizado na página Ambientes {#adding-cdn-environments}

As etapas para adicionar um nome de domínio personalizado da página **Ambientes** são as mesmas de [adicionar um nome de domínio personalizado da página Configurações de Domínio](#adding-cdn-settings), mas o ponto de entrada é diferente. Siga estas etapas para adicionar um nome de domínio personalizado na página **Ambientes**.

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriado.

1. Acesse a página **Detalhes do ambiente** do ambiente em que está interessado.

   ![Inserção do nome de domínio na página Detalhes do ambiente](/help/implementing/cloud-manager/assets/cdn/cdn-create4.png)

1. Use a tabela **Nomes de domínio** para enviar o nome de domínio personalizado.

   1. Insira o nome de domínio personalizado.
   1. Selecione o certificado SSL associado a esse nome na lista suspensa.
   1. Clique em **+Adicionar**.

   ![Adicionar um nome de domínio personalizado](/help/implementing/cloud-manager/assets/cdn/cdn-create3.png)

1. A caixa de diálogo **Adicionar nome de domínio** é aberta na guia **Nome de Domínio**. Continue como faria para [adicionar um nome de domínio personalizado da página Configurações de Domínio](#adding-cdn-settings).
