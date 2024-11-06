---
title: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 90e1ca38bd517215a631573987462a716bfed160
workflow-type: tm+mt
source-wordcount: '629'
ht-degree: 17%

---


# Notas da versão de manutenção {#maintenance-release-notes}

A seção a seguir descreve as notas de versão técnicas para a versão de manutenção atual do Experience Manager as a Cloud Service.

## Versão 18459 {#18459}

Veja abaixo um resumo das melhorias contínuas da versão de manutenção 18459, lançada publicamente em quarta-feira, 5 de novembro de 2024. A versão de manutenção anterior era a versão 18311.

A ativação de recursos do 2024.11.0 fornecerá o conjunto completo de recursos para esta versão de manutenção. Consulte o [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obter mais informações.

### Aprimoramentos {#enhancements-18459}

* CQ-4357471: adição de suporte para tradução de dicionários i18n no AEMaaCS.
* SITES-23591: Fragmentos de conteúdo: atualização de fragmento de conteúdo para suporte a UUID.
* SITES-25440: Fragmentos de conteúdo: API de pesquisa CFM para mostrar o status de replicação.
* SITES-24369: Fragmentos de conteúdo: melhorias na documentação da OpenAPI.
* SITES-25478: fragmentos de conteúdo: adicione suporte de back-end para referências de ativos externos.
* SITES-26119: Fragmentos de conteúdo: adicione suporte a referências de ativos externos no tipo de referência.
* SITES-21199: Edge Delivery com Universal Editor: adicionar suporte para modelos criados a partir de páginas.
* SITES-20311: Edge Delivery com editor universal: adicione suporte para importar CSVs para planilhas.
* SITES-24821: Edge Delivery com Universal Editor: torne aem.page / aem.live o padrão para integrar com o Edge Delivery.

### Problemas corrigidos {#fixed-issues-18459}

* CQ-4358730: CQPagePreviewGenerator falha quando há mais de 10 chaves a serem traduzidas.
* FORMS-14978: Ativação do carregamento de página para um formulário baseado em Componente principal para o editor de tema.
* FORMS-16596: Problema de acessibilidade: botões desativados não reconhecidos pelo Reader de tela.
* SITES-10575: MSM: O carregador de bloomfilter de blueprint tenta carregar >100.000 linhas.
* SITES-20755: Fragmentos de conteúdo: a referência de ativo com atualização de UUID não mostra a miniatura.
* SITES-26253: Fragmentos de conteúdo: Migração de UUID: alterar o tópico de trabalho do sling para genérico.
* SITES-21338: Fragmentos de conteúdo: o endpoint referencedBy não retorna a referência de página correta.
* SITES-24421: Fragmentos de conteúdo: editar o ponto de extremidade do CF não funciona para o CF recuperado via GET CF.
* SITES-25461: Fragmentos de conteúdo: filtre por modelo na pesquisa de CFs não deve diferenciar maiúsculas de minúsculas.
* SITES-25471: Fragmentos de conteúdo: corrigir a validação de modelos globais no ModelValidatorServlet.
* SITES-25795: Fragmentos de conteúdo: a API do modelo CF falha quando não há data de cq definida.
* SITES-25817: Fragmentos de conteúdo: aprimorar promoteLaunch: atualizar última promoção para Lançamentos de CF.
* SITES-26030: Fragmentos de conteúdo: Endpoint /referencesTree não retorna o cabeçalho necessário.
* SITES-26031: Fragmentos de conteúdo: status de replicação não retornado no endpoint de pesquisa CFM.
* SITES-26213: fragmentos de conteúdo: desfazer a publicação de fragmentos de conteúdo deve validar somente as referências publicadas.
* SITES-26226: Fragmentos de conteúdo: inicia um problema de fluxo de trabalho quando nenhum dos caminhos fornecidos é utilizável.
* SITES-26238: Fragmentos de conteúdo: as referências de ativos retornadas pela API têm uma ordem diferente da ordem do JCR.
* SITES-25456: eventos: ao mover uma página, um evento de exclusão de página é gerado além do evento de movimentação de página.
* SITES-25658: Eventos: a camada e sourceUrl não são preenchidas nos eventos de estado de conteúdo da página.
* SITES-6497: Inicializações: a página Criar na inicialização não funciona.
* SITES-25938: inicializações: exclusão inesperada após o projeto de tradução.
* SITES-25393: Edge Delivery com Universal Editor: nós de texto perdidos ao renderizar richtext formatado com parágrafo único.
* SITES-24643: Edge Delivery com Universal Editor: os atributos de metadados OpenGraph e twitter não funcionam no modelo de metadados da página.
* SITES-25401: Fragmentos de experiência: atualização de referência XF lenta


### Problemas conhecidos {#known-issues-18459}

Nenhum.

### Recursos e APIs obsoletos {#deprecated-18459}

Os recursos e APIs obsoletos e removidos do AEM as a Cloud Service estão detalhados no documento [Recursos e APIs obsoletos e removidos](/help/release-notes/deprecated-removed-features.md).

### Correções de segurança {#security-18459}

A AEM as a Cloud Service dedica-se a otimizar a segurança e o desempenho da sua plataforma. Esta versão de manutenção aborda 21 vulnerabilidades identificadas, reforçando nosso compromisso com a proteção robusta do sistema.

### Tecnologias integradas {#embedded-tech-18459}

| Tecnologia | Versão | Link |
|---|---|---|
| AEM Oak | 1.70.0 | [API Oak API 1.70.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.70.0/index.html) |
| API DO SLING DO AEM | 2.27.6 | [API Apache Sling API 2.27.6](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| HTL do AEM | 1.4.24-1.4.0 | [Especificação da linguagem de modelo HTML](https://github.com/adobe/htl-spec) |
| Componentes principais do AEM | 2.27.0 | [Componentes principais de WCM do AEM](https://github.com/adobe/aem-core-wcm-components) |
