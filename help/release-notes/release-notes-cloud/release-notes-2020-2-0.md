---
title: Notas de versão para 2020.2.0
description: Notas de versão para 2020.2.0
translation-type: ht
source-git-commit: e9514d2ba625a7df8a8126f5b0ab74b975eeda51

---


# Notas de versão para AEM as a Cloud Service 2020.2.0{#release-notes}

A seção a seguir descreve as Notas de versão gerais para Experience Manager as a Cloud Service 2020.2.0.

## Cloud Manager {#cloud-manager}

A data de lançamento do Cloud Manager versão 2020.2.0 é quinta-feira, 13 de fevereiro de 2020.

Siga esta seção para saber mais sobre as novidades e as atualizações do Cloud Manager Versão 2020.2.0.

### Novidades {#what-is-new}

* A versão do arquétipo do Adobe Experience Manager foi atualizada para a versão 22.
* Os ambientes de Preparo e Produção nos programas Sandbox/Demo já podem ser atualizados por meio da interface do usuário do Cloud Manager.
* Os URLs usados nas notificações da Experience Cloud foram otimizados para evitar um redirecionamento extra.
* As etapas de execução do pipeline que expiraram agora indicam isso explicitamente.
* A etapa de Verificação de código agora tem um registro que pode ser baixado.
* A planilha que contém os problemas detectados durante a verificação de código agora tem uma coluna com um link para a documentação da regra específica.

### Correções de erros {#bug-fixes}

* Às vezes, as políticas de segurança do navegador impediam que determinados botões na tela de execução do pipeline funcionassem corretamente.
* Os links Visão geral, Ambientes e Atividade às vezes ficavam disponíveis na página de aterrissagem do Cloud Manager.
* Certas falhas na implantação poderiam impedir erroneamente a criação de novos pipelines.