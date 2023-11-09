---
title: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: a8651a44300772b5c9706a5fd85e7fefef72e47d
workflow-type: tm+mt
source-wordcount: '1124'
ht-degree: 12%

---

# Notas da versão de manutenção {#maintenance-release-notes}

A seção a seguir descreve as notas de versão técnicas para a versão de manutenção atual do Experience Manager as a Cloud Service.

## Versão 14227 {#release-14227}

Veja abaixo um resumo das melhorias contínuas da versão de manutenção 14227, lançada publicamente em 9 de novembro de 2023. Esta versão de manutenção é uma atualização da versão de manutenção anterior: versão 14029. A versão de manutenção 14227 substitui 14157 para corrigir um problema.

A Ativação de recursos 2023.11.0 fornecerá o conjunto completo de recursos para esta versão de manutenção. Consulte o [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=pt-BR) para obter mais informações.

### Aprimoramentos {#enhancements-14227}

* ASSETS-29631: Assets Cloud: use dam:roles para entrega/pesquisa segura.
* CQ-4354515: Translations: opção para suprimir a tradução de recursos referenciados.
* FORMS-9993: Definir etapas para mover os Componentes principais do Forms para o Skyline.
* FORMS-10570: APIs EC integradas para API - Primeiro roteador.
* GRANITE-48143: atualize o Sling ResourceMerger para 1.4.4.
* SITES-14874: evento: expanda a árvore CFM para eventos de modelo e inclua alterações de metadados.
* SITES-2719: Fragmentos de conteúdo: Suporte à marcação para variações de fragmento de conteúdo (reativado).
* SITES-3619: Fragmentos de conteúdo: saída de tags de variação do GraphQL CF em JSON e filtragem por tag de variação (reativado).
* SITES-13750: fragmentos de conteúdo: exclua tags de um modelo de fragmento de conteúdo.
* SITES-13920: Fragmentos de conteúdo: suporte para a configuração minItems para vários campos (pré-lançamento).
* SITES-14080: Fragmentos de conteúdo: excluir tag de uma variação de Fragmento de conteúdo.
* SITES-14770: fragmentos de conteúdo: a variação do fragmento deve incluir a propriedade fieldTags.
* SITES-15356: Fragmentos de conteúdo: retorno de etag como cabeçalho de resposta quando um recurso é criado.
* SITES-15357: Fragmentos de conteúdo: permitem a publicação de fragmentos sem suas referências.
* SITES-15938: Fragmentos de conteúdo: metadados de referência de conteúdo ausentes.
* SITES-16078: fragmentos de conteúdo: preencha a propriedade do resultado de validação da variação quando um fragmento for buscado.
* SITES-16545: fragmentos de conteúdo: adicione um endpoint para recuperar as referências da variação de um fragmento de conteúdo.
* SITES-16853: Fragmentos de conteúdo: Remover /adobe/sites/cf/fragments/{fragmentId}/variation/{name}Ponto de extremidade /tags.

### Problemas corrigidos {#fixed-issues-14227}

