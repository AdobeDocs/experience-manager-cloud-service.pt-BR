---
title: Adicionando um nome de domínio personalizado
description: Adicionando um nome de domínio personalizado
translation-type: tm+mt
source-git-commit: 6571c11cedbc0d81fbdfd8072a39b1327bdba10b
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 0%

---


# Adicionando um nome de domínio personalizado {#adding-cdn}

Um usuário deve ser um proprietário de negócios ou gerente de implantação para adicionar um nome de domínio personalizado no Cloud Manager.

>[!NOTE]
>Antes de adicionar um nome de domínio personalizado, um certificado SSL válido que contenha o nome de domínio personalizado deve ser instalado no seu Programa. Consulte Instalação de um certificado SSL para saber mais.

Somente um nome de domínio pode ser adicionado por vez. No entanto, os usuários podem adicionar curingas, por exemplo, `*.wknd.com` como um nome de domínio, e isso permitiria que vários subdomínios fossem hospedados com um único registro TXT.
Cada Ambiente do Cloud Manager pode hospedar até 50 domínios personalizados por ambiente.
O mesmo nome de domínio não pode ser usado em mais de um ambiente.

## Adicionando um nome de domínio personalizado da página Configurações de domínio {#adding-cdn-settings}

Siga as etapas abaixo para adicionar um Nome de domínio personalizado na página Configurações do domínio:

1. Navegue até a página Configurações de domínio na **Página Ambientes**

1. Selecione **Adicionar nome de domínio personalizado** para iniciar o assistente para adicionar nome de domínio personalizado.

1. Insira o nome de domínio personalizado.

   >[!NOTE]
   >Você não deve incluir `http://`, `https://` ou espaços ao entrar em seu domínio.

1. Selecione o Ambiente cujo serviço de Publicação será associado ao nome do domínio.

1. Selecione o certificado SSL no menu suspenso e selecione Continuar.

1. Isso levará você à Verificação de nome de domínio para a tela do seu Ambiente. Consulte Adicionando um registro TXT para saber mais.

   >[!NOTE]
   >Siga as instruções fornecidas para provar a propriedade do domínio do seu ambiente.

1. Selecione Continuar.
1. A implantação de CDN requer um certificado SSL válido e verificação de TXT bem-sucedida. Isso é indicado pelo status **Verificado e Implantado**.
1. Navegue até Verificando o status do nome de domínio personalizado para saber mais sobre vários status e como tratar.

   >[!NOTE]
   >A prova DNS pode levar algumas horas para ser reconhecida, devido a atrasos de propagação de DNS. O Cloud Manager verificará a propriedade e atualizará o status que pode ser visto na Tabela de configurações do domínio. Consulte Verificando o status do nome do domínio para obter mais detalhes.

## Adicionando um nome de domínio personalizado da página de Ambientes {#adding-cdn-environments}

1. Navegue até a página Detalhes do Ambiente para obter o ambiente de interesse.
1. Use os campos de entrada na parte superior da tabela Nomes de domínio para enviar o nome de domínio personalizado, certificado SSL. Em seguida, selecione Adicionar.
1. Isso iniciará o assistente para Adicionar nome de domínio personalizado com o nome do Ambiente pré-preenchido.
1. Insira o nome de domínio personalizado. Observação: Não inclua `http://`, `https://` ou espaços ao entrar em seu domínio. Selecione Continuar.
1. Isso levará você à Verificação de nome de domínio para a tela do seu Ambiente. Consulte Verificação de domínio (Adicionar registro TXT) para saber mais.

   >[!NOTE]
   >Siga as instruções fornecidas para provar a propriedade do domínio do seu ambiente.

1. Selecione Continuar.
1. A implantação de CDN requer um certificado SSL válido e verificação de TXT bem-sucedida. Isso é indicado pelo status **Verificado e Implantado**.

Neste ponto, seu nome de domínio personalizado está pronto para teste e um `CNAME` para apontá-lo. Consulte Status do nome de domínio para saber mais sobre vários status e como tratar.

>[!NOTE]
>A prova DNS pode levar algumas horas para ser reconhecida, devido a atrasos de propagação de DNS. O Cloud Manager verificará a propriedade e atualizará o status que pode ser visto na Tabela de configurações do domínio. Consulte Verificando o status do nome do domínio para saber mais.
