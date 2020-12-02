---
title: Notas de versão do Cloud Manager no AEM como Cloud Service versão 2020.6.0
description: Notas de versão do Cloud Manager no AEM como Cloud Service versão 2020.6.0
translation-type: tm+mt
source-git-commit: ca690144a8254d5ffba354f0f96d9ef1c5202533
workflow-type: tm+mt
source-wordcount: '612'
ht-degree: 89%

---


# Notas de versão do Cloud Manager no Adobe Experience Manager como Cloud Service 2020.6.0 {#release-notes}

Esta página descreve as Notas de versão do Cloud Manager em AEM como Cloud Service 2020.6.0.

## Data de lançamento {#release-date}

A data de lançamento do Cloud Manager no AEM como Cloud Service 2020.6.0 é 4 de junho de 2020.

## Novidades {#whats-new-cloud-manager}

* Os usuários que estiverem exercendo a função de *Proprietário comercial* no Cloud Manager agora podem excluir um Programa de sandbox a partir da página de aterrissagem (com o botão de ação rápida no cartão Programa) ou dentro do programa.

   Consulte [Exclusão de um programa de sandbox](https://docs.adobe.com/content/help/pt-BR/experience-manager-cloud-service/onboarding/getting-access/cloud-service-programs/creating-a-program.html) para obter mais detalhes.

* Os usuários de programas de sandbox que estiverem exercendo a função de *Proprietário comercial* ou *Gerente de implantação* no Cloud Manager agora podem excluir seu conjunto de ambientes de produção e preparo na interface do Cloud Manager. A opção de exclusão agora está disponível no cartão Ambiente da página **Visão geral de programas**, bem como na página **Ambientes**. Selecionar a opção de exclusão no ambiente de produção também exclui o ambiente de preparo no mesmo conjunto, e vice-versa.

   Consulte [Exclusão de um programa de sandbox](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/onboarding/getting-access/cloud-service-programs/creating-a-program.html) para obter mais detalhes.

* Há notas explicativas na página de aterrissagem para informar e instruir o usuário sobre a navegação básica.

* Há notas explicativas na página **Visão geral de programas** para informar e instruir o usuário sobre a navegação básica dentro do Cloud Manager.

* Agora há uma página **Saiba mais** na área de navegação superior do Cloud Manager. Essa página inclui recursos para ajudar os usuários a saber mais sobre os fluxos de trabalho usados com mais frequência, conforme a relevância para as suas funções atribuídas no Cloud Manager.

* Os Programas de sandbox agora são identificados por meio de um selo **Sandbox**, que será exibido no cartão do programa na página de aterrissagem e também ao lado do nome do programa na página **Visão geral de programas**.

* Os usuários que estiverem exercendo a função SysAdmin agora têm acesso com um só clique ao local do Admin Console onde podem gerenciar funções ou permissões de usuários para o Cloud Manager. Agora há um botão **Gerenciar acesso** na página de aterrissagem, ao lado do botão **Adicionar programa**.

   Consulte [Tarefas de SysAdmin](https://docs.adobe.com/content/help/pt-BR/experience-manager-cloud-service/onboarding/getting-access/navigation.html#sysadmin-tasks) para saber mais.

* Agora os usuários que estiverem exercendo a função SysAdmin têm acesso à instância do autor diretamente do Cloud Manager, com um só clique.

   Consulte [Gerenciar o acesso à instância do autor](https://docs.adobe.com/content/help/pt-BR/experience-manager-cloud-service/onboarding/getting-access/navigation.html#manage-access-aem) para saber mais.

* O log da etapa Criar agora inclui a lista de artefatos descobertos, incluindo pacotes de conteúdo ignorados.

* A etapa Criar agora verifica a inclusão das propriedades obrigatórias — nome, grupo e versão — em todos os pacotes de conteúdo gerados.

* A etapa Criar agora verifica se a criação produziu pelo menos um pacote de conteúdo.

### Correções de erros {#bug-fixes-cm}

* Em determinadas situações, os ícones na caixa de diálogo **Criar programa** estavam desalinhados.

* O identificador de versão do AEM não era exibido de maneira consistente na página **Visão geral de programas**.

* Ao configurar o pipeline de produção, a opção **Implantação agendada** não estava visível para alguns clientes.

### Problemas conhecidos {#known-issues-cm}

* Os ambientes do programa de sandbox hibernam quando não é detectada nenhuma atividade por um determinado período. Isso não ocorre no Cloud Manager, mas pode ocorrer por meio do Console do desenvolvedor. O problema será resolvido em uma versão futura.

* O link direto do Cloud Manager para o Console do desenvolvedor não exibe a opção de desibernar/hibernar o ambiente de um Programa de sandbox. Para resolver isso, uma vez no Console do desenvolvedor, adicione o padrão `#release-cm-p1234-e5678` ao final do URL, em que *1234* é a ID do programa e *5678* é a ID do ambiente. O problema será resolvido em uma versão futura.
