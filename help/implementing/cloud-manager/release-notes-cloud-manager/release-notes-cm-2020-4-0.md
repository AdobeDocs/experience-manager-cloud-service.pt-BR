---
title: Notas de versão do Cloud Manager AEM versão as a Cloud Service 2020.4.0
description: Notas de versão do Cloud Manager AEM versão as a Cloud Service 2020.4.0
feature: Release Information
exl-id: 15665fb5-9444-416b-938a-45c31fdce5cf
source-git-commit: 09d5d125840abb6d6cc5443816f3b2fe6602459f
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 77%

---

# Notas de versão do Cloud Manager no Adobe Experience Manager as a Cloud Service 2020.4.0 {#release-notes}

Esta página descreve as Notas de versão do Cloud Manager AEM as a Cloud Service 2020.4.0.

## Data de lançamento {#release-date}

A Data de lançamento do Cloud Manager AEM as a Cloud Service 2020.4.0 é 9 de abril de 2020.

## Novidades {#whats-new-cloud-manager}

* Agora os URLs do editor estão disponíveis na página Ambiente na interface do usuário do Cloud Manager.
* Alterações na navegação para permitir que o usuário edite, alterne ou adicione um programa na página de visão geral do Cloud Manager.
* Alterações para permitir que o usuário edite o programa no cartão de programa na página de aterrissagem do Cloud Manager.
* Novo status de pipeline **Pipeline Running** exibido no ambiente ao qual está associado.
* Melhorias na compreensão da página de execução do pipeline. Isso inclui a exibição do nome (somente para pipeline de não produção) e tipo do Pipeline e um selo para indicar se o status do pipeline é Em andamento/Cancelado/Com falha.
* Dicas de ferramentas para melhorar a experiência do usuário e a compreensão sobre por que o botão Adicionar Programa/Ambiente está desativado.
* Agora ambientes com falha podem ser excluídos por meio da interface do usuário e da API.
* O processo usado para gerar senhas git tornou-se mais resiliente aos problemas na camada de serviço subjacente.

### Correções de erros {#bug-fixes-cloud-manager}

* Os links para o ambiente de preparo na página de detalhes de execução do pipeline não estavam navegando consistentemente para o local correto.
* As etapas individuais no processo de criação do ambiente atingiriam o tempo limite antes do que o necessário, causando a falha do processo.
* A configuração de Maven usada em Criar contêiner foi atualizada para evitar bloqueios ao baixar metadados de artefato.
* Em alguns casos, a etapa Criar imagem não baixaria os pacotes do cliente com êxito.
* Algumas condições raras impediriam a exclusão de ambientes.
* As notificações da Experience Cloud não eram recebidas de forma consistente.
