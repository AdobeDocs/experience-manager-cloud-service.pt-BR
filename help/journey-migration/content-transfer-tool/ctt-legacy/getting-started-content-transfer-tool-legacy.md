---
title: Introdução à ferramenta Transferência de conteúdo (herdado)
description: Introdução à ferramenta Transferência de conteúdo
hide: true
hidefromtoc: true
exl-id: a6ee6996-510e-42d7-9a7c-f64732764f97
source-git-commit: 22bbf15e33ab3d5608dc01ed293bb04b07cb6c8c
workflow-type: tm+mt
source-wordcount: '966'
ht-degree: 24%

---

# Introdução à ferramenta Transferência de conteúdo (herdado) {#getting-started-content-transfer-tool}


## Disponibilidade {#availability}

O Content Transfer Tool pode ser baixado como arquivo zip no Portal de distribuição de software. É possível instalar o pacote via [Gerenciador de pacotes](/help/implementing/developing/tools/package-manager.md) na instância do Adobe Experience Manager (AEM) de origem. Baixe a versão mais recente. Para obter mais informações sobre a versão mais recente, consulte [Notas de versão](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=pt-BR).

>[!NOTE]
>Baixe a ferramenta Transferência de conteúdo no [Portal de distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html).

## Conectividade do ambiente de origem {#source-environment-connectivity}

A instância do AEM de origem pode estar sendo executada por trás de um firewall, em que ela só pode alcançar determinados hosts que foram adicionados a uma Lista de permissões. Para executar uma extração com êxito, os seguintes endpoints precisarão estar acessíveis na instância que está executando o AEM:

* O ambiente as a Cloud Service do AEM: `author-p<program_id>-e<env_id>.adobeaemcloud.com`
* O serviço de armazenamento de blobs do Azure: `*.blob.core.windows.net`
* O ponto de extremidade de E/S do Mapeamento de Usuário: `usermanagement.adobe.io`

Para testar a conectividade com o ambiente as a Cloud Service AEM de destino, emita o seguinte comando cURL no shell da instância de origem (replace `program_id`, `environment_id`, e `migration_token`):

`curl -i https://author-p<program_id>-e<environment_id>.adobeaemcloud.com/api/migration/migrationSet -H "Authorization: Bearer <migration_token>"`

>[!NOTE]
>Se um `HTTP/2 200` for recebido, uma conexão com o AEM as a Cloud Service foi bem-sucedida.

## Execução da ferramenta Transferência de conteúdo {#running-tool}

>[!VIDEO](https://video.tv.adobe.com/v/35460/?quality=12&learn=on)


Siga esta seção para saber como usar a ferramenta Transferência de conteúdo para migrar o conteúdo para o AEM as a Cloud Service (Autor/Publicação):

1. Selecione o Adobe Experience Manager e navegue até ferramentas -> **Operações** -> **Migração de conteúdo**.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/ctt01.png)

1. Selecione o **Transferência de conteúdo** opção de **Migração de conteúdo** assistente.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/ctt02.png)


1. O console abaixo é exibido quando você cria o primeiro conjunto de migração. Clique em **Criar conjunto de migração** para criar um novo conjunto de migração.

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
      >Você pode recuperar o token de acesso usando o **Token de acesso aberto** botão. Você precisa garantir que pertença ao grupo &quot;Administradores&quot; na instância do Cloud Service de destino.

   1. **Parâmetros**: selecione os seguintes parâmetros para criar o conjunto de migração:

      1. **Incluir versão**: selecione conforme necessário. Quando as versões são incluídas, o caminho `/var/audit` é incluído automaticamente para migrar eventos de auditoria.

         ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/ctt05.png)

         >[!NOTE]
         >Se você pretende incluir versões como parte de um conjunto de migração e estiver executando atualizações com `wipe=false`, é necessário desativar a limpeza de versão devido a uma limitação atual na Ferramenta de transferência de conteúdo. Se preferir manter a limpeza de versão ativada e estiver executando atualizações complementares em um conjunto de migração, você deverá executar a assimilação como `wipe=true`.


      1. **Caminhos a serem incluídos**: use o navegador de caminhos para selecionar os caminhos que precisam ser migrados. O seletor de caminhos aceita a entrada digitando ou selecionando.

         >[!IMPORTANT]
         >Os seguintes caminhos estão restritos ao criar um conjunto de migração:
         >* `/apps`
         >* `/libs`
         >* `/home`
         >* `/etc` (algumas `/etc` caminhos podem ser selecionados na CTT)


1. Clique em **Salvar** depois de preencher todos os campos no **Criar conjunto de migração** tela de detalhes.

1. Você visualizará seu conjunto de migração na **Transferência de conteúdo** conforme mostrado na figura abaixo.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/ctt07.png)

   Todos os conjuntos de migração existentes são exibidos no **Transferência de conteúdo** com suas informações de status atuais. Você pode ver alguns desses ícones descritos abaixo.

   * Uma *nuvem vermelha* indica que não é possível concluir o processo de extração.
   * A *nuvem verde* indica que você pode concluir o processo de extração.
   * Um *ícone amarelo* indica que você não criou o conjunto de migração existente e o específico é criado por algum outro usuário na mesma instância.

1. Selecione um conjunto de migração e clique em **Propriedades** para exibir ou editar as propriedades do conjunto de migração. Ao editar propriedades, não é possível alterar a variável **Nome do conjunto de migrações** ou o **URL do serviço**.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/ctt06.png)

### Determinação do tamanho do conjunto de migração e do espaço em disco {#migration-set-size}

Depois de criar um conjunto de migração, é altamente recomendável executar uma verificação de tamanho no conjunto de migração antes de iniciar um processo de Extração.
Ao executar uma verificação de tamanho no conjunto de migração, você será capaz de:
* Determine se há espaço em disco suficiente no `crx-quickstart` subdiretório para concluir a extração com êxito.
* Determine se o tamanho do conjunto de migração se enquadra nos limites do produto compatível e evite assimilações de conteúdo com falha.

Siga as etapas abaixo para executar uma verificação de tamanho:

1. Selecione um conjunto de migração e clique em **Verificar tamanho**.

   ![imagem](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image1.png)

1. Isso abrirá o **Verificar tamanho** diálogo.

   ![imagem](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image2.png)

1. Clique em **Verificar tamanho** para iniciar o processo. Em seguida, você retornará à exibição da lista de conjuntos de migração e verá uma mensagem indicando que **Verificar tamanho** está em execução.

   ![imagem](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image3.png)


1. Uma vez **Verificar tamanho** processo for concluído, o status mudará para **CONCLUÍDO**. Selecione o mesmo conjunto de migração e clique em **Verificar tamanho** para visualizar os resultados.

   ![imagem](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image4.png)

   Veja abaixo um exemplo de **Verificar tamanho** resultados sem avisos.

   ![imagem](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image5.png)

1. Se a variável **Verificar tamanho** os resultados indicam que há espaço em disco insuficiente e/ou que o conjunto de migração excede os limites do produto, **AVISO** O status será exibido.

![imagem](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image6.png)

Veja abaixo um exemplo de **Verificar tamanho** resultados com avisos.

![imagem](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image7.png)


## O que vem a seguir {#whats-next}

Depois de aprender a criar um conjunto de migração, você estará pronto para aprender sobre os processos de extração e assimilação na ferramenta Transferência de conteúdo. Antes de aprender esses processos, você deve revisar [Lidar com grandes repositórios de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en) para acelerar significativamente as fases de extração e assimilação da atividade de transferência de conteúdo para mover o conteúdo para o AEM as a Cloud Service.
