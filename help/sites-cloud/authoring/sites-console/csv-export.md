---
title: Exportar para CSV
description: Exportar informações sobre suas páginas para um arquivo CSV em seu sistema local
badgeSaas: label="AEM Sites" type="Positive" tooltip="Aplicável ao AEM Sites)."
exl-id: 818e927e-40b2-4ccb-bfb3-88284ad49829
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 98c0c9b6adbc3d7997bc68311575b1bb766872a6
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 88%

---

# Exportar para CSV   {#export-to-csv}

**Criar relatórios de arquivos CSV** permite exportar informações sobre suas páginas para um arquivo CSV em seu sistema local.

* O arquivo baixado é chamado de `export.csv`
* Os conteúdos dependem das propriedades que você selecionar.
* É possível definir o caminho junto com o detalhamento da exportação.

>[!NOTE]
>
>O recurso para download e o destino padrão do seu navegador são usados.

O assistente **Criar exportação de arquivos CSV** permite selecionar:

* Propriedades para exportar
   * Metadados
      * Nome
      * Modificado
      * Publicado
      * Modelo
      * Fluxo de trabalho
   * Tradução
      * Traduzido
   * Analytics
      * Visualizações de página
      * Visitantes únicos
      * Tempo na página
* Profundidade
   * Caminho principal
   * Apenas filhos diretos
   * Níveis adicionais de filhos
   * Níveis

O arquivo `export.csv` resultante pode ser aberto no Excel ou qualquer outro aplicativo compatível.

Para criar uma exportação de arquivos CSV:

1. Abra o console **Sites** e navegue até o local desejado, se necessário.
   * A opção Criar **relatório de CSV** está disponível ao navegar pelo console **Sites** (na exibição de Lista)
   * É uma opção do menu suspenso **Criar**:

     ![Opção Criar CSV](/help/sites-cloud/authoring/assets/csv-create.png)

1. Na barra de ferramentas, selecione **Criar**, em seguida, **Relatórios de arquivos CSV** para abrir o assistente:

   ![Opções de exportação de CSV](/help/sites-cloud/authoring/assets/csv-options.png)

1. Selecione as propriedades necessárias para exportar.
1. Selecione **Criar**.
   ![Exportação de CSV resultante no Excel](/help/sites-cloud/authoring/assets/csv-example.png)
