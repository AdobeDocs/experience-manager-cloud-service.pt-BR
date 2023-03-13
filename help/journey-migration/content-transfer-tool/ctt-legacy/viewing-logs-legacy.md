---
title: Visualização de logs para um conjunto de migração na ferramenta Transferência de conteúdo (herdado)
description: Visualização de logs para um conjunto de migração na ferramenta Transferência de conteúdo
hide: true
hidefromtoc: true
exl-id: 01c8afd3-c594-4a41-b905-8c3a2d74db6f
source-git-commit: 22bbf15e33ab3d5608dc01ed293bb04b07cb6c8c
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 64%

---

# Visualização de logs para um conjunto de migração (herdado) {#view-logs-content-transfer-tool}

Após a conclusão de cada etapa (extração e assimilação), verifique os registros e procure por erros.  Quaisquer erros devem ser solucionados imediatamente, tratando dos problemas relatados ou entrando em contato com o suporte da Adobe.

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
