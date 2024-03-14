---
title: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: d16d908d39df3c7d72dc48ac877c1543d2442416
workflow-type: tm+mt
source-wordcount: '1240'
ht-degree: 11%

---

# Notas da versão de manutenção {#maintenance-release-notes}

A seção a seguir descreve as notas de versão técnicas para a versão de manutenção atual do Experience Manager as a Cloud Service.

## Versão 15262 {#release-15262}

Veja abaixo um resumo das melhorias contínuas da versão de manutenção 15262, lançada publicamente em quinta-feira, 6 de março de 2024. A versão de manutenção anterior era a versão 14697.

A Ativação de recursos 2024.3.0 fornecerá o conjunto completo de recursos para esta versão de manutenção. Consulte o [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=pt-BR) para obter mais informações.

### Aprimoramentos {#enhancements-15262}

* ASSETS-30632: adição de uma coluna separada de status de publicação do Brand Portal na exibição em lista.
* ASSETS-30934: adição de suporte para `Iptc4xmpCore:AltTextAccessibility` e `Iptc4xmpCore:ExtDescrAccessibility` Propriedades do no Editor de metadados de ativos.
* ASSETS-31297: melhore as verificações para impedir a exclusão de ativos copiados da mídia dinâmica.
* ASSETS-33246: definição do índice de liberação `damAssetLucene-10`.
* ASSETS-33590: adicione suporte para representações da Web para vídeos em perfis de processamento.
* GRANITE-36205: atualização da versão do oak para 1.60-T20240131102219-0cde853.
* SITES-19326: Atualizar links na interface do usuário do Assets para abrir o CF no novo Editor de CF.
* GUIDES-12945: Sugestões inteligentes alimentadas por IA para adicionar referências de conteúdo ao criar conteúdo
* GUIDES-12706: Recurso de histórico de versão renovada no Editor da Web
* GUIDES-14948: Experiência do usuário aprimorada no painel Tradução
* GUIDES-8782: Lógica de pesquisa aprimorada na caixa de diálogo Inserir elemento
* GUIDES-14681: Capacidade de publicar várias predefinições de saída com linhas de base dinâmicas
* Para obter uma lista completa das melhorias nos Guias do AEM, consulte: [Novidades nos Guias do AEM](https://experienceleague.adobe.com/docs/experience-manager-guides/using/release-info/release-notes/cloud-release-notes/2024-releases/2402-release/whats-new-2024-2-0.html?lang=en#release-info)

### Problemas corrigidos {#fixed-issues-15262}

* ASSETS-15977: remova os eventos de pesquisa v1 obsoletos e o produtor de pipeline.
* ASSETS-18088: atualize as dependências da biblioteca batik para 1.17.
* ASSETS-21965: o fluxo de trabalho de writeback de metadados só deve ser iniciado em alterações de metadados de ativos.
* ASSETS-26368: os trabalhos de importação em massa agendados não são removidos se a configuração do trabalho não existir.
* ASSETS-26549: ativos/nós com &quot;jcr:lastModifiedBy&quot;: &quot;workflow-process-service&quot; são exibidos como &quot;usuário externo&quot; na exibição em lista.
* ASSETS-26842: atualize o texto &quot;Firefly&quot; para ler &quot;Construtor de aplicativos&quot; no perfil de processamento.
* ASSETS-28708: resposta muito lenta para algumas solicitações de token IMS.
* ASSETS-28767: estado de publicação inconsistente em ativos se a pasta contiver um número grande. de ativos publicados.
* ASSETS-29011: o recorte inteligente está visível para usuários somente leitura.
* ASSETS-29348: o AssetMoveEventHandler pode consumir muita memória.
* ASSETS-29738: a restrição de carregamento de ativos falha com NullPointerException para arquivos woff.
* ASSETS-30068: Importação em massa do Asset Essentials para incluir o status COMPLETED_WITH_ERROR para &quot;trabalho concluído, mas com erro&quot;.
* ASSETS-30261: imsUserId incorreto enviado ao pipeline para eventos de ativo.
* ASSETS-30538: a opção Exibir página está ausente após mover um arquivo PDF.
* ASSETS-30626: Falha ao criar solicitação de entrega relatada para ativos com assetId vazio.
* ATIVOS-30756: a ação do Assistente para mover ativos falha quando o nome da pasta termina em &#39;html&#39;.
* ASSETS-30810: limpe as tags antes de renderizar a configuração herdada do YouTube.
* ASSETS-31015: não é possível fazer upload de ativos com extensão de nome de arquivo .msg.
* ASSETS-31038: os eventos de tarefas recebidos pelo serviço de notificação não estão sendo processados.
* ASSETS-31097: desative a Cópia assíncrona para conteúdo WCM para evitar avisos de consulta de passagem.
* ASSETS-31256: ativos/nós com &quot;jcr:lastModifiedBy&quot;: &quot;workflow-process-service&quot; são exibidos como &quot;usuário externo&quot; na exibição em lista.
* ATIVOS-31260: o campo suspenso Formulário de metadados de ativo não está funcionando corretamente quando o JSON suspenso tem uma lista grande.
* ASSETS-31280: fazer com que os ativos sejam baixados em uma estrutura nivelada quando adicionados a uma coleção.
* ASSETS-31301: `dynamicmedia_sly.js` não pode ser instanciado corretamente pela API de uso.
* ASSETS-31330: ko_KR: cadeias de caracteres não localizadas em Legendas e faixas de áudio.
* ASSETS-31405: falha no processamento do servidor do InDesign para layouts de InDesigns grandes.
* ASSETS-31570: shell unificado - os detalhes do ativo &quot;Salvar e fechar&quot;, os botões &quot;Cancelar&quot; precisam ser pressionados mais de uma vez para funcionar.
* ASSETS-31673: falha na importação em massa para arquivos Dropbox grandes.
* ASSETS-32108: O AEM Assets não salva o tamanho do cartão definido pelo usuário nas configurações de exibição.
* ASSETS-32230: atualização da versão mínima de tempo de execução do pacote com.adobe.aem.repoapi.
* ASSETS-32544: o trabalho de exportação de metadados falha intermitentemente.
* ASSETS-32679: problemas de cache com visualizações de ativos (PDF).
* ASSETS-32754: as tarefas não podem ser atribuídas a usuários que não fizeram logon anteriormente.
* ASSETS-32755: configure o tópico de trabalho com/adobe/cq/dam/assetmove para usar uma fila ordenada.
* ASSETS-32899: a pesquisa dentro de Coleções é extremamente lenta.
* ASSETS-33098: os aspectos de pesquisa do AEM Assets &quot;Predicado de tags&quot; não funcionam conforme esperado.
* ASSETS-33454: atividade de Tarefa de revisão e comentários que não aparecem na Linha do tempo.
* ASSETS-34088: a visualização de PDF não está funcionando no AEM Assets.
* ASSETS-34155: Dynamic Media - Visualizadores de AEM atualizados / 2024.1.0.
* ASSETS-34684: lida com vários valores dc:title na árvore de conteúdo.
* ASSETS-34789: corrija problemas de normalização na verificação de conflito de nome de arquivo.
* DXML-13276: Guias AEM - integra índices no GraniteContent e os remove da biblioteca.
* GRANITE-47995: as operações de exclusão podem falhar devido a conflitos com a propriedade &quot;cq:isDelivered&quot;.
* GRANITE-48079: Ative solicitações POST para validação de token online OAuth.
* GRANITE-48143: Atualização do org.apache.sling.resourcemerger para 1.4.4.
* GRANITE-49031: atualização para Jackson 2.16.1.
* SCRNS-3961: Screens - Canal de sequência: a animação Jquery usada na transição Fade leva à tela preta.
* SITES-15868: melhore o desempenho para listar fragmentos.
* SITES-16079: `/fragments/{id}/references` começou a retornar duplicatas.
* SITES-16118: se um fragmento for corrigido e um campo de fragmento estiver ausente do modelo, uma exceção será lançada.
* SITES-16121: A recuperação de um campo de data de modelo gera uma exceção.
* SITES-16207: a operação POST /adobe/sites/cf/models retorna dois códigos de status OK diferentes.
* SITES-17361: incorpore novamente o Jsopa no pacote sites-headless.
* SITES-17768: GraphQL para produzir o URL do Dynamic Media para ativos referenciados em fragmentos de conteúdo.
* SKYOPS-66622: Falha no loop da implantação do autor após executar um pipeline habilitado para buildTransform.
* SKYOPS-69977: O Servlet de imagem adaptável não carrega a imagem após a atualização mais recente.
* GUIDES-15045: A verificação ortográfica no Editor não permite a seleção de sugestões.
* GUIDES-14968: O botão de navegação global não está funcionando e ocorre falha ao carregar o painel.
* GUIDES-14943: Na publicação de PDF nativo, os atributos personalizados nas predefinições de condição não estão funcionando para a publicação de PDF nativo.
* GUIDES-15085: Na publicação de PDF nativo, as referências principais não serão resolvidas na versão de dezembro de 2023 dos Guias do Adobe Experience Manager.
* GUIDES-13486: **Filtro de Linha de Base** Os arquivos não estão funcionando com o Nome do arquivo no Editor da Web.
* Para obter uma lista completa dos problemas corrigidos nos Guias do AEM, consulte: [Problemas corrigidos do AEM Guides](https://experienceleague.adobe.com/docs/experience-manager-guides/using/release-info/release-notes/cloud-release-notes/2024-releases/2402-release/fixed-issues-2024-2-0.html?lang=en#release-info)

### Problemas conhecidos {#known-issues-15262}

* ASSETS-35923: `UnsupportedClassVersionError` na etapa de build do pipeline CM após a atualização `aem-sdk-api` versão para `2024.2.15262.20240224T002940Z-231200`. **Exige ação do cliente para definir a versão do Java CM como 11**, consulte [Ambiente de compilação / Configuração da versão do JDK Maven](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/create-application-project/build-environment-details.html?lang=en#alternate-maven-jdk-version)
* ASSETS-35860: conversão de fuso horário incorreta na exibição em coluna do AEM Assets.
* SCRNS-4171: O Windows Screens fica em branco e deixa de funcionar ao atualizar para 15262 e publicar um canal.
* GRANITE-50774: GraniteContent deve usar a ordem determinística de valores de propriedade no momento da inicialização.

### Aviso de mudança {#change-notice-15262}

**Ações necessárias**

#### Defina a versão do Java CM para 11 {#set-java-version-11}

A nova versão do aem-sdk-api contém classes compiladas com um destino Java 11, que não é compatível com a versão 1.8 do JDK padrão do ambiente de compilação do Cloud Manager. Esta atualização requer que o Maven seja executado usando o JDK 11.

Os clientes são aconselhados a adicionar um `.cloudmanager/java-version` para a raiz do repositório Git com o conteúdo: `11`. [Ambiente de compilação / Configuração da versão do JDK Maven](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/create-application-project/build-environment-details.html?lang=en#alternate-maven-jdk-version)

#### Atualizar aem-cloud-testing-clients para 1.2.1 {#update-aem-cloud-testing-clients}

As próximas alterações exigirão a biblioteca [aem-cloud-testing-clients](https://github.com/adobe/aem-testing-clients) usado em seus testes funcionais personalizados para ser atualizado para pelo menos a versão **1.2.1**

Certifique-se de que sua dependência no `it.tests/pom.xml` foi atualizado.

```xml
<dependency>
   <groupId>com.adobe.cq</groupId>
   <artifactId>aem-cloud-testing-clients</artifactId>
   <version>1.2.1</version>
</dependency>
```

Essa alteração será necessária após 6 de abril de 2024.

Falha ao atualizar a biblioteca de dependências resultará em falhas de pipeline na etapa &quot;Teste funcional personalizado&quot;.

### Tecnologias integradas {#embedded-tech-15262}

| Tecnologia | Versão | Link |
|---|---|---|
| AEM OAK | 1.60-T20240131102219-0cde853 | [API Oak API 1.60.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.60.0/index.html) |
| API DO SLING DO AEM | Versão 2.27.2 | [API Apache Sling API 2.27.2](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| HTL do AEM | Versão 1.4.20-1.4.0 | [Especificação da linguagem de modelo HTML](https://github.com/adobe/htl-spec) |
| Componentes principais do AEM | Versão 2.23.4 | [Componentes principais de WCM do AEM](https://github.com/adobe/aem-core-wcm-components) |
