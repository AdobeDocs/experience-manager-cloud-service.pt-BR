---
title: Notas de versão do Cloud Manager AEM versão as a Cloud Service 2021.3.0
description: Notas de versão do Cloud Manager AEM versão as a Cloud Service 2021.3.0
feature: Release Information
exl-id: f826e0c6-3b1d-44f5-99a2-f792f5df3a55
source-git-commit: 575be022704e998e63162f19c37ece877efef627
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 1%

---

# Notas de versão do Cloud Manager no Adobe Experience Manager as a Cloud Service 2021.3.0 {#release-notes}

Esta página descreve as Notas de versão do Cloud Manager AEM as a Cloud Service 2021.3.0.

## Data de lançamento {#release-date}

A data de lançamento do Cloud Manager AEM as a Cloud Service 2021.3.0 é 11 de março de 2021.

## Cloud Manager {#cloud-manager}

### Novidades {#what-is-new}

* Clientes com ambientes com configurações pré-existentes de Nome de domínio personalizado para [LISTAS DE PERMISSÕES de IP](/help/implementing/cloud-manager/ip-allow-lists/managing-ip-allow-lists.md#pre-existing-cdn), [Certificados SSL](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md#pre-existing-cdn) e [Nomes de Domínio Personalizados](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md#pre-existing-cdn) O verá uma mensagem sobre suas configurações existentes anteriormente e poderá se autoservir por meio da interface do usuário.

* Os usuários com as permissões necessárias agora podem editar um Programa, permitindo que façam o seguinte de maneira automatizada:
   * Adicionar a solução Sites a um programa existente com Ativos ou vice-versa.
   * Remova Sites ou Ativos de um programa existente com Sites e Ativos.
   * Adicione o segundo direito de solução não utilizado a um programa existente ou como um novo Programa.

* **Atualização de manutenção de AEM** agora será exibido para as telas Execução do pipeline e Atividade .

* Se um ambiente estiver hibernado, mas também houver uma atualização de AEM disponível, a variável **Hibernado** o status terá precedência sobre **Atualização disponível**.

* Agora os usuários podem ver suas funções do Cloud Manager selecionando a opção &quot;Exibir função(ões) do Cloud Manager&quot; após navegar até o ícone Perfil do usuário (canto superior direito) do Unified Shell.

* O rótulo **Pedido de aprovação** foi renomeado para **Aprovação de produção** para maior clareza.

* O **Versão** foi renomeado para **Tag Git** na tela Production pipeline execution .

* Os rótulos que definem o comportamento quando métricas importantes não atingirem o limite definido foram renomeados para refletir seu comportamento verdadeiro: **Cancelar imediatamente** e **Aprovar imediatamente**.

* As listas de desaprovação de classe e método foram atualizadas com base na versão `2021.3.4997.20210303T022849Z-210225` do SDK do AEM Cloud Service.

* O pipeline de Produção do Cloud Manager agora incluirá [Teste de interface personalizada](/help/implementing/cloud-manager/functional-testing.md#custom-ui-testing) capacidade.

### Correções de erros  {#bug-fixes}

* O controle de versão do pacote foi ignorado em alguns casos durante AEM atualização por push.

* Alguns problemas de qualidade não foram detectados corretamente quando os pacotes eram incorporados em outros pacotes.

* Em situações obscuras, o nome de programa padrão gerado ao abrir a caixa de diálogo Adicionar programa pode ser uma duplicata de um nome de programa existente.

* Ocasionalmente, se o usuário sair da página de execução do pipeline imediatamente após iniciar um pipeline, uma mensagem de erro será exibida informando que a ação falhou, embora a execução realmente comece.

* A etapa de build foi reiniciada desnecessariamente quando as builds do cliente resultaram em pacotes inválidos.

* Ocasionalmente, o usuário pode ver um status verde &quot;ativo&quot; ao lado de uma  de IP Lista de permissões mesmo quando essa configuração não foi implantada.

* Todos os pipelines de produção existentes serão ativados automaticamente com a etapa Auditoria de experiência.
