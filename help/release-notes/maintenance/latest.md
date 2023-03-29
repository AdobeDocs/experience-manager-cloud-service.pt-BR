---
title: Notas da versão de manutenção mais recente do  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Notas da versão de manutenção mais recente do  [!DNL Adobe Experience Manager]  as a Cloud Service.
source-git-commit: edb8949b532b80a55106e706a49e2ada68722a67
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 100%

---


# Notas da versão de manutenção {#maintenance-release-notes}

A seção a seguir descreve as rotas de lançamento técnico para a versão de manutenção mais recente do Experience Manager as a Cloud Service.

## Versão 11289 {#release-11289}

Veja abaixo um resumo das melhorias contínuas da versão de manutenção 11289, lançada publicamente em 7 de março de 2023. Esta versão de manutenção é uma atualização da versão de manutenção anterior: 10912.

A ativação de recursos desta versão de manutenção fornecerá o conjunto completo de recursos. Consulte as [notas de versão atuais](/help/release-notes/release-notes-cloud/release-notes-current.md) para obter detalhes completos.

### Problemas conhecidos {#known-issues}

Não atualize se estiver usando o CORS. Um problema que afeta a funcionalidade de entrega de conteúdo GraphQL foi identificado nesta versão. Uma alteração na configuração padrão do Dispatcher do AEM, em relação ao modo como as consultas persistentes de GraphQL são armazenadas em cache, pode interromper a entrega de conteúdo GraphQL de tais consultas. Esse problema será corrigido na próxima versão de manutenção.

### Problemas corrigidos {#fixed-issues}

#### Sites {#sites-issues}

- SITES-11584 Corrigido um problema com live copies que não podiam ser criadas para páginas com anotações
- SITES-11683 Desativação de live copies do MSM que possuíam uma herança parcialmente corrompida

#### Assets {#assets-issues}

- ASSETS-20879 Corrigida a regressão que impedia o funcionamento correto da interface dos relatórios de ativos e exibia resultados incorretos nos relatórios gerados.
- ASSETS-21020 Corrigido um problema com o download de ativos corrompidos: o perfil de imagem deixava de existir após mover o ativo
- ASSETS-21023 Corrigido um problema com representações de imagem no Dynamic Media que impediam o acesso por meio da API

#### Forms {#forms-issues}

- Nenhum

#### Platform {#platform-issues}

- GRANITE-44467 - Corrigido um problema que causava a falha da importação ao atualizar um nó existente; em determinadas instâncias, o Filevault não preservava os tipos de mixin e os nós secundários

### Tecnologias integradas {#embedded-tech}

| Tecnologia | Versão | Link |
|---|---|---|
| AEM OAK | 1.44-T20221206170501-6d59064 | [API Oak 1.44.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.44.0/index.html) |
| API do Sling do AEM | Versão 2.27.0 | [API do Apache Sling 2.27.0](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| HTL do AEM | Versão 1.4.20-1.4.0 | [Especificação da linguagem de modelo HTML](https://github.com/adobe/htl-spec) |
| Componentes principais do AEM | Versão 2.21.2 | [Componentes principais de WCM do AEM](https://github.com/adobe/aem-core-wcm-components) |
