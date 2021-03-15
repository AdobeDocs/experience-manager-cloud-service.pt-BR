---
title: Notas de versão do Cloud Manager no AEM as a Cloud Service versão 2021.3.0
description: Notas de versão do Cloud Manager no AEM as a Cloud Service versão 2021.3.0
translation-type: tm+mt
source-git-commit: 36e5e90785a1bc9a4f4f8d4febd462e00252a0ea
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 1%

---


# Notas de versão do Cloud Manager no Adobe Experience Manager as a Cloud Service 2021.3.0 {#release-notes}

Esta página descreve as Notas de versão do Cloud Manager no AEM as a Cloud Service 2021.3.0.

## Data de lançamento {#release-date}

A Data de lançamento do Cloud Manager no AEM as a Cloud Service 2021.3.0 é 11 de março de 2021.
A próxima versão está planejada para 8 de abril de 2021.

## Cloud Manager {#cloud-manager}

### Novidades {#what-is-new}

* Os clientes com ambientes com configurações pré-existentes de Nome de domínio personalizado para [Lista de permissões IP](/help/implementing/cloud-manager/ip-allow-lists/check-ip-allow-list-status.md#pre-existing-cdn), [Certificados SSL](/help/implementing/cloud-manager/managing-ssl-certifications/check-status-ssl-certificate.md#pre-existing-cdn) e [Nomes de domínio personalizados](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md#pre-existing-cdn) verão uma mensagem sobre suas configurações existentes anteriormente e poderão se autoservir por meio da interface do usuário.

* Os usuários com as permissões necessárias agora podem editar um Programa, permitindo que façam o seguinte de maneira automatizada:
   * Adicionar a solução Sites a um programa existente com Ativos (ou vice-versa).
   * Remova Sites (ou Ativos) de um programa existente com Sites e Ativos.
   * Adicione o segundo direito de solução não utilizado a um programa existente ou como um novo Programa.

* AEM &quot;Atualização de push&quot; agora será exibido para as telas Execução de pipeline e Atividade.

* Se um ambiente estiver hibernado, mas também houver uma atualização de AEM disponível, o status &quot;Hibernado&quot; terá prioridade sobre &quot;Atualização disponível&quot;.

* Agora os usuários podem ver suas funções do Cloud Manager selecionando a opção &quot;Exibir função(ões) do Cloud Manager&quot; após navegar até o ícone Perfil do usuário (canto superior direito) do Unified Shell.

* O rótulo &quot;Pedido de aprovação&quot; foi renomeado para &quot;Aprovação de produção&quot; para maior clareza.

* O rótulo &quot;Versão&quot; foi renomeado para &quot;Git Tag&quot; na tela de execução do pipeline de Produção.

* Os rótulos que definem o comportamento quando métricas importantes não alcançam o limite definido foram renomeados para refletir seu comportamento verdadeiro - Cancelar imediatamente e Aprovar imediatamente.

* As listas de desaprovação de classe e método foram atualizadas com base na versão `2021.3.4997.20210303T022849Z-210225` do SDK do Cloud Service AEM.

* O pipeline de Produção do Cloud Manager agora incluirá o recurso de teste da interface de usuário personalizada.

### Correções de erros {#bug-fixes}

* O controle de versão do pacote foi ignorado em alguns casos durante AEM atualização por push.

* Alguns problemas de qualidade não foram detectados corretamente quando os pacotes eram incorporados em outros pacotes.

* Em situações obscuras, o nome de programa padrão gerado ao abrir a caixa de diálogo Adicionar programa pode ser uma duplicata de um nome de programa existente.

* Ocasionalmente, se o usuário sair da página de execução do pipeline imediatamente após iniciar um pipeline, uma mensagem de erro será exibida informando que a ação falhou, embora a execução realmente comece.

* A etapa de build foi reiniciada desnecessariamente quando as builds do cliente resultaram em pacotes inválidos.

* Ocasionalmente, o usuário pode ver um status verde &quot;ativo&quot; ao lado de uma  de IP Lista de permissões mesmo quando essa configuração não foi implantada.

* Todos os pipelines de produção existentes serão ativados automaticamente com a etapa Auditoria de experiência.