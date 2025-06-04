---
title: Visão geral das ferramentas de refatoração
description: Saiba como começar a usar as Ferramentas de refatoração do AEM
source-git-commit: a77dfef8dce9f4ed549135087f7b63f6d46a4ea1
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 1%

---


<!-- Alexandru: temporarily commeting this out, since it breaks validation

>[!CONTEXTUALHELP]
>id="aemcloud_rs_overview"
>title="Overview"
>abstract="Refactoring Tools is a solution developed by Adobe to help refactor existing AEM projects for compatibility with AEM as a Cloud Service. The tools are executed via Cloud Acceleration Manager (CAM) and automate key modernization tasks."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html?lang=pt-BR" text="Guidelines and Best Practices"

-->

# Visão geral das ferramentas de refatoração {#refactoring-tools-overview}

As **Ferramentas de Refatoração** simplificam o processo de atualização de projetos existentes do AEM para serem compatíveis com o **AEM as a Cloud Service (AEMaaCS)**. Essas ferramentas automatizam tarefas comuns de refatoração e modernização e são integradas ao **Cloud Acceleration Manager (CAM)** para proporcionar uma experiência contínua.

Anteriormente disponível apenas como utilitários CLI, as Ferramentas de refatoração agora fornecem uma interface unificada com recursos como inspeção automatizada, geração de configuração e execução de tarefas — reduzindo a sobrecarga manual e melhorando a visibilidade.

## Fluxo de Trabalho de Inspeção {#inspection-workflow}

O **Fluxo de Trabalho de Inspeção** simplifica o processo de preparação para executar ferramentas de refatoração.

### Principais recursos:

* **Acionador automático** - O carregamento de um projeto inicia automaticamente a inspeção.
* **Geração de Configuração** - As ferramentas inspecionam o código-fonte carregado e geram as configurações necessárias.
* **Envio de carga** - Essas configurações são passadas diretamente para as ferramentas selecionadas para execução.

## Ferramentas de refatoração disponíveis

### Modernizador de repositório {#repo-modernizer}

O **Modernizador de repositório** reestrutura o layout e o conteúdo do repositório do seu projeto do AEM para alinhar-se aos padrões e práticas recomendadas do AEMaaCS. Ele substitui a ferramenta de modernização de repositório herdada pela automação e precisão aprimoradas.

### Transformador de código {#code-transformer}

O **Transformador de código** usa reconhecimento de padrão inteligente e análise orientada por IA para detectar e atualizar segmentos de código incompatíveis com o AEMaaCS. Essa ferramenta simplifica o esforço de migração e reduz as alterações manuais de código.

## Refatorando Fases do Fluxo de Trabalho {#phases-in-refactoring-tools}

As Ferramentas de refatoração seguem um processo estruturado de duas fases:

### Fase 1: Fazer upload do código Source

* Faça upload do seu código fonte (em formato ZIP) usando a interface CAM.
* Depois de carregado, o **Fluxo de Trabalho de Inspeção** é automaticamente acionado para analisar o projeto e prepará-lo para a execução da ferramenta.

>[!NOTE]
>Durante o processo de inspeção, o upload de outro projeto não é permitido.

### Fase 2: Acionar um trabalho de refatoração

Após uma inspeção bem-sucedida, é possível executar uma ou mais ferramentas de refatoração:

* **Executar Modernizador de Repositório** - Executa a modernização de repositório.
* **Executar Transformador de Código** - Executa uma transformação de código com base na saída da inspeção.
* **Executar Todas as Ferramentas Juntos** - Executa todas as ferramentas disponíveis em uma única operação.

>[!NOTE]
>Os trabalhos de refatoração só podem ser iniciados depois que o código-fonte tiver sido carregado e inspecionado com êxito.

>[!NOTE]
>Os usuários podem acionar vários trabalhos de refatoração simultaneamente, mas cada trabalho será executado separadamente.
