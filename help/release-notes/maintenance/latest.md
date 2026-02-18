---
title: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: a58225edb8ca49db9743db6c9c5b08c786fa0144
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 13%

---


# Notas da versão de manutenção {#maintenance-release-notes}

A seção a seguir descreve as notas de versão técnicas para a versão de manutenção atual do Experience Manager as a Cloud Service.

## Versão 24464 {#release-24464}

Veja abaixo um resumo das melhorias contínuas da versão de manutenção 24464, lançada publicamente em quarta-feira, 17 de fevereiro de 2026. A versão de manutenção anterior era 24288.

A ativação de recursos do 2026.2.0 fornece o conjunto completo de recursos para esta versão de manutenção. Consulte o [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/pt-br/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obter mais informações.

### Aprimoramentos {#enhancements-24464}

* AEMARCH-264: adicionar suporte para validação de solicitações condicionais com base em RequestEntity.
* AEMARCH-269: Expor APIs de validação JavaEE para implementações de OpenAPI.
* AEMARCH-276: fornecer suporte a i18n por meio da RequestEntity.
* ASSETS-10995: Defina o limite no número de ativos no zip de download.
* ASSETS-50788: atualize a API de pesquisa para usar a API do GET de metadados de ativos.
* ASSETS-50946: Mapeie o corpo da solicitação usando a API do Metadata GET para metadados JCR.
* ASSETS-55866: Evite enviar uma nova solicitação para o mesmo ativo até que o processamento anterior seja concluído.
* ASSETS-60300: forneça a API para recuperar o contexto e o resultado do trabalho assíncrono.
* ASSETS-60574: Adicionar suporte para a versão mais recente do pacote da API do Sling.
* ASSETS-61049: Continuar o desenvolvimento do pacote do gerenciador de metadados.
* ASSETS-61692: Execute a pesquisa semântica por padrão na API aberta de pesquisa.
* ASSETS-61696: Rota do BAM e invólucro do MFE na exibição de ativos.
* ASSETS-61854: Enviar a solução GenStudio na mensagem de ativação/desativação.
* ASSETS-61973: Criar API no AEM para gerenciar prompts.
* ASSETS-62182: manipulador de eventos do Asset Compute para representação c2pa-manifest.
* ASSETS-62311: problemas de regressão de pesquisa.
* ASSETS-62413: adicionar suporte para o campo customModifier em cada camada no JSON.
* ASSETS-62432: API de exclusão da pasta de mesclagem PR.
* ASSETS-62540: aumente a versão otimizada para ui-touch no quickstart.
* ASSETS-62622: Manipular o modo de pesquisa em MatchQuery.
* ASSETS-62671: Corrigir o operador startsWith de MatchQuery.
* ASSETS-62780: Adicionar alternância de recurso para a API da pasta.
* ASSETS-62988: oculta a exibição da representação do manifesto c2pa na guia representações.
* ASSETS-63336: a sincronização de modelo do AEM para o DM só deve ocorrer para metadados com namespace dam.
* ASSETS-63375: Ativar o upload de ativos usando OpenAPIs experimentais.
* ASSETS-63453: verifique se todos os usuários podem ler a configuração omnisearch.
* GRANITE-63744: permitir a conexão de trabalhos assíncronos a trabalhos do sling.
* GRANITE-64567: desative automaticamente a pesquisa semântica para pesquisas de SKU.
* GUIDES-41187: Adicionar cabeçalhos para uso do Guides.
* SITES-30452: API de conteúdo com ASO - sugestões de título e descrição.
* SITES-33116: corrija a validação de caminho.
* SITES-34234: editor de páginas: preservar estado da árvore de conteúdo.

### Problemas corrigidos {#fixed-issues-24464}

* ASSETS-43198: os emails de notificação de expiração de ativo não respeitam a preferência de idioma do usuário.
* ASSETS-51840: melhorias no processamento de ativos.
* ASSETS-52061: não é possível navegar de volta após selecionar a pesquisa salva.
* ASSETS-53155: melhorias no conteúdo do ativo.
* ASSETS-53745: o fluxo de download do Dynamic Media requer o cancelamento da seleção do ativo original antes de escolher a predefinição da Web.
* ASSETS-54260: correções de conteúdo de ativos.
* ASSETS-54787: Melhorias no conteúdo do ativo.
* ASSETS-57391: atualizações de conteúdo de ativos.
* ASSETS-59213: cq-dynamicmedia-core depende da biblioteca commons-lang obsoleta.
* ASSETS-59214: cq-scene7-imaging depende da biblioteca commons-lang obsoleta.
* ASSETS-59546: cq-remotedam-client-core depende da biblioteca commons-lang obsoleta.
* ASSETS-59703: cq-dam-core depende da biblioteca commons-lang obsoleta.
* ASSETS-59705: cq-dam-handler depende da biblioteca commons-lang obsoleta.
* ASSETS-59707: cq-dam-indesign depende da biblioteca commons-lang obsoleta.
* ASSETS-59709: cq-scene7-core depende da biblioteca commons-lang obsoleta.
* ASSETS-59929: o CSV da exportação de metadados é interrompido quando o campo tem caractere de nova linha.
* ASSETS-60241: falha no trabalho de movimentação assíncrono ao renomear a pasta.
* ASSETS-61134: remova as tags comparisonVersion dos arquivos pom.
* ASSETS-61309: a movimentação/cópia do fragmento de conteúdo não atualiza mais as referências internas.
* ASSETS-61730: o redirecionamento para o Acesso binário direto deve respeitar a codificação do ativo.
* ASSETS-62358: o CSV de relatório do Assets mostra valores corrompidos no caminho do conteúdo.
* ASSETS-62610: botão de licença do Adobe Stock desativado na interface do usuário do Assets.
* ASSETS-62613: NPE em `downloadasset`/`saveas`.
* ASSETS-62656: Indicador de Pesquisa com IA Omnisearch mostrado incorretamente para pesquisas que não são da Assets.
* GRANITE-55387: a correção da palavra entre aspas exclui a palavra inteira.
* GRANITE-61240: RCE via XSS armazenado em lazycontainer.js.
* GRANITE-64101: índices OOTB convertidos em ES revertidos para Lucene ao reiniciar.
* SITES-24530: destino de toque de botões de fechar/remover no modal de pesquisa não é grande o suficiente.
* SITES-31425: mensagem de erro não localizada no fluxo de trabalho inicial.

### Problemas conhecidos {#known-issues-24464}

Nenhum.

### Recursos e APIs obsoletos {#deprecated-24464}

Os recursos e APIs obsoletos e removidos do AEM as a Cloud Service estão detalhados no documento [Recursos e APIs obsoletos e removidos](/help/release-notes/deprecated-removed-features.md).

### Correções de segurança {#security-24464}

A AEM as a Cloud Service dedica-se a otimizar a segurança e o desempenho da sua plataforma. Esta versão de manutenção aborda 14 vulnerabilidades identificadas, reforçando nosso compromisso com a proteção robusta do sistema.

### Tecnologias integradas {#embedded-tech-24464}

| Tecnologia | Versão | Link |
|---|---|---|
| AEM Oak | 1.90.0 | [API do Oak 1.90.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.90.0/index.html) |
| API DO SLING DO AEM | 2.27.6 | [API Apache Sling API 2.27.6](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| HTL do AEM | 1.4.28-1.4.0 | [Especificação da linguagem de modelo HTML](https://github.com/adobe/htl-spec) |
| Apache HTTP Server | 2.4.65 | [Apache Httpd 2.4.65](https://apache.googlesource.com/httpd/+/refs/tags/2.4.65/CHANGES) |
| Componentes principais do AEM | 2.30.4 | [Componentes principais de WCM do AEM](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14 (padrão) | [Versões Node.js com suporte](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |

