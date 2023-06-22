---
title: Utilização da Ferramenta de mapeamento de usuário (herdada)
description: Utilização da Ferramenta de mapeamento de usuário (herdada)
exl-id: dcb750c4-0f81-4d11-ac6c-0592162b683d
hide: true
hidefromtoc: true
source-git-commit: 1fc57dacbf811070664d5f5aaa591dd705516fa8
workflow-type: tm+mt
source-wordcount: '831'
ht-degree: 2%

---

# Utilização da Ferramenta de mapeamento de usuário (herdada) {#using-user-mapping-tool}

>[!INFO]
>
>Esta documentação se refere a uma versão obsoleta da ferramenta. Para obter mais informações sobre a versão mais recente, consulte [Mapeamento de usuários e migração de entidade de segurança](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/user-mapping-and-migration.md).

A Ferramenta de mapeamento de usuários usa uma API que permite pesquisar usuários do Adobe Identity Management System (IMS) por email e retornar suas IDs de IMS. Essa API exige que o usuário crie uma ID do cliente para sua organização, um Segredo do cliente e um Token de acesso ou portador.

## Configuração da ferramenta Mapeamento de usuários {#setting-up-user-mapping}

**Pré-requisito:** O mapeamento de usuários exige que cada usuário seja mapeado para sua ID IMS tenha um endereço de email em seu perfil no AEM e no IMS. Mesmo que o usuário use um endereço de email como uma ID de usuário para fazer logon, o mapeamento não funcionará para esse usuário, a menos que o endereço de email também esteja no perfil e também no IMS.

Siga as etapas abaixo para configurar isso:

1. Navegue até [Console do Adobe Developer](https://developer.adobe.com/console/) usando sua Adobe ID.
1. Crie um projeto ou abra um projeto existente.
1. Adicionar uma API - Clique **Adicionar ao projeto** e selecione **API**
1. Escolha API de gerenciamento de usuários. Você deve ter permissões de Administrador do sistema para disponibilizar essa opção.
1. Criar uma credencial JWT.
1. Gere um par de chaves ou faça o upload de uma chave pública (o rsa não é bom). Há um botão, **Gerar um par de chaves públicas/privadas** que cria esse par de chaves para você. Salve as chaves pública e privada.
1. Navegue até a API de gerenciamento de usuários.
1. Gere um token de acesso (ou token do portador) colando o conteúdo da chave privada na caixa de texto e clicando em **Gerar token**.
1. Salve todas essas informações, como **ID do cliente**, **Segredo do cliente**, **ID da conta técnica**, **Email da conta técnica**, **ID da organização**, e **Token de acesso** com segurança.

## Acessando a Interface do Usuário para a Ferramenta de Mapeamento do Usuário {#user-interface}

A Ferramenta de mapeamento de usuários é integrada à Ferramenta de transferência de conteúdo. É possível baixar a ferramenta Transferência de conteúdo em [Portal de distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html). Para obter mais informações sobre a versão mais recente, consulte o [Notas de versão atuais](/help/release-notes/release-notes-cloud/release-notes-current.md).

1. Selecione o Adobe Experience Manager e navegue até ferramentas -> **Operações** -> **Migração de conteúdo**.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-access1.png)

1. Clique em **Mapeamento de usuários** cartão.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-access2.png)

1. Clique em **Criar configuração de mapeamento de usuário**.

   >[!NOTE]
   >Se você ignorar essa etapa, o mapeamento de usuários e grupos será ignorado durante a fase de Extração.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-access5.png)

   Preencha os campos em **Configuração da API de gerenciamento de usuários**, conforme descrito abaixo.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-access3.png)


   * **ID da organização**: digite a ID da organização da Adobe Identity Management System (IMS) da organização para a qual os usuários estão sendo migrados.

     >[!NOTE]
     >Para obter a ID da organização, faça logon na [Admin Console](https://adminconsole.adobe.com/) e escolha sua organização (na área superior direita) se pertencer a mais de uma. A ID da organização está no URL dessa página, no formato como `xx@AdobeOrg`, em que xx é a ID organizacional IMS. Como alternativa, você pode encontrar a ID da organização na [Console do Adobe Developer](https://developer.adobe.com/console/) página na qual você gera o token de acesso.

   * **ID do cliente**: digite a ID do cliente que você salvou na etapa de configuração.

   * **Token de acesso**: Insira o token de acesso salvo na etapa de Configuração.

     >[!NOTE]
     >O token de acesso expira a cada 24 horas e um novo deve ser criado. Para criar um token, volte para [Console do Adobe Developer](https://developer.adobe.com/console/)escolha seu projeto e clique em **API de gerenciamento de usuários** e cole a mesma chave privada na caixa.

1. Depois de preencher os campos, clique em **Testar configuração** para testar a conexão com o serviço de API de gerenciamento de usuários. Se a conexão for bem-sucedida, você pode clicar em **Salvar** para salvar a configuração.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-access4.png)

1. Depois de salvar a configuração, selecione-a e clique em **Iniciar mapeamento de usuário**.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-landing4.png)

1. Clique em **Início** na caixa de diálogo para iniciar o processo de Mapeamento de usuários.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-user-mapping/resume-user-mapping3.png)

   Ele exibe a variável **Status** as **EM EXECUÇÃO**.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-start1.png)


1. Após a conclusão do Mapeamento de usuários, clique em **Resultados** para exibir o resumo.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-landing5.png)

   >[!IMPORTANT]
   >
   >* Após a conclusão do Mapeamento de usuários, você pode navegar de volta para a página Migração de conteúdo usando a navegação estrutural. O cartão Mapeamento de usuário exibe o status e o carimbo de data e hora. Clique em **Transferência de conteúdo** para que você possa criar um Conjunto de migração para executar a extração. Consulte [Execução da ferramenta Transferência de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=en#running-tool) para obter mais detalhes.

### Retomando o Processo de Mapeamento de Usuário {#resume-user-mapping-process}

Se o processo de Mapeamento de usuário for interrompido devido a um dos seguintes motivos:

* A opção **Interromper mapeamento de usuários** foi selecionado pelo usuário.
* O token de acesso expirou durante o processo.
* Ou por alguma outra razão.

  >[!NOTE]
  >O progresso é salvo de onde o processo foi interrompido.

Siga as etapas abaixo para retomar o processo de Mapeamento de Usuários:

1. Clique em **Exibir registro** para revisar o log de Mapeamento do usuário e verificar o progresso salvo.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-user-mapping/resume-user-mapping1.png)

1. Clique em **Iniciar mapeamento de usuário** botão novamente para retomar de onde parou.

   >[!NOTE]
   >Antes de reiniciar, verifique se o token de acesso ainda é válido ou se foi atualizado.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-user-mapping/resume-user-mapping2.png)

1. Clique em **Início** na caixa de diálogo para retomar o processo de Mapeamento de usuários.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-user-mapping/resume-user-mapping3.png)

   Depois que o processo de Mapeamento de usuários for concluído, você poderá exibir a **Status** as **CONCLUÍDO** para essa configuração específica.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-user-mapping/resume-user-mapping4.png)
