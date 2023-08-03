---
title: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: acaed9eed20e8134574fd326e23ac68130ac019b
workflow-type: tm+mt
source-wordcount: '981'
ht-degree: 11%

---

# Notas da versão de manutenção {#maintenance-release-notes}

A seção a seguir descreve as notas de versão técnicas para a versão de manutenção atual do Experience Manager as a Cloud Service.

## Versão 12874 {#release-12874}

Resumidos abaixo estão as melhorias contínuas da versão de manutenção 12874, que foi lançada publicamente em 2 de agosto de 2023. Esta versão de manutenção é uma atualização da versão de manutenção anterior: versão 12790.

A Ativação de recursos 2023.8.0 fornecerá o conjunto completo de recursos para esta versão de manutenção. Consulte a [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=pt-BR) para obter mais informações.

### Aprimoramentos {#enhancements-12874}

- Nova versão da definição de índice: `/oak:index/damAssetLucene-9`
- ASSETS-18351: Alternar para facetas inseguras - para melhorar o desempenho da pesquisa
- ASSETS-17896: remove os vetores de recursos do índice - pesquisa de similaridade com base em tags inteligentes
- ASSETS-8715: adiciona verificação nula / não nula para a propriedade &quot;jcr:content/metadata/dam:status&quot;
- GRANITE-45138: remove o índice de propriedade da propriedade de reforço dinâmico das tags previstas
- ASSETS-17614: adiciona a Scene7 ID como uma propriedade indexada (verificação nula e não verificação nula ativada)
- ASSETS-14516: adiciona propriedades da funcionalidade de Lixeira &quot;nova interface&quot; ao índice
- ASSETS-16270: adiciona a propriedade de título agrupado ao índice (para uso na classificação)
- ASSETS-24478: remova cinco propriedades potencialmente grandes do índice (com base na análise dos dados do índice do cliente)
- ASSETS-3383: adiciona uma tag adicional &quot;assetsOmnisearch&quot;

As versões do AEM 12874 e superiores contêm uma nova versão do índice damAssetLucene (damAssetLucene-9). Para fornecer a experiência de pesquisa mais responsiva, damAssetLucene-9 altera o comportamento da facetagem de resultados da Consulta do Oak para não avaliar mais o controle de acesso nas contagens de facetas retornadas pelo índice de pesquisa subjacente (referido como modo &quot;inseguro&quot;).

Dessa forma, é possível que os usuários sejam apresentados com valores de contagem de facetas que incluem ativos aos quais o usuário atual não tem acesso. Isso não permite que o usuário acesse, baixe ou leia esses ativos, nem permite que o usuário obtenha mais informações sobre a existência dos ativos.

Se o comportamento anterior for desejado, os clientes deverão seguir as etapas descritas em [Pesquisa e indexação de conteúdo](/help/operations/indexing.md) para criar uma versão personalizada do índice damAssetLucene-9 com o modo de faceta &quot;estatística&quot; anterior.

### Problemas corrigidos {#fixed-issues-12874}

