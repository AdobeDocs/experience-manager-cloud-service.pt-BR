---
title: Introdução à ferramenta Transferência de conteúdo (herdado)
description: Introdução à ferramenta Transferência de conteúdo
hide: true
hidefromtoc: true
exl-id: a6ee6996-510e-42d7-9a7c-f64732764f97
source-git-commit: 22bbf15e33ab3d5608dc01ed293bb04b07cb6c8c
workflow-type: tm+mt
source-wordcount: '966'
ht-degree: 22%

---

# Introdução à ferramenta Transferência de conteúdo (herdado) {#getting-started-content-transfer-tool}


## Disponibilidade {#availability}

A ferramenta Transferência de conteúdo pode ser baixada como um arquivo zip no Portal de distribuição de software. Você pode instalar o pacote via [Gerenciador de pacotes](/help/implementing/developing/tools/package-manager.md) na instância de origem do Adobe Experience Manager (AEM). Faça o download da versão mais recente. Para obter mais detalhes sobre a versão mais recente, consulte [Notas de versão](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=pt-BR).

>[!NOTE]
>Baixe a ferramenta Transferência de conteúdo no [Portal de distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html).

## Conectividade do ambiente de origem {#source-environment-connectivity}

A instância de AEM de origem pode estar em execução atrás de um firewall em que só pode alcançar determinados hosts que foram adicionados a uma Lista de permissões. Para executar com êxito uma extração, os seguintes endpoints precisarão ser acessíveis da instância que está executando AEM:

* O público-alvo AEM ambiente as a Cloud Service: `author-p<program_id>-e<env_id>.adobeaemcloud.com`
* O serviço de armazenamento de blobs do Azure: `*.blob.core.windows.net`
* O ponto de extremidade de E/S de Mapeamento de Usuário: `usermanagement.adobe.io`

Para testar a conectividade com o ambiente de destino AEM as a Cloud Service, emita o seguinte comando cURL do shell da instância de origem (substitua `program_id`, `environment_id`e `migration_token`):

`curl -i https://author-p<program_id>-e<environment_id>.adobeaemcloud.com/api/migration/migrationSet -H "Authorization: Bearer <migration_token>"`

>[!NOTE]
>Se uma `HTTP/2 200` for recebida, uma conexão com AEM as a Cloud Service foi bem-sucedida.

## Execução da ferramenta Transferência de conteúdo {#running-tool}

>[!VIDEO](https://video.tv.adobe.com/v/35460/?quality=12&learn=on)


Siga esta seção para saber como usar a ferramenta Transferência de conteúdo para migrar o conteúdo para o AEM as a Cloud Service (Autor/Publicação):

1. Selecione o Adobe Experience Manager e navegue até as ferramentas -> **Operações** -> **Migração de conteúdo**.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/ctt01.png)

1. Selecione o **Transferência de conteúdo** opção de **Migração de conteúdo** assistente.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/ctt02.png)


1. O console abaixo é exibido ao criar o primeiro conjunto de migração. Clique em **Criar conjunto de migração** para criar um novo conjunto de migração.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/ctt03.png)

   >[!NOTE]
   >Se você tiver conjuntos de migração existentes, o console exibirá a lista de conjuntos de migração existentes com seu status atual.


