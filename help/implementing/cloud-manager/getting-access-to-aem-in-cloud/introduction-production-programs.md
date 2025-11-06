---
title: Introdução aos programas de produção
description: Saiba quais são os programas de produção e obtenha sugestões para configurar o seu.
exl-id: bb8d4a5a-b26a-4718-9327-149fedb87e6a
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 83%

---


# Introdução aos programas de produção {#production-programs}

Um programa de produção deve ser usado por uma equipe pronta para começar a gravar, compilar e testar o código com o objetivo de implantá-lo para hospedar o tráfego direto.

Depois que você [cria seu programa de produção](creating-production-programs.md), um [assistente de criação de programas](using-the-wizard.md) orienta o usuário por meio de seleções, dependendo do objetivo dele ao criar o programa.

## Opções de criação de programa {#program-creation-options}

Seu contrato com a Adobe define o número e os tipos de soluções disponíveis especificamente para a sua organização ao criar programas de produção. Você tem controle sobre como mapear as soluções disponíveis aos programas do Cloud Manager.

A tabela a seguir descreve cenários comuns de soluções disponíveis e os programas de produção típicos criados com base nelas.

| Soluções disponíveis | Opções de programa | O que está incluído | Quando usar | Exemplos |
|---------------------|-------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 1 Solução do Sites | Criar 1 programa somente Sites | 1 Produção + 1 Preparo, 1 Desenvolvimento, 1 Desenvolvimento Rápido | N/A | N/A |
| 1 Solução do Assets | Criar 1 programa somente Assets | 1 Produção + 1 Preparo, 1 Desenvolvimento, 1 Desenvolvimento Rápido | N/A | N/A |
| 1 Sites +1 Assets | Crie um programa: <br>1 Programa do Sites e Assets | 1 Produção + 1 Preparo, 2 Desenvolvimento, 2 Desenvolvimento Rápido | Quando a maioria dos ativos digitais é usada para dar suporte à implementação dos sites.<br>Nesses casos, a maioria dos ativos digitais está em um estado finalizado, pronta para ser usada em experiências entre canais por meio do Sites.<br>Normalmente, uma única equipe é responsável pelo gerenciamento de conteúdo para Sites e Assets. | Imagens usadas principalmente para um site.<br>Um portal interno integrado ao AEM Sites distribui PDFs. |
| 1 Sites +1 Assets | Crie programas separados:<br>1 Programa somente Sites e 1 Programa somente Assets | 1 Produção + 1 Fase, 1 Desenvolvimento, 1 Desenvolvimento rápido<br>1 Produção + 1 Fase, 1 Desenvolvimento, 1 Desenvolvimento rápido | Quando muitos ativos digitais não dao suporte diretamente à implementação de sites.<br> Nesses casos, os ativos estão em vários estados, incluindo tipos de arquivo brutos e trabalhos em andamento.<br>Uma equipe criativa dedicada gerencia os ativos digitais por meio de seu próprio ciclo de vida e tem fluxos de trabalho e ciclos de lançamento independentes dos da equipe de gerenciamento de conteúdo do Sites. | Imagens brutas de uma sessão fotográfica são armazenadas no programa de ativos e somente algumas serão usadas na implementação de sites.<br>Um grande número de tipos de arquivos da Creative Cloud, como Photoshop e Illustrator, são gerenciados no AEM Assets e passam por seu próprio fluxo de trabalho de aprovação antes de um ativo concluído ser gerado.<br>Considere usar [Ativos conectados](/help/assets/use-assets-across-connected-assets-instances.md#overview-of-connected-assets) nesses casos. |
| 1 Sites + 1 Sites | Criar programas separados:<br>1 Programa somente Sites e 1 programa somente Sites | 1 Produção + 1 Fase, 1 Desenvolvimento, 1 Desenvolvimento rápido<br>1 Produção + 1 Fase, 1 Desenvolvimento, 1 Desenvolvimento rápido | Para implementações de sites de vários locatários.<br>Nesses casos, vários sites com seus próprios cronogramas de lançamento e equipes dedicadas de desenvolvimento e conteúdo devem ser gerenciados. | Duas marcas de varejo com sites dedicados e equipes de desenvolvimento independentes |


>[!NOTE]
>
>Os programas de produção [podem ser editados, mas não excluídos](editing-programs.md).
