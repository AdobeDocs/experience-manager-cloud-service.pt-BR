---
title: Uso da ferramenta Mapeamento de usuários
description: Uso da ferramenta Mapeamento de usuários
translation-type: tm+mt
source-git-commit: 664c278494a5ac88362b994946060ab3baa846d8
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 0%

---


# Usando a ferramenta de mapeamento de usuário {#user-mapping-tool}

## Visão geral {#overview}

Como parte da jornada da transição para AEM como Cloud Service, é necessário mover usuários e grupos do sistema de AEM existente para AEM como Cloud Service. Isso é feito pela Ferramenta de transferência de conteúdo.

Uma grande mudança para AEM como Cloud Service é o uso totalmente integrado de IDs de Adobe para acessar a camada do autor.  Isso requer o uso do Adobe Admin Console para gerenciar usuários e grupos de usuários. As informações do perfil do usuário são centralizadas no Adobe Identity Management System (IMS), que fornece logon único em todos os aplicativos da nuvem de Adobe. Para obter mais detalhes, consulte Identity Management. Devido a essa alteração, os usuários e grupos existentes precisam ser mapeados para suas IDs IMS para evitar que usuários e grupos do duplicado na instância do autor do Cloud Service.

## Considerações importantes {#important-considerations}

Há alguns casos excepcionais a considerar. Os seguintes casos específicos serão registrados e o usuário ou grupo em questão não será mapeado:

1. Se um usuário não tiver endereço de email no campo `profile/email` de seu nó jcr.

1. Se um determinado email não for encontrado no sistema IMS para a ID da organização usada (ou se a ID IMS não puder ser recuperada por outro motivo).

1. Se o usuário estiver desabilitado no momento, ele será tratado como se não estivesse desabilitado.  Ele será mapeado e migrado normalmente e permanecerá desativado na instância da nuvem.

## Usando a ferramenta de mapeamento de usuário {#using-user-mapping-tool}

A Ferramenta de mapeamento de usuário usa uma API que permite pesquisar usuários do IMS por email e retornar suas IDs IMS. Essa API exige que o usuário crie uma ID do cliente para sua organização, um Segredo do cliente e um Token do Token de acesso/portador.

Siga estas etapas para configurar:

1. Navegue até [Console do desenvolvedor do Adobe](https://console.adobe.io) usando seu Adobe ID.
1. Criar um novo projeto ou abrir um projeto existente
1. Adicionar uma API
1. Escolher API de gerenciamento de usuário
1. Criar uma credencial JWT
1. Gerar um par de chaves ou Carregar uma chave pública (rsa não está funcionando)
1. Gere um token de acesso (ou token JWT ou token do portador).
1. Salve todas essas informações (ID do cliente, segredo do cliente, ID da conta técnica, e-mail da conta técnica, ID da organização, Token de acesso) em um local seguro.