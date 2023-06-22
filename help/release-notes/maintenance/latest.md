---
title: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: 46f0f8ba51b328bef1061d574b0d378a510fcf38
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 31%

---

# Notas da versão de manutenção {#maintenance-release-notes}

A seção a seguir descreve as notas de versão técnicas para a versão de manutenção atual do Experience Manager as a Cloud Service.

## Versão 12255 {#release-12255}

Veja abaixo um resumo das melhorias contínuas da versão de manutenção 12255, lançada publicamente em 13 de junho de 2023. Esta versão de manutenção é uma atualização da versão de manutenção anterior a 12142.

A ativação de recursos para esta versão de manutenção fornecerá o conjunto completo de recursos com a ativação de recursos 2023.6.0. Consulte a [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=pt-BR) para obter mais informações.

### Aprimoramentos {#enhancements-12255}

Nenhum.

### Problemas corrigidos {#fixed-issues-12255}

- Várias atualizações relacionadas à acessibilidade
- ASSETS-15116 - A opção &quot;Ir para o local&quot; está disponível na exibição de pesquisa do Assets
- ASSETS-17453 - (Dynamic Media) Não é possível selecionar uma miniatura personalizada para vídeos
- ASSETS-19279 - Arquivo de download de ativos para arquivos grandes
- ASSETS-19544 - Última modificação feita pelo usuário para atualizações de ativos
- ASSETS-20146 - (Interface para toque) Relatórios de falha no download de ativos devido a erros de validação são exibidos sempre na parte superior da página de lista para relatórios
- ASSETS-21056 - Otimiza o desempenho de referência de ativos para minimizar gravações
- ASSETS-21909 - Não é possível ver o vídeo de recorte inteligente quando a vtt falha no download
- ASSETS-22261 - A estrutura de pastas de downloads do Linkshare é inconsistente com downloads da interface do usuário do Assets
- ASSETS-22550 - O painel Filtro de pesquisa agora está aberto por padrão
- ASSETS-22920 - O cancelamento da publicação da pasta do Brand Portal não marca os ativos no como não publicados
- ASSETS-22922 - Predefinições do visualizador desativado exibidas no componente Dynamic Media
- ASSETS-23461 - Publicação rápida do Brand Portal a partir da exibição de pesquisa do Assets
- ASSETS-23466 - O tratamento de links inacessíveis do InDesign Server falha ao resolver links AAL que contêm espaços
- ASSETS-23469 - Os filtros de ativos padrão colidem com filtros personalizados
- ASSETS-23981 - Função de classificação para títulos que não funcionam em links de coleção
- ASSETS-24723 - Os ativos publicados foram reprocessados sem intervenção do usuário
- GRANITE-45385 - Migrar ativação de árvore para usar o trabalho do sling em vez do fluxo de trabalho

### Problemas conhecidos {#known-issues-12255}

- ASSETS-25729 - O menu do alternador de exibição está cortado
- ASSETS-25728 - Opção Reprocessar ativo não disponível na exibição de pesquisa
- ASSETS-22603 - Algumas colunas do Relatório de ativos do tipo Download exibem valores &quot;nulos&quot; na interface. O CSV para download não é afetado.

### Tecnologias integradas {#embedded-tech-12255}

| Tecnologia | Versão | Link |
|---|---|---|
| AEM OAK | 1.50-T20230405052634-f9df4aa | [API Oak 1.50.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.50.0/index.html) |
| API do Sling do AEM | Versão 2.27.0 | [API do Apache Sling 2.27.0](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| HTL do AEM | Versão 1.4.20-1.4.0 | [Especificação da linguagem de modelo HTML](https://github.com/adobe/htl-spec) |
| Componentes principais do AEM | Versão 2.23.0 | [Componentes principais de WCM do AEM](https://github.com/adobe/aem-core-wcm-components) |
