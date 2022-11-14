---
title: Notas de versão do Cloud Manager no AEM as a Cloud Service versão 2021.3.0
description: Notas de versão do Cloud Manager no AEM as a Cloud Service versão 2021.3.0
feature: Release Information
exl-id: f826e0c6-3b1d-44f5-99a2-f792f5df3a55
source-git-commit: 575be022704e998e63162f19c37ece877efef627
workflow-type: ht
source-wordcount: '447'
ht-degree: 100%

---

# Notas de versão do Cloud Manager no Adobe Experience Manager as a Cloud Service 2021.3.0 {#release-notes}

Esta página descreve as notas de versão do Cloud Manager no AEM as a Cloud Service 2021.3.0.

## Data de lançamento {#release-date}

A data de lançamento do Cloud Manager no AEM as a Cloud Service 2021.3.0 é 11 de março de 2021.

## Cloud Manager {#cloud-manager}

### Novidades {#what-is-new}

* Clientes que tenham ambientes com configurações pré-existentes de nomes de domínio personalizados para [Listas de permissões de IP](/help/implementing/cloud-manager/ip-allow-lists/managing-ip-allow-lists.md#pre-existing-cdn), [Certificados SSL](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md#pre-existing-cdn) e [Nomes de domínio personalizados](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md#pre-existing-cdn) verão uma mensagem sobre essas configurações pré-existentes e poderão realizar ações por autoatendimento por meio da interface do usuário.

* Os usuários com as permissões necessárias agora podem editar um programa, permitindo fazer o seguinte de maneira automatizada:
   * Adicionar a solução do Sites a um programa existente com o Assets, e vice-versa.
   * Remover sites ou ativos de um programa existente usando o Sites e o Assets.
   * Adicionar o segundo direito de solução não utilizado a um programa existente ou como um novo programa.

* O rótulo **Atualização de manutenção do AEM** agora será exibido para as telas Execução do pipeline e Atividade.

* Se um ambiente estiver hibernado, mas também houver uma atualização do AEM disponível, o status **Hibernado** terá precedência sobre a **Atualização disponível**.

* Agora os usuários podem ver suas funções do Cloud Manager selecionando a opção “Exibir função(ões) do Cloud Manager” após navegar até o ícone Perfil do usuário (canto superior direito) do Unified Shell.

* O rótulo **Pedido de aprovação** foi renomeado para **Aprovação de produção** para maior clareza.

* O rótulo **Versão** foi renomeado para **Tag do Git** na tela Execução do pipeline de produção.

* Os rótulos que definem o comportamento quando métricas importantes não atingem o limite definido foram renomeados para refletir seu real comportamento: **Cancelar imediatamente** e **Aprovar imediatamente**.

* As listas de reprovação de classe e método foram atualizadas com base na versão `2021.3.4997.20210303T022849Z-210225` do SDK do AEM Cloud Service.

* O pipeline de produção do Cloud Manager agora incluirá a capacidade de [teste de interface personalizado](/help/implementing/cloud-manager/functional-testing.md#custom-ui-testing).

### Correções de erros  {#bug-fixes}

* O controle de versão do pacote foi ignorado em alguns casos durante a atualização por push do AEM.

* Alguns problemas de qualidade não eram detectados corretamente quando os pacotes eram incorporados em outros pacotes.

* Em situações obscuras, o nome de programa padrão gerado ao abrir a caixa de diálogo Adicionar programa podia ser uma duplicata de um nome de programa existente.

* Ocasionalmente, se o usuário saísse da página de execução do pipeline imediatamente após iniciar um pipeline, uma mensagem de erro seria exibida informando que a ação falhou, embora a execução realmente começasse.

* A etapa de compilação foi reiniciada desnecessariamente quando as compilações do cliente resultaram em pacotes inválidos.

* Ocasionalmente, o usuário podia ver um status verde “ativo” ao lado de uma de lista de permissões de IP, mesmo quando essa configuração não era implantada.

* Todos os pipelines de produção existentes serão habilitados automaticamente na etapa Auditoria de experiência.
