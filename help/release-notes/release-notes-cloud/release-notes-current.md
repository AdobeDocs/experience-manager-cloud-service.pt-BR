---
title: Notas de versão da versão 2020.8.0 [!DNL Adobe Experience Manager] como Cloud Service.
description: '[!DNL Adobe Experience Manager] como notas de versão do Cloud Service para 2020.8.0.'
translation-type: tm+mt
source-git-commit: 85f5262c2af7502e98fcb60b51b9b13d2c2c0f2c
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 6%

---


# Release Notes for [!DNL Adobe Experience Manager] as a Cloud Service 2020.8.0 {#release-notes}

A seção a seguir descreve as Notas de versão gerais do Experience Manager as a Cloud Service 2020.8.0.

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novidades {#what-is-new-commerce}

* O recurso Console do produto agora está disponível. Isso permite que os profissionais de marketing/autores em AEM visualizações e naveguem por categorias e produtos armazenados no backend de comércio. Também é fornecido suporte para propriedades de categorias e produtos no console de produtos.

* Os seletores de produto e Categoria foram aprimorados para permitir que os profissionais de marketing selecionem o produto por SKU ou selecionem a categoria por meio da ID da categoria.

## Cloud Manager {#cloud-manager}

### Data de lançamento {#release-date-cm}

The Release Date for [!UICONTROL Cloud Manager] Version 2020.8.0 is August 06, 2020.

### Novidades {#what-is-new-cloud-manager}

* A Auditoria de conteúdo é um recurso ativado nos Pipelines de Produção de Sites do Cloud Manager. A configuração do pipeline de produção para programas com Sites agora inclui uma terceira guia chamada Auditoria **de** conteúdo. Sempre que um pipeline de produção for executado, uma nova etapa de Auditoria de conteúdo será incluída no pipeline após um teste funcional personalizado que avaliará o site em relação a várias dimensões, incluindo desempenho, SEO (Search Engine Otimization), acessibilidade, práticas recomendadas e PWA (Progressive Web App).

   Refer to [Content Audit Testing](/help/implementing/developing/introduction/understand-test-results.md#content-audit-testing) for more details.

* Ambientes recém-criados em programas do Assets agora serão configurados automaticamente com o Smart Content Services.

* Ambientes hibernados podem ser removidos da hibernação na página **Visão geral** do Gerenciador de nuvem.

* Agora há suporte para Repositórios de Maven Privado com vínculo de autenticação.

### Correções de erros {#bug-fixes-cm}

* Alguns plug-ins SonarQube desnecessários e indesejados estavam sendo executados como parte da verificação de qualidade de código.

* Na página de execução de pipeline, o nome da ramificação estava formatado incorretamente.

* Em alguns casos, as execuções de pipeline concluídas não foram registradas com êxito como tendo sido concluídas, impedindo assim novas execuções do pipeline.

* Ocasionalmente, as execuções de tubulação ficariam *presas* devido a problemas de comunicação interna.

* Ao provisionar uma nova organização, alguns usuários com funções administrativas diferentes dos administradores de sistema receberam erroneamente acesso ao Cloud Manager.

* Em determinadas condições, o trabalho de índices de atualização foi iniciado várias vezes em paralelo, resultando em uma falha de implantação.

* A dica de ferramenta nos cartões de programa não estava consistentemente correta.

* A interface do usuário permitia erroneamente que as operações fossem tentadas em um ambiente durante sua exclusão.

* Ocorreu uma incompatibilidade de cores na página **Visão geral** do Gerenciador de nuvem.

### Problemas conhecidos {#known-issues-cm}

* As páginas inválidas são incluídas, colocando a Pontuação média de auditoria de conteúdo abaixo do que deveriam ser.

* A guia Auditoria de conteúdo exibe incorretamente o URL base usando o domínio do autor em vez do domínio de publicação.

* Para ativar a etapa Auditoria de conteúdo, os usuários devem editar o pipeline e, opcionalmente, adicionar páginas. Se nenhuma página for adicionada, a página inicial será auditada.

