---
title: Adicionar um nome de domínio personalizado
description: Adicionar um nome de domínio personalizado
exl-id: 0fc427b9-560f-4f6e-ac57-32cdf09ec623
source-git-commit: 98c137645351c86da8680a31b4929c588863a981
workflow-type: tm+mt
source-wordcount: '785'
ht-degree: 0%

---

# Adicionar um nome de domínio personalizado {#adding-cdn}

Um usuário deve ser um Proprietário comercial ou Gerente de implantação para adicionar um nome de Domínio personalizado no Cloud Manager.

As etapas a seguir devem ser completadas conforme indicado no quadro abaixo:

| Etapa |  | Responsabilidade | Saiba mais |
|--- |--- |--- |---|
| Adicionar certificado SLL | Adicionar certificado SLL | Cliente | [Adicionar um certificado SSL](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-ssl-certificates/add-ssl-certificate.html?lang=en) |
| Verificação de domínio | Adicionar registro TXT | Cliente | [Adicionar um registro TXT](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/add-text-record.html?lang=en) |
| Verificar Status de Verificação de Domínio |  | Cliente |  |
|  | Status: Falha na Verificação de Domínio | Cliente | [Verificando o status do nome de domínio](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/check-domain-name-status.html?lang=en) |
|  | Status: Verificado, Falha na Implantação | Entre em contato com o representante da Adobe | [Verificando o status do nome de domínio](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/check-domain-name-status.html?lang=en) |
| Adicionar registros DNS que apontam para AEM as a Cloud Service adicionando registros CNAME ou APEX | Definir configurações de DNS | Cliente | [Definição das configurações de DNS](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/configure-dns-settings.html?lang=en) |
| Verificar Status do Registro DNS |  | Cliente | [Verificando o Status do Registro DNS](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/check-dns-record-status.html?lang=en) |
|  | Status: Status de DNS não detectado | Cliente | [Verificando o Status do Registro DNS](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/check-dns-record-status.html?lang=en) |
|  | Status: O DNS resolve incorretamente | Cliente |  |


## Considerações importantes {#important-considerations}

* Antes de adicionar um nome de domínio personalizado, um certificado SSL válido que contenha o nome de domínio personalizado deve ser instalado no Programa. Consulte [Adicionar um certificado SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) para saber mais.

* Os nomes de domínio não podem ser adicionados a ambientes enquanto houver um pipeline de execução atual anexado a esses ambientes.

* Somente um nome de domínio pode ser adicionado por vez. Domínios personalizados no lado do autor não são compatíveis.

* AEM as a Cloud Service não oferece suporte a domínios curingas.

* Cada Ambiente do Cloud Manager pode hospedar até 500 domínios personalizados por ambiente.

* O mesmo nome de domínio não pode ser usado em mais de um ambiente.

## Adicionar um nome de domínio personalizado na página Configurações de domínio {#adding-cdn-settings}

Siga as etapas abaixo para adicionar um Nome de domínio personalizado na página Configurações de domínio :

1. Navegar para **Ambientes** tela de **Visão geral** página.

1. Clique em **Configurações de domínio** no menu de navegação esquerdo.

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create.png)

1. Clique em **Adicionar domínio** botão para abrir **Adicionar Nome de Domínio** caixa de diálogo.

   ![](/help/implementing/cloud-manager/assets/cdn/add-cdn1.png)

1. Insira o nome de domínio personalizado em **Nome do domínio**.

   >[!NOTE]
   >Você não deve incluir `http://`, `https://`ou espaços ao inserir no seu domínio.

1. Selecione o **Ambiente** cujo serviço de Publicação será associado ao nome do domínio.

1. Selecione o serviço como **Publicar** ou **Visualizar**.

   >[!NOTE]
   >Agora, os nomes de domínio personalizados são compatíveis com os programas do Cloud Manager for Sites para Serviços de publicação e visualização. Cada Ambiente do Cloud Manager pode hospedar até 500 domínios personalizados por ambiente. Para saber mais sobre o Serviço de visualização, consulte [Serviço de visualização](/help/implementing/cloud-manager/manage-environments.md#preview-service).

1. Selecione o **Certificado SSL de domínio** no menu suspenso e selecione **Continuar**.

1. **Adicionar Nome de Domínio** será exibida. Isso o levará à tela Verificação de nome de domínio de seu ambiente. Consulte [Adicionar um registro TXT](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md) para saber mais.

   Siga as instruções fornecidas para provar a propriedade do domínio para seu ambiente:

1. Clique em **Criar**.
1. A implantação de CDN requer um certificado SSL válido e uma verificação TXT bem-sucedida. Isso é indicado pelo status **Verificado e implantado**.
Navegar para [Verificando o status do nome de domínio personalizado](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) para saber mais sobre vários status e como abordar o problema.

   >[!NOTE]
   >A prova de DNS pode levar algumas horas para ser reconhecida, devido a atrasos de propagação de DNS. O Cloud Manager verificará a propriedade e atualizará o status que pode ser visto na Tabela de configurações do domínio. Consulte Verificar o status do nome do domínio para obter mais detalhes.

## Adicionar um nome de domínio personalizado na página Ambientes {#adding-cdn-environments}

1. Navegue até a página Detalhes do ambiente do ambiente de interesse.

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create4.png)

1. Use os campos de entrada na parte superior da tabela Nomes de domínio para enviar o nome de domínio personalizado e selecione o certificado SSL na lista suspensa. Clique em **+ Adicionar**.

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create3.png)

1. Verifique os campos do **Adicionar Nome de Domínio** e clique em **Continuar**.

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create5.png)

   >[!NOTE]
   >Não incluir `http://`, `https://`ou espaços ao inserir no seu domínio.

1. Verificação de nome de domínio para a tela Ambiente é exibida.

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create6.png)

   Consulte [Verificação de domínio](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md) para saber mais. Siga as instruções fornecidas para provar a propriedade do domínio para seu ambiente.

1. Clique em **Criar**.

1. A implantação do Nome de domínio personalizado requer um certificado SSL válido e uma verificação TXT bem-sucedida. Isso é indicado pelo status **Verificado e implantado**.

Neste ponto, o nome de domínio personalizado está pronto para testes e um `CNAME` aponte para isso. Consulte [Estado do Nome de Domínio](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) para saber mais sobre vários status e como abordar o problema.

>[!NOTE]
>A prova de DNS pode levar algumas horas para ser reconhecida, devido a atrasos de propagação de DNS. O Cloud Manager verificará a propriedade e atualizará o status que pode ser visto na Tabela de configurações do domínio. Consulte Verificar o status do nome do domínio para saber mais.
