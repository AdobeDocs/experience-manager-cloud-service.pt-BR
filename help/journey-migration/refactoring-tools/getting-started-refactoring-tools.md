---
title: Introdução às ferramentas de refatoração
description: Saiba como começar a usar as Ferramentas de refatoração no AEM as a Cloud Service
exl-id: 84394bdd-2b92-4f5d-b08a-7dc2c681baa4
source-git-commit: edfefb163e2d48dc9f9ad90fa68809484ce6abb0
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 2%

---

# Introdução às ferramentas de refatoração {#getting-started-refactoring-tools}

## Disponibilidade {#availability}

<!-- Alexandru: duplicate contextualhelp id, drafting this for now

>[!CONTEXTUALHELP]
>id="aemcloud_rs_upload"
>title="Download"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/release-notes/release-notes-current.html?lang=pt-BR" text="Release Notes"
>additional-url="https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html" text="Software Distribution Portal"

-->

## Executando as ferramentas de refatoração {#running-refactoring-tools}

Use a Ferramenta de refatoração para migrar seu código e obter compatibilidade com o AEM as a Cloud Service.

1. Se você ainda não criou um projeto CAM, consulte [Criação e gerenciamento de um projeto no CAM](/help/journey-migration/cloud-acceleration-manager/using-cam/getting-started-cam.md#create-project).
1. Clique no cartão **Refatoração de código** para carregar o código-fonte.

   ![imagem](/help/journey-migration/refactoring-tools/assets/rscam1.png)

1. Ao acessar pela primeira vez a **Exibição de código do Source**, você verá um estado vazio solicitando que carregue seu código-fonte.

   ![imagem](/help/journey-migration/refactoring-tools/assets/rscam2.png)

## Upload do código do Source {#uploading}

Quando os clientes acessam as **Ferramentas de refatoração** pela primeira vez, eles apresentam um estado vazio na **Exibição do código Source**. Siga as etapas abaixo para fazer upload do projeto e iniciar o processo de inspeção:

1. **Acessar a Página de Carregamento do Projeto**\
   Clique no botão **Carregar Projeto** no estado vazio para iniciar o processo de carregamento.

   ![imagem](/help/journey-migration/refactoring-tools/assets/rscam3.png)

1. **Carregar seu código Source**
   - Na caixa de diálogo de upload, selecione o arquivo ZIP do código-fonte.
   - Clique em **Carregar** para começar.
   - O progresso do upload será exibido na caixa de diálogo. A duração depende do tamanho do projeto.

   ![imagem](/help/journey-migration/refactoring-tools/assets/rscam4.png)

1. **Processo de Inspeção**
   - Após o carregamento, o **Processo de Inspeção** começa automaticamente em segundo plano.
   - A **Visualização de Código do Source** agora exibirá o projeto carregado e seu status de inspeção.

1. **Status de Inspeção** O processo de inspeção foi projetado para simplificar a execução de ferramentas de refatoração, reduzindo a sobrecarga das configurações manuais.

   A inspeção mostrará um dos seguintes status:
   - **Em execução** - A inspeção está em andamento.
   - **Pronto** - A inspeção foi concluída; agora você pode executar ferramentas de refatoração.
   - **Falha** - Erro. Clique no projeto para revisar o relatório de inspeção e resolver quaisquer problemas.

   ![imagem](/help/journey-migration/refactoring-tools/assets/rscam5.png)

>[!NOTE]
>
>Fazer upload de um novo projeto excluirá o projeto existente. Verifique se os dados necessários foram salvos antes de continuar.

>[!NOTE]
>
>Os trabalhos de refatoração só poderão ser executados se o upload do código-fonte for bem-sucedido.

## Trabalhos de refatoração {#refactoring-jobs}

Ao clicar na guia **Trabalho de Refatoração**, você verá uma lista de trabalhos existentes. Se nenhum trabalho tiver sido criado ainda, um estado vazio será exibido solicitando a criação do trabalho.

![imagem](/help/journey-migration/refactoring-tools/assets/rscam6.png)

### &#x200B;1. Criar um Novo Trabalho de Refatoração

- Clique no botão **Criar Novo Trabalho**.
- Selecione as ferramentas de refatoração desejadas.
- Clique em **Iniciar** para iniciar o processo de refatoração.

![imagem](/help/journey-migration/refactoring-tools/assets/rscam7.png)

>[!NOTE]
>
>Você pode acionar trabalhos individuais de refatoração ou executar todas as ferramentas disponíveis de uma só vez usando a opção **Todas as ferramentas em conjunto**.

### &#x200B;2. Status da tarefa

- **Em execução** - O trabalho está em andamento. O status é atualizado automaticamente após a conclusão ou falha.
- **Concluído** - O trabalho foi concluído com êxito. Agora você pode revisar os resultados ou baixar o código refatorado.
- **Falha** - O trabalho encontrou um erro. Clique no trabalho para exibir registros detalhados e solucionar o problema.

![imagem](/help/journey-migration/refactoring-tools/assets/rscam8.png)

Quando o trabalho for concluído com êxito, o botão **Download** ficará disponível, permitindo que você recupere:

- **O Projeto Refatorado**: este é o código atualizado após a aplicação da transformação. Os clientes podem baixar o código mais recente para o projeto.
- **Logs de atividade**: durante a execução do trabalho, todas as etapas executadas pela ferramenta e as alterações feitas são registradas como parte disso.
- **Relatório de descobertas**: este relatório contém itens que não foram totalmente executados pela ferramenta, mas ainda precisam ser abordados. Todas essas alterações são registradas aqui.

![imagem](/help/journey-migration/refactoring-tools/assets/rscam9.png)

>[!NOTE]
>
>Cada tarefa pode levar até 1 hora para ser concluída. Se o status não for atualizado, entre em contato com o Suporte da Adobe.
