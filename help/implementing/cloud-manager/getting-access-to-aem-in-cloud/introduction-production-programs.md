---
title: 'Introdução aos programas de produção '
description: Introdução aos programas de produção
exl-id: bb8d4a5a-b26a-4718-9327-149fedb87e6a
source-git-commit: 09d5d125840abb6d6cc5443816f3b2fe6602459f
workflow-type: tm+mt
source-wordcount: '422'
ht-degree: 0%

---

# Introdução aos programas de produção {#production-programs}

Um programa de *Produção* destina-se a um usuário familiarizado com o AEM e o Cloud Manager e está pronto para começar a escrever, criar e testar o código com o objetivo de implantá-lo em produção.

>[!NOTE]
>Você não poderá excluir um programa de Produção.

Um assistente de criação de programa guiará o usuário a fazer seleções, dependendo do objetivo do usuário ao criar o programa. Com base nos direitos da solução não utilizados disponíveis para o cliente ou organização específica, o usuário tem controle sobre como mapear os direitos da solução (não utilizados) disponíveis para os programas do Cloud Manager.

## Considerações sobre a criação de programas {#program-creation-considerations}

A tabela abaixo descreve cenários comuns a serem considerados ao criar programas no Cloud Manager:

| Direitos de solução não usados disponíveis na organização | Criar opções de programa | O que está incluído | Quando usar e outras considerações |
|--- |--- |--- |--- |
| Solução de 1 Sites | Criar 1 programa somente Sites | 1 Produção + 1 Estágio, 1 Desenvolvimento | ND |
| 1 Solução de ativos | Criar 1 programa somente de ativos | 1 Produção + 1 Estágio, 1 Desenvolvimento | ND |
| 1 Sites +1 Ativos | Criar um programa: 1 Programa Sites e ativos | 1 Produção + 1 Estágio, 2 Desenvolvimento | A maioria dos ativos digitais é usada para suportar a implementação dos sites. A maioria dos ativos digitais está em um estado finalizado, pronta para ser usada em experiências entre canais por meio do Sites.Normalmente, uma única equipe é responsável pelo gerenciamento de conteúdo para Sites e Ativos. **Exemplos** comuns: Imagens usadas principalmente para um site. PDFs que serão distribuídos por meio de um portal interno integrado ao AEM Sites. |
| 1 Sites +1 Ativos | Criar programas separados: Programa somente Sites e 1 Programa somente Ativos | 1 Produção + 1 Estágio, 1 Desenvolvimento<br> 1 Produção + 1 Estágio, 1 Desenvolvimento | Muitos ativos digitais não suportam diretamente a implementação de sites. Os ativos gerenciados estão em vários estados, incluindo tipos de arquivos brutos e trabalhos em andamento. Uma equipe criativa dedicada gerencia ativos digitais por meio de seu próprio ciclo de vida e tem fluxos de trabalho e ciclos de lançamento separados que a equipe de gerenciamento de conteúdo do Sites. *Exemplos* comuns: Imagens brutas de uma sessão fotográfica são armazenadas no programa Ativos e somente algumas poucas serão usadas na implementação do Sites . Um grande número de tipos de arquivos do Creative Cloud, como Photoshop e Illustrator, são gerenciados no AEM Assets e passam por seu próprio fluxo de trabalho de aprovação antes da geração de um ativo concluído. Recursos para aproveitar: [Ativos conectados](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/use-assets-across-connected-assets-instances.html?lang=en#overview-of-connected-assets) |
| 1 Sites + 1 Sites | Criar programas separados: Programa somente Sites e 1 Programa somente Sites | 1 Produção + 1 Estágio, 1 Desenvolvimento<br>1 Produção + 1 Estágio, 1 Desenvolvimento | Implementações de sites de vários locatários. Vários sites com seu próprio agendamento de lançamento e equipes dedicadas de desenvolvimento e conteúdo. *Exemplos* comuns: Duas marcas de varejo com sites dedicados e equipes de desenvolvimento separadas |
