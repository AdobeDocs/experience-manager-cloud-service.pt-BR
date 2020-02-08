---
title: Exportar para CSV
description: Exportar informações sobre suas páginas em um arquivo CSV em seu sistema local
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8

---


# Exportar para CSV {#export-to-csv}

**Criar relatórios de arquivos CSV** permite exportar informações sobre suas páginas para um arquivo CSV em seu sistema local.

* O arquivo baixado é chamado de `export.csv`
* Os conteúdos dependem das propriedades que você selecionar.
* É possível definir o caminho junto com o detalhamento da exportação.

>[!NOTE]
>
>O recurso para download e o destino padrão do seu navegador são usados.

O assistente **Criar exportação de arquivos CSV** permite selecionar:

* Propriedades a serem exportadas
   * Metadados
      * Nome
      * Modificado
      * Publicado
      * Modelo
      * Fluxo de trabalho
   * Tradução
      * Traduzido
   * Análise
      * Exibições da página
      * Visitantes únicos
      * Tempo na página
* Profundidade
   * Caminho pai
   * Apenas secundários diretos
   * Níveis adicionais de secundários
   * Níveis

O arquivo `export.csv` resultante pode ser aberto no Excel ou qualquer outro aplicativo compatível.

Para criar uma exportação de arquivos CSV:

1. Abra o console **Sites** e navegue até o local desejado, se necessário.
   * A opção Criar relatório **** CSV está disponível ao navegar pelo console **Sites** (na exibição de Lista)
   * É uma opção do menu suspenso **Criar** :

      ![Opção Criar CSV](/help/sites-cloud/authoring/assets/csv-create.png)

1. From the toolbar, select **Create** then **CSV Report** to open the wizard:

   ![Opções de exportação para CSV](/help/sites-cloud/authoring/assets/csv-options.png)

1. Selecione as propriedades desejadas para exportar.
1. Selecione **Criar**.
   ![Exportação CSV resultante no Excel](/help/sites-cloud/authoring/assets/csv-example.png)
