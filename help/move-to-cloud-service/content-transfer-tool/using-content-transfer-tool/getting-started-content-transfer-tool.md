---
title: Introdução à ferramenta Transferência de conteúdo
description: Introdução à ferramenta Transferência de conteúdo
exl-id: a19b8424-33ab-488a-91b3-47f0d3c8abf5
source-git-commit: fc0628c2bfd345a7846d3d4fbd0fe11a459b10a1
workflow-type: tm+mt
source-wordcount: '860'
ht-degree: 29%

---

# Introdução à ferramenta Transferência de conteúdo {#getting-started-content-transfer-tool}

## Conectividade do ambiente de origem

A instância de AEM de origem pode estar em execução atrás de um firewall em que só pode alcançar determinados hosts que foram adicionados a uma Lista de permissões. Para executar com êxito uma extração, os seguintes endpoints precisarão ser acessíveis da instância que está executando AEM:

* O público-alvo AEM ambiente as a Cloud Service:
   `author-p<program_id>-e<env_id>.adobeaemcloud.com`
* O serviço de armazenamento de blobs do Azure:
   `*.blob.core.windows.net`
* O ponto de extremidade de E/S de Mapeamento de Usuário:
   `usermanagement.adobe.io`

Para testar a conectividade com o ambiente de destino AEM as a Cloud Service, emita o seguinte comando cURL do shell da instância de origem (substitua `program_id`, `environment_id`e `migration_token`):

```
 curl -i https://author-p<program_id>-e<environment_id>.adobeaemcloud.com/api/migration/migrationSet -H "Authorization: Bearer <migration_token>"
```

>[!NOTE]
>Se uma `HTTP/2 200` for recebida, uma conexão com AEM as a Cloud Service foi bem-sucedida.

## Disponibilidade {#availability}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_download"
>title="Download"
>abstract="A ferramenta Transferência de conteúdo pode ser baixada como um arquivo zip no Portal de distribuição de software. Você pode instalar o pacote por meio do Gerenciador de pacotes na sua instância de origem do Adobe Experience Manager (AEM). Faça o download da versão mais recente."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html" text="Notas de versão"
>additional-url="https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html" text="Portal de distribuição de software"

A ferramenta Transferência de conteúdo pode ser baixada como um arquivo zip no Portal de distribuição de software. Você pode instalar o pacote por meio do Gerenciador de pacotes na sua instância de origem do Adobe Experience Manager (AEM). Faça o download da versão mais recente. Para obter mais detalhes sobre a versão mais recente, consulte [Notas de versão](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=pt-BR).

>[!NOTE]
>Baixe a ferramenta Transferência de conteúdo no [Portal de distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html).

## Execução da ferramenta Transferência de conteúdo {#running-tool}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_demo"
>title="Execução da ferramenta Transferência de conteúdo"
>abstract="Saiba como usar a ferramenta Transferência de conteúdo para migrar o conteúdo para AEM as a Cloud Service (Autor/Publicação)."
>additional-url="https://video.tv.adobe.com/v/35460/?quality=12&amp;learn=on" text=" Consulte Demonstração"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/migration/content-transfer-tool.html?lang=en#migration" text="Tutorial - Uso da ferramenta Transferência de conteúdo"

>[!VIDEO](https://video.tv.adobe.com/v/35460/?quality=12&learn=on)


Siga esta seção para saber como usar a ferramenta Transferência de conteúdo para migrar o conteúdo para o AEM as a Cloud Service (Autor/Publicação):

1. Selecione o Adobe Experience Manager e navegue até as ferramentas -> **Operações** -> **Migração de conteúdo**.

   ![imagem](/help/move-to-cloud-service/content-transfer-tool/assets-ctt/ctt01.png)

1. Selecione o **Transferência de conteúdo** opção de **Migração de conteúdo** assistente.

   ![imagem](/help/move-to-cloud-service/content-transfer-tool/assets-ctt/ctt02.png)


1. O console abaixo é exibido ao criar o primeiro conjunto de migração. Clique em **Criar conjunto de migração** para criar um novo conjunto de migração.

   ![imagem](/help/move-to-cloud-service/content-transfer-tool/assets-ctt/ctt03.png)

   >[!NOTE]
   >Se você tiver conjuntos de migração existentes, o console exibirá a lista de conjuntos de migração existentes com seu status atual.


1. Preencha os campos em **Criar conjunto de migração** conforme descrito abaixo.

   ![imagem](/help/move-to-cloud-service/content-transfer-tool/assets-ctt/ctt04.png)

   1. **Nome**: insira o nome do conjunto de migração.
      >[!NOTE]
      >Nenhum caractere especial é permitido para o nome do conjunto de migração.

   1. **Configuração do Cloud Service**: insira a URL do autor do AEM as a Cloud Service.

      >[!NOTE]
      >Você pode criar e manter no máximo dez conjuntos de migração por vez durante a atividade de transferência de conteúdo.
      >Além disso, é necessário criar uma migração separadamente para cada um dos ambientes específicos - *Preparação*, *Desenvolvimento* ou *Produção*.

   1. **Token de acesso**: insira o token de acesso.

      >[!NOTE]
      >Você pode recuperar o token de acesso usando o **Abrir token de acesso** botão. Você precisa garantir que pertença ao grupo dos administradores de AEM na instância do Cloud Service de destino.

   1. **Parâmetros**: selecione os seguintes parâmetros para criar o conjunto de migração:

      1. **Incluir versão**: selecione conforme necessário. Quando as versões são incluídas, o caminho `/var/audit` é incluído automaticamente para migrar eventos de auditoria.

         ![imagem](/help/move-to-cloud-service/content-transfer-tool/assets-ctt/ctt05.png)

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

   ![imagem](/help/move-to-cloud-service/content-transfer-tool/assets-ctt/ctt07.png)

   Todos os conjuntos de migração existentes são exibidos na **Transferência de conteúdo** com seu status atual e informações de status. Você pode ver alguns desses ícones descritos abaixo.

   * Uma *nuvem vermelha* indica que não é possível concluir o processo de extração.
   * A *nuvem verde* indica que você pode concluir o processo de extração.
   * Um *ícone amarelo* indica que você não criou o conjunto de migração existente e o específico é criado por algum outro usuário na mesma instância.

1. Selecione um conjunto de migração e clique em **Propriedades** para exibir ou editar as propriedades do conjunto de migração. Ao editar propriedades, não é possível alterar a variável **Nome do conjunto de migração** ou **URL de serviço**.

   ![imagem](/help/move-to-cloud-service/content-transfer-tool/assets-ctt/ctt06.png)


## O que vem a seguir {#whats-next}

Depois de aprender a criar um conjunto de migração, agora você está pronto para aprender sobre os Processos de extração e assimilação na ferramenta Transferência de conteúdo. Antes de aprender esses processos, você deve revisar [Lidar com grandes repositórios de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en) para acelerar significativamente as fases de extração e assimilação da atividade de transferência de conteúdo para mover o conteúdo para AEM as a Cloud Service.
