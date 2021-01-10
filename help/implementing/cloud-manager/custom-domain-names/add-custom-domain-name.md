---
title: Adicionando um nome de domínio personalizado
description: Adicionando um nome de domínio personalizado
translation-type: tm+mt
source-git-commit: b336f361b496b672d26a5316952ee52ce828e201
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 0%

---


# Adicionando um nome de domínio personalizado {#adding-cdn}

Um usuário deve ser um proprietário de negócios ou gerente de implantação para adicionar um nome de domínio personalizado no Cloud Manager.

## Considerações importantes {#important-considerations}

* Antes de adicionar um nome de domínio personalizado, um certificado SSL válido que contenha o nome de domínio personalizado deve ser instalado no seu Programa. Consulte [Adicionar um certificado SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) para saber mais.

* Os nomes de domínio não podem ser adicionados aos ambientes enquanto houver um pipeline em execução atual anexado a esses ambientes.

* Somente um nome de domínio pode ser adicionado por vez. No entanto, domínios não podem conter curingas. Não há suporte para domínios personalizados no lado do autor.

* Cada Ambiente do Cloud Manager pode hospedar até 100 domínios personalizados por ambiente.

* O mesmo nome de domínio não pode ser usado em mais de um ambiente.

## Adicionando um nome de domínio personalizado da página Configurações de domínio {#adding-cdn-settings}

Siga as etapas abaixo para adicionar um Nome de domínio personalizado na página Configurações do domínio:

1. Navegue até a tela **Ambientes** da página **Visão geral**.

1. Clique em **Configurações de domínio** no menu de navegação esquerdo.

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create.png)

1. Clique no botão **Adicionar domínio** para abrir a caixa de diálogo **Adicionar nome de domínio**.

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create2.png)

1. Digite o nome do domínio personalizado em **Nome do domínio**.

   >[!NOTE]
   >Você não deve incluir `http://`, `https://` ou espaços ao entrar em seu domínio.

1. Selecione o **Ambiente** cujo serviço de Publicação será associado ao nome do domínio.

1. Selecione **Certificado SSL de Domínio** no menu suspenso e selecione **Continuar**.

1. **A caixa de diálogo Adicionar** nome de domínio é exibida. Isso levará você à Verificação de nome de domínio para a tela do seu Ambiente. Consulte [Adicionar um registro TXT](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md) para saber mais.
Siga as instruções fornecidas para provar a propriedade do domínio do seu ambiente.

1. Clique em **Criar**.
1. A implantação de CDN requer um certificado SSL válido e verificação de TXT bem-sucedida. Isso é indicado pelo status **Verificado e Implantado**.
Navegue até [Verificando o Status do Nome de Domínio Personalizado](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) para saber mais sobre vários status e como lidar.

   >[!NOTE]
   >A prova DNS pode levar algumas horas para ser reconhecida, devido a atrasos de propagação de DNS. O Cloud Manager verificará a propriedade e atualizará o status que pode ser visto na Tabela de configurações do domínio. Consulte Verificando o status do nome do domínio para obter mais detalhes.

## Adicionando um nome de domínio personalizado da página de Ambientes {#adding-cdn-environments}

1. Navegue até a página Detalhes do Ambiente para obter o ambiente de interesse.

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create4.png)

1. Use os campos de entrada na parte superior da tabela Nomes de domínio para enviar o nome de domínio personalizado e selecionar o certificado SSL na lista suspensa. Clique em **+ Adicionar**.

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create3.png)

1. Marque os campos na caixa de diálogo **Adicionar nome de domínio** e clique em **Continuar**.

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create5.png)

   >[!NOTE]
   >Não inclua `http://`, `https://` ou espaços ao entrar em seu domínio.

1. A verificação de nome de domínio para a tela do seu Ambiente é exibida.

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create6.png)

   Consulte [Verificação de domínio](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md) para saber mais. Siga as instruções fornecidas para provar a propriedade do domínio do seu ambiente.

1. Clique em **Criar**.

1. A implantação de Nome de domínio personalizado requer um certificado SSL válido e uma verificação TXT bem-sucedida. Isso é indicado pelo status **Verificado e Implantado**.

Neste ponto, seu nome de domínio personalizado está pronto para teste e um `CNAME` para apontá-lo. Consulte [Status do Nome de Domínio](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) para saber mais sobre vários status e como lidar.

>[!NOTE]
>A prova DNS pode levar algumas horas para ser reconhecida, devido a atrasos de propagação de DNS. O Cloud Manager verificará a propriedade e atualizará o status que pode ser visto na Tabela de configurações do domínio. Consulte Verificando o status do nome do domínio para saber mais.
