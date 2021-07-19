---
title: Adicionar um nome de domínio personalizado
description: Adicionar um nome de domínio personalizado
exl-id: 0fc427b9-560f-4f6e-ac57-32cdf09ec623
source-git-commit: 4be76f19c27aeab84de388106a440434a99a738c
workflow-type: tm+mt
source-wordcount: '610'
ht-degree: 0%

---

# Adicionar um nome de domínio personalizado {#adding-cdn}

Um usuário deve ser um Proprietário comercial ou Gerente de implantação para adicionar um nome de Domínio personalizado no Cloud Manager.

## Considerações importantes {#important-considerations}

* Antes de adicionar um nome de domínio personalizado, um certificado SSL válido que contenha o nome de domínio personalizado deve ser instalado no Programa. Consulte [Adicionar um certificado SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) para saber mais.

* Os nomes de domínio não podem ser adicionados a ambientes enquanto houver um pipeline de execução atual anexado a esses ambientes.

* Somente um nome de domínio pode ser adicionado por vez. No entanto, os domínios não podem conter curingas. Domínios personalizados no lado do autor não são compatíveis.

* O AEM as a Cloud Service não oferece suporte a domínios curingas.

* Cada Ambiente do Cloud Manager pode hospedar até 500 domínios personalizados por ambiente.

* O mesmo nome de domínio não pode ser usado em mais de um ambiente.

## Adicionar um nome de domínio personalizado na página Configurações de domínio {#adding-cdn-settings}

Siga as etapas abaixo para adicionar um Nome de domínio personalizado na página Configurações de domínio :

1. Navegue até a tela **Ambientes** a partir da página **Visão geral**.

1. Clique em **Configurações de domínio** no menu de navegação esquerdo.

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create.png)

1. Clique no botão **Adicionar Domínio** para abrir a caixa de diálogo **Adicionar Nome de Domínio**.

   ![](/help/implementing/cloud-manager/assets/cdn/add-cdn1.png)

1. Insira o nome de domínio personalizado em **Domain Name**.

   >[!NOTE]
   >Você não deve incluir `http://`, `https://` ou espaços ao inserir o seu domínio.

1. Selecione o **Ambiente** cujo serviço de Publicação será associado ao nome do domínio.

1. Selecione o serviço como **Publish** ou **Preview**.

   >[!NOTE]
   >Agora, os nomes de domínio personalizados são compatíveis com os programas do Cloud Manager for Sites para Serviços de publicação e visualização. Cada Ambiente do Cloud Manager pode hospedar até 250 domínios personalizados por ambiente. Para saber mais sobre o Serviço de visualização, consulte [Serviço de visualização](/help/implementing/cloud-manager/manage-environments.md#preview-service).

1. Selecione o **Certificado SSL de Domínio** no menu suspenso e selecione **Continuar**.

1. **A caixa de diálogo Adicionar** nome de domínio é exibida. Isso o levará à tela Verificação de nome de domínio de seu ambiente. Consulte [Adicionar um registro TXT](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md) para saber mais.

   Siga as instruções fornecidas para provar a propriedade do domínio para seu ambiente:

1. Clique em **Criar**.
1. A implantação de CDN requer um certificado SSL válido e uma verificação TXT bem-sucedida. Isso é indicado pelo status **Verified and Deployed**.
Navegue até [Verificando o Status do Nome de Domínio Personalizado](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) para saber mais sobre vários status e como abordar.

   >[!NOTE]
   >A prova de DNS pode levar algumas horas para ser reconhecida, devido a atrasos de propagação de DNS. O Cloud Manager verificará a propriedade e atualizará o status que pode ser visto na Tabela de configurações do domínio. Consulte Verificar o status do nome do domínio para obter mais detalhes.

## Adicionar um nome de domínio personalizado na página Ambientes {#adding-cdn-environments}

1. Navegue até a página Detalhes do ambiente do ambiente de interesse.

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create4.png)

1. Use os campos de entrada na parte superior da tabela Nomes de domínio para enviar o nome de domínio personalizado e selecione o certificado SSL na lista suspensa. Clique em **+ Adicionar**.

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create3.png)

1. Marque os campos na caixa de diálogo **Adicionar nome de domínio** e clique em **Continuar**.

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create5.png)

   >[!NOTE]
   >Não inclua `http://`, `https://` ou espaços ao entrar em seu domínio.

1. Verificação de nome de domínio para a tela Ambiente é exibida.

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create6.png)

   Consulte [Verificação de Domínio](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md) para saber mais. Siga as instruções fornecidas para provar a propriedade do domínio para seu ambiente.

1. Clique em **Criar**.

1. A implantação do Nome de domínio personalizado requer um certificado SSL válido e uma verificação TXT bem-sucedida. Isso é indicado pelo status **Verified and Deployed**.

Neste ponto, o nome de domínio personalizado está pronto para teste e um `CNAME` para apontar para ele. Consulte [Status do Nome de Domínio](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) para saber mais sobre vários status e como abordar.

>[!NOTE]
>A prova de DNS pode levar algumas horas para ser reconhecida, devido a atrasos de propagação de DNS. O Cloud Manager verificará a propriedade e atualizará o status que pode ser visto na Tabela de configurações do domínio. Consulte Verificar o status do nome do domínio para saber mais.
