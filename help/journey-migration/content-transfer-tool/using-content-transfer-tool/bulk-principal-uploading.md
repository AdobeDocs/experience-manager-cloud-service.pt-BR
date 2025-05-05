---
title: Upload em massa de entidades de segurança para o IMS após o uso da CTT
description: Visão geral dos arquivos de upload em massa para grupos e usuários e como usá-los no Admin Console para criar grupos e usuários no IMS.
exl-id: 43ebd6f1-1492-461a-8d9b-2b55dcde9052
source-git-commit: b9c739a03b358de7c011e50ddbdd609c90f86b6f
workflow-type: tm+mt
source-wordcount: '2384'
ht-degree: 3%

---

# Upload em massa de principais para IMS após o uso da CTT {#bulk-principal-uploading}

>[!CONTEXTUALHELP]
>id="bulk-principal-uploading"
>title="Upload em massa de principais"
>abstract="Visão geral dos arquivos de upload em massa para grupos e usuários e como usá-los no Admin Console para criar grupos e usuários no IMS."
>additional-url="https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/onboarding/journey/admin-console" text="Documentação do Admin Console do AEM"
>additional-url="https://adminconsole.adobe.com/" text="Admin Console do AEM"

## Introdução {#introduction}

A migração de conteúdo para a nuvem usando CTT e CAM cria grupos na instância da nuvem do AEM, mas não pode fazer nada para colocar grupos ou usuários no IMS. Eles precisam existir no IMS para serem gerenciados corretamente pelos clientes. Felizmente, há uma funcionalidade fornecida pela Admin Console para criar grupos e usuários de IMS em massa. A assimilação de CAM ajuda esse processo, salvando arquivos de entrada para essa criação em massa, permitindo que os clientes concluam essa ação do Admin Console como parte de seu processo de migração geral. Dois tipos de arquivos de upload em massa são criados: um para grupos e um para usuários.