- ASSETS-24379: melhorias feitas no ReplicateOnModifyListener.
- ASSETS-25794: correção de um problema com S7ConfigResolverImpl que fazia com que ele executasse uma consulta cara na inicialização.
- ASSETS-25473: correção de um erro em que a Opção de publicação rápida estava visível para usuários sem permissão de replicação.
- ASSETS-24803: solucionou uma vulnerabilidade XSS no recurso Visualizadores.
- ASSETS-25489: correção de um problema em que os cortes inteligentes estavam sendo baixados com o sufixo incorreto.
- ASSETS-25435: correção de um erro em que os campos WidthxHeight estavam ausentes no Download para representações dinâmicas
- ASSETS-25741: correção da ausência de um asterisco visual (`*`) para o campo de edição obrigatório &quot;largura&quot; na seção de guia &quot;Básico&quot;.
- ASSETS-25759: melhoria da visibilidade do foco em elementos suspensos nos modos em preto/branco de alto contraste.
- ASSETS-25749: corrigido o problema em que o foco não era movido para vários controles abaixo do vídeo ao navegar usando a guia do teclado, resultando na inacessibilidade deles.
- ASSETS-26074: o limite de 127 caracteres foi restaurado para nomes de ativos que não são de vídeo.
- ASSETS-21428: correção de um problema em que um campo de várias linhas no Editor de esquema de metadados sobreporia o seguinte campo
- ASSETS-21989: correção de um problema que os cabeçalhos CORS podiam ser substituídos nas respostas 302 e 401, impedindo o logon remoto no DAM
- ASSETS-22603: problemas corrigidos que afetam nomes e valores de colunas ao exibir relatórios de download de ativos
- ASSETS-23120: correção de um problema no AssetSetLastModifiedProcess relacionado ao vazamento de resolvedores de recursos
- ASSETS-24938: correção de um problema que fazia com que o botão Salvar da caixa de diálogo Propriedades da pasta de ativos se comportasse como Salvar + Fechar
- ASSETS-25456: corrigido um problema em que um ativo com um nome longo impede o clique em ações no Editor de propriedades do ativo
- ASSETS-25832: correção de um problema com ativos relacionados de uma pasta de acesso completo para uma pasta de acesso somente leitura.
- ASSETS-25397: correção de um problema em que o novo nome de um ativo renomeado na nova interface do usuário não era refletido nos resultados da pesquisa
- ASSETS-26102: correção de um problema que impedia uploads do conector do Hub CI
- ASSETS-26172: tamanho reduzido do conteúdo do log de progresso da Importação em massa salvo nos nós de trabalho Sling persistentes
- ASSETS-26292: métodos createOrUpdateAsset() e createOrReplaceAsset() obsoletos no Java API
- ASSETS-26399: correção de um problema que impedia a publicação de coleções no Brand Portal
- ASSETS-26533: correção de um problema na integração do servidor do Indesign que poderia levar a um tempo limite para solicitações de processamento longas
- ASSETS-26549: correção de um problema na Exibição da lista de ativos que fazia com que &quot;Usuário externo&quot; fosse exibido como o último usuário modificado para todos os ativos carregados
- ASSETS-26551: resolução de um problema em que a publicação dos Ativos excluídos no autor não era desfeita
- ASSETS-26571: correção de um problema na página Relatórios de ativos em que a página não era carregada se vários trabalhos de relatório com falha estivessem presentes na lista
- ASSETS-26147: correção de um problema em que o Unified Shell tentava redirecionar um iframe para /ui quando window.top.opener está definido, mas não window.opener
- ASSETS-26576: correção de um problema com a Importação de Dropbox em que a hierarquia de pastas incorreta era criada
- ASSETS-26671: correção de um problema que impedia a Importação em massa de incluir arquivos localizados em uma pasta DCIM
- ASSETS-26700: correção de um problema em que salvar a página de propriedades de uma pasta pública sem alterações criaria três grupos desnecessários
- CQ-4353449: correção de um problema que permitia que usuários com permissões de marcação somente leitura criassem tags usando a interface de marcação
- GRANITE-46601: correção de um problema que impedia o SDK do Quickstart de iniciar no JDK 11.0.20
- SKYOPS-33168: Correção de um problema no Console do desenvolvedor do CM que impedia o carregamento de /content/dam para nomes de ativos sem extensão
- SKYOPS-61484: Correção de um problema no serviço RDEProvider que permitia que tokens ${sling.home} não substituídos persistissem em configurações OSGi mescladas
- Várias correções de segurança, acessibilidade e localização

### Problemas conhecidos {#known-issues-12874}

- GRANITE-46851: Testar conexão na distribuição de conteúdo não funciona

### Tecnologias integradas {#embedded-tech-12874}

| Tecnologia | Versão | Link |
|---|---|---|
| AEM OAK | 1.52-T20230629133256-25c01b8 | [API Oak 1.52.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.52.0/index.html) |
| API do Sling do AEM | Versão 2.27.2 | [API do Apache Sling 2.27.2](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| HTL do AEM | Versão 1.4.20-1.4.0 | [Especificação da linguagem de modelo HTML](https://github.com/adobe/htl-spec) |
| Componentes principais do AEM | Versão 2.23.0 | [Componentes principais de WCM do AEM](https://github.com/adobe/aem-core-wcm-components) |
