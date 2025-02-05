---
title: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 77d8ebeaa3914f4a91d2cf27ccc5b048e64d6b38
workflow-type: tm+mt
source-wordcount: '887'
ht-degree: 12%

---


# Notas da versão de manutenção {#maintenance-release-notes}

A seção a seguir descreve as notas de versão técnicas para a versão de manutenção atual do Experience Manager as a Cloud Service.

## Versão 19352 {#19352}

Veja abaixo um resumo das melhorias contínuas da versão de manutenção 19352, lançada publicamente em quinta-feira, 5 de fevereiro de 2025. A versão de manutenção anterior foi lançada em 19149.

A ativação de recursos do 2025.2.0 fornecerá o conjunto completo de recursos para esta versão de manutenção. Consulte o [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obter mais informações.

### Aprimoramentos {#enhancements-19352}

* FORMS-13998: adição do componente Acordeão.
* FORMS-17913: Adicionar variante de placas para grupo de rádio.
* FORMS-17333: Ativação de modelos de email HTML no envio do formulário AEM.
* FORMS-17702: Ativar os PDF gerados nas APIs de sincronização de saída para serem carregados no Armazenamento Azure Blob.
* SITES-28282: Edge Delivery com Universal Editor: forneça o caminho base, o nome do site e a organização como informações de página para qualquer página.
* SITES-27055: Edge Delivery com Universal Editor: suporte a parâmetros de consulta no servlet de proxy reverso.
* SITES-26796: Edge Delivery com Universal Editor: suporte a colunas personalizadas para a planilha Taxonomia.
* SITES-26087: Edge Delivery com Universal Editor: suporte à exportação de CSV para planilhas.
* SITES-26265: Edge Delivery com Universal Editor: exibir a conta TA para integrar ao Edge Delivery na interface do usuário de configuração.
* SITES-20372: Edge Delivery com Universal Editor: ativar casos de uso básicos do MSM para planilhas.
* SITES-26681: Edge Delivery com Universal Editor: suporte o parâmetro ?sheet= para as planilhas de Taxonomia no autor.
* SITES-26479: [Esquema] Ponto de Extremidade de Status de Publicação Agendada do Modelo Contents-Fragment.
* SITES-25944: [Visão geral da Live Copy] adicione o status &quot;live copy atualizado com herança limitada&quot;.
* SITES-28713: [V2] Adicione suporte a dados estruturados ao scraper de conteúdo.
* SITES-27896: abertura automática da Guia Comentários na notificação.
* SITES-26720: o usuário não deve ter permissão para selecionar uma coleção inteira do seletor de ativos.
* SITES-27875: torna qualquer item editável em um contêiner móvel por padrão.
* SITES-28340: Plug-in do serviço Dark Alley Universal Editor.
* SITES-26098: possibilidade de evitar a publicação de páginas referenciadas ao publicar um fragmento de conteúdo.
* SITES-27789: suporte do atributo de dados data-aue-component no DOM.
* SITES-25997: aumente as variações para suportar a data de modificação.
* SITES-28023: saída do GraphQL para referências de ativos remotos (repositório + ID do ativo).
* SITES-26058: endpoint do status de publicação agendada do modelo de fragmento de conteúdo.
* SITES-25108: Migração de modelo para referências UUID.
* SITES-26630: endpoint do status de publicação agendada do fragmento de conteúdo para vários fragmentos de conteúdo.
* SITES-23432: melhore o recurso de referências de exclusão.
* SITES-25797: suporte para referências de ativos externos - GraphQL.
* SITES-17514: exclua o aprimoramento do endpoint para desfazer a publicação de conteúdo-fragmento.
* SITES-14633: valide o modelo de conteúdo-fragmento para criar cargas antes de instalar o - Dry Run.

### Problemas corrigidos {#fixed-issues-19352}

* SITES-28415: Edge Delivery com Universal Editor: Corrigir propriedades abertas botão para planilhas.
* SITES-26669: Edge Delivery com Universal Editor: corrija problemas ao carregar arquivos CSV codificados em UTF-8 com uma BOM como planilha.
* SITES-26543: Edge Delivery com Universal Editor: corrija blocos vazios sem um modelo que renderize a marcação incorreta.
* SITES-26857: Edge Delivery com Universal Editor: corrija o token de autenticação do site que está visível na interface do usuário para configurações baseadas em arquivo.
* SITES-26662: Edge Delivery com Universal Editor: corrija problemas com metadados em massa que diferenciam maiúsculas de minúsculas.
* SITES-28133: o Publish para &quot;Pré-visualização&quot; está causando a disponibilização do conteúdo na produção.
* SITES-27187: ativação agendada de página/ativo, incluindo referências (experimental) que não publicam referências.
* SITES-27264: 2 testes Selenium relacionados a criação de LiveCopy e fragmento de conteúdo falham consistentemente no Principal.
* SITES-26559: Fixar consulta para modelos de Fragmento de conteúdo no índice cqPageLucene.
* SITES-24469: o elemento interativo não é acessível pelo teclado.
* SITES-24518: os botões Nome e Modelo na tabela Referência pai não são acessíveis pelo teclado.
* SITES-27937: as restrições UISchema são definidas como nulas após a atualização do modelo.
* SITES-27852: Categorizações ausentes no UISchema do modelo.
* SITES-27904: MetadataSchema ausente da lista/pesquisa Modelos de conteúdo-fragmento para projeção completa.
* SITES-26827: a listagem de fragmentos acaba em um loop infinito.
* SITES-27678: [Desempenho] Impede a busca desnecessária de _referências.
* SITES-27589: Falha de atualização de UUID para modelos de Fragmento de conteúdo com vários campos de referência de conteúdo/fragmento.
* SITES-26679: os modelos de fragmentos de conteúdo de cancelamento de publicação devem validar somente as referências publicadas.
* SITES-26666: referencesTree e endpoint de referências retornam com resultados diferentes.
* SITES-26499: ordem incorreta do valor do campo de tag em GET(s) e PATCH para tornar a ordem aleatória.
* SITES-26585: corrija o erro de descrição pequena no esquema.
* SITES-26647: a validação de referência Excluir endpoint e UnpublishFragments pode falhar para usuários não administradores.
* SITES-26458: [Pesquisar Modelo de Conteúdo-Fragmento] Corrija a filtragem por status de replicação.
* SITES-23513: [Editor de modelo de conteúdo-fragmento] Falha na validação da propriedade &quot;Referência de fragmento&quot; - &quot;Modelo de fragmento de conteúdo permitido&quot;.
* SITES-26575: o cancelamento da publicação de um fragmento da pré-visualização deve atualizar o previewStatus.
* SITES-26571: as referências de página não podem ser salvas quando FT_SITES-12435 está habilitado.
* SITES-26660: a comparação de versão do fragmento de conteúdo pode ser interrompida quando @ContentType é do tipo &quot;string&quot;.
* SITES-26626: customErrorMessage ausente em campos numéricos e booleanos.
* SITES-26268: Código de status incorreto retornado se uma referência for inválida ao criar um fragmento.

### Problemas conhecidos {#known-issues-19352}

Nenhum.

### Recursos e APIs obsoletos {#deprecated-19352}

Os recursos e APIs obsoletos e removidos do AEM as a Cloud Service estão detalhados no documento [Recursos e APIs obsoletos e removidos](/help/release-notes/deprecated-removed-features.md).

### Correções de segurança {#security-19352}

A AEM as a Cloud Service dedica-se a otimizar a segurança e o desempenho da sua plataforma. Esta versão de manutenção aborda 36 vulnerabilidades identificadas, reforçando nosso compromisso com a proteção robusta do sistema.

### Tecnologias integradas {#embedded-tech-19352}

| Tecnologia | Versão | Link |
|---|---|---|
| AEM Oak | 1.72.0 | [API Oak API 1.72.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.72.0/index.html) |
| API DO SLING DO AEM | 2.27.6 | [API Apache Sling API 2.27.6](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| HTL do AEM | 1.4.24-1.4.0 | [Especificação da linguagem de modelo HTML](https://github.com/adobe/htl-spec) |
| Componentes principais do AEM | 2.27.0 | [Componentes principais de WCM do AEM](https://github.com/adobe/aem-core-wcm-components) |
