---
title: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 80affbf9d68de5cdba884ea7c7b277d834816613
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 19%

---


# Notas da versão de manutenção {#maintenance-release-notes}

A seção a seguir descreve as notas de versão técnicas para a versão de manutenção atual do Experience Manager as a Cloud Service.

## Versão 25194 {#25194}

Veja abaixo um resumo das melhorias contínuas da versão de manutenção 25194, lançada publicamente em quinta-feira, 1 de abril de 2026. A versão de manutenção anterior era 24678.

A ativação de recursos do 2026.4.0 fornece o conjunto completo de recursos para esta versão de manutenção. Consulte o [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/pt-br/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obter mais informações.

>[!NOTE]
>
>A versão 24893 foi tornada privada.

### Aprimoramentos {#enhancements-25194}

* ASSETS-65127: Metadados personalizados do evento: tratamento aprimorado de nomes de metadados.
* ASSETS-63313: crie links relacionados automaticamente para ativos e pais exportados com base em manifestos C2PA.
* ASSETS-10995: limite o número de ativos em um zip de download.

### Problemas corrigidos {#fixed-issues-25194}

* ASSETS-62882: Visualização do administrador: a dica de ferramenta info é interrompida quando vários nomes de arquivo inválidos são carregados.
* ASSETS-63642: O link de compartilhamento falha ao renderizar o ativo em alguns ambientes de desenvolvimento (SLA3).
* ASSETS-59267: NPE ao carregar metadados de aplicativo para carga do delivery.
* ASSETS-59227: Exportação de metadados: as propriedades não selecionadas não são mais incluídas devido à correspondência de regex.
* ASSETS-65187: visualização de CSV na nuvem quando os dados da coluna contêm vírgulas de escape.
* ASSETS-63441: Verifique se todos os usuários têm permissão para ler a configuração do Assets Omnisearch.
* SITES-40095: Editor de metadados: o fragmento de conteúdo local faz referência a mais de 10 entradas.

#### Guias do AEM {#guides-25194}

* GUIDES-38412 : Ao editar um arquivo do Schematron `(*.sch)` e usar o recurso localizar e substituir, o painel localizar e substituir aparece parcialmente fora da tela na parte inferior, impedindo o acesso aos campos e controles de entrada.
* GUIDES-37806: Quando o mesmo tópico é reutilizado em vários mapas com diferentes predefinições condicionais, a publicação do mapa mais recente no Salesforce substitui o conteúdo do tópico, resultando na exibição de dados incorretos para os usuários de mapas publicados anteriormente.
* GUIDES-39394: Quando uma imagem gerenciada inicialmente como um ativo específico de idioma com uma versão específica (por exemplo, em `/en/`) é movida para uma pasta global com uma versão atualizada e a exportação da linha de base é executada, a nova linha de base continua a fazer referência a versões desatualizadas específicas do idioma dessa imagem, resultando em uma falha na exportação da linha de base.
* GUIDES-39054: Ao criar uma linha de base dinâmica, o Editor às vezes fica sem responder devido a várias solicitações de API simultâneas, fazendo com que todas as outras operações travem.
* GUIDES-37781: Ao atribuir um usuário a uma tarefa de revisão, a lista suspensa lista todos os usuários em vez de apenas aqueles associados aos projetos selecionados, resultando em opções de usuário inválidas.
* GUIDES-39385: Ao abrir um Relatório para um mapa, há um atraso no carregamento do painel Filtros.

Para obter mais informações sobre recursos e problemas novos e aprimorados corrigidos nessa versão, exiba o [roteiro de versão do Experience Manager Guides](https://experienceleague.adobe.com/pt-br/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap).

### Problemas conhecidos {#known-issues-25194}

Nenhum.

### Recursos e APIs obsoletos {#deprecated-25194}

Os recursos e APIs obsoletos e removidos do AEM as a Cloud Service estão detalhados no documento [Recursos e APIs obsoletos e removidos](/help/release-notes/deprecated-removed-features.md).

### Correções de segurança {#security-25194}

A AEM as a Cloud Service dedica-se a otimizar a segurança e o desempenho da sua plataforma. Esta versão de manutenção aborda 9 vulnerabilidades identificadas, reforçando nosso compromisso com a proteção robusta do sistema.

### Tecnologias integradas {#embedded-tech-25194}

| Tecnologia | Versão | Link |
|---|---|---|
| AEM Oak | 1.90.0 | [API do Oak 1.90.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.90.0/index.html) |
| API DO SLING DO AEM | 2.27.6 | [API Apache Sling API 2.27.6](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| HTL do AEM | 1.4.28-1.4.0 | [Especificação da linguagem de modelo HTML](https://github.com/adobe/htl-spec) |
| Apache HTTP Server | 2.4.65 | [Apache Httpd 2.4.65](https://apache.googlesource.com/httpd/+/refs/tags/2.4.65/CHANGES) |
| Componentes principais do AEM | 2.30.4 | [Componentes principais de WCM do AEM](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14 (padrão) | [Versões Node.js com suporte](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |
