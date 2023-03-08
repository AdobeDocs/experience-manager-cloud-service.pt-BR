---
title: Notas de versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
source-git-commit: edb8949b532b80a55106e706a49e2ada68722a67
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 6%

---


# Notas de versão de manutenção {#maintenance-release-notes}

A seção a seguir descreve as rotas de lançamento técnico para a versão de manutenção mais recente do Experience Manager as a Cloud Service.

## Versão 11289 {#release-11289}

Veja abaixo um resumo das melhorias contínuas da versão de manutenção 11289, lançada publicamente em 7 de março de 2023. Esta versão de manutenção é uma atualização da versão de manutenção anterior 10912.

A ativação de recursos para esta versão de manutenção fornecerá o conjunto completo de recursos. Consulte a [notas de versão atuais](/help/release-notes/release-notes-cloud/release-notes-current.md) para obter detalhes completos.

### Problemas conhecidos {#known-issues}

Não atualize se estiver usando o CORS. Um problema que afeta a funcionalidade de entrega de conteúdo do GraphQL foi identificado nesta versão. Uma alteração na configuração padrão do dispatcher AEM em relação ao modo como as consultas persistentes do GraphQL são armazenadas em cache pode interromper a entrega de conteúdo do GraphQL dessas consultas. Esse problema será corrigido na próxima versão de manutenção.

### Problemas corrigidos {#fixed-issues}

#### Sites {#sites-issues}

- SITES-11584 Corrigido um problema com Live Copies que não podia ser criado para páginas com anotações
- SITES-11683 Live Copies do MSM desativadas com herança parcialmente interrompida

#### Assets {#assets-issues}

- ASSETS-20879 Regressão fixa que impedia o funcionamento correto da interface do usuário dos relatórios de ativos e resultava em resultados incorretos nos relatórios gerados.
- ATIVOS-21020 Problema corrigido com o download de ativos corrompido - O perfil de imagem não existe após mover o ativo
- ASSETS-21023 Correção de um problema com representações de imagem no Dynamic Media que impedia o acesso por meio da API

#### Forms {#forms-issues}

- Nenhum

#### Plataforma {#platform-issues}

- GRANITE-44467 - Corrigido o problema que causava a falha da importação ao atualizar um nó existente, o Filevault em determinadas instâncias não preservava os tipos de mixin e nós filhos

### Tecnologias integradas {#embedded-tech}

| Tecnologia | Versão | Link |
|---|---|---|
| AEM OAK | 1.44-T20221206170501-6d59064 | [API Oak API 1.44.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.44.0/index.html) |
| API AEM SLING | Versão 2.27.0 | [API Apache Sling 2.27.0](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| HTL do AEM | Versão 1.4.20-1.4.0 | [Especificação de linguagem do modelo HTML](https://github.com/adobe/htl-spec) |
| Componentes principais do AEM | Versão 2.21.2 | [Componentes principais do WCM no AEM](https://github.com/adobe/aem-core-wcm-components) |
