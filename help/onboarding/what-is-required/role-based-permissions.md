---
title: Permissões baseadas em função
description: Permissões baseadas em função
translation-type: tm+mt
source-git-commit: 3c56d94f9922cb65b91912dd96eb8aa60efc2b53
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 23%

---


# Permissões baseadas em função {#role-based-permissions}

[!UICONTROL O Cloud Manager tem funções pré-configuradas com permissões apropriadas.] Por exemplo, um desenvolvedor desenvolve código e tem permissão para enviar o código para o Repositório **Git**. Como alternativa, um proprietário de negócios tem permissões diferentes que permitem definir os Indicadores-chave de desempenho (KPIs) e aprovar implantações.

## Permissões de usuário {#user-permissions}

Cada uma das funções tem permissões específicas, tarefas pré-configuradas ou permissões associadas a cada função. Esta tabela lista as funções disponíveis e as funções que podem executar a função.

| Permissão | Descrição | Proprietário da empresa | Gerenciador de implantação | Gerenciador de programas | Desenvolvedor |
|--- |--- |--- |--- |--- |--- |
| Adicionar Programa | Adicionar um novo Programa. | x |  |  |  |
| Criar Ambiente | Crie Ambientes Prod+Stage, Dev, Playground. | x | x |  |  |
| Atualizar Ambiente | Atualize Ambientes Prod+Stage, Dev, Playground. | x | x |  |  |
| Excluir Ambiente | Exclua Ambientes Não Prod, Dev, Playground. | x | x |  |  |
| Excluir Ambiente | Excluir Prod+Ambiente de Palco. |  |  |  |  |
| Configuração do Programa | Configure o Programa (incluindo KPIs). | x |  |  |  |
| Configuração do Programa | Confirmar acesso. |  | x |  | x |
| Configuração de pipeline | Configure ou edite o pipeline. |  | x |  |  |
| Execução do pipeline | Start o Pipeline. | x | x |  |  |
| Execução do pipeline | Rejeitar/Aprovar Falhas Importantes De 3 Camadas. | x | x | x |  |
| Execução do pipeline | Fornecer aprovação do GoLive. | x | x | x |  |
| Execução do pipeline | Agendar implantação de produção. | x | x | x |  |
| Execução do pipeline | Retomar Pipeline de Produção. |  |  |  |  |
| Exclusão de Pipeline | Permite a exclusão de um pipeline. |  | x |  |  |
| Cancelamento de execução | Cancelar Execução Atual. |  | x |  |  |
| Gerenciar Ambiente | Adicione o segmento Publicar-Dispatcher da tela Gerenciar Ambiente. | x | x |  |  |  |
| Atualização de push | Pipeline de atualização de push de Start. |  |  |  |  |
| Gerar Token de acesso pessoal | Git de acesso. |  | x |  | x |

