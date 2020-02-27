---
title: Permissões baseadas em função
description: Permissões baseadas em função
translation-type: tm+mt
source-git-commit: e59fe55c255d5239a561a9fb878faa81d17b4b48

---


# Permissões baseadas em função {#role-based-permissions}

[!UICONTROL O Cloud Manager] tem funções pré-configuradas com permissões apropriadas. Por exemplo, um desenvolvedor desenvolve código e tem permissão para enviar o código para o Repositório **Git**. Como alternativa, um proprietário de negócios tem permissões diferentes que permitem definir os Indicadores-chave de desempenho (KPIs) e aprovar implantações.

## Permissões de usuário {#user-permissions}

Cada uma das funções tem permissões específicas, tarefas pré-configuradas ou permissões associadas a cada função. Esta tabela lista as funções disponíveis e as funções que podem executar a função.

| Permissão | Descrição | Proprietário da empresa | Gerenciador de implantação | Gerente do programa | Desenvolvedor |
|--- |--- |--- |--- |--- |--- |
| Adicionar programa | Adicionar novo programa. | x | x | x | x |
| Ler aplicativo | Leia os KPIs do programa. | x | x | x | x |
| Aplicativo de gravação | Configuração ou edição do programa. | x |  |  |  |  |
| Ler ambiente | Consulte Detalhes do ambiente. | x | x | x | x |
| Criar execução | Inicie o Pipeline. | x | x | x |  |
| Execução de leitura | Consulte status de execução. | x | x | x | x |
| Retomar execução | Pode retomar a execução quando pausada. | x | x | x |  | x |
| Execução Aprovar implantação para produção | Fornecer aprovação do GoLive. | x | x | x |  |  |
| Implementação da Programação de Execução para Produção | Agendar implantação de produção. | x | x | x |
| Cancelamento de execução | Cancelar a execução atual. | x | x | x |  |
| Falhas na Porta de Qualidade de Substituição de Execução | Aprovar Falhas Importantes Do Portão De Qualidade. | x | x | x |  |
| Criação de Pipeline | Configuração / Editar Pipeline. |  | x |  |  |
| Leitura do pipeline | Consulte Detalhes do pipeline. | x | x | x | x |
| Gravação de Pipeline | Configuração / Editar Pipeline. |  | x |  |  |
| Modificação de Pipeline Aprovação | Permite editar a opção Proprietário da empresa. |  | x |  |  |
| Leitura da etapa | Consulte os resultados das métricas de qualidade da etapa. | x | x | x | x |
