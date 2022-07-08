---
title: Exportar para CSV
description: Exportar informações sobre suas páginas em um arquivo CSV em seu sistema local
exl-id: 818e927e-40b2-4ccb-bfb3-88284ad49829
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: ht
source-wordcount: '199'
ht-degree: 100%

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

* Propriedades a serem exportadas
   * Metadados
      * Nome
      * Modificado
      * Publicado
      * Modelo
      * Fluxo de trabalho
   * Tradução
      * Traduzido
   * Analytics
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
   * A opção Criar **relatório de CSV** está disponível ao navegar pelo console **Sites** (na exibição de Lista)
   * É uma opção do menu suspenso **Criar**:

      ![Opção Criar CSV](/help/sites-cloud/authoring/assets/csv-create.png)

1. Na barra de ferramentas, selecione **Criar**, em seguida, **Relatórios de arquivos CSV** para abrir o assistente:

   ![Opções de exportação de CSV](/help/sites-cloud/authoring/assets/csv-options.png)

1. Selecione as propriedades desejadas para exportar.
1. Selecione **Criar**.
   ![Exportação de CSV resultante no Excel](/help/sites-cloud/authoring/assets/csv-example.png)
