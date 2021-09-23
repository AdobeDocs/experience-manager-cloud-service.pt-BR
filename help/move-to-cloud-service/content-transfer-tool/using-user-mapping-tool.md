---
title: Usar a ferramenta Mapeamento de usuários
description: Usar a ferramenta Mapeamento de usuários
exl-id: 88ce7ed3-46fe-4b3f-8e18-c7c8423faf24
source-git-commit: c8e7c6c45d898029b55bcfc09f7f2b7051d03031
workflow-type: tm+mt
source-wordcount: '1375'
ht-degree: 2%

---

# Usar a ferramenta Mapeamento de usuários {#user-mapping-tool}

## Visão geral {#overview}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_usermapping"
>title="Ferramenta de mapeamento de usuários"
>abstract="A ferramenta Transferência de conteúdo ajuda a mover usuários e grupos do sistema de AEM existente para o AEM como Cloud Service. Os usuários e grupos existentes precisam ser mapeados para suas IDs IMS para evitar usuários e grupos duplicados na instância do autor do Cloud Service."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#important-considerations" text="Considerações importantes sobre o uso da ferramenta Mapeamento de usuários"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#using-user-mapping-tool" text="Usar a ferramenta Mapeamento de usuários"

Como parte da jornada de transição para o Adobe Experience Manager (AEM) as a Cloud Service, é necessário mover usuários e grupos do sistema de AEM existente para o AEM como Cloud Service. Isso é feito pela ferramenta Transferência de conteúdo.

Uma mudança importante no AEM como Cloud Service é o uso totalmente integrado de IDs de Adobe para acessar o nível de criação.  Isso requer o uso do [Adobe Admin Console](https://helpx.adobe.com/br/enterprise/using/admin-console.html) para gerenciar usuários e grupos de usuários. As informações do perfil do usuário são centralizadas no Adobe Identity Management System (IMS), que fornece o logon único em todos os aplicativos de nuvem do Adobe. Para obter mais detalhes, consulte [Identity Management](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/what-is-new-and-different.html?lang=en#identity-management). Devido a essa alteração, usuários e grupos existentes precisam ser mapeados para suas IDs de IMS para evitar usuários e grupos duplicados na instância de autor do Cloud Service.

### Ferramenta de mapeamento de usuários {#mapping-tool}

A ferramenta Transferência de conteúdo (sem Mapeamento de usuários) migrará qualquer usuário e grupo associado ao conteúdo que está sendo migrado. A Ferramenta de mapeamento de usuários faz parte da Ferramenta de transferência de conteúdo e seu único objetivo é modificar os usuários e grupos para que eles possam ser reconhecidos corretamente pelo IMS, a funcionalidade de logon único usada pelo AEM como um Cloud Service. Quando essas modificações forem feitas, a ferramenta Transferência de conteúdo migrará os usuários e grupos do conteúdo especificado como de costume.

## Considerações importantes {#important-considerations}

### Casos excepcionais {#exceptional-cases}

Os seguintes casos específicos serão registrados:

1. Se um usuário não tiver endereço de email no campo `profile/email` de seu nó *jcr*, o usuário ou grupo em questão será migrado, mas não mapeado.

1. Se um determinado email não for encontrado no sistema Adobe Identity Management System (IMS) para a ID da organização usada (ou se a ID IMS não puder ser recuperada por outro motivo), o usuário ou grupo em questão será migrado, mas não mapeado.

1. Se o usuário estiver desabilitado no momento, ele será tratado como se não estivesse desabilitado. Ele será mapeado e migrado normalmente e permanecerá desativado na instância da nuvem.

1. Se um usuário existir na instância do Cloud Service de AEM de destino com o mesmo nome de usuário (rep:principalName) de um dos usuários na instância de AEM de origem, o usuário ou grupo em questão não será migrado.

### Considerações adicionais {#additional-considerations}

* Se a configuração **Limpar conteúdo existente na instância do Cloud antes da assimilação** for definida, os usuários já transferidos na instância do Cloud Service serão excluídos juntamente com todo o repositório existente e um novo repositório será criado para assimilar conteúdo. Isso também redefine todas as configurações, incluindo permissões na instância do Cloud Service de destino, e é verdadeiro para um usuário administrador adicionado ao grupo **administradores**. O usuário administrador precisará ser adicionado novamente ao grupo **administrators** para recuperar o token de acesso para CTT.

* Recomenda-se remover qualquer usuário existente da instância do Cloud Service de destino AEM antes de executar a CTT com o Mapeamento de usuários. Isso é para evitar qualquer conflito entre a migração de usuários da instância de AEM de origem para a instância de AEM de destino. Os conflitos ocorrerão durante a assimilação se o mesmo usuário existir na instância de AEM de origem e na instância de AEM de destino.

* Quando os upups de conteúdo são executados, se o conteúdo não for transferido porque não foi alterado desde a transferência anterior, os usuários e grupos associados a esse conteúdo também não serão transferidos, mesmo se os usuários e grupos tiverem sido alterados enquanto isso. Isso ocorre porque os usuários e grupos são migrados junto com o conteúdo ao qual estão associados.

* Se a instância do Cloud Service de destino AEM tiver um usuário com um nome de usuário diferente, mas o mesmo endereço de email de um dos usuários na instância de origem do AEM e o Mapeamento de usuários estiver ativado, uma mensagem de erro será gravada nos logs e o usuário do AEM de origem não será transferido, pois somente um usuário com um determinado endereço de email é permitido no sistema de destino.

* Se dois usuários na instância de AEM de origem tiverem o mesmo endereço de email e o Mapeamento de usuários estiver ativado, uma mensagem de erro será gravada nos logs e um dos usuários de AEM de origem não será transferido, pois somente um usuário com um determinado endereço de email é permitido no sistema de destino.


## Usar a ferramenta Mapeamento de usuários {#using-user-mapping-tool}

A Ferramenta de mapeamento de usuários usa uma API que permite procurar usuários do Adobe Identity Management System (IMS) por email e retornar suas IDs IMS. Essa API exige que o usuário crie uma ID do cliente para sua organização, um Segredo do cliente e um Token de acesso ou portador.

Siga as etapas abaixo para configurar isso:

1. Navegue até [Console do desenvolvedor do Adobe](https://console.adobe.io) usando sua Adobe ID.
1. Crie um novo projeto ou abra um projeto existente.
1. Adicionar uma API - Clique em **Adicionar ao Projeto** e selecione **API**
1. Escolha a API de gerenciamento de usuários.  Talvez seja necessário obter permissões para ter essa opção.
1. Crie uma credencial JWT.
1. Gere um par de chaves ou Carregue uma chave pública (rsa não está bom).  Há um botão, **Generate a public/private keypair**, que fará isso para você.  Salve as chaves públicas e privadas.
1. Navegue até a API de gerenciamento de usuários.
1. Gere um token de acesso (ou token portador) colando seu conteúdo da chave privada na caixa de texto e clicando em **Gerar token**.
1. Salve todas essas informações, como **Client ID**, **Client Secret**, **Technical Account ID**, **Technical Account Email**, **Org ID** e **Access Token** com segurança.

## Interface do usuário {#user-interface}

A Ferramenta de mapeamento de usuários é integrada à Ferramenta de transferência de conteúdo. Você pode baixar a ferramenta Transferência de conteúdo no [Portal de distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html). Para obter mais detalhes sobre a versão mais recente, consulte as [Notas de versão atuais](/help/release-notes/release-notes-cloud/release-notes-current.md).

1. Selecione o Adobe Experience Manager e navegue até Ferramentas -> **Operações** -> **Transferência de conteúdo**.
1. Clique em **Criar configuração de mapeamento de usuário**.

   >[!NOTE]
   >Se você ignorar esta etapa, o mapeamento de usuários e grupos será ignorado durante a fase de Extração.

   ![imagem](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-1.png)

   Preencha os campos na Configuração da API de gerenciamento de usuário, conforme descrito abaixo:

   ![imagem](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-2.png)

   * **ID** da organização: Insira a ID da organização do Sistema Adobe Identity Management (IMS) para a organização na qual os usuários estão sendo migrados.

      >[!NOTE]
      >Para obter a ID da organização, faça logon no [Admin Console](https://adminconsole.adobe.com/) e escolha sua organização (na área superior direita) se você pertencer a mais de uma. A ID da organização estará no URL dessa página, no formato como `xx@AdobeOrg`, onde xx é a ID da organização IMS.  Como alternativa, você pode encontrar a ID da organização na página [Console do desenvolvedor do Adobe](https://console.adobe.io) onde gera o Token de acesso.

   * **ID** do cliente: Insira a ID do cliente que você salvou na etapa Configuração .

   * **Token** de acesso: Insira o Token de acesso que você salvou na etapa Configuração.

      >[!NOTE]
      >O Token de acesso expira a cada 24 horas e um novo precisa ser criado. Para criar um novo token, volte para [Console do Desenvolvedor do Adobe](https://console.adobe.io), escolha seu projeto, clique em **API do Gerenciamento de Usuário** e cole a mesma chave privada na caixa.

1. Depois de inserir as informações acima, clique em **Salvar**.

   ![imagem](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-3.png)


1. Crie um Conjunto de Migração clicando em **Criar Conjunto de Migração**, preenchendo os campos e clicando em **Salvar**. Para obter mais detalhes, consulte [Execução da ferramenta Transferência de conteúdo](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#running-tool).

   >[!NOTE]
   >A opção de alternância para incluir o Mapeamento de usuários e grupos do IMS está ATIVADA por padrão. Com essa configuração, quando a Extração for executada nesse conjunto de migração, a Ferramenta de mapeamento de usuários será executada como parte da fase de Extração. Essa é a maneira recomendada de executar a fase de Extração da ferramenta Transferência de conteúdo. Se esse botão estiver desativado e/ou a configuração de mapeamento do usuário não for criada, o mapeamento de usuários e grupos será ignorado durante a fase de Extração.

   ![imagem](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-4.png)

1. Para executar a fase de Extração, consulte [Executar a ferramenta de transferência de conteúdo](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#running-tool).
