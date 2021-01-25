---
title: Uso da ferramenta Mapeamento de usuários
description: Uso da ferramenta Mapeamento de usuários
translation-type: tm+mt
source-git-commit: 410b7900981596590fa80b286b40a965700f108e
workflow-type: tm+mt
source-wordcount: '750'
ht-degree: 1%

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

## Interface do usuário {#user-interface}

A Ferramenta de mapeamento do usuário é integrada à Ferramenta de transferência de conteúdo. Você pode baixar a Ferramenta de transferência de conteúdo do Portal de distribuição de software. Para obter mais detalhes sobre a versão mais recente, consulte as Notas de versão.

1. Selecione Selecionar o Adobe Experience Manager e navegue até Ferramentas -> **Operações** -> **Transferência de Conteúdo**.
1. Clique em **Create User Mapping Config**.

   >[!NOTE]
   >Se você ignorar esta etapa, o mapeamento de usuários e grupos será ignorado durante a fase de Extração.

   Preencha os campos na Configuração da API de Gerenciamento de Usuário, conforme descrito abaixo:

   * **ID** da organização: Digite a ID de organização IMS da organização na qual os usuários estão sendo migrados.

      >[!NOTE]
      >Para obter a ID da organização, faça logon no [Admin Console](https://adminconsole.adobe.com/) e escolha sua organização (na área superior direita) se você pertencer a mais de uma. A ID da organização estará no URL dessa página, no formato `xx@AdobeOrg`, onde xx é a ID da organização IMS.  Como alternativa, você pode encontrar a ID da organização na página [Console do desenvolvedor do Adobe](https://console.adobe.io) onde você gera o Token de acesso.

   * **ID** do cliente: Insira a ID do cliente que você salvou na etapa de instalação

   * **token de acesso**: Digite o Token de acesso salvo na etapa de configuração

      >[!NOTE]
      >O Token de acesso expira a cada 24 horas e é necessário criar um novo. Para criar um novo token, volte para [Console do desenvolvedor do Adobe](https://console.adobe.io), escolha o seu projeto, clique em API de gerenciamento de usuários e cole a mesma chave privada na caixa.

1. Depois de inserir as informações acima, clique em Salvar.

1. Crie um Conjunto de Migrações clicando em Criar Conjunto de Migrações e preenchendo os campos e, em seguida, clicando em Salvar. Para obter mais detalhes, consulte Executar a ferramenta de transferência de conteúdo.

   >[!NOTE]
   >A opção de alternância para incluir o Mapeamento de usuários e grupos de IMS está ATIVADA por padrão. Com essa configuração, quando a Extração é executada nesse conjunto de migração, a Ferramenta de Mapeamento de Usuário será executada como parte da fase de Extração. Essa é a maneira recomendada para executar a fase de Extração da Ferramenta de transferência de conteúdo. Se essa alternância estiver desativada e/ou a Configuração de mapeamento do usuário não for criada, os mapeamentos de usuários e grupos serão ignorados durante a fase de Extração.

1. Para executar a fase de Extração, consulte [Execução da Ferramenta de Transferência de Conteúdo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#running-tool).



