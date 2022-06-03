---
title: Visualização de logs para um conjunto de migração na ferramenta Transferência de conteúdo (herdado)
description: Visualização de logs para um conjunto de migração na ferramenta Transferência de conteúdo
hide: true
hidefromtoc: true
source-git-commit: 1fb4d0f2a3b3f9a27f5ab1228ec2d419149e0764
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 64%

---

# Visualização de logs para um conjunto de migração (herdado) {#view-logs-content-transfer-tool}

Após a conclusão de cada etapa (extração e assimilação), verifique os logs e procure erros.  Todos os erros devem ser resolvidos imediatamente, lidando com os problemas relatados ou entrando em contato com o suporte ao Adobe.

## Etapas para visualizar logs {#viewing-logs}

Você pode visualizar logs de um conjunto de migração existente na página *Visão geral*.
Siga as etapas abaixo:

1. Navegue até a página *Visão geral*, selecione o conjunto de migração que você deseja excluir e clique em **Exibir log** na barra de ações.

   ![imagem](/help/journey-migration/content-transfer-tool/assets/view-log1.png)

1. A caixa de diálogo **Logs** é exibida. Clique em **Logs de extração** para visualizar os logs em uma nova guia.

   ![imagem](/help/journey-migration/content-transfer-tool/assets/view-log2.png)
Ou,

   Você também pode visualizar logs para o seu conjunto de migração na tela *Visão geral*. Selecione o conjunto de migração e clique no status do campo **EXTRAÇÃO**. Nesse caso, clique em **CONCLUÍDO** para visualizar os logs em uma nova guia.

   ![imagem](/help/journey-migration/content-transfer-tool/assets/view-log3.png)

1. Para rastrear os logs sem usar a interface do usuário, você pode aplicar SSH ao ambiente do AEM de origem e rastrear o conteúdo do `crx-quickstart/cloud-migration/extraction-XXXXX/output.log file`.
