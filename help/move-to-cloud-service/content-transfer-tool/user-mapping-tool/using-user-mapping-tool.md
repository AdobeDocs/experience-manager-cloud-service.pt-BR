---
title: Usar a ferramenta Mapeamento de usuários
description: Usar a ferramenta Mapeamento de usuários
source-git-commit: 6ab32a952a53eed612192ee8359373087e6cf624
workflow-type: tm+mt
source-wordcount: '680'
ht-degree: 2%

---


# Usar a ferramenta Mapeamento de usuários {#using-user-mapping-tool}

A Ferramenta de mapeamento de usuários usa uma API que permite procurar usuários do Adobe Identity Management System (IMS) por email e retornar suas IDs IMS. Essa API exige que o usuário crie uma ID do cliente para sua organização, um Segredo do cliente e um Token de acesso ou portador.

## Configurar a ferramenta Mapeamento de usuários {#setting-up-user-mapping}

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

## Acessar a interface do usuário para a ferramenta Mapeamento de usuário {#user-interface}

A Ferramenta de mapeamento de usuários é integrada à Ferramenta de transferência de conteúdo. Você pode baixar a ferramenta Transferência de conteúdo no [Portal de distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html). Para obter mais detalhes sobre a versão mais recente, consulte as [Notas de versão atuais](/help/release-notes/release-notes-cloud/release-notes-current.md).

1. Selecione o Adobe Experience Manager e navegue até Ferramentas -> **Operações** -> **Migração de Conteúdo**.

   ![imagem](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-access1.png)

1. Clique no cartão **Mapeamento de Usuário**.

   ![imagem](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-access2.png)

1. Clique em **Criar configuração de mapeamento de usuário**.

   >[!NOTE]
   >Se você ignorar esta etapa, o mapeamento de usuários e grupos será ignorado durante a fase de Extração.

   ![imagem](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-access5.png)

   Preencha os campos em **User Management API Configuration**, conforme descrito abaixo.

   ![imagem](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-access3.png)


   * **ID** da organização: Insira a ID da organização do Sistema Adobe Identity Management (IMS) para a organização na qual os usuários estão sendo migrados.

      >[!NOTE]
      >Para obter a ID da organização, faça logon no [Admin Console](https://adminconsole.adobe.com/) e escolha sua organização (na área superior direita) se você pertencer a mais de uma. A ID da organização estará no URL dessa página, no formato como `xx@AdobeOrg`, onde xx é a ID da organização IMS.  Como alternativa, você pode encontrar a ID da organização na página [Console do desenvolvedor do Adobe](https://console.adobe.io) onde gera o Token de acesso.

   * **ID** do cliente: Insira a ID do cliente que você salvou na etapa Configuração .

   * **Token** de acesso: Insira o Token de acesso que você salvou na etapa Configuração.

      >[!NOTE]
      >O Token de acesso expira a cada 24 horas e um novo precisa ser criado. Para criar um novo token, volte para [Console do Desenvolvedor do Adobe](https://console.adobe.io), escolha seu projeto, clique em **API do Gerenciamento de Usuário** e cole a mesma chave privada na caixa.

1. Depois de preencher os campos, clique em **Testar configuração** para testar a conexão com o serviço de API de Gerenciamento de Usuário. Se a conexão for bem-sucedida, você poderá clicar em **Save** para salvar a configuração.

   ![imagem](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-access4.png)

1. Depois de salvar a configuração, selecione a configuração e clique em **Iniciar mapeamento de usuários**.

   ![imagem](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-landing4.png)

1. Depois que o Mapeamento do usuário for concluído, clique em **Resultados** para exibir o resumo.

   ![imagem](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-landing5.png)

   >[!IMPORTANT]
   >* Quando o Mapeamento de usuários for concluído, você poderá navegar de volta para a página Migração de conteúdo usando a navegação estrutural. O cartão Mapeamento de usuário exibe o status e o carimbo de data e hora. Clique em **Transferência de conteúdo** para criar um Conjunto de migração para executar a extração. Consulte [Execução da ferramenta Transferência de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#running-tool) para obter mais detalhes.


### Retomando o processo de mapeamento de usuários {#resume-user-mapping}

Se o processo de Mapeamento de Usuário for interrompido por um dos seguintes motivos:

* O usuário selecionou **Parar o mapeamento de usuários**
* o token de acesso expirado durante o processo ou
* outra razão.

O progresso é salvo de onde o processo parou. Revise o log de Mapeamento de Usuário para verificar o progresso salvo. Clique novamente no botão **Iniciar mapeamento de usuários** para retomar de onde parou. Antes de reiniciar, verifique se o token de acesso ainda é válido ou foi atualizado.