Consulte também [Gerenciar usuários](https://helpx.adobe.com/br/enterprise/using/users.html) para obter detalhes adicionais sobre como gerenciar usuários do AEM as a Cloud Service.

## Regras gerais para o upload de arquivos {#rules}

Há algumas diretrizes gerais para editar e usar os dois tipos de arquivos de upload:

* O acesso de administrador à Admin Console deve ser concedido primeiro para que essas instruções possam ser seguidas.
* Observe que há algumas maneiras diferentes de criar usuários e grupos no IMS.  Consulte [Suporte IMS para Adobe Experience Manager as a Cloud Service](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/security/ims-support) para saber mais sobre todas as opções disponíveis.  Somente os métodos de upload em massa do Admin Console são descritos aqui.
* Há três tipos de identidade possíveis no IMS: Adobe ID, Enterprise ID e Federated ID.  As instruções nesta página são fornecidas somente para **Adobe ID**.  Se você precisar usar o Enterprise ID ou o Federated ID, consulte a [documentação completa do Admin Console](https://helpx.adobe.com/ca/enterprise/using/admin-console.html) e também a documentação específica para o [upload de Grupo em Massa do Admin Console](https://helpx.adobe.com/ca/enterprise/using/user-groups.html) e o [upload de Usuário em Massa do Admin Console](https://helpx.adobe.com/ca/enterprise/using/bulk-upload-users.html).  As especificações para os arquivos de upload são um pouco diferentes para esses dois tipos de identidade.
* Se um único campo CSV permitir várias entradas (como vários perfis de produto, vários grupos ou vários administradores), as entradas deverão estar contidas entre aspas duplas e separadas por vírgula, ou seja, `"profile 1,profile 2"`.

   * Aspas simples podem ser usadas para esse caso, em vez de aspas duplas, mas editar o arquivo no Microsoft Excel pode resultar em problemas de análise. Se estiver usando o Excel para editar esses arquivos, certifique-se de usar aspas duplas em vez de aspas simples.

## Upload de grupo em massa {#group-upload}

#### Caso de uso: os grupos foram migrados para o AEM as a Cloud Service, mas não estão presentes no IMS/Admin Console, portanto, precisam ser carregados para o IMS por meio da Admin Console.

Para usar a funcionalidade de upload de grupo em massa do Admin Console depois de executar uma migração CTT/CAM, siga estas etapas:
1. Baixar o arquivo de grupo em massa do CAM

   1. No CAM, vá para **Transferência de conteúdo** e selecione **Trabalhos de assimilação**.
   1. Clique nas reticências (...) na linha da Assimilação em questão e escolha **Exibir resumo principal**.
   1. Na caixa de diálogo exibida, selecione **Arquivo de Grupo em Massa** na lista suspensa em **Baixar um arquivo...** e clique no botão **Download**.
   1. Salve o arquivo CSV resultante.

1. Editar o arquivo de grupo em massa

   * Cada linha representa um grupo a ser carregado e tem quatro campos (os nomes dos campos constituem a primeira linha do arquivo):

      * _Nome do Grupo de Usuários_ - O nome do grupo é obrigatório e pode conter no máximo 255 caracteres.  Esse nome de grupo deve ser o mesmo no IMS e no AEM
      * _Descrição_ - Este campo é opcional e pode conter no máximo 255 caracteres
      * _Administradores do grupo de usuários_ - Pelo menos um administrador de grupo deve ser incluído neste campo. Vários administradores podem ser atribuídos separando cada administrador com uma vírgula e colocando a lista entre aspas. A entrada para cada administrador deve incluir o tipo de identidade do usuário, seguido por um hífen e, em seguida, o endereço de email.  Por exemplo

        `"Adobe ID-myAdmin@example.com,Adobe ID-myOtherAdmin@example.com"`. Não inclua um espaço após a vírgula que separa os administradores. Não é possível incluir usuários (como administradores) que não façam parte da organização no Admin Console
      * _Perfis de produto atribuídos_ - Este campo é opcional. É possível atribuir vários perfis de produto separando cada perfil com uma vírgula e colocando a lista entre aspas. No entanto, os perfis de produto incluídos já devem estar configurados para a organização. Certifique-se de especificar o nome do Perfil do produto, e não o nome do produto.  A associação de Perfis de produto atribuídos a um grupo será herdada por todos os usuários colocados nesse grupo.  Para localizar um perfil de produto:

         1. Ir para o Admin Console
         1. Encontre seu produto (ou seja, o Adobe Experience Manager as a Cloud Service) e clique nele
         1. Encontre seu ambiente (instância) e clique nele
         1. Liste os Perfis de produto e clique naquele do ambiente do AEM. O perfil de produto está no topo, ou seja, &quot;_Usuários do AEM - autor - Programa 12345 - Ambiente 012345_&quot;.

   * Ao editar o CSV, alguns aplicativos podem adicionar aspas extras ao salvar, o que faz com que o processamento falhe. É uma boa prática inspecionar o CSV bruto em um editor de texto simples para garantir que cada campo tenha apenas uma aspa de abertura e uma aspa de fechamento (e elas não devem ser &quot;aspas inteligentes&quot;).

1. Fazer upload do arquivo de grupo em massa na Admin Console

   1. Na Admin Console, vá para **Usuários** e, em seguida, **Grupos de Usuários**
   1. No lado direito, clique no botão &quot;...&quot;. Escolha **Adicionar grupos de usuários por CSV** no menu e escolha o CSV para carregar. Clique em **Carregar**
   1. Você receberá uma resposta informando que o CSV foi carregado (para o Admin Console), mas ainda não foi importado para o IMS
   1. Vá para o mesmo menu &quot;...&quot; e escolha **Resultados da operação em massa**. Ele mostrará uma lista de tentativas de carregamento em massa e informará (em **Status**) se o carregamento em massa está sendo processado, foi bem-sucedido ou falhou

      * No início, ele mostrará Processamento, indicando que ainda não foi concluído
      * Depois de concluído com êxito, clique no link **Adicionar grupos de usuários** para ver uma mensagem de status simples para cada linha.
      * Se, em vez disso, ele falhar, clique no ícone pequeno em **Arquivo** e ele fornecerá um pouco mais de informações sobre por que falhou.  Os números de linha de grupo são referenciados começando na linha 1.
1. Use o Admin Console para verificar suas alterações.

## Upload e edição de usuários em massa {#bulk-user}

O Admin Console inclui duas ações separadas para carregar e editar detalhes do usuário. As instruções imediatamente abaixo são para adicionar novos usuários ao IMS. As instruções para editar usuários do IMS existentes estão na seguinte seção chamada [Edição de usuário em massa](#user-edit).

### Upload de usuário em massa {#user-upload}

#### Caso de uso: os grupos foram migrados para o AEM as a Cloud Service e carregados por upload em massa ou por algum outro método.  Os usuários podem não estar presentes no IMS/Admin Console, portanto, eles precisam ser carregados e vinculados a seus grupos no IMS por meio da Admin Console.

>[!NOTE]
>
>Um usuário aparecerá no arquivo **Upload de usuário em massa** se ele estiver em um grupo assimilado durante a mesma assimilação da qual o arquivo foi criado. Ela também pode aparecer se o usuário estiver diretamente em uma ACL ou CUG do conteúdo migrado, ou se for membro de um grupo integrado ou local que esteja em uma ACL ou CUG do conteúdo migrado. Consulte [Migração de grupo](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/group-migration.md) para obter mais informações sobre esses casos.

Para usar a funcionalidade de upload de usuários em massa do Admin Console, siga estas etapas:

1. Baixar o arquivo de usuário em massa do CAM
   1. No CAM, vá para **Transferência de conteúdo** e selecione **Trabalhos de assimilação**.
   1. Clique nas reticências (...) na linha da Assimilação em questão e escolha **Exibir resumo principal**.
   1. Na caixa de diálogo exibida, selecione **Arquivo de Usuário em Massa** na lista suspensa em **Baixar um arquivo...** e clique no botão **Baixar**.
   1. Salvar o arquivo CSV resultante
1. Editar o arquivo de usuário em massa
   * Cada linha representa um usuário a ser carregado e tem quinze campos (os nomes dos campos constituem a primeira linha do arquivo). Alguns campos são opcionais e não estão descritos aqui. Consulte [Formato CSV de Usuário em Massa](https://helpx.adobe.com/enterprise/using/bulk-upload-users.html#csv-format).  Os campos são:

      * _Tipo De Identidade_ - Opcional.  Se não for especificado, será criado como um Adobe ID
      * _Nome de usuário_ - Opcional e não usado para carregamentos do Adobe ID
      * _Domínio_ - Opcional e não usado para carregamentos do Adobe ID
      * _Email_ - Obrigatório.  O endereço de email será usado para verificação na primeira vez que o usuário fizer logon
      * _Nome_ - Opcional.  Deve ser usado porque aparece, com Sobrenome, em vários lugares
      * _Sobrenome_ - Opcional.  Deve ser usado porque aparece em vários lugares
      * _Código do país_ - Opcional e não usado para carregamentos do Adobe ID
      * _ID_ - Opcional e não usado para carregamentos do Adobe ID
      * _Configurações de produto_ - Opcional. Este campo também será herdado de qualquer grupo do qual o usuário seja membro
      * _Funções de administrador_ - Opcional. Use este campo se o usuário for um Administrador. Consulte [Formato CSV de usuário em massa](https://helpx.adobe.com/enterprise/using/bulk-upload-users.html#csv-format) para obter detalhes
      * _Configurações de Produto Administradas_ - Opcional.  Consulte [Formato CSV de Usuário em Massa](https://helpx.adobe.com/enterprise/using/bulk-upload-users.html#csv-format) para obter detalhes. Este campo também será herdado de qualquer grupo do qual o usuário seja membro
      * _Grupos de Usuários_ - Opcional. Uma lista de grupos aos quais o usuário deve ser atribuído como membro. Cada grupo deve ser um grupo IMS já existente. Quando o arquivo de usuário em massa é baixado do CAM, esse campo é pré-preenchido com nomes de grupo habilitado para IMS do qual o usuário era membro (direta ou indiretamente) antes da migração
      * _Grupos De Usuários Administrados_ - Opcional.  Consulte [Formato CSV de Usuário em Massa](https://helpx.adobe.com/enterprise/using/bulk-upload-users.html#csv-format) para obter detalhes. Este campo também será herdado de qualquer grupo do qual o usuário seja membro
      * _Produtos Administrados_ - Opcional.  Consulte [Formato CSV de Usuário em Massa](https://helpx.adobe.com/enterprise/using/bulk-upload-users.html#csv-format) para obter detalhes. Este campo também será herdado de qualquer grupo do qual o usuário seja membro
      * _Contratos Administrados_ - Opcional.  Consulte [Formato CSV de usuário em massa](https://helpx.adobe.com/enterprise/using/bulk-upload-users.html#csv-format) para obter detalhes
      * _Acesso do Desenvolvedor_ - Opcional.  Consulte [Formato CSV de usuário em massa](https://helpx.adobe.com/enterprise/using/bulk-upload-users.html#csv-format) para obter detalhes
      * _Produtos Atribuídos Automaticamente_ - Opcional.  Consulte [Formato CSV de usuário em massa](https://helpx.adobe.com/enterprise/using/bulk-upload-users.html#csv-format) para obter detalhes

   * Ao editar o CSV, alguns aplicativos podem adicionar aspas extras ao salvar, o que faz com que o processamento falhe. É uma boa prática inspecionar o CSV bruto em um editor de texto simples para garantir que cada campo tenha apenas uma aspa de abertura e uma de fechamento (e elas não devem ser &quot;aspas inteligentes&quot;)

1. Usar o Admin Console para importar o arquivo de usuário em massa

   1. No Admin Console, acesse Usuários
   1. Clique no botão **Adicionar usuários por CSV**
   1. Arraste e solte ou selecione um arquivo CSV de usuário em massa baixado do CAM
   1. Clique no botão **Carregar**
   1. Você receberá uma resposta informando que o CSV foi carregado (para o Admin Console), mas ainda não foi importado para o IMS.
   1. Vá para o menu &quot;...&quot; à direita e escolha **Resultados da operação em massa**.  Ele mostrará uma lista de tentativas de carregamento em massa e exibirá (em **Status**) se o carregamento em massa está sendo processado, bem-sucedido ou falhou.

      * No início, ele mostrará Processamento, indicando que ainda não foi concluído
      * Depois de concluído com êxito, clique no link **Adicionar usuários** para ver uma mensagem de status simples para cada linha
      * Se, em vez disso, ele falhar, clique no ícone pequeno em **Arquivo** e ele lhe dará um pouco mais de informações sobre por que falhou. Os números de linha do usuário são referenciados começando na linha 1.

1. Use o Admin Console para verificar suas alterações.

>[!NOTE]
>
>Após uma assimilação sem limpeza, é possível que os usuários que foram migrados anteriormente e criados no IMS apareçam no arquivo Upload de usuário em massa. Isso pode ocorrer por várias razões. Nesse caso, o upload do usuário novamente falhará. Em vez disso, tente remover o usuário do arquivo de Upload de usuário em massa e, se o usuário precisar ser adicionado a grupos diferentes, use o arquivo de Edição de usuário em massa conforme descrito abaixo.

### Edição de usuário em massa {#user-edit}

#### Caso de uso: grupos e usuários foram migrados para o AEM as a Cloud Service e carregados por upload em massa ou por algum outro método. Agora, algumas alterações precisam ser feitas a vários usuários de uma só vez, como adicioná-las a um grupo IMS existente.

Para usar a funcionalidade de edição de usuários em massa do Admin Console, siga estas etapas:

1. Baixar o arquivo de usuário em massa do Admin Console

   1. No Admin Console, acesse Usuários
   1. No lado direito, clique no botão &quot;...&quot;.  Escolha **Editar detalhes do usuário por CSV** no menu
   1. Clique em **Baixar modelo CSV** e escolha **Usuários atuais**.  Um arquivo CSV deve aparecer na pasta Downloads local.

1. Editar o arquivo de usuário em massa

   1. No Admin Console, acesse Usuários
   1. Edite o arquivo CSV usando um editor de texto (recomendado) ou um aplicativo de planilha, como o Excel. O uso de um aplicativo pode fazer alterações imprevisíveis nos dados. Portanto, recomenda-se que, após todas as edições, um editor de texto seja usado para verificar a formatação do arquivo
   1. As descrições dos campos neste arquivo são as mesmas descritas acima, em Upload de usuário em massa
   1. Remover todos os usuários que não estão sendo editados
   1. Se você alterar o campo Grupos de usuários, deixe os grupos atuais e adicione novos, conforme necessário. Se você remover um grupo existente, o usuário será removido desse grupo no IMS
   1. Ao editar o CSV, alguns aplicativos podem adicionar aspas extras ao salvar, o que faz com que o processamento falhe. É uma boa prática inspecionar o arquivo CSV bruto em um editor de texto simples para garantir que cada campo tenha apenas uma aspa de abertura e uma de fechamento (e elas não devem ser &quot;aspas inteligentes&quot;)

1. Fazer upload do arquivo de usuário em massa na Admin Console

   1. No Admin Console, acesse Usuários
   1. No lado direito, clique no botão &quot;...&quot;. Escolha **Editar detalhes do usuário por CSV** no menu
   1. Arraste e solte ou selecione o arquivo CSV editado do usuário em massa
   1. Clique no botão Upload
   1. Você receberá uma resposta informando que o CSV foi carregado (para o Admin Console), mas ainda não foi importado para o IMS
   1. Vá para o menu &quot;...&quot; à direita e escolha **Resultados da operação em massa**. Ele mostrará uma lista de tentativas de upload em massa e informará (em Status) se o upload em massa está sendo processado, bem-sucedido ou falhou.

      * No início, ele mostrará Processamento, indicando que ainda não foi concluído
      * Depois de concluído com êxito, clique no link **Editar detalhes do usuário** para ver uma mensagem de status simples para cada linha
      * Se, em vez disso, ele falhar, clique no ícone pequeno em **Arquivo** e ele exibirá um pouco mais de informações sobre o motivo da falha. Os números de linha do usuário são referenciados começando na linha 1.

1. Use o Admin Console para verificar suas alterações.
