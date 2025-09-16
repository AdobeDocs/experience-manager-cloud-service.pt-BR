---
title: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: d73ccc454c89c7e06752de694af97ac26694be17
workflow-type: tm+mt
source-wordcount: '902'
ht-degree: 12%

---


# Notas da versão de manutenção {#maintenance-release-notes}

A seção a seguir descreve as notas de versão técnicas para a versão de manutenção atual do Experience Manager as a Cloud Service.

## Versão 22450 {#22450}

Veja abaixo um resumo das melhorias contínuas da versão de manutenção 22450, lançada publicamente em quarta-feira, 16 de setembro de 2025. A versão de manutenção anterior era 22171.

A ativação de recursos do 2025.9.0 fornecerá o conjunto completo de recursos para esta versão de manutenção. Consulte o [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obter mais informações.

### Novos recursos {#new-features-22450}

* SITES-32595: os fluxos de trabalho que terminam com fragmentos ignorados ou rejeitados agora podem ser identificados. Uma nova propriedade está disponível na resposta da API de fluxo de trabalho, listando fragmentos que foram excluídos por serem inválidos ou terem referências inválidas.
* SITES-33642: um novo evento de API agora é produzido e consumido para fragmentos de conteúdo modificados.
* SITES-33320: agora é possível pesquisar um Modelo de fragmento de conteúdo usando seu `technicalName` por meio da API de pesquisa.

### Aprimoramentos {#enhancements-22450}

* SITES-34023: o campo `technicalName` foi adicionado às respostas dos pontos de extremidade do Modelo de fragmento de conteúdo para melhor identificação.
* SITES-32766: as referências de ativos de conteúdo nos modelos de fragmento de conteúdo agora oferecem suporte a uma variedade maior de tipos de arquivos binários.
* SITES-33974: Melhoria na documentação da OpenAPI, tornando-a mais precisa e fácil de usar.
* SITES-9173: Cache `ContentPolicyStatus`.
* SITES-9290: Melhore o cache de `TouchEditContext`.
* SITES-33355: Abra um novo Editor de CF em &quot;View payload&quot; no console do workflow.
* SITES-33356: Abra um novo Editor de CF em Criar CF → Abrir na interface do Administrador da interface para toque.
* SITES-32952: Tratamento inconsistente de valores padrão para campos CFM ao usar a API de entrega.
* SITES-31539: Edge Delivery com Universal Editor: adicionar suporte para metatags de configuração do Universal Editor em `head.html`.
* SITES-20672: Edge Delivery com Universal Editor: adicione suporte para planilhas de metadados em massa adicionais na criação.
* SITES-32963: Edge Delivery com Universal Editor: adicione novos metadados de experimentação para direcionamento de otimização, alocação automática e autoaprendizado.
* SITES-30847: Componentes principais de versão 2.30.0.
* SITES-29617: O endpoint referencedBy foi atualizado para usar a classe ReferenceSearch, melhorando seu desempenho e confiabilidade.
* SITES-19308: aprimoramento do desempenho do processo de exclusão de páginas ao otimizar a etapa de validação de referência.
* SITES-34293: implementação de carregamento lento para recursos modelados para melhorar o desempenho.
* SITES-33892: adição de um botão de alternância de recurso para ignorar verificações de referência para pseudopáginas, o que pode melhorar o desempenho.

### Problemas corrigidos {#fixed-issues-22450}

* CQ-4360550: corrigido o desaparecimento inesperado de cópia de idioma após reverter a movimentação de página no AEM Cloud Service.
* SITES-25232: os links Definir data e Saída do Timewarp não têm um indicador de foco visível.
* SITES-25258: o foco não é gerenciado com a caixa de diálogo modal Excluir anotação.
* SITES-25305: a barra de ferramentas Demográfica não recebe foco em uma ordem lógica.
* SITES-25366: O estado de carregamento do modal do teaser não é anunciado pelo leitor de tela.
* SITES-34276: Edge Delivery com Universal Editor: correção da política CORS criada automaticamente não aplicada no nível de publicação.
* SITES-34811: Edge Delivery com Universal Editor: corrija se o seletor hlx não for adicionado aos links para planilhas na criação.
* SITES-31669: cadeias de caracteres não localizadas &quot;Esta página redireciona para&quot; em Ferramentas > Sites > Inicializações.
* SITES-30879: cadeias de caracteres não localizadas em Sites > Editor de páginas > Componente de pesquisa.
* SITES-30959: cadeias de caracteres não localizadas no Editor de páginas > Componente de imagem.
* SITES-21743: deslocalizado &quot;Selecione um documento a ser exibido&quot;. string no Editor de páginas > Visualizador do PDF
* SITES-19785: as cadeias de caracteres são deslocalizadas em Site dos componentes principais > Guias.
* SITES-22059: string &quot;Visualização de arquivo não disponível&quot; deslocalizada no site Componentes principais > Visualizador do PDF.
* SITES-33360: &quot;Erro durante a operação&quot; não localizado. O caminho fornecido não é uma sequência de caracteres de &quot;inicialização&quot; em Inicializações > Editar.
* SITES-32975: formato de data não localizado em interface do usuário headless > Inicializações > Comparar o Launch ao Source.
* SITES-32973: strings codificadas na interface do usuário headless > Inicializações > Rebase.
* SITES-13540: cadeias de caracteres não localizadas em Inicializações > Promoção.
* SITES-13085: cadeias de caracteres de erro não localizadas na página Sites > Criação de inicialização.
* SITES-21499: a cadeia de caracteres não localizada é Sites > Inicializações > Editar.
* SITES-14961: Truncamento do campo de data em Sites > Propriedades > Blueprint > Caixa de diálogo Implantação.
* SITES-33764: os filtros de inicialização (Caminho do Source/Inicializações criadas por fluxo de trabalho) não funcionam.
* SITES-33884: &quot;Promover página atual e subpáginas&quot; promove involuntariamente páginas fora do escopo.
* SITES-33611: a visão geral da Live Copy não funciona em mercados de alto volume.
* SITES-34331: tempo limite 503 ao carregar a sobreposição de implantação para usuários não administradores.
* SITES-34403: `NullPointerException` em `GraphqlClientImpl deactivate()` durante o encerramento.
* SITES-33817: resolução de problemas de sincronização entre o Esquema da interface do usuário e o modelo JCR para garantir consistência.
* SITES-31141: As referências de conteúdo que não são representadas por caminho agora são retornadas corretamente na resposta da API.
* SITES-34080: o processo de criação do fragmento de conteúdo agora é mais robusto e não falhará se nenhum campo for fornecido para a solicitação.
* SITES-30773: a expressão regular para encontrar palavras usando &quot;Localizar e substituir&quot; foi aprimorada para corresponder corretamente aos caracteres UTF-8.
* SITES-33742: correção de um erro que impedia a movimentação bem-sucedida de um fragmento de conteúdo ao usar a API de fluxo de trabalho.

### Problemas conhecidos {#known-issues-22450}

Nenhum.

### Recursos e APIs obsoletos {#deprecated-22450}

Os recursos e APIs obsoletos e removidos do AEM as a Cloud Service estão detalhados no documento [Recursos e APIs obsoletos e removidos](/help/release-notes/deprecated-removed-features.md).

### Correções de segurança {#security-22450}

A AEM as a Cloud Service dedica-se a otimizar a segurança e o desempenho da sua plataforma. Esta versão de manutenção aborda 18 vulnerabilidades identificadas, reforçando nosso compromisso com a proteção robusta do sistema.

### Tecnologias integradas {#embedded-tech-22450}

| Tecnologia | Versão | Link |
|---|---|---|
| AEM Oak | 1.84.0 | [API Oak API 1.84.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.84/index.html) |
| API DO SLING DO AEM | 2.27.6 | [API Apache Sling API 2.27.6](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| HTL do AEM | 1.4.28-1.4.0 | [Especificação da linguagem de modelo HTML](https://github.com/adobe/htl-spec) |
| Apache HTTP Server | 2.4.65 | [Apache Httpd 2.4.65](https://apache.googlesource.com/httpd/+/refs/tags/2.4.65/CHANGES) |
| Componentes principais do AEM | 2.29.0 | [Componentes principais de WCM do AEM](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14 (padrão) | [Versões Node.js com suporte](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |
