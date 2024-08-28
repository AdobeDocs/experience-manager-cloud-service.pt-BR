---
title: Utilização da Ferramenta de mapeamento de usuário (herdada)
description: Utilização da Ferramenta de mapeamento de usuário (herdada)
exl-id: dcb750c4-0f81-4d11-ac6c-0592162b683d
hide: true
hidefromtoc: true
feature: Migration
role: Admin
source-git-commit: e5fd1b351047213adbb83ef1d1722352958ce823
workflow-type: tm+mt
source-wordcount: '803'
ht-degree: 1%

---


# Utilização da Ferramenta de mapeamento de usuário (herdada) {#using-user-mapping-tool}

>[!INFO]
>
>Esta documentação se refere a uma versão obsoleta da ferramenta. Para obter mais informações sobre a versão mais recente, consulte [Migração de grupo](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/group-migration.md).

A Ferramenta de mapeamento de usuários usa uma API que permite pesquisar usuários do Adobe Identity Management System (IMS) por email e retornar suas IDs de IMS. Essa API exige que o usuário crie uma ID do cliente para sua organização, um Segredo do cliente e um Token de acesso ou portador.

## Configuração da ferramenta Mapeamento de usuários {#setting-up-user-mapping}

**Pré-requisito:** o mapeamento de usuários exige que cada usuário seja mapeado para sua respectiva ID IMS e tenha um endereço de email em seu perfil no AEM e no IMS. Mesmo que o usuário use um endereço de email como uma ID de usuário para fazer logon, o mapeamento não funcionará para esse usuário, a menos que o endereço de email também esteja no perfil e também no IMS.

Siga as etapas abaixo para configurar isso:

1. Navegue até [Adobe Developer Console](https://developer.adobe.com/console/) usando sua Adobe ID.
1. Crie um projeto ou abra um projeto existente.
1. Adicionar uma API - Clique em **Adicionar ao Projeto** e selecione **API**
1. Escolha API de gerenciamento de usuários. Você deve ter permissões de Administrador do sistema para disponibilizar essa opção.
1. Criar uma credencial JWT.
1. Gere um par de chaves ou faça o upload de uma chave pública (o rsa não é bom). Há um botão, **Gerar um par de chaves público/privado** que cria esse par de chaves para você. Salve as chaves pública e privada.
1. Navegue até a API de gerenciamento de usuários.
1. Gere um token de acesso (ou token de portador) colando o conteúdo da sua chave privada na caixa de texto e clicando em **Gerar token**.
1. Salve com segurança todas essas informações, como **ID do Cliente**, **Segredo do Cliente**, **ID da Conta Técnica**, **Email da Conta Técnica**, **ID da Organização** e **Token de Acesso**.

## Acessando a Interface do Usuário para a Ferramenta de Mapeamento do Usuário {#user-interface}

A Ferramenta de mapeamento de usuários é integrada à Ferramenta de transferência de conteúdo. Você pode baixar a Ferramenta de Transferência de Conteúdo do [Portal de Distribuição de Software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html). Para obter mais detalhes sobre a versão mais recente, consulte [Notas de versão atuais](/help/release-notes/release-notes-cloud/release-notes-current.md).

1. Selecione o Adobe Experience Manager e navegue até Ferramentas > **Operações** > **Migração de conteúdo**.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-access1.png)

1. Clique no cartão **Mapeamento de Usuário**.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-access2.png)

1. Clique em **Criar configuração de mapeamento de usuário**.

   >[!NOTE]
   >Se você ignorar essa etapa, o mapeamento de usuários e grupos será ignorado durante a fase de Extração.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-access5.png)

   Preencha os campos em **Configuração da API de gerenciamento de usuários**, conforme descrito abaixo.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-access3.png)


   * **ID da Organização**: insira a ID da Organização do Adobe Identity Management System (IMS) da organização para a qual os usuários estão sendo migrados.

     >[!NOTE]
     >Para obter a ID da organização, faça logon no [Admin Console](https://adminconsole.adobe.com/) e escolha sua organização (na área superior direita) se você pertencer a mais de uma. A ID da organização está na URL dessa página, no formato como `xx@AdobeOrg`, onde xx é a ID da organização IMS. Como alternativa, você pode encontrar a ID da organização na página [Adobe Developer Console](https://developer.adobe.com/console/) onde gera o token de acesso.

   * **ID do Cliente**: Insira a ID do Cliente que você salvou da etapa de Instalação.

   * **Token de acesso**: insira o Token de acesso salvo na etapa de Instalação.

     >[!NOTE]
     >O token de acesso expira a cada 24 horas e um novo deve ser criado. Para criar um token, volte para a [Adobe Developer Console](https://developer.adobe.com/console/), escolha seu projeto, clique na **API de Gerenciamento de Usuários** e cole a mesma chave privada na caixa.

1. Depois de preencher os campos, clique em **Testar Configuração** para testar a conexão com o serviço da API de Gerenciamento de Usuários. Se a conexão for bem-sucedida, você pode clicar em **Salvar** para salvar a configuração.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-access4.png)

1. Depois de salvar a configuração, selecione-a e clique em **Iniciar mapeamento de usuário**.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-landing4.png)

1. Clique em **Iniciar** na caixa de diálogo para iniciar o processo de Mapeamento de Usuário.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-user-mapping/resume-user-mapping3.png)

   Ele exibe o **Status** como **RUNNING**.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-start1.png)


1. Após a conclusão do Mapeamento de Usuários, clique em **Resultados** para exibir o resumo.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-landing5.png)

   >[!IMPORTANT]
   >
   >* Após a conclusão do Mapeamento de usuários, você pode navegar de volta para a página Migração de conteúdo usando a navegação estrutural. O cartão Mapeamento de usuário exibe o status e o carimbo de data e hora. Clique em **Transferência de conteúdo** para criar um Conjunto de migração para executar a extração. Consulte [Executando a Ferramenta de Transferência de Conteúdo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html#running-tool) para obter mais detalhes.

### Retomando o Processo de Mapeamento de Usuário {#resume-user-mapping-process}

Se o processo de Mapeamento de usuário for interrompido devido a um dos seguintes motivos:

* A opção **Parar Mapeamento de Usuário** foi selecionada pelo usuário.
* O token de acesso expirou durante o processo.
* Ou por alguma outra razão.

  >[!NOTE]
  >O progresso é salvo de onde o processo foi interrompido.

Siga as etapas abaixo para retomar o processo de Mapeamento de Usuários:

1. Clique em **Exibir Log** para examinar o log de Mapeamento de Usuário para que você possa verificar o progresso salvo.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-user-mapping/resume-user-mapping1.png)

1. Clique no botão **Iniciar Mapeamento de Usuário** novamente para retomar de onde parou.

   >[!NOTE]
   >Antes de reiniciar, verifique se o token de acesso ainda é válido ou se foi atualizado.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-user-mapping/resume-user-mapping2.png)

1. Clique em **Iniciar** na caixa de diálogo para retomar o processo de Mapeamento de Usuário.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-user-mapping/resume-user-mapping3.png)

   Depois que o processo de Mapeamento de Usuário for concluído, você poderá exibir o **Status** como **CONCLUÍDO** para essa configuração específica.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-user-mapping/resume-user-mapping4.png)
