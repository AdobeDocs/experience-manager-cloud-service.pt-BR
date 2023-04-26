---
title: Usar a ferramenta Mapeamento de usuários (herdada)
description: Usar a ferramenta Mapeamento de usuários (herdada)
exl-id: dcb750c4-0f81-4d11-ac6c-0592162b683d
hide: true
hidefromtoc: true
source-git-commit: 154c3eb3dbee07e830f489212777540a18c952b3
workflow-type: tm+mt
source-wordcount: '842'
ht-degree: 3%

---

# Usar a ferramenta Mapeamento de usuários (herdada) {#using-user-mapping-tool}

>[!INFO]
>
>Esta documentação se refere a uma versão obsoleta dessa ferramenta. Para obter mais informações sobre a versão mais recente, consulte [Mapeamento de usuários e migração principal](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/user-mapping-and-migration.md).

A Ferramenta de mapeamento de usuários usa uma API que permite procurar usuários do Adobe Identity Management System (IMS) por email e retornar suas IDs IMS. Essa API exige que o usuário crie uma ID do cliente para sua organização, um Segredo do cliente e um Token de acesso ou portador.

## Configurar a ferramenta Mapeamento de usuários {#setting-up-user-mapping}

**Pré-requisito:** O mapeamento de usuário exige que cada usuário seja mapeado para sua ID IMS tenha um endereço de email no perfil no AEM e no IMS.  Observe que mesmo que o usuário use um endereço de email como ID de usuário para fazer logon, o mapeamento não funcionará para esse usuário, a menos que o endereço de email também esteja no perfil e também no IMS.

Siga as etapas abaixo para configurar isso:

1. Navegar para [Console do Adobe Developer](https://console.adobe.io) usando sua Adobe ID.
1. Crie um novo projeto ou abra um projeto existente.
1. Adicionar uma API - Clique **Adicionar ao projeto** e selecione **API**
1. Escolha a API de gerenciamento de usuários.  Você deve ter permissões de Administrador do sistema para ter essa opção disponível.
1. Crie uma credencial JWT.
1. Gere um par de chaves ou Carregue uma chave pública (rsa não está bom).  Há um botão. **Gerar um par de chaves público/privado**, o que fará isso por você.  Salve as chaves públicas e privadas.
1. Navegue até a API de gerenciamento de usuários.
1. Gere um token de acesso (ou token portador) colando seu conteúdo de chave privada na caixa de texto e clicando em **Gerar token**.
1. Salve todas essas informações, como **ID do cliente**, **Segredo do cliente**, **ID da conta técnica**, **Email da conta técnica**, **ID da organização** e **Token de acesso** em segurança.

## Acessar a interface do usuário para a ferramenta Mapeamento de usuário {#user-interface}

A Ferramenta de mapeamento de usuários é integrada à Ferramenta de transferência de conteúdo. Você pode baixar a ferramenta Transferência de conteúdo em [Portal de distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html). Para obter mais detalhes sobre a versão mais recente, consulte [Notas de versão atuais](/help/release-notes/release-notes-cloud/release-notes-current.md).

1. Selecione o Adobe Experience Manager e navegue até as ferramentas -> **Operações** -> **Migração de conteúdo**.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-access1.png)

1. Clique em **Mapeamento de usuários** cartão.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-access2.png)

1. Clique em **Criar configuração de mapeamento de usuário**.

   >[!NOTE]
   >Se você ignorar esta etapa, o mapeamento de usuários e grupos será ignorado durante a fase de Extração.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-access5.png)

   Preencha os campos em **Configuração da API de gerenciamento de usuários**, conforme descrito abaixo.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-access3.png)


   * **ID da organização**: Insira a ID da organização do Sistema Adobe Identity Management (IMS) para a organização na qual os usuários estão sendo migrados.

      >[!NOTE]
      >Para obter a ID da organização, faça logon na [Admin Console](https://adminconsole.adobe.com/) e escolha sua organização (na área superior direita) se você pertencer a mais de uma. A ID da organização estará no URL dessa página, no formato como `xx@AdobeOrg`, onde xx é a ID organizacional IMS.  Como alternativa, você pode encontrar a ID da organização na variável [Console do Adobe Developer](https://console.adobe.io) página onde você gera o Token de acesso.

   * **ID do cliente**: Insira a ID do cliente que você salvou na etapa Configuração .

   * **Token de acesso**: Insira o Token de acesso que você salvou na etapa Configuração.

      >[!NOTE]
      >O Token de acesso expira a cada 24 horas e um novo precisa ser criado. Para criar um novo token, volte para [Console do Adobe Developer](https://console.adobe.io), escolha o projeto, clique em **API de gerenciamento de usuários** e cole a mesma chave privada na caixa.

1. Depois de preencher os campos, clique em **Testar configuração** para testar a conexão com o serviço da API de gerenciamento de usuários. Se a conexão for bem-sucedida, você poderá clicar em **Salvar** para salvar a configuração.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-access4.png)

1. Depois de salvar a configuração, selecione a configuração e clique em **Iniciar mapeamento de usuário**.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-landing4.png)

1. Clique em **Iniciar** na caixa de diálogo para iniciar o processo de Mapeamento de usuários.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-user-mapping/resume-user-mapping3.png)

   Ele exibe a variável **Status** as **EM EXECUÇÃO**.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-start1.png)


1. Depois que o Mapeamento do usuário for concluído, clique em **Resultados** para exibir o resumo.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-landing5.png)

   >[!IMPORTANT]
   >* Quando o Mapeamento de usuários for concluído, você poderá navegar de volta para a página Migração de conteúdo usando a navegação estrutural. O cartão Mapeamento de usuário exibe o status e o carimbo de data e hora. Clique em **Transferência de conteúdo** para criar um Conjunto de migração para executar a extração. Consulte [Execução da ferramenta Transferência de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#running-tool) para obter mais detalhes.


### Retomando o processo de mapeamento de usuários {#resume-user-mapping-process}

Se o processo de Mapeamento de Usuário for interrompido por um dos seguintes motivos:

* O usuário selecionado **Parar Mapeamento de Usuários**
* o token de acesso expirado durante o processo ou
* alguma outra razão

   >[!NOTE]
   >O progresso é salvo de onde o processo parou.

Siga as etapas abaixo para retomar o processo de Mapeamento de usuários:

1. Clique em **Exibir registro** para revisar o log de Mapeamento de Usuário para verificar o progresso salvo.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-user-mapping/resume-user-mapping1.png)

1. Clique no botão **Iniciar mapeamento de usuário** novamente para retomar de onde parou.

   >[!NOTE]
   >Antes de reiniciar, verifique se o token de acesso ainda é válido ou foi atualizado.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-user-mapping/resume-user-mapping2.png)

1. Clique em **Iniciar** na caixa de diálogo para retomar o processo de Mapeamento de usuários.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-user-mapping/resume-user-mapping3.png)

   Depois que o processo de Mapeamento de usuários for concluído, você exibirá a variável **Status** as **CONCLUÍDO** para essa configuração específica.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-user-mapping/resume-user-mapping4.png)