1. Preencha os campos em **Criar conjunto de migração** conforme descrito abaixo.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/ctt04.png)

   1. **Nome**: insira o nome do conjunto de migração.
      >[!NOTE]
      >Nenhum caractere especial é permitido para o nome do conjunto de migração.

   1. **Configuração do Cloud Service**: insira a URL do autor do AEM as a Cloud Service.

      >[!NOTE]
      >Você pode criar e manter no máximo dez conjuntos de migração por vez durante a atividade de transferência de conteúdo.
      >Além disso, é necessário criar uma migração separadamente para cada um dos ambientes específicos - *Preparação*, *Desenvolvimento* ou *Produção*.

   1. **Token de acesso**: insira o token de acesso.

      >[!NOTE]
      >Você pode recuperar o token de acesso usando o **Abrir token de acesso** botão. Você precisa garantir que pertença ao grupo &quot;Administradores&quot; na instância do Cloud Service de destino.

   1. **Parâmetros**: selecione os seguintes parâmetros para criar o conjunto de migração:

      1. **Incluir versão**: selecione conforme necessário. Quando as versões são incluídas, o caminho `/var/audit` é incluído automaticamente para migrar eventos de auditoria.

         ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/ctt05.png)

         >[!NOTE]
         >Se você pretende incluir versões como parte de um conjunto de migração e estiver executando atualizações adicionais com `wipe=false`, você deve desativar a limpeza de versão devido a uma limitação atual na ferramenta Transferência de conteúdo. Se você preferir manter a limpeza de versão ativada e estiver executando os upups em um conjunto de migração, você deverá executar a assimilação como `wipe=true`.


      1. **Caminhos a serem incluídos**: use o navegador de caminhos para selecionar os caminhos que precisam ser migrados. O seletor de caminho aceita entrada digitando ou por seleção.

         >[!IMPORTANT]
         >Os seguintes caminhos estão restritos ao criar um conjunto de migração:
         >* `/apps`
         >* `/libs`
         >* `/home`
         >* `/etc` (alguns `/etc` caminhos podem ser selecionados em CTT)


1. Clique em **Salvar** depois de preencher todos os campos no **Criar conjunto de migração** tela de detalhes.

1. Você visualizará seu conjunto de migração no **Transferência de conteúdo** como mostrado na figura abaixo.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/ctt07.png)

   Todos os conjuntos de migração existentes são exibidos na **Transferência de conteúdo** com seu status atual e informações de status. Você pode ver alguns desses ícones descritos abaixo.

   * Uma *nuvem vermelha* indica que não é possível concluir o processo de extração.
   * A *nuvem verde* indica que você pode concluir o processo de extração.
   * Um *ícone amarelo* indica que você não criou o conjunto de migração existente e o específico é criado por algum outro usuário na mesma instância.

1. Selecione um conjunto de migração e clique em **Propriedades** para exibir ou editar as propriedades do conjunto de migração. Ao editar propriedades, não é possível alterar a variável **Nome do conjunto de migração** ou **URL de serviço**.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/ctt06.png)

### Determinando o tamanho e o espaço em disco do conjunto de migração {#migration-set-size}

Depois de criar um conjunto de migração, é altamente recomendável executar uma verificação de tamanho no conjunto de migração antes de iniciar um processo de Extração.
Ao executar uma verificação de tamanho no conjunto de migração, você poderá:
* Determine se há espaço em disco suficiente no `crx-quickstart` subdiretório para concluir a extração com êxito.
* Determine se o tamanho do conjunto de migração está dentro dos limites do produto suportado e evite ingestões de conteúdo com falha.

Siga as etapas abaixo para executar uma verificação de tamanho:

1. Selecione um conjunto de migração e clique em **Verificar tamanho**.

   ![imagem](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image1.png)

1. Isso abrirá o **Verificar tamanho** caixa de diálogo.

   ![imagem](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image2.png)

1. Clique em **Verificar tamanho** para iniciar o processo. Em seguida, você retornará à exibição de lista do conjunto de migração e verá uma mensagem indicando que **Verificar tamanho** está em execução.

   ![imagem](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image3.png)


1. Uma vez **Verificar tamanho** o processo estiver concluído, o status será alterado para **CONCLUÍDO**. Selecione o mesmo conjunto de migração e clique em **Verificar tamanho** para visualizar os resultados.

   ![imagem](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image4.png)

   Veja abaixo um exemplo de **Verificar tamanho** resulta sem avisos.

   ![imagem](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image5.png)

1. Se a variável **Verificar tamanho** os resultados indicam que há espaço em disco insuficiente e/ou que o conjunto de migração excede os limites do produto, **AVISO** será exibido.

![imagem](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image6.png)

Veja abaixo um exemplo de **Verificar tamanho** resulta com avisos.

![imagem](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image7.png)


## O que vem a seguir {#whats-next}

Depois de aprender a criar um conjunto de migração, agora você está pronto para aprender sobre os Processos de extração e assimilação na ferramenta Transferência de conteúdo. Antes de aprender esses processos, você deve revisar [Lidar com grandes repositórios de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en) para acelerar significativamente as fases de extração e assimilação da atividade de transferência de conteúdo para mover o conteúdo para AEM as a Cloud Service.