* Correção de vários problemas de acessibilidade
* ASSETS-31015: não é possível carregar arquivos para Assets com extensões de arquivo desconhecidas.
* ASSETS-24739: Desative o Ponto de extremidade da ação personalizada Frame.io na publicação.
* CMGR-49845: Fluxo de retorno de conteúdo: problema na identificação do caminho raiz correto para determinado ponto de verificação.
* CMGR-49709: Fluxo de retorno de conteúdo: atualize o filtro de propriedade para ignorar propriedades adicionais.
* CQ-4354503: a configuração do Adobe IMS é removida aleatoriamente.
* CQ-4354414: ConfigurationReplicationEventHandler cria muitas ações de liberação individuais.
* CQ-4354401: Traduções: os ativos criados por projetos devem ser salvos antes de iniciar o processamento de ativos.
* CQ-4354430: Traduções: obtenção de um erro ao adicionar ativos que não fazem parte de uma estrutura de pastas de idioma a um projeto de tradução.
* CQ-4354412: Traduções: a exclusão do conteúdo da tarefa de tradução não exclui todo o conteúdo referenciado.
* CQ-4354636: Traduções: a criação de uma cópia de idioma no nível da raiz de idioma não ajusta caminhos na página.
* CQ-4354700: Workflows: a tela de carga do workflow não carrega.
* CQ-4354834: Workflows: não é possível adicionar comentário na tarefa da caixa de entrada do workflow.
* FORMS-11302: O título do componente editado no RTE é exibido incorretamente no Editor de formulários adaptáveis > Editor de regras.
* GRANITE-45706: falha na importação do i18n se o valor principal tiver — Äú).
* SITES-14156: evento: os eventos de publicação nem sempre são enviados.
* SITES-14520: GraphQL: desempenho incorreto com consultas graphql paginadas devido a FT_SITES-2719.
* SITES-16444: GraphQL: DataFetchingException para campos de mesmo nome ausentes na consulta do GraphQL.
* SITES-16225: GraphQL: os tipos de conteúdo dos campos de modelo e fragmento de RTE retornados pela API Java não estão corretos.
* SITES-15373: Fragmentos de conteúdo: O /adobe/sites/cf/fragments/{fragmentId}/variation/{name}O ponto de extremidade /tags não usa as convenções de nomenclatura de recursos corretas.
* SITES-15709: Fragmentos de conteúdo: problema de criação de ponto de extremidade de modelo ao criar um campo booleano.
* SITES-15727: Fragmentos de conteúdo: o campo do tipo &quot;Tag&quot; só pode ser adicionado uma vez no editor de modelo.
* SITES-15782: Fragmentos de conteúdo: propriedade exclusiva do modelo de campo do tipo Lista discriminada ausente.
* SITES-15786: fragmentos de conteúdo: o fragmento de conteúdo não pode ser criado em uma pasta que contém &#39;.
* SITES-15790: Fragmentos de conteúdo: Atualizar cabeçalho de local para criação de versão.
* SITES-15923: Fragmentos de conteúdo: o administrador do CF não mostra todas as pastas.
* SITES-15987: Fragmentos de conteúdo: Obter 500 ao criar uma variante.
* SITES-16067: Fragmentos de conteúdo: o tipo MIME do campo de fragmento de texto longo não pode ser modificado.
* SITES-16074: Fragmentos de conteúdo: campos de tag que não são String[] não pode ser recuperado do JCR.
* SITES-16079: Fragmentos de conteúdo: /fragments/{id}/references começou a retornar duplicatas.
* SITES-16118: Fragmentos de conteúdo: se um fragmento for corrigido e um campo de fragmento estiver ausente do modelo, uma exceção será lançada.
* SITES-16119: Fragmentos de conteúdo: se os metadados do fragmento contiverem campos não reconhecidos, uma exceção será lançada.
* SITES-16121: Fragmentos de conteúdo: a recuperação de um campo de data de modelo gera uma exceção.
* SITES-16123: Fragmentos de conteúdo: se um recurso não for um fragmento de conteúdo, o endpoint de obtenção de fragmentos acionará uma exceção.
* SITES-16208: Fragmentos de conteúdo: o ContentFragmentModelIdentifier expõe uma propriedade de título enganosa.
* SITES-16707: Fragmentos de conteúdo: os tipos de dados dos modelos de fragmento de conteúdo não são lidos corretamente.
* SITES-16818: fragmentos de conteúdo: execute a exclusão somente quando as tags estiverem presentes.
* SITES-16207: Fragmentos de conteúdo: a operação POST /adobe/sites/cf/models retorna dois códigos de status OK diferentes.
* SITES-15616: Fragmentos de conteúdo: o endpoint de publicação não publica, às vezes, todas as referências de um Fragmento de conteúdo.
* SITES-16027: Fragmentos de conteúdo: as informações de referência de variação estão ausentes da resposta do fragmento.
* SITES-16243: Fragmentos de conteúdo: localizar e substituir não funciona com campos que tenham Renderizar como: Vários.
* SITES-16250: Fragmentos de conteúdo: corrigir um CF às vezes retorna um cabeçalho etag incorreto.
* SITES-16686: Fragmentos de conteúdo: as referências sem fragmento do fragmento de conteúdo são serializadas quando a referência principal está na profundidade máxima.
* SITES-12880: Rastreamento rápido: corrigir a localização de Sites > Configurar o Analytics.
* SITES-16103: Fragmentos de experiência: as opções do Target não são exibidas em Cloud Service devido a um erro no console.
* SITES-16001: MSM: capacidade de excluir componentes de vários campos da configuração de implantação ao criar a Live Copy.
* SITES-16559: MSM: configurações de implantação removidas durante o processo de implantação para fragmentos de experiência.
* SITES-16797: MSM: corrigido Reativar a herança de um campo CF no editor.
* SITES-16273: Editor de páginas: erro ao copiar e colar nas páginas do aem sites da área de transferência.
* SITES-16126: Administrador do Sites: o desempenho de criação fica lento para usuários não administradores após o SITES-10288.
* FORMS-10534: Ocorre um erro no editor de regras ao selecionar a opção de operando booleano.
* FORMS-10248: em um formulário adaptável, quando o valor dos dados é do tipo Booleano, as regras não definem corretamente valores para botões de opção ou componentes de caixa de seleção.
* FORMS-11361: o componente suspenso assume automaticamente a seleção da primeira opção na lista.
* FORMS-11413: um erro relacionado ao serviço de preenchimento prévio do Forms Portal é acionado pelo Adaptive Forms, mesmo quando o serviço não está em uso.
* FORMS-11433: quando um componente não formulário é incluído em um Formulário adaptável, o processo de envio falha ao ser concluído.
* FORMS-11206: quando um usuário tenta agendar um fluxo de trabalho de Publicação para um Formulário adaptável, ele não funciona conforme esperado.
* FORMS-11546: o Lighthouse detectou um rótulo ARIA ausente para painéis repetidos em um Formulário adaptável, afetando a acessibilidade.
* FORMS-11095: o atributo ARIA é definido incorretamente para campos de número de telefone, endereço de email e número, resultando em problemas de acessibilidade.

### Problemas conhecidos {#known-issues-14227}

Nenhum.

### Tecnologias integradas {#embedded-tech-14227}

| Tecnologia | Versão | Link |
|---|---|---|
| AEM OAK | 1.56-T20230927085643-189caed | [API Oak API 1.56.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.56.0/index.html) |
| API DO SLING DO AEM | Versão 2.27.2 | [API Apache Sling API 2.27.2](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| HTL do AEM | Versão 1.4.20-1.4.0 | [Especificação da linguagem de modelo HTML](https://github.com/adobe/htl-spec) |
| Componentes principais do AEM | Versão 2.23.4 | [Componentes principais de WCM do AEM](https://github.com/adobe/aem-core-wcm-components) |
