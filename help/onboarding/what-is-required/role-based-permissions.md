---
title: Permissões baseadas em função
description: Permissões baseadas em função
translation-type: tm+mt
source-git-commit: 645c1e72adeafe437851930a68c9cf905ef0539f

---


# Permissões baseadas em função {#role-based-permissions}

[!UICONTROL O Cloud Manager] tem funções pré-configuradas com permissões apropriadas. Por exemplo, um desenvolvedor desenvolve código e tem permissão para enviar o código para o Repositório **Git**. Como alternativa, um proprietário de negócios tem permissões diferentes que permitem definir os Indicadores-chave de desempenho (KPIs) e aprovar implantações.

## Permissões de usuário {#user-permissions}

Cada uma das funções tem permissões específicas, tarefas pré-configuradas ou permissões associadas a cada função. Esta tabela lista as funções disponíveis e as funções que podem executar a função.

| Permissão | Descrição | Proprietário da empresa | Gerenciador de implantação | Gerente do programa | Desenvolvedor |
|--- |--- |--- |--- |--- |--- |
| Criar inquilino | Criar um novo inquilino. |  |  |  |  |
| Atualizar Locatário | Atualizar Locatário. |  |  |  |  |
| Adicionar programa | Adicionar um novo programa. | x |  |  |  |
| Criar ambiente | Crie Ambientes Prod+Stage, Dev, Playground. | x | x |  |  |
| Configurar variáveis de ambiente | Configurar variáveis e segredos de ambiente. |  | x |  | x |
| Adicionar ou remover nome de domínio personalizado, carregar ou atualizar certificado SSL | Adicionar / Remover Nome de Domínio Personalizado, Carregar / Atualizar Certificado SSL. | x | x |  |  |
| Atualizar ambiente | Atualize Ambientes Prod+Stage, Dev, Playground. | x | x |  |  |
| Excluir ambiente | Exclua Ambientes sem produção, Desenvolvimento e Reprodução. | x | x |  |  |
| Excluir ambiente | Excluir Prod+Stage Environment. |  |  |  |  |
| Configuração do programa | Configurar programa (incluindo KPIs). | x |  |  |  |
| Configuração do programa | Confirmar acesso. |  | x |  | x |
| Configuração de pipeline | Configure ou edite o pipeline. |  | x |  |  |
| Execução do pipeline | Inicie o Pipeline. | x | x |  |  |
| Execução do pipeline | Rejeitar/Aprovar Falhas Importantes De 3 Camadas. | x | x | x |  |
| Execução do pipeline | Fornecer aprovação do GoLive. | x | x | x |  |
| Execução do pipeline | Agendar implantação de produção. | x | x | x |  |
| Execução do pipeline | Retomar Pipeline de Produção. |  |  |  |  |
| Gerenciar ambiente | Adicione o segmento Publicar-Dispatcher da tela Gerenciar ambiente. | x | x |  |  |  |
| Atualização de push | Inicie o pipeline de atualização de push. |  |  |  |  |
| Gerar token de acesso pessoal | Gerar token de acesso pessoal. |  | x |  | x |

