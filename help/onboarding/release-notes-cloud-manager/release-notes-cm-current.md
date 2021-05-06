---
title: Notas de versão do Cloud Manager no AEM as a Cloud Service versão 2021.5.0
description: Notas de versão do Cloud Manager no AEM as a Cloud Service versão 2021.5.0
feature: Informações da versão
translation-type: tm+mt
source-git-commit: e2d4bb7649fad3ee172c6f049ecfdedc71417ee2
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 2%

---


# Notas de versão do Cloud Manager no Adobe Experience Manager as a Cloud Service 2021.5.0 {#release-notes}

Esta página descreve as Notas de versão do Cloud Manager no AEM as a Cloud Service 2021.5.0.

## Data de lançamento {#release-date}

A data de lançamento do Cloud Manager no AEM as a Cloud Service 2021.5.0 é 6 de maio de 2021.
A próxima versão está planejada para 3 de junho de 2021.

### Novidades {#what-is-new}

* A regra de qualidade PackageOverlaps agora detecta casos em que o mesmo pacote foi implantado várias vezes, ou seja, em vários locais incorporados, no mesmo conjunto de pacotes implantado.

* O endpoint do repositório na API pública agora inclui o URL do Git.

* O log de implantação baixado por um usuário do Cloud Manager será mais revelador e incluirá detalhes sobre falhas e cenários de sucesso.

* Falhas intermitentes encontradas ao enviar o código para o Adobe git foram resolvidas.

* O complemento Commerce agora pode ser aplicado a programas Sandbox durante o fluxo de trabalho Editar programa .

* A experiência Editar programa foi atualizada.

* A tabela Nomes de Domínio na página Detalhes do Ambiente exibirá até 250 nomes de Domínio por paginação.

* A guia Soluções nos fluxos de trabalho Adicionar programa e Editar programa exibirá a solução, mesmo que apenas uma solução esteja disponível para o programa.

* A mensagem de erro no log de etapas da criação quando a build não produziu nenhum pacote de conteúdo implantado não estava clara.

### Correções de erros {#bug-fixes}

* Ocasionalmente, o usuário pode ver um status verde &quot;ativo&quot; ao lado de uma Lista de permissões de IP, mesmo quando essa configuração não foi implantada.

* Em vez de remover variáveis &quot;excluídas&quot;, a API de variáveis de pipelines somente as marcaria com o status **DELETED**.

* Alguns problemas de qualidade do tipo Código Smell estavam afetando incorretamente a Classificação de confiabilidade.

* Como domínios curingas não são compatíveis, a interface do usuário não permitirá que o usuário envie um domínio curinga.

* Quando uma execução de pipeline era iniciada entre meia-noite e 1h UTC, a versão de artefato gerada pelo Cloud Manager não tinha garantia de ser maior do que uma versão criada no dia anterior.

* Durante a configuração do programa de sandbox, depois que o projeto com código de amostra for criado com êxito, o Gerenciar Git será exibido como um link do cartão herói na página Visão geral .