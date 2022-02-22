---
title: 'Introdução aos programas de produção '
description: Saiba quais são os programas de produção e sugestões para configurar o seu.
exl-id: bb8d4a5a-b26a-4718-9327-149fedb87e6a
source-git-commit: a6152a1529b5c70bcf056857204e7ff97fc614e4
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 2%

---


# Introdução aos programas de produção {#production-programs}

Um programa de produção destina-se a uma equipe pronta para começar a escrever, criar e testar o código com o objetivo de implantá-lo para hospedar o tráfego ao vivo.

Depois de [crie seu programa de produção,](creating-production-programs.md) a [assistente de criação de programas](using-the-wizard.md) orienta o usuário por meio de seleções, dependendo do objetivo do usuário na criação do programa.

## Opções de criação de programas {#program-creation-options}

Seu contrato com o Adobe define o número e os tipos de soluções disponíveis para sua organização específica ao criar programas de produção. Você tem controle sobre como mapear as soluções disponíveis para os programas do Cloud Manager.

A tabela a seguir descreve cenários comuns de soluções disponíveis e os programas de produção típicos criados com base nelas.

| Soluções disponíveis | Opções de programa | O que está incluído | Quando usar | Exemplos |
|--- |--- |--- |--- |---|
| Solução de 1 Sites | Criar um programa somente Sites | 1 Produção + 1 Estágio, 1 Desenvolvimento | N/A | N/D |
| 1 Solução de ativos | Criar 1 programa somente ativos | 1 Produção + 1 Estágio, 1 Desenvolvimento | N/D | N/D |
| 1 Sites +1 Ativos | Crie um programa: <br>1 Programa Sites e ativos | 1 Produção + 1 Estágio, 2 Desenvolvimento | Quando a maioria dos ativos digitais é usada para suportar a implementação dos sites.<br>Nesses casos, a maioria dos ativos digitais está em um estado finalizado, pronta para ser usada em experiências entre canais por meio do Sites.<br>Normalmente, uma única equipe é responsável pelo gerenciamento de conteúdo para sites e ativos. | Imagens usadas principalmente para um site.<br>PDF que será distribuído por meio de um portal interno integrado ao AEM Sites. |
| 1 Sites +1 Ativos | Criar programas separados:<br>Programa somente Sites e 1 Programa somente Ativos | 1 Produção + 1 Estágio, 1 Desenvolvimento<br> 1 Produção + 1 Estágio, 1 Desenvolvimento | Quando muitos ativos digitais não suportam diretamente a implementação de sites.<br> Nesses casos, os ativos estão em vários estados, incluindo tipos de arquivo brutos e trabalhos em andamento.<br>Uma equipe criativa dedicada gerencia ativos digitais por meio de seu próprio ciclo de vida e tem fluxos de trabalho e ciclos de lançamento separados que a equipe de gerenciamento de conteúdo do Sites. | Imagens brutas de uma sessão fotográfica são armazenadas no programa Ativos e somente algumas poucas serão usadas na implementação do Sites .<br>Um grande número de tipos de arquivos do Creative Cloud, como Photoshop e Illustrator, são gerenciados no AEM Assets e passam por seu próprio fluxo de trabalho de aprovação antes da geração de um ativo concluído.<br>Considere usar [Ativos conectados](/help/assets/use-assets-across-connected-assets-instances.md#overview-of-connected-assets) em tais casos. |
| 1 Sites + 1 Sites | Criar programas separados:<br>Programa somente Sites e programa somente 1 Sites | 1 Produção + 1 Estágio, 1 Desenvolvimento<br>1 Produção + 1 Estágio, 1 Desenvolvimento | Para implementações de sites de vários locatários.<br>Nesses casos, vários sites com seu próprio agendamento de lançamento e equipes dedicadas de desenvolvimento e conteúdo devem ser gerenciados. | Duas marcas de varejo com sites dedicados e equipes de desenvolvimento separadas |

>[!NOTE]
>
>Programas de produção [não pode ser editado.](editing-programs.md)
