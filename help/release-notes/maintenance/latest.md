---
title: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: fd0b8ca281f35a92876f3c31baa4e17884f23948
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 41%

---

# Notas da versão de manutenção {#maintenance-release-notes}

A seção a seguir descreve as notas de versão técnicas para a versão de manutenção atual do Experience Manager as a Cloud Service.

## Versão 12441 {#release-12441}

Veja abaixo um resumo das melhorias contínuas da versão de manutenção 12441, lançada publicamente em 27 de junho de 2023. Esta versão de manutenção é uma atualização da versão de manutenção anterior a 12255.

A Ativação de recursos 2023.7.0 fornecerá o conjunto completo de recursos para esta versão de manutenção. Consulte a [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=pt-BR) para obter mais informações.

### Aprimoramentos {#enhancements-12441}

- SITES-8769: Melhorar chamadas StyleImpl em ResponsiveGrid

### Problemas corrigidos {#fixed-issues-12441}

- Várias atualizações relacionadas à acessibilidade
- SITES-12688: Editor de páginas: operador lógico OU que não está funcionando corretamente na pesquisa do Localizador de ativos
- SITES-4951: Editor de páginas: a pesquisa de tags no editor de páginas não encontra subtags
- SITES-12465: Fragmentos de experiência: as teclas de seta não funcionam na caixa de diálogo do componente de Fragmento de experiência
- SITES-12893: Fragmentos de experiência: aplicar validação de referência circular para Fragmentos de experiência
- SITES-12715: Fragmentos de experiência: as configurações do serviço em nuvem aplicadas à pasta Fragmentos de experiência não persistem
- SITES-13097: Fragmentos de experiência: não é possível adicionar fragmentos de experiência a um projeto de tradução
- SITES-13165: GraphQL: restaura o comportamento padrão para a filtragem de valores nulos
- SITES-12577: Verificador de links: transformador não reescreve links intermitentemente
- SITES-13559: MSM: exceção &quot;Não é modificável&quot; lançada ao implantar o componente
- SITES-11757: MSM: herdar a configuração de implantação do Pai não é revertido para páginas filhas
- SITES-14073: Administrador de sites: o relatório CSV falha com 500 ao selecionar nenhuma propriedade para exportar

### Problemas conhecidos {#known-issues-12441}

Nenhum.

### Tecnologias integradas {#embedded-tech-12441}

| Tecnologia | Versão | Link |
|---|---|---|
| AEM OAK | 1.50-T20230405052634-f9df4aa | [API Oak 1.50.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.50.0/index.html) |
| API do Sling do AEM | Versão 2.27.0 | [API do Apache Sling 2.27.0](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| HTL do AEM | Versão 1.4.20-1.4.0 | [Especificação da linguagem de modelo HTML](https://github.com/adobe/htl-spec) |
| Componentes principais do AEM | Versão 2.23.0 | [Componentes principais de WCM do AEM](https://github.com/adobe/aem-core-wcm-components) |
